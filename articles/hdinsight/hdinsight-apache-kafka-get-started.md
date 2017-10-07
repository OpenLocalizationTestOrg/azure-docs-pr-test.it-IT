---
title: aaaStart con Apache Kafka - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toocreate un Kafka Apache cluster in Azure HDInsight. Informazioni su come toocreate argomenti, i sottoscrittori e i consumer.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 43585abf-bec1-4322-adde-6db21de98d7f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: 
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: b93299d88dc2cf9a9764662509308ff75fd74474
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="start-with-apache-kafka-preview-on-hdinsight"></a><span data-ttu-id="eabb0-104">Iniziare a usare Apache Kafka (anteprima) in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eabb0-104">Start with Apache Kafka (preview) on HDInsight</span></span>

<span data-ttu-id="eabb0-105">Informazioni su come toocreate e utilizzare un [Kafka Apache](https://kafka.apache.org) cluster in Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eabb0-105">Learn how toocreate and use an [Apache Kafka](https://kafka.apache.org) cluster on Azure HDInsight.</span></span> <span data-ttu-id="eabb0-106">Kafka è una piattaforma di streaming distribuita open source disponibile con HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eabb0-106">Kafka is an open-source, distributed streaming platform that is available with HDInsight.</span></span> <span data-ttu-id="eabb0-107">Viene spesso usato come broker di messaggi, che fornisce funzionalità simili tooa pubblicazione-sottoscrizione coda di messaggi.</span><span class="sxs-lookup"><span data-stu-id="eabb0-107">It is often used as a message broker, as it provides functionality similar tooa publish-subscribe message queue.</span></span>

> [!NOTE]
> <span data-ttu-id="eabb0-108">Con HDInsight sono attualmente disponibili due versioni di Kafka: 0.9.0 (HDInsight 3.4) e 0.10.0 (HDInsight 3.5 e 3.6).</span><span class="sxs-lookup"><span data-stu-id="eabb0-108">There are currently two versions of Kafka available with HDInsight; 0.9.0 (HDInsight 3.4) and 0.10.0 (HDInsight 3.5 and 3.6).</span></span> <span data-ttu-id="eabb0-109">passaggi di Hello in questo documento si presuppongono che si stanno utilizzando Kafka 3.6 di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eabb0-109">hello steps in this document assume that you are using Kafka on HDInsight 3.6.</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="create-a-kafka-cluster"></a><span data-ttu-id="eabb0-110">Creare un cluster Kafka</span><span class="sxs-lookup"><span data-stu-id="eabb0-110">Create a Kafka cluster</span></span>

<span data-ttu-id="eabb0-111">Utilizzare hello seguendo i passaggi toocreate un Kafka cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="eabb0-111">Use hello following steps toocreate a Kafka on HDInsight cluster:</span></span>

1. <span data-ttu-id="eabb0-112">Da hello [portale di Azure](https://portal.azure.com)selezionare **+ nuovo**, **Intelligence + Analitica**, quindi selezionare **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="eabb0-112">From hello [Azure portal](https://portal.azure.com), select **+ NEW**, **Intelligence + Analytics**, and then select **HDInsight**.</span></span>
   
    ![Creazione di un cluster HDInsight](./media/hdinsight-apache-kafka-get-started/create-hdinsight.png)

2. <span data-ttu-id="eabb0-114">Da **nozioni di base**, immettere hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="eabb0-114">From **Basics**, enter hello following information:</span></span>

    * <span data-ttu-id="eabb0-115">**Nome del cluster**: nome hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-115">**Cluster Name**: hello name of hello HDInsight cluster.</span></span>
    * <span data-ttu-id="eabb0-116">**Sottoscrizione**: selezionare hello toouse di sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="eabb0-116">**Subscription**: Select hello subscription toouse.</span></span>
    * <span data-ttu-id="eabb0-117">**Nome utente account di accesso del cluster** e **password dell'account di accesso Cluster**: accesso hello quando si accede a cluster hello tramite HTTPS.</span><span class="sxs-lookup"><span data-stu-id="eabb0-117">**Cluster login username** and **Cluster login password**: hello login when accessing hello cluster over HTTPS.</span></span> <span data-ttu-id="eabb0-118">Usare questi servizi tooaccess credenziali, ad esempio hello dell'interfaccia utente Web Ambari o l'API REST.</span><span class="sxs-lookup"><span data-stu-id="eabb0-118">You use these credentials tooaccess services such as hello Ambari Web UI or REST API.</span></span>
    * <span data-ttu-id="eabb0-119">**Secure Shell (SSH) username**: hello account di accesso quando si accede a cluster hello su SSH.</span><span class="sxs-lookup"><span data-stu-id="eabb0-119">**Secure Shell (SSH) username**: hello login used when accessing hello cluster over SSH.</span></span> <span data-ttu-id="eabb0-120">Per impostazione predefinita la password di hello è hello come password di accesso cluster hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-120">By default hello password is hello same as hello cluster login password.</span></span>
    * <span data-ttu-id="eabb0-121">**Gruppo di risorse**: hello gruppo toocreate hello cluster della risorsa in.</span><span class="sxs-lookup"><span data-stu-id="eabb0-121">**Resource Group**: hello resource group toocreate hello cluster in.</span></span>
    * <span data-ttu-id="eabb0-122">**Percorso**: hello Azure area toocreate hello cluster.</span><span class="sxs-lookup"><span data-stu-id="eabb0-122">**Location**: hello Azure region toocreate hello cluster in.</span></span>
   
 ![Selezionare la sottoscrizione](./media/hdinsight-apache-kafka-get-started/hdinsight-basic-configuration.png)

3. <span data-ttu-id="eabb0-124">Selezionare **Cluster tipo**, e quindi set hello seguendo i valori da **configurazione Cluster**:</span><span class="sxs-lookup"><span data-stu-id="eabb0-124">Select **Cluster type**, and then set hello following values from **Cluster configuration**:</span></span>
   
    * <span data-ttu-id="eabb0-125">**Tipo di cluster**: Kafka</span><span class="sxs-lookup"><span data-stu-id="eabb0-125">**Cluster Type**: Kafka</span></span>

    * <span data-ttu-id="eabb0-126">**Versione**: Kafka 0.10.0 (HDI 3.6)</span><span class="sxs-lookup"><span data-stu-id="eabb0-126">**Version**: Kafka 0.10.0 (HDI 3.6)</span></span>

    * <span data-ttu-id="eabb0-127">**Livello cluster**: Standard</span><span class="sxs-lookup"><span data-stu-id="eabb0-127">**Cluster Tier**: Standard</span></span>
     
 <span data-ttu-id="eabb0-128">Infine, utilizzare hello **selezionare** pulsante toosave impostazioni.</span><span class="sxs-lookup"><span data-stu-id="eabb0-128">Finally, use hello **Select** button toosave settings.</span></span>
     
 ![Selezionare il tipo di cluster](./media/hdinsight-apache-kafka-get-started/set-hdinsight-cluster-type.png)

4. <span data-ttu-id="eabb0-130">Dopo aver selezionato il tipo di cluster hello, utilizzare hello __selezionare__ tooset hello cluster tipo di pulsante.</span><span class="sxs-lookup"><span data-stu-id="eabb0-130">After selecting hello cluster type, use hello __Select__ button tooset hello cluster type.</span></span> <span data-ttu-id="eabb0-131">Successivamente, utilizzare hello __Avanti__ configurazione di base toofinish pulsante.</span><span class="sxs-lookup"><span data-stu-id="eabb0-131">Next, use hello __Next__ button toofinish basic configuration.</span></span>

5. <span data-ttu-id="eabb0-132">In **Archiviazione** selezionare o creare un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="eabb0-132">From **Storage**, select or create a Storage account.</span></span> <span data-ttu-id="eabb0-133">Per i passaggi hello in questo documento, lasciare hello altri campi valori predefiniti di hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-133">For hello steps in this document, leave hello other fields at hello default values.</span></span> <span data-ttu-id="eabb0-134">Hello utilizzare __Avanti__ configurazione dell'archiviazione toosave pulsante.</span><span class="sxs-lookup"><span data-stu-id="eabb0-134">Use hello __Next__ button toosave storage configuration.</span></span>

    ![Configurare le impostazioni di account di archiviazione hello per HDInsight](./media/hdinsight-apache-kafka-get-started/set-hdinsight-storage-account.png)

6. <span data-ttu-id="eabb0-136">Da __applicazioni (facoltative)__selezionare __Avanti__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="eabb0-136">From __Applications (optional)__, select __Next__ toocontinue.</span></span> <span data-ttu-id="eabb0-137">Non sono richieste applicazioni per questo esempio.</span><span class="sxs-lookup"><span data-stu-id="eabb0-137">No applications are required for this example.</span></span>

7. <span data-ttu-id="eabb0-138">Da __dimensioni del Cluster__selezionare __Avanti__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="eabb0-138">From __Cluster size__, select __Next__ toocontinue.</span></span>

    > [!WARNING]
    > <span data-ttu-id="eabb0-139">disponibilità tooguarantee Kafka in HDInsight, il cluster deve contenere almeno tre nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="eabb0-139">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span>

    ![Set hello dimensione del cluster Kafka](./media/hdinsight-apache-kafka-get-started/kafka-cluster-size.png)

    > [!NOTE]
    > <span data-ttu-id="eabb0-141">Hello **dischi per ogni nodo del lavoro** controlli voce hello scalabilità di Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eabb0-141">hello **disks per worker node** entry controls hello scalability of Kafka on HDInsight.</span></span> <span data-ttu-id="eabb0-142">Per altre informazioni, vedere [Configurare l'archiviazione e la scalabilità per Apache Kafka in HDInsight](hdinsight-apache-kafka-scalability.md).</span><span class="sxs-lookup"><span data-stu-id="eabb0-142">For more information, see [Configure storage and scalability of Kafka on HDInsight](hdinsight-apache-kafka-scalability.md).</span></span>

8. <span data-ttu-id="eabb0-143">Da __impostazioni avanzate__selezionare __Avanti__ toocontinue.</span><span class="sxs-lookup"><span data-stu-id="eabb0-143">From __Advanced settings__, select __Next__ toocontinue.</span></span>

9. <span data-ttu-id="eabb0-144">Da hello **riepilogo**, esaminare la configurazione hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-144">From hello **Summary**, review hello configuration for hello cluster.</span></span> <span data-ttu-id="eabb0-145">Hello utilizzare __modifica__ collegamenti toochange eventuali impostazioni non sono corrette.</span><span class="sxs-lookup"><span data-stu-id="eabb0-145">Use hello __Edit__ links toochange any settings that are incorrect.</span></span> <span data-ttu-id="eabb0-146">Infine, utilizzare the__Create__ pulsante toocreate hello cluster.</span><span class="sxs-lookup"><span data-stu-id="eabb0-146">Finally, use the__Create__ button toocreate hello cluster.</span></span>
   
    ![Riepilogo della configurazione del cluster](./media/hdinsight-apache-kafka-get-started/hdinsight-configuration-summary.png)
   
    > [!NOTE]
    > <span data-ttu-id="eabb0-148">Può richiedere di cluster hello toocreate di too20 minuti.</span><span class="sxs-lookup"><span data-stu-id="eabb0-148">It can take up too20 minutes toocreate hello cluster.</span></span>

## <a name="connect-toohello-cluster"></a><span data-ttu-id="eabb0-149">Connettere il cluster toohello</span><span class="sxs-lookup"><span data-stu-id="eabb0-149">Connect toohello cluster</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eabb0-150">Quando si esegue hello alla procedura seguente, è necessario utilizzare un client SSH.</span><span class="sxs-lookup"><span data-stu-id="eabb0-150">When performing hello following steps, you must use an SSH client.</span></span> <span data-ttu-id="eabb0-151">Per ulteriori informazioni, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="eabb0-151">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

<span data-ttu-id="eabb0-152">Dal client, usare SSH tooconnect toohello cluster:</span><span class="sxs-lookup"><span data-stu-id="eabb0-152">From your client, use SSH tooconnect toohello cluster:</span></span>

```ssh SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net```

<span data-ttu-id="eabb0-153">Sostituire **SSHUSER** con il nome utente SSH hello fornito durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="eabb0-153">Replace **SSHUSER** with hello SSH username you provided during cluster creation.</span></span> <span data-ttu-id="eabb0-154">Sostituire **CLUSTERNAME** con nome hello del cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-154">Replace **CLUSTERNAME** with hello name of hello cluster.</span></span>

<span data-ttu-id="eabb0-155">Quando richiesto, immettere la password di hello utilizzati per hello account SSH.</span><span class="sxs-lookup"><span data-stu-id="eabb0-155">When prompted, enter hello password you used for hello SSH account.</span></span>

<span data-ttu-id="eabb0-156">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="eabb0-156">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="eabb0-157"><a id="getkafkainfo"></a>Ottenere informazioni di host hello Zookeeper e Service Broker</span><span class="sxs-lookup"><span data-stu-id="eabb0-157"><a id="getkafkainfo"></a>Get hello Zookeeper and Broker host information</span></span>

<span data-ttu-id="eabb0-158">Quando si lavora con Kafka, è necessario conoscere i due valori di host. Hello *Zookeeper* host e hello *Broker* host.</span><span class="sxs-lookup"><span data-stu-id="eabb0-158">When working with Kafka, you must know two host values; hello *Zookeeper* hosts and hello *Broker* hosts.</span></span> <span data-ttu-id="eabb0-159">Questi host vengono utilizzati con l'API Kafka hello e molte delle utilità hello forniti con Kafka.</span><span class="sxs-lookup"><span data-stu-id="eabb0-159">These hosts are used with hello Kafka API and many of hello utilities that ship with Kafka.</span></span>

<span data-ttu-id="eabb0-160">Utilizzare hello seguenti variabili di ambiente toocreate passaggi che contengono informazioni sull'host hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-160">Use hello following steps toocreate environment variables that contain hello host information.</span></span> <span data-ttu-id="eabb0-161">Queste variabili di ambiente vengono utilizzate nei passaggi hello in questo documento.</span><span class="sxs-lookup"><span data-stu-id="eabb0-161">These environment variables are used in hello steps in this document.</span></span>

1. <span data-ttu-id="eabb0-162">Da un cluster di toohello connessione SSH, seguente hello utilizzare comandi hello tooinstall `jq` utilità.</span><span class="sxs-lookup"><span data-stu-id="eabb0-162">From an SSH connection toohello cluster, use hello following command tooinstall hello `jq` utility.</span></span> <span data-ttu-id="eabb0-163">Questa utilità è tooparse utilizzati documenti JSON ed è utile per il recupero di informazioni sull'host di Service broker hello:</span><span class="sxs-lookup"><span data-stu-id="eabb0-163">This utility is used tooparse JSON documents, and is useful in retrieving hello broker host information:</span></span>
   
    ```bash
    sudo apt -y install jq
    ```

2. <span data-ttu-id="eabb0-164">le variabili di ambiente hello tooset con le informazioni recuperate dai Ambari, hello di utilizzare i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="eabb0-164">tooset hello environment variables with information retrieved from Ambari, use hello following commands:</span></span>

    ```bash
    CLUSTERNAME='your cluster name'
    PASSWORD='your cluster password'
    export KAFKAZKHOSTS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2`

    export KAFKABROKERS=`curl -sS -u admin:$PASSWORD -G https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2`

    echo '$KAFKAZKHOSTS='$KAFKAZKHOSTS
    echo '$KAFKABROKERS='$KAFKABROKERS
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="eabb0-165">Impostare `CLUSTERNAME=` toohello nome di cluster Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-165">Set `CLUSTERNAME=` toohello name of hello Kafka cluster.</span></span> <span data-ttu-id="eabb0-166">Impostare `PASSWORD=` password di accesso (amministrazione) toohello utilizzato per la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-166">Set `PASSWORD=` toohello login (admin) password you used when creating hello cluster.</span></span>

    <span data-ttu-id="eabb0-167">testo Hello è riportato un esempio del contenuto di hello di `$KAFKAZKHOSTS`:</span><span class="sxs-lookup"><span data-stu-id="eabb0-167">hello following text is an example of hello contents of `$KAFKAZKHOSTS`:</span></span>
   
    `zk0-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181,zk2-kafka.eahjefxxp1netdbyklgqj5y1ud.ex.internal.cloudapp.net:2181`
   
    <span data-ttu-id="eabb0-168">testo Hello è riportato un esempio del contenuto di hello di `$KAFKABROKERS`:</span><span class="sxs-lookup"><span data-stu-id="eabb0-168">hello following text is an example of hello contents of `$KAFKABROKERS`:</span></span>
   
    `wn1-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092,wn0-kafka.eahjefxxp1netdbyklgqj5y1ud.cx.internal.cloudapp.net:9092`

    > [!NOTE]
    > <span data-ttu-id="eabb0-169">Hello `cut` comando è elenco hello tootrim utilizzato di voci di host tootwo host.</span><span class="sxs-lookup"><span data-stu-id="eabb0-169">hello `cut` command is used tootrim hello list of hosts tootwo host entries.</span></span> <span data-ttu-id="eabb0-170">Elenco completo di hello tooprovide degli host non è necessario quando si crea un consumer Kafka o il produttore.</span><span class="sxs-lookup"><span data-stu-id="eabb0-170">You do not need tooprovide hello full list of hosts when creating a Kafka consumer or producer.</span></span>
   
    > [!WARNING]
    > <span data-ttu-id="eabb0-171">Non fare affidamento su hello le informazioni restituite da questa sessione tooalways sia accurato.</span><span class="sxs-lookup"><span data-stu-id="eabb0-171">Do not rely on hello information returned from this session tooalways be accurate.</span></span> <span data-ttu-id="eabb0-172">Se si modifica la scala cluster hello, nuovo Broker vengono aggiunti o rimossi.</span><span class="sxs-lookup"><span data-stu-id="eabb0-172">If you scale hello cluster, new brokers are added or removed.</span></span> <span data-ttu-id="eabb0-173">Se si verifica un errore e viene sostituito un nodo, il nome host hello per nodo hello potrebbe cambiare.</span><span class="sxs-lookup"><span data-stu-id="eabb0-173">If a failure occurs and a node is replaced, hello host name for hello node may change.</span></span>
    >
    > <span data-ttu-id="eabb0-174">È necessario recuperare informazioni di host Zookeeper e broker hello poco prima di utilizzare tooensure si dispone di informazioni valide.</span><span class="sxs-lookup"><span data-stu-id="eabb0-174">You should retrieve hello Zookeeper and broker hosts information shortly before you use it tooensure you have valid information.</span></span>

## <a name="create-a-topic"></a><span data-ttu-id="eabb0-175">Creare un argomento</span><span class="sxs-lookup"><span data-stu-id="eabb0-175">Create a topic</span></span>

<span data-ttu-id="eabb0-176">Kafka archivia i flussi di dati in categorie denominate *argomenti*.</span><span class="sxs-lookup"><span data-stu-id="eabb0-176">Kafka stores streams of data in categories called *topics*.</span></span> <span data-ttu-id="eabb0-177">Da un SSH connessione tooa nodo head cluster, utilizzare uno script fornito con Kafka toocreate un argomento:</span><span class="sxs-lookup"><span data-stu-id="eabb0-177">From An SSH connection tooa cluster headnode, use a script provided with Kafka toocreate a topic:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic test --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="eabb0-178">Questo comando si connette utilizzando hello host informazioni archiviate in tooZookeeper `$KAFKAZKHOSTS`e quindi creare l'argomento Kafka denominato **test**.</span><span class="sxs-lookup"><span data-stu-id="eabb0-178">This command connects tooZookeeper using hello host information stored in `$KAFKAZKHOSTS`, and then create Kafka topic named **test**.</span></span> <span data-ttu-id="eabb0-179">È possibile verificare che tale argomento hello è stato creato utilizzando i seguenti argomenti toolist script hello:</span><span class="sxs-lookup"><span data-stu-id="eabb0-179">You can verify that hello topic was created by using hello following script toolist topics:</span></span>

```bash
/usr/hdp/current/kafka-broker/bin/kafka-topics.sh --list --zookeeper $KAFKAZKHOSTS
```

<span data-ttu-id="eabb0-180">Hello output di questo comando Elenca argomenti Kafka, che contiene hello **test** argomento.</span><span class="sxs-lookup"><span data-stu-id="eabb0-180">hello output of this command lists Kafka topics, which contains hello **test** topic.</span></span>

## <a name="produce-and-consume-records"></a><span data-ttu-id="eabb0-181">Produrre e utilizzare record</span><span class="sxs-lookup"><span data-stu-id="eabb0-181">Produce and consume records</span></span>

<span data-ttu-id="eabb0-182">Kafka archivia i *record* negli argomenti.</span><span class="sxs-lookup"><span data-stu-id="eabb0-182">Kafka stores *records* in topics.</span></span> <span data-ttu-id="eabb0-183">I record vengono prodotti da *producer* e usati da *consumer*.</span><span class="sxs-lookup"><span data-stu-id="eabb0-183">Records are produced by *producers*, and consumed by *consumers*.</span></span> <span data-ttu-id="eabb0-184">I producer recuperano i record da *broker* di Kafka.</span><span class="sxs-lookup"><span data-stu-id="eabb0-184">Producers retrieve records from Kafka *brokers*.</span></span> <span data-ttu-id="eabb0-185">Ogni nodo del ruolo di lavoro nel cluster HDInsight è un broker Kafka.</span><span class="sxs-lookup"><span data-stu-id="eabb0-185">Each worker node in your HDInsight cluster is a Kafka broker.</span></span>

<span data-ttu-id="eabb0-186">Utilizzare i seguenti record di toostore passaggi nell'argomento di prova hello creato in precedenza e quindi leggerli utilizzando un consumer hello:</span><span class="sxs-lookup"><span data-stu-id="eabb0-186">Use hello following steps toostore records into hello test topic you created earlier, and then read them using a consumer:</span></span>

1. <span data-ttu-id="eabb0-187">Dalla sessione SSH hello, usare uno script fornito con l'argomento di toohello Kafka toowrite record:</span><span class="sxs-lookup"><span data-stu-id="eabb0-187">From hello SSH session, use a script provided with Kafka toowrite records toohello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-producer.sh --broker-list $KAFKABROKERS --topic test
    ```
   
    <span data-ttu-id="eabb0-188">Non vengono restituiti toohello prompt dei comandi dopo questo comando.</span><span class="sxs-lookup"><span data-stu-id="eabb0-188">You are not returned toohello prompt after this command.</span></span> <span data-ttu-id="eabb0-189">Digitare alcuni messaggi di testo e quindi utilizzare **Ctrl + C** toostop invio toohello argomento.</span><span class="sxs-lookup"><span data-stu-id="eabb0-189">Instead, type a few text messages and then use **Ctrl + C** toostop sending toohello topic.</span></span> <span data-ttu-id="eabb0-190">Ogni riga viene inviata come record distinto.</span><span class="sxs-lookup"><span data-stu-id="eabb0-190">Each line is sent as a separate record.</span></span>

2. <span data-ttu-id="eabb0-191">Utilizzare uno script fornito con i record di tooread Kafka dall'argomento hello:</span><span class="sxs-lookup"><span data-stu-id="eabb0-191">Use a script provided with Kafka tooread records from hello topic:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic test --from-beginning
    ```
   
    <span data-ttu-id="eabb0-192">Questo comando recupera i record di hello dall'argomento hello e li visualizza.</span><span class="sxs-lookup"><span data-stu-id="eabb0-192">This command retrieves hello records from hello topic and displays them.</span></span> <span data-ttu-id="eabb0-193">Utilizzando `--from-beginning` indica hello consumer toostart dall'inizio di hello del flusso di hello, pertanto vengono recuperati tutti i record.</span><span class="sxs-lookup"><span data-stu-id="eabb0-193">Using `--from-beginning` tells hello consumer toostart from hello beginning of hello stream, so all records are retrieved.</span></span>

3. <span data-ttu-id="eabb0-194">Utilizzare __Ctrl + C__ consumer hello toostop.</span><span class="sxs-lookup"><span data-stu-id="eabb0-194">Use __Ctrl + C__ toostop hello consumer.</span></span>

## <a name="producer-and-consumer-api"></a><span data-ttu-id="eabb0-195">API per producer e consumer</span><span class="sxs-lookup"><span data-stu-id="eabb0-195">Producer and consumer API</span></span>

<span data-ttu-id="eabb0-196">È possibile anche a livello di codice producono e utilizzano i record mediante hello [Kafka API](http://kafka.apache.org/documentation#api).</span><span class="sxs-lookup"><span data-stu-id="eabb0-196">You can also programmatically produce and consume records using hello [Kafka APIs](http://kafka.apache.org/documentation#api).</span></span> <span data-ttu-id="eabb0-197">toobuild un produttore di Java e i consumer, utilizzare hello seguendo i passaggi nell'ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="eabb0-197">toobuild a Java producer and consumer, use hello following steps from your development environment.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eabb0-198">È necessario che i seguenti componenti installati nell'ambiente di sviluppo hello:</span><span class="sxs-lookup"><span data-stu-id="eabb0-198">You must have hello following components installed in your development environment:</span></span>
>
> * <span data-ttu-id="eabb0-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o equivalente, ad esempio OpenJDK.</span><span class="sxs-lookup"><span data-stu-id="eabb0-199">[Java JDK 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) or an equivalent, such as OpenJDK.</span></span>
>
> * [<span data-ttu-id="eabb0-200">Apache Maven</span><span class="sxs-lookup"><span data-stu-id="eabb0-200">Apache Maven</span></span>](http://maven.apache.org/)
>
> * <span data-ttu-id="eabb0-201">Un client SSH e hello `scp` comando.</span><span class="sxs-lookup"><span data-stu-id="eabb0-201">An SSH client and hello `scp` command.</span></span> <span data-ttu-id="eabb0-202">Per ulteriori informazioni, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="eabb0-202">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

1. <span data-ttu-id="eabb0-203">Scaricare esempi hello da [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span><span class="sxs-lookup"><span data-stu-id="eabb0-203">Download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started).</span></span> <span data-ttu-id="eabb0-204">Ad esempio di tipo produttore/consumer hello, utilizzare il progetto di hello in hello `Producer-Consumer` directory.</span><span class="sxs-lookup"><span data-stu-id="eabb0-204">For hello producer/consumer example, use hello project in hello `Producer-Consumer` directory.</span></span> <span data-ttu-id="eabb0-205">In questo esempio contiene hello le seguenti classi:</span><span class="sxs-lookup"><span data-stu-id="eabb0-205">This example contains hello following classes:</span></span>
   
    * <span data-ttu-id="eabb0-206">**Eseguire** -avvia consumer hello o produttori.</span><span class="sxs-lookup"><span data-stu-id="eabb0-206">**Run** - starts either hello consumer or producer.</span></span>

    * <span data-ttu-id="eabb0-207">**Producer** -archivi 1.000.000 record toohello argomento.</span><span class="sxs-lookup"><span data-stu-id="eabb0-207">**Producer** - stores 1,000,000 records toohello topic.</span></span>

    * <span data-ttu-id="eabb0-208">**Consumer** -legge i record da un argomento di hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-208">**Consumer** - reads records from hello topic.</span></span>

2. <span data-ttu-id="eabb0-209">un pacchetto, jar toocreate posizionarsi directory toohello di hello `Producer-Consumer` directory e utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eabb0-209">toocreate a jar package, change directories toohello location of hello `Producer-Consumer` directory and use hello following command:</span></span>

    ```
    mvn clean package
    ```

    <span data-ttu-id="eabb0-210">Questo comando crea una directory denominata `target`, che contiene un file denominato `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="eabb0-210">This command creates a directory named `target`, that contains a file named `kafka-producer-consumer-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="eabb0-211">Seguente hello utilizzare comandi hello toocopy `kafka-producer-consumer-1.0-SNAPSHOT.jar` cluster HDInsight tooyour di file:</span><span class="sxs-lookup"><span data-stu-id="eabb0-211">Use hello following commands toocopy hello `kafka-producer-consumer-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-producer-consumer-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-producer-consumer.jar
    ```
   
    <span data-ttu-id="eabb0-212">Sostituire **SSHUSER** con utente SSH hello per il cluster, quindi sostituire **CLUSTERNAME** con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="eabb0-212">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="eabb0-213">Quando richiesto immettere la password di hello hello SSH utente.</span><span class="sxs-lookup"><span data-stu-id="eabb0-213">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="eabb0-214">Una volta hello `scp` comando al termine della copia del file hello, connettere il cluster toohello tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="eabb0-214">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH.</span></span> <span data-ttu-id="eabb0-215">Utilizzare hello comando toowrite record toohello test argomento:</span><span class="sxs-lookup"><span data-stu-id="eabb0-215">Use hello following command toowrite records toohello test topic:</span></span>

    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS
    ```

5. <span data-ttu-id="eabb0-216">Al termine il processo di hello, utilizzare hello successivo comando tooread dall'argomento hello:</span><span class="sxs-lookup"><span data-stu-id="eabb0-216">Once hello process has finished, use hello following command tooread from hello topic:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS
    ```
   
    <span data-ttu-id="eabb0-217">record di Hello letti, insieme a un conteggio di record, viene visualizzato.</span><span class="sxs-lookup"><span data-stu-id="eabb0-217">hello records read, along with a count of records, is displayed.</span></span> <span data-ttu-id="eabb0-218">È possibile visualizzare alcuni maggiore di 1.000.000 registrati come argomento di toohello record diversi tramite uno script in un passaggio precedente è stata inviata.</span><span class="sxs-lookup"><span data-stu-id="eabb0-218">You may see a few more than 1,000,000 logged as you sent several records toohello topic using a script in an earlier step.</span></span>

6. <span data-ttu-id="eabb0-219">Utilizzare __Ctrl + C__ consumer hello tooexit.</span><span class="sxs-lookup"><span data-stu-id="eabb0-219">Use __Ctrl + C__ tooexit hello consumer.</span></span>

### <a name="multiple-consumers"></a><span data-ttu-id="eabb0-220">Consumer multipli</span><span class="sxs-lookup"><span data-stu-id="eabb0-220">Multiple consumers</span></span>

<span data-ttu-id="eabb0-221">I consumer Kafka usano un gruppo di consumer durante la lettura dei record.</span><span class="sxs-lookup"><span data-stu-id="eabb0-221">Kafka consumers use a consumer group when reading records.</span></span> <span data-ttu-id="eabb0-222">Utilizzo hello stessa raggruppamento con più consumer risultati carico bilanciato legge da un argomento.</span><span class="sxs-lookup"><span data-stu-id="eabb0-222">Using hello same group with multiple consumers results in load balanced reads from a topic.</span></span> <span data-ttu-id="eabb0-223">Nel gruppo hello ogni consumer riceve una parte del record di hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-223">Each consumer in hello group receives a portion of hello records.</span></span> <span data-ttu-id="eabb0-224">toosee il processo, utilizzare hello seguendo i passaggi:</span><span class="sxs-lookup"><span data-stu-id="eabb0-224">toosee this process in action, use hello following steps:</span></span>

1. <span data-ttu-id="eabb0-225">Aprire un nuovo SSH sessione toohello cluster, in modo da disporre di due di essi.</span><span class="sxs-lookup"><span data-stu-id="eabb0-225">Open a new SSH session toohello cluster, so that you have two of them.</span></span> <span data-ttu-id="eabb0-226">In ogni sessione, utilizzare hello seguenti toostart un consumer con hello stesso ID di gruppo di consumer:</span><span class="sxs-lookup"><span data-stu-id="eabb0-226">In each session, use hello following toostart a consumer with hello same consumer group ID:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar consumer $KAFKABROKERS mygroup
    ```

    <span data-ttu-id="eabb0-227">Questo comando avvia un consumer con ID gruppo hello `mygroup`.</span><span class="sxs-lookup"><span data-stu-id="eabb0-227">This command starts a consumer using hello group ID `mygroup`.</span></span>

    > [!NOTE]
    > <span data-ttu-id="eabb0-228">Utilizzare i comandi di hello in hello [informazioni hello Zookeeper e Broker host](#getkafkainfo) tooset sezione `$KAFKABROKERS` per questa sessione SSH.</span><span class="sxs-lookup"><span data-stu-id="eabb0-228">Use hello commands in hello [Get hello Zookeeper and Broker host information](#getkafkainfo) section tooset `$KAFKABROKERS` for this SSH session.</span></span>

2. <span data-ttu-id="eabb0-229">Osservare come i record di hello conteggi ogni sessione ricevuti da un argomento di hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-229">Watch as each session counts hello records it receives from hello topic.</span></span> <span data-ttu-id="eabb0-230">Totale Hello di entrambe le sessioni deve hello stesso come ricevuto in precedenza da un consumer.</span><span class="sxs-lookup"><span data-stu-id="eabb0-230">hello total of both sessions should be hello same as you received previously from one consumer.</span></span>

<span data-ttu-id="eabb0-231">Consumo client all'interno dello stesso gruppo viene gestito tramite le partizioni di hello per argomento hello hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-231">Consumption by clients within hello same group is handled through hello partitions for hello topic.</span></span> <span data-ttu-id="eabb0-232">Per hello `test` argomento creato in precedenza, include otto partizioni.</span><span class="sxs-lookup"><span data-stu-id="eabb0-232">For hello `test` topic created earlier, it has eight partitions.</span></span> <span data-ttu-id="eabb0-233">Se si apre otto sessioni SSH e avvia un consumer in tutte le sessioni, ogni consumer legge i record da una singola partizione per l'argomento hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-233">If you open eight SSH sessions and launch a consumer in all sessions, each consumer reads records from a single partition for hello topic.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eabb0-234">Un gruppo di consumer non può contenere un numero di istanze di consumer maggiore del numero di partizioni.</span><span class="sxs-lookup"><span data-stu-id="eabb0-234">There cannot be more consumer instances in a consumer group than partitions.</span></span> <span data-ttu-id="eabb0-235">In questo esempio, un gruppo di consumer può contenere i consumatori tooeight poiché questo è il numero di hello di partizioni nell'argomento hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-235">In this example, one consumer group can contain up tooeight consumers since that is hello number of partitions in hello topic.</span></span> <span data-ttu-id="eabb0-236">In alternativa è possibile avere più gruppi di consumer, ognuno con al massimo otto consumer.</span><span class="sxs-lookup"><span data-stu-id="eabb0-236">Or you can have multiple consumer groups, each with no more than eight consumers.</span></span>

<span data-ttu-id="eabb0-237">Record archiviati in Kafka vengono archiviati in ordine di hello che vengono ricevuti all'interno di una partizione.</span><span class="sxs-lookup"><span data-stu-id="eabb0-237">Records stored in Kafka are stored in hello order they are received within a partition.</span></span> <span data-ttu-id="eabb0-238">tooachieve nell'ordine di recapito per i record *all'interno di una partizione*, creare un gruppo di consumer in cui il numero di hello di istanze di consumer corrisponde numero hello di partizioni.</span><span class="sxs-lookup"><span data-stu-id="eabb0-238">tooachieve in-ordered delivery for records *within a partition*, create a consumer group where hello number of consumer instances matches hello number of partitions.</span></span> <span data-ttu-id="eabb0-239">tooachieve nell'ordine di recapito per i record *in argomento hello*, creare un gruppo di consumer con l'istanza di un solo consumer.</span><span class="sxs-lookup"><span data-stu-id="eabb0-239">tooachieve in-ordered delivery for records *within hello topic*, create a consumer group with only one consumer instance.</span></span>

## <a name="streaming-api"></a><span data-ttu-id="eabb0-240">API di streaming</span><span class="sxs-lookup"><span data-stu-id="eabb0-240">Streaming API</span></span>

<span data-ttu-id="eabb0-241">Hello streaming API tooKafka è stato aggiunto nella versione 0.10.0; le versioni precedenti si basano su Apache Spark o Storm per l'elaborazione del flusso.</span><span class="sxs-lookup"><span data-stu-id="eabb0-241">hello streaming API was added tooKafka in version 0.10.0; earlier versions rely on Apache Spark or Storm for stream processing.</span></span>

1. <span data-ttu-id="eabb0-242">Se non già stato fatto, scaricare gli esempi di hello da [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour ambiente di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="eabb0-242">If you haven't already done so, download hello examples from [https://github.com/Azure-Samples/hdinsight-kafka-java-get-started](https://github.com/Azure-Samples/hdinsight-kafka-java-get-started) tooyour development environment.</span></span> <span data-ttu-id="eabb0-243">Per hello lo streaming di esempio, utilizzare il progetto di hello in hello `streaming` directory.</span><span class="sxs-lookup"><span data-stu-id="eabb0-243">For hello streaming example, use hello project in hello `streaming` directory.</span></span>
   
    <span data-ttu-id="eabb0-244">Questo progetto contiene solo una classe, `Stream`, che legge i record da hello `test` argomento creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="eabb0-244">This project contains only one class, `Stream`, which reads records from hello `test` topic created previously.</span></span> <span data-ttu-id="eabb0-245">Conteggi parole hello leggere e genera ogni argomento tooa conteggio delle parole e denominato `wordcounts`.</span><span class="sxs-lookup"><span data-stu-id="eabb0-245">It counts hello words read, and emits each word and count tooa topic named `wordcounts`.</span></span> <span data-ttu-id="eabb0-246">Hello `wordcounts` argomento viene creato in un passaggio successivo in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="eabb0-246">hello `wordcounts` topic is created in a later step in this section.</span></span>

2. <span data-ttu-id="eabb0-247">Dalla riga di comando hello nell'ambiente di sviluppo, modificare il percorso di directory toohello di hello `Streaming` directory, quindi utilizzare hello comando toocreate un pacchetto di file jar seguenti:</span><span class="sxs-lookup"><span data-stu-id="eabb0-247">From hello command line in your development environment, change directories toohello location of hello `Streaming` directory, and then use hello following command toocreate a jar package:</span></span>

    ```bash
    mvn clean package
    ```

    <span data-ttu-id="eabb0-248">Questo comando crea una directory denominata `target`, che contiene un file denominato `kafka-streaming-1.0-SNAPSHOT.jar`.</span><span class="sxs-lookup"><span data-stu-id="eabb0-248">This command creates a directory named `target`, which contains a file named `kafka-streaming-1.0-SNAPSHOT.jar`.</span></span>

3. <span data-ttu-id="eabb0-249">Seguente hello utilizzare comandi hello toocopy `kafka-streaming-1.0-SNAPSHOT.jar` cluster HDInsight tooyour di file:</span><span class="sxs-lookup"><span data-stu-id="eabb0-249">Use hello following commands toocopy hello `kafka-streaming-1.0-SNAPSHOT.jar` file tooyour HDInsight cluster:</span></span>
   
    ```bash
    scp ./target/kafka-streaming-1.0-SNAPSHOT.jar SSHUSER@CLUSTERNAME-ssh.azurehdinsight.net:kafka-streaming.jar
    ```
   
    <span data-ttu-id="eabb0-250">Sostituire **SSHUSER** con utente SSH hello per il cluster, quindi sostituire **CLUSTERNAME** con nome hello del cluster.</span><span class="sxs-lookup"><span data-stu-id="eabb0-250">Replace **SSHUSER** with hello SSH user for your cluster, and replace **CLUSTERNAME** with hello name of your cluster.</span></span> <span data-ttu-id="eabb0-251">Quando richiesto immettere la password di hello hello SSH utente.</span><span class="sxs-lookup"><span data-stu-id="eabb0-251">When prompted enter hello password for hello SSH user.</span></span>

4. <span data-ttu-id="eabb0-252">Una volta hello `scp` comando al termine della copia del file hello, connettere il cluster toohello tramite SSH e quindi usare hello successivo comando toocreate hello `wordcounts` argomento:</span><span class="sxs-lookup"><span data-stu-id="eabb0-252">Once hello `scp` command finishes copying hello file, connect toohello cluster using SSH, and then use hello following command toocreate hello `wordcounts` topic:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic wordcounts --zookeeper $KAFKAZKHOSTS
    ```

5. <span data-ttu-id="eabb0-253">Successivamente, avviare hello streaming processo utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="eabb0-253">Next, start hello streaming process by using hello following command:</span></span>
   
    ```bash
    java -jar kafka-streaming.jar $KAFKABROKERS $KAFKAZKHOSTS 2>/dev/null &
    ```
   
    <span data-ttu-id="eabb0-254">Questo comando avvia il flusso di processo in background hello hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-254">This command starts hello streaming process in hello background.</span></span>

6. <span data-ttu-id="eabb0-255">Comando che segue di hello utilizzare toosend messaggi toohello `test` argomento.</span><span class="sxs-lookup"><span data-stu-id="eabb0-255">Use hello following command toosend messages toohello `test` topic.</span></span> <span data-ttu-id="eabb0-256">Questi messaggi vengono elaborati da hello lo streaming di esempio:</span><span class="sxs-lookup"><span data-stu-id="eabb0-256">These messages are processed by hello streaming example:</span></span>
   
    ```bash
    java -jar kafka-producer-consumer.jar producer $KAFKABROKERS &>/dev/null &
    ```

7. <span data-ttu-id="eabb0-257">Hello Usa seguenti output di hello tooview comando che viene scritto toohello `wordcounts` argomento dal processo di streaming hello:</span><span class="sxs-lookup"><span data-stu-id="eabb0-257">Use hello following command tooview hello output that is written toohello `wordcounts` topic by hello streaming process:</span></span>
   
    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --bootstrap-server $KAFKABROKERS --topic wordcounts --from-beginning --formatter kafka.tools.DefaultMessageFormatter --property print.key=true --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer
    ```
   
    > [!NOTE]
    > <span data-ttu-id="eabb0-258">dati hello tooview, è necessario indicare hello consumer tooprint hello chiave e hello deserializzatore toouse per hello chiave e il valore.</span><span class="sxs-lookup"><span data-stu-id="eabb0-258">tooview hello data, you must tell hello consumer tooprint hello key and hello deserializer toouse for hello key and value.</span></span> <span data-ttu-id="eabb0-259">nome della chiave Hello è parola hello e valore di chiave hello contiene il conteggio di hello.</span><span class="sxs-lookup"><span data-stu-id="eabb0-259">hello key name is hello word, and hello key value contains hello count.</span></span>
   
    <span data-ttu-id="eabb0-260">Hello l'output è simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="eabb0-260">hello output is similar toohello following text:</span></span>
   
        dwarfs  13635
        ago     13664
        snow    13636
        dwarfs  13636
        ago     13665
        a       13803
        ago     13666
        a       13804
        ago     13667
        ago     13668
        jumped  13640
        jumped  13641
        a       13805
        snow    13637
   
    > [!NOTE]
    > <span data-ttu-id="eabb0-261">conteggio Hello viene incrementato ogni volta che viene rilevata una parola.</span><span class="sxs-lookup"><span data-stu-id="eabb0-261">hello count increments each time a word is encountered.</span></span>

7. <span data-ttu-id="eabb0-262">Utilizzare hello __Ctrl + C__ tooexit hello consumer, quindi utilizzare hello `fg` comando toobring hello streaming in primo piano toohello indietro delle attività in background.</span><span class="sxs-lookup"><span data-stu-id="eabb0-262">Use hello __Ctrl + C__ tooexit hello consumer, then use hello `fg` command toobring hello streaming background task back toohello foreground.</span></span> <span data-ttu-id="eabb0-263">Utilizzare __Ctrl + C__ tooexit viene anche.</span><span class="sxs-lookup"><span data-stu-id="eabb0-263">Use __Ctrl + C__ tooexit it also.</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="eabb0-264">Eliminare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="eabb0-264">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="eabb0-265">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="eabb0-265">Troubleshoot</span></span>

<span data-ttu-id="eabb0-266">Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="eabb0-266">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="eabb0-267">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eabb0-267">Next steps</span></span>

<span data-ttu-id="eabb0-268">In questo documento, si sono appreso hello nozioni fondamentali sulle operazioni con Apache Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="eabb0-268">In this document, you have learned hello basics of working with Apache Kafka on HDInsight.</span></span> <span data-ttu-id="eabb0-269">Utilizzare hello toolearn più informazioni sull'utilizzo di Kafka seguenti:</span><span class="sxs-lookup"><span data-stu-id="eabb0-269">Use hello following toolearn more about working with Kafka:</span></span>

* [<span data-ttu-id="eabb0-270">Garantire la disponibilità elevata dei dati con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eabb0-270">Ensure high availability of your data with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-high-availability.md)
* [<span data-ttu-id="eabb0-271">Aumentare la scalabilità configurando dischi gestiti con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eabb0-271">Increase scalability by configuring managed disks with Kafka on HDInsight</span></span>](hdinsight-apache-kafka-scalability.md)
* <span data-ttu-id="eabb0-272">[Documentazione di Apache Kafka](http://kafka.apache.org/documentation.html) in kafka.apache.org.</span><span class="sxs-lookup"><span data-stu-id="eabb0-272">[Apache Kafka documentation](http://kafka.apache.org/documentation.html) at kafka.apache.org.</span></span>
* [<span data-ttu-id="eabb0-273">Utilizzare MirrorMaker toocreate una replica di Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eabb0-273">Use MirrorMaker toocreate a replica of Kafka on HDInsight</span></span>](hdinsight-apache-kafka-mirroring.md)
* [<span data-ttu-id="eabb0-274">Usare Apache Storm (anteprima) con Kafka in HDInsight</span><span class="sxs-lookup"><span data-stu-id="eabb0-274">Use Apache Storm with Kafka on HDInsight</span></span>](hdinsight-apache-storm-with-kafka.md)
* <span data-ttu-id="eabb0-275">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md) (Usare Apache Spark con Kafka in HDInsight)</span><span class="sxs-lookup"><span data-stu-id="eabb0-275">[Use Apache Spark with Kafka on HDInsight](hdinsight-apache-spark-with-kafka.md)</span></span>
* [<span data-ttu-id="eabb0-276">Connettersi tooKafka tramite una rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="eabb0-276">Connect tooKafka through an Azure Virtual Network</span></span>](hdinsight-apache-kafka-connect-vpn-gateway.md)
