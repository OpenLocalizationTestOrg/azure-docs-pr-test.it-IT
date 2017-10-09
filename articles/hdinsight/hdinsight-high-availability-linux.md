---
title: "disponibilità aaaHigh per Hadoop - HDInsight di Azure | Documenti Microsoft"
description: "Informazioni su come i cluster HDInsight migliorano l'affidabilità e la disponibilità tramite l'uso di un nodo head aggiuntivo. Informazioni su come ciò influisce sulla servizi Hadoop, ad esempio Ambari e Hive, nonché come tooindividually connettersi tooeach nodo head con SSH."
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
ms.openlocfilehash: 9ff62afe6b63b241cb984225233157219f8d7411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="availability-and-reliability-of-hadoop-clusters-in-hdinsight"></a><span data-ttu-id="925e0-105">Disponibilità e affidabilità dei cluster Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="925e0-105">Availability and reliability of Hadoop clusters in HDInsight</span></span>

<span data-ttu-id="925e0-106">Cluster HDInsight forniscono due nodi head tooincrease hello disponibilità e l'affidabilità dei servizi di Hadoop e i processi in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="925e0-106">HDInsight clusters provide two head nodes tooincrease hello availability and reliability of Hadoop services and jobs running.</span></span>

<span data-ttu-id="925e0-107">Hadoop ottiene alta disponibilità e affidabilità replicando i servizi e i dati su più nodi di un cluster.</span><span class="sxs-lookup"><span data-stu-id="925e0-107">Hadoop achieves high availability and reliability by replicating services and data across multiple nodes in a cluster.</span></span> <span data-ttu-id="925e0-108">Tuttavia le distribuzioni standard di Hadoop hanno in genere un singolo nodo head.</span><span class="sxs-lookup"><span data-stu-id="925e0-108">However standard distributions of Hadoop typically have only a single head node.</span></span> <span data-ttu-id="925e0-109">Qualsiasi interruzione del nodo head singolo hello può causare lavoro toostop di hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="925e0-109">Any outage of hello single head node can cause hello cluster toostop working.</span></span> <span data-ttu-id="925e0-110">HDInsight fornisce due headnodes tooimprove Hadoop disponibilità e affidabilità.</span><span class="sxs-lookup"><span data-stu-id="925e0-110">HDInsight provides two headnodes tooimprove Hadoop's availability and reliability.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="925e0-111">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="925e0-111">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="925e0-112">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="925e0-112">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="availability-and-reliability-of-nodes"></a><span data-ttu-id="925e0-113">Disponibilità e affidabilità dei nodi</span><span class="sxs-lookup"><span data-stu-id="925e0-113">Availability and reliability of nodes</span></span>

<span data-ttu-id="925e0-114">I nodi in un cluster HDInsight vengono implementati con macchine virtuali di Azure.</span><span class="sxs-lookup"><span data-stu-id="925e0-114">Nodes in an HDInsight cluster are implemented using Azure Virtual Machines.</span></span> <span data-ttu-id="925e0-115">Hello nelle sezioni seguenti vengono illustrano i tipi di nodo singolo hello utilizzati con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="925e0-115">hello following sections discuss hello individual node types used with HDInsight.</span></span> 

> [!NOTE]
> <span data-ttu-id="925e0-116">Non tutti i tipi di nodo vengono usati per un tipo di cluster.</span><span class="sxs-lookup"><span data-stu-id="925e0-116">Not all node types are used for a cluster type.</span></span> <span data-ttu-id="925e0-117">Ad esempio, un tipo di cluster Hadoop non ha alcun nodo Nimbus.</span><span class="sxs-lookup"><span data-stu-id="925e0-117">For example, a Hadoop cluster type does not have any Nimbus nodes.</span></span> <span data-ttu-id="925e0-118">Per ulteriori informazioni sui nodi utilizzato dai tipi di cluster HDInsight, vedere sezione tipi di Cluster hello di hello [cluster basati su Linux creare Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) documento.</span><span class="sxs-lookup"><span data-stu-id="925e0-118">For more information on nodes used by HDInsight cluster types, see hello Cluster types section of hello [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) document.</span></span>

### <a name="head-nodes"></a><span data-ttu-id="925e0-119">Nodi head</span><span class="sxs-lookup"><span data-stu-id="925e0-119">Head nodes</span></span>

<span data-ttu-id="925e0-120">tooensure un'elevata disponibilità dei servizi Hadoop, HDInsight fornisce due nodi head.</span><span class="sxs-lookup"><span data-stu-id="925e0-120">tooensure high availability of Hadoop services, HDInsight provides two head nodes.</span></span> <span data-ttu-id="925e0-121">Entrambi i nodi head sono contemporaneamente attivi e in esecuzione all'interno del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-121">Both head nodes are active and running within hello HDInsight cluster simultaneously.</span></span> <span data-ttu-id="925e0-122">Alcuni servizi, ad esempio HDFS o YARN, sono "attivi"in qualsiasi momento soltanto in un nodo head.</span><span class="sxs-lookup"><span data-stu-id="925e0-122">Some services, such as HDFS or YARN, are only 'active' on one head node at any given time.</span></span> <span data-ttu-id="925e0-123">Altri servizi, ad esempio HiveServer2 o MetaStore Hive sono attivi su entrambi i nodi head in hello contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="925e0-123">Other services such as HiveServer2 or Hive MetaStore are active on both head nodes at hello same time.</span></span>

<span data-ttu-id="925e0-124">I nodi HEAD (e gli altri nodi in HDInsight) hanno un valore numerico come parte del nome host hello del nodo hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-124">Head nodes (and other nodes in HDInsight) have a numeric value as part of hello hostname of hello node.</span></span> <span data-ttu-id="925e0-125">Ad esempio, `hn0-CLUSTERNAME` o `hn4-CLUSTERNAME`.</span><span class="sxs-lookup"><span data-stu-id="925e0-125">For example, `hn0-CLUSTERNAME` or `hn4-CLUSTERNAME`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="925e0-126">Non associare il valore numerico hello con tratti di un nodo primario o secondario.</span><span class="sxs-lookup"><span data-stu-id="925e0-126">Do not associate hello numeric value with whether a node is primary or secondary.</span></span> <span data-ttu-id="925e0-127">valore numerico di Hello è presente tooprovide solo un nome univoco per ogni nodo.</span><span class="sxs-lookup"><span data-stu-id="925e0-127">hello numeric value is only present tooprovide a unique name for each node.</span></span>

### <a name="nimbus-nodes"></a><span data-ttu-id="925e0-128">Nodi Nimbus</span><span class="sxs-lookup"><span data-stu-id="925e0-128">Nimbus Nodes</span></span>

<span data-ttu-id="925e0-129">I nodi nimbus sono disponibili con i cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="925e0-129">Nimbus nodes are available with Storm clusters.</span></span> <span data-ttu-id="925e0-130">nodi Nimbus Hello forniscono simili funzionalità toohello Hadoop JobTracker per la distribuzione e il monitoraggio di elaborazione tra i nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="925e0-130">hello Nimbus nodes provide similar functionality toohello Hadoop JobTracker by distributing and monitoring processing across worker nodes.</span></span> <span data-ttu-id="925e0-131">HDInsight offre due nodi Nimbus per i cluster Storm</span><span class="sxs-lookup"><span data-stu-id="925e0-131">HDInsight provides two Nimbus nodes for Storm clusters</span></span>

### <a name="zookeeper-nodes"></a><span data-ttu-id="925e0-132">Nodi Zookeeper</span><span class="sxs-lookup"><span data-stu-id="925e0-132">Zookeeper nodes</span></span>

<span data-ttu-id="925e0-133">I nodi [ZooKeeper](http://zookeeper.apache.org/) vengono usati per la designazione di leader dei servizi master nei nodi head.</span><span class="sxs-lookup"><span data-stu-id="925e0-133">[ZooKeeper](http://zookeeper.apache.org/) nodes are used for leader election of master services on head nodes.</span></span> <span data-ttu-id="925e0-134">Sono anche utilizzati tooinsure che servizi, nodi di dati (lavoratore) e gateway sapere quale nodo head è attivo in un servizio principale.</span><span class="sxs-lookup"><span data-stu-id="925e0-134">They are also used tooinsure that services, data (worker) nodes, and gateways know which head node a master service is active on.</span></span> <span data-ttu-id="925e0-135">Per impostazione predefinita, HDInsight specifica tre nodi ZooKeeper.</span><span class="sxs-lookup"><span data-stu-id="925e0-135">By default, HDInsight provides three ZooKeeper nodes.</span></span>

### <a name="worker-nodes"></a><span data-ttu-id="925e0-136">Nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="925e0-136">Worker nodes</span></span>

<span data-ttu-id="925e0-137">Nodi di lavoro eseguono analisi di dati effettivi hello quando cluster toohello inviato è un processo.</span><span class="sxs-lookup"><span data-stu-id="925e0-137">Worker nodes perform hello actual data analysis when a job is submitted toohello cluster.</span></span> <span data-ttu-id="925e0-138">Se un nodo di lavoro non riesce, attività hello che stava eseguendo è il nodo di lavoro tooanother inviato.</span><span class="sxs-lookup"><span data-stu-id="925e0-138">If a worker node fails, hello task that it was performing is submitted tooanother worker node.</span></span> <span data-ttu-id="925e0-139">Per impostazione predefinita, HDInsight crea quattro nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="925e0-139">By default, HDInsight creates four worker nodes.</span></span> <span data-ttu-id="925e0-140">È possibile modificare questo numero toosuit esigenze durante e dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="925e0-140">You can change this number toosuit your needs both during and after cluster creation.</span></span>

### <a name="edge-node"></a><span data-ttu-id="925e0-141">Nodo perimetrale</span><span class="sxs-lookup"><span data-stu-id="925e0-141">Edge node</span></span>

<span data-ttu-id="925e0-142">Analisi dei dati all'interno di cluster hello non partecipa attivamente un nodo del bordo.</span><span class="sxs-lookup"><span data-stu-id="925e0-142">An edge node does not actively participate in data analysis within hello cluster.</span></span> <span data-ttu-id="925e0-143">Viene usato dagli sviluppatori o i data scientist quando lavorano con Hadoop.</span><span class="sxs-lookup"><span data-stu-id="925e0-143">It is used by developers or data scientists when working with Hadoop.</span></span> <span data-ttu-id="925e0-144">vite di nodo edge Hello in hello stessa rete virtuale di Azure come hello altri nodi cluster hello e accedere direttamente a tutti gli altri nodi.</span><span class="sxs-lookup"><span data-stu-id="925e0-144">hello edge node lives in hello same Azure Virtual Network as hello other nodes in hello cluster, and can directly access all other nodes.</span></span> <span data-ttu-id="925e0-145">Hello edge nodo può essere utilizzato senza portare le risorse da servizi critici di Hadoop o i processi di analisi.</span><span class="sxs-lookup"><span data-stu-id="925e0-145">hello edge node can be used without taking resources away from critical Hadoop services or analysis jobs.</span></span>

<span data-ttu-id="925e0-146">Attualmente, il Server di R in HDInsight è hello unico tipo di cluster che fornisce un nodo del bordo per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="925e0-146">Currently, R Server on HDInsight is hello only cluster type that provides an edge node by default.</span></span> <span data-ttu-id="925e0-147">Per il Server di R in HDInsight, hello bordo viene usato il codice R di test in locale nel nodo hello prima di inviarla toohello cluster per l'elaborazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="925e0-147">For R Server on HDInsight, hello edge node is used test R code locally on hello node before submitting it toohello cluster for distributed processing.</span></span>

<span data-ttu-id="925e0-148">Per informazioni sull'uso di un nodo del bordo con tipi di cluster diverso dal Server di R, vedere hello [utilizzare nodi periferici in HDInsight](hdinsight-apps-use-edge-node.md) documento.</span><span class="sxs-lookup"><span data-stu-id="925e0-148">For information on using an edge node with cluster types other than R Server, see hello [Use edge nodes in HDInsight](hdinsight-apps-use-edge-node.md) document.</span></span>

## <a name="accessing-hello-nodes"></a><span data-ttu-id="925e0-149">Accesso ai nodi di hello</span><span class="sxs-lookup"><span data-stu-id="925e0-149">Accessing hello nodes</span></span>

<span data-ttu-id="925e0-150">Cluster di accesso toohello su hello internet viene fornito tramite un gateway pubblico.</span><span class="sxs-lookup"><span data-stu-id="925e0-150">Access toohello cluster over hello internet is provided through a public gateway.</span></span> <span data-ttu-id="925e0-151">L'accesso è limitato tooconnecting toohello i nodi head e (se presente) hello nodo del bordo.</span><span class="sxs-lookup"><span data-stu-id="925e0-151">Access is limited tooconnecting toohello head nodes and (if one exists) hello edge node.</span></span> <span data-ttu-id="925e0-152">Accesso tooservices in esecuzione nei nodi head hello non viene effettuata con più nodi head.</span><span class="sxs-lookup"><span data-stu-id="925e0-152">Access tooservices running on hello head nodes is not effected by having multiple head nodes.</span></span> <span data-ttu-id="925e0-153">Hello gateway pubblica le route richieste toohello nodo head che ospita hello servizio richiesto.</span><span class="sxs-lookup"><span data-stu-id="925e0-153">hello public gateway routes requests toohello head node that hosts hello requested service.</span></span> <span data-ttu-id="925e0-154">Ad esempio, se Ambari è attualmente ospitato nel nodo head secondario hello, gateway hello instrada le richieste in ingresso per il nodo toothat Ambari.</span><span class="sxs-lookup"><span data-stu-id="925e0-154">For example, if Ambari is currently hosted on hello secondary head node, hello gateway routes incoming requests for Ambari toothat node.</span></span>

<span data-ttu-id="925e0-155">Accesso tramite gateway pubblica hello è limitato tooport 443 (HTTPS), 22 e 23.</span><span class="sxs-lookup"><span data-stu-id="925e0-155">Access over hello public gateway is limited tooport 443 (HTTPS), 22, and 23.</span></span>

* <span data-ttu-id="925e0-156">Porta __443__ è usato tooaccess Ambari e altri web dell'interfaccia utente o le API REST ospitate nei nodi head hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-156">Port __443__ is used tooaccess Ambari and other web UI or REST APIs hosted on hello head nodes.</span></span>

* <span data-ttu-id="925e0-157">Porta __22__ nodo head di tooaccess utilizzati hello primario o nodo di bordo con SSH.</span><span class="sxs-lookup"><span data-stu-id="925e0-157">Port __22__ is used tooaccess hello primary head node or edge node with SSH.</span></span>

* <span data-ttu-id="925e0-158">Porta __23__ è usato tooaccess hello secondario nodo head con SSH.</span><span class="sxs-lookup"><span data-stu-id="925e0-158">Port __23__ is used tooaccess hello secondary head node with SSH.</span></span> <span data-ttu-id="925e0-159">Ad esempio, `ssh username@mycluster-ssh.azurehdinsight.net` si connette toohello primario nodo head del cluster di hello denominato **mycluster**.</span><span class="sxs-lookup"><span data-stu-id="925e0-159">For example, `ssh username@mycluster-ssh.azurehdinsight.net` connects toohello primary head node of hello cluster named **mycluster**.</span></span>

<span data-ttu-id="925e0-160">Per ulteriori informazioni sull'utilizzo di SSH, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="925e0-160">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

### <a name="internal-fully-qualified-domain-names-fqdn"></a><span data-ttu-id="925e0-161">Nomi di dominio completo interni (FQDN) </span><span class="sxs-lookup"><span data-stu-id="925e0-161">Internal fully qualified domain names (FQDN)</span></span>

<span data-ttu-id="925e0-162">I nodi in un cluster HDInsight dispongono di un indirizzo IP e un nome di dominio completo è accessibile solo dal cluster hello interno.</span><span class="sxs-lookup"><span data-stu-id="925e0-162">Nodes in an HDInsight cluster have an internal IP address and FQDN that can only be accessed from hello cluster.</span></span> <span data-ttu-id="925e0-163">Quando si accede ai servizi in cluster hello utilizzando hello interno FQDN o indirizzo IP, è consigliabile utilizzare Ambari tooverify hello IP o FQDN toouse durante l'accesso servizio hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-163">When accessing services on hello cluster using hello internal FQDN or IP address, you should use Ambari tooverify hello IP or FQDN toouse when accessing hello service.</span></span>

<span data-ttu-id="925e0-164">Ad esempio, hello Oozie servizio può essere eseguito solo su un nodo head e utilizzando hello `oozie` comando da una sessione SSH richiede servizio toohello di hello URL.</span><span class="sxs-lookup"><span data-stu-id="925e0-164">For example, hello Oozie service can only run on one head node, and using hello `oozie` command from an SSH session requires hello URL toohello service.</span></span> <span data-ttu-id="925e0-165">Questo URL può essere recuperato da Ambari tramite hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="925e0-165">This URL can be retrieved from Ambari by using hello following command:</span></span>

    curl -u admin:PASSWORD "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/configurations?type=oozie-site&tag=TOPOLOGY_RESOLVED" | grep oozie.base.url

<span data-ttu-id="925e0-166">Questo comando restituisce un toohello simile valore seguente comando, che contiene hello interno URL toouse con hello `oozie` comando:</span><span class="sxs-lookup"><span data-stu-id="925e0-166">This command returns a value similar toohello following command, which contains hello internal URL toouse with hello `oozie` command:</span></span>

    "oozie.base.url": "http://hn0-CLUSTERNAME-randomcharacters.cx.internal.cloudapp.net:11000/oozie"

<span data-ttu-id="925e0-167">Per ulteriori informazioni sull'uso di API REST Ambari hello, vedere [monitorare e gestire HDInsight utilizzando l'API REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="925e0-167">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

### <a name="accessing-other-node-types"></a><span data-ttu-id="925e0-168">Accesso ad altri tipi di nodo</span><span class="sxs-lookup"><span data-stu-id="925e0-168">Accessing other node types</span></span>

<span data-ttu-id="925e0-169">È possibile connettersi toonodes che sono non direttamente accessibile su internet di hello utilizzando hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="925e0-169">You can connect toonodes that are not directly accessible over hello internet by using hello following methods:</span></span>

* <span data-ttu-id="925e0-170">**SSH**: una volta connessi tooa nodo head con SSH, è quindi possibile utilizzare SSH da hello nodo head tooconnect tooother i nodi nel cluster hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-170">**SSH**: Once connected tooa head node using SSH, you can then use SSH from hello head node tooconnect tooother nodes in hello cluster.</span></span> <span data-ttu-id="925e0-171">Per ulteriori informazioni, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="925e0-171">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

* <span data-ttu-id="925e0-172">**Tunnel SSH**: se è necessario tooaccess un servizio web ospitato in uno dei nodi di hello che non è esposta toohello internet, è necessario utilizzare un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="925e0-172">**SSH Tunnel**: If you need tooaccess a web service hosted on one of hello nodes that is not exposed toohello internet, you must use an SSH tunnel.</span></span> <span data-ttu-id="925e0-173">Per ulteriori informazioni, vedere hello [utilizzare un tunnel SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="925e0-173">For more information, see hello [Use an SSH tunnel with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

* <span data-ttu-id="925e0-174">**Rete virtuale di Azure**: se hello di HDInsight cluster fa parte di una rete virtuale di Azure, tutte le risorse della stessa rete virtuale possono accedere direttamente ai tutti i nodi cluster hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-174">**Azure Virtual Network**: If your HDInsight cluster is part of an Azure Virtual Network, any resource on hello same Virtual Network can directly access all nodes in hello cluster.</span></span> <span data-ttu-id="925e0-175">Per ulteriori informazioni, vedere hello [estendere HDInsight mediante la rete virtuale di Azure](hdinsight-extend-hadoop-virtual-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="925e0-175">For more information, see hello [Extend HDInsight using Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span>

## <a name="how-toocheck-on-a-service-status"></a><span data-ttu-id="925e0-176">Come toocheck in uno stato di servizio</span><span class="sxs-lookup"><span data-stu-id="925e0-176">How toocheck on a service status</span></span>

<span data-ttu-id="925e0-177">lo stato di hello toocheck di servizi in esecuzione nei nodi head hello, utilizzare hello dell'interfaccia utente Web Ambari o hello Ambari REST API.</span><span class="sxs-lookup"><span data-stu-id="925e0-177">toocheck hello status of services that run on hello head nodes, use hello Ambari Web UI or hello Ambari REST API.</span></span>

### <a name="ambari-web-ui"></a><span data-ttu-id="925e0-178">Interfaccia utente Web Ambari</span><span class="sxs-lookup"><span data-stu-id="925e0-178">Ambari Web UI</span></span>

<span data-ttu-id="925e0-179">interfaccia utente Web Ambari Hello è visualizzabile in https://CLUSTERNAME.azurehdinsight.net.</span><span class="sxs-lookup"><span data-stu-id="925e0-179">hello Ambari Web UI is viewable at https://CLUSTERNAME.azurehdinsight.net.</span></span> <span data-ttu-id="925e0-180">Sostituire **CLUSTERNAME** con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="925e0-180">Replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="925e0-181">Se richiesto, immettere le credenziali utente di hello HTTP per il cluster.</span><span class="sxs-lookup"><span data-stu-id="925e0-181">If prompted, enter hello HTTP user credentials for your cluster.</span></span> <span data-ttu-id="925e0-182">è il nome utente HTTP predefinito Hello **admin** e hello password è hello immessi durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-182">hello default HTTP user name is **admin** and hello password is hello password you entered when creating hello cluster.</span></span>

<span data-ttu-id="925e0-183">Quando si arriva nella pagina Ambari hello, servizi di hello installato sono elencati in a sinistra della pagina hello hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-183">When you arrive on hello Ambari page, hello installed services are listed on hello left of hello page.</span></span>

![Servizi installati](./media/hdinsight-high-availability-linux/services.png)

<span data-ttu-id="925e0-185">Esistono una serie di icone che possono essere visualizzati lo stato successivo tooindicate del servizio tooa.</span><span class="sxs-lookup"><span data-stu-id="925e0-185">There are a series of icons that may appear next tooa service tooindicate status.</span></span> <span data-ttu-id="925e0-186">Tutti gli avvisi correlati tooa servizio può essere visualizzato utilizzando hello **avvisi** collegamento nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-186">Any alerts related tooa service can be viewed using hello **Alerts** link at hello top of hello page.</span></span> <span data-ttu-id="925e0-187">È possibile selezionare ogni tooview servizio ulteriori informazioni su di esso.</span><span class="sxs-lookup"><span data-stu-id="925e0-187">You can select each service tooview more information on it.</span></span>

<span data-ttu-id="925e0-188">Pagina servizio hello offre informazioni sullo stato di hello e configurazione di ogni servizio, non fornisce informazioni in cui il servizio di hello nodo head è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="925e0-188">While hello service page provides information on hello status and configuration of each service, it does not provide information on which head node hello service is running on.</span></span> <span data-ttu-id="925e0-189">tooview questa informazioni, utilizzare hello **host** collegamento nella parte superiore di hello della pagina hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-189">tooview this information, use hello **Hosts** link at hello top of hello page.</span></span> <span data-ttu-id="925e0-190">Questa pagina consente di visualizzare gli host in cluster hello, inclusi i nodi head hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-190">This page displays hosts within hello cluster, including hello head nodes.</span></span>

![elenco di host](./media/hdinsight-high-availability-linux/hosts.png)

<span data-ttu-id="925e0-192">Collegamento hello selezionando per uno dei nodi head hello Visualizza servizi hello e componenti in esecuzione su tale nodo.</span><span class="sxs-lookup"><span data-stu-id="925e0-192">Selecting hello link for one of hello head nodes displays hello services and components running on that node.</span></span>

![Stato dei componenti](./media/hdinsight-high-availability-linux/nodeservices.png)

<span data-ttu-id="925e0-194">Per ulteriori informazioni sull'utilizzo Ambari, vedere [Monitor e gestire HDInsight mediante hello dell'interfaccia utente Web Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="925e0-194">For more information on using Ambari, see [Monitor and manage HDInsight using hello Ambari Web UI](hdinsight-hadoop-manage-ambari.md).</span></span>

### <a name="ambari-rest-api"></a><span data-ttu-id="925e0-195">API REST Ambari</span><span class="sxs-lookup"><span data-stu-id="925e0-195">Ambari REST API</span></span>

<span data-ttu-id="925e0-196">API REST Ambari Hello è disponibile sulla hello internet.</span><span class="sxs-lookup"><span data-stu-id="925e0-196">hello Ambari REST API is available over hello internet.</span></span> <span data-ttu-id="925e0-197">gateway di Hello HDInsight pubblica gestisce richieste toohello head nodo di routing che attualmente ospita hello API REST.</span><span class="sxs-lookup"><span data-stu-id="925e0-197">hello HDInsight public gateway handles routing requests toohello head node that is currently hosting hello REST API.</span></span>

<span data-ttu-id="925e0-198">È possibile utilizzare hello stato hello toocheck del comando di un servizio tramite l'API REST Ambari hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="925e0-198">You can use hello following command toocheck hello state of a service through hello Ambari REST API:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICENAME?fields=ServiceInfo/state

* <span data-ttu-id="925e0-199">Sostituire **PASSWORD** con password dell'account utente (amministrazione) hello HTTP.</span><span class="sxs-lookup"><span data-stu-id="925e0-199">Replace **PASSWORD** with hello HTTP user (admin) account password.</span></span>
* <span data-ttu-id="925e0-200">Sostituire **CLUSTERNAME** con nome hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-200">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>
* <span data-ttu-id="925e0-201">Sostituire **SERVICENAME** con nome hello del servizio hello da toocheck hello stato.</span><span class="sxs-lookup"><span data-stu-id="925e0-201">Replace **SERVICENAME** with hello name of hello service you want toocheck hello status of.</span></span>

<span data-ttu-id="925e0-202">Ad esempio, lo stato hello toocheck di hello **HDFS** servizio in un cluster denominato **mycluster**, con una password di **password**, si utilizzerebbe hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="925e0-202">For example, toocheck hello status of hello **HDFS** service on a cluster named **mycluster**, with a password of **password**, you would use hello following command:</span></span>

    curl -u admin:password https://mycluster.azurehdinsight.net/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state

<span data-ttu-id="925e0-203">risposta Hello è simile toohello JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="925e0-203">hello response is similar toohello following JSON:</span></span>

    {
      "href" : "http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8080/api/v1/clusters/mycluster/services/HDFS?fields=ServiceInfo/state",
      "ServiceInfo" : {
        "cluster_name" : "mycluster",
        "service_name" : "HDFS",
        "state" : "STARTED"
      }
    }

<span data-ttu-id="925e0-204">Hello URL indica che il servizio di hello è attualmente in esecuzione in un nodo head denominato **hn0 CLUSTERNAME**.</span><span class="sxs-lookup"><span data-stu-id="925e0-204">hello URL tells us that hello service is currently running on a head node named **hn0-CLUSTERNAME**.</span></span>

<span data-ttu-id="925e0-205">Hello stato indica che il servizio di hello è attualmente in esecuzione, o **STARTED**.</span><span class="sxs-lookup"><span data-stu-id="925e0-205">hello state tells us that hello service is currently running, or **STARTED**.</span></span>

<span data-ttu-id="925e0-206">Se non si conosce quali servizi sono installati nel cluster hello, è possibile utilizzare hello comando tooretrieve un elenco di seguito:</span><span class="sxs-lookup"><span data-stu-id="925e0-206">If you do not know what services are installed on hello cluster, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services

<span data-ttu-id="925e0-207">Per ulteriori informazioni sull'uso di API REST Ambari hello, vedere [monitorare e gestire HDInsight utilizzando l'API REST Ambari hello](hdinsight-hadoop-manage-ambari-rest-api.md).</span><span class="sxs-lookup"><span data-stu-id="925e0-207">For more information on working with hello Ambari REST API, see [Monitor and Manage HDInsight using hello Ambari REST API](hdinsight-hadoop-manage-ambari-rest-api.md).</span></span>

#### <a name="service-components"></a><span data-ttu-id="925e0-208">Componenti del servizio</span><span class="sxs-lookup"><span data-stu-id="925e0-208">Service components</span></span>

<span data-ttu-id="925e0-209">Servizi potrebbero contenere componenti che si desidera toocheck hello stato singolarmente.</span><span class="sxs-lookup"><span data-stu-id="925e0-209">Services may contain components that you wish toocheck hello status of individually.</span></span> <span data-ttu-id="925e0-210">Ad esempio, HDFS contiene componente NameNode hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-210">For example, HDFS contains hello NameNode component.</span></span> <span data-ttu-id="925e0-211">tooview informazioni su un componente, il comando hello è:</span><span class="sxs-lookup"><span data-stu-id="925e0-211">tooview information on a component, hello command would be:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

<span data-ttu-id="925e0-212">Se non si conosce quali componenti vengono forniti da un servizio, è possibile utilizzare hello comando tooretrieve un elenco di seguito:</span><span class="sxs-lookup"><span data-stu-id="925e0-212">If you do not know what components are provided by a service, you can use hello following command tooretrieve a list:</span></span>

    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/SERVICE/components/component

## <a name="how-tooaccess-log-files-on-hello-head-nodes"></a><span data-ttu-id="925e0-213">Come tooaccess file di registro in nodi head hello</span><span class="sxs-lookup"><span data-stu-id="925e0-213">How tooaccess log files on hello head nodes</span></span>

### <a name="ssh"></a><span data-ttu-id="925e0-214">SSH</span><span class="sxs-lookup"><span data-stu-id="925e0-214">SSH</span></span>

<span data-ttu-id="925e0-215">Durante il nodo head di tooa connesso tramite SSH, i file di log sono reperibile nella **var/log**.</span><span class="sxs-lookup"><span data-stu-id="925e0-215">While connected tooa head node through SSH, log files can be found under **/var/log**.</span></span> <span data-ttu-id="925e0-216">Ad esempio, **/var/log/hadoop-yarn/yarn** contiene i registri per YARN.</span><span class="sxs-lookup"><span data-stu-id="925e0-216">For example, **/var/log/hadoop-yarn/yarn** contain logs for YARN.</span></span>

<span data-ttu-id="925e0-217">Ogni nodo head può contenere le voci di log univoco, è consigliabile controllare entrambi accede hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-217">Each head node can have unique log entries, so you should check hello logs on both.</span></span>

### <a name="sftp"></a><span data-ttu-id="925e0-218">SFTP</span><span class="sxs-lookup"><span data-stu-id="925e0-218">SFTP</span></span>

<span data-ttu-id="925e0-219">È possibile connettersi toohello nodo head usando hello SSH File Transfer Protocol o Secure File Transfer Protocol (SFTP) e scaricare i file di log hello direttamente.</span><span class="sxs-lookup"><span data-stu-id="925e0-219">You can also connect toohello head node using hello SSH File Transfer Protocol or Secure File Transfer Protocol (SFTP), and download hello log files directly.</span></span>

<span data-ttu-id="925e0-220">Toousing simili quando ci si connette toohello cluster è necessario fornire un client SSH hello SSH utente account name e hello SSH l'indirizzo del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-220">Similar toousing an SSH client, when connecting toohello cluster you must provide hello SSH user account name and hello SSH address of hello cluster.</span></span> <span data-ttu-id="925e0-221">ad esempio `sftp username@mycluster-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="925e0-221">For example, `sftp username@mycluster-ssh.azurehdinsight.net`.</span></span> <span data-ttu-id="925e0-222">Specificare password hello per conto di hello quando richiesto, o fornire una chiave pubblica utilizzando hello `-i` parametro.</span><span class="sxs-lookup"><span data-stu-id="925e0-222">Provide hello password for hello account when prompted, or provide a public key using hello `-i` parameter.</span></span>

<span data-ttu-id="925e0-223">Una volta connessi, viene visualizzato un prompt `sftp>` .</span><span class="sxs-lookup"><span data-stu-id="925e0-223">Once connected, you are presented with a `sftp>` prompt.</span></span> <span data-ttu-id="925e0-224">Da questo prompt è possibile modificare le directory nonché caricare e scaricare i file.</span><span class="sxs-lookup"><span data-stu-id="925e0-224">From this prompt, you can change directories, upload, and download files.</span></span> <span data-ttu-id="925e0-225">Ad esempio, hello seguenti comandi cambiare directory toohello **/var/log/hadoop/hdfs** directory e quindi scaricare tutti i file nella directory hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-225">For example, hello following commands change directories toohello **/var/log/hadoop/hdfs** directory and then download all files in hello directory.</span></span>

    cd /var/log/hadoop/hdfs
    get *

<span data-ttu-id="925e0-226">Per un elenco di comandi disponibili, immettere `help` in hello `sftp>` prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="925e0-226">For a list of available commands, enter `help` at hello `sftp>` prompt.</span></span>

> [!NOTE]
> <span data-ttu-id="925e0-227">Esistono anche interfacce grafiche che consentono di toovisualize hello file system quando connesso tramite SFTP.</span><span class="sxs-lookup"><span data-stu-id="925e0-227">There are also graphical interfaces that allow you toovisualize hello file system when connected using SFTP.</span></span> <span data-ttu-id="925e0-228">Ad esempio, [MobaXTerm](http://mobaxterm.mobatek.net/) consente toobrowse hello file system utilizzando un tooWindows simile interfaccia Explorer.</span><span class="sxs-lookup"><span data-stu-id="925e0-228">For example, [MobaXTerm](http://mobaxterm.mobatek.net/) allows you toobrowse hello file system using an interface similar tooWindows Explorer.</span></span>

### <a name="ambari"></a><span data-ttu-id="925e0-229">Ambari</span><span class="sxs-lookup"><span data-stu-id="925e0-229">Ambari</span></span>

> [!NOTE]
> <span data-ttu-id="925e0-230">tooaccess con Ambari i file di log, è necessario utilizzare un tunnel SSH.</span><span class="sxs-lookup"><span data-stu-id="925e0-230">tooaccess log files using Ambari, you must use an SSH tunnel.</span></span> <span data-ttu-id="925e0-231">interfacce di Hello web per i singoli servizi hello non vengono esposte pubblicamente hello Internet.</span><span class="sxs-lookup"><span data-stu-id="925e0-231">hello web interfaces for hello individual services are not exposed publicly on hello Internet.</span></span> <span data-ttu-id="925e0-232">Per informazioni sull'utilizzo di un tunnel SSH, vedere hello [usare SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="925e0-232">For information on using an SSH tunnel, see hello [Use SSH Tunneling](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="925e0-233">Hello dell'interfaccia utente Web Ambari, selezionare servizio hello desiderato tooview registri per (ad esempio, YARN).</span><span class="sxs-lookup"><span data-stu-id="925e0-233">From hello Ambari Web UI, select hello service you wish tooview logs for (for example, YARN).</span></span> <span data-ttu-id="925e0-234">Utilizzare quindi **collegamenti rapidi** tooselect quali hello tooview nodo head per il registro.</span><span class="sxs-lookup"><span data-stu-id="925e0-234">Then use **Quick Links** tooselect which head node tooview hello logs for.</span></span>

![Utilizzando rapida collega tooview log](./media/hdinsight-high-availability-linux/viewlogs.png)

## <a name="how-tooconfigure-hello-node-size"></a><span data-ttu-id="925e0-236">Come tooconfigure hello dimensione del nodo</span><span class="sxs-lookup"><span data-stu-id="925e0-236">How tooconfigure hello node size</span></span>

<span data-ttu-id="925e0-237">è possibile selezionare dimensioni Hello di un nodo solo durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="925e0-237">hello size of a node can only be selected during cluster creation.</span></span> <span data-ttu-id="925e0-238">È possibile trovare un elenco di hello diverse dimensioni di macchina virtuale disponibile per HDInsight su hello [pagina dei prezzi di HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="925e0-238">You can find a list of hello different VM sizes available for HDInsight on hello [HDInsight pricing page](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="925e0-239">Quando si crea un cluster, è possibile specificare dimensioni di hello dei nodi di hello.</span><span class="sxs-lookup"><span data-stu-id="925e0-239">When creating a cluster, you can specify hello size of hello nodes.</span></span> <span data-ttu-id="925e0-240">Hello informazioni riportate di seguito vengono fornite indicazioni sulla modalità toospecify hello dimensione tramite hello [portale di Azure][preview-portal], [Azure PowerShell][azure-powershell], hello e [CLI di Azure][azure-cli]:</span><span class="sxs-lookup"><span data-stu-id="925e0-240">hello following information provides guidance on how toospecify hello size using hello [Azure portal][preview-portal], [Azure PowerShell][azure-powershell], and hello [Azure CLI][azure-cli]:</span></span>

* <span data-ttu-id="925e0-241">**Portale di Azure**: durante la creazione di un cluster, è possibile impostare dimensioni hello dei nodi di hello usati dal cluster hello:</span><span class="sxs-lookup"><span data-stu-id="925e0-241">**Azure portal**: When creating a cluster, you can set hello size of hello nodes used by hello cluster:</span></span>

    ![Immagine della creazione guidata di cluster con la selezione delle dimensioni del nodo](./media/hdinsight-high-availability-linux/headnodesize.png)

* <span data-ttu-id="925e0-243">**CLI di Azure**: quando si utilizza hello `azure hdinsight cluster create` comando, è possibile impostare dimensioni hello head hello, lavoro e i nodi ZooKeeper utilizzando hello `--headNodeSize`, `--workerNodeSize`, e `--zookeeperNodeSize` parametri.</span><span class="sxs-lookup"><span data-stu-id="925e0-243">**Azure CLI**: When using hello `azure hdinsight cluster create` command, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `--headNodeSize`, `--workerNodeSize`, and `--zookeeperNodeSize` parameters.</span></span>

* <span data-ttu-id="925e0-244">**Azure PowerShell**: quando si utilizza hello `New-AzureRmHDInsightCluster` cmdlet, è possibile impostare dimensioni hello head hello, lavoro e i nodi ZooKeeper utilizzando hello `-HeadNodeVMSize`, `-WorkerNodeSize`, e `-ZookeeperNodeSize` parametri.</span><span class="sxs-lookup"><span data-stu-id="925e0-244">**Azure PowerShell**: When using hello `New-AzureRmHDInsightCluster` cmdlet, you can set hello size of hello head, worker, and ZooKeeper nodes by using hello `-HeadNodeVMSize`, `-WorkerNodeSize`, and `-ZookeeperNodeSize` parameters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="925e0-245">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="925e0-245">Next steps</span></span>

<span data-ttu-id="925e0-246">Utilizzare hello seguendo i collegamenti toolearn ulteriori informazioni sulle operazioni descritte in questo documento.</span><span class="sxs-lookup"><span data-stu-id="925e0-246">Use hello following links toolearn more about things mentioned in this document.</span></span>

* [<span data-ttu-id="925e0-247">Riferimento REST Ambari</span><span class="sxs-lookup"><span data-stu-id="925e0-247">Ambari REST Reference</span></span>](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md)
* [<span data-ttu-id="925e0-248">Installare e configurare hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="925e0-248">Install and configure hello Azure CLI</span></span>](../cli-install-nodejs.md)
* [<span data-ttu-id="925e0-249">Installare e configurare Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="925e0-249">Install and configure Azure PowerShell</span></span>](/powershell/azure/overview)
* [<span data-ttu-id="925e0-250">Gestire HDInsight tramite Ambari</span><span class="sxs-lookup"><span data-stu-id="925e0-250">Manage HDInsight using Ambari</span></span>](hdinsight-hadoop-manage-ambari.md)
* [<span data-ttu-id="925e0-251">provisioning di cluster HDInsight basati su Linux</span><span class="sxs-lookup"><span data-stu-id="925e0-251">Provision Linux-based HDInsight clusters</span></span>](hdinsight-hadoop-provision-linux-clusters.md)

[preview-portal]: https://portal.azure.com/
[azure-powershell]: /powershell/azureps-cmdlets-docs
[azure-cli]: ../cli-install-nodejs.md
