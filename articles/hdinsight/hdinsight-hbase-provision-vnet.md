---
title: Creare cluster HBase in una rete virtuale | Microsoft Docs
description: Introduzione all'uso di HBase in Azure HDInsight. Informazioni su come creare cluster HBase di HDInsight in Rete virtuale di Azure.
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
ms.openlocfilehash: 668bd494ce3274188af56cf7d6253cec7af9abbc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-hbase-clusters-on-hdinsight-in-azure-virtual-network"></a><span data-ttu-id="77ad8-104">Creare cluster HBase su HDInsight nella rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="77ad8-104">Create HBase clusters on HDInsight in Azure Virtual Network</span></span>
<span data-ttu-id="77ad8-105">Informazioni su come creare cluster HBase in Azure HDInsight in una [Rete virtuale di Azure][1].</span><span class="sxs-lookup"><span data-stu-id="77ad8-105">Learn how to create Azure HDInsight HBase clusters in an [Azure Virtual Network][1].</span></span>

<span data-ttu-id="77ad8-106">Grazie all'integrazione con la rete virtuale, i cluster HBase possono essere distribuiti nella stessa rete virtuale delle applicazioni, consentendo così alle applicazioni di comunicare direttamente con HBase.</span><span class="sxs-lookup"><span data-stu-id="77ad8-106">With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span> <span data-ttu-id="77ad8-107">Questo approccio offre i vantaggi seguenti:</span><span class="sxs-lookup"><span data-stu-id="77ad8-107">The benefits include:</span></span>

* <span data-ttu-id="77ad8-108">Connettività diretta dell'applicazione Web con i nodi del cluster HBase, che consente le comunicazioni tramite le API RPC (Remote Procedure Call) Java di HBase.</span><span class="sxs-lookup"><span data-stu-id="77ad8-108">Direct connectivity of the web application to the nodes of the HBase cluster, which enables communication via HBase Java remote procedure call (RPC) APIs.</span></span>
* <span data-ttu-id="77ad8-109">Miglioramento delle prestazioni, poiché il traffico non deve attraversare più gateway e servizi di bilanciamento del carico.</span><span class="sxs-lookup"><span data-stu-id="77ad8-109">Improved performance by not having your traffic go over multiple gateways and load-balancers.</span></span>
* <span data-ttu-id="77ad8-110">Possibilità di elaborare le informazioni sensibili in modo più sicuro, senza esporre un endpoint pubblico.</span><span class="sxs-lookup"><span data-stu-id="77ad8-110">The ability to process sensitive information in a more secure manner without exposing a public endpoint.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="77ad8-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="77ad8-111">Prerequisites</span></span>
<span data-ttu-id="77ad8-112">Prima di iniziare questa esercitazione sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="77ad8-112">Before you begin this tutorial, you must have the following items:</span></span>

* <span data-ttu-id="77ad8-113">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="77ad8-113">**An Azure subscription**.</span></span> <span data-ttu-id="77ad8-114">Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="77ad8-114">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="77ad8-115">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="77ad8-115">**A workstation with Azure PowerShell**.</span></span> <span data-ttu-id="77ad8-116">Vedere [Installare e usare Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span><span class="sxs-lookup"><span data-stu-id="77ad8-116">See [Install and use Azure PowerShell](https://azure.microsoft.com/documentation/videos/install-and-use-azure-powershell/).</span></span>

## <a name="create-hbase-cluster-into-virtual-network"></a><span data-ttu-id="77ad8-117">Creare cluster HBase nella rete virtuale</span><span class="sxs-lookup"><span data-stu-id="77ad8-117">Create HBase cluster into virtual network</span></span>
<span data-ttu-id="77ad8-118">In questa sezione viene creato un cluster HBase basato su Linux con l'account di archiviazione di Azure dipendente in una rete virtuale di Azure tramite un [modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="77ad8-118">In this section, you create a Linux-based HBase cluster with the dependent Azure Storage account in an Azure virtual network using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="77ad8-119">Per altri metodi di creazione di cluster e per informazioni sulle impostazioni, vedere l'articolo sulla [creazione di cluster HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="77ad8-119">For other cluster creation methods and understanding the settings, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span> <span data-ttu-id="77ad8-120">Per altre informazioni sull'uso di un modello per creare cluster Hadoop in HDInsight, vedere l'articolo relativo alla [creazione di cluster Hadoop in HDInsight tramite modelli di Azure Resource Manager](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span><span class="sxs-lookup"><span data-stu-id="77ad8-120">For more information about using a template to create Hadoop clusters in HDInsight, see [Create Hadoop clusters in HDInsight using Azure Resource Manager templates](hdinsight-hadoop-create-windows-clusters-arm-templates.md)</span></span>

> [!NOTE]
> <span data-ttu-id="77ad8-121">Alcune proprietà sono state impostate come hardcoded nel modello.</span><span class="sxs-lookup"><span data-stu-id="77ad8-121">Some properties are hard-coded into the template.</span></span> <span data-ttu-id="77ad8-122">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="77ad8-122">For example:</span></span>
>
> * <span data-ttu-id="77ad8-123">**Location**: Stati Uniti orientali 2</span><span class="sxs-lookup"><span data-stu-id="77ad8-123">**Location**: East US 2</span></span>
> * <span data-ttu-id="77ad8-124">**Versione del cluster**: 3.5</span><span class="sxs-lookup"><span data-stu-id="77ad8-124">**Cluster version**: 3.5</span></span>
> * <span data-ttu-id="77ad8-125">**Cluster worker node count**: 2</span><span class="sxs-lookup"><span data-stu-id="77ad8-125">**Cluster worker node count**: 2</span></span>
> * <span data-ttu-id="77ad8-126">**Default storage account**: stringa univoca</span><span class="sxs-lookup"><span data-stu-id="77ad8-126">**Default storage account**: a unique string</span></span>
> * <span data-ttu-id="77ad8-127">**Virtual network name**: &lt;Nome cluster>-vnet</span><span class="sxs-lookup"><span data-stu-id="77ad8-127">**Virtual network name**: &lt;Cluster Name>-vnet</span></span>
> * <span data-ttu-id="77ad8-128">**Virtual network address space**: 10.0.0.0/16</span><span class="sxs-lookup"><span data-stu-id="77ad8-128">**Virtual network address space**: 10.0.0.0/16</span></span>
> * <span data-ttu-id="77ad8-129">**Subnet name**: subnet1</span><span class="sxs-lookup"><span data-stu-id="77ad8-129">**Subnet name**: subnet1</span></span>
> * <span data-ttu-id="77ad8-130">**Subnet address range**: 10.0.0.0/24</span><span class="sxs-lookup"><span data-stu-id="77ad8-130">**Subnet address range**: 10.0.0.0/24</span></span>
>
> <span data-ttu-id="77ad8-131">&lt;Cluster Name > viene sostituito con il nome del cluster fornito quando si usa il modello.</span><span class="sxs-lookup"><span data-stu-id="77ad8-131">&lt;Cluster Name> is replaced with the cluster name you provide when using the template.</span></span>
>
>

1. <span data-ttu-id="77ad8-132">Fare clic sull'immagine seguente per aprire il modello nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="77ad8-132">Click the following image to open the template in the Azure portal.</span></span> <span data-ttu-id="77ad8-133">Il modello è disponibile tra i [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span><span class="sxs-lookup"><span data-stu-id="77ad8-133">The template is located in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-linux-vnet/).</span></span>

    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-provision-vnet/deploy-to-azure.png" alt="Deploy to Azure"></a>
2. <span data-ttu-id="77ad8-134">Inserire le proprietà seguenti dal pannello **Distribuzione personalizzata**:</span><span class="sxs-lookup"><span data-stu-id="77ad8-134">From the **Custom deployment** blade, enter the following properties:</span></span>

   * <span data-ttu-id="77ad8-135">**Sottoscrizione**: selezionare una sottoscrizione di Azure usata per creare il cluster HDInsight, l'account di archiviazione dipendente e la rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="77ad8-135">**Subscription**: Select an Azure subscription used to create the HDInsight cluster, the dependent Storage account and the Azure virtual network.</span></span>
   * <span data-ttu-id="77ad8-136">**Gruppo di risorse**: selezionare **Crea nuovo** e assegnare un nome al nuovo gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="77ad8-136">**Resource group**: Select **Create new**, and specify a new resource group name.</span></span>
   * <span data-ttu-id="77ad8-137">**Posizione**: selezionare una posizione per il gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="77ad8-137">**Location**: Select a location for the resource group.</span></span>
   * <span data-ttu-id="77ad8-138">**ClusterName**: immettere un nome per il cluster Hadoop da creare.</span><span class="sxs-lookup"><span data-stu-id="77ad8-138">**ClusterName**: Enter a name for the Hadoop cluster to be created.</span></span>
   * <span data-ttu-id="77ad8-139">**Cluster login name and password**: il nome dell'account di accesso predefinito è **admin**.</span><span class="sxs-lookup"><span data-stu-id="77ad8-139">**Cluster login name and password**: The default login name is **admin**.</span></span>
   * <span data-ttu-id="77ad8-140">**SSH username and password**: il nome utente predefinito è **sshuser**.</span><span class="sxs-lookup"><span data-stu-id="77ad8-140">**SSH username and password**: The default username is **sshuser**.</span></span>  <span data-ttu-id="77ad8-141">È possibile rinominarlo.</span><span class="sxs-lookup"><span data-stu-id="77ad8-141">You can rename it.</span></span>
   * <span data-ttu-id="77ad8-142">**Accetto le condizioni riportate sopra**: (selezionare)</span><span class="sxs-lookup"><span data-stu-id="77ad8-142">**I agree to the terms and the conditions stated above**: (Select)</span></span>
3. <span data-ttu-id="77ad8-143">Fare clic su **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="77ad8-143">Click **Purchase**.</span></span> <span data-ttu-id="77ad8-144">La creazione di un cluster richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="77ad8-144">It takes about around 20 minutes to create a cluster.</span></span> <span data-ttu-id="77ad8-145">Dopo aver creato il cluster, è possibile fare clic sul pannello del cluster nel portale per aprirlo.</span><span class="sxs-lookup"><span data-stu-id="77ad8-145">Once the cluster is created, you can click the cluster blade in the portal to open it.</span></span>

<span data-ttu-id="77ad8-146">Al termine dell'esercitazione, è consigliabile eliminare il cluster.</span><span class="sxs-lookup"><span data-stu-id="77ad8-146">After you complete the tutorial, you might want to delete the cluster.</span></span> <span data-ttu-id="77ad8-147">Con HDInsight, i dati vengono archiviati in Archiviazione di Azure ed è possibile eliminare tranquillamente un cluster quando non viene usato.</span><span class="sxs-lookup"><span data-stu-id="77ad8-147">With HDInsight, your data is stored in Azure Storage, so you can safely delete a cluster when it is not in use.</span></span> <span data-ttu-id="77ad8-148">Vengono addebitati i costi anche per i cluster HDInsight che non sono in uso.</span><span class="sxs-lookup"><span data-stu-id="77ad8-148">You are also charged for an HDInsight cluster, even when it is not in use.</span></span> <span data-ttu-id="77ad8-149">Poiché i costi per il cluster sono decisamente superiori a quelli per l'archiviazione, economicamente ha senso eliminare i cluster quando non vengono usati.</span><span class="sxs-lookup"><span data-stu-id="77ad8-149">Since the charges for the cluster are many times more than the charges for storage, it makes economic sense to delete clusters when they are not in use.</span></span> <span data-ttu-id="77ad8-150">Per istruzioni sull'eliminazione di un cluster, vedere [Gestire cluster Hadoop in HDInsight tramite il portale di Azure](hdinsight-administer-use-management-portal.md#delete-clusters).</span><span class="sxs-lookup"><span data-stu-id="77ad8-150">For the instructions of deleting a cluster, see [Manage Hadoop clusters in HDInsight by using the Azure portal](hdinsight-administer-use-management-portal.md#delete-clusters).</span></span>

<span data-ttu-id="77ad8-151">Per iniziare a lavorare con il nuovo cluster HBase, è possibile usare le procedure disponibili in [Introduzione a HBase con Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="77ad8-151">To begin working with your new HBase cluster, you can use the procedures found in [Get started using HBase with Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started.md).</span></span>

## <a name="connect-to-the-hbase-cluster-using-hbase-java-rpc-apis"></a><span data-ttu-id="77ad8-152">Connettersi al cluster HBase tramite le API RPC Java di HBase</span><span class="sxs-lookup"><span data-stu-id="77ad8-152">Connect to the HBase cluster using HBase Java RPC APIs</span></span>
1. <span data-ttu-id="77ad8-153">Creare una macchina virtuale IaaS (Infrastructure as a Service) nella stessa rete virtuale di Azure e nella stessa subnet.</span><span class="sxs-lookup"><span data-stu-id="77ad8-153">Create an infrastructure as a service (IaaS) virtual machine into the same Azure virtual network and the same subnet.</span></span> <span data-ttu-id="77ad8-154">Per le istruzioni su come creare una nuova macchina virtuale IaaS, vedere [Creare una macchina virtuale che esegue Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span><span class="sxs-lookup"><span data-stu-id="77ad8-154">For instructions on creating a new IaaS virtual machine, see [Create a Virtual Machine Running Windows Server](../virtual-machines/virtual-machines-windows-hero-tutorial.md).</span></span> <span data-ttu-id="77ad8-155">Quando si usa la procedura indicata in questo documento, è necessario inserire i valori seguenti per la configurazione di rete:</span><span class="sxs-lookup"><span data-stu-id="77ad8-155">When following the steps in this document, you must use the following values for the Network configuration:</span></span>

   * <span data-ttu-id="77ad8-156">**Virtual network**: &lt;Nome cluster>-vnet</span><span class="sxs-lookup"><span data-stu-id="77ad8-156">**Virtual network**: &lt;Cluster name>-vnet</span></span>
   * <span data-ttu-id="77ad8-157">**Subnet**: subnet1</span><span class="sxs-lookup"><span data-stu-id="77ad8-157">**Subnet**: subnet1</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="77ad8-158">Sostituire &lt;Nome cluster> con il nome usato durante la creazione del cluster HDInsight nei passaggi precedenti.</span><span class="sxs-lookup"><span data-stu-id="77ad8-158">Replace &lt;Cluster name> with the name you used when creating the HDInsight cluster in previous steps.</span></span>
   >
   >

   <span data-ttu-id="77ad8-159">Applicando questi valori, la macchina virtuale viene configurata nella stessa rete virtuale e subnet del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="77ad8-159">Using these values, the virtual machine is placed in the same virtual network and subnet as the HDInsight cluster.</span></span> <span data-ttu-id="77ad8-160">Ciò consente la comunicazione bidirezionale diretta.</span><span class="sxs-lookup"><span data-stu-id="77ad8-160">This configuration allows them to directly communicate with each other.</span></span> <span data-ttu-id="77ad8-161">È possibile creare un cluster HDInsight con un nodo perimetrale vuoto.</span><span class="sxs-lookup"><span data-stu-id="77ad8-161">There is a way to create an HDInsight cluster with an empty edge node.</span></span> <span data-ttu-id="77ad8-162">Il nodo perimetrale può essere usato per gestire il cluster.</span><span class="sxs-lookup"><span data-stu-id="77ad8-162">The edge node can be used to manage the cluster.</span></span>  <span data-ttu-id="77ad8-163">Per altre informazioni, vedere [Usare nodi perimetrali vuoti in HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="77ad8-163">For more information, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>

2. <span data-ttu-id="77ad8-164">Quando si usa un'applicazione Java per connettersi a HBase da remoto, è necessario usare il nome di dominio completo (FQDN).</span><span class="sxs-lookup"><span data-stu-id="77ad8-164">When using a Java application to connect to HBase remotely, you must use the fully qualified domain name (FQDN).</span></span> <span data-ttu-id="77ad8-165">Per determinare quest'ultimo, è necessario ottenere il suffisso DNS specifico della connessione del cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="77ad8-165">To determine this, you must get the connection-specific DNS suffix of the HBase cluster.</span></span> <span data-ttu-id="77ad8-166">A questo scopo, è possibile usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="77ad8-166">To do that, you can use one of the following methods:</span></span>

   * <span data-ttu-id="77ad8-167">Usare un Web browser per effettuare una chiamata Ambari:</span><span class="sxs-lookup"><span data-stu-id="77ad8-167">Use a Web browser to make an Ambari call:</span></span>

     <span data-ttu-id="77ad8-168">Passare a https://&lt;Nome cluster>.azurehdinsight.net/api/v1/clusters/&lt;Nome cluster>/hosts?minimal_response=true.</span><span class="sxs-lookup"><span data-stu-id="77ad8-168">Browse to https://&lt;ClusterName>.azurehdinsight.net/api/v1/clusters/&lt;ClusterName>/hosts?minimal_response=true.</span></span> <span data-ttu-id="77ad8-169">Viene restituito un file JSON con i suffissi DNS.</span><span class="sxs-lookup"><span data-stu-id="77ad8-169">It turns a JSON file with the DNS suffixes.</span></span>
   * <span data-ttu-id="77ad8-170">Usare il sito Web Ambari:</span><span class="sxs-lookup"><span data-stu-id="77ad8-170">Use the Ambari website:</span></span>

     1. <span data-ttu-id="77ad8-171">Passare a https://&lt;Nome cluster>.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="77ad8-171">Browse to  https://&lt;ClusterName>.azurehdinsight.net.</span></span>
     2. <span data-ttu-id="77ad8-172">Scegliere **Host** dal menu in alto.</span><span class="sxs-lookup"><span data-stu-id="77ad8-172">Click **Hosts** from the top menu.</span></span>
   * <span data-ttu-id="77ad8-173">Usare Curl per effettuare chiamate REST:</span><span class="sxs-lookup"><span data-stu-id="77ad8-173">Use Curl to make REST calls:</span></span>

    ```bash
        curl -u <username>:<password> -k https://<clustername>.azurehdinsight.net/ambari/api/v1/clusters/<clustername>.azurehdinsight.net/services/hbase/components/hbrest
    ```

     <span data-ttu-id="77ad8-174">Nei dati JSON (JavaScript Object Notation) restituiti, trovare la voce "host_name".</span><span class="sxs-lookup"><span data-stu-id="77ad8-174">In the JavaScript Object Notation (JSON) data returned, find the "host_name" entry.</span></span> <span data-ttu-id="77ad8-175">Contiene il nome di dominio completo (FQDN) per i nodi nel cluster.</span><span class="sxs-lookup"><span data-stu-id="77ad8-175">It contains the FQDN for the nodes in the cluster.</span></span> <span data-ttu-id="77ad8-176">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="77ad8-176">For example:</span></span>

         ...
         "host_name": "wordkernode0.<clustername>.b1.cloudapp.net
         ...

     <span data-ttu-id="77ad8-177">La porzione del nome di dominio che inizia con il nome del cluster è il suffisso DNS.</span><span class="sxs-lookup"><span data-stu-id="77ad8-177">The portion of the domain name beginning with the cluster name is the DNS suffix.</span></span> <span data-ttu-id="77ad8-178">Ad esempio, mycluster.b1.cloudapp.net.</span><span class="sxs-lookup"><span data-stu-id="77ad8-178">For example, mycluster.b1.cloudapp.net.</span></span>
   * <span data-ttu-id="77ad8-179">Uso di Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="77ad8-179">Use Azure PowerShell</span></span>

     <span data-ttu-id="77ad8-180">Usare lo script di Azure PowerShell seguente per registrare la funzione **Get-ClusterDetail**, che può essere usata per restituire il suffisso DNS:</span><span class="sxs-lookup"><span data-stu-id="77ad8-180">Use the following Azure PowerShell script to register the **Get-ClusterDetail** function, which can be used to return the DNS suffix:</span></span>

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
            Displays information to facilitate an HDInsight cluster-to-cluster scenario within the same virtual network.
            .Description
            This command shows the following 4 properties of an HDInsight cluster:
            1. ZookeeperQuorum (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.quorum".
            2. ZookeeperClientPort (supports only HBase type cluster)
                Shows the value of HBase property "hbase.zookeeper.property.clientPort".
            3. HBaseRestServers (supports only HBase type cluster)
                Shows a list of host FQDNs that run the HBase REST server.
            4. FQDNSuffix (supports all cluster types)
                Shows the FQDN suffix of hosts in the cluster.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperQuorum
            This command shows the value of HBase property "hbase.zookeeper.quorum".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName ZookeeperClientPort
            This command shows the value of HBase property "hbase.zookeeper.property.clientPort".
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName HBaseRestServers
            This command shows a list of host FQDNs that run the HBase REST server.
            .EXAMPLE
            Get-ClusterDetail -ClusterDnsName {clusterDnsName} -Username {username} -Password {password} -PropertyName FQDNSuffix
            This command shows the FQDN suffix of hosts in the cluster.
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

     <span data-ttu-id="77ad8-181">Dopo l'esecuzione dello script di Azure PowerShell, usare il comando seguente per restituire il suffisso DNS tramite la funzione **Get-ClusterDetail**.</span><span class="sxs-lookup"><span data-stu-id="77ad8-181">After running the Azure PowerShell script, use the following command to return the DNS suffix by using the **Get-ClusterDetail** function.</span></span> <span data-ttu-id="77ad8-182">Quando si usa il comando, specificare il nome del cluster HBase di HDInsight e il nome e la password dell'amministratore.</span><span class="sxs-lookup"><span data-stu-id="77ad8-182">Specify your HDInsight HBase cluster name, admin name, and admin password when using this command.</span></span>

    ```powershell
        Get-ClusterDetail -ClusterDnsName <yourclustername> -PropertyName FQDNSuffix -Username <clusteradmin> -Password <clusteradminpassword>
    ```

     <span data-ttu-id="77ad8-183">Questo comando restituisce il suffisso DNS.</span><span class="sxs-lookup"><span data-stu-id="77ad8-183">This command returns the DNS suffix.</span></span> <span data-ttu-id="77ad8-184">Ad esempio, **yourclustername.b4.internal.cloudapp.net**.</span><span class="sxs-lookup"><span data-stu-id="77ad8-184">For example, **yourclustername.b4.internal.cloudapp.net**.</span></span>


<!--
3.    Change the primary DNS suffix configuration of the virtual machine. This enables the virtual machine to automatically resolve the host name of the HBase cluster without explicit specification of the suffix. For example, the *workernode0* host name will be correctly resolved to workernode0 of the HBase cluster.

    To make the configuration change:

    1. RDP into the virtual machine.
    2. Open **Local Group Policy Editor**. The executable is gpedit.msc.
    3. Expand **Computer Configuration**, expand **Administrative Templates**, expand **Network**, and then click **DNS Client**.
    - Set **Primary DNS Suffix** to the value obtained in step 2:

        ![hdinsight.hbase.primary.dns.suffix][img-primary-dns-suffix]
    4. Click **OK**.
    5. Reboot the virtual machine.
-->

<span data-ttu-id="77ad8-185">Per verificare che la macchina virtuale possa comunicare con il cluster HBase, usare il comando `ping headnode0.<dns suffix>` dalla macchina virtuale.</span><span class="sxs-lookup"><span data-stu-id="77ad8-185">To verify that the virtual machine can communicate with the HBase cluster, use the command `ping headnode0.<dns suffix>` from the virtual machine.</span></span> <span data-ttu-id="77ad8-186">Ad esempio, eseguire il ping di headnode0.mycluster.b1.cloudapp.net</span><span class="sxs-lookup"><span data-stu-id="77ad8-186">For example, ping headnode0.mycluster.b1.cloudapp.net.</span></span>

<span data-ttu-id="77ad8-187">Per usare queste informazioni in un'applicazione Java e creare un'applicazione, è possibile seguire i passaggi in [Usare Maven per compilare applicazioni Java che usano HBase con HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) .</span><span class="sxs-lookup"><span data-stu-id="77ad8-187">To use this information in a Java application, you can follow the steps in [Use Maven to build Java applications that use HBase with HDInsight (Hadoop)](hdinsight-hbase-build-java-maven.md) to create an application.</span></span> <span data-ttu-id="77ad8-188">Per fare in modo che l'applicazione si connetta a un server HBase remoto, modificare il file **hbase-site.xml** in questo esempio, in modo che usi il nome di dominio completo (FQDN) per Zookeeper.</span><span class="sxs-lookup"><span data-stu-id="77ad8-188">To have the application connect to a remote HBase server, modify the **hbase-site.xml** file in this example to use the FQDN for Zookeeper.</span></span> <span data-ttu-id="77ad8-189">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="77ad8-189">For example:</span></span>

    <property>
        <name>hbase.zookeeper.quorum</name>
        <value>zookeeper0.<dns suffix>,zookeeper1.<dns suffix>,zookeeper2.<dns suffix></value>
    </property>

> [!NOTE]
> <span data-ttu-id="77ad8-190">Per altre informazioni sulla risoluzione dei nomi in reti virtuali di Azure, comprese quelle relative all'uso del proprio server DNS, vedere [Risoluzione dei nomi (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span><span class="sxs-lookup"><span data-stu-id="77ad8-190">For more information about name resolution in Azure virtual networks, including how to use your own DNS server, see [Name Resolution (DNS)](../virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances.md).</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="77ad8-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="77ad8-191">Next steps</span></span>
<span data-ttu-id="77ad8-192">In questa esercitazione si è appreso come creare un cluster HBase.</span><span class="sxs-lookup"><span data-stu-id="77ad8-192">In this tutorial, you learned how to create an HBase cluster.</span></span> <span data-ttu-id="77ad8-193">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="77ad8-193">To learn more, see:</span></span>

* [<span data-ttu-id="77ad8-194">Introduzione all'uso di HDInsight</span><span class="sxs-lookup"><span data-stu-id="77ad8-194">Get started with HDInsight</span></span>](hdinsight-hadoop-linux-tutorial-get-started.md)
* [<span data-ttu-id="77ad8-195">Usare nodi perimetrali vuoti in HDInsight</span><span class="sxs-lookup"><span data-stu-id="77ad8-195">Use empty edge nodes in HDInsight</span></span>](hdinsight-apps-use-edge-node.md)
* [<span data-ttu-id="77ad8-196">Configurare la replica di HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="77ad8-196">Configure HBase replication in HDInsight</span></span>](hdinsight-hbase-replication.md)
* [<span data-ttu-id="77ad8-197">Creare cluster Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="77ad8-197">Create Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
* [<span data-ttu-id="77ad8-198">Introduzione all'uso di HBase con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="77ad8-198">Get started using HBase with Hadoop in HDInsight</span></span>](hdinsight-hbase-tutorial-get-started.md)
* [<span data-ttu-id="77ad8-199">Analizzare i sentimenti Twitter con HBase in HDInsight</span><span class="sxs-lookup"><span data-stu-id="77ad8-199">Analyze Twitter sentiment with HBase in HDInsight</span></span>](hdinsight-hbase-analyze-twitter-sentiment.md)
* <span data-ttu-id="77ad8-200">[Panoramica di Rete virtuale][vnet-overview]</span><span class="sxs-lookup"><span data-stu-id="77ad8-200">[Virtual Network Overview][vnet-overview]</span></span>

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
[img-provision-cluster-page1]: ./media/hdinsight-hbase-provision-vnet/hbasewizard1.png "Dettagli di provisioning per il nuovo cluster HBase"
[img-provision-cluster-page5]: ./media/hdinsight-hbase-provision-vnet/hbasewizard5.png "Usare azioni di script per personalizzare un cluster HBase"

[azure-preview-portal]: https://portal.azure.com
