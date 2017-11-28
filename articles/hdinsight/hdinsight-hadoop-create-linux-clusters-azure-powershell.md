---
title: i cluster Hadoop aaaCreate con PowerShell - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toocreate Hadoop, HBase, Storm o Spark cluster Linux per HDInsight tramite Azure PowerShell.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="2f210-103">Creare cluster basati su Linux in HDInsight tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f210-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="2f210-104">Azure PowerShell è un ambiente di scripting potente che è possibile utilizzare toocontrol e automatizzare la distribuzione di hello e la gestione dei carichi di lavoro in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="2f210-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="2f210-105">Questo documento fornisce informazioni su come toocreate un HDInsight basati su Linux cluster tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f210-105">This document provides information about how toocreate a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="2f210-106">Include anche uno script di esempio.</span><span class="sxs-lookup"><span data-stu-id="2f210-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="2f210-107">Azure PowerShell è disponibile solo su client Windows.</span><span class="sxs-lookup"><span data-stu-id="2f210-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="2f210-108">Se si utilizza un client Mac OS X, Linux o Unix, vedere [creare un cluster HDInsight basati su Linux mediante Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) per informazioni sull'utilizzo di hello Azure CLI toocreate un cluster.</span><span class="sxs-lookup"><span data-stu-id="2f210-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using hello Azure CLI toocreate a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f210-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2f210-109">Prerequisites</span></span>
<span data-ttu-id="2f210-110">È necessario disporre delle seguenti hello prima di iniziare questa procedura:</span><span class="sxs-lookup"><span data-stu-id="2f210-110">You must have hello following before starting this procedure:</span></span>

* <span data-ttu-id="2f210-111">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f210-111">An Azure subscription.</span></span> <span data-ttu-id="2f210-112">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="2f210-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="2f210-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="2f210-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="2f210-114">Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017.</span><span class="sxs-lookup"><span data-stu-id="2f210-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="2f210-115">Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="2f210-115">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="2f210-116">Eseguire le operazioni di hello in [installare Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2f210-116">Please follow hello steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="2f210-117">Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) per ulteriori informazioni.</span><span class="sxs-lookup"><span data-stu-id="2f210-117">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="2f210-118">Creare cluster</span><span class="sxs-lookup"><span data-stu-id="2f210-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="2f210-119">toocreate un cluster HDInsight tramite Azure PowerShell, è necessario completare hello seguire le procedure seguenti:</span><span class="sxs-lookup"><span data-stu-id="2f210-119">toocreate an HDInsight cluster by using Azure PowerShell, you must complete hello following procedures:</span></span>

* <span data-ttu-id="2f210-120">Creare un gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="2f210-120">Create an Azure resource group</span></span>
* <span data-ttu-id="2f210-121">Creare un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2f210-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="2f210-122">Creazione di un contenitore BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="2f210-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="2f210-123">Creazione di un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f210-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="2f210-124">Hello script riportato di seguito viene illustrato come toocreate un nuovo cluster:</span><span class="sxs-lookup"><span data-stu-id="2f210-124">hello following script demonstrates how toocreate a new cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

<span data-ttu-id="2f210-125">i valori di Hello specificati per l'account di accesso cluster hello sono utilizzati toocreate hello account utente Hadoop per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2f210-125">hello values you specify for hello cluster login are used toocreate hello Hadoop user account for hello cluster.</span></span> <span data-ttu-id="2f210-126">Utilizzare questo tooservices tooconnect account ospitate nel cluster di hello, ad esempio web le interfacce utente o le API REST.</span><span class="sxs-lookup"><span data-stu-id="2f210-126">Use this account tooconnect tooservices hosted on hello cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="2f210-127">valori Hello specificati per l'utente SSH hello sono utilizzati toocreate hello SSH utente cluster hello.</span><span class="sxs-lookup"><span data-stu-id="2f210-127">hello values you specify for hello SSH user are used toocreate hello SSH user for hello cluster.</span></span> <span data-ttu-id="2f210-128">Utilizzare questo account toostart una sessione SSH remota in cluster hello ed eseguire i processi.</span><span class="sxs-lookup"><span data-stu-id="2f210-128">Use this account toostart a remote SSH session on hello cluster and run jobs.</span></span> <span data-ttu-id="2f210-129">Per ulteriori informazioni, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="2f210-129">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2f210-130">Se si prevede di toouse più di 32 nodi di lavoro (al momento della creazione del cluster o hello scalabilità del cluster dopo la creazione), è necessario specificare anche una dimensione del nodo head con almeno 8 core e 14 GB di RAM.</span><span class="sxs-lookup"><span data-stu-id="2f210-130">If you plan toouse more than 32 worker nodes (either at cluster creation or by scaling hello cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="2f210-131">Per altre informazioni sulle dimensioni di nodo e i costi associati, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="2f210-131">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="2f210-132">Potrebbe essere necessaria fino too20 minuti toocreate un cluster.</span><span class="sxs-lookup"><span data-stu-id="2f210-132">It can take up too20 minutes toocreate a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="2f210-133">Creare il cluster: oggetto di configurazione</span><span class="sxs-lookup"><span data-stu-id="2f210-133">Create cluster: Configuration object</span></span>

<span data-ttu-id="2f210-134">È anche possibile creare un oggetto di configurazione di HDInsight tramite il cmdlet `New-AzureRmHDInsightClusterConfig`.</span><span class="sxs-lookup"><span data-stu-id="2f210-134">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="2f210-135">È quindi possibile modificare questa configurazione oggetto tooenable ulteriori opzioni di configurazione per il cluster.</span><span class="sxs-lookup"><span data-stu-id="2f210-135">You can then modify this configuration object tooenable additional configuration options for your cluster.</span></span> <span data-ttu-id="2f210-136">Infine, utilizzare hello `-Config` parametro di hello `New-AzureRmHDInsightCluster` configurazione hello toouse di cmdlet.</span><span class="sxs-lookup"><span data-stu-id="2f210-136">Finally, use hello `-Config` parameter of hello `New-AzureRmHDInsightCluster` cmdlet toouse hello configuration.</span></span>

<span data-ttu-id="2f210-137">Hello script seguente crea un tooconfigure oggetto di configurazione Server R sul tipo di cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="2f210-137">hello following script creates a configuration object tooconfigure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="2f210-138">configurazione di Hello consente un nodo del bordo, RStudio e un account di archiviazione aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="2f210-138">hello configuration enables an edge node, RStudio, and an additional storage account.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> <span data-ttu-id="2f210-139">Non è supportato l'utilizzo di un account di archiviazione in un percorso diverso da quello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="2f210-139">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span> <span data-ttu-id="2f210-140">Quando si utilizza questo esempio, creare account di archiviazione aggiuntivo hello in hello stesso percorso server hello.</span><span class="sxs-lookup"><span data-stu-id="2f210-140">When using this example, create hello additional storage account in hello same location as hello server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="2f210-141">Personalizzare i cluster</span><span class="sxs-lookup"><span data-stu-id="2f210-141">Customize clusters</span></span>

* <span data-ttu-id="2f210-142">Vedere [Personalizzare cluster HDInsight tramite Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="2f210-142">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="2f210-143">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="2f210-143">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="2f210-144">Eliminare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="2f210-144">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="2f210-145">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="2f210-145">Troubleshoot</span></span>

<span data-ttu-id="2f210-146">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="2f210-146">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f210-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2f210-147">Next steps</span></span>

<span data-ttu-id="2f210-148">Ora che è stato creato correttamente un cluster HDInsight, utilizzare hello seguenti come risorse toolearn toowork con il cluster.</span><span class="sxs-lookup"><span data-stu-id="2f210-148">Now that you have successfully created an HDInsight cluster, use hello following resources toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="2f210-149">Cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="2f210-149">Hadoop clusters</span></span>

* [<span data-ttu-id="2f210-150">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f210-150">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="2f210-151">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f210-151">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="2f210-152">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f210-152">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="2f210-153">Cluster HBase</span><span class="sxs-lookup"><span data-stu-id="2f210-153">HBase clusters</span></span>

* [<span data-ttu-id="2f210-154">Introduzione a HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f210-154">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="2f210-155">Sviluppare applicazioni Java per HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f210-155">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="2f210-156">Cluster Storm</span><span class="sxs-lookup"><span data-stu-id="2f210-156">Storm clusters</span></span>

* [<span data-ttu-id="2f210-157">Sviluppare topologie Java per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f210-157">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="2f210-158">Usare i componenti di Python in Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f210-158">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="2f210-159">Distribuire e monitorare le topologie con Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f210-159">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="2f210-160">Cluster Spark</span><span class="sxs-lookup"><span data-stu-id="2f210-160">Spark clusters</span></span>

* [<span data-ttu-id="2f210-161">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="2f210-161">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="2f210-162">Eseguire i processi in modalità remota in un cluster Spark utilizzando Livy</span><span class="sxs-lookup"><span data-stu-id="2f210-162">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="2f210-163">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="2f210-163">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="2f210-164">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="2f210-164">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="2f210-165">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="2f210-165">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

