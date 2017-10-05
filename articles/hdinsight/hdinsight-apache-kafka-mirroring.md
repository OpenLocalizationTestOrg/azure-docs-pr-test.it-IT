---
title: 'Eseguire il mirroring degli argomenti di Apache Kafka: Azure HDInsight| Microsoft Docs'
description: "Informazioni su come usare la funzionalità di mirroring di Apache Kafka per gestire una replica di un cluster Kafka in HDInsight eseguendo il mirroring degli argomenti in un cluster secondario."
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
ms.openlocfilehash: e418cb01e1a9168e3662e8d6242903e052b6047b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-mirrormaker-to-replicate-apache-kafka-topics-with-kafka-on-hdinsight-preview"></a><span data-ttu-id="4f821-103">Usare MirrorMaker per replicare gli argomenti di Apache Kafka con Kafka in HDInsight (anteprima)</span><span class="sxs-lookup"><span data-stu-id="4f821-103">Use MirrorMaker to replicate Apache Kafka topics with Kafka on HDInsight (preview)</span></span>

<span data-ttu-id="4f821-104">Informazioni su come usare la funzionalità di mirroring di Apache Kafka per replicare gli argomenti in un cluster secondario.</span><span class="sxs-lookup"><span data-stu-id="4f821-104">Learn how to use Apache Kafka's mirroring feature to replicate topics to a secondary cluster.</span></span> <span data-ttu-id="4f821-105">Il mirroring può essere eseguito come processo continuo o usato in modo intermittente come metodo di migrazione dei dati da un cluster all'altro.</span><span class="sxs-lookup"><span data-stu-id="4f821-105">Mirroring can be ran as a continuous process, or used intermittently as a method of migrating data from one cluster to another.</span></span>

<span data-ttu-id="4f821-106">In questo esempio il mirroring viene usato per replicare argomenti tra due cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f821-106">In this example, mirroring is used to replicate topics between two HDInsight clusters.</span></span> <span data-ttu-id="4f821-107">Entrambi i cluster si trovano in una rete virtuale di Azure nella stessa area.</span><span class="sxs-lookup"><span data-stu-id="4f821-107">Both clusters are in an Azure Virtual Network in the same region.</span></span>

> [!WARNING]
> <span data-ttu-id="4f821-108">Il mirroring non deve essere considerato un mezzo per ottenere la tolleranza di errore.</span><span class="sxs-lookup"><span data-stu-id="4f821-108">Mirroring should not be considered as a means to achieve fault-tolerance.</span></span> <span data-ttu-id="4f821-109">Gli offset per gli elementi all'interno di un argomento sono diversi nei cluster di origine e di destinazione, quindi i client non possono usarli in modo intercambiabile.</span><span class="sxs-lookup"><span data-stu-id="4f821-109">The offset to items within a topic are different between the source and destination clusters, so clients cannot use the two interchangeably.</span></span>
>
> <span data-ttu-id="4f821-110">Per preservare la tolleranza di errore è necessario impostare la replica per gli argomenti all'interno del cluster.</span><span class="sxs-lookup"><span data-stu-id="4f821-110">If you are concerned about fault tolerance, you should set replication for the topics within your cluster.</span></span> <span data-ttu-id="4f821-111">Per altre informazioni, vedere [Introduzione a Kafka in HDInsight](hdinsight-apache-kafka-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="4f821-111">For more information, see [Get started with Kafka on HDInsight](hdinsight-apache-kafka-get-started.md).</span></span>

## <a name="how-kafka-mirroring-works"></a><span data-ttu-id="4f821-112">Funzionamento del mirroring di Kafka</span><span class="sxs-lookup"><span data-stu-id="4f821-112">How Kafka mirroring works</span></span>

<span data-ttu-id="4f821-113">Il mirroring usa lo strumento MirrorMaker (componente di Apache Kafka) per utilizzare i record degli argomenti nel cluster di origine e creare una copia locale nel cluster di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4f821-113">Mirroring works by using the MirrorMaker tool (part of Apache Kafka) to consume records from topics on the source cluster and then create a local copy on the destination cluster.</span></span> <span data-ttu-id="4f821-114">MirrorMaker usa uno o più *consumer* che leggono dal cluster di origine e un *producer* che scrive nel cluster locale (destinazione).</span><span class="sxs-lookup"><span data-stu-id="4f821-114">MirrorMaker uses one (or more) *consumers* that read from the source cluster, and a *producer* that writes to the local (destination) cluster.</span></span>

<span data-ttu-id="4f821-115">Il diagramma seguente illustra il processo di mirroring:</span><span class="sxs-lookup"><span data-stu-id="4f821-115">The following diagram illustrates the Mirroring process:</span></span>

![Diagramma del processo di mirroring](./media/hdinsight-apache-kafka-mirroring/kafka-mirroring.png)

<span data-ttu-id="4f821-117">Apache Kafka in HDInsight non fornisce l'accesso al servizio Kafka tramite Internet pubblico.</span><span class="sxs-lookup"><span data-stu-id="4f821-117">Apache Kafka on HDInsight does not provide access to the Kafka service over the public internet.</span></span> <span data-ttu-id="4f821-118">I producer o i consumer di Kafka devono trovarsi nella stessa rete virtuale di Azure in cui sono presenti i nodi del cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="4f821-118">Kafka producers or consumers must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="4f821-119">Per questo esempio, i cluster Kafka di origine e destinazione si trovano entrambi in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4f821-119">For this example, both the Kafka source and destination clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="4f821-120">Il diagramma seguente illustra il flusso delle comunicazioni tra i cluster:</span><span class="sxs-lookup"><span data-stu-id="4f821-120">The following diagram shows how communication flows between the clusters:</span></span>

![Diagramma dei cluster Kafka di origine e destinazione in una rete virtuale di Azure](./media/hdinsight-apache-kafka-mirroring/spark-kafka-vnet.png)

<span data-ttu-id="4f821-122">I cluster di origine e destinazione possono differire per numero di nodi e partizioni. Anche gli offset negli argomenti differiscono.</span><span class="sxs-lookup"><span data-stu-id="4f821-122">The source and destination clusters can be different in the number of nodes and partitions, and offsets within the topics are different also.</span></span> <span data-ttu-id="4f821-123">Il mirroring mantiene il valore della chiave usato per il partizionamento, quindi l'ordine dei record viene conservato in base alla chiave.</span><span class="sxs-lookup"><span data-stu-id="4f821-123">Mirroring maintains the key value that is used for partitioning, so record order is preserved on a per-key basis.</span></span>

### <a name="mirroring-across-network-boundaries"></a><span data-ttu-id="4f821-124">Mirroring tra i limiti di rete</span><span class="sxs-lookup"><span data-stu-id="4f821-124">Mirroring across network boundaries</span></span>

<span data-ttu-id="4f821-125">Se è necessario eseguire il mirroring di cluster Kafka in reti diverse, si notino le seguenti considerazioni aggiuntive:</span><span class="sxs-lookup"><span data-stu-id="4f821-125">If you need to mirror between Kafka clusters in different networks, there are the following additional considerations:</span></span>

* <span data-ttu-id="4f821-126">**Gateway**: le reti devono poter comunicare a livello di TCP/IP.</span><span class="sxs-lookup"><span data-stu-id="4f821-126">**Gateways**: The networks must be able to communicate at the TCPIP level.</span></span>

* <span data-ttu-id="4f821-127">**Risoluzione dei nomi**: i cluster Kafka in ogni rete devono potersi connettere tra loro usando nomi host.</span><span class="sxs-lookup"><span data-stu-id="4f821-127">**Name resolution**: The Kafka clusters in each network must be able to connect to each other by using hostnames.</span></span> <span data-ttu-id="4f821-128">Potrebbe essere necessario un server DNS (Domain Name System) in ogni rete configurato per l'inoltro delle richieste ad altre reti.</span><span class="sxs-lookup"><span data-stu-id="4f821-128">This may require a Domain Name System (DNS) server in each network that is configured to forward requests to the other networks.</span></span>

    <span data-ttu-id="4f821-129">Quando si crea una rete virtuale di Azure, invece di usare il DNS automatico fornito con la rete è necessario specificare un server DNS personalizzato con il relativo indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="4f821-129">When creating an Azure Virtual Network, instead of using the automatic DNS provided with the network, you must specify a custom DNS server and the IP address for the server.</span></span> <span data-ttu-id="4f821-130">Dopo aver creato la rete virtuale è necessario creare una macchina virtuale di Azure che usi quell'indirizzo IP, quindi installare e configurare il software DNS sulla macchina stessa.</span><span class="sxs-lookup"><span data-stu-id="4f821-130">After the Virtual Network has been created, you must then create an Azure Virtual Machine that uses that IP address, then install and configure DNS software on it.</span></span>

    > [!WARNING]
    > <span data-ttu-id="4f821-131">Creare e configurare il server DNS personalizzato prima di installare HDInsight nella rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f821-131">Create and configure the custom DNS server before installing HDInsight into the Virtual Network.</span></span> <span data-ttu-id="4f821-132">Non sono necessarie altre operazioni di configurazione per far sì che HDInsight usi il server DNS configurato per la rete virtuale.</span><span class="sxs-lookup"><span data-stu-id="4f821-132">There is no additional configuration required for HDInsight to use the DNS server configured for the Virtual Network.</span></span>

<span data-ttu-id="4f821-133">Per altre informazioni sulla connessione di due reti virtuali di Azure, vedere [Configurare una connessione da rete virtuale a rete virtuale](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span><span class="sxs-lookup"><span data-stu-id="4f821-133">For more information on connecting two Azure Virtual Networks, see [Configure a VNet-to-VNet connection](../vpn-gateway/vpn-gateway-vnet-vnet-rm-ps.md).</span></span>

## <a name="create-kafka-clusters"></a><span data-ttu-id="4f821-134">Creare cluster Kafka</span><span class="sxs-lookup"><span data-stu-id="4f821-134">Create Kafka clusters</span></span>

<span data-ttu-id="4f821-135">Anche se è possibile creare manualmente cluster Kafka e una rete virtuale di Azure, è più semplice usare un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4f821-135">While you can create an Azure virtual network and Kafka clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="4f821-136">Seguire questa procedura per distribuire una rete virtuale di Azure e due cluster Kafka e nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="4f821-136">Use the following steps to deploy an Azure virtual network and two Kafka clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="4f821-137">Usare il pulsante seguente per accedere ad Azure e aprire il modello nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4f821-137">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json" target="_blank"><img src="./media/hdinsight-apache-kafka-mirroring/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="4f821-138">Il modello di Azure Resource Manager è disponibile su **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span><span class="sxs-lookup"><span data-stu-id="4f821-138">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-mirror-cluster-in-vnet-v2.1.json**.</span></span>

    > [!WARNING]
    > <span data-ttu-id="4f821-139">Per garantire la disponibilità di Kafka in HDInsight, il cluster deve contenere almeno tre nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4f821-139">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="4f821-140">Questo modello crea un cluster Kafka contenente tre nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="4f821-140">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="4f821-141">Usare le informazioni seguenti per popolare le voci nel pannello **Distribuzione personalizzata**:</span><span class="sxs-lookup"><span data-stu-id="4f821-141">Use the following information to populate the entries on the **Custom deployment** blade:</span></span>
    
    ![Distribuzione personalizzata di HDInsight](./media/hdinsight-apache-kafka-mirroring/parameters.png)
    
    * <span data-ttu-id="4f821-143">**Gruppo di risorse**: creare un gruppo o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="4f821-143">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="4f821-144">Questo gruppo contiene il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="4f821-144">This group contains the HDInsight cluster.</span></span>

    * <span data-ttu-id="4f821-145">**Località**: scegliere una località geograficamente vicina.</span><span class="sxs-lookup"><span data-stu-id="4f821-145">**Location**: Select a location geographically close to you.</span></span>
     
    * <span data-ttu-id="4f821-146">**Base Cluster Name** (Nome di base del cluster): questo valore viene usato come nome di base per i cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="4f821-146">**Base Cluster Name**: This value is used as the base name for the Kafka clusters.</span></span> <span data-ttu-id="4f821-147">Se ad esempio si immette **hdi** verranno creati cluster denominati **source-hdi** e **dest-hdi**.</span><span class="sxs-lookup"><span data-stu-id="4f821-147">For example, entering **hdi** creates clusters named **source-hdi** and **dest-hdi**.</span></span>

    * <span data-ttu-id="4f821-148">**Cluster Login User Name** (Nome utente di accesso del cluster): nome utente amministratore per i cluster Kafka di origine e destinazione.</span><span class="sxs-lookup"><span data-stu-id="4f821-148">**Cluster Login User Name**: The admin user name for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="4f821-149">**Cluster Login Password** (Password di accesso del cluster): password dell'utente amministratore per i cluster Kafka di origine e destinazione.</span><span class="sxs-lookup"><span data-stu-id="4f821-149">**Cluster Login Password**: The admin user password for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="4f821-150">**SSH User Name** (Nome utente SSH): utente SSH da creare per i cluster Kafka di origine e destinazione.</span><span class="sxs-lookup"><span data-stu-id="4f821-150">**SSH User Name**: The SSH user to create for the source and destination Kafka clusters.</span></span>

    * <span data-ttu-id="4f821-151">**SSH Password** (Password SSH): password dell'utente SSH per i cluster Kafka di origine e destinazione.</span><span class="sxs-lookup"><span data-stu-id="4f821-151">**SSH Password**: The password for the SSH user for the source and destination Kafka clusters.</span></span>

3. <span data-ttu-id="4f821-152">Leggere le **Condizioni** e quindi selezionare **Accetto le condizioni riportate sopra**.</span><span class="sxs-lookup"><span data-stu-id="4f821-152">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="4f821-153">Selezionare infine **Aggiungi al dashboard** e quindi **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="4f821-153">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="4f821-154">La creazione dei cluster richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="4f821-154">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="4f821-155">Dopo aver creato le risorse, si viene reindirizzati a un pannello del gruppo di risorse che contiene i cluster e il dashboard Web.</span><span class="sxs-lookup"><span data-stu-id="4f821-155">Once the resources have been created, you are redirected to a blade for the resource group that contains the clusters and web dashboard.</span></span>

![Pannello Gruppo di risorse per la rete virtuale e i cluster](./media/hdinsight-apache-kafka-mirroring/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="4f821-157">Si noti che i nomi dei cluster HDInsight sono **source-BASENAME** e **dest-BASENAME**, dove BASENAME è il nome specificato per il modello.</span><span class="sxs-lookup"><span data-stu-id="4f821-157">Notice that the names of the HDInsight clusters are **source-BASENAME** and **dest-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="4f821-158">Questi nomi verranno usati nei passaggi successivi per la connessione ai cluster.</span><span class="sxs-lookup"><span data-stu-id="4f821-158">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="create-topics"></a><span data-ttu-id="4f821-159">Creare argomenti</span><span class="sxs-lookup"><span data-stu-id="4f821-159">Create topics</span></span>

1. <span data-ttu-id="4f821-160">Connettersi al cluster di **origine** tramite SSH:</span><span class="sxs-lookup"><span data-stu-id="4f821-160">Connect to the **source** cluster using SSH:</span></span>

    ```bash
    ssh sshuser@source-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4f821-161">Sostituire **sshuser** con il nome utente SSH usato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="4f821-161">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="4f821-162">Sostituire **BASENAME** con il nome di base usato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="4f821-162">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="4f821-163">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4f821-163">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4f821-164">Usare i comandi seguenti per trovare gli host Zookeeper per il cluster di origine:</span><span class="sxs-lookup"><span data-stu-id="4f821-164">Use the following commands to find the Zookeeper hosts for the source cluster:</span></span>

    ```bash
    # Install jq if it is not installed
    sudo apt -y install jq
    # get the zookeeper hosts for the source cluster
    export SOURCE_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    
    Replace `$PASSWORD` with the password for the cluster.

    Replace `$CLUSTERNAME` with the name of the source cluster.

3. To create a topic named `testtopic`, use the following command:

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 2 --partitions 8 --topic testtopic --zookeeper $SOURCE_ZKHOSTS
    ```

3. <span data-ttu-id="4f821-165">Usare il comando seguente per verificare che l'argomento sia stato creato:</span><span class="sxs-lookup"><span data-stu-id="4f821-165">Use the following command to verify that the topic was created:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="4f821-166">La risposta contiene `testtopic`.</span><span class="sxs-lookup"><span data-stu-id="4f821-166">The response contains `testtopic`.</span></span>

4. <span data-ttu-id="4f821-167">Usare il comando seguente per visualizzare le informazioni degli host Zookeeper per questo cluster, ovvero il cluster di **origine**:</span><span class="sxs-lookup"><span data-stu-id="4f821-167">Use the following to view the Zookeeper host information for this (the **source**) cluster:</span></span>

    ```bash
    echo $SOURCE_ZKHOSTS
    ```

    <span data-ttu-id="4f821-168">Verranno restituite informazioni simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="4f821-168">This returns information similar to the following text:</span></span>

    `zk0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181,zk1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:2181`

    <span data-ttu-id="4f821-169">Salvare queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="4f821-169">Save this information.</span></span> <span data-ttu-id="4f821-170">Verranno usate nella sezione successiva.</span><span class="sxs-lookup"><span data-stu-id="4f821-170">It is used in the next section.</span></span>

## <a name="configure-mirroring"></a><span data-ttu-id="4f821-171">Configurare il mirroring</span><span class="sxs-lookup"><span data-stu-id="4f821-171">Configure mirroring</span></span>

1. <span data-ttu-id="4f821-172">Connettersi al cluster di **destinazione** con un'altra sessione SSH:</span><span class="sxs-lookup"><span data-stu-id="4f821-172">Connect to the **destination** cluster using a different SSH session:</span></span>

    ```bash
    ssh sshuser@dest-BASENAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="4f821-173">Sostituire **sshuser** con il nome utente SSH usato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="4f821-173">Replace **sshuser** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="4f821-174">Sostituire **BASENAME** con il nome di base usato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="4f821-174">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

    <span data-ttu-id="4f821-175">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="4f821-175">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="4f821-176">Usare il comando seguente per creare un file `consumer.properties` che descrive come comunicare con il cluster di **origine**:</span><span class="sxs-lookup"><span data-stu-id="4f821-176">Use the following command to create a `consumer.properties` file that describes how to communicate with the **source** cluster:</span></span>

    ```bash
    nano consumer.properties
    ```

    <span data-ttu-id="4f821-177">Usare il testo seguente come contenuto del file `consumer.properties`:</span><span class="sxs-lookup"><span data-stu-id="4f821-177">Use the following text as the contents of the `consumer.properties` file:</span></span>

    ```yaml
    zookeeper.connect=SOURCE_ZKHOSTS
    group.id=mirrorgroup
    ```

    <span data-ttu-id="4f821-178">Sostituire **SOURCE_ZKHOSTS** con le informazioni degli host Zookeeper presenti nel cluster di **origine**.</span><span class="sxs-lookup"><span data-stu-id="4f821-178">Replace **SOURCE_ZKHOSTS** with the Zookeeper hosts information from the **source** cluster.</span></span>

    <span data-ttu-id="4f821-179">Questo file descrive le informazioni sui consumer da usare durante la lettura dal cluster Kafka di origine.</span><span class="sxs-lookup"><span data-stu-id="4f821-179">This file describes the consumer information to use when reading from the source Kafka cluster.</span></span> <span data-ttu-id="4f821-180">Per altre informazioni sulla configurazione dei consumer, vedere [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) (Configurazione di consumer) in kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="4f821-180">For more information consumer configuration, see [Consumer Configs](https://kafka.apache.org/documentation#consumerconfigs) at kafka.apache.org.</span></span>

    <span data-ttu-id="4f821-181">Per salvare il file, usare **Ctrl + X**, **Y** e **INVIO**.</span><span class="sxs-lookup"><span data-stu-id="4f821-181">To save the file, use **Ctrl + X**, **Y**, and then **Enter**.</span></span>

3. <span data-ttu-id="4f821-182">Prima di configurare il producer che comunica con il cluster di destinazione è necessario trovare gli host broker per il cluster di **destinazione** stesso.</span><span class="sxs-lookup"><span data-stu-id="4f821-182">Before configuring the producer that communicates with the destination cluster, you must find the broker hosts for the **destination** cluster.</span></span> <span data-ttu-id="4f821-183">Usare i comandi seguenti per recuperare queste informazioni:</span><span class="sxs-lookup"><span data-stu-id="4f821-183">Use the following commands to retrieve this information:</span></span>

    ```bash
    sudo apt -y install jq
    DEST_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    echo $DEST_BROKERHOSTS
    ```

    <span data-ttu-id="4f821-184">Sostituire `$PASSWORD` con la password dell'account di accesso (amministratore) del cluster.</span><span class="sxs-lookup"><span data-stu-id="4f821-184">Replace `$PASSWORD` with the login account (admin) password for the cluster.</span></span>

    <span data-ttu-id="4f821-185">Sostituire `$CLUSTERNAME` con il nome del cluster di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4f821-185">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="4f821-186">Questi comandi restituiscono informazioni simili alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="4f821-186">These commands return information similar to the following:</span></span>

        wn0-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn1-dest.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092

4. <span data-ttu-id="4f821-187">Usare il comando seguente per creare un file `producer.properties` che descrive come comunicare con il cluster di **destinazione**:</span><span class="sxs-lookup"><span data-stu-id="4f821-187">Use the following to create a `producer.properties` file that describes how to communicate with the **destination** cluster:</span></span>

    ```bash
    nano producer.properties
    ```

    <span data-ttu-id="4f821-188">Usare il testo seguente come contenuto del file `producer.properties`:</span><span class="sxs-lookup"><span data-stu-id="4f821-188">Use the following text as the contents of the `producer.properties` file:</span></span>

    ```yaml
    bootstrap.servers=DEST_BROKERS
    compression.type=none
    ```

    <span data-ttu-id="4f821-189">Sostituire **DEST_BROKERS** con le informazioni del broker indicate nel passaggio precedente.</span><span class="sxs-lookup"><span data-stu-id="4f821-189">Replace **DEST_BROKERS** with the broker information from the previous step.</span></span>

    <span data-ttu-id="4f821-190">Per altre informazioni sulla configurazione dei producer, vedere [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) (Configurazione di producer) in kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="4f821-190">For more information producer configuration, see [Producer Configs](https://kafka.apache.org/documentation#producerconfigs) at kafka.apache.org.</span></span>

## <a name="start-mirrormaker"></a><span data-ttu-id="4f821-191">Avviare MirrorMaker</span><span class="sxs-lookup"><span data-stu-id="4f821-191">Start MirrorMaker</span></span>

1. <span data-ttu-id="4f821-192">Dalla connessione SSH al cluster di **destinazione** usare il comando seguente per avviare il processo MirrorMaker:</span><span class="sxs-lookup"><span data-stu-id="4f821-192">From the SSH connection to the **destination** cluster, use the following command to start the MirrorMaker process:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-run-class.sh kafka.tools.MirrorMaker --consumer.config consumer.properties --producer.config producer.properties --whitelist testtopic --num.streams 4
    ```

    <span data-ttu-id="4f821-193">I parametri usati in questo esempio sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="4f821-193">The parameters used in this example are:</span></span>

    * <span data-ttu-id="4f821-194">**--consumer.config**: specifica il file che contiene le proprietà del consumer.</span><span class="sxs-lookup"><span data-stu-id="4f821-194">**--consumer.config**: Specifies the file that contains consumer properties.</span></span> <span data-ttu-id="4f821-195">Queste proprietà vengono usate per creare un consumer che legge dal cluster Kafka di *origine*.</span><span class="sxs-lookup"><span data-stu-id="4f821-195">These properties are used to create a consumer that reads from the *source* Kafka cluster.</span></span>

    * <span data-ttu-id="4f821-196">**--producer.config**: specifica il file che contiene le proprietà del producer.</span><span class="sxs-lookup"><span data-stu-id="4f821-196">**--producer.config**: Specifies the file that contains producer properties.</span></span> <span data-ttu-id="4f821-197">Queste proprietà vengono usate per creare un producer che scrive nel cluster Kafka di *destinazione*.</span><span class="sxs-lookup"><span data-stu-id="4f821-197">These properties are used to create a producer that writes to the *destination* Kafka cluster.</span></span>

    * <span data-ttu-id="4f821-198">**--whitelist**: elenco di argomenti che vengono replicati da MirrorMaker dal cluster di origine alla destinazione.</span><span class="sxs-lookup"><span data-stu-id="4f821-198">**--whitelist**: A list of topics that MirrorMaker replicates from the source cluster to the destination.</span></span>

    * <span data-ttu-id="4f821-199">**--num.streams**: numero di thread consumer da creare.</span><span class="sxs-lookup"><span data-stu-id="4f821-199">**--num.streams**: The number of consumer threads to create.</span></span>

 <span data-ttu-id="4f821-200">All'avvio, MirrorMaker restituisce informazioni simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="4f821-200">On startup, MirrorMaker returns information similar to the following text:</span></span>

    ```json
    {metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-3, security.protocol=PLAINTEXT}{metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-0, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-kafka.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-2, security.protocol=PLAINTEXT}
    metadata.broker.list=wn1-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092,wn0-source.aazwc2onlofevkbof0cuixrp5h.gx.internal.cloudapp.net:9092, request.timeout.ms=30000, client.id=mirror-group-1, security.protocol=PLAINTEXT}
    ```

2. <span data-ttu-id="4f821-201">Dalla connessione SSH al cluster di **origine**, usare il comando seguente per avviare un producer e inviare messaggi all'argomento:</span><span class="sxs-lookup"><span data-stu-id="4f821-201">From the SSH connection to the **source** cluster, use the following command to start a producer and send messages to the topic:</span></span>

    ```bash
    SOURCE_BROKERHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $SOURCE_BROKERHOSTS --topic testtopic
    ```

    <span data-ttu-id="4f821-202">Sostituire `$PASSWORD` con la password dell'account di accesso (amministratore) del cluster di origine.</span><span class="sxs-lookup"><span data-stu-id="4f821-202">Replace `$PASSWORD` with the login (admin) password for the source cluster.</span></span>

    <span data-ttu-id="4f821-203">Sostituire `$CLUSTERNAME` con il nome del cluster di origine.</span><span class="sxs-lookup"><span data-stu-id="4f821-203">Replace `$CLUSTERNAME` with the name of the source cluster.</span></span>

     <span data-ttu-id="4f821-204">Quando si arriva a una riga vuota con un cursore, digitare alcuni messaggi di testo.</span><span class="sxs-lookup"><span data-stu-id="4f821-204">When you arrive at a blank line with a cursor, type in a few text messages.</span></span> <span data-ttu-id="4f821-205">Questi vengono inviati all'argomento nel cluster di **origine**.</span><span class="sxs-lookup"><span data-stu-id="4f821-205">These are sent to the topic on the **source** cluster.</span></span> <span data-ttu-id="4f821-206">Al termine, usare **Ctrl + C** per chiudere il processo del producer.</span><span class="sxs-lookup"><span data-stu-id="4f821-206">When done, use **Ctrl + C** to end the producer process.</span></span>

3. <span data-ttu-id="4f821-207">Dalla connessione SSH al cluster di **destinazione**, usare **Ctrl + C** per chiudere il processo MirrorMaker.</span><span class="sxs-lookup"><span data-stu-id="4f821-207">From the SSH connection to the **destination** cluster, use **Ctrl + C** to end the MirrorMaker process.</span></span> <span data-ttu-id="4f821-208">Usare quindi i comandi seguenti per verificare che l'argomento `testtopic` sia stato creato e che i dati nell'argomento siano stati replicati al mirror:</span><span class="sxs-lookup"><span data-stu-id="4f821-208">Then use the following commands to verify that the `testtopic` topic was created, and that data in the topic was replicated to this mirror:</span></span>

    ```bash
    DEST_ZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $DEST_ZKHOSTS
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $DEST_ZKHOSTS --topic testtopic --from-beginning
    ```

    <span data-ttu-id="4f821-209">Sostituire `$PASSWORD` con la password dell'account di accesso (amministratore) del cluster di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4f821-209">Replace `$PASSWORD` with the login (admin) password for the destination cluster.</span></span>

    <span data-ttu-id="4f821-210">Sostituire `$CLUSTERNAME` con il nome del cluster di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4f821-210">Replace `$CLUSTERNAME` with the name of the destination cluster.</span></span>

    <span data-ttu-id="4f821-211">L'elenco degli argomenti include ora `testtopic`, che viene creato quando MirrorMaster esegue il mirroring dell'argomento dal cluster di origine a quello di destinazione.</span><span class="sxs-lookup"><span data-stu-id="4f821-211">The list of topics now includes `testtopic`, which is created when MirrorMaster mirrors the topic from the source cluster to the destination.</span></span> <span data-ttu-id="4f821-212">I messaggi recuperati dall'argomento sono gli stessi immessi nel cluster di origine.</span><span class="sxs-lookup"><span data-stu-id="4f821-212">The messages retrieved from the topic are the same as entered on the source cluster.</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="4f821-213">Eliminazione del cluster</span><span class="sxs-lookup"><span data-stu-id="4f821-213">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="4f821-214">Le procedure illustrate in questo documento creano entrambi i cluster nello stesso gruppo di risorse di Azure. È quindi possibile eliminare il gruppo di risorse dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4f821-214">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="4f821-215">In questo modo vengono rimosse tutte le risorse create seguendo le istruzioni di questo documento, la rete virtuale di Azure e l'account di archiviazione usato dai cluster.</span><span class="sxs-lookup"><span data-stu-id="4f821-215">Deleting the resource group removes all resources created by following this document, the Azure Virtual Network, and storage account used by the clusters.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4f821-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4f821-216">Next Steps</span></span>

<span data-ttu-id="4f821-217">In questo documento è stato descritto come usare MirrorMaker per creare la replica di un cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="4f821-217">In this document, you learned how to use MirrorMaker to create a replica of a Kafka cluster.</span></span> <span data-ttu-id="4f821-218">Per trovare altri modi per lavorare con Kafka, vedere i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="4f821-218">Use the following links to discover other ways to work with Kafka:</span></span>

* <span data-ttu-id="4f821-219">[Documentazione su Apache Kafka MirrorMaker](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) in cwiki.apache.org.</span><span class="sxs-lookup"><span data-stu-id="4f821-219">[Apache Kafka MirrorMaker documentation](https://cwiki.apache.org/confluence/pages/viewpage.action?pageId=27846330) at cwiki.apache.org.</span></span>
* [<span data-ttu-id="4f821-220">Introduzione ad Apache Kafka (anteprima) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f821-220">Get started with Apache Kafka on HDInsight</span></span>](hdinsight-apache-kafka-get-started.md)
* <span data-ttu-id="4f821-221">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Usare Apache Spark con Kafka in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="4f821-221">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>
* [<span data-ttu-id="4f821-222">Usare Apache Storm (anteprima) con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="4f821-222">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* <span data-ttu-id="4f821-223">[Connect to Kafka through an Azure Virtual Network](hdinsight-apache-kafka-connect-vpn-gateway.md) (Connettersi a Kafka tramite una rete virtuale di Azure)</span><span class="sxs-lookup"><span data-stu-id="4f821-223">[Connect to Kafka through an Azure Virtual Network](hdinsight-apache-kafka-connect-vpn-gateway.md)</span></span>
