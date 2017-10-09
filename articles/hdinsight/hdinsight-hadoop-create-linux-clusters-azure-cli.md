---
title: i cluster Hadoop aaaCreate tramite riga di comando - hello Azure HDInsight | Documenti Microsoft
description: Informazioni su come i cluster HDInsight toocreate usando hello multipiattaforma Azure CLI 1.0.
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
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a><span data-ttu-id="d7c49-103">Creare il cluster HDInsight tramite hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="d7c49-103">Create HDInsight clusters using hello Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="d7c49-104">Hello passaggi in questa procedura dettagliata documento creazione di un cluster HDInsight 3.5 utilizzando hello Azure CLI 1.0.</span><span class="sxs-lookup"><span data-stu-id="d7c49-104">hello steps in this document walk-through creating a HDInsight 3.5 cluster using hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="d7c49-105">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d7c49-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d7c49-106">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d7c49-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="d7c49-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d7c49-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="d7c49-108">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d7c49-108">**An Azure subscription**.</span></span> <span data-ttu-id="d7c49-109">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d7c49-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="d7c49-110">**Interfaccia della riga di comando di Azure**.</span><span class="sxs-lookup"><span data-stu-id="d7c49-110">**Azure CLI**.</span></span> <span data-ttu-id="d7c49-111">passaggi di Hello in questo documento sono stati testati ultima con versione 0.10.14 CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="d7c49-111">hello steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d7c49-112">passaggi di Hello in questo documento non funzionano con l'interfaccia CLI di Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="d7c49-112">hello steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="d7c49-113">L'interfaccia della riga di comando di Azure 2.0 non supporta la creazione di un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d7c49-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="d7c49-114">Accedi tooyour sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="d7c49-114">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="d7c49-115">Seguire i passaggi di hello documentati in [connettersi tooan sottoscrizione di Azure da hello interfaccia della riga di comando di Azure (Azure CLI)](../xplat-cli-connect.md) e connettersi tooyour sottoscrizione utilizzando hello **accesso** (metodo).</span><span class="sxs-lookup"><span data-stu-id="d7c49-115">Follow hello steps documented in [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect tooyour subscription using hello **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="d7c49-116">Creare un cluster</span><span class="sxs-lookup"><span data-stu-id="d7c49-116">Create a cluster</span></span>

<span data-ttu-id="d7c49-117">Hello alla procedura seguente deve essere eseguita dalla riga di comando, ad esempio PowerShell o Bash.</span><span class="sxs-lookup"><span data-stu-id="d7c49-117">hello following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="d7c49-118">Utilizzare hello successivo comando tooauthenticate tooyour sottoscrizione di Azure:</span><span class="sxs-lookup"><span data-stu-id="d7c49-118">Use hello following command tooauthenticate tooyour Azure subscription:</span></span>

        azure login

    <span data-ttu-id="d7c49-119">Si è tooprovide richiesto il nome e la password.</span><span class="sxs-lookup"><span data-stu-id="d7c49-119">You are prompted tooprovide your name and password.</span></span> <span data-ttu-id="d7c49-120">Se si dispone di più sottoscrizioni di Azure, utilizzare `azure account set <subscriptionname>` sottoscrizione hello tooset hello CLI di Azure, i comandi usano.</span><span class="sxs-lookup"><span data-stu-id="d7c49-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` tooset hello subscription that hello Azure CLI commands use.</span></span>

2. <span data-ttu-id="d7c49-121">Passare in modalità di gestione risorse tooAzure utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d7c49-121">Switch tooAzure Resource Manager mode using hello following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="d7c49-122">Creare un gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d7c49-122">Create a resource group.</span></span> <span data-ttu-id="d7c49-123">Il gruppo di risorse cluster HDInsight hello e account di archiviazione associato.</span><span class="sxs-lookup"><span data-stu-id="d7c49-123">This resource group contains hello HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="d7c49-124">Sostituire `groupname` con un nome univoco per il gruppo di hello.</span><span class="sxs-lookup"><span data-stu-id="d7c49-124">Replace `groupname` with a unique name for hello group.</span></span>

    * <span data-ttu-id="d7c49-125">Sostituire `location` con area geografica hello che si desidera che il gruppo di hello toocreate in.</span><span class="sxs-lookup"><span data-stu-id="d7c49-125">Replace `location` with hello geographic region that you want toocreate hello group in.</span></span>

       <span data-ttu-id="d7c49-126">Per un elenco di percorsi validi, utilizzare hello `azure location list` comandi e quindi utilizzare uno dei percorsi di hello da hello `Name` colonna.</span><span class="sxs-lookup"><span data-stu-id="d7c49-126">For a list of valid locations, use hello `azure location list` command, and then use one of hello locations from hello `Name` column.</span></span>

4. <span data-ttu-id="d7c49-127">Creare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d7c49-127">Create a storage account.</span></span> <span data-ttu-id="d7c49-128">Questo account di archiviazione viene utilizzato come spazio di archiviazione di hello predefinito per il cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d7c49-128">This storage account is used as hello default storage for hello HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="d7c49-129">Sostituire `groupname` con nome hello del gruppo di hello creato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d7c49-129">Replace `groupname` with hello name of hello group created in hello previous step.</span></span>

    * <span data-ttu-id="d7c49-130">Sostituire `location` con hello nello stesso percorso utilizzato nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d7c49-130">Replace `location` with hello same location used in hello previous step.</span></span>

    * <span data-ttu-id="d7c49-131">Sostituire `storagename` con un nome univoco per l'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="d7c49-131">Replace `storagename` with a unique name for hello storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="d7c49-132">Per ulteriori informazioni sui parametri hello utilizzati in questo comando, utilizzare `azure storage account create -h` tooview della Guida in linea per questo comando.</span><span class="sxs-lookup"><span data-stu-id="d7c49-132">For more information on hello parameters used in this command, use `azure storage account create -h` tooview help for this command.</span></span>

5. <span data-ttu-id="d7c49-133">Recuperare l'account di archiviazione hello hello chiave tooaccess utilizzato.</span><span class="sxs-lookup"><span data-stu-id="d7c49-133">Retrieve hello key used tooaccess hello storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="d7c49-134">Sostituire `groupname` con nome gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="d7c49-134">Replace `groupname` with hello resource group name.</span></span>
    * <span data-ttu-id="d7c49-135">Sostituire `storagename` con nome hello hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d7c49-135">Replace `storagename` with hello name of hello storage account.</span></span>

     <span data-ttu-id="d7c49-136">Nei dati hello che viene restituiti, salvare hello `key` valore per `key1`.</span><span class="sxs-lookup"><span data-stu-id="d7c49-136">In hello data that is returned, save hello `key` value for `key1`.</span></span>

6. <span data-ttu-id="d7c49-137">Creare un cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7c49-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="d7c49-138">Sostituire `groupname` con nome gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="d7c49-138">Replace `groupname` with hello resource group name.</span></span>

    * <span data-ttu-id="d7c49-139">Sostituire `Hadoop` con tipo di cluster hello che si desidera toocreate.</span><span class="sxs-lookup"><span data-stu-id="d7c49-139">Replace `Hadoop` with hello cluster type that you wish toocreate.</span></span> <span data-ttu-id="d7c49-140">ad esempio, `Hadoop`, `HBase`, `Kafka`, `Spark` o `Storm`.</span><span class="sxs-lookup"><span data-stu-id="d7c49-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="d7c49-141">HDInsight cluster possono essere di vario tipo, che corrispondono a carico di lavoro toohello o tecnologia di hello cluster è ottimizzata per.</span><span class="sxs-lookup"><span data-stu-id="d7c49-141">HDInsight clusters come in various types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="d7c49-142">Non è toocreate alcun metodo supportato per un cluster che combina più tipi, ad esempio Storm e HBase in un cluster.</span><span class="sxs-lookup"><span data-stu-id="d7c49-142">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="d7c49-143">Sostituire `location` con hello nello stesso percorso utilizzato nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="d7c49-143">Replace `location` with hello same location used in previous steps.</span></span>

    * <span data-ttu-id="d7c49-144">Sostituire `storagename` con nome di account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="d7c49-144">Replace `storagename` with hello storage account name.</span></span>

    * <span data-ttu-id="d7c49-145">Sostituire `storagekey` con chiave hello ottenuta nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="d7c49-145">Replace `storagekey` with hello key obtained in hello previous step.</span></span>

    * <span data-ttu-id="d7c49-146">Per hello `--defaultStorageContainer` parametro, utilizzare hello stesso nome che si utilizzi per i cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="d7c49-146">For hello `--defaultStorageContainer` parameter, use hello same name as you are using for hello cluster.</span></span>

    * <span data-ttu-id="d7c49-147">Sostituire `admin` e `httppassword` con nome hello e una password desiderato toouse quando si accede a cluster hello tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d7c49-147">Replace `admin` and `httppassword` with hello name and password you wish toouse when accessing hello cluster through HTTPS.</span></span>

    * <span data-ttu-id="d7c49-148">Sostituire `sshuser` e `sshuserpassword` con hello username e password desiderato toouse quando si accede a cluster hello tramite SSH</span><span class="sxs-lookup"><span data-stu-id="d7c49-148">Replace `sshuser` and `sshuserpassword` with hello username and password you wish toouse when accessing hello cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="d7c49-149">L'esempio precedente crea un cluster con 2 nodi di ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d7c49-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="d7c49-150">È inoltre possibile modificare il numero di hello di nodi di lavoro dopo la creazione del cluster eseguendo le operazioni di ridimensionamento.</span><span class="sxs-lookup"><span data-stu-id="d7c49-150">You can also change hello number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="d7c49-151">Se si prevede di usare più di 32 nodi del ruolo di lavoro, è necessario selezionare una dimensione del nodo head con almeno 8 core e 14 GB di RAM.</span><span class="sxs-lookup"><span data-stu-id="d7c49-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="d7c49-152">È possibile impostare le dimensioni di un nodo head hello utilizzando hello `--headNodeSize` parametro durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="d7c49-152">You can set hello head node size by using hello `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="d7c49-153">Per altre informazioni sulle dimensioni di nodo e i costi associati, vedere [Prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="d7c49-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="d7c49-154">Potrebbe richiedere alcuni minuti per hello cluster creazione processo toofinish.</span><span class="sxs-lookup"><span data-stu-id="d7c49-154">It may take several minutes for hello cluster creation process toofinish.</span></span> <span data-ttu-id="d7c49-155">in genere circa 15.</span><span class="sxs-lookup"><span data-stu-id="d7c49-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="d7c49-156">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="d7c49-156">Troubleshoot</span></span>

<span data-ttu-id="d7c49-157">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="d7c49-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d7c49-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d7c49-158">Next steps</span></span>

<span data-ttu-id="d7c49-159">Ora che la creazione di un cluster HDInsight tramite hello CLI di Azure è stata completata, utilizzare hello seguente come toolearn toowork con il cluster:</span><span class="sxs-lookup"><span data-stu-id="d7c49-159">Now that you have successfully created an HDInsight cluster using hello Azure CLI, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="d7c49-160">Cluster Hadoop</span><span class="sxs-lookup"><span data-stu-id="d7c49-160">Hadoop clusters</span></span>

* [<span data-ttu-id="d7c49-161">Usare Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7c49-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d7c49-162">Usare Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7c49-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="d7c49-163">Usare MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7c49-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="d7c49-164">Cluster HBase</span><span class="sxs-lookup"><span data-stu-id="d7c49-164">HBase clusters</span></span>

* [<span data-ttu-id="d7c49-165">Introduzione a HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7c49-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="d7c49-166">Sviluppare applicazioni Java per HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7c49-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="d7c49-167">Cluster Storm</span><span class="sxs-lookup"><span data-stu-id="d7c49-167">Storm clusters</span></span>

* [<span data-ttu-id="d7c49-168">Sviluppare topologie Java per Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7c49-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="d7c49-169">Usare i componenti di Python in Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7c49-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="d7c49-170">Distribuire e monitorare le topologie con Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d7c49-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
