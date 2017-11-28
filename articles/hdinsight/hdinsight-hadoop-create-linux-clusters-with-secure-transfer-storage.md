---
title: aaaCreate Hadoop cluster con gli account di archiviazione di protezione del trasferimento in Azure HDInsight | Documenti Microsoft
description: Informazioni su come i cluster di HDInsight toocreate con protezione del trasferimento di abilitare gli account di archiviazione di Azure.
keywords: introduzione a Hadoop,Hadoop basato su Linux,guida introduttiva a Hadoop,trasferimento sicuro,account di archiviazione di Azure
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="8c5af-104">Creare un cluster Hadoop con account di archiviazione con trasferimento sicuro in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="8c5af-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="8c5af-105">Hello [necessario trasferimento sicuro](../storage/common/storage-require-secure-transfer.md) funzionalità migliora la sicurezza hello dell'account di archiviazione di Azure tramite l'applicazione di tutti i conti tooyour richieste tramite una connessione protetta.</span><span class="sxs-lookup"><span data-stu-id="8c5af-105">hello [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances hello security of your Azure Storage account by enforcing all requests tooyour account through a secure connection.</span></span> <span data-ttu-id="8c5af-106">Questo schema wasbs funzionalità e hello sono supportati solo dalla versione del cluster HDInsight 3.6 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="8c5af-106">This feature and hello wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="8c5af-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="8c5af-107">Prerequisites</span></span>
<span data-ttu-id="8c5af-108">Prima di iniziare questa esercitazione, è necessario avere:</span><span class="sxs-lookup"><span data-stu-id="8c5af-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="8c5af-109">**Sottoscrizione di Azure**: toocreate un mese di un account di prova, è esplorare troppo[azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="8c5af-109">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="8c5af-110">**Account di archiviazione di Azure con trasferimento sicuro abilitato**.</span><span class="sxs-lookup"><span data-stu-id="8c5af-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="8c5af-111">Per istruzioni hello, vedere [creare un account di archiviazione](../storage/common/storage-create-storage-account.md#create-a-storage-account) e [richiedono il trasferimento protetto](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="8c5af-111">For hello instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="8c5af-112">**Un contenitore Blob nell'account di archiviazione hello**.</span><span class="sxs-lookup"><span data-stu-id="8c5af-112">**A Blob container on hello storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="8c5af-113">Creare cluster</span><span class="sxs-lookup"><span data-stu-id="8c5af-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="8c5af-114">In questa sezione viene creato un cluster Hadoop in HDInsight usando un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="8c5af-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="8c5af-115">modello Hello nella [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="8c5af-115">hello template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="8c5af-116">Per questa esercitazione non è necessario conoscere il modello di Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="8c5af-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="8c5af-117">Per altri metodi di creazione del cluster e informazioni sulle proprietà hello utilizzate in questa esercitazione, vedere [cluster HDInsight creare](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="8c5af-117">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="8c5af-118">Fare clic su hello seguente immagine toosign in tooAzure e il modello di gestione risorse hello Apri nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="8c5af-118">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="8c5af-119">Segue hello istruzioni toocreate hello cluster con hello seguenti specifiche:</span><span class="sxs-lookup"><span data-stu-id="8c5af-119">Follow hello instructions toocreate hello cluster with hello following specifications:</span></span> 

    - <span data-ttu-id="8c5af-120">Specificare HDInsight versione 3.6.</span><span class="sxs-lookup"><span data-stu-id="8c5af-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="8c5af-121">versione predefinita di Hello è 3.5.</span><span class="sxs-lookup"><span data-stu-id="8c5af-121">hello default version is 3.5.</span></span> <span data-ttu-id="8c5af-122">È necessaria la versione 3.6 o successiva.</span><span class="sxs-lookup"><span data-stu-id="8c5af-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="8c5af-123">Specificare un account di archiviazione con trasferimento sicuro abilitato.</span><span class="sxs-lookup"><span data-stu-id="8c5af-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="8c5af-124">Utilizzare un nome breve per l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="8c5af-124">Use short name for hello storage account.</span></span>
    - <span data-ttu-id="8c5af-125">Account di archiviazione hello sia il contenitore di blob hello deve essere create in precedenza.</span><span class="sxs-lookup"><span data-stu-id="8c5af-125">Both hello storage account and hello blob container must be created beforehand.</span></span> 

    <span data-ttu-id="8c5af-126">Per istruzioni hello, vedere [Crea cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="8c5af-126">For hello instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="8c5af-127">Se si utilizzano script azione tooprovide dei file di configurazione, è necessario utilizzare wasbs in hello seguenti impostazioni:</span><span class="sxs-lookup"><span data-stu-id="8c5af-127">If you use script action tooprovide your own configuration files, you must use wasbs in hello following settings:</span></span>

- <span data-ttu-id="8c5af-128">fs.defaultFS (core-site)</span><span class="sxs-lookup"><span data-stu-id="8c5af-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="8c5af-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="8c5af-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="8c5af-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="8c5af-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="8c5af-131">Aggiungere altri account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="8c5af-131">Add additional storage accounts</span></span>

<span data-ttu-id="8c5af-132">Sono disponibili diverse opzioni tooadd account di archiviazione aggiuntive trasferimento sicuro abilitato:</span><span class="sxs-lookup"><span data-stu-id="8c5af-132">There are several options tooadd additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="8c5af-133">Modificare il modello di Azure Resource Manager hello nell'ultima sezione hello.</span><span class="sxs-lookup"><span data-stu-id="8c5af-133">Modify hello Azure Resource Manager template in hello last section.</span></span>
- <span data-ttu-id="8c5af-134">Creare un cluster utilizzando hello [portale di Azure](https://portal.azure.com) e specificare l'account di archiviazione collegato.</span><span class="sxs-lookup"><span data-stu-id="8c5af-134">Create a cluster using hello [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="8c5af-135">Utilizzare script azione tooadd aggiuntive il trasferimento protetto è abilitato il cluster HDInsight esistente di storage account tooan.</span><span class="sxs-lookup"><span data-stu-id="8c5af-135">Use script action tooadd additional secure transfer enabled storage accounts tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="8c5af-136">Per ulteriori informazioni, vedere [aggiungere ulteriore spazio di archiviazione account tooHDInsight](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8c5af-136">For more information, see [Add additional storage accounts tooHDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="8c5af-137">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8c5af-137">Next steps</span></span>
<span data-ttu-id="8c5af-138">In questa esercitazione, si è appreso come toocreate un cluster HDInsight e abilitare protezione trasferire account di archiviazione toohello.</span><span class="sxs-lookup"><span data-stu-id="8c5af-138">In this tutorial, you have learned how toocreate an HDInsight cluster, and enable secure transfer toohello storage accounts.</span></span>

<span data-ttu-id="8c5af-139">toolearn più sull'analisi dei dati con HDInsight, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="8c5af-139">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="8c5af-140">toolearn ulteriori informazioni sull'utilizzo di Hive con HDInsight, incluso come una query Hive tooperform da Visual Studio, vedere [utilizzare Hive con HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="8c5af-140">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="8c5af-141">toolearn su Pig, un linguaggio tootransform dati, vedere [usare Pig con HDInsight][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="8c5af-141">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="8c5af-142">toolearn su MapReduce, un toowrite programmi che elaborano i dati in Hadoop, vedere [utilizzare MapReduce con HDInsight][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="8c5af-142">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="8c5af-143">toolearn sull'uso di strumenti di HDInsight hello per i dati di Visual Studio tooanalyze in HDInsight, vedere [iniziare a usare gli strumenti di Visual Studio Hadoop per HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8c5af-143">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="8c5af-144">altre informazioni sulle modalità di archiviazione dati HDInsight toolearn o dati tooget in HDInsight, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="8c5af-144">toolearn more about how HDInsight stores data or how tooget data into HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="8c5af-145">Per informazioni sul modo in cui HDInsight usa Archiviazione di Azure, vedere [Usare Archiviazione di Azure con HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="8c5af-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="8c5af-146">Per informazioni su come tooupload tooHDInsight di dati, vedere [caricare dati tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="8c5af-146">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="8c5af-147">toolearn più sulla creazione o la gestione di un cluster HDInsight, vedere hello seguenti articoli:</span><span class="sxs-lookup"><span data-stu-id="8c5af-147">toolearn more about creating or managing an HDInsight cluster, see hello following articles:</span></span>

* <span data-ttu-id="8c5af-148">toolearn sulla gestione dei cluster HDInsight basati su Linux, vedere [cluster di gestire HDInsight con Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="8c5af-148">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="8c5af-149">toolearn più sulle opzioni di hello è possibile selezionare durante la creazione di un cluster HDInsight, vedere [la creazione di HDInsight su Linux usando le opzioni personalizzate](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="8c5af-149">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="8c5af-150">Se si ha familiarità con Linux e Hadoop, ma si desidera specifiche tooknow sul Hadoop in HDInsight hello, vedere [utilizzo di HDInsight su Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="8c5af-150">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="8c5af-151">In questo articolo sono disponibili informazioni quali:</span><span class="sxs-lookup"><span data-stu-id="8c5af-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="8c5af-152">URL per i servizi ospitati nel cluster di hello, ad esempio Ambari e WebHCat</span><span class="sxs-lookup"><span data-stu-id="8c5af-152">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="8c5af-153">percorso di Hello del file Hadoop ed esempi sulla hello file system locale</span><span class="sxs-lookup"><span data-stu-id="8c5af-153">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="8c5af-154">utilizzo di Hello di Azure Storage (WASB) anziché HDFS come archivio dati predefinito di hello</span><span class="sxs-lookup"><span data-stu-id="8c5af-154">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


