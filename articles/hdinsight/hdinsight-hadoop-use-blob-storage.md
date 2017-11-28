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
# <a name="use-azure-storage-with-azure-hdinsight-clusters"></a><span data-ttu-id="a9224-104">Usare una risorsa di archiviazione di Azure con cluster Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="a9224-104">Use Azure storage with Azure HDInsight clusters</span></span>

<span data-ttu-id="a9224-105">dati tooanalyze nel cluster HDInsight, è possibile archiviare dati hello in archiviazione di Azure, archivio Azure Data Lake o entrambi.</span><span class="sxs-lookup"><span data-stu-id="a9224-105">tooanalyze data in HDInsight cluster, you can store hello data either in Azure Storage, Azure Data Lake Store, or both.</span></span> <span data-ttu-id="a9224-106">Entrambe le opzioni di archiviazione consentono di eliminare il toosafely che cluster HDInsight vengono utilizzate per il calcolo senza perdita di dati utente.</span><span class="sxs-lookup"><span data-stu-id="a9224-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="a9224-107">Hadoop supporta una nozione di file system predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-107">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="a9224-108">file system predefinito Hello implica un schema predefinito e l'autorità.</span><span class="sxs-lookup"><span data-stu-id="a9224-108">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="a9224-109">Può anche essere percorsi relativi tooresolve utilizzato.</span><span class="sxs-lookup"><span data-stu-id="a9224-109">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="a9224-110">Durante il processo di creazione del cluster HDInsight hello, è possibile specificare un contenitore blob in archiviazione di Azure come file system predefinito hello o con HDInsight 3.5, è possibile selezionare l'archiviazione di Azure o archivio Azure Data Lake come sistema di file predefinito hello con alcune eccezioni.</span><span class="sxs-lookup"><span data-stu-id="a9224-110">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> <span data-ttu-id="a9224-111">Per il supporto di hello dell'utilizzo di archivio Data Lake come predefinite hello e collegato di archiviazione, vedere [disponibilità per il cluster HDInsight](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span><span class="sxs-lookup"><span data-stu-id="a9224-111">For hello supportability of using Data Lake Store as both hello default and linked storage, see [Availabilities for HDInsight cluster](./hdinsight-hadoop-use-data-lake-store.md#availabilities-for-hdinsight-clusters).</span></span>

<span data-ttu-id="a9224-112">Questo articolo illustra come usare Archiviazione di Azure con i cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9224-112">In this article, you learn how Azure Storage works with HDInsight clusters.</span></span> <span data-ttu-id="a9224-113">toolearn come archivio Data Lake funziona con i cluster HDInsight, vedere [archivio utilizzare Azure Data Lake con Azure HDInsight cluster](hdinsight-hadoop-use-data-lake-store.md).</span><span class="sxs-lookup"><span data-stu-id="a9224-113">toolearn how Data Lake Store works with HDInsight clusters, see [Use Azure Data Lake Store with Azure HDInsight clusters](hdinsight-hadoop-use-data-lake-store.md).</span></span> <span data-ttu-id="a9224-114">Per altre informazioni sulla creazione di un cluster HDInsight, vedere [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a9224-114">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

<span data-ttu-id="a9224-115">Archiviazione di Azure è una soluzione di archiviazione affidabile, con finalità generali che si integra facilmente con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9224-115">Azure storage is a robust, general-purpose storage solution that integrates seamlessly with HDInsight.</span></span> <span data-ttu-id="a9224-116">HDInsight può utilizzare un contenitore blob in archiviazione di Azure come file system predefinito hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-116">HDInsight can use a blob container in Azure Storage as hello default file system for hello cluster.</span></span> <span data-ttu-id="a9224-117">Attraverso un'interfaccia di Hadoop distributed file system (HDFS), set completo di hello dei componenti in HDInsight possibile utilizzare direttamente dati strutturati o archiviati come BLOB.</span><span class="sxs-lookup"><span data-stu-id="a9224-117">Through a Hadoop distributed file system (HDFS) interface, hello full set of components in HDInsight can operate directly on structured or unstructured data stored as blobs.</span></span>

> [!WARNING]
> <span data-ttu-id="a9224-118">Sono disponibili diverse opzioni per la creazione di un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9224-118">There are several options available when creating an Azure Storage account.</span></span> <span data-ttu-id="a9224-119">Hello nella tabella seguente vengono fornite informazioni su quali opzioni sono supportate con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a9224-119">hello following table provides information on what options are supported with HDInsight:</span></span>
> 
> | <span data-ttu-id="a9224-120">Tipo di account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a9224-120">Storage account type</span></span> | <span data-ttu-id="a9224-121">Livello di archiviazione</span><span class="sxs-lookup"><span data-stu-id="a9224-121">Storage tier</span></span> | <span data-ttu-id="a9224-122">Supportato con HDInsight</span><span class="sxs-lookup"><span data-stu-id="a9224-122">Supported with HDInsight</span></span> |
> | ------- | ------- | ------- |
> | <span data-ttu-id="a9224-123">Account di archiviazione di uso generico</span><span class="sxs-lookup"><span data-stu-id="a9224-123">General-purpose Storage Account</span></span> | <span data-ttu-id="a9224-124">Standard</span><span class="sxs-lookup"><span data-stu-id="a9224-124">Standard</span></span> | <span data-ttu-id="a9224-125">__Sì__</span><span class="sxs-lookup"><span data-stu-id="a9224-125">__Yes__</span></span> |
> | &nbsp; | <span data-ttu-id="a9224-126">Premium</span><span class="sxs-lookup"><span data-stu-id="a9224-126">Premium</span></span> | <span data-ttu-id="a9224-127">No</span><span class="sxs-lookup"><span data-stu-id="a9224-127">No</span></span> |
> | <span data-ttu-id="a9224-128">Account di archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="a9224-128">Blob Storage Account</span></span> | <span data-ttu-id="a9224-129">Accesso frequente</span><span class="sxs-lookup"><span data-stu-id="a9224-129">Hot</span></span> | <span data-ttu-id="a9224-130">No</span><span class="sxs-lookup"><span data-stu-id="a9224-130">No</span></span> |
> | &nbsp; | <span data-ttu-id="a9224-131">Accesso sporadico</span><span class="sxs-lookup"><span data-stu-id="a9224-131">Cool</span></span> | <span data-ttu-id="a9224-132">No</span><span class="sxs-lookup"><span data-stu-id="a9224-132">No</span></span> |

<span data-ttu-id="a9224-133">Non è consigliabile utilizzare contenitore blob di hello predefinito per l'archiviazione dei dati di business.</span><span class="sxs-lookup"><span data-stu-id="a9224-133">We do not recommend that you use hello default blob container for storing business data.</span></span> <span data-ttu-id="a9224-134">L'eliminazione di contenitore di blob predefinito hello dopo ogni tooreduce utilizzare costo di archiviazione è buona norma.</span><span class="sxs-lookup"><span data-stu-id="a9224-134">Deleting hello default blob container after each use tooreduce storage cost is a good practice.</span></span> <span data-ttu-id="a9224-135">Si noti che il contenitore predefinito hello contiene l'applicazione e del sistema log.</span><span class="sxs-lookup"><span data-stu-id="a9224-135">Note that hello default container contains application and system logs.</span></span> <span data-ttu-id="a9224-136">Verificare i registri di hello tooretrieve che prima di eliminare il contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-136">Make sure tooretrieve hello logs before deleting hello container.</span></span>

<span data-ttu-id="a9224-137">La condivisione di un contenitore BLOB tra più cluster non è supportata.</span><span class="sxs-lookup"><span data-stu-id="a9224-137">Sharing one blob container for multiple clusters is not supported.</span></span>

## <a name="hdinsight-storage-architecture"></a><span data-ttu-id="a9224-138">Architettura di archiviazione di HDInsight</span><span class="sxs-lookup"><span data-stu-id="a9224-138">HDInsight storage architecture</span></span>
<span data-ttu-id="a9224-139">Hello seguente diagramma fornisce una visualizzazione astratta dell'architettura di archiviazione di HDInsight dell'utilizzo di archiviazione di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="a9224-139">hello following diagram provides an abstract view of hello HDInsight storage architecture of using Azure Storage:</span></span>

<span data-ttu-id="a9224-140">![I cluster Hadoop utilizzano tooaccess HDFS API hello e archiviano dati strutturati nell'archiviazione Blob. ] (./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "Architettura di archiviazione di HDInsight")</span><span class="sxs-lookup"><span data-stu-id="a9224-140">![Hadoop clusters use hello HDFS API tooaccess and store structured and unstructured data in Blob storage.](./media/hdinsight-hadoop-use-blob-storage/HDI.WASB.Arch.png "HDInsight Storage Architecture")</span></span>

<span data-ttu-id="a9224-141">HDInsight fornisce accesso toohello distribuita file system locale associata toohello nodi di calcolo.</span><span class="sxs-lookup"><span data-stu-id="a9224-141">HDInsight provides access toohello distributed file system that is locally attached toohello compute nodes.</span></span> <span data-ttu-id="a9224-142">Questo file system è possibile accedere tramite hello completo URI, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="a9224-142">This file system can be accessed by using hello fully qualified URI, for example:</span></span>

    hdfs://<namenodehost>/<path>

<span data-ttu-id="a9224-143">Inoltre, HDInsight consente tooaccess i dati archiviati in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9224-143">In addition, HDInsight allows you tooaccess data that is stored in Azure Storage.</span></span> <span data-ttu-id="a9224-144">sintassi di Hello è:</span><span class="sxs-lookup"><span data-stu-id="a9224-144">hello syntax is:</span></span>

    wasb[s]://<containername>@<accountname>.blob.core.windows.net/<path>

<span data-ttu-id="a9224-145">Di seguito sono riportate alcune considerazioni sull'uso di un account di Archiviazione di Azure con i cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9224-145">Here are some considerations when using Azure Storage account with HDInsight clusters.</span></span>

* <span data-ttu-id="a9224-146">**Contenitori di account di archiviazione hello che sono connessi tooa cluster:** poiché hello nome e la chiave sono associati ai cluster hello durante la creazione, occorre BLOB toohello accesso completo in tali contenitori.</span><span class="sxs-lookup"><span data-stu-id="a9224-146">**Containers in hello storage accounts that are connected tooa cluster:** Because hello account name and key are associated with hello cluster during creation, you have full access toohello blobs in those containers.</span></span>

* <span data-ttu-id="a9224-147">**Contenitori pubblici o BLOB pubblici negli account di archiviazione che non sono connessi a cluster tooa:** sono presenti i BLOB di autorizzazione di sola lettura toohello nei contenitori hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-147">**Public containers or public blobs in storage accounts that are NOT connected tooa cluster:** You have read-only permission toohello blobs in hello containers.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="a9224-148">Contenitori pubblici consentono di tooget un elenco di tutti i blob che sono disponibili in tale contenitore e ottenere i metadati del contenitore.</span><span class="sxs-lookup"><span data-stu-id="a9224-148">Public containers allow you tooget a list of all blobs that are available in that container and get container metadata.</span></span> <span data-ttu-id="a9224-149">BLOB pubblici consentono di BLOB hello tooaccess solo se si conosce l'URL esatto hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-149">Public blobs allow you tooaccess hello blobs only if you know hello exact URL.</span></span> <span data-ttu-id="a9224-150">Per ulteriori informazioni, vedere <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">limitare l'accesso toocontainers e blob</a>.</span><span class="sxs-lookup"><span data-stu-id="a9224-150">For more information, see <a href="http://msdn.microsoft.com/library/windowsazure/dd179354.aspx">Restrict access toocontainers and blobs</a>.</span></span>
  > 
  > 
* <span data-ttu-id="a9224-151">**Contenitori privati negli account di archiviazione che non sono connessi a cluster tooa:** non è possibile accedere BLOB hello in contenitori di hello se non si definisce l'account di archiviazione hello quando si inviano processi WebHCat hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-151">**Private containers in storage accounts that are NOT connected tooa cluster:** You can't access hello blobs in hello containers unless you define hello storage account when you submit hello WebHCat jobs.</span></span> <span data-ttu-id="a9224-152">Questo concetto verrà spiegato più avanti nell'articolo.</span><span class="sxs-lookup"><span data-stu-id="a9224-152">This is explained later in this article.</span></span>

<span data-ttu-id="a9224-153">account di archiviazione Hello che sono definiti nel processo di creazione hello e le relative chiavi vengono archiviate in %HADOOP_HOME%/conf/core-site.xml nei nodi del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-153">hello storage accounts that are defined in hello creation process and their keys are stored in %HADOOP_HOME%/conf/core-site.xml on hello cluster nodes.</span></span> <span data-ttu-id="a9224-154">comportamento predefinito di Hello di HDInsight è definiti nel file core-Site.XML hello gli account di archiviazione di toouse hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-154">hello default behavior of HDInsight is toouse hello storage accounts defined in hello core-site.xml file.</span></span> <span data-ttu-id="a9224-155">È possibile modificare questa impostazione usando [Ambari](./hdinsight-hadoop-manage-ambari.md)</span><span class="sxs-lookup"><span data-stu-id="a9224-155">You can modify this setting using [Ambari](./hdinsight-hadoop-manage-ambari.md)</span></span>

<span data-ttu-id="a9224-156">Più processi WebHCat, inclusi Hive, MapReduce, lo streaming Hadoop e Pig, possono includere una descrizione degli account di archiviazione e dei metadati</span><span class="sxs-lookup"><span data-stu-id="a9224-156">Multiple WebHCat jobs, including Hive, MapReduce, Hadoop streaming, and Pig, can carry a description of storage accounts and metadata with them.</span></span> <span data-ttu-id="a9224-157">(questo è valido solo per Pig con account di archiviazione, non per i metadati). Per altre informazioni, vedere [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx) (Uso di un cluster HDInsight con account di archiviazione e metastore alternativi).</span><span class="sxs-lookup"><span data-stu-id="a9224-157">(This currently works for Pig with storage accounts, but not for metadata.) For more information, see [Using an HDInsight Cluster with Alternate Storage Accounts and Metastores](http://social.technet.microsoft.com/wiki/contents/articles/23256.using-an-hdinsight-cluster-with-alternate-storage-accounts-and-metastores.aspx).</span></span>

<span data-ttu-id="a9224-158">I BLOB possono essere usati per i dati strutturati e non strutturati.</span><span class="sxs-lookup"><span data-stu-id="a9224-158">Blobs can be used for structured and unstructured data.</span></span> <span data-ttu-id="a9224-159">I contenitori BLOB archiviano i dati come coppie chiave-valore e non esiste una gerarchia di directory.</span><span class="sxs-lookup"><span data-stu-id="a9224-159">Blob containers store data as key/value pairs, and there is no directory hierarchy.</span></span> <span data-ttu-id="a9224-160">Tuttavia, il carattere di barra hello (/) può essere utilizzato all'interno di hello toomake nome della chiave appare come se un file viene archiviato in una struttura di directory.</span><span class="sxs-lookup"><span data-stu-id="a9224-160">However hello slash character ( / ) can be used within hello key name toomake it appear as if a file is stored within a directory structure.</span></span> <span data-ttu-id="a9224-161">Ad esempio, la chiave di un BLOB potrebbe essere *input/log1.txt*.</span><span class="sxs-lookup"><span data-stu-id="a9224-161">For example, a blob's key may be *input/log1.txt*.</span></span> <span data-ttu-id="a9224-162">Non effettivo *input* directory esistente, ma a causa di toohello presenza del carattere di barra hello nel nome della chiave hello, con aspetto hello di un percorso di file.</span><span class="sxs-lookup"><span data-stu-id="a9224-162">No actual *input* directory exists, but due toohello presence of hello slash character in hello key name, it has hello appearance of a file path.</span></span>

## <span data-ttu-id="a9224-163"><a id="benefits"></a>Vantaggi di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a9224-163"><a id="benefits"></a>Benefits of Azure Storage</span></span>
<span data-ttu-id="a9224-164">Hello implicita impatto sulle prestazioni del cluster di calcolo non condivisione della posizione e le risorse di archiviazione verrà attenuato modo hello cluster di calcolo hello vengono create le risorse di account di archiviazione toohello Chiudi interno hello regione di Azure, in cui la rete ad alta velocità hello rende efficiente per i nodi di calcolo hello tooaccess hello dati all'interno di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9224-164">hello implied performance cost of not co-locating compute clusters and storage resources is mitigated by hello way hello compute clusters are created close toohello storage account resources inside hello Azure region, where hello high-speed network makes it efficient for hello compute nodes tooaccess hello data inside Azure storage.</span></span>

<span data-ttu-id="a9224-165">Esistono numerosi vantaggi associati alla memorizzazione di dati hello in archiviazione di Azure anziché HDFS:</span><span class="sxs-lookup"><span data-stu-id="a9224-165">There are several benefits associated with storing hello data in Azure storage instead of HDFS:</span></span>

* <span data-ttu-id="a9224-166">**Riutilizzo di dati e la condivisione:** dati hello in HDFS si trovano all'interno di cluster di calcolo hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-166">**Data reuse and sharing:** hello data in HDFS is located inside hello compute cluster.</span></span> <span data-ttu-id="a9224-167">Solo le applicazioni che hanno accesso toohello hello di calcolo cluster è possibile utilizzare dati hello tramite API di HDFS.</span><span class="sxs-lookup"><span data-stu-id="a9224-167">Only hello applications that have access toohello compute cluster can use hello data by using HDFS APIs.</span></span> <span data-ttu-id="a9224-168">Hello dati nell'archiviazione di Azure sono accessibili tramite le API di HDFS hello o hello [API REST dell'archiviazione Blob][blob-storage-restAPI].</span><span class="sxs-lookup"><span data-stu-id="a9224-168">hello data in Azure storage can be accessed either through hello HDFS APIs or through hello [Blob Storage REST APIs][blob-storage-restAPI].</span></span> <span data-ttu-id="a9224-169">Di conseguenza, un set più ampio di applicazioni (inclusi altri cluster di HDInsight) e gli strumenti possono essere tooproduce utilizzato e utilizzare dati di hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-169">Thus, a larger set of applications (including other HDInsight clusters) and tools can be used tooproduce and consume hello data.</span></span>
* <span data-ttu-id="a9224-170">**Archiviazione dei dati:** l'archiviazione dei dati nell'archiviazione di Azure consente il cluster di HDInsight hello utilizzati per toobe calcolo eliminato in modo sicuro senza perdita di dati utente.</span><span class="sxs-lookup"><span data-stu-id="a9224-170">**Data archiving:** Storing data in Azure storage enables hello HDInsight clusters used for computation toobe safely deleted without losing user data.</span></span>
* <span data-ttu-id="a9224-171">**Il costo di archiviazione di dati:** l'archiviazione dei dati in DFS per a lungo termine hello è più costoso rispetto all'archiviazione hello in archiviazione di Azure perché costo hello di un cluster di calcolo è maggiore del costo di hello di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9224-171">**Data storage cost:** Storing data in DFS for hello long term is more costly than storing hello data in Azure storage because hello cost of a compute cluster is higher than hello cost of Azure storage.</span></span> <span data-ttu-id="a9224-172">Inoltre, poiché non devono di dati hello toobe ricaricato per la generazione di ogni cluster di calcolo, si sta salvando i costi di caricamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="a9224-172">In addition, because hello data does not have toobe reloaded for every compute cluster generation, you are also saving data loading costs.</span></span>
* <span data-ttu-id="a9224-173">**Scalabilità orizzontale elastica:** HDFS Sebbene fornisce un sistema di file di scalabilità orizzontale, scala hello è determinata dal numero di hello di nodi creato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="a9224-173">**Elastic scale-out:** Although HDFS provides you with a scaled-out file system, hello scale is determined by hello number of nodes that you create for your cluster.</span></span> <span data-ttu-id="a9224-174">Modifica scala hello può diventare una maggiore complessità del processo di affidarsi alla scalabilità di funzionalità che si ottengono automaticamente nell'archiviazione di Azure elastica di hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-174">Changing hello scale can become a more complicated process than relying on hello elastic scaling capabilities that you get automatically in Azure storage.</span></span>
* <span data-ttu-id="a9224-175">**Replica geografica:** è possibile eseguire la replica geografica di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9224-175">**Geo-replication:** Your Azure storage can be geo-replicated.</span></span> <span data-ttu-id="a9224-176">Sebbene in questo modo la ridondanza dei dati e ripristino geografico, un percorso di replica geografica toohello failover influisce negativamente sulle prestazioni e potrebbe comportare costi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="a9224-176">Although this gives you geographic recovery and data redundancy, a failover toohello geo-replicated location severely impacts your performance, and it may incur additional costs.</span></span> <span data-ttu-id="a9224-177">Pertanto, si consiglia di replica geografica hello toochoose cautela e solo se il valore di hello dei dati di hello vale la pena costi aggiuntivi hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-177">So our recommendation is toochoose hello geo-replication wisely and only if hello value of hello data is worth hello additional cost.</span></span>

<span data-ttu-id="a9224-178">Alcuni pacchetti e i processi MapReduce possono creare i risultati intermedi non è toostore nell'archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9224-178">Certain MapReduce jobs and packages may create intermediate results that you don't really want toostore in Azure storage.</span></span> <span data-ttu-id="a9224-179">In tale caso, è possibile scegliere dati hello toostore hello HDFS locale.</span><span class="sxs-lookup"><span data-stu-id="a9224-179">In that case, you can elect toostore hello data in hello local HDFS.</span></span> <span data-ttu-id="a9224-180">In effetti, HDInsight utilizza DFS per molti di questi risultati intermedi nei processi Hive e in altri processi.</span><span class="sxs-lookup"><span data-stu-id="a9224-180">In fact, HDInsight uses DFS for several of these intermediate results in Hive jobs and other processes.</span></span>

> [!NOTE]
> <span data-ttu-id="a9224-181">La maggior parte dei comandi HDFS, ad esempio <b>ls</b>, <b>copyFromLocal</b> e <b>mkdir</b>, funziona come previsto.</span><span class="sxs-lookup"><span data-stu-id="a9224-181">Most HDFS commands (for example, <b>ls</b>, <b>copyFromLocal</b> and <b>mkdir</b>) still work as expected.</span></span> <span data-ttu-id="a9224-182">Hello solo i comandi specifici toohello HDFS implementazione nativa (ovvero tooas cui DFS), ad esempio <b>fschk</b> e <b>dfsadmin</b>, Mostra un comportamento diverso in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9224-182">Only hello commands that are specific toohello native HDFS implementation (which is referred tooas DFS), such as <b>fschk</b> and <b>dfsadmin</b>, show different behavior in Azure storage.</span></span>
> 
> 

## <a name="create-blob-containers"></a><span data-ttu-id="a9224-183">Creare dei contenitori BLOB</span><span class="sxs-lookup"><span data-stu-id="a9224-183">Create Blob containers</span></span>
<span data-ttu-id="a9224-184">toouse BLOB, creare innanzitutto un [account di archiviazione Azure][azure-storage-create].</span><span class="sxs-lookup"><span data-stu-id="a9224-184">toouse blobs, you first create an [Azure Storage account][azure-storage-create].</span></span> <span data-ttu-id="a9224-185">Come parte di questa operazione, specificare un'area di Azure in cui viene creato l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-185">As part of this, you specify an Azure region where hello storage account is created.</span></span> <span data-ttu-id="a9224-186">cluster Hello e account di archiviazione hello deve essere ospitati in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="a9224-186">hello cluster and hello storage account must be hosted in hello same region.</span></span> <span data-ttu-id="a9224-187">database di SQL Server metastore Hello Hive e Oozie metastore SQL Server database deve trovarsi in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="a9224-187">hello Hive metastore SQL Server database and Oozie metastore SQL Server database must also be located in hello same region.</span></span>

<span data-ttu-id="a9224-188">Ogni volta che viene eseguito, ogni blob che crei appartiene tooa contenitore nell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9224-188">Wherever it lives, each blob you create belongs tooa container in your Azure Storage account.</span></span> <span data-ttu-id="a9224-189">Può trattarsi di un contenitore BLOB esistente, creato all'esterno di HDInsight, oppure di un contenitore creato per un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9224-189">This container may be an existing blob that was created outside of HDInsight, or it may be a container that is created for an HDInsight cluster.</span></span>

<span data-ttu-id="a9224-190">contenitore di Blob predefinito Hello archivia informazioni specifiche del cluster, ad esempio i registri e cronologia dei processi.</span><span class="sxs-lookup"><span data-stu-id="a9224-190">hello default Blob container stores cluster-specific information such as job history and logs.</span></span> <span data-ttu-id="a9224-191">Non condividere un contenitore BLOB predefinito con più cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9224-191">Don't share a default Blob container with multiple HDInsight clusters.</span></span> <span data-ttu-id="a9224-192">Questa operazione potrebbe danneggiare la cronologia processo.</span><span class="sxs-lookup"><span data-stu-id="a9224-192">This might corrupt job history.</span></span> <span data-ttu-id="a9224-193">È consigliabile toouse un contenitore diverso per ogni cluster e inserire dati condivisa su un account di archiviazione collegato specificato nella distribuzione di tutti i cluster anziché come account di archiviazione predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-193">It is recommended toouse a different container for each cluster and put shared data on a linked storage account specified in deployment of all relevant clusters rather than hello default storage account.</span></span> <span data-ttu-id="a9224-194">Per altre informazioni sulla configurazione degli account di archiviazione collegati, vedere [Creare cluster HDInsight][hdinsight-creation].</span><span class="sxs-lookup"><span data-stu-id="a9224-194">For more information on configuring linked storage accounts, see [Create HDInsight clusters][hdinsight-creation].</span></span> <span data-ttu-id="a9224-195">È tuttavia possibile riutilizzare un contenitore di archiviazione predefinito dopo aver eliminato il cluster HDInsight originale di hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-195">However you can reuse a default storage container after hello original HDInsight cluster has been deleted.</span></span> <span data-ttu-id="a9224-196">Per i cluster HBase, è possibile mantenere effettivamente schema della tabella HBase hello e i dati creando un nuovo cluster HBase tramite contenitore di blob hello predefinito utilizzato da un cluster HBase che è stato eliminato.</span><span class="sxs-lookup"><span data-stu-id="a9224-196">For HBase clusters, you can actually retain hello HBase table schema and data by creating a new HBase cluster using hello default blob container that is used by an HBase cluster that has been deleted.</span></span>

[!INCLUDE [secure-transfer-enabled-storage-account](../../includes/hdinsight-secure-transfer.md)]

### <a name="use-hello-azure-portal"></a><span data-ttu-id="a9224-197">Utilizzare hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="a9224-197">Use hello Azure portal</span></span>
<span data-ttu-id="a9224-198">Quando si crea un cluster HDInsight da hello portale, è dettagli dell'account archiviazione tooprovide hello hello opzioni (come illustrato di seguito).</span><span class="sxs-lookup"><span data-stu-id="a9224-198">When creating an HDInsight cluster from hello Portal, you have hello options (as shown below) tooprovide hello storage account details.</span></span> <span data-ttu-id="a9224-199">È inoltre possibile specificare se si desidera un account di archiviazione aggiuntivo associato hello cluster e in tal caso, scegliere da un altro blob di archiviazione di Azure come spazio di archiviazione aggiuntivo hello o archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="a9224-199">You can also specify whether you want an additional storage account associated with hello cluster, and if so, choose from Data Lake Store or another Azure Storage blob as hello additional storage.</span></span>

![Origine dati della creazione di HDInsight Hadoop](./media/hdinsight-hadoop-use-blob-storage/hdinsight.provision.data.source.png)

> [!WARNING]
> <span data-ttu-id="a9224-201">Utilizzo di un account di archiviazione aggiuntivo in un percorso diverso da quello del cluster HDInsight hello non è supportato.</span><span class="sxs-lookup"><span data-stu-id="a9224-201">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>


### <a name="use-azure-powershell"></a><span data-ttu-id="a9224-202">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9224-202">Use Azure PowerShell</span></span>
<span data-ttu-id="a9224-203">Se si [installato e configurato Azure PowerShell][powershell-install], è possibile utilizzare hello seguente dal prompt dei comandi toocreate di hello Azure PowerShell, un account di archiviazione e un contenitore:</span><span class="sxs-lookup"><span data-stu-id="a9224-203">If you [installed and configured Azure PowerShell][powershell-install], you can use hello following from hello Azure PowerShell prompt toocreate a storage account and container:</span></span>

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

### <a name="use-azure-cli"></a><span data-ttu-id="a9224-204">Utilizzare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a9224-204">Use Azure CLI</span></span>

[!INCLUDE [use-latest-version](../../includes/hdinsight-use-latest-cli.md)]

<span data-ttu-id="a9224-205">Se dispone di [installato e configurato Azure CLI hello](../cli-install-nodejs.md), comando che segue hello possono essere utilizzati tooa account di archiviazione e contenitore.</span><span class="sxs-lookup"><span data-stu-id="a9224-205">If you have [installed and configured hello Azure CLI](../cli-install-nodejs.md), hello following command can be used tooa storage account and container.</span></span>

    azure storage account create <storageaccountname> --type LRS

> [!NOTE]
> <span data-ttu-id="a9224-206">Hello `--type` parametro indica come account di archiviazione hello è stata replicata.</span><span class="sxs-lookup"><span data-stu-id="a9224-206">hello `--type` parameter indicates how hello storage account is replicated.</span></span> <span data-ttu-id="a9224-207">Per altre informazioni, vedere [Replica di Archiviazione di Azure](../storage/storage-redundancy.md).</span><span class="sxs-lookup"><span data-stu-id="a9224-207">For more information, see [Azure Storage Replication](../storage/storage-redundancy.md).</span></span> <span data-ttu-id="a9224-208">Non usare ZRS in quanto ZRS non supporta BLOB di pagine, file, tabelle o code.</span><span class="sxs-lookup"><span data-stu-id="a9224-208">Don't use ZRS as ZRS doesn't support page blob, file, table, or queue.</span></span>
> 
> 

<span data-ttu-id="a9224-209">Si è richiesta toospecify hello area geografica che viene creato l'account di archiviazione di hello in.</span><span class="sxs-lookup"><span data-stu-id="a9224-209">You are prompted toospecify hello geographic region that hello storage account is created in.</span></span> <span data-ttu-id="a9224-210">È necessario creare account di archiviazione hello in hello stessa area che si prevede di creare il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9224-210">You should create hello storage account in hello same region that you plan on creating your HDInsight cluster.</span></span>

<span data-ttu-id="a9224-211">Una volta creato l'account di archiviazione hello, utilizzare hello chiavi dell'account di archiviazione hello tooretrieve comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a9224-211">Once hello storage account is created, use hello following command tooretrieve hello storage account keys:</span></span>

    azure storage account keys list <storageaccountname>

<span data-ttu-id="a9224-212">toocreate un contenitore, usare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a9224-212">toocreate a container, use hello following command:</span></span>

    azure storage container create <containername> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="address-files-in-azure-storage"></a><span data-ttu-id="a9224-213">Accedere ai file in Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="a9224-213">Address files in Azure storage</span></span>
<span data-ttu-id="a9224-214">schema URI Hello per accedere ai file nell'archiviazione di Azure da HDInsight è:</span><span class="sxs-lookup"><span data-stu-id="a9224-214">hello URI scheme for accessing files in Azure storage from HDInsight is:</span></span>

    wasb[s]://<BlobStorageContainerName>@<StorageAccountName>.blob.core.windows.net/<path>

<span data-ttu-id="a9224-215">schema URI Hello fornisce l'accesso non crittografata (con hello *wasb:* prefisso) e SSL crittografate di accesso (con *wasbs*).</span><span class="sxs-lookup"><span data-stu-id="a9224-215">hello URI scheme provides unencrypted access (with hello *wasb:* prefix) and SSL encrypted access (with *wasbs*).</span></span> <span data-ttu-id="a9224-216">Si consiglia di utilizzare *wasbs* laddove possibile, anche quando l'accesso ai dati che si trova all'interno di hello stessa area in Azure.</span><span class="sxs-lookup"><span data-stu-id="a9224-216">We recommend using *wasbs* wherever possible, even when accessing data that lives inside hello same region in Azure.</span></span>

<span data-ttu-id="a9224-217">Hello &lt;BlobStorageContainerName&gt; identifica hello nome del contenitore blob hello in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="a9224-217">hello &lt;BlobStorageContainerName&gt; identifies hello name of hello blob container in Azure storage.</span></span>
<span data-ttu-id="a9224-218">Hello &lt;StorageAccountName&gt; identifica il nome di account di archiviazione di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="a9224-218">hello &lt;StorageAccountName&gt; identifies hello Azure Storage account name.</span></span> <span data-ttu-id="a9224-219">È necessario specificare un nome di dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="a9224-219">A fully qualified domain name (FQDN) is required.</span></span>

<span data-ttu-id="a9224-220">Se non si specifica &lt;BlobStorageContainerName&gt; né &lt;StorageAccountName&gt; è stata specificata, viene utilizzato il file system di hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="a9224-220">If neither &lt;BlobStorageContainerName&gt; nor &lt;StorageAccountName&gt; has been specified, hello default file system is used.</span></span> <span data-ttu-id="a9224-221">Per i file hello nel file system di hello predefinito, è possibile utilizzare un percorso relativo o assoluto.</span><span class="sxs-lookup"><span data-stu-id="a9224-221">For hello files on hello default file system, you can use a relative path or an absolute path.</span></span> <span data-ttu-id="a9224-222">Ad esempio, hello *hadoop-mapreduce-examples.jar* file fornito con i cluster HDInsight può essere tooby cui viene fatto riferimento utilizzando uno dei seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="a9224-222">For example, hello *hadoop-mapreduce-examples.jar* file that comes with HDInsight clusters can be referred tooby using one of hello following:</span></span>

    wasb://mycontainer@myaccount.blob.core.windows.net/example/jars/hadoop-mapreduce-examples.jar
    wasb:///example/jars/hadoop-mapreduce-examples.jar
    /example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="a9224-223">nome del file Hello è <i>hadoop examples.jar</i> nel cluster di HDInsight versioni 2.1 e 1.6.</span><span class="sxs-lookup"><span data-stu-id="a9224-223">hello file name is <i>hadoop-examples.jar</i> in HDInsight versions 2.1 and 1.6 clusters.</span></span>
> 
> 

<span data-ttu-id="a9224-224">Hello &lt;percorso&gt; hello nome percorso HDFS file o directory.</span><span class="sxs-lookup"><span data-stu-id="a9224-224">hello &lt;path&gt; is hello file or directory HDFS path name.</span></span> <span data-ttu-id="a9224-225">Poiché i contenitori in Archiviazione di Azure sono semplicemente archivi chiave-valore, non esiste un vero file system gerarchico.</span><span class="sxs-lookup"><span data-stu-id="a9224-225">Because containers in Azure storage are simply key-value stores, there is no true hierarchical file system.</span></span> <span data-ttu-id="a9224-226">Un carattere barra ( / ) all'interno di una chiave BLOB viene interpretato come un separatore di directory.</span><span class="sxs-lookup"><span data-stu-id="a9224-226">A slash character ( / ) inside a blob key is interpreted as a directory separator.</span></span> <span data-ttu-id="a9224-227">Ad esempio, nome blob hello per *hadoop-mapreduce-examples.jar* è:</span><span class="sxs-lookup"><span data-stu-id="a9224-227">For example, hello blob name for *hadoop-mapreduce-examples.jar* is:</span></span>

    example/jars/hadoop-mapreduce-examples.jar

> [!NOTE]
> <span data-ttu-id="a9224-228">Quando si lavora con i BLOB all'esterno di HDInsight, la maggior parte delle utilità non riconosce il formato WASB hello e invece prevede un formato del percorso di base, ad esempio `example/jars/hadoop-mapreduce-examples.jar`.</span><span class="sxs-lookup"><span data-stu-id="a9224-228">When working with blobs outside of HDInsight, most utilities do not recognize hello WASB format and instead expect a basic path format, such as `example/jars/hadoop-mapreduce-examples.jar`.</span></span>
> 
> 

## <a name="access-blobs"></a><span data-ttu-id="a9224-229">Accedere ai BLOB</span><span class="sxs-lookup"><span data-stu-id="a9224-229">Access blobs</span></span> 


### <span data-ttu-id="a9224-230"><a name="access-blobs-using-azure-powershell"></a> Usare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9224-230"><a name="access-blobs-using-azure-powershell"></a> Use Azure PowerShell</span></span>
> [!NOTE]
> <span data-ttu-id="a9224-231">comandi Hello in questa sezione forniscono un esempio di base dell'utilizzo di PowerShell tooaccess dati archiviati nel BLOB.</span><span class="sxs-lookup"><span data-stu-id="a9224-231">hello commands in this section provide a basic example of using PowerShell tooaccess data stored in blobs.</span></span> <span data-ttu-id="a9224-232">Per un esempio più completo personalizzato per l'utilizzo di HDInsight, vedere hello [strumenti HDInsight](https://github.com/Blackmist/hdinsight-tools).</span><span class="sxs-lookup"><span data-stu-id="a9224-232">For a more full-featured example that is customized for working with HDInsight, see hello [HDInsight Tools](https://github.com/Blackmist/hdinsight-tools).</span></span>
> 
> 

<span data-ttu-id="a9224-233">Utilizzare hello comando toolist hello blob cmdlet seguenti:</span><span class="sxs-lookup"><span data-stu-id="a9224-233">Use hello following command toolist hello blob-related cmdlets:</span></span>

    Get-Command *blob*

![Elenco dei cmdlet PowerShell correlati al BLOB.][img-hdi-powershell-blobcommands]

#### <a name="upload-files"></a><span data-ttu-id="a9224-235">Caricare file</span><span class="sxs-lookup"><span data-stu-id="a9224-235">Upload files</span></span>
<span data-ttu-id="a9224-236">Vedere [caricare dati tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="a9224-236">See [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

#### <a name="download-files"></a><span data-ttu-id="a9224-237">Download dei file</span><span class="sxs-lookup"><span data-stu-id="a9224-237">Download files</span></span>
<span data-ttu-id="a9224-238">Hello lo script seguente consente di scaricare una cartella di blocco blob toohello corrente.</span><span class="sxs-lookup"><span data-stu-id="a9224-238">hello following script downloads a block blob toohello current folder.</span></span> <span data-ttu-id="a9224-239">Prima dell'esecuzione dello script hello, modificare hello tooa cartella in cui si dispone delle autorizzazioni di scrittura.</span><span class="sxs-lookup"><span data-stu-id="a9224-239">Before running hello script, change hello directory tooa folder where you have write permissions.</span></span>

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

<span data-ttu-id="a9224-240">Fornire nome gruppo di risorse hello e nome del cluster hello, è possibile utilizzare hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="a9224-240">Providing hello resource group name and hello cluster name, you can use hello following code:</span></span>

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


#### <a name="delete-files"></a><span data-ttu-id="a9224-241">Eliminare file</span><span class="sxs-lookup"><span data-stu-id="a9224-241">Delete files</span></span>
    Remove-AzureStorageBlob -Container $containerName -Context $storageContext -blob $blob

#### <a name="list-files"></a><span data-ttu-id="a9224-242">Elencare file</span><span class="sxs-lookup"><span data-stu-id="a9224-242">List files</span></span>
    Get-AzureStorageBlob -Container $containerName -Context $storageContext -prefix "example/data/"

#### <a name="run-hive-queries-using-an-undefined-storage-account"></a><span data-ttu-id="a9224-243">Esecuzione di query Hive utilizzando un account di archiviazione non definito</span><span class="sxs-lookup"><span data-stu-id="a9224-243">Run Hive queries using an undefined storage account</span></span>
<span data-ttu-id="a9224-244">Questo esempio mostra come toolist una cartella dall'account di archiviazione che non è definito durante hello creazione processo.</span><span class="sxs-lookup"><span data-stu-id="a9224-244">This example shows how toolist a folder from storage account that is not defined during hello creating process.</span></span>
<span data-ttu-id="a9224-245">$clusterName = "<HDInsightClusterName>"</span><span class="sxs-lookup"><span data-stu-id="a9224-245">$clusterName = "<HDInsightClusterName>"</span></span>

    $undefinedStorageAccount = "<UnboundedStorageAccountUnderTheSameSubscription>"
    $undefinedContainer = "<UnboundedBlobContainerAssociatedWithTheStorageAccount>"

    $undefinedStorageKey = Get-AzureStorageKey $undefinedStorageAccount | %{ $_.Primary }

    Use-AzureRmHDInsightCluster $clusterName

    $defines = @{}
    $defines.Add("fs.azure.account.key.$undefinedStorageAccount.blob.core.windows.net", $undefinedStorageKey)

    Invoke-AzureRmHDInsightHiveJob -Defines $defines -Query "dfs -ls wasb://$undefinedContainer@$undefinedStorageAccount.blob.core.windows.net/;"

### <a name="use-azure-cli"></a><span data-ttu-id="a9224-246">Utilizzare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="a9224-246">Use Azure CLI</span></span>
<span data-ttu-id="a9224-247">Utilizzare hello comandi toolist hello relativi blob dei comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a9224-247">Use hello following command toolist hello blob-related commands:</span></span>

    azure storage blob

<span data-ttu-id="a9224-248">**Esempio di utilizzo tooupload CLI di Azure un file**</span><span class="sxs-lookup"><span data-stu-id="a9224-248">**Example of using Azure CLI tooupload a file**</span></span>

    azure storage blob upload <sourcefilename> <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="a9224-249">**Esempio di utilizzo toodownload CLI di Azure un file**</span><span class="sxs-lookup"><span data-stu-id="a9224-249">**Example of using Azure CLI toodownload a file**</span></span>

    azure storage blob download <containername> <blobname> <destinationfilename> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="a9224-250">**Esempio di utilizzo toodelete CLI di Azure un file**</span><span class="sxs-lookup"><span data-stu-id="a9224-250">**Example of using Azure CLI toodelete a file**</span></span>

    azure storage blob delete <containername> <blobname> --account-name <storageaccountname> --account-key <storageaccountkey>

<span data-ttu-id="a9224-251">**Esempio di utilizzo dei file toolist CLI di Azure**</span><span class="sxs-lookup"><span data-stu-id="a9224-251">**Example of using Azure CLI toolist files**</span></span>

    azure storage blob list <containername> <blobname|prefix> --account-name <storageaccountname> --account-key <storageaccountkey>

## <a name="use-additional-storage-accounts"></a><span data-ttu-id="a9224-252">Usare account di archiviazione aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="a9224-252">Use additional storage accounts</span></span>

<span data-ttu-id="a9224-253">Durante la creazione di un cluster HDInsight, specificare l'account di archiviazione di Azure hello da tooassociate con esso.</span><span class="sxs-lookup"><span data-stu-id="a9224-253">While creating an HDInsight cluster, you specify hello Azure Storage account you want tooassociate with it.</span></span> <span data-ttu-id="a9224-254">In account di archiviazione toothis, è inoltre possibile aggiungere ulteriore spazio di archiviazione di account da hello stessa sottoscrizione di Azure o sottoscrizioni di Azure diversi durante il processo di creazione di hello o dopo aver creato un cluster.</span><span class="sxs-lookup"><span data-stu-id="a9224-254">In addition toothis storage account, you can add additional storage accounts from hello same Azure subscription or different Azure subscriptions during hello creation process or after a cluster has been created.</span></span> <span data-ttu-id="a9224-255">Per istruzioni sull'aggiunta di altri account di archiviazione, vedere [Creare cluster HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="a9224-255">For instructions about adding additional storage accounts, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!WARNING]
> <span data-ttu-id="a9224-256">Utilizzo di un account di archiviazione aggiuntivo in un percorso diverso da quello del cluster HDInsight hello non è supportato.</span><span class="sxs-lookup"><span data-stu-id="a9224-256">Using an additional storage account in a different location than hello HDInsight cluster is not supported.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a9224-257">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a9224-257">Next steps</span></span>
<span data-ttu-id="a9224-258">In questo articolo, si è appreso come toouse HDFS compatibile con archiviazione di Azure con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a9224-258">In this article, you learned how toouse HDFS-compatible Azure storage with HDInsight.</span></span> <span data-ttu-id="a9224-259">In questo modo si toobuild scalabili e a lungo termine, l'archiviazione di soluzioni di acquisizione dei dati e usare HDInsight toounlock hello informazioni all'interno di hello archiviato strutturate e i dati non strutturati.</span><span class="sxs-lookup"><span data-stu-id="a9224-259">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="a9224-260">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="a9224-260">For more information, see:</span></span>

* <span data-ttu-id="a9224-261">[Introduzione ad Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="a9224-261">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="a9224-262">Introduzione ad Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="a9224-262">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="a9224-263">[Caricare dati tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="a9224-263">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="a9224-264">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="a9224-264">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="a9224-265">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="a9224-265">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="a9224-266">[Utilizzo di firme di accesso condiviso archiviazione Azure toorestrict accesso toodata con HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="a9224-266">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
