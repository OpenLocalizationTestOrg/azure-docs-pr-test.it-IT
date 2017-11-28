---
title: aaaUse Kafka Apache con Storm in HDInsight - Azure | Documenti Microsoft
description: Apache Kafka viene installato con Apache Storm in HDInsight. Informazioni su come toowrite tooKafka e quindi leggere da essa, utilizzando hello KafkaBolt e KafkaSpout componenti forniti Storm. E inoltre come toouse hello luminoso framework toodefine e inviare le topologie di Storm.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: e4941329-1580-4cd8-b82e-a2258802c1a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/21/2017
ms.author: larryfr
ms.openlocfilehash: 95701f51dfdf6f1a859dcde96d7053df4f21701f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="d9b3f-105">Usare Apache Kafka (anteprima) con Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d9b3f-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="d9b3f-106">Informazioni su come toouse Apache Storm tooread da e scrittura tooApache Kafka.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-106">Learn how toouse Apache Storm tooread from and write tooApache Kafka.</span></span> <span data-ttu-id="d9b3f-107">Questo esempio viene illustrato come toosave di dati da un toohello topologia Storm compatibile HDFS file di sistema utilizzate da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-107">This example also demonstrates how toosave data from a Storm topology toohello HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="d9b3f-108">procedura di Hello in questo documento consente di creare un gruppo di risorse di Azure che contiene sia una tempesta di HDInsight e un Kafka nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-108">hello steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="d9b3f-109">Questi cluster sono entrambi contenuti all'interno di una rete virtuale di Azure, che consente di hello toodirectly cluster Storm comunicare hello cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-109">These clusters are both located within an Azure Virtual Network, which allows hello Storm cluster toodirectly communicate with hello Kafka cluster.</span></span>
> 
> <span data-ttu-id="d9b3f-110">Al termine con i passaggi di hello in questo documento, tenere presente toodelete hello cluster tooavoid in eccesso addebiti.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-110">When you are done with hello steps in this document, remember toodelete hello clusters tooavoid excess charges.</span></span>

## <a name="get-hello-code"></a><span data-ttu-id="d9b3f-111">Ottenere il codice hello</span><span class="sxs-lookup"><span data-stu-id="d9b3f-111">Get hello code</span></span>

<span data-ttu-id="d9b3f-112">codice Hello ad esempio hello utilizzato in questo documento è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="d9b3f-112">hello code for hello example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="d9b3f-113">toocompile questo progetto, è necessario hello seguente configurazione per l'ambiente di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-113">toocompile this project, you need hello following configuration for your development environment:</span></span>

* <span data-ttu-id="d9b3f-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="d9b3f-115">Per HDInsight 3.5 o una versione successiva è necessario Java 8.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="d9b3f-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="d9b3f-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="d9b3f-117">Un client SSH (è necessario hello `ssh` e `scp` comandi): per informazioni, vedere [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d9b3f-117">An SSH client (you need hello `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="d9b3f-118">Un editor di testo o ambiente IDE.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-118">A text editor or IDE.</span></span>

<span data-ttu-id="d9b3f-119">Hello seguenti variabili di ambiente possono essere impostate durante l'installazione di Java e hello JDK nella workstation di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-119">hello following environment variables may be set when you install Java and hello JDK on your development workstation.</span></span> <span data-ttu-id="d9b3f-120">Tuttavia, è necessario verificare che esistano e che contengono i valori corretti di hello per il sistema.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-120">However, you should check that they exist and that they contain hello correct values for your system.</span></span>

* <span data-ttu-id="d9b3f-121">`JAVA_HOME`-deve puntare toohello directory in cui hello JDK è installato.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-121">`JAVA_HOME` - should point toohello directory where hello JDK is installed.</span></span>
* <span data-ttu-id="d9b3f-122">`PATH`-deve contenere hello seguenti percorsi:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-122">`PATH` - should contain hello following paths:</span></span>
  
    * <span data-ttu-id="d9b3f-123">`JAVA_HOME`(o percorso equivalente hello).</span><span class="sxs-lookup"><span data-stu-id="d9b3f-123">`JAVA_HOME` (or hello equivalent path).</span></span>
    * <span data-ttu-id="d9b3f-124">`JAVA_HOME\bin`(o percorso equivalente hello).</span><span class="sxs-lookup"><span data-stu-id="d9b3f-124">`JAVA_HOME\bin` (or hello equivalent path).</span></span>
    * <span data-ttu-id="d9b3f-125">directory di Hello in cui è installato Maven.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-125">hello directory where Maven is installed.</span></span>

## <a name="create-hello-clusters"></a><span data-ttu-id="d9b3f-126">Creare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="d9b3f-126">Create hello clusters</span></span>

<span data-ttu-id="d9b3f-127">Apache Kafka in HDInsight non forniscono accesso toohello Kafka Broker hello rete internet pubblica.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-127">Apache Kafka on HDInsight does not provide access toohello Kafka brokers over hello public internet.</span></span> <span data-ttu-id="d9b3f-128">Tutto ciò che deve essere tooKafka discussioni hello stessa rete virtuale come nodi di hello hello cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-128">Anything that talks tooKafka must be in hello same Azure virtual network as hello nodes in hello Kafka cluster.</span></span> <span data-ttu-id="d9b3f-129">In questo esempio hello Kafka sia cluster Storm si trovano in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-129">For this example, both hello Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="d9b3f-130">Hello diagramma seguente illustra il flusso delle comunicazioni tra i cluster hello:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-130">hello following diagram shows how communication flows between hello clusters:</span></span>

![Diagramma dei cluster Storm e Kafka in una rete virtuale di Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="d9b3f-132">Ad esempio SSH e Ambari sia accessibile tramite altri servizi in cluster hello hello internet.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-132">Other services on hello cluster such as SSH and Ambari can be accessed over hello internet.</span></span> <span data-ttu-id="d9b3f-133">Per ulteriori informazioni sulle porte pubbliche hello disponibili con HDInsight, vedere [porte e gli URI utilizzato da HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="d9b3f-133">For more information on hello public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="d9b3f-134">È possibile creare una rete virtuale di Azure, Kafka, e Storm cluster manualmente, ma è più facile toouse un modello di gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier toouse an Azure Resource Manager template.</span></span> <span data-ttu-id="d9b3f-135">Utilizzare hello seguenti passaggi viene toodeploy una rete virtuale di Azure, Kafka, e Storm cluster tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-135">Use hello following steps toodeploy an Azure virtual network, Kafka, and Storm clusters tooyour Azure subscription.</span></span>

1. <span data-ttu-id="d9b3f-136">Utilizzare hello seguente pulsante toosign in tooAzure e modello hello Apri nel portale di Azure hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-136">Use hello following button toosign in tooAzure and open hello template in hello Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy tooAzure"></a>
   
    <span data-ttu-id="d9b3f-137">Hello Azure Resource Manager modello si trova in **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-137">hello Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="d9b3f-138">Crea hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-138">It creates hello following resources:</span></span>
    
    * <span data-ttu-id="d9b3f-139">Gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="d9b3f-139">Azure resource group</span></span>
    * <span data-ttu-id="d9b3f-140">Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="d9b3f-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="d9b3f-141">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d9b3f-141">Azure Storage account</span></span>
    * <span data-ttu-id="d9b3f-142">Kafka in HDInsight versione 3.6 con tre nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="d9b3f-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="d9b3f-143">Storm in HDInsight versione 3.6 con tre nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="d9b3f-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="d9b3f-144">disponibilità tooguarantee Kafka in HDInsight, il cluster deve contenere almeno tre nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-144">tooguarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="d9b3f-145">Questo modello crea un cluster Kafka contenente tre nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="d9b3f-146">Hello utilizzare seguendo le voci di informazioni aggiuntive toopopulate hello hello **distribuzione personalizzata** pannello:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-146">Use hello following guidance toopopulate hello entries on hello **Custom deployment** blade:</span></span>
   
    ![Distribuzione personalizzata di HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="d9b3f-148">**Gruppo di risorse**: creare un gruppo o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="d9b3f-149">Questo gruppo contiene cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-149">This group contains hello HDInsight cluster.</span></span>
   
    * <span data-ttu-id="d9b3f-150">**Percorso**: selezionare un tooyou geograficamente Chiudi percorso.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-150">**Location**: Select a location geographically close tooyou.</span></span>

    * <span data-ttu-id="d9b3f-151">**Nome del Cluster di base**: questo valore viene utilizzato come nome di base per i cluster Storm e Kafka hello hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-151">**Base Cluster Name**: This value is used as hello base name for hello Storm and Kafka clusters.</span></span> <span data-ttu-id="d9b3f-152">Ad esempio, se si immette **hdi** viene creato un cluster Storm denominato **storm-hdi** e un cluster Kafka denominato **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="d9b3f-153">**Nome utente di accesso del cluster**: nome utente amministratore di hello per i cluster Storm e Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-153">**Cluster Login User Name**: hello admin user name for hello Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="d9b3f-154">**Password di account di accesso cluster**: password dell'utente per i cluster Storm e Kafka hello hello admin.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-154">**Cluster Login Password**: hello admin user password for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="d9b3f-155">**Nome utente SSH**: hello toocreate utente SSH per i cluster Storm e Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-155">**SSH User Name**: hello SSH user toocreate for hello Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="d9b3f-156">**Password SSH**: password hello per utente SSH hello per i cluster Storm e Kafka hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-156">**SSH Password**: hello password for hello SSH user for hello Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="d9b3f-157">Hello lettura **termini e condizioni**, quindi selezionare **accetto le condizioni indicate in precedenza toohello**.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-157">Read hello **Terms and Conditions**, and then select **I agree toohello terms and conditions stated above**.</span></span>

4. <span data-ttu-id="d9b3f-158">Infine, controllare **Pin toodashboard** e quindi selezionare **acquisto**.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-158">Finally, check **Pin toodashboard** and then select **Purchase**.</span></span> <span data-ttu-id="d9b3f-159">Sono necessari circa 20 minuti toocreate cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-159">It takes about 20 minutes toocreate hello clusters.</span></span>

<span data-ttu-id="d9b3f-160">Dopo avere create le risorse di hello, viene visualizzato il pannello hello per il gruppo di risorse hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-160">Once hello resources have been created, hello blade for hello resource group is displayed.</span></span>

![Pannello di gruppo di risorse per la rete virtuale hello e cluster](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="d9b3f-162">Si noti che sono nomi hello dei cluster HDInsight hello **storm BASENAME** e **kafka BASENAME**, dove BASENAME è nome hello toohello modello specificato.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-162">Notice that hello names of hello HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is hello name you provided toohello template.</span></span> <span data-ttu-id="d9b3f-163">Utilizzare questi nomi nei passaggi successivi per la connessione toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-163">You use these names in later steps when connecting toohello clusters.</span></span>

## <a name="understanding-hello-code"></a><span data-ttu-id="d9b3f-164">Informazioni sul codice hello</span><span class="sxs-lookup"><span data-stu-id="d9b3f-164">Understanding hello code</span></span>

<span data-ttu-id="d9b3f-165">Questo progetto contiene due topologie:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-165">This project contains two topologies:</span></span>

* <span data-ttu-id="d9b3f-166">**KafkaWriter**: definito da hello **writer.yaml** file, questa topologia scrive tooKafka frasi casuale usando hello KafkaBolt fornito con Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-166">**KafkaWriter**: Defined by hello **writer.yaml** file, this topology writes random sentences tooKafka using hello KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="d9b3f-167">Questa topologia viene utilizzato un oggetto personalizzato **SentenceSpout** frasi casuale toogenerate di componente.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-167">This topology uses a custom **SentenceSpout** component toogenerate random sentences.</span></span>

* <span data-ttu-id="d9b3f-168">**KafkaReader**: definito da hello **reader.yaml** file, questa topologia legge i dati da Kafka utilizzando hello KafkaSpout fornito con Apache Storm quindi registri hello toostdout di dati.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-168">**KafkaReader**: Defined by hello **reader.yaml** file, this topology reads data from Kafka using hello KafkaSpout provided with Apache Storm, then logs hello data toostdout.</span></span>

    <span data-ttu-id="d9b3f-169">Questa topologia utilizza l'archiviazione toodefault hello Storm HdfsBolt toowrite dati per i cluster Storm hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-169">This topology uses hello Storm HdfsBolt toowrite data toodefault storage for hello Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="d9b3f-170">Flux</span><span class="sxs-lookup"><span data-stu-id="d9b3f-170">Flux</span></span>

<span data-ttu-id="d9b3f-171">topologie di Hello vengono definite utilizzando [flusso](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="d9b3f-171">hello topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="d9b3f-172">Flusso è stato introdotto in Storm 0.10 e consente di configurazione della topologia hello tooseparate dal codice hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-172">Flux was introduced in Storm 0.10.x and allows you tooseparate hello topology configuration from hello code.</span></span> <span data-ttu-id="d9b3f-173">Per le topologie che usano framework luminoso hello, topologia hello è definita in un file YAML.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-173">For Topologies that use hello Flux framework, hello topology is defined in a YAML file.</span></span> <span data-ttu-id="d9b3f-174">file YAML Hello può essere incluso come parte della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-174">hello YAML file can be included as part of hello topology.</span></span> <span data-ttu-id="d9b3f-175">Può essere anche un file autonomo utilizzato quando si invia la topologia hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-175">It can also be a standalone file used when you submit hello topology.</span></span> <span data-ttu-id="d9b3f-176">Flux supporta anche la sostituzione delle variabili in fase di esecuzione, caratteristica che viene usata in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="d9b3f-177">i seguenti parametri Hello vengono impostati in fase di esecuzione per queste topologie:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-177">hello following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="d9b3f-178">`${kafka.topic}`: nome hello di hello Kafka argomento topologie hello lettura/scrittura a.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-178">`${kafka.topic}`: hello name of hello Kafka topic that hello topologies read/write to.</span></span>

* <span data-ttu-id="d9b3f-179">`${kafka.broker.hosts}`: hello ospita tale hello Kafka di connessione eseguito.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-179">`${kafka.broker.hosts}`: hello hosts that hello Kafka brokers run on.</span></span> <span data-ttu-id="d9b3f-180">informazioni di Service broker Hello viene utilizzate dalle hello KafkaBolt tooKafka di scrittura.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-180">hello broker information is used by hello KafkaBolt when writing tooKafka.</span></span>

* <span data-ttu-id="d9b3f-181">`${kafka.zookeeper.hosts}`: host hello in esecuzione Zookeeper in hello cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-181">`${kafka.zookeeper.hosts}`: hello hosts that Zookeeper runs on in hello Kafka cluster.</span></span>

<span data-ttu-id="d9b3f-182">Per altre informazioni sulle topologie di Flux, vedere [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="d9b3f-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-hello-project"></a><span data-ttu-id="d9b3f-183">Scaricare e compilare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="d9b3f-183">Download and compile hello project</span></span>

1. <span data-ttu-id="d9b3f-184">In ambiente di sviluppo, scaricare il progetto hello da [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), aprire una riga di comando e modificare le directory toohello percorso sia stato scaricato il progetto hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-184">On your development environment, download hello project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories toohello location that you downloaded hello project.</span></span>

2. <span data-ttu-id="d9b3f-185">Da hello **hdinsight-storm-java-kafka** directory seguenti hello utilizzare comandi progetto hello toocompile e creare un pacchetto per la distribuzione:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-185">From hello **hdinsight-storm-java-kafka** directory, use hello following command toocompile hello project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="d9b3f-186">processo del pacchetto Hello crea un file denominato `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-186">hello package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in hello `target` directory.</span></span>

3. <span data-ttu-id="d9b3f-187">Utilizzare hello seguenti comandi toocopy hello pacchetto tooyour Storm nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-187">Use hello following commands toocopy hello package tooyour Storm on HDInsight cluster.</span></span> <span data-ttu-id="d9b3f-188">Sostituire **USERNAME** con nome utente di hello SSH per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-188">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="d9b3f-189">Sostituire **BASENAME** con nome base hello utilizzato per la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-189">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="d9b3f-190">Quando richiesto, immettere la password di hello utilizzati durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-190">When prompted, enter hello password you used when creating hello clusters.</span></span>

## <a name="configure-hello-topology"></a><span data-ttu-id="d9b3f-191">Configurare la topologia di hello</span><span class="sxs-lookup"><span data-stu-id="d9b3f-191">Configure hello topology</span></span>

1. <span data-ttu-id="d9b3f-192">Utilizzare uno dei seguenti metodi toodiscover hello hello host di Service broker Kafka:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-192">Use one of hello following methods toodiscover hello Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/KAFKA/components/KAFKA_BROKER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $brokerHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($brokerHosts -join ":9092,") + ":9092"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/KAFKA/components/KAFKA_BROKER" | jq -r '["\(.host_components[].HostRoles.host_name):9092"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="d9b3f-193">Hello Bash esempio si presuppone che `$CLUSTERNAME` contiene il nome di hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-193">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="d9b3f-194">Presuppone anche che [jq](https://stedolan.github.io/jq/) sia installato.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="d9b3f-195">Quando richiesto, immettere la password di hello per account di accesso cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-195">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="d9b3f-196">il valore di Hello restituito è simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-196">hello value returned is similar toohello following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="d9b3f-197">Anche se possono essere presenti più di due host di Service broker per il cluster, non è necessario un elenco completo di tutti gli host tooclients tooprovide.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-197">While there may be more than two broker hosts for your cluster, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="d9b3f-198">È sufficiente specificarne uno o due.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-198">One or two is enough.</span></span>

2. <span data-ttu-id="d9b3f-199">Utilizzare uno dei seguenti host Kafka Zookeeper di metodi toodiscover hello hello:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-199">Use one of hello following methods toodiscover hello Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $clusterName = Read-Host -Prompt "Enter hello Kafka cluster name"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" `
        -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $zookeeperHosts = $respObj.host_components.HostRoles.host_name[0..1]
    ($zookeeperHosts -join ":2181,") + ":2181"
    ```

    ```bash
    curl -su admin -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/ZOOKEEPER/components/ZOOKEEPER_SERVER" | jq -r '["\(.host_components[].HostRoles.host_name):2181"] | join(",")' | cut -d',' -f1,2
    ```

    > [!IMPORTANT]
    > <span data-ttu-id="d9b3f-200">Hello Bash esempio si presuppone che `$CLUSTERNAME` contiene il nome di hello del cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-200">hello Bash example assumes that `$CLUSTERNAME` contains hello name of hello HDInsight cluster.</span></span> <span data-ttu-id="d9b3f-201">Presuppone anche che [jq](https://stedolan.github.io/jq/) sia installato.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="d9b3f-202">Quando richiesto, immettere la password di hello per account di accesso cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-202">When prompted, enter hello password for hello cluster login account.</span></span>

    <span data-ttu-id="d9b3f-203">il valore di Hello restituito è simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-203">hello value returned is similar toohello following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="d9b3f-204">Anche se sono presenti più di due nodi Zookeeper, non è necessario un elenco completo di tutti gli host tooclients tooprovide.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-204">While there are more than two Zookeeper nodes, you do not need tooprovide a full list of all hosts tooclients.</span></span> <span data-ttu-id="d9b3f-205">È sufficiente specificarne uno o due.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-205">One or two is enough.</span></span>

    <span data-ttu-id="d9b3f-206">Salvare questo valore, che verrà usato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="d9b3f-207">Modifica hello `dev.properties` file nella directory radice del progetto hello hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-207">Edit hello `dev.properties` file in hello root of hello project.</span></span> <span data-ttu-id="d9b3f-208">Aggiungere hello Broker e righe corrispondenti toohello Zookeeper host informazioni in questo file.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-208">Add hello Broker and Zookeeper hosts information toohello matching lines in this file.</span></span> <span data-ttu-id="d9b3f-209">Hello esempio seguente viene configurata utilizzando i valori di esempio hello nei passaggi precedenti hello:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-209">hello following example is configured using hello sample values from hello previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="d9b3f-210">Salvare hello `dev.properties` file, quindi utilizzare hello seguenti comando tooupload il cluster Storm toohello:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-210">Save hello `dev.properties` file and then use hello following command tooupload it toohello Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="d9b3f-211">Sostituire **USERNAME** con nome utente di hello SSH per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-211">Replace **USERNAME** with hello SSH user name for hello cluster.</span></span> <span data-ttu-id="d9b3f-212">Sostituire **BASENAME** con nome base hello utilizzato per la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-212">Replace **BASENAME** with hello base name you used when creating hello cluster.</span></span>

## <a name="start-hello-writer"></a><span data-ttu-id="d9b3f-213">Avvio del writer hello</span><span class="sxs-lookup"><span data-stu-id="d9b3f-213">Start hello writer</span></span>

1. <span data-ttu-id="d9b3f-214">Utilizzare hello seguente cluster Storm di toohello tooconnect tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-214">Use hello following tooconnect toohello Storm cluster using SSH.</span></span> <span data-ttu-id="d9b3f-215">Sostituire **USERNAME** con nome dell'utente SSH hello utilizzato durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-215">Replace **USERNAME** with hello SSH user name used when creating hello cluster.</span></span> <span data-ttu-id="d9b3f-216">Sostituire **BASENAME** con il nome di base hello utilizzato durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-216">Replace **BASENAME** with hello base name used when creating hello cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="d9b3f-217">Quando richiesto, immettere la password di hello utilizzati durante la creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-217">When prompted, enter hello password you used when creating hello clusters.</span></span>
   
    <span data-ttu-id="d9b3f-218">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="d9b3f-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="d9b3f-219">Da hello connessione SSH, utilizzare hello comando toocreate hello argomento Kafka utilizzato dalla topologia hello seguente:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-219">From hello SSH connection, use hello following command toocreate hello Kafka topic used by hello topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="d9b3f-220">Sostituire `$KAFKAZKHOSTS` con hello Zookeeper recuperato nella sezione precedente hello informazioni sull'host.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-220">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

2. <span data-ttu-id="d9b3f-221">Da cluster Storm toohello di connessione SSH di hello, utilizzare hello topologia writer hello toostart di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-221">From hello SSH connection toohello Storm cluster, use hello following command toostart hello writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="d9b3f-222">Hello parametri utilizzati con questo comando sono:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-222">hello parameters used with this command are:</span></span>

    * <span data-ttu-id="d9b3f-223">`org.apache.storm.flux.Flux`: Utilizzare luminoso tooconfigure ed eseguire questa topologia.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-223">`org.apache.storm.flux.Flux`: Use Flux tooconfigure and run this topology.</span></span>

    * <span data-ttu-id="d9b3f-224">`--remote`: Inviare tooNimbus topologia hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-224">`--remote`: Submit hello topology tooNimbus.</span></span> <span data-ttu-id="d9b3f-225">topologia Hello viene distribuita tra i nodi di lavoro hello cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-225">hello topology is distributed across hello worker nodes in hello cluster.</span></span>

    * <span data-ttu-id="d9b3f-226">`-R /writer.yaml`: Hello utilizzare `writer.yaml` topologia hello tooconfigure del file.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-226">`-R /writer.yaml`: Use hello `writer.yaml` file tooconfigure hello topology.</span></span> <span data-ttu-id="d9b3f-227">`-R`indica che la risorsa è incluso nel file jar hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-227">`-R` indicates that this resource is included in hello jar file.</span></span> <span data-ttu-id="d9b3f-228">È pertanto nella directory radice del file jar hello, hello `/writer.yaml` è tooit percorso hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-228">It's in hello root of hello jar, so `/writer.yaml` is hello path tooit.</span></span>

    * <span data-ttu-id="d9b3f-229">`--filter`: Consente di popolare i hello `writer.yaml` topologia utilizzando valori hello `dev.properties` file.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-229">`--filter`: Populate entries in hello `writer.yaml` topology using values in hello `dev.properties` file.</span></span> <span data-ttu-id="d9b3f-230">Ad esempio, hello valore hello `kafka.topic` voce nel file hello è hello tooreplace utilizzati `${kafka.topic}` voce nella definizione della topologia hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-230">For example, hello value of hello `kafka.topic` entry in hello file is used tooreplace hello `${kafka.topic}` entry in hello topology definition.</span></span>

5. <span data-ttu-id="d9b3f-231">Una volta avviata la topologia hello, utilizzare hello tooverify comando scrive dati toohello argomento Kafka seguenti:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-231">Once hello topology has started, use hello following command tooverify that it is writing data toohello Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="d9b3f-232">Sostituire `$KAFKAZKHOSTS` con hello Zookeeper recuperato nella sezione precedente hello informazioni sull'host.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-232">Replace `$KAFKAZKHOSTS` with hello Zookeeper host information you retrieved in hello previous section.</span></span>

    <span data-ttu-id="d9b3f-233">Questo comando Usa uno script fornito con l'argomento di hello toomonitor Kafka.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-233">This command uses a script shipped with Kafka toomonitor hello topic.</span></span> <span data-ttu-id="d9b3f-234">Dopo qualche istante, deve iniziare restituzione casuale frasi che sono stati scritti toohello argomento.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-234">After a moment, it should start returning random sentences that have been written toohello topic.</span></span> <span data-ttu-id="d9b3f-235">Hello l'output è simile toohello seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-235">hello output is similar toohello following example:</span></span>

        i am at two with nature             
        an apple a day keeps hello doctor away
        snow white and hello seven dwarfs     
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        hello cow jumped over hello moon        
        an apple a day keeps hello doctor away
        an apple a day keeps hello doctor away
        four score and seven years ago      
        snow white and hello seven dwarfs     
        snow white and hello seven dwarfs     
        i am at two with nature             
        an apple a day keeps hello doctor away

    <span data-ttu-id="d9b3f-236">Utilizzare Ctrl + script hello toostop c.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-236">Use Ctrl+c toostop hello script.</span></span>

## <a name="start-hello-reader"></a><span data-ttu-id="d9b3f-237">Avviare il lettore hello</span><span class="sxs-lookup"><span data-stu-id="d9b3f-237">Start hello reader</span></span>

1. <span data-ttu-id="d9b3f-238">Da cluster hello SSH sessione toohello Storm utilizzare hello topologia lettore hello toostart di comando seguente:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-238">From hello SSH session toohello Storm cluster, use hello following command toostart hello reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="d9b3f-239">Una volta avviata la topologia hello, aprire hello Storm UI.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-239">Once hello topology starts, open hello Storm UI.</span></span> <span data-ttu-id="d9b3f-240">Questa interfaccia utente Web è disponibile all'indirizzo https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="d9b3f-241">Sostituire __BASENAME__ con il nome di base hello utilizzato al momento della creazione di cluster hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-241">Replace __BASENAME__ with hello base name used when hello cluster was created.</span></span> 

    <span data-ttu-id="d9b3f-242">Quando richiesto, utilizzare nome account di accesso di amministratore hello (impostazione predefinita, `admin`) e la password utilizzati quando è stato creato il cluster di hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-242">When prompted, use hello admin login name (default, `admin`) and password used when hello cluster was created.</span></span> <span data-ttu-id="d9b3f-243">Viene visualizzato un toohello simile a pagina web seguente immagine:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-243">You see a web page similar toohello following image:</span></span>

    ![Interfaccia utente di Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="d9b3f-245">Dall'interfaccia utente di Storm hello, selezionare hello __kafka lettore__ collegamento hello __topologia riepilogo__ sezione toodisplay informazioni hello __kafka lettore__ topologia.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-245">From hello Storm UI, select hello __kafka-reader__ link in hello __Topology Summary__ section toodisplay information about hello __kafka-reader__ topology.</span></span>

    ![Nella sezione Riepilogo della topologia dell'interfaccia utente web di Storm hello](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="d9b3f-247">toodisplay informazioni sulle istanze di hello del componente di logger fulmine hello, seleziona hello __logger fulmine__ collegamento hello __bulloni (tutto il tempo)__ sezione.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-247">toodisplay information about hello instances of hello logger-bolt component, select hello __logger-bolt__ link in hello __Bolts (All time)__ section.</span></span>

    ![Logger fulmine collegamento nella sezione bulloni hello](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="d9b3f-249">In hello __executor__ , selezionare un collegamento in hello __porta__ registrazione toodisplay colonna informazioni su questa istanza del componente hello.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-249">In hello __Executors__ section, select a link in hello __Port__ column toodisplay logging information about this instance of hello component.</span></span>

    ![Collegamento esecutori](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="d9b3f-251">log Hello contiene un registro dei dati di hello letti da hello argomento Kafka.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-251">hello log contains a log of hello data read from hello Kafka topic.</span></span> <span data-ttu-id="d9b3f-252">informazioni Hello nel registro hello sono simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-252">hello information in hello log is similar toohello following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] hello cow jumped over hello moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: hello cow jumped over hello moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and hello seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and hello seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps hello doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps hello doctor away

## <a name="stop-hello-topologies"></a><span data-ttu-id="d9b3f-253">Arrestare le topologie di hello</span><span class="sxs-lookup"><span data-stu-id="d9b3f-253">Stop hello topologies</span></span>

<span data-ttu-id="d9b3f-254">Da un cluster Storm toohello sessione SSH, utilizzare hello topologie di Storm hello toostop i comandi seguenti:</span><span class="sxs-lookup"><span data-stu-id="d9b3f-254">From an SSH session toohello Storm cluster, use hello following commands toostop hello Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-hello-cluster"></a><span data-ttu-id="d9b3f-255">Eliminare il cluster hello</span><span class="sxs-lookup"><span data-stu-id="d9b3f-255">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="d9b3f-256">Poiché i passaggi di hello in questo documento crea entrambi i cluster in hello nello stesso gruppo di risorse di Azure, è possibile eliminare il gruppo di risorse hello in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-256">Since hello steps in this document create both clusters in hello same Azure resource group, you can delete hello resource group in hello Azure portal.</span></span> <span data-ttu-id="d9b3f-257">Eliminazione gruppo di risorse hello rimuove tutte le risorse create seguendo questo documento.</span><span class="sxs-lookup"><span data-stu-id="d9b3f-257">Deleting hello resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="d9b3f-258">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d9b3f-258">Next steps</span></span>

<span data-ttu-id="d9b3f-259">Per altri esempi di topologie che possono essere usate con Storm in HDInsight, vedere [Esempi di topologie e componenti Storm per Apache Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="d9b3f-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="d9b3f-260">Per informazioni sulla distribuzione e sul monitoraggio di topologie in HDInsight basato su Linux, vedere [Distribuzione e gestione di topologie Apache Storm in HDInsight basato su Linux](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="d9b3f-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>