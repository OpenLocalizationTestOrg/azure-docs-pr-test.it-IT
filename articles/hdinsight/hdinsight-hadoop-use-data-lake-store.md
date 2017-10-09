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
# <a name="use-data-lake-store-with-azure-hdinsight-clusters"></a><span data-ttu-id="47bf8-104">Usare Data Lake Store con cluster Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="47bf8-104">Use Data Lake Store with Azure HDInsight clusters</span></span>

<span data-ttu-id="47bf8-105">dati tooanalyze nel cluster HDInsight, è possibile archiviare dati hello sia in [di archiviazione di Azure](../storage/common/storage-introduction.md), [archivio Azure Data Lake](../data-lake-store/data-lake-store-overview.md), o entrambi.</span><span class="sxs-lookup"><span data-stu-id="47bf8-105">tooanalyze data in HDInsight cluster, you can store hello data either in [Azure Storage](../storage/common/storage-introduction.md), [Azure Data Lake Store](../data-lake-store/data-lake-store-overview.md), or both.</span></span> <span data-ttu-id="47bf8-106">Entrambe le opzioni di archiviazione consentono di eliminare il toosafely che cluster HDInsight vengono utilizzate per il calcolo senza perdita di dati utente.</span><span class="sxs-lookup"><span data-stu-id="47bf8-106">Both storage options enable you toosafely delete HDInsight clusters that are used for computation without losing user data.</span></span>

<span data-ttu-id="47bf8-107">Questo articolo illustra come usare Data Lake Store con i cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47bf8-107">In this article, you learn how Data Lake Store works with HDInsight clusters.</span></span> <span data-ttu-id="47bf8-108">toolearn come archiviazione di Azure funziona con i cluster HDInsight, vedere [cluster di archiviazione di Azure usare con Azure HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="47bf8-108">toolearn how Azure Storage works with HDInsight clusters, see [Use Azure Storage with Azure HDInsight clusters](hdinsight-hadoop-use-blob-storage.md).</span></span> <span data-ttu-id="47bf8-109">Per altre informazioni sulla creazione di un cluster HDInsight, vedere [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="47bf8-109">For more information about creating an HDInsight cluster, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

> [!NOTE]
> <span data-ttu-id="47bf8-110">L'accesso a Data Lake Store avviene sempre tramite un canale protetto, pertanto non è presente un nome di schema del file system `adls`.</span><span class="sxs-lookup"><span data-stu-id="47bf8-110">Data Lake Store is always accessed through a secure channel, so there is no `adls` filesystem scheme name.</span></span> <span data-ttu-id="47bf8-111">Viene usato sempre `adl`.</span><span class="sxs-lookup"><span data-stu-id="47bf8-111">You always use `adl`.</span></span>
> 
> 

## <a name="availabilities-for-hdinsight-clusters"></a><span data-ttu-id="47bf8-112">Disponibilità per i cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="47bf8-112">Availabilities for HDInsight clusters</span></span>

<span data-ttu-id="47bf8-113">Hadoop supporta una nozione di file system predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="47bf8-113">Hadoop supports a notion of hello default file system.</span></span> <span data-ttu-id="47bf8-114">file system predefinito Hello implica un schema predefinito e l'autorità.</span><span class="sxs-lookup"><span data-stu-id="47bf8-114">hello default file system implies a default scheme and authority.</span></span> <span data-ttu-id="47bf8-115">Può anche essere percorsi relativi tooresolve utilizzato.</span><span class="sxs-lookup"><span data-stu-id="47bf8-115">It can also be used tooresolve relative paths.</span></span> <span data-ttu-id="47bf8-116">Durante il processo di creazione del cluster HDInsight hello, è possibile specificare un contenitore blob in archiviazione di Azure come file system predefinito hello o con HDInsight 3.5 e versioni successive, è possibile selezionare l'archiviazione di Azure o archivio Azure Data Lake come sistema di file hello predefinito con un alcune eccezioni.</span><span class="sxs-lookup"><span data-stu-id="47bf8-116">During hello HDInsight cluster creation process, you can specify a blob container in Azure Storage as hello default file system, or with HDInsight 3.5 and newer versions, you can select either Azure Storage or Azure Data Lake Store as hello default files system with a few exceptions.</span></span> 

<span data-ttu-id="47bf8-117">I cluster HDInsight possono usare Data Lake Store in due modi:</span><span class="sxs-lookup"><span data-stu-id="47bf8-117">HDInsight clusters can use Data Lake Store in two ways:</span></span>

* <span data-ttu-id="47bf8-118">Come spazio di archiviazione predefinito hello</span><span class="sxs-lookup"><span data-stu-id="47bf8-118">As hello default storage</span></span>
* <span data-ttu-id="47bf8-119">Come risorsa di archiviazione aggiuntiva, con BLOB del servizio di archiviazione di Azure come risorsa predefinita.</span><span class="sxs-lookup"><span data-stu-id="47bf8-119">As additional storage, with Azure Storage Blob as default storage.</span></span>

<span data-ttu-id="47bf8-120">Al momento, solo alcuni hello HDInsight cluster tipi/versioni supportano l'utilizzo di archivio Data Lake come spazio di archiviazione predefinito e account di archiviazione aggiuntivi:</span><span class="sxs-lookup"><span data-stu-id="47bf8-120">As of now, only some of hello HDInsight cluster types/versions support using Data Lake Store as default storage and additional storage accounts:</span></span>

| <span data-ttu-id="47bf8-121">Tipo di cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="47bf8-121">HDInsight cluster type</span></span> | <span data-ttu-id="47bf8-122">Data Lake Store come risorsa di archiviazione predefinita</span><span class="sxs-lookup"><span data-stu-id="47bf8-122">Data Lake Store as default storage</span></span> | <span data-ttu-id="47bf8-123">Data Lake Store come risorsa di archiviazione aggiuntiva</span><span class="sxs-lookup"><span data-stu-id="47bf8-123">Data Lake Store as additional storage</span></span>| <span data-ttu-id="47bf8-124">Note</span><span class="sxs-lookup"><span data-stu-id="47bf8-124">Notes</span></span> |
|------------------------|------------------------------------|---------------------------------------|------|
| <span data-ttu-id="47bf8-125">HDInsight versione 3.6</span><span class="sxs-lookup"><span data-stu-id="47bf8-125">HDInsight version 3.6</span></span> | <span data-ttu-id="47bf8-126">Sì</span><span class="sxs-lookup"><span data-stu-id="47bf8-126">Yes</span></span> | <span data-ttu-id="47bf8-127">Sì</span><span class="sxs-lookup"><span data-stu-id="47bf8-127">Yes</span></span> | |
| <span data-ttu-id="47bf8-128">HDInsight versione 3.5</span><span class="sxs-lookup"><span data-stu-id="47bf8-128">HDInsight version 3.5</span></span> | <span data-ttu-id="47bf8-129">Sì</span><span class="sxs-lookup"><span data-stu-id="47bf8-129">Yes</span></span> | <span data-ttu-id="47bf8-130">Sì</span><span class="sxs-lookup"><span data-stu-id="47bf8-130">Yes</span></span> | <span data-ttu-id="47bf8-131">Con l'eccezione hello di HBase</span><span class="sxs-lookup"><span data-stu-id="47bf8-131">With hello exception of HBase</span></span>|
| <span data-ttu-id="47bf8-132">HDInsight versione 3.4</span><span class="sxs-lookup"><span data-stu-id="47bf8-132">HDInsight version 3.4</span></span> | <span data-ttu-id="47bf8-133">No</span><span class="sxs-lookup"><span data-stu-id="47bf8-133">No</span></span> | <span data-ttu-id="47bf8-134">Sì</span><span class="sxs-lookup"><span data-stu-id="47bf8-134">Yes</span></span> | |
| <span data-ttu-id="47bf8-135">HDInsight versione 3.3</span><span class="sxs-lookup"><span data-stu-id="47bf8-135">HDInsight version 3.3</span></span> | <span data-ttu-id="47bf8-136">No</span><span class="sxs-lookup"><span data-stu-id="47bf8-136">No</span></span> | <span data-ttu-id="47bf8-137">No</span><span class="sxs-lookup"><span data-stu-id="47bf8-137">No</span></span> | |
| <span data-ttu-id="47bf8-138">HDInsight versione 3.2</span><span class="sxs-lookup"><span data-stu-id="47bf8-138">HDInsight version 3.2</span></span> | <span data-ttu-id="47bf8-139">No</span><span class="sxs-lookup"><span data-stu-id="47bf8-139">No</span></span> | <span data-ttu-id="47bf8-140">Sì</span><span class="sxs-lookup"><span data-stu-id="47bf8-140">Yes</span></span> | |
| <span data-ttu-id="47bf8-141">HDInsight Premium (livello)</span><span class="sxs-lookup"><span data-stu-id="47bf8-141">HDInsight Premium (tier)</span></span>| <span data-ttu-id="47bf8-142">No</span><span class="sxs-lookup"><span data-stu-id="47bf8-142">No</span></span> | <span data-ttu-id="47bf8-143">No</span><span class="sxs-lookup"><span data-stu-id="47bf8-143">No</span></span> | |
| <span data-ttu-id="47bf8-144">Storm</span><span class="sxs-lookup"><span data-stu-id="47bf8-144">Storm</span></span> | | |<span data-ttu-id="47bf8-145">È possibile utilizzare i dati di archivio Data Lake toowrite da una topologia di Storm.</span><span class="sxs-lookup"><span data-stu-id="47bf8-145">You can use Data Lake Store toowrite data from a Storm topology.</span></span> <span data-ttu-id="47bf8-146">È anche possibile usare Data Lake Store per archiviare dati di riferimento che possono essere letti da una topologia Storm.</span><span class="sxs-lookup"><span data-stu-id="47bf8-146">You can also use Data Lake Store for reference data that can then be read by a Storm topology.</span></span>|

<span data-ttu-id="47bf8-147">Utilizzo archivio Data Lake come un account di archiviazione aggiuntive non influiscono sulle prestazioni o hello possibilità tooread o scrivere tooAzure archiviazione dal cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="47bf8-147">Using Data Lake Store as an additional storage account does not affect performance or hello ability tooread or write tooAzure storage from hello cluster.</span></span>


## <a name="use-data-lake-store-as-default-storage"></a><span data-ttu-id="47bf8-148">Usare Data Lake Store come risorsa di archiviazione predefinita</span><span class="sxs-lookup"><span data-stu-id="47bf8-148">Use Data Lake Store as default storage</span></span>

<span data-ttu-id="47bf8-149">Quando HDInsight viene distribuito con l'archivio Data Lake come spazio di archiviazione predefinito, vengono archiviati i file correlati al cluster hello in archivio Data Lake nella seguente posizione hello:</span><span class="sxs-lookup"><span data-stu-id="47bf8-149">When HDInsight is deployed with Data Lake Store as default storage, hello cluster-related files are stored in Data Lake Store in hello following location:</span></span>

    adl://mydatalakestore/<cluster_root_path>/

<span data-ttu-id="47bf8-150">dove `<cluster_root_path>` hello nome di una cartella in cui si crea in archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="47bf8-150">where `<cluster_root_path>` is hello name of a folder you create in Data Lake Store.</span></span> <span data-ttu-id="47bf8-151">Se si specifica un percorso radice per ogni cluster, è possibile utilizzare hello stesso account archivio Data Lake per più di un cluster.</span><span class="sxs-lookup"><span data-stu-id="47bf8-151">By specifying a root path for each cluster, you can use hello same Data Lake Store account for more than one cluster.</span></span> <span data-ttu-id="47bf8-152">Pertanto, è possibile disporre di una configurazione in cui:</span><span class="sxs-lookup"><span data-stu-id="47bf8-152">So, you can have a setup where:</span></span>

* <span data-ttu-id="47bf8-153">Cluster1 possibile utilizzare il percorso di hello`adl://mydatalakestore/cluster1storage`</span><span class="sxs-lookup"><span data-stu-id="47bf8-153">Cluster1 can use hello path `adl://mydatalakestore/cluster1storage`</span></span>
* <span data-ttu-id="47bf8-154">Cluster2 possibile utilizzare il percorso di hello`adl://mydatalakestore/cluster2storage`</span><span class="sxs-lookup"><span data-stu-id="47bf8-154">Cluster2 can use hello path `adl://mydatalakestore/cluster2storage`</span></span>

<span data-ttu-id="47bf8-155">Si noti che entrambi hello utilizzare cluster hello stesso account archivio Data Lake **mydatalakestore**.</span><span class="sxs-lookup"><span data-stu-id="47bf8-155">Notice that both hello clusters use hello same Data Lake Store account **mydatalakestore**.</span></span> <span data-ttu-id="47bf8-156">Ogni cluster dispone di accesso tooits proprietari filesystem radice nell'archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="47bf8-156">Each cluster has access tooits own root filesystem in Data Lake Store.</span></span> <span data-ttu-id="47bf8-157">Hello esperienza di distribuzione del portale di Azure in particolare viene richiesto un nome di cartella toouse come **/clusters/\<clustername >** per il percorso radice hello.</span><span class="sxs-lookup"><span data-stu-id="47bf8-157">hello Azure portal deployment experience in particular prompts you toouse a folder name such as **/clusters/\<clustername>** for hello root path.</span></span>

<span data-ttu-id="47bf8-158">toobe toouse in grado di un archivio Data Lake come spazio di archiviazione predefinito, è necessario concedere toohello di accesso dell'entità servizio hello seguenti percorsi:</span><span class="sxs-lookup"><span data-stu-id="47bf8-158">toobe able toouse a Data Lake Store as default storage, you must grant hello service principal access toohello following paths:</span></span>

- <span data-ttu-id="47bf8-159">radice di account archivio Data Lake Hello.</span><span class="sxs-lookup"><span data-stu-id="47bf8-159">hello Data Lake Store account root.</span></span>  <span data-ttu-id="47bf8-160">ad esempio adl://mydatalakestore/.</span><span class="sxs-lookup"><span data-stu-id="47bf8-160">For example: adl://mydatalakestore/.</span></span>
- <span data-ttu-id="47bf8-161">cartella Hello per tutte le cartelle di cluster.</span><span class="sxs-lookup"><span data-stu-id="47bf8-161">hello folder for all cluster folders.</span></span>  <span data-ttu-id="47bf8-162">ad esempio adl://mydatalakestore/clusters.</span><span class="sxs-lookup"><span data-stu-id="47bf8-162">For example: adl://mydatalakestore/clusters.</span></span>
- <span data-ttu-id="47bf8-163">cartella Hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="47bf8-163">hello folder for hello cluster.</span></span>  <span data-ttu-id="47bf8-164">ad esempio adl://mydatalakestore/clusters/cluster1storage.</span><span class="sxs-lookup"><span data-stu-id="47bf8-164">For example: adl://mydatalakestore/clusters/cluster1storage.</span></span>

<span data-ttu-id="47bf8-165">Per altre informazioni su come creare un'entità servizio e concedere l'accesso, vedere [Configurare l'accesso a Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="47bf8-165">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-data-lake-store-as-additional-storage"></a><span data-ttu-id="47bf8-166">Usare Data Lake Store come risorsa di archiviazione aggiuntiva</span><span class="sxs-lookup"><span data-stu-id="47bf8-166">Use Data Lake Store as additional storage</span></span>

<span data-ttu-id="47bf8-167">È possibile utilizzare l'archivio Data Lake come ulteriore spazio di archiviazione per cluster hello anche.</span><span class="sxs-lookup"><span data-stu-id="47bf8-167">You can use Data Lake Store as additional storage for hello cluster as well.</span></span> <span data-ttu-id="47bf8-168">In questi casi, spazio di archiviazione predefinito hello cluster può essere un Blob di archiviazione di Azure o un account archivio Data Lake.</span><span class="sxs-lookup"><span data-stu-id="47bf8-168">In such cases, hello cluster default storage can either be an Azure Storage Blob or a Data Lake Store account.</span></span> <span data-ttu-id="47bf8-169">Se si eseguono i processi di HDInsight sui dati hello archiviati nell'archivio Data Lake come ulteriore spazio di archiviazione, è necessario utilizzare i file toohello di hello percorso completo.</span><span class="sxs-lookup"><span data-stu-id="47bf8-169">If you are running HDInsight jobs against hello data stored in Data Lake Store as additional storage, you must use hello fully-qualified path toohello files.</span></span> <span data-ttu-id="47bf8-170">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="47bf8-170">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="47bf8-171">Si noti che non esiste alcun **cluster_root_path** nell'URL hello ora.</span><span class="sxs-lookup"><span data-stu-id="47bf8-171">Note that there's no **cluster_root_path** in hello URL now.</span></span> <span data-ttu-id="47bf8-172">Ciò avviene perché l'archivio Data Lake non è un archivio predefinito in questo caso è sufficiente toodo fornire hello percorso toohello file.</span><span class="sxs-lookup"><span data-stu-id="47bf8-172">That's because Data Lake Store is not a default storage in this case so all you need toodo is provide hello path toohello files.</span></span>

<span data-ttu-id="47bf8-173">toobe toouse in grado di un archivio Data Lake come ulteriore spazio di archiviazione, è necessario solo toogrant hello servizio principale toohello percorsi di accesso in cui sono archiviati i file.</span><span class="sxs-lookup"><span data-stu-id="47bf8-173">toobe able toouse a Data Lake Store as additional storage, you only need toogrant hello service principal access toohello paths where your files are stored.</span></span>  <span data-ttu-id="47bf8-174">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="47bf8-174">For example:</span></span>

    adl://mydatalakestore.azuredatalakestore.net/<file_path>

<span data-ttu-id="47bf8-175">Per altre informazioni su come creare un'entità servizio e concedere l'accesso, vedere [Configurare l'accesso a Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="47bf8-175">For more information for creating service principal and grant access, see [Configure Data Lake store access](#configure-data-lake-store-access).</span></span>


## <a name="use-more-than-one-data-lake-store-accounts"></a><span data-ttu-id="47bf8-176">Usare più di un account di Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47bf8-176">Use more than one Data Lake Store accounts</span></span>

<span data-ttu-id="47bf8-177">Aggiunta di un account archivio Data Lake come aggiuntive e più di un archivio Data Lake account vengono effettuati mediante l'assegnazione di autorizzazioni di cluster HDInsight hello del dati negli account archivio Data Lake di uno o più.</span><span class="sxs-lookup"><span data-stu-id="47bf8-177">Adding a Data Lake Store account as additional and adding more than one Data Lake Store accounts are accomplished by giving hello HDInsight cluster permission on data in one ore more Data Lake Store accounts.</span></span> <span data-ttu-id="47bf8-178">Vedere [Configurare l'accesso a Data Lake Store](#configure-data-lake-store-access).</span><span class="sxs-lookup"><span data-stu-id="47bf8-178">See [Configure Data Lake Store access](#configure-data-lake-store-access).</span></span>

## <a name="configure-data-lake-store-access"></a><span data-ttu-id="47bf8-179">Configurare l'accesso a Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47bf8-179">Configure Data Lake store access</span></span>

<span data-ttu-id="47bf8-180">tooconfigure accesso archivio Data Lake dal cluster HDInsight, è necessario disporre di un'entità servizio di Azure Active directory (Azure AD).</span><span class="sxs-lookup"><span data-stu-id="47bf8-180">tooconfigure Data Lake store access from your HDInsight cluster, you must have an Azure Active directory (Azure AD) service principal.</span></span> <span data-ttu-id="47bf8-181">Solo un amministratore di Azure AD può creare un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="47bf8-181">Only an Azure AD administrator can create a service principal.</span></span> <span data-ttu-id="47bf8-182">entità servizio Hello deve essere creata con un certificato.</span><span class="sxs-lookup"><span data-stu-id="47bf8-182">hello service principal must be created with a certificate.</span></span> <span data-ttu-id="47bf8-183">Per altre informazioni, vedere [Configurare l'accesso a Data Lake Store](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access) e [Creare un'entità servizio con certificato autofirmato](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span><span class="sxs-lookup"><span data-stu-id="47bf8-183">For more information, see [Configure Data Lake Store access](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md#configure-data-lake-store-access), and [Create service principal with self-signed-certificate](../azure-resource-manager/resource-group-authenticate-service-principal.md#create-service-principal-with-self-signed-certificate).</span></span>

> [!NOTE]
> <span data-ttu-id="47bf8-184">Se si intende archivio Azure Data Lake di toouse come spazio di archiviazione aggiuntivo per il cluster HDInsight, è consigliabile farlo durante la creazione di cluster hello come descritto in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="47bf8-184">If you are going toouse Azure Data Lake Store as additional storage for HDInsight cluster, we strongly recommend that you do this while you create hello cluster as described in this article.</span></span> <span data-ttu-id="47bf8-185">Aggiunta archivio Azure Data Lake come tooan ulteriore spazio di archiviazione cluster HDInsight esistente è una complessità del processo e soggetta a tooerrors.</span><span class="sxs-lookup"><span data-stu-id="47bf8-185">Adding Azure Data Lake Store as additional storage tooan existing HDInsight cluster is a complicated process and prone tooerrors.</span></span>
>

## <a name="access-files-from-hello-cluster"></a><span data-ttu-id="47bf8-186">Accedere ai file dal cluster hello</span><span class="sxs-lookup"><span data-stu-id="47bf8-186">Access files from hello cluster</span></span>

<span data-ttu-id="47bf8-187">Esistono diversi modi per accedere a file hello in archivio Data Lake da un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47bf8-187">There are several ways you can access hello files in Data Lake Store from an HDInsight cluster.</span></span>

* <span data-ttu-id="47bf8-188">**Usa il nome completo di hello**.</span><span class="sxs-lookup"><span data-stu-id="47bf8-188">**Using hello fully qualified name**.</span></span> <span data-ttu-id="47bf8-189">Con questo approccio, si fornita i file toohello percorso completo di hello che si desidera tooaccess.</span><span class="sxs-lookup"><span data-stu-id="47bf8-189">With this approach, you provide hello full path toohello file that you want tooaccess.</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/<file_path>

* <span data-ttu-id="47bf8-190">**Utilizzando il formato di percorso abbreviato hello**.</span><span class="sxs-lookup"><span data-stu-id="47bf8-190">**Using hello shortened path format**.</span></span> <span data-ttu-id="47bf8-191">Con questo approccio, è sostituire percorso hello backup principale del cluster toohello adl: / / /.</span><span class="sxs-lookup"><span data-stu-id="47bf8-191">With this approach, you replace hello path up toohello cluster root with adl:///.</span></span> <span data-ttu-id="47bf8-192">Nell'esempio hello sopra, in tal caso, è possibile sostituire `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` con `adl:///`.</span><span class="sxs-lookup"><span data-stu-id="47bf8-192">So, in hello example above, you can replace `adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/` with `adl:///`.</span></span>

        adl:///<file path>

* <span data-ttu-id="47bf8-193">**Percorso relativo hello utilizzando**.</span><span class="sxs-lookup"><span data-stu-id="47bf8-193">**Using hello relative path**.</span></span> <span data-ttu-id="47bf8-194">Con questo approccio, si fornisce solo hello relativo percorso toohello file che si desidera tooaccess.</span><span class="sxs-lookup"><span data-stu-id="47bf8-194">With this approach, you only provide hello relative path toohello file that you want tooaccess.</span></span> <span data-ttu-id="47bf8-195">Ad esempio, se hello file toohello percorso completo è:</span><span class="sxs-lookup"><span data-stu-id="47bf8-195">For example, if hello complete path toohello file is:</span></span>

        adl://mydatalakestore.azuredatalakestore.net/<cluster_root_path>/example/data/sample.log

    <span data-ttu-id="47bf8-196">È possibile accedere hello stesso file sample.log usando invece il percorso relativo.</span><span class="sxs-lookup"><span data-stu-id="47bf8-196">You can access hello same sample.log file by using this relative path instead.</span></span>

        /example/data/sample.log

## <a name="create-hdinsight-clusters-with-access-toodata-lake-store"></a><span data-ttu-id="47bf8-197">Creare cluster HDInsight con accesso tooData Lake archivio</span><span class="sxs-lookup"><span data-stu-id="47bf8-197">Create HDInsight clusters with access tooData Lake Store</span></span>

<span data-ttu-id="47bf8-198">Utilizzare i seguenti collegamenti per informazioni dettagliate su come cluster di HDInsight con toocreate accedere archivio Lake tooData hello.</span><span class="sxs-lookup"><span data-stu-id="47bf8-198">Use hello following links for detailed instructions on how toocreate HDInsight clusters with access tooData Lake Store.</span></span>

* [<span data-ttu-id="47bf8-199">Uso del portale</span><span class="sxs-lookup"><span data-stu-id="47bf8-199">Using Portal</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-portal.md)
* [<span data-ttu-id="47bf8-200">Uso di PowerShell con Data Lake Store come risorsa di archiviazione predefinita</span><span class="sxs-lookup"><span data-stu-id="47bf8-200">Using PowerShell (with Data Lake Store as default storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell-for-default-storage.md)
* [<span data-ttu-id="47bf8-201">Uso di PowerShell con Data Lake Store come risorsa di archiviazione aggiuntiva</span><span class="sxs-lookup"><span data-stu-id="47bf8-201">Using PowerShell (with Data Lake Store as additional storage)</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-powershell.md)
* [<span data-ttu-id="47bf8-202">Uso di modelli di Azure</span><span class="sxs-lookup"><span data-stu-id="47bf8-202">Using Azure templates</span></span>](../data-lake-store/data-lake-store-hdinsight-hadoop-use-resource-manager-template.md)


## <a name="next-steps"></a><span data-ttu-id="47bf8-203">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="47bf8-203">Next steps</span></span>
<span data-ttu-id="47bf8-204">In questo articolo, si è appreso toouse archivio HDFS compatibili con Azure Data Lake con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="47bf8-204">In this article, you learned how toouse HDFS-compatible Azure Data Lake Store with HDInsight.</span></span> <span data-ttu-id="47bf8-205">In questo modo si toobuild scalabili e a lungo termine, l'archiviazione di soluzioni di acquisizione dei dati e usare HDInsight toounlock hello informazioni all'interno di hello archiviato strutturate e i dati non strutturati.</span><span class="sxs-lookup"><span data-stu-id="47bf8-205">This allows you toobuild scalable, long-term, archiving data acquisition solutions and use HDInsight toounlock hello information inside hello stored structured and unstructured data.</span></span>

<span data-ttu-id="47bf8-206">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="47bf8-206">For more information, see:</span></span>

* <span data-ttu-id="47bf8-207">[Introduzione ad Azure HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="47bf8-207">[Get started with Azure HDInsight][hdinsight-get-started]</span></span>
* [<span data-ttu-id="47bf8-208">Introduzione ad Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="47bf8-208">Get started with Azure Data Lake Store</span></span>](../data-lake-store/data-lake-store-get-started-portal.md)
* <span data-ttu-id="47bf8-209">[Caricare dati tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="47bf8-209">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="47bf8-210">[Usare Hive con HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="47bf8-210">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="47bf8-211">[Usare Pig con HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="47bf8-211">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="47bf8-212">[Utilizzo di firme di accesso condiviso archiviazione Azure toorestrict accesso toodata con HDInsight][hdinsight-use-sas]</span><span class="sxs-lookup"><span data-stu-id="47bf8-212">[Use Azure Storage Shared Access Signatures toorestrict access toodata with HDInsight][hdinsight-use-sas]</span></span>

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
