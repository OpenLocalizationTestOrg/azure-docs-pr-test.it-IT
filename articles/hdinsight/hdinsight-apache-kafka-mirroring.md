---
title: argomenti di Apache Kafka aaaMirror - HDInsight di Azure | Documenti Microsoft
description: "Informazioni su come mirroring toouse Apache Kafka funzionalità toomaintain una replica di un Kafka nel cluster HDInsight dal mirroring del cluster secondario tooa di argomenti."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 015d276e-f678-4f2b-9572-75553c56625b
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/13/2017
ms.author: larryfr
ms.openlocfilehash: 5ace0251d7402d4d7d9b28726e253ce7091a87ef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-mirrormaker-tooreplicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="0f7e6-103">Utilizzare gli argomenti di Apache Kafka tooreplicate MirrorMaker con Kafka in HDInsight (anteprima)</span><span class="sxs-lookup"><span data-stu-id="0f7e6-103">Use MirrorMaker tooreplicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="0f7e6-104">Informazioni su come toouse Kafka Apache del mirroring del cluster secondario tooa funzionalità tooreplicate argomenti.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-104">Learn how toouse Apache Kafka's mirroring feature tooreplicate topics tooa secondary cluster.</span></span> <span data-ttu-id="0f7e6-105">Il mirroring può essere eseguito come un processo continuo o utilizzato in modo intermittente come metodo di migrazione dei dati da un cluster tooanother.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster tooanother.</span></span>

<span data-ttu-id="0f7e6-106">In questo esempio, il mirroring è tooreplicate utilizzati argomenti tra due cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-106">In this example, mirroring is used tooreplicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="0f7e6-107">Entrambi i cluster sono in una rete virtuale di Azure in hello stessa area.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-107">Both clusters are in an Azure Virtual Network in hello same region.</span></span>

> [!WARNING]
> <span data-ttu-id="0f7e6-108">Il mirroring non deve essere considerato come una tolleranza di errore indica tooachieve.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-108">Mirroring should not be considered as a means tooachieve fault-tolerance.</span></span> <span data-ttu-id="0f7e6-109">Hello tooitems offset all'interno di un argomento sono le differenze tra i cluster di origine e destinazione hello, pertanto i client non è possibile utilizzare hello due in modo intercambiabile.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-109">hello offset tooitems within a topic are different between hello source and destination clusters, so clients cannot use hello two interchangeably.</span></span>
>
> <span data-ttu-id="0f7e6-110">Se si teme la tolleranza di errore, è necessario impostare la replica per argomenti hello all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-110">If you are concerned about fault tolerance, you should set replication for hello topics within your cluster.</span></span> <span data-ttu-id="0f7e6-111">Per altre informazioni, vedere [Introduzione a Kafka in HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0f7e6-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="0f7e6-112">Funzionamento del mirroring di Kafka</span><span class="sxs-lookup"><span data-stu-id="0f7e6-112">How Kafka mirroring works</span></span>

<span data-ttu-id="0f7e6-113">Funzionamento del mirroring utilizzando hello MirrorMaker strumento (parte di Apache Kafka) tooconsume registra dagli argomenti su cluster di origine hello e quindi crea una copia locale nel cluster di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-113">Mirroring works by using hello MirrorMaker tool (part of Apache Kafka) tooconsume records from topics on hello source cluster and then create a local copy on hello destination cluster.</span></span> <span data-ttu-id="0f7e6-114">MirrorMaker utilizza (almeno) *consumer* che letti dal cluster di origine, hello e una *producer* che scrive cluster locale (destinazione) toohello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-114">MirrorMaker uses one (or more) *consumers* that read from hello source cluster, and a *producer* that writes toohello local (destination) cluster.</span></span>

<span data-ttu-id="0f7e6-115">Hello seguente diagramma illustra il processo di Mirroring hello:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-115">hello following diagram illustrates hello Mirroring process:</span></span>

![Diagramma del processo di mirroring hello](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="0f7e6-117">Apache Kafka in HDInsight non forniscono accesso toohello servizio Kafka hello rete internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-117">Apache Kafka on HDInsight does not provide access toohello Kafka service over hello public internet.</span></span> <span data-ttu-id="0f7e6-118">Produttori di Kafka o i consumer devono trovarsi nella hello stessa rete virtuale come nodi cluster Kafka hello hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-118">Kafka producers or consumers must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="0f7e6-119">In questo esempio hello origine Kafka sia quelli di destinazione si trovano in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-119">For this example, both hello Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="0f7e6-120">Hello diagramma seguente illustra il flusso delle comunicazioni tra i cluster hello:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-120">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagramma dei cluster Kafka di origine e destinazione in una rete virtuale di Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="0f7e6-122">cluster di origine e destinazione Hello può essere diverso in numero hello dei nodi e delle partizioni e offset all'interno degli argomenti hello sono diversi.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-122">hello source and destination clusters can be different in hello number of nodes and partitions, and offsets within hello topics are different also.</span></span> <span data-ttu-id="0f7e6-123">Il mirroring gestisce valore hello chiave utilizzato per il partizionamento, in modo viene mantenuto l'ordine di record in una base per ogni chiave.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-123">Mirroring maintains hello key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="0f7e6-124">Mirroring tra i limiti di rete</span><span class="sxs-lookup"><span data-stu-id="0f7e6-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="0f7e6-125">Se è necessario toomirror tra cluster Kafka in reti diverse, esistono hello considerazioni aggiuntive seguenti:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-125">If you need toomirror between Kafka clusters in different networks, there are hello following additional considerations:</span></span>

* <span data-ttu-id="0f7e6-126">**Gateway**: reti hello devono essere in grado di toocommunicate in hello livello TCPIP.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-126">**Gateways**: hello networks must be able toocommunicate at hello TCPIP level.</span></span>

* <span data-ttu-id="0f7e6-127">**Risoluzione dei nomi**: hello Kafka cluster in ogni rete deve essere in grado di tooconnect tooeach altri usando i nomi host.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-127">**Name resolution**: hello Kafka clusters in each network must be able tooconnect tooeach other by using hostnames.</span></span> <span data-ttu-id="0f7e6-128">Tale operazione potrebbe richiedere un server di sistema DNS (Domain Name) in ogni rete che viene configurato tooforward richieste toohello altre reti.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-128">This may require a Domain Name System (DNS) server in each network that is configured tooforward requests toohello other networks.</span></span>

    <span data-ttu-id="0f7e6-129">Quando si crea una rete virtuale di Azure, anziché utilizzare hello che automatica DNS fornito con la rete hello, è necessario specificare un personalizzato DNS server hello indirizzo IP e per server hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-129">When creating an Azure Virtual Network, instead of using hello automatic DNS provided with hello network, you must specify a custom DNS server and hello IP address for hello server.</span></span> <span data-ttu-id="0f7e6-130">Dopo aver hello che rete virtuale è stata creata, è necessario quindi creare una macchina virtuale di Azure che utilizza tale indirizzo IP, quindi installare e configurare software DNS su di esso.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-130">After hello Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0f7e6-131">Creare e configurare un server DNS personalizzato hello prima di installare HDInsight in hello rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-131">Create and configure hello custom DNS server before installing HDInsight into hello Virtual Network.</span></span> <span data-ttu-id="0f7e6-132">Non sussiste alcuna configurazione aggiuntiva necessaria per il server DNS di HDInsight toouse hello configurato per la rete virtuale hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-132">There is no additional configuration required for HDInsight toouse hello DNS server configured for hello Virtual Network.</span></span>

<span data-ttu-id="0f7e6-133">Per altre informazioni sulla connessione di due reti virtuali di Azure, vedere [Configurare una connessione da rete virtuale a rete virtuale](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="0f7e6-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="0f7e6-134">Creare cluster Kafka</span><span class="sxs-lookup"><span data-stu-id="0f7e6-134">Create Kafka clusters</span></span>

<span data-ttu-id="0f7e6-135">È possibile creare una rete virtuale di Azure e Kafka cluster manualmente, ma è più facile toouse un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="0f7e6-136">Utilizzare hello seguendo i passaggi toodeploy una rete virtuale di Azure e due Kafka cluster tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-136">Use hello following steps toodeploy an Azure virtual network and two Kafka clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="0f7e6-137">Utilizzare hello seguente pulsante toosign in tooAzure e modello hello Apri nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-137">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="0f7e6-138">Hello Azure Resource Manager modello si trova in **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-138">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="0f7e6-139">disponibilità tooguarantee Kafka in HDInsight, il cluster deve contenere almeno tre nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="0f7e6-140">Questo modello crea un cluster Kafka contenente tre nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="0f7e6-141">Hello utilizzare seguendo le voci di informazioni toopopulate hello hello **distribuzione personalizzata** pannello:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-141">Use hello following information toopopulate hello entries on hello **Custom deployment** blade:</span></span>
    
    ![Distribuzione personalizzata di HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="0f7e6-143">**Gruppo di risorse**: creare un gruppo o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="0f7e6-144">Questo gruppo contiene cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-144">This group contains hello HDInsight cluster.</span></span>

    * <span data-ttu-id="0f7e6-145">**Percorso**: selezionare un tooyou geograficamente Chiudi percorso.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-145">**Location**: Select a location geographically close tooyou.</span></span>
     
    * <span data-ttu-id="0f7e6-146">**Nome del Cluster di base**: questo valore viene utilizzato come nome base hello hello Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-146">**Base Cluster Name**: This value is used as hello base name for hello Kafka clusters.</span></span> <span data-ttu-id="0f7e6-147">Se ad esempio si immette **hdi** verranno creati cluster denominati **source-hdi** e **dest-hdi**.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="0f7e6-148">**Nome utente di accesso del cluster**: nome utente amministratore di hello per hello origine e destinazione Kafka cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-148">**Cluster Login User Name**: hello admin user name for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="0f7e6-149">**Password di account di accesso cluster**: cluster Kafka password dell'utente admin hello per hello origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-149">**Cluster Login Password**: hello admin user password for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="0f7e6-150">**Nome utente SSH**: cluster Kafka hello SSH utente toocreate per hello origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-150">**SSH User Name**: hello SSH user toocreate for hello source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="0f7e6-151">**Password SSH**: cluster Kafka password hello per utente SSH hello hello origine e di destinazione.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-151">**SSH Password**: hello password for hello SSH user for hello source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="0f7e6-152">Hello lettura **termini e condizioni**, quindi selezionare **accetto le condizioni indicate in precedenza toohello**.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-152">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="0f7e6-153">Infine, controllare **Pin toodashboard** e quindi selezionare **acquisto**.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-153">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="0f7e6-154">Sono necessari circa 20 minuti toocreate cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-154">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="0f7e6-155">Dopo avere create le risorse di hello, verrà reindirizzato tooa pannello per gruppo di risorse hello che contiene i cluster hello e dashboard web.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-155">Once hello resources have been created, you are redirected tooa blade for hello resource group that contains hello clusters and web dashboard.</span></span>

![Pannello di gruppo di risorse per la rete virtuale hello e cluster](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="0f7e6-157">Si noti che sono nomi hello dei cluster HDInsight hello **origine BASENAME** e **dest BASENAME**, dove BASENAME è nome hello toohello modello specificato.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-157">Notice that hello names of hello HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="0f7e6-158">Utilizzare questi nomi nei passaggi successivi per la connessione toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-158">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="0f7e6-159">Creare argomenti</span><span class="sxs-lookup"><span data-stu-id="0f7e6-159">Create topics</span></span>

1. <span data-ttu-id="0f7e6-160">Connettersi toohello **origine** cluster tramite SSH:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-160">Connect toohello **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="0f7e6-161">Sostituire **sshuser** con nome dell'utente SSH hello utilizzato durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-161">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="0f7e6-162">Sostituire **BASENAME** con il nome di base hello utilizzato durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-162">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="0f7e6-163">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0f7e6-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0f7e6-164">Seguente hello utilizzare comandi toofind hello Zookeeper host del cluster di origine hello:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-164">Use hello following commands toofind hello Zookeeper hosts for hello source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get hello zookeeper hosts for hello source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with hello password for hello cluster.

    Replace `$CLUSTERNAME` with hello name of hello source cluster.

3. toocreate a topic named `testtopic`, use hello following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="0f7e6-165">È stato creato hello utilizzare tooverify comando che hello argomento seguente:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-165">Use hello following command tooverify that hello topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="0f7e6-166">risposta Hello contiene `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-166">hello response contains `testtopic`.</span></span>

4. <span data-ttu-id="0f7e6-167">Hello di utilizzare le seguenti informazioni di tooview hello Zookeeper host per questo (hello **origine**) cluster:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-167">Use hello following tooview hello Zookeeper host information for this (hello **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="0f7e6-168">Restituisce toohello di informazioni simili seguente testo:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-168">This returns information similar toohello following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="0f7e6-169">Salvare queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-169">Save this information.</span></span> <span data-ttu-id="0f7e6-170">Viene usato nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-170">It is used in hello next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="0f7e6-171">Configurare il mirroring</span><span class="sxs-lookup"><span data-stu-id="0f7e6-171">Configure mirroring</span></span>

1. <span data-ttu-id="0f7e6-172">Connettersi toohello **destinazione** utilizzando una sessione SSH diversa del cluster:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-172">Connect toohello **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="0f7e6-173">Sostituire **sshuser** con nome dell'utente SSH hello utilizzato durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-173">Replace **sshuser** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="0f7e6-174">Sostituire **BASENAME** con il nome di base hello utilizzato durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-174">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

    <span data-ttu-id="0f7e6-175">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="0f7e6-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="0f7e6-176">Comando che segue di hello utilizzare toocreate un `consumer.properties` file che descrive come toocommunicate con hello **origine** cluster:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-176">Use hello following command toocreate a `consumer.properties` file that describes how toocommunicate with hello **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="0f7e6-177">Hello utilizzo successivo di testo come contenuto di hello di hello `consumer.properties` file:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-177">Use hello following text as hello contents of hello `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="0f7e6-178">Sostituire **SOURCE_ZKHOSTS** con hello Zookeeper ospita informazioni da hello **origine** cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-178">Replace **SOURCE_ZKHOSTS** with hello Zookeeper hosts information from hello **source** cluster.</span></span>

    <span data-ttu-id="0f7e6-179">Questo file descrive hello consumer informazioni toouse durante la lettura dall'origine hello cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-179">This file describes hello consumer information toouse when reading from hello source Kafka cluster.</span></span> <span data-ttu-id="0f7e6-180">Per altre informazioni sulla configurazione dei consumer, vedere [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) (Configurazione di consumer) in kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="0f7e6-181">file hello toosave, usare **Ctrl + X**, **Y**e quindi **invio**.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-181">toosave hello file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="0f7e6-182">Prima di configurare producer hello che comunica con i cluster di destinazione hello, deve trovare broker hello host per hello **destinazione** cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-182">Before configuring hello producer that communicates with hello destination cluster, you must find hello broker hosts for hello **destination** cluster.</span></span> <span data-ttu-id="0f7e6-183">Utilizzare queste informazioni di hello tooretrieve i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-183">Use hello following commands tooretrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="0f7e6-184">Sostituire `$PASSWORD` con password di account (amministratore) hello account di accesso per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-184">Replace `$PASSWORD` with hello login account (admin) password for hello cluster.</span></span>

    <span data-ttu-id="0f7e6-185">Sostituire `$CLUSTERNAME` con nome hello del cluster di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-185">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="0f7e6-186">Questi comandi restituiscono informazioni simili che seguono di toohello:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-186">These commands return information similar toohello following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="0f7e6-187">Hello utilizzare seguente toocreate un `producer.properties` file che descrive come toocommunicate con hello **destinazione** cluster:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-187">Use hello following toocreate a `producer.properties` file that describes how toocommunicate with hello **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="0f7e6-188">Hello utilizzo successivo di testo come contenuto di hello di hello `producer.properties` file:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-188">Use hello following text as hello contents of hello `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="0f7e6-189">Sostituire **DEST_BROKERS** con informazioni di Service broker hello del passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-189">Replace **DEST_BROKERS** with hello broker information from hello previous step.</span></span>

    <span data-ttu-id="0f7e6-190">Per altre informazioni sulla configurazione dei producer, vedere [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) (Configurazione di producer) in kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="0f7e6-191">Avviare MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="0f7e6-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="0f7e6-192">Da hello SSH connessione toohello **destinazione** cluster, utilizzare hello comando toostart hello MirrorMaker processo:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-192">From hello SSH connection toohello **destination** cluster, use hello following command toostart hello MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="0f7e6-193">Hello parametri in questo esempio vengono utilizzati:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-193">hello parameters used in this example are:</span></span>

    * <span data-ttu-id="0f7e6-194">**-consumer.config**: Specifica il file hello che contiene le proprietà di consumer.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-194">**--consumer.config**: Specifies hello file that contains consumer properties.</span></span> <span data-ttu-id="0f7e6-195">Queste proprietà sono utilizzate toocreate un consumer che legge da hello *origine* cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-195">These properties are used toocreate a consumer that reads from hello *source* Kafka cluster.</span></span>

    * <span data-ttu-id="0f7e6-196">**-producer.config**: Specifica il file hello che contiene le proprietà di producer.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-196">**--producer.config**: Specifies hello file that contains producer properties.</span></span> <span data-ttu-id="0f7e6-197">Queste proprietà sono utilizzate toocreate un produttore che scrive toohello *destinazione* cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-197">These properties are used toocreate a producer that writes toohello *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="0f7e6-198">**-whitelist**: un elenco di argomenti che vengono replicate MirrorMaker hello origine cluster toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-198">**--whitelist**: A list of topics that MirrorMaker replicates from hello source cluster toohello destination.</span></span>

    * <span data-ttu-id="0f7e6-199">**-num.streams**: hello svariate toocreate thread consumer.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-199">**--num.streams**: hello number of consumer threads toocreate.</span></span>

 <span data-ttu-id="0f7e6-200">All'avvio, MirrorMaker restituisce toohello di informazioni simili seguente testo:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-200">On startup, MirrorMaker returns information similar toohello following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="0f7e6-201">Da hello SSH connessione toohello **origine** cluster, utilizzare hello successivo comando toostart un produttore di inviare l'argomento toohello messaggi:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-201">From hello SSH connection toohello **source** cluster, use hello following command toostart a producer and send messages toohello topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="0f7e6-202">Sostituire `$PASSWORD` con password di accesso (amministrazione) hello per cluster di origine hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-202">Replace `$PASSWORD` with hello login (admin) password for hello source cluster.</span></span>

    <span data-ttu-id="0f7e6-203">Sostituire `$CLUSTERNAME` con nome hello del cluster di origine di hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-203">Replace `$CLUSTERNAME` with hello name of hello source cluster.</span></span>

     <span data-ttu-id="0f7e6-204">Quando si arriva a una riga vuota con un cursore, digitare alcuni messaggi di testo.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="0f7e6-205">Questi vengono inviati toohello argomento sul hello **origine** cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-205">These are sent toohello topic on hello **source** cluster.</span></span> <span data-ttu-id="0f7e6-206">Al termine, utilizzare **Ctrl + C** processo producer di hello tooend.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-206">When done, use **Ctrl + C** tooend hello producer process.</span></span>

3. <span data-ttu-id="0f7e6-207">Da hello SSH connessione toohello **destinazione** cluster, utilizzare **Ctrl + C** hello tooend MirrorMaker processo.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-207">From hello SSH connection toohello **destination** cluster, use **Ctrl + C** tooend hello MirrorMaker process.</span></span> <span data-ttu-id="0f7e6-208">Quindi seguito hello utilizzare i comandi che hello tooverify `testtopic` argomento è stato creato, e i dati di argomento hello è stata replicata toothis mirror:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-208">Then use hello following commands tooverify that hello `testtopic` topic was created, and that data in hello topic was replicated toothis mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="0f7e6-209">Sostituire `$PASSWORD` con password di accesso (amministrazione) hello per cluster di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-209">Replace `$PASSWORD` with hello login (admin) password for hello destination cluster.</span></span>

    <span data-ttu-id="0f7e6-210">Sostituire `$CLUSTERNAME` con nome hello del cluster di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-210">Replace `$CLUSTERNAME` with hello name of hello destination cluster.</span></span>

    <span data-ttu-id="0f7e6-211">Hello elenco di argomenti include ora `testtopic`, che viene creato quando MirrorMaster rispecchia argomento hello hello origine cluster toohello destinazione.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-211">hello list of topics now includes `testtopic`, which is created when MirrorMaster mirrors hello topic from hello source cluster toohello destination.</span></span> <span data-ttu-id="0f7e6-212">messaggi Hello recuperati dall'argomento hello sono hello identico a quello immesso nel cluster di origine hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-212">hello messages retrieved from hello topic are hello same as entered on hello source cluster.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="0f7e6-213">Eliminare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="0f7e6-213">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="0f7e6-214">Poiché i passaggi di hello in questo documento crea entrambi i cluster in hello nello stesso gruppo di risorse di Azure, è possibile eliminare il gruppo di risorse hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-214">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="0f7e6-215">Eliminazione gruppo di risorse hello rimuove tutte le risorse create eseguendo questo documento, hello rete virtuale di Azure e l'account di archiviazione utilizzato dal cluster hello.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-215">Deleting hello resource group removes all resources created by following this document, hello Azure Virtual Network, and storage account used by hello clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f7e6-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0f7e6-216">Next Steps</span></span>

<span data-ttu-id="0f7e6-217">In questo documento è stato descritto come toouse MirrorMaker toocreate una replica di un Kafka del cluster.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-217">In this document, you learned how toouse MirrorMaker toocreate a replica of a Kafka cluster.</span></span> <span data-ttu-id="0f7e6-218">Utilizzare hello seguendo i collegamenti toodiscover toowork altri modi con Kafka:</span><span class="sxs-lookup"><span data-stu-id="0f7e6-218">Use hello following links toodiscover other ways toowork with Kafka:</span></span>

* <span data-ttu-id="0f7e6-219">[Documentazione su Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) in cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="0f7e6-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="0f7e6-220">Introduzione ad Apache Kafka (anteprima) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f7e6-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* <span data-ttu-id="0f7e6-221">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Usare Apache Spark con Kafka in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="0f7e6-221">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>
* [<span data-ttu-id="0f7e6-222">Usare Apache Storm (anteprima) con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="0f7e6-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* [<span data-ttu-id="0f7e6-223">Connettersi tooKafka tramite una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="0f7e6-223">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
