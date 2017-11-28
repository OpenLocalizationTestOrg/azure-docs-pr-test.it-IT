---
title: Creare cluster Hadoop con una riga di comando - Azure HDInsight | Documentazione Microsoft
description: Informazioni su come creare cluster HDInsight tramite l'interfaccia della riga di comando di Azure 1.0.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 8f2fcb46789d000cd66164508f1159338dcae5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-using-the-azure-cli"></a><span data-ttu-id="f579e-103">Creare cluster HDInsight tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f579e-103">Create HDInsight clusters using the Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="f579e-104">La procedura presentata in questo documento illustra come creare un cluster HDInsight 3.5 usando l'interfaccia della riga di comando di Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="f579e-104">The steps in this document walk-through creating a HDInsight 3.5 cluster using the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f579e-105">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="f579e-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="f579e-106">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="f579e-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="f579e-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f579e-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="f579e-108">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="f579e-108">**An Azure subscription**.</span></span> <span data-ttu-id="f579e-109">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f579e-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="f579e-110">**Interfaccia della riga di comando di Azure**.</span><span class="sxs-lookup"><span data-stu-id="f579e-110">**Azure CLI**.</span></span> <span data-ttu-id="f579e-111">I passaggi descritti nel presente documento sono stati testati con la versione dell'interfaccia della riga di comando di Azure 0.10.14.</span><span class="sxs-lookup"><span data-stu-id="f579e-111">The steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f579e-112">La procedura descritta in questo documento non funziona con l'interfaccia della riga di comando di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="f579e-112">The steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="f579e-113">L'interfaccia della riga di comando di Azure 2.0 non supporta la creazione di un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f579e-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="f579e-114">Accedere alla sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="f579e-114">Log in to your Azure subscription</span></span>

<span data-ttu-id="f579e-115">Seguire i passaggi descritti in [Connettersi a una sottoscrizione Azure dall'interfaccia della riga di comando di Azure](../xplat-cli-connect.md) e connettersi alla sottoscrizione usando il metodo **login** .</span><span class="sxs-lookup"><span data-stu-id="f579e-115">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="f579e-116">Creare un cluster</span><span class="sxs-lookup"><span data-stu-id="f579e-116">Create a cluster</span></span>

<span data-ttu-id="f579e-117">I passaggi seguenti devono essere eseguiti dalla riga di comando, ad esempio PowerShell o Bash.</span><span class="sxs-lookup"><span data-stu-id="f579e-117">The following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="f579e-118">Per eseguire l'autenticazione della sottoscrizione di Azure, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f579e-118">Use the following command to authenticate to your Azure subscription:</span></span>

        azure login

    <span data-ttu-id="f579e-119">Occorre specificare il nome e la password.</span><span class="sxs-lookup"><span data-stu-id="f579e-119">You are prompted to provide your name and password.</span></span> <span data-ttu-id="f579e-120">Se si dispone di più sottoscrizioni di Azure, usare `azure account set <subscriptionname>` per impostare la sottoscrizione utilizzata dai comandi dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="f579e-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` to set the subscription that the Azure CLI commands use.</span></span>

2. <span data-ttu-id="f579e-121">Passare alla modalità Gestione risorse di Azure usando il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f579e-121">Switch to Azure Resource Manager mode using the following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="f579e-122">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f579e-122">Create a resource group.</span></span> <span data-ttu-id="f579e-123">Questo gruppo di risorse contiene il cluster HDInsight e l'account di archiviazione associato.</span><span class="sxs-lookup"><span data-stu-id="f579e-123">This resource group contains the HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="f579e-124">Sostituire `groupname` con un nome univoco per il gruppo.</span><span class="sxs-lookup"><span data-stu-id="f579e-124">Replace `groupname` with a unique name for the group.</span></span>

    * <span data-ttu-id="f579e-125">Sostituire `location` con l'area geografica in cui si vuole creare il gruppo.</span><span class="sxs-lookup"><span data-stu-id="f579e-125">Replace `location` with the geographic region that you want to create the group in.</span></span>

       <span data-ttu-id="f579e-126">Per un elenco di località valide, usare il comando `azure location list` e quindi una delle località della colonna `Name`.</span><span class="sxs-lookup"><span data-stu-id="f579e-126">For a list of valid locations, use the `azure location list` command, and then use one of the locations from the `Name` column.</span></span>

4. <span data-ttu-id="f579e-127">Creare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f579e-127">Create a storage account.</span></span> <span data-ttu-id="f579e-128">Questo account di archiviazione verrà usato come risorsa di archiviazione predefinita per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="f579e-128">This storage account is used as the default storage for the HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="f579e-129">Sostituire `groupname` con il nome del gruppo creato nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="f579e-129">Replace `groupname` with the name of the group created in the previous step.</span></span>

    * <span data-ttu-id="f579e-130">Sostituire `location` con la stessa località usata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="f579e-130">Replace `location` with the same location used in the previous step.</span></span>

    * <span data-ttu-id="f579e-131">Sostituire `storagename` con un nome univoco per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f579e-131">Replace `storagename` with a unique name for the storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="f579e-132">Per altre informazioni sui parametri usati in questo comando, usare `azure storage account create -h` per visualizzare la Guida relativa a questo comando.</span><span class="sxs-lookup"><span data-stu-id="f579e-132">For more information on the parameters used in this command, use `azure storage account create -h` to view help for this command.</span></span>

5. <span data-ttu-id="f579e-133">Recuperare la chiave usata per accedere all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f579e-133">Retrieve the key used to access the storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="f579e-134">Sostituire `groupname` con il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f579e-134">Replace `groupname` with the resource group name.</span></span>
    * <span data-ttu-id="f579e-135">Sostituire `storagename` con il nome per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f579e-135">Replace `storagename` with the name of the storage account.</span></span>

     <span data-ttu-id="f579e-136">Nei dati restituiti salvare il valore `key` per `key1`.</span><span class="sxs-lookup"><span data-stu-id="f579e-136">In the data that is returned, save the `key` value for `key1`.</span></span>

6. <span data-ttu-id="f579e-137">Creare un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="f579e-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="f579e-138">Sostituire `groupname` con il nome del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="f579e-138">Replace `groupname` with the resource group name.</span></span>

    * <span data-ttu-id="f579e-139">Sostituire `Hadoop` con il tipo di cluster da creare,</span><span class="sxs-lookup"><span data-stu-id="f579e-139">Replace `Hadoop` with the cluster type that you wish to create.</span></span> <span data-ttu-id="f579e-140">ad esempio, `Hadoop`, `HBase`, `Kafka`, `Spark` o `Storm`.</span><span class="sxs-lookup"><span data-stu-id="f579e-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="f579e-141">Sono disponibili molti tipi di cluster HDInsight, che corrispondono al carico di lavoro o alla tecnologia per cui è ottimizzato il cluster.</span><span class="sxs-lookup"><span data-stu-id="f579e-141">HDInsight clusters come in various types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="f579e-142">Non è disponibile alcun metodo supportato per creare un cluster che combini più tipi, ad esempio Storm e HBase in un cluster.</span><span class="sxs-lookup"><span data-stu-id="f579e-142">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="f579e-143">Sostituire `location` con la stessa località usata nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="f579e-143">Replace `location` with the same location used in previous steps.</span></span>

    * <span data-ttu-id="f579e-144">Sostituire `storagename` con il nome per l'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="f579e-144">Replace `storagename` with the storage account name.</span></span>

    * <span data-ttu-id="f579e-145">Sostituire `storagekey` con la chiave ottenuta nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="f579e-145">Replace `storagekey` with the key obtained in the previous step.</span></span>

    * <span data-ttu-id="f579e-146">Per il parametro `--defaultStorageContainer` usare lo stesso nome usato per il cluster.</span><span class="sxs-lookup"><span data-stu-id="f579e-146">For the `--defaultStorageContainer` parameter, use the same name as you are using for the cluster.</span></span>

    * <span data-ttu-id="f579e-147">Sostituire `admin` e `httppassword` con il nome e la password da usare per l'accesso al cluster tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="f579e-147">Replace `admin` and `httppassword` with the name and password you wish to use when accessing the cluster through HTTPS.</span></span>

    * <span data-ttu-id="f579e-148">Sostituire `sshuser` e `sshuserpassword` con il nome utente e la password da usare per l'accesso al cluster tramite SSH</span><span class="sxs-lookup"><span data-stu-id="f579e-148">Replace `sshuser` and `sshuserpassword` with the username and password you wish to use when accessing the cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="f579e-149">L'esempio precedente crea un cluster con 2 nodi di ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="f579e-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="f579e-150">È inoltre possibile modificare il numero di nodi del ruolo di lavoro dopo la creazione del cluster eseguendo le operazioni di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="f579e-150">You can also change the number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="f579e-151">Se si prevede di usare più di 32 nodi del ruolo di lavoro, è necessario selezionare una dimensione del nodo head con almeno 8 core e 14 GB di RAM.</span><span class="sxs-lookup"><span data-stu-id="f579e-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="f579e-152">È possibile impostare le dimensioni del nodo head usando il parametro `--headNodeSize` durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="f579e-152">You can set the head node size by using the `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="f579e-153">Per altre informazioni sulle dimensioni di nodo e i costi associati, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="f579e-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="f579e-154">Il processo di creazione del cluster può richiedere alcuni minuti,</span><span class="sxs-lookup"><span data-stu-id="f579e-154">It may take several minutes for the cluster creation process to finish.</span></span> <span data-ttu-id="f579e-155">in genere circa 15.</span><span class="sxs-lookup"><span data-stu-id="f579e-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="f579e-156">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="f579e-156">Troubleshoot</span></span>

<span data-ttu-id="f579e-157">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="f579e-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="f579e-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f579e-158">Next steps</span></span>

<span data-ttu-id="f579e-159">Dopo aver creato un cluster HDInsight tramite l'interfaccia della riga di comando di Azure, usare le informazioni seguenti per acquisire familiarità con il cluster:</span><span class="sxs-lookup"><span data-stu-id="f579e-159">Now that you have successfully created an HDInsight cluster using the Azure CLI, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="f579e-160">Cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="f579e-160">Hadoop clusters</span></span>

* [<span data-ttu-id="f579e-161">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="f579e-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="f579e-162">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="f579e-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="f579e-163">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="f579e-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="f579e-164">Cluster HBase</span><span class="sxs-lookup"><span data-stu-id="f579e-164">HBase clusters</span></span>

* [<span data-ttu-id="f579e-165">Introduzione a HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f579e-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="f579e-166">Sviluppare applicazioni Java per HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f579e-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="f579e-167">Cluster Storm</span><span class="sxs-lookup"><span data-stu-id="f579e-167">Storm clusters</span></span>

* [<span data-ttu-id="f579e-168">Sviluppare topologie Java per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f579e-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="f579e-169">Usare i componenti di Python in Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f579e-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="f579e-170">Distribuire e monitorare le topologie con Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="f579e-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
