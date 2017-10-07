---
title: la replica cluster HBase di aaaConfigure nelle reti virtuali - Azure | Documenti Microsoft
description: "Informazioni su come la replica di HBase tooconfigure per il bilanciamento del carico, la disponibilità elevata, senza tempi di inattività migrazione o aggiornamento da una tooanother versione di HDInsight e il ripristino di emergenza."
services: hdinsight,virtual-network
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: ba1c44f26b7cbf4a7a88159b12b3e064ea9f9a20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hbase-cluster-replication-within-virtual-networks"></a><span data-ttu-id="b8f62-103">Configurare la replica di cluster HBase nelle reti virtuali</span><span class="sxs-lookup"><span data-stu-id="b8f62-103">Configure HBase cluster replication within virtual networks</span></span>

<span data-ttu-id="b8f62-104">Informazioni su come tooconfigure HBase replica all'interno di una rete virtuale (VNet) o tra due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="b8f62-104">Learn how tooconfigure HBase replication within one virtual network (VNet) or between two virtual networks.</span></span>

<span data-ttu-id="b8f62-105">La replica di cluster usa una metodologia con push dell'origine.</span><span class="sxs-lookup"><span data-stu-id="b8f62-105">Cluster replication uses a source-push methodology.</span></span> <span data-ttu-id="b8f62-106">Un cluster HBase può essere un'origine o una destinazione o può soddisfare entrambi i ruoli in una sola volta.</span><span class="sxs-lookup"><span data-stu-id="b8f62-106">An HBase cluster can be a source or a destination, or it can fulfill both roles at once.</span></span> <span data-ttu-id="b8f62-107">La replica è asincrona e obiettivo hello di replica è coerenza finale.</span><span class="sxs-lookup"><span data-stu-id="b8f62-107">Replication is asynchronous, and hello goal of replication is eventual consistency.</span></span> <span data-ttu-id="b8f62-108">Quando origine hello riceve una famiglia di colonna tooa Modifica abilitata la replica, tale modifica è propagata tooall i cluster di destinazione.</span><span class="sxs-lookup"><span data-stu-id="b8f62-108">When hello source receives an edit tooa column family with replication enabled, that edit is propagated tooall destination clusters.</span></span> <span data-ttu-id="b8f62-109">Quando i dati vengono replicati da un cluster tooanother, il cluster di origine hello e tutti i cluster che è sono già utilizzata da dati hello vengono rilevati tooprevent cicli di replica.</span><span class="sxs-lookup"><span data-stu-id="b8f62-109">When data is replicated from one cluster tooanother, hello source cluster and all clusters that have already consumed hello data are tracked tooprevent replication loops.</span></span>

<span data-ttu-id="b8f62-110">In questa esercitazione si configurerà una replica origine-destinazione.</span><span class="sxs-lookup"><span data-stu-id="b8f62-110">In this tutorial, you will configure a source-destination replication.</span></span> <span data-ttu-id="b8f62-111">Per altre topologie di cluster, vedere la [guida di riferimento relativa a Apache HBase](http://hbase.apache.org/book.html#_cluster_replication).</span><span class="sxs-lookup"><span data-stu-id="b8f62-111">For other cluster topologies, see [Apache HBase Reference Guide](http://hbase.apache.org/book.html#_cluster_replication).</span></span>

<span data-ttu-id="b8f62-112">Casi di utilizzo della replica di HBase per una singola rete virtuale:</span><span class="sxs-lookup"><span data-stu-id="b8f62-112">HBase replication usage cases for a single virtual network:</span></span>

* <span data-ttu-id="b8f62-113">Bilanciamento del carico, ad esempio, l'esecuzione di analisi o i processi MapReduce nel cluster di destinazione hello e l'inserimento di dati nel cluster di origine hello</span><span class="sxs-lookup"><span data-stu-id="b8f62-113">Load balancing--for example, running scans or MapReduce jobs on hello destination cluster and ingesting data on hello source cluster</span></span>
* <span data-ttu-id="b8f62-114">Disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="b8f62-114">High availability</span></span>
* <span data-ttu-id="b8f62-115">Migrazione dei dati da un tooanother di cluster HBase</span><span class="sxs-lookup"><span data-stu-id="b8f62-115">Migrating data from one HBase cluster tooanother</span></span>
* <span data-ttu-id="b8f62-116">L'aggiornamento di un cluster Azure HDInsight da una versione tooanother</span><span class="sxs-lookup"><span data-stu-id="b8f62-116">Upgrading an Azure HDInsight cluster from one version tooanother</span></span>

<span data-ttu-id="b8f62-117">Casi di utilizzo della replica di HBase per due reti virtuali:</span><span class="sxs-lookup"><span data-stu-id="b8f62-117">HBase replication usage cases for two virtual networks:</span></span>

* <span data-ttu-id="b8f62-118">Ripristino di emergenza</span><span class="sxs-lookup"><span data-stu-id="b8f62-118">Disaster recovery</span></span>
* <span data-ttu-id="b8f62-119">Bilanciamento del carico e partizionamento di un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="b8f62-119">Load balancing and partitioning hello application</span></span>
* <span data-ttu-id="b8f62-120">Disponibilità elevata</span><span class="sxs-lookup"><span data-stu-id="b8f62-120">High availability</span></span>

<span data-ttu-id="b8f62-121">È possibile replicare i cluster tramite gli script [Azione script](hdinsight-hadoop-customize-cluster-linux.md) disponibili in [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span><span class="sxs-lookup"><span data-stu-id="b8f62-121">You replicate clusters by using [script action](hdinsight-hadoop-customize-cluster-linux.md) scripts located at [GitHub](https://github.com/Azure/hbase-utils/tree/master/replication).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8f62-122">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b8f62-122">Prerequisites</span></span>
<span data-ttu-id="b8f62-123">Prima di iniziare questa esercitazione, è necessario disporre di un abbonamento ad Azure.</span><span class="sxs-lookup"><span data-stu-id="b8f62-123">Before you begin this tutorial, you must have an Azure subscription.</span></span> <span data-ttu-id="b8f62-124">Vedere [Ottenere una versione di prova gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="b8f62-124">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

## <a name="configure-hello-environments"></a><span data-ttu-id="b8f62-125">Configurare ambienti hello</span><span class="sxs-lookup"><span data-stu-id="b8f62-125">Configure hello environments</span></span>

<span data-ttu-id="b8f62-126">Sono disponibili tre opzioni di configurazione:</span><span class="sxs-lookup"><span data-stu-id="b8f62-126">There are three possible configurations:</span></span>

- <span data-ttu-id="b8f62-127">Due cluster HBase in una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="b8f62-127">Two HBase clusters in one Azure virtual network</span></span>
- <span data-ttu-id="b8f62-128">Hello di due cluster HBase in due reti virtuali diverse nella stessa area geografica</span><span class="sxs-lookup"><span data-stu-id="b8f62-128">Two HBase clusters in two different virtual networks in hello same region</span></span>
- <span data-ttu-id="b8f62-129">Due cluster HBase in due reti virtuali differenti in due aree differenti (replica geografica)</span><span class="sxs-lookup"><span data-stu-id="b8f62-129">Two HBase clusters in two different virtual networks in two different regions (geo-replication)</span></span>

<span data-ttu-id="b8f62-130">toomake, ambienti di hello tooconfigure più semplici, sono stati creati alcuni [modelli di Azure Resource Manager](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8f62-130">toomake it easier tooconfigure hello environments, we have created some [Azure Resource Manager templates](../azure-resource-manager/resource-group-overview.md).</span></span> <span data-ttu-id="b8f62-131">Se si preferiscono ambienti hello tooconfigure utilizzando altri metodi, vedere:</span><span class="sxs-lookup"><span data-stu-id="b8f62-131">If you prefer tooconfigure hello environments by using other methods, see:</span></span>

- [<span data-ttu-id="b8f62-132">Creare cluster Hadoop basati su Linux in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b8f62-132">Create Linux-based Hadoop clusters in HDInsight</span></span>](hdinsight-hadoop-provision-linux-clusters.md)
- [<span data-ttu-id="b8f62-133">Creare cluster HBase nella rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="b8f62-133">Create HBase clusters in Azure Virtual Network</span></span>](hdinsight-hbase-provision-vnet.md)

### <a name="configure-one-virtual-network"></a><span data-ttu-id="b8f62-134">Configurare una rete virtuale</span><span class="sxs-lookup"><span data-stu-id="b8f62-134">Configure one virtual network</span></span>

<span data-ttu-id="b8f62-135">Fare clic su hello seguente immagine toocreate due HBase cluster in hello stessa rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="b8f62-135">Click hello following image toocreate two HBase clusters in hello same virtual network.</span></span> <span data-ttu-id="b8f62-136">modello Hello viene archiviato [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span><span class="sxs-lookup"><span data-stu-id="b8f62-136">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-one-vnet/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-one-vnet%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

### <a name="configure-two-virtual-networks-in-hello-same-region"></a><span data-ttu-id="b8f62-137">Configurare due reti virtuali in hello stessa area geografica</span><span class="sxs-lookup"><span data-stu-id="b8f62-137">Configure two virtual networks in hello same region</span></span>

<span data-ttu-id="b8f62-138">Fare clic su hello seguente immagine toocreate due reti virtuali con rete virtuale per il peering e due cluster HBase in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="b8f62-138">Click hello following image toocreate two virtual networks with VNet peering and two HBase clusters in hello same region.</span></span> <span data-ttu-id="b8f62-139">modello Hello viene archiviato [modelli di avvio rapido di Azure](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span><span class="sxs-lookup"><span data-stu-id="b8f62-139">hello template is stored in [Azure QuickStart Templates](https://azure.microsoft.com/resources/templates/101-hdinsight-hbase-replication-two-vnets-same-region/).</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-replication-two-vnets-same-region%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>



<span data-ttu-id="b8f62-140">Questo scenario richiede il [Peering reti virtuali](../virtual-network/virtual-network-peering-overview.md).</span><span class="sxs-lookup"><span data-stu-id="b8f62-140">This scenario requires [VNet peering](../virtual-network/virtual-network-peering-overview.md).</span></span> <span data-ttu-id="b8f62-141">modello di Hello consente peering reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="b8f62-141">hello template enables VNet peering.</span></span>   

<span data-ttu-id="b8f62-142">La replica di HBase utilizza indirizzi IP delle macchine virtuali ZooKeeper hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-142">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="b8f62-143">È necessario configurare gli indirizzi IP statici per i nodi di HBase ZooKeeper destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-143">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span>

<span data-ttu-id="b8f62-144">**indirizzi IP statici tooconfigure**</span><span class="sxs-lookup"><span data-stu-id="b8f62-144">**tooconfigure static IP addresses**</span></span>

1. <span data-ttu-id="b8f62-145">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8f62-145">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8f62-146">Scegliere dal menu a sinistra hello **gruppi di risorse**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-146">From hello left menu, click **Resource Groups**.</span></span>
3. <span data-ttu-id="b8f62-147">Scegliere il gruppo di risorse contenente cluster HBase di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-147">Click your resource group that contains hello destination HBase cluster.</span></span> <span data-ttu-id="b8f62-148">Si tratta di gruppo di risorse hello specificato quando si utilizza l'ambiente di hello Gestione risorse modello toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-148">This is hello resource group that you specified when you used hello Resource Manager template toocreate hello environment.</span></span> <span data-ttu-id="b8f62-149">È possibile utilizzare hello filtro toonarrow elenco hello verso il basso.</span><span class="sxs-lookup"><span data-stu-id="b8f62-149">You can use hello filter toonarrow down hello list.</span></span> <span data-ttu-id="b8f62-150">È possibile visualizzare un elenco di risorse che contiene due reti virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-150">You can see a list of resources that contains hello two virtual networks.</span></span>
4. <span data-ttu-id="b8f62-151">Fare clic su rete virtuale hello contenente cluster HBase di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-151">Click hello virtual network that contains hello destination HBase cluster.</span></span> <span data-ttu-id="b8f62-152">Ad esempio, fare clic su **xxxx-vnet2**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-152">For example, click **xxxx-vnet2**.</span></span> <span data-ttu-id="b8f62-153">Vengono visualizzati tre dispositivi i cui nomi iniziano con **nic-zookeepermode -**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-153">You can see three devices with names that start with **nic-zookeepermode-**.</span></span> <span data-ttu-id="b8f62-154">Tali dispositivi sono le macchine virtuali ZooKeeper hello tre.</span><span class="sxs-lookup"><span data-stu-id="b8f62-154">Those devices are hello three ZooKeeper VMs.</span></span>
5. <span data-ttu-id="b8f62-155">Fare clic su una delle macchine virtuali ZooKeeper hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-155">Click one of hello ZooKeeper VMs.</span></span>
6. <span data-ttu-id="b8f62-156">Fare clic su **Configurazioni IP**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-156">Click **IP configurations**.</span></span>
7. <span data-ttu-id="b8f62-157">Fare clic su **ipConfig1** dall'elenco di hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-157">Click **ipConfig1** from hello list.</span></span>
8. <span data-ttu-id="b8f62-158">Fare clic su **statico**e annotare l'indirizzo IP effettivo hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-158">Click **Static**, and write down hello actual IP address.</span></span> <span data-ttu-id="b8f62-159">Quando si esegue la replica di tooenable hello script azione, è necessario l'indirizzo IP hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-159">You will need hello IP address when you run hello script action tooenable replication.</span></span>

  ![Replica di HBase in HDInsight - Indirizzo IP statico di ZooKeeper](./media/hdinsight-hbase-replication/hdinsight-hbase-replication-zookeeper-static-ip.png)

9. <span data-ttu-id="b8f62-161">Ripetere il passaggio 6 tooset hello indirizzo IP per hello altri due nodi ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="b8f62-161">Repeat step 6 tooset hello static IP address for hello other two ZooKeeper nodes.</span></span>

<span data-ttu-id="b8f62-162">Scenario di rete virtuale cross hello, è necessario utilizzare hello **- ip** passare quando si chiama hello **hdi_enable_replication.sh** script azione.</span><span class="sxs-lookup"><span data-stu-id="b8f62-162">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

### <a name="configure-two-virtual-networks-in-two-different-regions"></a><span data-ttu-id="b8f62-163">Configurare due reti virtuali in due aree differenti</span><span class="sxs-lookup"><span data-stu-id="b8f62-163">Configure two virtual networks in two different regions</span></span>

<span data-ttu-id="b8f62-164">Fare clic su hello seguente immagine toocreate due reti virtuali in due aree diverse.</span><span class="sxs-lookup"><span data-stu-id="b8f62-164">Click hello following image toocreate two virtual networks in two different regions.</span></span> <span data-ttu-id="b8f62-165">modello Hello viene archiviato in un contenitore Blob di Azure pubblico.</span><span class="sxs-lookup"><span data-stu-id="b8f62-165">hello template is stored in a public Azure Blob container.</span></span>

<a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Fhbaseha%2Fdeploy-hbase-geo-replication.json" target="_blank"><img src="./media/hdinsight-hbase-replication/deploy-to-azure.png" alt="Deploy tooAzure"></a>

<span data-ttu-id="b8f62-166">Creare un gateway VPN tra due reti virtuali hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-166">Create a VPN gateway between hello two virtual networks.</span></span> <span data-ttu-id="b8f62-167">Per istruzioni, vedere [Creare una rete virtuale con una connessione da sito a sito](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span><span class="sxs-lookup"><span data-stu-id="b8f62-167">For instructions, see [Create a VNet with a site-to-site connection](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md).</span></span>

<span data-ttu-id="b8f62-168">La replica di HBase utilizza indirizzi IP delle macchine virtuali ZooKeeper hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-168">HBase replication uses IP addresses of hello ZooKeeper VMs.</span></span> <span data-ttu-id="b8f62-169">È necessario configurare gli indirizzi IP statici per i nodi di HBase ZooKeeper destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-169">You must configure static IP addresses for hello destination HBase ZooKeeper nodes.</span></span> <span data-ttu-id="b8f62-170">indirizzo IP statico tooconfigure, nella sezione hello "Configura due reti virtuali in hello stessa area" in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="b8f62-170">tooconfigure static IP, see hello "Configure two virtual networks in hello same region" section in this article.</span></span>

<span data-ttu-id="b8f62-171">Scenario di rete virtuale cross hello, è necessario utilizzare hello **- ip** passare quando si chiama hello **hdi_enable_replication.sh** script azione.</span><span class="sxs-lookup"><span data-stu-id="b8f62-171">For hello cross-VNet scenario, you must use hello **-ip** switch when calling hello **hdi_enable_replication.sh** script action.</span></span>

## <a name="load-test-data"></a><span data-ttu-id="b8f62-172">Dati del test di carico</span><span class="sxs-lookup"><span data-stu-id="b8f62-172">Load test data</span></span>

<span data-ttu-id="b8f62-173">Quando si esegue la replica di un cluster, è necessario specificare tooreplicate tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-173">When you replicate a cluster, you must specify hello tables tooreplicate.</span></span> <span data-ttu-id="b8f62-174">In questa sezione si caricherà alcuni dati in cluster di origine hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-174">In this section, you will load some data into hello source cluster.</span></span> <span data-ttu-id="b8f62-175">Nella sezione successiva hello, verrà abilitata la replica tra due cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-175">In hello next section, you will enable replication between hello two clusters.</span></span>

<span data-ttu-id="b8f62-176">Seguire le istruzioni hello [HBase esercitazione: Introduzione all'uso di Apache HBase con basati su Linux, Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate un **contatti** tabella e inserire alcuni dati nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-176">Follow hello instructions in [HBase tutorial: Get started using Apache HBase with Linux-based Hadoop in HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) toocreate a **Contacts** table and insert some data into hello table.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="b8f62-177">Abilitare la replica</span><span class="sxs-lookup"><span data-stu-id="b8f62-177">Enable replication</span></span>

<span data-ttu-id="b8f62-178">Hello alla procedura seguente viene illustrato come toocall hello script dell'azione script da hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="b8f62-178">hello following steps show how toocall hello script action script from hello Azure portal.</span></span> <span data-ttu-id="b8f62-179">Per l'esecuzione di un'azione di script tramite Azure PowerShell e hello Azure interfaccia della riga di comando (CLI), vedere [ai cluster HDInsight basati su Linux personalizzare mediante l'azione di script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="b8f62-179">For running a script action by using Azure PowerShell and hello Azure command-line interface (CLI), see [Customize Linux-based HDInsight clusters using script action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

<span data-ttu-id="b8f62-180">**replica di HBase tooenable da hello portale di Azure**</span><span class="sxs-lookup"><span data-stu-id="b8f62-180">**tooenable HBase replication from hello Azure portal**</span></span>

1. <span data-ttu-id="b8f62-181">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="b8f62-181">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="b8f62-182">Aprire cluster HBase di origine hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-182">Open hello source HBase cluster.</span></span>
3. <span data-ttu-id="b8f62-183">Scegliere dal menu cluster hello **azioni Script**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-183">From hello cluster menu, click **Script Actions**.</span></span>
4. <span data-ttu-id="b8f62-184">Fare clic su **inviare nuove** dalla parte superiore di hello del pannello hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-184">Click **Submit New** from hello top of hello blade.</span></span>
5. <span data-ttu-id="b8f62-185">Selezionare o immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="b8f62-185">Select or enter hello following information:</span></span>

  - <span data-ttu-id="b8f62-186">**Nome**: immettere **Abilitazione replica**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-186">**Name**: Enter **Enable replication**.</span></span>
  - <span data-ttu-id="b8f62-187">**URL dello script Bash**: immettere **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-187">**Bash Script URL**: Enter **https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_enable_replication.sh**.</span></span>
  - <span data-ttu-id="b8f62-188">**Intestazione**: Selezionata.</span><span class="sxs-lookup"><span data-stu-id="b8f62-188">**Head**: Selected.</span></span> <span data-ttu-id="b8f62-189">Deselezionare hello altri tipi di nodo.</span><span class="sxs-lookup"><span data-stu-id="b8f62-189">Clear hello other node types.</span></span>
  - <span data-ttu-id="b8f62-190">**I parametri**: esempio hello parametri abilitare la replica per tutte le tabelle esistenti hello di esempio e copiare tutti i dati di hello dal cluster di destinazione toohello hello origine cluster:</span><span class="sxs-lookup"><span data-stu-id="b8f62-190">**Parameters**: hello following sample parameters enable replication for all hello existing tables and copy all hello data from hello source cluster toohello destination cluster:</span></span>

            -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -copydata

6. <span data-ttu-id="b8f62-191">Fare clic su **Crea**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-191">Click **Create**.</span></span> <span data-ttu-id="b8f62-192">script Hello può richiedere del tempo, soprattutto quando argomento - copydata hello è utilizzata.</span><span class="sxs-lookup"><span data-stu-id="b8f62-192">hello script can take some time, especially when hello -copydata argument is used.</span></span>

<span data-ttu-id="b8f62-193">Argomenti obbligatori:</span><span class="sxs-lookup"><span data-stu-id="b8f62-193">Required arguments:</span></span>

|<span data-ttu-id="b8f62-194">Nome</span><span class="sxs-lookup"><span data-stu-id="b8f62-194">Name</span></span>|<span data-ttu-id="b8f62-195">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b8f62-195">Description</span></span>|
|----|-----------|
|<span data-ttu-id="b8f62-196">-s, --src-cluster</span><span class="sxs-lookup"><span data-stu-id="b8f62-196">-s, --src-cluster</span></span> | <span data-ttu-id="b8f62-197">Specificare il nome DNS hello dei cluster HBase di origine hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-197">Specify hello DNS name of hello source HBase cluster.</span></span> <span data-ttu-id="b8f62-198">Ad esempio: -s hbsrccluster, --src-cluster=hbsrccluster</span><span class="sxs-lookup"><span data-stu-id="b8f62-198">For example: -s hbsrccluster, --src-cluster=hbsrccluster</span></span> |
|<span data-ttu-id="b8f62-199">-d, - dst-cluster</span><span class="sxs-lookup"><span data-stu-id="b8f62-199">-d, --dst-cluster</span></span> | <span data-ttu-id="b8f62-200">Specificare il nome DNS hello della destinazione hello cluster HBase (replica).</span><span class="sxs-lookup"><span data-stu-id="b8f62-200">Specify hello DNS name of hello destination (replica) HBase cluster.</span></span> <span data-ttu-id="b8f62-201">Ad esempio: -s dsthbcluster, --src-cluster=dsthbcluster</span><span class="sxs-lookup"><span data-stu-id="b8f62-201">For example: -s dsthbcluster, --src-cluster=dsthbcluster</span></span> |
|<span data-ttu-id="b8f62-202">-sp, --src-ambari-password</span><span class="sxs-lookup"><span data-stu-id="b8f62-202">-sp, --src-ambari-password</span></span> | <span data-ttu-id="b8f62-203">Specificare la password di amministratore di hello per Ambari cluster HBase di origine hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-203">Specify hello admin password for Ambari on hello source HBase cluster.</span></span> |
|<span data-ttu-id="b8f62-204">-dp, --dst-ambari-password</span><span class="sxs-lookup"><span data-stu-id="b8f62-204">-dp, --dst-ambari-password</span></span> | <span data-ttu-id="b8f62-205">Specificare la password di amministratore di hello per Ambari nel cluster HBase di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-205">Specify hello admin password for Ambari on hello destination HBase cluster.</span></span>|

<span data-ttu-id="b8f62-206">Argomenti facoltativi:</span><span class="sxs-lookup"><span data-stu-id="b8f62-206">Optional arguments:</span></span>

|<span data-ttu-id="b8f62-207">Nome</span><span class="sxs-lookup"><span data-stu-id="b8f62-207">Name</span></span>|<span data-ttu-id="b8f62-208">Descrizione</span><span class="sxs-lookup"><span data-stu-id="b8f62-208">Description</span></span>|
|----|-----------|
|<span data-ttu-id="b8f62-209">-su, --src-ambari-user</span><span class="sxs-lookup"><span data-stu-id="b8f62-209">-su, --src-ambari-user</span></span> | <span data-ttu-id="b8f62-210">Specificare nome utente amministratore hello per Ambari cluster HBase di origine hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-210">Specify hello admin username for Ambari on hello source HBase cluster.</span></span> <span data-ttu-id="b8f62-211">valore predefinito di Hello è **admin**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-211">hello default value is **admin**.</span></span> |
|<span data-ttu-id="b8f62-212">-du, --dst-ambari-user</span><span class="sxs-lookup"><span data-stu-id="b8f62-212">-du, --dst-ambari-user</span></span> | <span data-ttu-id="b8f62-213">Specificare nome utente amministratore hello per Ambari nel cluster HBase di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="b8f62-213">Specify hello admin username for Ambari on hello destination HBase cluster.</span></span> <span data-ttu-id="b8f62-214">valore predefinito di Hello è **admin**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-214">hello default value is **admin**.</span></span> |
|<span data-ttu-id="b8f62-215">-t, --table-list</span><span class="sxs-lookup"><span data-stu-id="b8f62-215">-t, --table-list</span></span> | <span data-ttu-id="b8f62-216">Specificare hello toobe di tabelle replicate.</span><span class="sxs-lookup"><span data-stu-id="b8f62-216">Specify hello tables toobe replicated.</span></span> <span data-ttu-id="b8f62-217">Ad esempio: --table-list="table1;table2;table3".</span><span class="sxs-lookup"><span data-stu-id="b8f62-217">For example: --table-list="table1;table2;table3".</span></span> <span data-ttu-id="b8f62-218">Se non si specificano tabelle, vengono replicate tutte le tabelle HBase esistenti.</span><span class="sxs-lookup"><span data-stu-id="b8f62-218">If you don't specify tables, all existing HBase tables are replicated.</span></span>|
|<span data-ttu-id="b8f62-219">-m, --machine</span><span class="sxs-lookup"><span data-stu-id="b8f62-219">-m, --machine</span></span> | <span data-ttu-id="b8f62-220">Specificare il nodo head hello in hello script verranno eseguiti.</span><span class="sxs-lookup"><span data-stu-id="b8f62-220">Specify hello head node where hello script action will run.</span></span> <span data-ttu-id="b8f62-221">il valore di Hello è hn1 o hn0.</span><span class="sxs-lookup"><span data-stu-id="b8f62-221">hello value is either hn1 or hn0.</span></span> <span data-ttu-id="b8f62-222">Poiché hn0 è usato con maggiore frequenza, è consigliabile usare hn1.</span><span class="sxs-lookup"><span data-stu-id="b8f62-222">Because hn0 is usually busier, we recommend using hn1.</span></span> <span data-ttu-id="b8f62-223">Utilizzare questa opzione quando si esegue uno script hello $0 come un'azione di script dal portale di HDInsight hello o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="b8f62-223">You use this option when you're running hello $0 script as a script action from hello HDInsight portal or Azure PowerShell.</span></span>|
|<span data-ttu-id="b8f62-224">-ip</span><span class="sxs-lookup"><span data-stu-id="b8f62-224">-ip</span></span> | <span data-ttu-id="b8f62-225">Questo argomento è obbligatorio quando si vuole abilitare la replica tra due reti virtuali.</span><span class="sxs-lookup"><span data-stu-id="b8f62-225">This argument is required when you're enabling replication between two virtual networks.</span></span> <span data-ttu-id="b8f62-226">Questo argomento viene utilizzato come un commutatore toouse hello statico gli indirizzi IP di ZooKeeper nodi dal cluster di replica anziché nomi di dominio completi.</span><span class="sxs-lookup"><span data-stu-id="b8f62-226">This argument acts as a switch toouse hello static IPs of ZooKeeper nodes from replica clusters instead of FQDN names.</span></span> <span data-ttu-id="b8f62-227">Hello statico IP necessario toobe preconfigurato prima di abilitare la replica.</span><span class="sxs-lookup"><span data-stu-id="b8f62-227">hello static IPs need toobe preconfigured before you enable replication.</span></span> |
|<span data-ttu-id="b8f62-228">-cp, -copydata</span><span class="sxs-lookup"><span data-stu-id="b8f62-228">-cp, -copydata</span></span> | <span data-ttu-id="b8f62-229">Abilitare la migrazione di hello dei dati esistenti nelle tabelle di hello in cui la replica è abilitata.</span><span class="sxs-lookup"><span data-stu-id="b8f62-229">Enable hello migration of existing data on hello tables where replication is enabled.</span></span> |
|<span data-ttu-id="b8f62-230">-rpm, -replicate-phoenix-meta</span><span class="sxs-lookup"><span data-stu-id="b8f62-230">-rpm, -replicate-phoenix-meta</span></span> | <span data-ttu-id="b8f62-231">Abilita la replica sulle tabelle di sistema Phoenix.</span><span class="sxs-lookup"><span data-stu-id="b8f62-231">Enable replication on Phoenix system tables.</span></span> <br><br><span data-ttu-id="b8f62-232">*Questa opzione deve essere usata con attenzione.*</span><span class="sxs-lookup"><span data-stu-id="b8f62-232">*Use this option with caution.*</span></span> <span data-ttu-id="b8f62-233">È consigliabile ricreare le tabelle di Phoenix nei cluster di replica prima di usare questo script.</span><span class="sxs-lookup"><span data-stu-id="b8f62-233">We recommend that you re-create Phoenix tables on replica clusters before you use this script.</span></span> |
|<span data-ttu-id="b8f62-234">-h, --help</span><span class="sxs-lookup"><span data-stu-id="b8f62-234">-h, --help</span></span> | <span data-ttu-id="b8f62-235">Visualizza le informazioni sull'utilizzo.</span><span class="sxs-lookup"><span data-stu-id="b8f62-235">Display usage information.</span></span> |

<span data-ttu-id="b8f62-236">Hello sezione print_usage() di hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) fornisce una spiegazione dettagliata dei parametri.</span><span class="sxs-lookup"><span data-stu-id="b8f62-236">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_enable_replication.sh) provides a detailed explanation of parameters.</span></span>

<span data-ttu-id="b8f62-237">Al termine dell'azione script hello correttamente distribuito, è possibile utilizzare cluster HBase SSH tooconnect toohello destinazione e verificare dati hello sono stati replicati.</span><span class="sxs-lookup"><span data-stu-id="b8f62-237">After hello script action is successfully deployed, you can use SSH tooconnect toohello destination HBase cluster, and verify hello data has been replicated.</span></span>

### <a name="replication-scenarios"></a><span data-ttu-id="b8f62-238">Scenari di replica</span><span class="sxs-lookup"><span data-stu-id="b8f62-238">Replication scenarios</span></span>

<span data-ttu-id="b8f62-239">Hello elenco seguente mostra alcuni casi di utilizzo generale e le relative impostazioni di parametro:</span><span class="sxs-lookup"><span data-stu-id="b8f62-239">hello following list shows you some general usage cases and their parameter settings:</span></span>

- <span data-ttu-id="b8f62-240">**Abilitare la replica in tutte le tabelle tra cluster hello due**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-240">**Enable replication on all tables between hello two clusters**.</span></span> <span data-ttu-id="b8f62-241">Questo scenario non richiede copia hello la migrazione dei dati esistenti nelle tabelle di hello e Usa tabelle Phoenix.</span><span class="sxs-lookup"><span data-stu-id="b8f62-241">This scenario does not require hello copy/migration of existing data on hello tables, and it does not use Phoenix tables.</span></span> <span data-ttu-id="b8f62-242">Utilizzare hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="b8f62-242">Use hello following parameters:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password>  

- <span data-ttu-id="b8f62-243">**Abilitare la replica su tabelle specifiche**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-243">**Enable replication on specific tables**.</span></span> <span data-ttu-id="b8f62-244">Utilizzare hello seguendo replica tooenable parametri table1, table2 e TABELLA3:</span><span class="sxs-lookup"><span data-stu-id="b8f62-244">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3"

- <span data-ttu-id="b8f62-245">**Abilitare la replica su tabelle specifiche e copiare i dati esistenti hello**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-245">**Enable replication on specific tables and copy hello existing data**.</span></span> <span data-ttu-id="b8f62-246">Utilizzare hello seguendo replica tooenable parametri table1, table2 e TABELLA3:</span><span class="sxs-lookup"><span data-stu-id="b8f62-246">Use hello following parameters tooenable replication on table1, table2, and table3:</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -copydata

- <span data-ttu-id="b8f62-247">**Abilitare la replica in tutte le tabelle con la replica dei metadati phoenix da origine toodestination**.</span><span class="sxs-lookup"><span data-stu-id="b8f62-247">**Enable replication on all tables with replicating phoenix metadata from source toodestination**.</span></span> <span data-ttu-id="b8f62-248">La replica dei metadati di Phoenix non è perfetta e deve essere usata con cautela.</span><span class="sxs-lookup"><span data-stu-id="b8f62-248">Phoenix metadata replication is not perfect and should be enabled with caution.</span></span>

        -m hn1 -s <source cluster DNS name> -d <destination cluster DNS name> -sp <source cluster Ambari password> -dp <destination cluster Ambari password> -t "table1;table2;table3" -replicate-phoenix-meta

## <a name="copy-and-migrate-data"></a><span data-ttu-id="b8f62-249">Copia e migrazione dei dati</span><span class="sxs-lookup"><span data-stu-id="b8f62-249">Copy and migrate data</span></span>

<span data-ttu-id="b8f62-250">Sono disponibili due script azione script distinti per la copia o la migrazione dei dati dopo aver abilitato la replica:</span><span class="sxs-lookup"><span data-stu-id="b8f62-250">There are two separate script action scripts for copying/migrating data after replication is enabled:</span></span>

- <span data-ttu-id="b8f62-251">[Script per tabelle di piccole dimensioni](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (pochi gigabyte nella copia di dimensione e complessiva è toofinish previsto in meno di un'ora)</span><span class="sxs-lookup"><span data-stu-id="b8f62-251">[Script for small tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_copy_table.sh) (a few gigabytes in size, and overall copy is expected toofinish in less than one hour)</span></span>

- <span data-ttu-id="b8f62-252">[Script per tabelle di grandi dimensioni](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (previsto più di un'ora toocopy tootake)</span><span class="sxs-lookup"><span data-stu-id="b8f62-252">[Script for large tables](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/nohup_hdi_copy_table.sh) (expected tootake longer than one hour toocopy)</span></span>

<span data-ttu-id="b8f62-253">È possibile seguire hello stessa procedura nel [abilitare la replica](#enable-replication) toocall hello script azione hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="b8f62-253">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -t <table1:start_timestamp:end_timestamp;table2:start_timestamp:end_timestamp;...> -p <replication_peer> [-everythingTillNow]

<span data-ttu-id="b8f62-254">Hello sezione print_usage() di hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) fornisce una descrizione dettagliata dei parametri.</span><span class="sxs-lookup"><span data-stu-id="b8f62-254">hello print_usage() section of hello [script](https://github.com/Azure/hbase-utils/blob/master/replication/hdi_copy_table.sh) provides a detailed description of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="b8f62-255">Scenari</span><span class="sxs-lookup"><span data-stu-id="b8f62-255">Scenarios</span></span>

- <span data-ttu-id="b8f62-256">**Copiare tabelle specifiche (test1, test2 e test3) per tutte le righe modificate finora (timestamp corrente)**:</span><span class="sxs-lookup"><span data-stu-id="b8f62-256">**Copy specific tables (test1, test2, and test3) for all rows edited till now (current time stamp)**:</span></span>

        -m hn1 -t "test1::;test2::;test3::" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow
  <span data-ttu-id="b8f62-257">oppure</span><span class="sxs-lookup"><span data-stu-id="b8f62-257">or</span></span>

        -m hn1 -t "test1::;test2::;test3::" --replication-peer="zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure" -everythingTillNow


- <span data-ttu-id="b8f62-258">**Copiare tabelle specifiche con un intervallo di tempo specificato**:</span><span class="sxs-lookup"><span data-stu-id="b8f62-258">**Copy specific tables with specified time range**:</span></span>

        -m hn1 -t "table1:0:452256397;table2:14141444:452256397" -p "zk5-hbrpl2;zk1-hbrpl2;zk5-hbrpl2:2181:/hbase-unsecure"


## <a name="disable-replication"></a><span data-ttu-id="b8f62-259">Disabilitare la replica</span><span class="sxs-lookup"><span data-stu-id="b8f62-259">Disable replication</span></span>

<span data-ttu-id="b8f62-260">replica toodisable, utilizzare un altro script dell'azione script si trova in [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span><span class="sxs-lookup"><span data-stu-id="b8f62-260">toodisable replication, you use another script action script located at [GitHub](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh).</span></span> <span data-ttu-id="b8f62-261">È possibile seguire hello stessa procedura nel [abilitare la replica](#enable-replication) toocall hello script azione hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="b8f62-261">You can follow hello same procedure in [Enable replication](#enable-replication) toocall hello script action with hello following parameters:</span></span>

    -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari Password> <-all|-t "table1;table2;...">  

<span data-ttu-id="b8f62-262">Hello sezione print_usage() di hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) fornisce una spiegazione dettagliata dei parametri.</span><span class="sxs-lookup"><span data-stu-id="b8f62-262">hello print_usage() section of hello [script](https://raw.githubusercontent.com/Azure/hbase-utils/master/replication/hdi_disable_replication.sh) provides a detailed explanation of parameters.</span></span>

### <a name="scenarios"></a><span data-ttu-id="b8f62-263">Scenari</span><span class="sxs-lookup"><span data-stu-id="b8f62-263">Scenarios</span></span>

- <span data-ttu-id="b8f62-264">**Disabilitare la replica in tutte le tabelle**:</span><span class="sxs-lookup"><span data-stu-id="b8f62-264">**Disable replication on all tables**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp Mypassword\!789 -all
  <span data-ttu-id="b8f62-265">oppure</span><span class="sxs-lookup"><span data-stu-id="b8f62-265">or</span></span>

        --src-cluster=<source cluster DNS name> --dst-cluster=<destination cluster DNS name> --src-ambari-user=<source cluster Ambari username> --src-ambari-password=<source cluster Ambari password>

- <span data-ttu-id="b8f62-266">**Disabilitare la replica in tabelle specifiche (table1, table2 e table3)**:</span><span class="sxs-lookup"><span data-stu-id="b8f62-266">**Disable replication on specified tables (table1, table2, and table3)**:</span></span>

        -m hn1 -s <source cluster DNS name> -sp <source cluster Ambari password> -t "table1;table2;table3"

## <a name="next-steps"></a><span data-ttu-id="b8f62-267">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b8f62-267">Next steps</span></span>

<span data-ttu-id="b8f62-268">In questa esercitazione, si è appreso come la replica di HBase tooconfigure tra due Data Center.</span><span class="sxs-lookup"><span data-stu-id="b8f62-268">In this tutorial, you learned how tooconfigure HBase replication across two datacenters.</span></span> <span data-ttu-id="b8f62-269">toolearn ulteriori informazioni su HDInsight e HBase, vedere:</span><span class="sxs-lookup"><span data-stu-id="b8f62-269">toolearn more about HDInsight and HBase, see:</span></span>

* <span data-ttu-id="b8f62-270">[Introduzione ad Apache HBase in HDInsight][hdinsight-hbase-get-started]</span><span class="sxs-lookup"><span data-stu-id="b8f62-270">[Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started]</span></span>
* <span data-ttu-id="b8f62-271">[Panoramica su HBase di HDInsight][hdinsight-hbase-overview]</span><span class="sxs-lookup"><span data-stu-id="b8f62-271">[HDInsight HBase overview][hdinsight-hbase-overview]</span></span>
* <span data-ttu-id="b8f62-272">[Creare cluster HBase nella rete virtuale di Azure][hdinsight-hbase-provision-vnet]</span><span class="sxs-lookup"><span data-stu-id="b8f62-272">[Create HBase clusters in Azure Virtual Network][hdinsight-hbase-provision-vnet]</span></span>
* <span data-ttu-id="b8f62-273">[Analisi dei sentimenti Twitter in tempo reale con HBase][hdinsight-hbase-twitter-sentiment]</span><span class="sxs-lookup"><span data-stu-id="b8f62-273">[Analyze real-time Twitter sentiment with HBase][hdinsight-hbase-twitter-sentiment]</span></span>
* <span data-ttu-id="b8f62-274">[Analisi dei dati dei sensori con Storm e HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span><span class="sxs-lookup"><span data-stu-id="b8f62-274">[Analyzing sensor data with Storm and HBase in HDInsight (Hadoop)][hdinsight-sensor-data]</span></span>

[hdinsight-hbase-geo-replication-vnet]: hdinsight-hbase-geo-replication-configure-vnets.md
[hdinsight-hbase-geo-replication-dns]: ../hdinsight-hbase-geo-replication-configure-VNet.md


[img-vnet-diagram]: ./media/hdinsight-hbase-geo-replication/HDInsight.HBase.Replication.Network.diagram.png

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started-linux.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[hdinsight-sensor-data]: hdinsight-storm-sensor-data-analysis.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
