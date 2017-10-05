---
title: Creare cluster Hadoop con PowerShell - Azure HDInsight | Microsoft Docs
description: Informazioni su come creare cluster Hadoop, HBase, Storm o Spark su Linux per HDInsight tramite Azure PowerShell.
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
ms.openlocfilehash: ca75974e6ec4f60739137d4cb5458bbfd735de3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="de109-103">Creare cluster basati su Linux in HDInsight tramite Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="de109-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="de109-104">Azure PowerShell è un ambiente di scripting potente che può essere usato per controllare e automatizzare la distribuzione e la gestione dei carichi di lavoro in Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="de109-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="de109-105">Questo documento offre informazioni su come creare un cluster HDInsight basato su Linux usando Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="de109-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="de109-106">Include anche uno script di esempio.</span><span class="sxs-lookup"><span data-stu-id="de109-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="de109-107">Azure PowerShell è disponibile solo su client Windows.</span><span class="sxs-lookup"><span data-stu-id="de109-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="de109-108">Se si usa un client Mac OS X, Linux o Unix, vedere [Creare cluster basati su Linux in HDInsight tramite l'interfaccia della riga di comando di Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) per informazioni sull'uso dell'interfaccia della riga di comando di Azure per creare un cluster.</span><span class="sxs-lookup"><span data-stu-id="de109-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de109-109">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="de109-109">Prerequisites</span></span>
<span data-ttu-id="de109-110">Prima di iniziare questa procedura è necessario disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="de109-110">You must have the following before starting this procedure:</span></span>

* <span data-ttu-id="de109-111">Una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="de109-111">An Azure subscription.</span></span> <span data-ttu-id="de109-112">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="de109-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="de109-113">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="de109-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="de109-114">Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017.</span><span class="sxs-lookup"><span data-stu-id="de109-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="de109-115">La procedura descritta in questo documento usa i nuovi cmdlet HDInsight, compatibili con Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="de109-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="de109-116">Per installare la versione più recente di Azure PowerShell, seguire la procedura descritta in [Installare Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="de109-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="de109-117">Se sono presenti script che devono essere modificati per l'uso dei nuovi cmdlet compatibili con Azure Resource Manager, per altre informazioni vedere [Migrazione a strumenti di sviluppo basati su Azure Resource Manager per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) .</span><span class="sxs-lookup"><span data-stu-id="de109-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="de109-118">Creare cluster</span><span class="sxs-lookup"><span data-stu-id="de109-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="de109-119">È necessario completare le procedure seguenti per creare un cluster HDInsight con Azure PowerShell:</span><span class="sxs-lookup"><span data-stu-id="de109-119">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span></span>

* <span data-ttu-id="de109-120">Creare un gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="de109-120">Create an Azure resource group</span></span>
* <span data-ttu-id="de109-121">Creare un account di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="de109-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="de109-122">Creazione di un contenitore BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="de109-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="de109-123">Creazione di un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="de109-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="de109-124">Lo script seguente illustra come creare un nuovo cluster:</span><span class="sxs-lookup"><span data-stu-id="de109-124">The following script demonstrates how to create a new cluster:</span></span>

<span data-ttu-id="de109-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span><span class="sxs-lookup"><span data-stu-id="de109-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span></span>

<span data-ttu-id="de109-126">I valori specificati per l'accesso al cluster vengono usati per creare l'account utente Hadoop per il cluster.</span><span class="sxs-lookup"><span data-stu-id="de109-126">The values you specify for the cluster login are used to create the Hadoop user account for the cluster.</span></span> <span data-ttu-id="de109-127">Usare questo account per connettersi ai servizi ospitati nel cluster, ad esempio interfacce utente Web o API REST.</span><span class="sxs-lookup"><span data-stu-id="de109-127">Use this account to connect to services hosted on the cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="de109-128">I valori specificati per l'utente SSH vengono usati per creare l'utente SSH per il cluster.</span><span class="sxs-lookup"><span data-stu-id="de109-128">The values you specify for the SSH user are used to create the SSH user for the cluster.</span></span> <span data-ttu-id="de109-129">Usare questo account per avviare una sessione SSH remota nel cluster ed eseguire i processi.</span><span class="sxs-lookup"><span data-stu-id="de109-129">Use this account to start a remote SSH session on the cluster and run jobs.</span></span> <span data-ttu-id="de109-130">Per altre informazioni, vedere il documento [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="de109-130">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="de109-131">Se si prevede di usare più di 32 nodi del ruolo di lavoro, al momento della creazione del cluster o con il ridimensionamento del cluster dopo la creazione, è necessario specificare anche una dimensione del nodo head con almeno 8 core e 14 GB di RAM.</span><span class="sxs-lookup"><span data-stu-id="de109-131">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="de109-132">Per altre informazioni sulle dimensioni di nodo e i costi associati, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="de109-132">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="de109-133">La creazione di un cluster può richiedere fino a 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="de109-133">It can take up to 20 minutes to create a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="de109-134">Creare il cluster: oggetto di configurazione</span><span class="sxs-lookup"><span data-stu-id="de109-134">Create cluster: Configuration object</span></span>

<span data-ttu-id="de109-135">È anche possibile creare un oggetto di configurazione di HDInsight tramite il cmdlet `New-AzureRmHDInsightClusterConfig`.</span><span class="sxs-lookup"><span data-stu-id="de109-135">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="de109-136">È quindi possibile modificare questo oggetto di configurazione per abilitare le opzioni di configurazione aggiuntive per il cluster.</span><span class="sxs-lookup"><span data-stu-id="de109-136">You can then modify this configuration object to enable additional configuration options for your cluster.</span></span> <span data-ttu-id="de109-137">Infine, usare il parametro `-Config` del cmdlet `New-AzureRmHDInsightCluster` per usare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="de109-137">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span></span>

<span data-ttu-id="de109-138">Lo script seguente crea un oggetto di configurazione per configurare un R Server sul tipo di cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="de109-138">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="de109-139">La configurazione consente a un nodo del bordo, RStudio e ad un account di archiviazione aggiuntivo.</span><span class="sxs-lookup"><span data-stu-id="de109-139">The configuration enables an edge node, RStudio, and an additional storage account.</span></span>

<span data-ttu-id="de109-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span><span class="sxs-lookup"><span data-stu-id="de109-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span></span>

> [!WARNING]
> <span data-ttu-id="de109-141">L'uso di un account di archiviazione in una località diversa rispetto al cluster HDInsight non è supportato.</span><span class="sxs-lookup"><span data-stu-id="de109-141">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span> <span data-ttu-id="de109-142">Quando si usa questo esempio, creare l'account di archiviazione aggiuntivo nello stesso percorso del server.</span><span class="sxs-lookup"><span data-stu-id="de109-142">When using this example, create the additional storage account in the same location as the server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="de109-143">Personalizzare i cluster</span><span class="sxs-lookup"><span data-stu-id="de109-143">Customize clusters</span></span>

* <span data-ttu-id="de109-144">Vedere [Personalizzare cluster HDInsight tramite Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="de109-144">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="de109-145">Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="de109-145">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="de109-146">Eliminazione del cluster</span><span class="sxs-lookup"><span data-stu-id="de109-146">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="de109-147">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="de109-147">Troubleshoot</span></span>

<span data-ttu-id="de109-148">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="de109-148">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="de109-149">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="de109-149">Next steps</span></span>

<span data-ttu-id="de109-150">Dopo aver creato un cluster HDInsight, usare le risorse seguenti per acquisire familiarità con il cluster.</span><span class="sxs-lookup"><span data-stu-id="de109-150">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="de109-151">Cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="de109-151">Hadoop clusters</span></span>

* [<span data-ttu-id="de109-152">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="de109-152">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="de109-153">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="de109-153">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="de109-154">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="de109-154">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="de109-155">Cluster HBase</span><span class="sxs-lookup"><span data-stu-id="de109-155">HBase clusters</span></span>

* [<span data-ttu-id="de109-156">Introduzione a HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="de109-156">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="de109-157">Sviluppare applicazioni Java per HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="de109-157">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="de109-158">Cluster Storm</span><span class="sxs-lookup"><span data-stu-id="de109-158">Storm clusters</span></span>

* [<span data-ttu-id="de109-159">Sviluppare topologie Java per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="de109-159">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="de109-160">Usare i componenti di Python in Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="de109-160">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="de109-161">Distribuire e monitorare le topologie con Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="de109-161">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="de109-162">Cluster Spark</span><span class="sxs-lookup"><span data-stu-id="de109-162">Spark clusters</span></span>

* [<span data-ttu-id="de109-163">Creare un'applicazione autonoma con Scala</span><span class="sxs-lookup"><span data-stu-id="de109-163">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="de109-164">Eseguire i processi in modalità remota in un cluster Spark utilizzando Livy</span><span class="sxs-lookup"><span data-stu-id="de109-164">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="de109-165">Spark con Business Intelligence: eseguire l'analisi interattiva dei dati con strumenti di Business Intelligence mediante Spark in HDInsight</span><span class="sxs-lookup"><span data-stu-id="de109-165">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="de109-166">Spark con Machine Learning: utilizzare Spark in HDInsight per stimare i risultati dell'ispezione cibo</span><span class="sxs-lookup"><span data-stu-id="de109-166">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="de109-167">Streaming Spark: usare Spark in HDInsight per la creazione di applicazioni di streaming in tempo reale</span><span class="sxs-lookup"><span data-stu-id="de109-167">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

