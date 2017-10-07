---
title: aaaCreate HBase cluster in una rete virtuale - Azure | Documenti Microsoft
description: Introduzione all'uso di HBase in Azure HDInsight. Informazioni su come cluster di HDInsight HBase toocreate nella rete virtuale di Azure.
keywords: 
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 8de8e446-f818-4e61-8fad-e9d38421e80d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 097338a5a650bb607a9f6f9ddb59bb88d098b56f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="0af11-104">Creare cluster HBase su HDInsight nella rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="0af11-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="0af11-105">Informazioni su come toocreate HBase di HDInsight di Azure cluster in un [rete virtuale di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="0af11-105">Learn how toocreate Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="0af11-106">Con l'integrazione di rete virtuale cluster HBase può essere distribuito toohello stessa virtuale rete delle applicazioni in modo che le applicazioni possono comunicare direttamente con HBase.</span><span class="sxs-lookup"><span data-stu-id="0af11-106">With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="0af11-107">Hello vantaggi includono:</span><span class="sxs-lookup"><span data-stu-id="0af11-107">hello benefits include:</span></span>

* <span data-ttu-id="0af11-108">Connettività diretta di hello web applicazione toohello i nodi del cluster HBase di hello, che consente la comunicazione tramite RPC HBase Java chiamare le API (RPC).</span><span class="sxs-lookup"><span data-stu-id="0af11-108">Direct connectivity of hello web application toohello nodes of hello HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="0af11-109">Miglioramento delle prestazioni, poiché il traffico non deve attraversare più gateway e servizi di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="0af11-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="0af11-110">Hello possibilità tooprocess informazioni riservate in modo più sicuro senza esporre un endpoint pubblico.</span><span class="sxs-lookup"><span data-stu-id="0af11-110">hello ability tooprocess sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="0af11-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0af11-111">Prerequisites</span></span>
<span data-ttu-id="0af11-112">Prima di iniziare questa esercitazione, è necessario disporre di hello seguenti elementi:</span><span class="sxs-lookup"><span data-stu-id="0af11-112">Before you begin this tutorial, you must have hello following items:</span></span>

* <span data-ttu-id="0af11-113">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="0af11-113">**An Azure subscription**.</span></span> <span data-ttu-id="0af11-114">Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="0af11-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="0af11-115">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="0af11-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="0af11-116">Vedere [Installare e usare Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="0af11-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="0af11-117">Creare cluster HBase nella rete virtuale</span><span class="sxs-lookup"><span data-stu-id="0af11-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="0af11-118">In questa sezione si crea un cluster HBase basati su Linux con account di archiviazione Azure dipendenti di hello in una rete virtuale di Azure utilizzando un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="0af11-118">In this section, you create a Linux-based HBase cluster with hello dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="0af11-119">Per altri metodi di creazione del cluster e informazioni sulle impostazioni di hello, vedere [cluster HDInsight creare](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="0af11-119">For other cluster creation methods and understanding hello settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="0af11-120">Per ulteriori informazioni sull'utilizzo di un toocreate modello Hadoop cluster in HDInsight, vedere [cluster creare Hadoop in HDInsight mediante modelli di gestione risorse di Azure](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="0af11-120">For more information about using a template toocreate Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="0af11-121">Alcune proprietà sono hardcoded nel modello di hello.</span><span class="sxs-lookup"><span data-stu-id="0af11-121">Some properties are hard-coded into hello template.</span></span> <span data-ttu-id="0af11-122">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0af11-122">For example:</span></span>
>
> * <span data-ttu-id="0af11-123">**Location**: Stati Uniti orientali 2</span><span class="sxs-lookup"><span data-stu-id="0af11-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="0af11-124">**Versione del cluster**: 3.5</span><span class="sxs-lookup"><span data-stu-id="0af11-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="0af11-125">**Cluster worker node count**: 2</span><span class="sxs-lookup"><span data-stu-id="0af11-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="0af11-126">**Default storage account**: stringa univoca</span><span class="sxs-lookup"><span data-stu-id="0af11-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="0af11-127">**Virtual network name**: &lt;Nome cluster&gt;-vnet</span><span class="sxs-lookup"><span data-stu-id="0af11-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="0af11-128">**Virtual network address space**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="0af11-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="0af11-129">**Subnet name**: subnet1</span><span class="sxs-lookup"><span data-stu-id="0af11-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="0af11-130">**Subnet address range**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="0af11-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="0af11-131">&lt;Nome del cluster > viene sostituito con il nome di cluster hello è fornire quando si utilizza il modello di hello.</span><span class="sxs-lookup"><span data-stu-id="0af11-131">&lt;Cluster Name> is replaced with hello cluster name you provide when using hello template.</span></span>
>
>

1. <span data-ttu-id="0af11-132">Fare clic su hello seguente immagine tooopen hello modello hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0af11-132">Click hello following image tooopen hello template in hello Azure portal.</span></span> <span data-ttu-id="0af11-133">modello Hello nella [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="0af11-133">hello template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. <span data-ttu-id="0af11-134">Da hello **distribuzione personalizzata** pannello immettere hello le proprietà seguenti:</span><span class="sxs-lookup"><span data-stu-id="0af11-134">From hello **Custom deployment** blade, enter hello following properties:</span></span>

   * <span data-ttu-id="0af11-135">**Sottoscrizione**: selezionare un cluster di HDInsight hello toocreate sottoscrizione di Azure usata, hello dipendenti account di archiviazione e rete virtuale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0af11-135">**Subscription**: Select an Azure subscription used toocreate hello HDInsight cluster, hello dependent Storage account and hello Azure virtual network.</span></span>
   * <span data-ttu-id="0af11-136">**Gruppo di risorse**: selezionare **Crea nuovo** e assegnare un nome al nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="0af11-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="0af11-137">**Percorso**: selezionare un percorso per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="0af11-137">**Location**: Select a location for hello resource group.</span></span>
   * <span data-ttu-id="0af11-138">**ClusterName**: immettere un nome per toobe di cluster Hadoop hello creato.</span><span class="sxs-lookup"><span data-stu-id="0af11-138">**ClusterName**: Enter a name for hello Hadoop cluster toobe created.</span></span>
   * <span data-ttu-id="0af11-139">**Nome account di accesso e la password del cluster**: nome di account di accesso predefinito hello **admin**.</span><span class="sxs-lookup"><span data-stu-id="0af11-139">**Cluster login name and password**: hello default login name is **admin**.</span></span>
   * <span data-ttu-id="0af11-140">**Nome utente SSH e password**: nome utente predefinito hello **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="0af11-140">**SSH username and password**: hello default username is **sshuser**.</span></span>  <span data-ttu-id="0af11-141">È possibile rinominarlo.</span><span class="sxs-lookup"><span data-stu-id="0af11-141">You can rename it.</span></span>
   * <span data-ttu-id="0af11-142">**Accetto le condizioni di hello indicate in precedenza toohello**: (Select)</span><span class="sxs-lookup"><span data-stu-id="0af11-142">**I agree toohello terms and hello conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="0af11-143">Fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="0af11-143">Click **Purchase**.</span></span> <span data-ttu-id="0af11-144">Dovrà trascorrere circa toocreate circa 20 minuti di un cluster.</span><span class="sxs-lookup"><span data-stu-id="0af11-144">It takes about around 20 minutes toocreate a cluster.</span></span> <span data-ttu-id="0af11-145">Una volta creato il cluster hello, è possibile fare clic su Pannello cluster hello in tooopen portale hello è.</span><span class="sxs-lookup"><span data-stu-id="0af11-145">Once hello cluster is created, you can click hello cluster blade in hello portal tooopen it.</span></span>

<span data-ttu-id="0af11-146">Dopo aver completato l'esercitazione hello, è consigliabile cluster hello toodelete.</span><span class="sxs-lookup"><span data-stu-id="0af11-146">After you complete hello tutorial, you might want toodelete hello cluster.</span></span> <span data-ttu-id="0af11-147">Con HDInsight, i dati vengono archiviati in Archiviazione di Azure ed è possibile eliminare tranquillamente un cluster quando non viene usato.</span><span class="sxs-lookup"><span data-stu-id="0af11-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="0af11-148">Vengono addebitati i costi anche per i cluster HDInsight che non sono in uso.</span><span class="sxs-lookup"><span data-stu-id="0af11-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="0af11-149">Poiché gli addebiti di hello per cluster hello sono spesso più addebiti hello per l'archiviazione, è opportuno economica toodelete cluster quando non sono in uso.</span><span class="sxs-lookup"><span data-stu-id="0af11-149">Since hello charges for hello cluster are many times more than hello charges for storage, it makes economic sense toodelete clusters when they are not in use.</span></span> <span data-ttu-id="0af11-150">Per istruzioni hello di eliminazione di un cluster, vedere [hello di cluster di gestire Hadoop in HDInsight mediante il portale di Azure](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="0af11-150">For hello instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using hello Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="0af11-151">toobegin utilizzo con il nuovo cluster HBase, è possibile utilizzare procedure hello in [informazioni introduttive sull'utilizzo di HBase con Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0af11-151">toobegin working with your new HBase cluster, you can use hello procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-toohello-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="0af11-152">Connettere il cluster di HBase toohello utilizzando le API di HBase Java RPC</span><span class="sxs-lookup"><span data-stu-id="0af11-152">Connect toohello HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="0af11-153">Creazione di un'infrastruttura come servizio (IaaS) macchina virtuale nella stessa rete virtuale hello e hello stessa subnet.</span><span class="sxs-lookup"><span data-stu-id="0af11-153">Create an infrastructure as a service (IaaS) virtual machine into hello same Azure virtual network and hello same subnet.</span></span> <span data-ttu-id="0af11-154">Per le istruzioni su come creare una nuova macchina virtuale IaaS, vedere [Creare una macchina virtuale che esegue Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="0af11-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="0af11-155">Quando hello procedura riportata in questo documento, è necessario utilizzare i seguenti valori per la configurazione di rete hello hello:</span><span class="sxs-lookup"><span data-stu-id="0af11-155">When following hello steps in this document, you must use hello following values for hello Network configuration:</span></span>

   * <span data-ttu-id="0af11-156">**Virtual network**: &lt;Nome cluster&gt;-vnet</span><span class="sxs-lookup"><span data-stu-id="0af11-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="0af11-157">**Subnet**: subnet1</span><span class="sxs-lookup"><span data-stu-id="0af11-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0af11-158">Sostituire &lt;nome Cluster > con nome hello utilizzato per la creazione del cluster HDInsight hello nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="0af11-158">Replace &lt;Cluster name> with hello name you used when creating hello HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="0af11-159">Utilizzando questi valori, hello macchina virtuale viene inserita in hello stessa subnet del cluster HDInsight hello e rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0af11-159">Using these values, hello virtual machine is placed in hello same virtual network and subnet as hello HDInsight cluster.</span></span> <span data-ttu-id="0af11-160">Questa configurazione consente loro toodirectly comunicare tra loro.</span><span class="sxs-lookup"><span data-stu-id="0af11-160">This configuration allows them toodirectly communicate with each other.</span></span> <span data-ttu-id="0af11-161">È un modo toocreate un cluster di HDInsight con un nodo del bordo vuoto.</span><span class="sxs-lookup"><span data-stu-id="0af11-161">There is a way toocreate an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="0af11-162">nodo del bordo Hello può essere cluster hello toomanage utilizzato.</span><span class="sxs-lookup"><span data-stu-id="0af11-162">hello edge node can be used toomanage hello cluster.</span></span>  <span data-ttu-id="0af11-163">Per altre informazioni, vedere [Usare nodi perimetrali vuoti in HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="0af11-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="0af11-164">Quando si utilizza un tooHBase tooconnect di applicazione Java in modalità remota, è necessario utilizzare il nome di dominio completo hello (FQDN).</span><span class="sxs-lookup"><span data-stu-id="0af11-164">When using a Java application tooconnect tooHBase remotely, you must use hello fully qualified domain name (FQDN).</span></span> <span data-ttu-id="0af11-165">toodetermine, è necessario ottenere suffisso DNS specifico della connessione di hello dei cluster HBase hello.</span><span class="sxs-lookup"><span data-stu-id="0af11-165">toodetermine this, you must get hello connection-specific DNS suffix of hello HBase cluster.</span></span> <span data-ttu-id="0af11-166">toodo, che è possibile utilizzare uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="0af11-166">toodo that, you can use one of hello following methods:</span></span>

   * <span data-ttu-id="0af11-167">Utilizzare un toomake browser Web chiamata Ambari:</span><span class="sxs-lookup"><span data-stu-id="0af11-167">Use a Web browser toomake an Ambari call:</span></span>

     <span data-ttu-id="0af11-168">Sfoglia toohttps: / /&lt;ClusterName >.azurehdinsight.net/api/v1/clusters/&lt;ClusterName > / ospita? minimal_response = true.</span><span class="sxs-lookup"><span data-stu-id="0af11-168">Browse toohttps://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="0af11-169">Verrà utilizzato un file JSON con i suffissi DNS hello.</span><span class="sxs-lookup"><span data-stu-id="0af11-169">It turns a JSON file with hello DNS suffixes.</span></span>
   * <span data-ttu-id="0af11-170">Usare Ambari hello:</span><span class="sxs-lookup"><span data-stu-id="0af11-170">Use hello Ambari website:</span></span>

     1. <span data-ttu-id="0af11-171">Sfoglia troppo https://&lt;ClusterName >. cluster>.azurehdinsight.NET.</span><span class="sxs-lookup"><span data-stu-id="0af11-171">Browse too https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="0af11-172">Fare clic su **host** menu principale di hello.</span><span class="sxs-lookup"><span data-stu-id="0af11-172">Click **Hosts** from hello top menu.</span></span>
   * <span data-ttu-id="0af11-173">Utilizzare le chiamate REST toomake Curl:</span><span class="sxs-lookup"><span data-stu-id="0af11-173">Use Curl toomake REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="0af11-174">Trovare la voce "host_name" hello in hello restituiti i dati di JavaScript Object Notation (JSON).</span><span class="sxs-lookup"><span data-stu-id="0af11-174">In hello JavaScript Object Notation (JSON) data returned, find hello "host_name" entry.</span></span> <span data-ttu-id="0af11-175">Contiene hello FQDN per i nodi nel cluster hello hello.</span><span class="sxs-lookup"><span data-stu-id="0af11-175">It contains hello FQDN for hello nodes in hello cluster.</span></span> <span data-ttu-id="0af11-176">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0af11-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="0af11-177">Hello di hello dominio nome che inizia con il nome del cluster hello è il suffisso DNS hello.</span><span class="sxs-lookup"><span data-stu-id="0af11-177">hello portion of hello domain name beginning with hello cluster name is hello DNS suffix.</span></span> <span data-ttu-id="0af11-178">Ad esempio, mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="0af11-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="0af11-179">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0af11-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="0af11-180">Hello utilizzare seguente hello tooregister script di PowerShell Azure **Get ClusterDetail** funzione, che può essere utilizzato tooreturn hello DNS suffisso:</span><span class="sxs-lookup"><span data-stu-id="0af11-180">Use hello following Azure PowerShell script tooregister hello **Get-ClusterDetail** function, which can be used tooreturn hello DNS suffix:</span></span>

    ```powershell
        function Get-ClusterDetail(
            [String]
            [Parameter( Position=0, Mandatory=$true )]
            $ClusterDnsName,
            [String]
            [Parameter( Position=1, Mandatory=$true )]
            $Username,
            [String]
            [Parameter( Position=2, Mandatory=$true )]
            $Password,
            [String]
            [Parameter( Position=3, Mandatory=$true )]
            $PropertyName
            )
        {
        <#
            .SYNOPSIS
            Displays information toofacilitate an HDInsight cluster-to-cluster scenario within hello same virtual network.
            .Description
            This command shows hello following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run hello HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows hello FQDN suffix of hosts in hello cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows hello value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows hello value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run hello HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows hello FQDN suffix of hosts in hello cluster.
        #>

            $DnsSuffix = ".azurehdinsight.net"

            $ClusterFQDN = $ClusterDnsName + $DnsSuffix
            $webclient = new-object System.Net.WebClient
            $webclient.Credentials = new-object System.Net.NetworkCredential($Username, $Password)

            if($PropertyName -eq "ZookeeperQuorum")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.quorum"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.quorum'
            }
            if($PropertyName -eq "ZookeeperClientPort")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.zookeeper.property.clientPort"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                Write-host $JsonObject.items[0].properties.'hbase.zookeeper.property.clientPort'
            }
            if($PropertyName -eq "HBaseRestServers")
            {
                $Url1 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/configurations?type=hbase-site&tag=default&fields=items/properties/hbase.rest.port"
                $Response1 = $webclient.DownloadString($Url1)
                $JsonObject1 = $Response1 | ConvertFrom-Json
                $PortNumber = $JsonObject1.items[0].properties.'hbase.rest.port'

                $Url2 = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/hbase/components/hbrest"
                $Response2 = $webclient.DownloadString($Url2)
                $JsonObject2 = $Response2 | ConvertFrom-Json
                foreach ($host_component in $JsonObject2.host_components)
                {
                    $ConnectionString = $host_component.HostRoles.host_name + ":" + $PortNumber
                    Write-host $ConnectionString
                }
            }
            if($PropertyName -eq "FQDNSuffix")
            {
                $Url = "https://" + $ClusterFQDN + "/ambari/api/v1/clusters/" + $ClusterFQDN + "/services/YARN/components/RESOURCEMANAGER"
                $Response = $webclient.DownloadString($Url)
                $JsonObject = $Response | ConvertFrom-Json
                $FQDN = $JsonObject.host_components[0].HostRoles.host_name
                $pos = $FQDN.IndexOf(".")
                $Suffix = $FQDN.Substring($pos + 1)
                Write-host $Suffix
            }
        }
    ```

     <span data-ttu-id="0af11-181">Dopo l'esecuzione di uno script Azure PowerShell hello, utilizzare hello comando che segue il suffisso DNS hello tooreturn utilizzando hello **Get ClusterDetail** (funzione).</span><span class="sxs-lookup"><span data-stu-id="0af11-181">After running hello Azure PowerShell script, use hello following command tooreturn hello DNS suffix by using hello **Get-ClusterDetail** function.</span></span> <span data-ttu-id="0af11-182">Quando si usa il comando, specificare il nome del cluster HBase di HDInsight e il nome e la password dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="0af11-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="0af11-183">Questo comando restituisce il suffisso DNS hello.</span><span class="sxs-lookup"><span data-stu-id="0af11-183">This command returns hello DNS suffix.</span></span> <span data-ttu-id="0af11-184">Ad esempio, **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="0af11-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change hello primary DNS suffix configuration of hello virtual machine. This enables hello virtual machine tooautomatically resolve hello host name of hello HBase cluster without explicit specification of hello suffix. For example, hello *workernode0* host name will be correctly resolved tooworkernode0 of hello HBase cluster.

    toomake hello configuration change:

    1. RDP into hello virtual machine.
    2. Open **Local Group Policy Editor**. hello executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** toohello value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot hello virtual machine.
-->

<span data-ttu-id="0af11-185">tooverify che hello macchina virtuale possono comunicare con hello cluster HBase, utilizzare il comando hello `ping headnode0.<dns suffix>` dalla macchina virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="0af11-185">tooverify that hello virtual machine can communicate with hello HBase cluster, use hello command `ping headnode0.<dns suffix>` from hello virtual machine.</span></span> <span data-ttu-id="0af11-186">Ad esempio, eseguire il ping di headnode0.mycluster.b1.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="0af11-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="0af11-187">toouse queste informazioni in un'applicazione Java, è possibile seguire i passaggi di hello in [utilizzare Maven toobuild Java le applicazioni che utilizzano HBase di HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="0af11-187">toouse this information in a Java application, you can follow hello steps in [Use Maven toobuild Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) toocreate an application.</span></span> <span data-ttu-id="0af11-188">un'applicazione hello toohave connettere tooa remoto HBase server, modificare hello **hbase-Site.XML** file in questo hello toouse esempio FQDN per Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="0af11-188">toohave hello application connect tooa remote HBase server, modify hello **hbase-site.xml** file in this example toouse hello FQDN for Zookeeper.</span></span> <span data-ttu-id="0af11-189">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="0af11-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="0af11-190">Per ulteriori informazioni sulla risoluzione dei nomi in reti virtuali di Azure, compresa la modalità toouse il proprio server DNS, vedere [risoluzione DNS (Name)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="0af11-190">For more information about name resolution in Azure virtual networks, including how toouse your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="0af11-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0af11-191">Next steps</span></span>
<span data-ttu-id="0af11-192">In questa esercitazione, si è appreso come un cluster HBase toocreate.</span><span class="sxs-lookup"><span data-stu-id="0af11-192">In this tutorial, you learned how toocreate an HBase cluster.</span></span> <span data-ttu-id="0af11-193">toolearn informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="0af11-193">toolearn more, see:</span></span>

* [<span data-ttu-id="0af11-194">Introduzione all'uso di HDInsight</span><span class="sxs-lookup"><span data-stu-id="0af11-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="0af11-195">Usare nodi perimetrali vuoti in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0af11-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="0af11-196">Configurare la replica di HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0af11-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="0af11-197">Creare cluster Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0af11-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="0af11-198">Introduzione all'uso di HBase con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0af11-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="0af11-199">Analizzare i sentimenti Twitter con HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0af11-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="0af11-200">[Panoramica di Rete virtuale][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="0af11-200">[Virtual Network Overview][vnet-overview]</span></span>

[1]: http://azure.microsoft.com/services/virtual-network/
[2]: http://technet.microsoft.com/library/ee176961.aspx
[3]: http://technet.microsoft.com/library/hh847889.aspx

[hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[vnet-overview]: ../virtual-network/virtual-networks-overview.md
[vm-create]: ../virtual-machines/virtual-machines-windows-hero-tutorial.md

[azure-portal]: https://portal.azure.com
[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp

[hdinsight-powershell-reference]: https://msdn.microsoft.com/library/dn858087.aspx


[twitter-streaming-api]: https://dev.twitter.com/docs/streaming-apis
[twitter-statuses-filter]: https://dev.twitter.com/docs/api/1.1/post/statuses/filter


[powershell-install]: /powershell/azureps-cmdlets-docs


[hdinsight-customize-cluster]: hdinsight-hadoop-customize-cluster.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage-powershell]: ../hdinsight-hadoop-use-blob-storage.md#powershell
[hdinsight-analyze-flight-delay-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-power-query]: hdinsight-connect-excel-power-query.md
[hdinsight-hive-odbc]: hdinsight-connect-excel-hive-ODBC-driver.md
[hdinsight-hbase-replication-dns]: hdinsight-hbase-geo-replication-configure-DNS.md

[img-dns-surffix]: ./media/hdinsight-hbase-provision-vnet/DNSSuffix.png
[img-primary-dns-suffix]: ./media/hdinsight-hbase-provision-vnet/PrimaryDNSSuffix.png
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Dettagli di provisioning per il nuovo cluster di HBase hello"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Utilizzare l'azione Script toocustomize un cluster HBase"

[azure-preview-portal]: https://portal.azure.com
