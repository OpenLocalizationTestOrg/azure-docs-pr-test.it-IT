---
title: "Alta disponibilità per Hadoop - Azure HDInsight | Microsoft Docs"
description: "Informazioni su come i cluster HDInsight migliorano l'affidabilità e la disponibilità tramite l'uso di un nodo head aggiuntivo. Informazioni su come questo influisce sui servizi di Hadoop come Ambari e Hive, e anche su come connettersi singolarmente a ogni nodo head tramite SSH."
services: hdinsight
editor: cgronlun
manager: jhubbard
author: Blackmist
documentationcenter: 
tags: azure-portal
keywords: "alta disponibilità di hadoop"
ms.assetid: 99c9f59c-cf6b-4529-99d1-bf060435e8d4
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 07/28/2017
ms.author: larryfr
ms.openlocfilehash: e66ba67a36fc48d1762ba302d708e060489fdc71
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="33041-105">Disponibilità e affidabilità dei cluster Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="33041-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="33041-106">I cluster HDInsight offrono due nodi head per aumentare la disponibilità e l'affidabilità dei servizi e dei processi di Hadoop in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="33041-106">HDInsight clusters provide two head nodes to increase the availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="33041-107">Hadoop ottiene alta disponibilità e affidabilità replicando i servizi e i dati su più nodi di un cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="33041-108">Tuttavia le distribuzioni standard di Hadoop hanno in genere un singolo nodo head.</span><span class="sxs-lookup"><span data-stu-id="33041-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="33041-109">Eventuali interruzioni del singolo nodo head possono causare l'interruzione del funzionamento del cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-109">Any outage of the single head node can cause the cluster to stop working.</span></span> <span data-ttu-id="33041-110">HDInsight fornisce due nodi head per migliorare la disponibilità e affidabilità di Hadoop.</span><span class="sxs-lookup"><span data-stu-id="33041-110">HDInsight provides two headnodes to improve Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33041-111">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="33041-111">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="33041-112">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="33041-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="33041-113">Disponibilità e affidabilità dei nodi</span><span class="sxs-lookup"><span data-stu-id="33041-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="33041-114">I nodi in un cluster HDInsight vengono implementati con macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="33041-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="33041-115">Le sezioni seguenti illustrano i singoli tipi di nodo usati con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="33041-115">The following sections discuss the individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="33041-116">Non tutti i tipi di nodo vengono usati per un tipo di cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="33041-117">Ad esempio, un tipo di cluster Hadoop non ha alcun nodo Nimbus.</span><span class="sxs-lookup"><span data-stu-id="33041-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="33041-118">Per altre informazioni sui nodi usati dai tipi di cluster HDInsight, vedere la sezione Tipi di cluster del documento [Creare cluster Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span><span class="sxs-lookup"><span data-stu-id="33041-118">For more information on nodes used by HDInsight cluster types, see the Cluster types section of the [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="33041-119">Nodi head</span><span class="sxs-lookup"><span data-stu-id="33041-119">Head nodes</span></span>

<span data-ttu-id="33041-120">Per garantire un'alta disponibilità dei servizi Hadoop, HDInsight fornisce due nodi head.</span><span class="sxs-lookup"><span data-stu-id="33041-120">To ensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="33041-121">Entrambi i nodi head sono contemporaneamente attivi e in esecuzione all'interno del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="33041-121">Both head nodes are active and running within the HDInsight cluster simultaneously.</span></span> <span data-ttu-id="33041-122">Alcuni servizi, ad esempio HDFS o YARN, sono "attivi"in qualsiasi momento soltanto in un nodo head.</span><span class="sxs-lookup"><span data-stu-id="33041-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="33041-123">Altri servizi come HiveServer2 o Hive Metastore sono attivi su entrambi i nodi head allo tesso tempo.</span><span class="sxs-lookup"><span data-stu-id="33041-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at the same time.</span></span>

<span data-ttu-id="33041-124">I nodi head, e altri nodi in HDInsight, hanno un valore numerico all'interno del nome host del nodo.</span><span class="sxs-lookup"><span data-stu-id="33041-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of the hostname of the node.</span></span> <span data-ttu-id="33041-125">Ad esempio, `hn0-CLUSTERNAME` o `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="33041-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="33041-126">Non associare il valore numerico con il fatto che un nodo sia primario o secondario.</span><span class="sxs-lookup"><span data-stu-id="33041-126">Do not associate the numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="33041-127">Il valore numerico serve solo per specificare un nome univoco per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="33041-127">The numeric value is only present to provide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="33041-128">Nodi Nimbus</span><span class="sxs-lookup"><span data-stu-id="33041-128">Nimbus Nodes</span></span>

<span data-ttu-id="33041-129">I nodi nimbus sono disponibili con i cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="33041-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="33041-130">I nodi Nimbus forniscono una funzionalità simile a JobTracker di Hadoop mediante la distribuzione e il monitoraggio dell'elaborazione tra nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="33041-130">The Nimbus nodes provide similar functionality to the Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="33041-131">HDInsight offre due nodi Nimbus per i cluster Storm</span><span class="sxs-lookup"><span data-stu-id="33041-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="33041-132">Nodi Zookeeper</span><span class="sxs-lookup"><span data-stu-id="33041-132">Zookeeper nodes</span></span>

<span data-ttu-id="33041-133">I nodi [ZooKeeper](http://zookeeper.apache.org/) vengono usati per la designazione di leader dei servizi master nei nodi head.</span><span class="sxs-lookup"><span data-stu-id="33041-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="33041-134">Vengono inoltre usati per garantire che i servizi, i nodi di dati (ruolo di lavoro) e i gateway sappiano su quale nodo head è attivo un servizio master.</span><span class="sxs-lookup"><span data-stu-id="33041-134">They are also used to insure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="33041-135">Per impostazione predefinita, HDInsight specifica tre nodi ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="33041-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="33041-136">Nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="33041-136">Worker nodes</span></span>

<span data-ttu-id="33041-137">I nodi di lavoro eseguono l'analisi dei dati effettivi quando un processo viene inviato al cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-137">Worker nodes perform the actual data analysis when a job is submitted to the cluster.</span></span> <span data-ttu-id="33041-138">In caso di errore di un nodo del ruolo di lavoro, l'attività che il nodo stava eseguendo viene inviata a un altro nodo del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="33041-138">If a worker node fails, the task that it was performing is submitted to another worker node.</span></span> <span data-ttu-id="33041-139">Per impostazione predefinita, HDInsight crea quattro nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="33041-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="33041-140">È possibile modificare questo numero in base alle proprie esigenze, durante e dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-140">You can change this number to suit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="33041-141">Nodo perimetrale</span><span class="sxs-lookup"><span data-stu-id="33041-141">Edge node</span></span>

<span data-ttu-id="33041-142">Un nodo perimetrale non partecipa attivamente all'analisi dei dati all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-142">An edge node does not actively participate in data analysis within the cluster.</span></span> <span data-ttu-id="33041-143">Viene usato dagli sviluppatori o i data scientist quando lavorano con Hadoop.</span><span class="sxs-lookup"><span data-stu-id="33041-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="33041-144">Il nodo perimetrale si trova nella stessa rete virtuale di Azure come gli altri nodi del cluster e può accedere direttamente a tutti gli altri nodi.</span><span class="sxs-lookup"><span data-stu-id="33041-144">The edge node lives in the same Azure Virtual Network as the other nodes in the cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="33041-145">Il nodo perimetrale può essere usato senza sottrarre risorse ai servizi critici di Hadoop o ai processi di analisi.</span><span class="sxs-lookup"><span data-stu-id="33041-145">The edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="33041-146">Attualmente, Server R in HDInsight è l'unico tipo di cluster che fornisce un nodo perimetrale per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="33041-146">Currently, R Server on HDInsight is the only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="33041-147">Per Server R in HDInsight, il nodo perimetrale viene usato per testare il codice R in locale nel nodo prima dell'invio al cluster per l'elaborazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="33041-147">For R Server on HDInsight, the edge node is used test R code locally on the node before submitting it to the cluster for distributed processing.</span></span>

<span data-ttu-id="33041-148">Per informazioni sull'uso di un nodo perimetrale con tipi di cluster diversi da R Server, vedere il documento [Usare nodi perimetrali vuoti in HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="33041-148">For information on using an edge node with cluster types other than R Server, see the [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-the-nodes"></a><span data-ttu-id="33041-149">Accesso ai nodi head</span><span class="sxs-lookup"><span data-stu-id="33041-149">Accessing the nodes</span></span>

<span data-ttu-id="33041-150">L'accesso al cluster tramite Internet avviene mediante un gateway pubblico.</span><span class="sxs-lookup"><span data-stu-id="33041-150">Access to the cluster over the internet is provided through a public gateway.</span></span> <span data-ttu-id="33041-151">L'accesso è limitato alla connessione ai nodi head e, se presente, al nodo perimetrale.</span><span class="sxs-lookup"><span data-stu-id="33041-151">Access is limited to connecting to the head nodes and (if one exists) the edge node.</span></span> <span data-ttu-id="33041-152">L'accesso ai servizi in esecuzione nei nodi head non avviene con più nodi head.</span><span class="sxs-lookup"><span data-stu-id="33041-152">Access to services running on the head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="33041-153">Il gateway pubblico instrada le richieste al nodo head che ospita il servizio richiesto.</span><span class="sxs-lookup"><span data-stu-id="33041-153">The public gateway routes requests to the head node that hosts the requested service.</span></span> <span data-ttu-id="33041-154">Ad esempio, se Ambari è attualmente ospitato nel nodo head secondario, il gateway instrada le richieste in ingresso per Ambari a quel nodo.</span><span class="sxs-lookup"><span data-stu-id="33041-154">For example, if Ambari is currently hosted on the secondary head node, the gateway routes incoming requests for Ambari to that node.</span></span>

<span data-ttu-id="33041-155">L'accesso tramite il gateway pubblico è limitato alle porte 443 (HTTPS), 22 e 23.</span><span class="sxs-lookup"><span data-stu-id="33041-155">Access over the public gateway is limited to port 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="33041-156">La porta __443__ viene usata per accedere ad Ambari e ad altre interfacce utente Web o API REST ospitate nei nodi head.</span><span class="sxs-lookup"><span data-stu-id="33041-156">Port __443__ is used to access Ambari and other web UI or REST APIs hosted on the head nodes.</span></span>

* <span data-ttu-id="33041-157">La porta __22__ viene usata per accedere al nodo head primario o a un nodo perimetrale con SSH.</span><span class="sxs-lookup"><span data-stu-id="33041-157">Port __22__ is used to access the primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="33041-158">La porta __23__ viene usata per accedere al nodo head secondario con SSH.</span><span class="sxs-lookup"><span data-stu-id="33041-158">Port __23__ is used to access the secondary head node with SSH.</span></span> <span data-ttu-id="33041-159">Ad esempio, `ssh username@mycluster-ssh.azurehdinsight.net` si connette al nodo head primario del cluster denominato **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="33041-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects to the primary head node of the cluster named **mycluster**.</span></span>

<span data-ttu-id="33041-160">Per altre informazioni sull'uso di SSH, vedere il documento [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="33041-160">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="33041-161">Nomi di dominio completo interni (FQDN) </span><span class="sxs-lookup"><span data-stu-id="33041-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="33041-162">I nodi di un cluster HDInsight hanno un indirizzo IP interno e un FQDN accessibili solo dal cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from the cluster.</span></span> <span data-ttu-id="33041-163">Quando si accede ai servizi del cluster utilizzando l'indirizzo IP o i FQDN interni, è necessario utilizzare Ambari per verificare l'IP o i FQDN da utilizzare per l’accesso al servizio.</span><span class="sxs-lookup"><span data-stu-id="33041-163">When accessing services on the cluster using the internal FQDN or IP address, you should use Ambari to verify the IP or FQDN to use when accessing the service.</span></span>

<span data-ttu-id="33041-164">Ad esempio, il servizio Oozie può essere eseguito solo su un nodo head e l’utilizzo del comando `oozie` da una sessione SSH richiede l'URL del servizio.</span><span class="sxs-lookup"><span data-stu-id="33041-164">For example, the Oozie service can only run on one head node, and using the `oozie` command from an SSH session requires the URL to the service.</span></span> <span data-ttu-id="33041-165">Tale URL può essere recuperato da Ambari tramite il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="33041-165">This URL can be retrieved from Ambari by using the following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="33041-166">Il comando restituisce un valore simile al seguente, che contiene l'URL interno da usare con il comando `oozie`:</span><span class="sxs-lookup"><span data-stu-id="33041-166">This command returns a value similar to the following command, which contains the internal URL to use with the `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="33041-167">Per altre informazioni sull'uso dell'API REST Ambari, vedere [Gestire i cluster HDInsight mediante l'API REST Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="33041-167">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="33041-168">Accesso ad altri tipi di nodo</span><span class="sxs-lookup"><span data-stu-id="33041-168">Accessing other node types</span></span>

<span data-ttu-id="33041-169">È possibile connettersi ai nodi non accessibili direttamente tramite Internet usando i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="33041-169">You can connect to nodes that are not directly accessible over the internet by using the following methods:</span></span>

* <span data-ttu-id="33041-170">**SSH**: dopo avere stabilito la connessione a un nodo head usando SSH, è possibile usare SSH dal nodo head per connettersi ad altri nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-170">**SSH**: Once connected to a head node using SSH, you can then use SSH from the head node to connect to other nodes in the cluster.</span></span> <span data-ttu-id="33041-171">Per altre informazioni, vedere il documento [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="33041-171">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="33041-172">**Tunnel SSH**: se è necessario accedere a un servizio Web ospitato in uno dei nodi non esposti a Internet, è necessario usare un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="33041-172">**SSH Tunnel**: If you need to access a web service hosted on one of the nodes that is not exposed to the internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="33041-173">Per altre informazioni, vedere il documento [Usare il tunneling SSH per accedere all'interfaccia Web di Ambari, JobHistory, NameNode, Oozie e altre interfacce Web](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="33041-173">For more information, see the [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="33041-174">**Rete virtuale di Azure**: se il cluster HDInsight fa parte di una rete virtuale di Azure, tutte le risorse della stessa rete virtuale possono accedere direttamente a tutti i nodi del cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on the same Virtual Network can directly access all nodes in the cluster.</span></span> <span data-ttu-id="33041-175">Per altre informazioni, vedere il documento [Estendere le funzionalità di HDInsight usando la rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md).</span><span class="sxs-lookup"><span data-stu-id="33041-175">For more information, see the [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-to-check-on-a-service-status"></a><span data-ttu-id="33041-176">Come controllare lo stato di un servizio</span><span class="sxs-lookup"><span data-stu-id="33041-176">How to check on a service status</span></span>

<span data-ttu-id="33041-177">Per controllare lo stato dei servizi in esecuzione nei nodi head, usare l'interfaccia utente Web di Ambari o l'API REST Ambari.</span><span class="sxs-lookup"><span data-stu-id="33041-177">To check the status of services that run on the head nodes, use the Ambari Web UI or the Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="33041-178">Interfaccia utente Web Ambari</span><span class="sxs-lookup"><span data-stu-id="33041-178">Ambari Web UI</span></span>

<span data-ttu-id="33041-179">L'interfaccia utente Web Ambari è visualizzabile all'indirizzo https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="33041-179">The Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="33041-180">Sostituire **CLUSTERNAME** con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-180">Replace **CLUSTERNAME** with the name of your cluster.</span></span> <span data-ttu-id="33041-181">Se richiesto, immettere le credenziali dell’utente HTTP del cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-181">If prompted, enter the HTTP user credentials for your cluster.</span></span> <span data-ttu-id="33041-182">Il nome utente HTTP predefinito è **admin** e la password è la password inserita durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-182">The default HTTP user name is **admin** and the password is the password you entered when creating the cluster.</span></span>

<span data-ttu-id="33041-183">Nella pagina di Ambari i servizi installati sono elencati a sinistra.</span><span class="sxs-lookup"><span data-stu-id="33041-183">When you arrive on the Ambari page, the installed services are listed on the left of the page.</span></span>

![Servizi installati](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="33041-185">Esistono molte icone che possono essere visualizzate accanto a un servizio per indicare lo stato.</span><span class="sxs-lookup"><span data-stu-id="33041-185">There are a series of icons that may appear next to a service to indicate status.</span></span> <span data-ttu-id="33041-186">È possibile visualizzare eventuali avvisi relativi a un servizio utilizzando il collegamento **Avvisi** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="33041-186">Any alerts related to a service can be viewed using the **Alerts** link at the top of the page.</span></span> <span data-ttu-id="33041-187">È possibile selezionare ogni servizio per visualizzare ulteriori informazioni su di esso.</span><span class="sxs-lookup"><span data-stu-id="33041-187">You can select each service to view more information on it.</span></span>

<span data-ttu-id="33041-188">La pagina del servizio fornisce informazioni sullo stato e sulla configurazione di ogni servizio, ma non indica su quale nodo head esso è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="33041-188">While the service page provides information on the status and configuration of each service, it does not provide information on which head node the service is running on.</span></span> <span data-ttu-id="33041-189">Per visualizzare questa informazione,  utilizzare il collegamento **Host** nella parte superiore della pagina.</span><span class="sxs-lookup"><span data-stu-id="33041-189">To view this information, use the **Hosts** link at the top of the page.</span></span> <span data-ttu-id="33041-190">La pagina visualizza gli host del cluster, inclusi i nodi head.</span><span class="sxs-lookup"><span data-stu-id="33041-190">This page displays hosts within the cluster, including the head nodes.</span></span>

![elenco di host](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="33041-192">Quando si seleziona il collegamento per uno dei nodi head, vengono visualizzati i servizi e i componenti in esecuzione su tale nodo.</span><span class="sxs-lookup"><span data-stu-id="33041-192">Selecting the link for one of the head nodes displays the services and components running on that node.</span></span>

![Stato dei componenti](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="33041-194">Per altre informazioni sull'uso di Ambari, vedere [Gestire i cluster HDInsight mediante l'uso dell'interfaccia utente Web Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="33041-194">For more information on using Ambari, see [Monitor and manage HDInsight using the Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="33041-195">API REST Ambari</span><span class="sxs-lookup"><span data-stu-id="33041-195">Ambari REST API</span></span>

<span data-ttu-id="33041-196">L'API REST Ambari è disponibile su Internet.</span><span class="sxs-lookup"><span data-stu-id="33041-196">The Ambari REST API is available over the internet.</span></span> <span data-ttu-id="33041-197">Il gateway pubblico HDInsight gestisce il routing delle richieste per il nodo head che attualmente ospita l'API REST.</span><span class="sxs-lookup"><span data-stu-id="33041-197">The HDInsight public gateway handles routing requests to the head node that is currently hosting the REST API.</span></span>

<span data-ttu-id="33041-198">È possibile utilizzare il comando seguente per verificare lo stato di un servizio tramite l'API REST di Ambari:</span><span class="sxs-lookup"><span data-stu-id="33041-198">You can use the following command to check the state of a service through the Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="33041-199">Sostituire **PASSWORD** con la password dell'account dell'utente HTTP (admin).</span><span class="sxs-lookup"><span data-stu-id="33041-199">Replace **PASSWORD** with the HTTP user (admin) account password.</span></span>
* <span data-ttu-id="33041-200">Sostituire **CLUSTERNAME** con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-200">Replace **CLUSTERNAME** with the name of the cluster.</span></span>
* <span data-ttu-id="33041-201">Sostituire **SERVICENAME** con il nome del servizio di cui controllare lo stato.</span><span class="sxs-lookup"><span data-stu-id="33041-201">Replace **SERVICENAME** with the name of the service you want to check the status of.</span></span>

<span data-ttu-id="33041-202">Ad esempio, per controllare lo stato del servizio **HDFS** in un cluster denominato **mycluster**, con la password **password**, è necessario usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="33041-202">For example, to check the status of the **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use the following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="33041-203">La risposta restituita è simile al codice JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="33041-203">The response is similar to the following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="33041-204">L'URL indica che il servizio è attualmente in esecuzione sul nodo head denominato **hn0-CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="33041-204">The URL tells us that the service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="33041-205">Lo stato indica che il servizio è in esecuzione, o **AVVIATO**.</span><span class="sxs-lookup"><span data-stu-id="33041-205">The state tells us that the service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="33041-206">Se non si sa quali servizi siano installati nel cluster, è possibile usare il comando seguente per recuperarne l'elenco:</span><span class="sxs-lookup"><span data-stu-id="33041-206">If you do not know what services are installed on the cluster, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="33041-207">Per altre informazioni sull'uso dell'API REST Ambari, vedere [Gestire i cluster HDInsight mediante l'API REST Ambari](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="33041-207">For more information on working with the Ambari REST API, see [Monitor and Manage HDInsight using the Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="33041-208">Componenti del servizio</span><span class="sxs-lookup"><span data-stu-id="33041-208">Service components</span></span>

<span data-ttu-id="33041-209">I servizi possono includere componenti di cui si desidera controllare lo stato singolarmente.</span><span class="sxs-lookup"><span data-stu-id="33041-209">Services may contain components that you wish to check the status of individually.</span></span> <span data-ttu-id="33041-210">HDFS, ad esempio, contiene il componente NameNode.</span><span class="sxs-lookup"><span data-stu-id="33041-210">For example, HDFS contains the NameNode component.</span></span> <span data-ttu-id="33041-211">Per visualizzare informazioni su un componente, il comando è:</span><span class="sxs-lookup"><span data-stu-id="33041-211">To view information on a component, the command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="33041-212">Se non si sa quali componenti siano specificati da un servizio, è possibile usare il comando seguente per recuperarne l'elenco:</span><span class="sxs-lookup"><span data-stu-id="33041-212">If you do not know what components are provided by a service, you can use the following command to retrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-to-access-log-files-on-the-head-nodes"></a><span data-ttu-id="33041-213">Come accedere ai file di log nel nodo head</span><span class="sxs-lookup"><span data-stu-id="33041-213">How to access log files on the head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="33041-214">SSH</span><span class="sxs-lookup"><span data-stu-id="33041-214">SSH</span></span>

<span data-ttu-id="33041-215">Durante la connessione a un nodo head tramite SSH, i file di registro sono disponibili su **/var/log**.</span><span class="sxs-lookup"><span data-stu-id="33041-215">While connected to a head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="33041-216">Ad esempio, **/var/log/hadoop-yarn/yarn** contiene i registri per YARN.</span><span class="sxs-lookup"><span data-stu-id="33041-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="33041-217">Ogni nodo head può avere voci di registro univoche, perciò è consigliabile controllare i registri su entrambi.</span><span class="sxs-lookup"><span data-stu-id="33041-217">Each head node can have unique log entries, so you should check the logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="33041-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="33041-218">SFTP</span></span>

<span data-ttu-id="33041-219">È anche possibile connettersi al nodo head usando SSH File Transfer Protocol o Secure File Transfer Protocol (SFTP) e scaricare direttamente i file di log.</span><span class="sxs-lookup"><span data-stu-id="33041-219">You can also connect to the head node using the SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download the log files directly.</span></span>

<span data-ttu-id="33041-220">In modo analogo all'uso di un client SSH, quando si stabilisce la connessione al cluster è necessario specificare il nome dell'account utente SSH e l'indirizzo SSH del cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-220">Similar to using an SSH client, when connecting to the cluster you must provide the SSH user account name and the SSH address of the cluster.</span></span> <span data-ttu-id="33041-221">Ad esempio, `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="33041-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="33041-222">Specificare la password per l'account quando richiesto oppure specificare una chiave pubblica tramite il parametro `-i`.</span><span class="sxs-lookup"><span data-stu-id="33041-222">Provide the password for the account when prompted, or provide a public key using the `-i` parameter.</span></span>

<span data-ttu-id="33041-223">Una volta connessi, viene visualizzato un prompt `sftp>` .</span><span class="sxs-lookup"><span data-stu-id="33041-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="33041-224">Da questo prompt è possibile modificare le directory nonché caricare e scaricare i file.</span><span class="sxs-lookup"><span data-stu-id="33041-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="33041-225">Ad esempio, i comandi seguenti consentono di passare alla directory **/var/log/hadoop/hdfs** directory e quindi scaricare tutti i file nella directory.</span><span class="sxs-lookup"><span data-stu-id="33041-225">For example, the following commands change directories to the **/var/log/hadoop/hdfs** directory and then download all files in the directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="33041-226">Per un elenco di comandi disponibili, immettere `help` al prompt `sftp>`.</span><span class="sxs-lookup"><span data-stu-id="33041-226">For a list of available commands, enter `help` at the `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="33041-227">Esistono anche interfacce grafiche che consentono di visualizzare il file system quando si è connessi tramite SFTP.</span><span class="sxs-lookup"><span data-stu-id="33041-227">There are also graphical interfaces that allow you to visualize the file system when connected using SFTP.</span></span> <span data-ttu-id="33041-228">Ad esempio, [MobaXTerm](http://mobaxterm.mobatek.net/) consente di sfogliare il file system con un'interfaccia simile a Esplora risorse.</span><span class="sxs-lookup"><span data-stu-id="33041-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you to browse the file system using an interface similar to Windows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="33041-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="33041-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="33041-230">Per accedere ai file di log tramite Ambari, è necessario usare un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="33041-230">To access log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="33041-231">Le interfacce Web per i singoli servizi non sono esposte pubblicamente su Internet.</span><span class="sxs-lookup"><span data-stu-id="33041-231">The web interfaces for the individual services are not exposed publicly on the Internet.</span></span> <span data-ttu-id="33041-232">Per informazioni sull'uso del tunnel SSH, vedere il documento [Usare il tunneling SSH](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="33041-232">For information on using an SSH tunnel, see the [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="33041-233">Dall'interfaccia utente Web di Ambari, selezionare il servizio di cui si vogliono visualizzare i log, ad esempio, YARN.</span><span class="sxs-lookup"><span data-stu-id="33041-233">From the Ambari Web UI, select the service you wish to view logs for (for example, YARN).</span></span> <span data-ttu-id="33041-234">Usare quindi **Collegamenti rapidi** per selezionare il nodo head di cui visualizzare i log.</span><span class="sxs-lookup"><span data-stu-id="33041-234">Then use **Quick Links** to select which head node to view the logs for.</span></span>

![Utilizzo dei collegamenti rapidi per visualizzare i registri](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-to-configure-the-node-size"></a><span data-ttu-id="33041-236">Come configurare le dimensioni del nodo</span><span class="sxs-lookup"><span data-stu-id="33041-236">How to configure the node size</span></span>

<span data-ttu-id="33041-237">È possibile selezionare le dimensioni di un nodo solo durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="33041-237">The size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="33041-238">È possibile trovare un elenco delle varie dimensioni di VM disponibili per HDInsight sulla [pagina dei prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="33041-238">You can find a list of the different VM sizes available for HDInsight on the [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="33041-239">Quando si crea un cluster, è possibile specificare le dimensioni dei nodi.</span><span class="sxs-lookup"><span data-stu-id="33041-239">When creating a cluster, you can specify the size of the nodes.</span></span> <span data-ttu-id="33041-240">Di seguito viene illustrato come specificare le dimensioni usando il [portale di Azure][preview-portal], [Azure PowerShell][azure-powershell] e l'[interfaccia della riga di comando di Azure][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="33041-240">The following information provides guidance on how to specify the size using the [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and the [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="33041-241">**Portale di Azure**: quando si crea un cluster, è possibile impostare le dimensioni dei nodi usati dal cluster:</span><span class="sxs-lookup"><span data-stu-id="33041-241">**Azure portal**: When creating a cluster, you can set the size of the nodes used by the cluster:</span></span>

    ![Immagine della creazione guidata di cluster con la selezione delle dimensioni del nodo](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="33041-243">**Interfaccia della riga di comando di Azure**: quando si usa il comando `azure hdinsight cluster create`, è possibile impostare le dimensioni dei nodi head, di lavoro e ZooKeeper usando i parametri `--headNodeSize`, `--workerNodeSize` e `--zookeeperNodeSize`.</span><span class="sxs-lookup"><span data-stu-id="33041-243">**Azure CLI**: When using the `azure hdinsight cluster create` command, you can set the size of the head, worker, and ZooKeeper nodes by using the `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="33041-244">**Azure PowerShell**: quando si usa il cmdlet `New-AzureRmHDInsightCluster`, è possibile impostare le dimensioni dei nodi head, di lavoro e ZooKeeper usando i parametri `-HeadNodeVMSize`, `-WorkerNodeSize` e `-ZookeeperNodeSize`.</span><span class="sxs-lookup"><span data-stu-id="33041-244">**Azure PowerShell**: When using the `New-AzureRmHDInsightCluster` cmdlet, you can set the size of the head, worker, and ZooKeeper nodes by using the `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33041-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="33041-245">Next steps</span></span>

<span data-ttu-id="33041-246">Per altre informazioni sugli aspetti menzionati in questo documento, usare i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="33041-246">Use the following links to learn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="33041-247">Riferimento REST Ambari</span><span class="sxs-lookup"><span data-stu-id="33041-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="33041-248">Installare e configurare l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="33041-248">Install and configure the Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="33041-249">Installare e configurare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="33041-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="33041-250">Gestire HDInsight tramite Ambari</span><span class="sxs-lookup"><span data-stu-id="33041-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="33041-251">Effettuare il provisioning di cluster HDInsight basati su Linux</span><span class="sxs-lookup"><span data-stu-id="33041-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
