---
title: Usare Apache Kafka con Storm in HDInsight di Azure | Microsoft Docs
description: Apache Kafka viene installato con Apache Storm in HDInsight. Informazioni su come scrivere in Kafka e leggere da Kafka usando componenti KafkaBolt e KafkaSpout forniti con Storm. Informazioni su come usare il framework Flux per definire e inviare topologie di Storm.
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
ms.openlocfilehash: e8895ef3c11aea48513e4060a20f5f49b11fc961
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="use-apache-kafka-preview-with-storm-on-hdinsight"></a><span data-ttu-id="e6723-105">Usare Apache Kafka (anteprima) con Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="e6723-105">Use Apache Kafka (preview) with Storm on HDInsight</span></span>

<span data-ttu-id="e6723-106">Informazioni su come usare Apache Storm per leggere e scrivere in Apache Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-106">Learn how to use Apache Storm to read from and write to Apache Kafka.</span></span> <span data-ttu-id="e6723-107">Questo esempio illustra anche come salvare i dati da una topologia di Storm nel file system compatibile con HDFS usato da HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6723-107">This example also demonstrates how to save data from a Storm topology to the HDFS-compatible file system used by HDInsight.</span></span>

> [!NOTE]
> <span data-ttu-id="e6723-108">La procedura descritta in questo documento permette di creare un gruppo di risorse di Azure che contiene sia un cluster Storm in HDInsight che un cluster Kafka in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6723-108">The steps in this document create an Azure resource group that contains both a Storm on HDInsight and a Kafka on HDInsight cluster.</span></span> <span data-ttu-id="e6723-109">Entrambi questi cluster si trovano all'interno di una rete virtuale di Azure, che consente al cluster Storm di comunicare direttamente con il cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-109">These clusters are both located within an Azure Virtual Network, which allows the Storm cluster to directly communicate with the Kafka cluster.</span></span>
> 
> <span data-ttu-id="e6723-110">Al termine della procedura descritta in questo documento, eliminare i cluster per evitare costi supplementari.</span><span class="sxs-lookup"><span data-stu-id="e6723-110">When you are done with the steps in this document, remember to delete the clusters to avoid excess charges.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="e6723-111">Ottenere il codice</span><span class="sxs-lookup"><span data-stu-id="e6723-111">Get the code</span></span>

<span data-ttu-id="e6723-112">Il codice per l'esempio usato in questo documento è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span><span class="sxs-lookup"><span data-stu-id="e6723-112">The code for the example used in this document is available at [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka).</span></span>

<span data-ttu-id="e6723-113">Per compilare questo progetto, è necessaria la seguente configurazione per l'ambiente di sviluppo:</span><span class="sxs-lookup"><span data-stu-id="e6723-113">To compile this project, you need the following configuration for your development environment:</span></span>

* <span data-ttu-id="e6723-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="e6723-114">[Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) or higher.</span></span> <span data-ttu-id="e6723-115">Per HDInsight 3.5 o una versione successiva è necessario Java 8.</span><span class="sxs-lookup"><span data-stu-id="e6723-115">HDInsight 3.5 or higher require Java 8.</span></span>

* [<span data-ttu-id="e6723-116">Maven 3.x</span><span class="sxs-lookup"><span data-stu-id="e6723-116">Maven 3.x</span></span>](https://maven.apache.org/download.cgi)

* <span data-ttu-id="e6723-117">Un client SSH (sono necessari i comandi `ssh` e `scp`). Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e6723-117">An SSH client (you need the `ssh` and `scp` commands) - For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

* <span data-ttu-id="e6723-118">Un editor di testo o ambiente IDE.</span><span class="sxs-lookup"><span data-stu-id="e6723-118">A text editor or IDE.</span></span>

<span data-ttu-id="e6723-119">Le variabili di ambiente seguenti possono essere impostate quando si installa Java e l'JDK nella workstation di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="e6723-119">The following environment variables may be set when you install Java and the JDK on your development workstation.</span></span> <span data-ttu-id="e6723-120">È tuttavia necessario verificare che esistano e che contengano i valori corretti per il sistema in uso.</span><span class="sxs-lookup"><span data-stu-id="e6723-120">However, you should check that they exist and that they contain the correct values for your system.</span></span>

* <span data-ttu-id="e6723-121">`JAVA_HOME` - deve puntare alla directory dove è installato JDK.</span><span class="sxs-lookup"><span data-stu-id="e6723-121">`JAVA_HOME` - should point to the directory where the JDK is installed.</span></span>
* <span data-ttu-id="e6723-122">`PATH`: deve contenere i percorsi seguenti:</span><span class="sxs-lookup"><span data-stu-id="e6723-122">`PATH` - should contain the following paths:</span></span>
  
    * <span data-ttu-id="e6723-123">`JAVA_HOME` o il percorso equivalente.</span><span class="sxs-lookup"><span data-stu-id="e6723-123">`JAVA_HOME` (or the equivalent path).</span></span>
    * <span data-ttu-id="e6723-124">`JAVA_HOME\bin` o il percorso equivalente.</span><span class="sxs-lookup"><span data-stu-id="e6723-124">`JAVA_HOME\bin` (or the equivalent path).</span></span>
    * <span data-ttu-id="e6723-125">Directory in cui è installato Maven.</span><span class="sxs-lookup"><span data-stu-id="e6723-125">The directory where Maven is installed.</span></span>

## <a name="create-the-clusters"></a><span data-ttu-id="e6723-126">Creare i cluster</span><span class="sxs-lookup"><span data-stu-id="e6723-126">Create the clusters</span></span>

<span data-ttu-id="e6723-127">Apache Kafka in HDInsight non fornisce l'accesso ai broker Kafka tramite Internet pubblico.</span><span class="sxs-lookup"><span data-stu-id="e6723-127">Apache Kafka on HDInsight does not provide access to the Kafka brokers over the public internet.</span></span> <span data-ttu-id="e6723-128">Tutto ciò che comunica con Kafka deve trovarsi nella stessa rete virtuale di Azure dei nodi del cluster Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-128">Anything that talks to Kafka must be in the same Azure virtual network as the nodes in the Kafka cluster.</span></span> <span data-ttu-id="e6723-129">Per questo esempio, i cluster Storm e Kafka si trovano entrambi in una rete virtuale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6723-129">For this example, both the Kafka and Storm clusters are located in an Azure virtual network.</span></span> <span data-ttu-id="e6723-130">Il diagramma seguente illustra il flusso delle comunicazioni tra i cluster:</span><span class="sxs-lookup"><span data-stu-id="e6723-130">The following diagram shows how communication flows between the clusters:</span></span>

![Diagramma dei cluster Storm e Kafka in una rete virtuale di Azure](./media/hdinsight-apache-storm-with-kafka/storm-kafka-vnet.png)

> [!NOTE]
> <span data-ttu-id="e6723-132">Altri servizi nel cluster, ad esempio SSH e Ambari, sono accessibili tramite Internet.</span><span class="sxs-lookup"><span data-stu-id="e6723-132">Other services on the cluster such as SSH and Ambari can be accessed over the internet.</span></span> <span data-ttu-id="e6723-133">Per altre informazioni sulle porte pubbliche disponibili con HDInsight, vedere [Porte e URI usati da HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span><span class="sxs-lookup"><span data-stu-id="e6723-133">For more information on the public ports available with HDInsight, see [Ports and URIs used by HDInsight](hdinsight-hadoop-port-settings-for-services.md).</span></span>

<span data-ttu-id="e6723-134">Anche se è possibile creare manualmente cluster Storm e Kafka e una rete virtuale di Azure, è più semplice usare un modello di Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e6723-134">While you can create an Azure virtual network, Kafka, and Storm clusters manually, it's easier to use an Azure Resource Manager template.</span></span> <span data-ttu-id="e6723-135">Seguire questa procedura per distribuire cluster Storm e Kafka e una rete virtuale di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6723-135">Use the following steps to deploy an Azure virtual network, Kafka, and Storm clusters to your Azure subscription.</span></span>

1. <span data-ttu-id="e6723-136">Usare il pulsante seguente per accedere ad Azure e aprire il modello nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6723-136">Use the following button to sign in to Azure and open the template in the Azure portal.</span></span>
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-kafka-storm-cluster-in-vnet-v2.json" target="_blank"><img src="./media/hdinsight-apache-storm-with-kafka/deploy-to-azure.png" alt="Deploy to Azure"></a>
   
    <span data-ttu-id="e6723-137">Il modello di Azure Resource Manager è disponibile all'indirizzo **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span><span class="sxs-lookup"><span data-stu-id="e6723-137">The Azure Resource Manager template is located at **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-kafka-storm-cluster-in-vnet-v1.json**.</span></span> <span data-ttu-id="e6723-138">Crea le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="e6723-138">It creates the following resources:</span></span>
    
    * <span data-ttu-id="e6723-139">Gruppo di risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="e6723-139">Azure resource group</span></span>
    * <span data-ttu-id="e6723-140">Rete virtuale di Azure</span><span class="sxs-lookup"><span data-stu-id="e6723-140">Azure Virtual Network</span></span>
    * <span data-ttu-id="e6723-141">Account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="e6723-141">Azure Storage account</span></span>
    * <span data-ttu-id="e6723-142">Kafka in HDInsight versione 3.6 con tre nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="e6723-142">Kafka on HDInsight version 3.6 (three worker nodes)</span></span>
    * <span data-ttu-id="e6723-143">Storm in HDInsight versione 3.6 con tre nodi di lavoro</span><span class="sxs-lookup"><span data-stu-id="e6723-143">Storm on HDInsight version 3.6 (three worker nodes)</span></span>

  > [!WARNING]
  > <span data-ttu-id="e6723-144">Per garantire la disponibilità di Kafka in HDInsight, il cluster deve contenere almeno tre nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e6723-144">To guarantee availability of Kafka on HDInsight, your cluster must contain at least three worker nodes.</span></span> <span data-ttu-id="e6723-145">Questo modello crea un cluster Kafka contenente tre nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e6723-145">This template creates a Kafka cluster that contains three worker nodes.</span></span>

2. <span data-ttu-id="e6723-146">Usare le linee guida seguenti per popolare le voci nel pannello **Distribuzione personalizzata**:</span><span class="sxs-lookup"><span data-stu-id="e6723-146">Use the following guidance to populate the entries on the **Custom deployment** blade:</span></span>
   
    ![Distribuzione personalizzata di HDInsight](./media/hdinsight-apache-storm-with-kafka/parameters.png)

    * <span data-ttu-id="e6723-148">**Gruppo di risorse**: creare un gruppo o selezionarne uno esistente.</span><span class="sxs-lookup"><span data-stu-id="e6723-148">**Resource group**: Create a group or select an existing one.</span></span> <span data-ttu-id="e6723-149">Questo gruppo contiene il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6723-149">This group contains the HDInsight cluster.</span></span>
   
    * <span data-ttu-id="e6723-150">**Località**: scegliere una località geograficamente vicina.</span><span class="sxs-lookup"><span data-stu-id="e6723-150">**Location**: Select a location geographically close to you.</span></span>

    * <span data-ttu-id="e6723-151">**Base Cluster Name** (Nome di base del cluster): questo valore viene usato come nome di base per i cluster Storm e Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-151">**Base Cluster Name**: This value is used as the base name for the Storm and Kafka clusters.</span></span> <span data-ttu-id="e6723-152">Ad esempio, se si immette **hdi** viene creato un cluster Storm denominato **storm-hdi** e un cluster Kafka denominato **kafka-hdi**.</span><span class="sxs-lookup"><span data-stu-id="e6723-152">For example, entering **hdi** creates a Storm cluster named **storm-hdi** and a Kafka cluster named **kafka-hdi**.</span></span>
   
    * <span data-ttu-id="e6723-153">**Cluster Login User Name** (Nome utente di accesso del cluster): nome utente amministratore per i cluster Storm e Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-153">**Cluster Login User Name**: The admin user name for the Storm and Kafka clusters.</span></span>
   
    * <span data-ttu-id="e6723-154">**Cluster Login Password** (Password di accesso del cluster): password amministratore per i cluster Storm e Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-154">**Cluster Login Password**: The admin user password for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="e6723-155">**SSH User Name** (Nome utente SSH): utente SSH da creare per i cluster Storm e Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-155">**SSH User Name**: The SSH user to create for the Storm and Kafka clusters.</span></span>
    
    * <span data-ttu-id="e6723-156">**SSH Password** (Password SSH): password dell'utente SSH per i cluster Storm e Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-156">**SSH Password**: The password for the SSH user for the Storm and Kafka clusters.</span></span>

3. <span data-ttu-id="e6723-157">Leggere le **Condizioni** e quindi selezionare **Accetto le condizioni riportate sopra**.</span><span class="sxs-lookup"><span data-stu-id="e6723-157">Read the **Terms and Conditions**, and then select **I agree to the terms and conditions stated above**.</span></span>

4. <span data-ttu-id="e6723-158">Selezionare infine **Aggiungi al dashboard** e quindi **Acquista**.</span><span class="sxs-lookup"><span data-stu-id="e6723-158">Finally, check **Pin to dashboard** and then select **Purchase**.</span></span> <span data-ttu-id="e6723-159">La creazione dei cluster richiede circa 20 minuti.</span><span class="sxs-lookup"><span data-stu-id="e6723-159">It takes about 20 minutes to create the clusters.</span></span>

<span data-ttu-id="e6723-160">Dopo avere creato le risorse, viene visualizzato il pannello del gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="e6723-160">Once the resources have been created, the blade for the resource group is displayed.</span></span>

![Pannello Gruppo di risorse per la rete virtuale e i cluster](./media/hdinsight-apache-storm-with-kafka/groupblade.png)

> [!IMPORTANT]
> <span data-ttu-id="e6723-162">Si noti che i nomi dei cluster HDInsight sono **storm-BASENAME** e **kafka-BASENAME**, dove BASENAME è il nome specificato per il modello.</span><span class="sxs-lookup"><span data-stu-id="e6723-162">Notice that the names of the HDInsight clusters are **storm-BASENAME** and **kafka-BASENAME**, where BASENAME is the name you provided to the template.</span></span> <span data-ttu-id="e6723-163">Questi nomi verranno usati nei passaggi successivi per la connessione ai cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-163">You use these names in later steps when connecting to the clusters.</span></span>

## <a name="understanding-the-code"></a><span data-ttu-id="e6723-164">Informazioni sul codice</span><span class="sxs-lookup"><span data-stu-id="e6723-164">Understanding the code</span></span>

<span data-ttu-id="e6723-165">Questo progetto contiene due topologie:</span><span class="sxs-lookup"><span data-stu-id="e6723-165">This project contains two topologies:</span></span>

* <span data-ttu-id="e6723-166">**KafkaWriter**: questa topologia, definita dal file **writer.yaml**, scrive frasi casuali in Kafka usando il KafkaBolt fornito con Apache Storm.</span><span class="sxs-lookup"><span data-stu-id="e6723-166">**KafkaWriter**: Defined by the **writer.yaml** file, this topology writes random sentences to Kafka using the KafkaBolt provided with Apache Storm.</span></span>

    <span data-ttu-id="e6723-167">Questa topologia usa un componente **SentenceSpout** personalizzato per generare frasi casuali.</span><span class="sxs-lookup"><span data-stu-id="e6723-167">This topology uses a custom **SentenceSpout** component to generate random sentences.</span></span>

* <span data-ttu-id="e6723-168">**KafkaReader**: questa topologia, definita dal file **reader.yaml**, legge i dati da Kafka usando il KafkaSpout fornito con Apache Storm e quindi registra i dati in stdout.</span><span class="sxs-lookup"><span data-stu-id="e6723-168">**KafkaReader**: Defined by the **reader.yaml** file, this topology reads data from Kafka using the KafkaSpout provided with Apache Storm, then logs the data to stdout.</span></span>

    <span data-ttu-id="e6723-169">Questa topologia usa iStorm HdfsBolt per scrivere dati nell'archivio predefinito per il cluster Storm.</span><span class="sxs-lookup"><span data-stu-id="e6723-169">This topology uses the Storm HdfsBolt to write data to default storage for the Storm cluster.</span></span>
### <a name="flux"></a><span data-ttu-id="e6723-170">Flux</span><span class="sxs-lookup"><span data-stu-id="e6723-170">Flux</span></span>

<span data-ttu-id="e6723-171">Le topologie vengono definite tramite [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="e6723-171">The topologies are defined using [Flux](https://storm.apache.org/releases/1.1.0/flux.html).</span></span> <span data-ttu-id="e6723-172">Flux è stato introdotto in Storm 0.10.x e consente di separare la configurazione della topologia dal codice.</span><span class="sxs-lookup"><span data-stu-id="e6723-172">Flux was introduced in Storm 0.10.x and allows you to separate the topology configuration from the code.</span></span> <span data-ttu-id="e6723-173">Per le topologie che fanno uso del framework Flux, la topologia viene definita in un file YAML.</span><span class="sxs-lookup"><span data-stu-id="e6723-173">For Topologies that use the Flux framework, the topology is defined in a YAML file.</span></span> <span data-ttu-id="e6723-174">Il file YAML può essere incluso come parte della topologia.</span><span class="sxs-lookup"><span data-stu-id="e6723-174">The YAML file can be included as part of the topology.</span></span> <span data-ttu-id="e6723-175">Può essere anche un file autonomo usato quando si invia la topologia.</span><span class="sxs-lookup"><span data-stu-id="e6723-175">It can also be a standalone file used when you submit the topology.</span></span> <span data-ttu-id="e6723-176">Flux supporta anche la sostituzione delle variabili in fase di esecuzione, caratteristica che viene usata in questo esempio.</span><span class="sxs-lookup"><span data-stu-id="e6723-176">Flux also supports variable substitution at run-time, which is used in this example.</span></span>

<span data-ttu-id="e6723-177">I parametri seguenti vengono impostati in fase di esecuzione per queste topologie:</span><span class="sxs-lookup"><span data-stu-id="e6723-177">The following parameters are set at run time for these topologies:</span></span>

* <span data-ttu-id="e6723-178">`${kafka.topic}`: nome dell'argomento Kafka usato dalla topologie per la lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="e6723-178">`${kafka.topic}`: The name of the Kafka topic that the topologies read/write to.</span></span>

* <span data-ttu-id="e6723-179">`${kafka.broker.hosts}`: host in cui vengono eseguiti i broker di Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-179">`${kafka.broker.hosts}`: The hosts that the Kafka brokers run on.</span></span> <span data-ttu-id="e6723-180">Le informazioni sui broker vengono usate da KafkaBolt durante la scrittura in Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-180">The broker information is used by the KafkaBolt when writing to Kafka.</span></span>

* <span data-ttu-id="e6723-181">`${kafka.zookeeper.hosts}`: host in cui viene eseguito Zookeeper nel cluster di Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-181">`${kafka.zookeeper.hosts}`: The hosts that Zookeeper runs on in the Kafka cluster.</span></span>

<span data-ttu-id="e6723-182">Per altre informazioni sulle topologie di Flux, vedere [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span><span class="sxs-lookup"><span data-stu-id="e6723-182">For more information on Flux topologies, see [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).</span></span>

## <a name="download-and-compile-the-project"></a><span data-ttu-id="e6723-183">Scaricare e compilare il progetto</span><span class="sxs-lookup"><span data-stu-id="e6723-183">Download and compile the project</span></span>

1. <span data-ttu-id="e6723-184">Nell'ambiente di sviluppo scaricare il progetto dall'indirizzo [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), aprire una riga di comando e passare al percorso in cui è stato scaricato il progetto.</span><span class="sxs-lookup"><span data-stu-id="e6723-184">On your development environment, download the project from [https://github.com/Azure-Samples/hdinsight-storm-java-kafka](https://github.com/Azure-Samples/hdinsight-storm-java-kafka), open a command-line, and change directories to the location that you downloaded the project.</span></span>

2. <span data-ttu-id="e6723-185">Dalla directory **hdinsight-storm-java-kafka** usare il comando seguente per compilare il progetto e creare un pacchetto per la distribuzione:</span><span class="sxs-lookup"><span data-stu-id="e6723-185">From the **hdinsight-storm-java-kafka** directory, use the following command to compile the project and create a package for deployment:</span></span>

  ```bash
  mvn clean package
  ```

    <span data-ttu-id="e6723-186">Il processo del pacchetto crea un file denominato `KafkaTopology-1.0-SNAPSHOT.jar` nella directory `target`.</span><span class="sxs-lookup"><span data-stu-id="e6723-186">The package process creates a file named `KafkaTopology-1.0-SNAPSHOT.jar` in the `target` directory.</span></span>

3. <span data-ttu-id="e6723-187">Usare i comandi seguenti per copiare il pacchetto nel cluster Storm in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6723-187">Use the following commands to copy the package to your Storm on HDInsight cluster.</span></span> <span data-ttu-id="e6723-188">Sostituire **USERNAME** con il nome utente SSH per il cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-188">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="e6723-189">Sostituire **BASENAME** con il nome di base usato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-189">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

  ```bash
  scp ./target/KafkaTopology-1.0-SNAPSHOT.jar USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
  ```

    <span data-ttu-id="e6723-190">Quando richiesto, immettere la password usata durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-190">When prompted, enter the password you used when creating the clusters.</span></span>

## <a name="configure-the-topology"></a><span data-ttu-id="e6723-191">Configurare la topologia</span><span class="sxs-lookup"><span data-stu-id="e6723-191">Configure the topology</span></span>

1. <span data-ttu-id="e6723-192">Usare uno dei metodi seguenti per individuare gli host del broker Kafka:</span><span class="sxs-lookup"><span data-stu-id="e6723-192">Use one of the following methods to discover the Kafka broker hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
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
    > <span data-ttu-id="e6723-193">Bash di esempio presuppone che `$CLUSTERNAME` contenga il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6723-193">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="e6723-194">Presuppone anche che [jq](https://stedolan.github.io/jq/) sia installato.</span><span class="sxs-lookup"><span data-stu-id="e6723-194">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="e6723-195">Quando richiesto, immettere la password dell'account di accesso al cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-195">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="e6723-196">Il valore restituito è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="e6723-196">The value returned is similar to the following text:</span></span>

        wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092

    > [!IMPORTANT]
    > <span data-ttu-id="e6723-197">Anche se possono essere presenti più di due host broker per il cluster, non è necessario fornire un elenco completo di tutti gli host ai client.</span><span class="sxs-lookup"><span data-stu-id="e6723-197">While there may be more than two broker hosts for your cluster, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="e6723-198">È sufficiente specificarne uno o due.</span><span class="sxs-lookup"><span data-stu-id="e6723-198">One or two is enough.</span></span>

2. <span data-ttu-id="e6723-199">Usare uno dei metodi seguenti per individuare gli host di Kafka Zookeeper:</span><span class="sxs-lookup"><span data-stu-id="e6723-199">Use one of the following methods to discover the Kafka Zookeeper hosts:</span></span>

    ```powershell
    $creds = Get-Credential -UserName "admin" -Message "Enter the HDInsight login"
    $clusterName = Read-Host -Prompt "Enter the Kafka cluster name"
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
    > <span data-ttu-id="e6723-200">Bash di esempio presuppone che `$CLUSTERNAME` contenga il nome del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="e6723-200">The Bash example assumes that `$CLUSTERNAME` contains the name of the HDInsight cluster.</span></span> <span data-ttu-id="e6723-201">Presuppone anche che [jq](https://stedolan.github.io/jq/) sia installato.</span><span class="sxs-lookup"><span data-stu-id="e6723-201">It also assumes that [jq](https://stedolan.github.io/jq/) is installed.</span></span> <span data-ttu-id="e6723-202">Quando richiesto, immettere la password dell'account di accesso al cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-202">When prompted, enter the password for the cluster login account.</span></span>

    <span data-ttu-id="e6723-203">Il valore restituito è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="e6723-203">The value returned is similar to the following text:</span></span>

        zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181

    > [!IMPORTANT]
    > <span data-ttu-id="e6723-204">Anche se sono presenti più di due nodi Zookeeper, non è necessario fornire un elenco completo di tutti gli host ai client.</span><span class="sxs-lookup"><span data-stu-id="e6723-204">While there are more than two Zookeeper nodes, you do not need to provide a full list of all hosts to clients.</span></span> <span data-ttu-id="e6723-205">È sufficiente specificarne uno o due.</span><span class="sxs-lookup"><span data-stu-id="e6723-205">One or two is enough.</span></span>

    <span data-ttu-id="e6723-206">Salvare questo valore, che verrà usato in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="e6723-206">Save this value, as it is used later.</span></span>

3. <span data-ttu-id="e6723-207">Modificare il file `dev.properties` nella radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="e6723-207">Edit the `dev.properties` file in the root of the project.</span></span> <span data-ttu-id="e6723-208">Aggiungere le informazioni di host di Broker e Zookeeper per le righe corrispondenti in questo file.</span><span class="sxs-lookup"><span data-stu-id="e6723-208">Add the Broker and Zookeeper hosts information to the matching lines in this file.</span></span> <span data-ttu-id="e6723-209">Nell'esempio seguente viene configurato con i valori di esempio dei passaggi precedenti:</span><span class="sxs-lookup"><span data-stu-id="e6723-209">The following example is configured using the sample values from the previous steps:</span></span>

        kafka.zookeeper.hosts: zk0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181,zk2-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:2181
        kafka.broker.hosts: wn0-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092,wn1-kafka.53qqkiavjsoeloiq3y1naf4hzc.ex.internal.cloudapp.net:9092
        kafka.topic: stormtopic

4. <span data-ttu-id="e6723-210">Salvare il file `dev.properties` e quindi usare il comando seguente per caricarlo nel cluster Storm:</span><span class="sxs-lookup"><span data-stu-id="e6723-210">Save the `dev.properties` file and then use the following command to upload it to the Storm cluster:</span></span>

     ```bash
    scp dev.properties USERNAME@storm-BASENAME-ssh.azurehdinsight.net:KafkaTopology-1.0-SNAPSHOT.jar
    ```

    <span data-ttu-id="e6723-211">Sostituire **USERNAME** con il nome utente SSH per il cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-211">Replace **USERNAME** with the SSH user name for the cluster.</span></span> <span data-ttu-id="e6723-212">Sostituire **BASENAME** con il nome di base usato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-212">Replace **BASENAME** with the base name you used when creating the cluster.</span></span>

## <a name="start-the-writer"></a><span data-ttu-id="e6723-213">Avviare il writer</span><span class="sxs-lookup"><span data-stu-id="e6723-213">Start the writer</span></span>

1. <span data-ttu-id="e6723-214">Usare quanto segue per connettersi al cluster Storm tramite SSH.</span><span class="sxs-lookup"><span data-stu-id="e6723-214">Use the following to connect to the Storm cluster using SSH.</span></span> <span data-ttu-id="e6723-215">Sostituire **USERNAME** con il nome utente SSH usato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-215">Replace **USERNAME** with the SSH user name used when creating the cluster.</span></span> <span data-ttu-id="e6723-216">Sostituire **BASENAME** con il nome di base usato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-216">Replace **BASENAME** with the base name used when creating the cluster.</span></span>

  ```bash
  ssh USERNAME@storm-BASENAME-ssh.azurehdinsight.net
  ```

    <span data-ttu-id="e6723-217">Quando richiesto, immettere la password usata durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-217">When prompted, enter the password you used when creating the clusters.</span></span>
   
    <span data-ttu-id="e6723-218">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="e6723-218">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="e6723-219">Dalla connessione SSH, usare il comando seguente per creare un argomento Kafka usato dalla topologia:</span><span class="sxs-lookup"><span data-stu-id="e6723-219">From the SSH connection, use the following command to create the Kafka topic used by the topology:</span></span>

    ```bash
    /usr/hdp/current/kafka-broker/bin/kafka-topics.sh --create --replication-factor 3 --partitions 8 --topic stormtopic --zookeeper $KAFKAZKHOSTS
    ```

    <span data-ttu-id="e6723-220">Sostituire `$KAFKAZKHOSTS` con l'informazione host di Zookeeper recuperata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="e6723-220">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

2. <span data-ttu-id="e6723-221">Dalla connessione SSH al cluster Storm usare il comando seguente per avviare la topologia del writer:</span><span class="sxs-lookup"><span data-stu-id="e6723-221">From the SSH connection to the Storm cluster, use the following command to start the writer topology:</span></span>

    ```bash
    storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
    ```

    <span data-ttu-id="e6723-222">I parametri usati con questo comando sono i seguenti:</span><span class="sxs-lookup"><span data-stu-id="e6723-222">The parameters used with this command are:</span></span>

    * <span data-ttu-id="e6723-223">`org.apache.storm.flux.Flux`: usa Flux per configurare ed eseguire questa topologia.</span><span class="sxs-lookup"><span data-stu-id="e6723-223">`org.apache.storm.flux.Flux`: Use Flux to configure and run this topology.</span></span>

    * <span data-ttu-id="e6723-224">`--remote`: invia la topologia a Nimbus.</span><span class="sxs-lookup"><span data-stu-id="e6723-224">`--remote`: Submit the topology to Nimbus.</span></span> <span data-ttu-id="e6723-225">La topologia viene distribuita ai nodi del ruolo di lavoro nel cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-225">The topology is distributed across the worker nodes in the cluster.</span></span>

    * <span data-ttu-id="e6723-226">`-R /writer.yaml`: usa il file `writer.yaml` per configurare la topologia.</span><span class="sxs-lookup"><span data-stu-id="e6723-226">`-R /writer.yaml`: Use the `writer.yaml` file to configure the topology.</span></span> <span data-ttu-id="e6723-227">`-R` indica che questa risorsa è inclusa nel file JAR.</span><span class="sxs-lookup"><span data-stu-id="e6723-227">`-R` indicates that this resource is included in the jar file.</span></span> <span data-ttu-id="e6723-228">È nella radice del file JAR, quindi `/writer.yaml` è il relativo percorso.</span><span class="sxs-lookup"><span data-stu-id="e6723-228">It's in the root of the jar, so `/writer.yaml` is the path to it.</span></span>

    * <span data-ttu-id="e6723-229">`--filter`: consente di compilare le voci nella topologia `writer.yaml` con i valori nel file `dev.properties`.</span><span class="sxs-lookup"><span data-stu-id="e6723-229">`--filter`: Populate entries in the `writer.yaml` topology using values in the `dev.properties` file.</span></span> <span data-ttu-id="e6723-230">Ad esempio, il valore della voce `kafka.topic` nel file viene usato per sostituire la voce `${kafka.topic}` nella definizione della topologia.</span><span class="sxs-lookup"><span data-stu-id="e6723-230">For example, the value of the `kafka.topic` entry in the file is used to replace the `${kafka.topic}` entry in the topology definition.</span></span>

5. <span data-ttu-id="e6723-231">Dopo aver avviato la topologia, usare il comando seguente per verificare che nell'argomento Kafka vengano scritti i dati:</span><span class="sxs-lookup"><span data-stu-id="e6723-231">Once the topology has started, use the following command to verify that it is writing data to the Kafka topic:</span></span>

  ```bash
  /usr/hdp/current/kafka-broker/bin/kafka-console-consumer.sh --zookeeper $KAFKAZKHOSTS --from-beginning --topic stormtopic
  ```

    <span data-ttu-id="e6723-232">Sostituire `$KAFKAZKHOSTS` con l'informazione host di Zookeeper recuperata nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="e6723-232">Replace `$KAFKAZKHOSTS` with the Zookeeper host information you retrieved in the previous section.</span></span>

    <span data-ttu-id="e6723-233">Questo comando usa uno script fornito con Kafka per monitorare l'argomento.</span><span class="sxs-lookup"><span data-stu-id="e6723-233">This command uses a script shipped with Kafka to monitor the topic.</span></span> <span data-ttu-id="e6723-234">Dopo qualche secondo dovrebbe iniziare a restituire frasi casuali che sono state scritte nell'argomento.</span><span class="sxs-lookup"><span data-stu-id="e6723-234">After a moment, it should start returning random sentences that have been written to the topic.</span></span> <span data-ttu-id="e6723-235">L'output è simile all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e6723-235">The output is similar to the following example:</span></span>

        i am at two with nature             
        an apple a day keeps the doctor away
        snow white and the seven dwarfs     
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        the cow jumped over the moon        
        an apple a day keeps the doctor away
        an apple a day keeps the doctor away
        four score and seven years ago      
        snow white and the seven dwarfs     
        snow white and the seven dwarfs     
        i am at two with nature             
        an apple a day keeps the doctor away

    <span data-ttu-id="e6723-236">Usare CTRL+C per arrestare lo script.</span><span class="sxs-lookup"><span data-stu-id="e6723-236">Use Ctrl+c to stop the script.</span></span>

## <a name="start-the-reader"></a><span data-ttu-id="e6723-237">Avviare il reader</span><span class="sxs-lookup"><span data-stu-id="e6723-237">Start the reader</span></span>

1. <span data-ttu-id="e6723-238">Dalla sessione SSH nel cluster Storm usare il comando seguente per avviare la topologia del reader:</span><span class="sxs-lookup"><span data-stu-id="e6723-238">From the SSH session to the Storm cluster, use the following command to start the reader topology:</span></span>

  ```bash
  storm jar KafkaTopology-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties
  ```

2. <span data-ttu-id="e6723-239">Dopo aver avviato la topologia, aprire l'interfaccia utente di Storm.</span><span class="sxs-lookup"><span data-stu-id="e6723-239">Once the topology starts, open the Storm UI.</span></span> <span data-ttu-id="e6723-240">Questa interfaccia utente Web è disponibile all'indirizzo https://storm-BASENAME.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="e6723-240">This web UI is located at https://storm-BASENAME.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="e6723-241">Sostituire __BASENAME__ con il nome di base usato durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-241">Replace __BASENAME__ with the base name used when the cluster was created.</span></span> 

    <span data-ttu-id="e6723-242">Quando richiesto, usare il nome dell'account di accesso amministratore, la cui impostazione predefinita è `admin`, e la password usati durante la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="e6723-242">When prompted, use the admin login name (default, `admin`) and password used when the cluster was created.</span></span> <span data-ttu-id="e6723-243">Verrà visualizzata una pagina Web simile all'immagine seguente:</span><span class="sxs-lookup"><span data-stu-id="e6723-243">You see a web page similar to the following image:</span></span>

    ![Interfaccia utente di Storm](./media/hdinsight-apache-storm-with-kafka/stormui.png)

3. <span data-ttu-id="e6723-245">Dall'interfaccia utente di Storm, selezionare il collegamento __kafka-reader__ nella sezione __Topology Summary__ (Riepilogo topologia) per visualizzare informazioni sulla topologia __kafka-reader__.</span><span class="sxs-lookup"><span data-stu-id="e6723-245">From the Storm UI, select the __kafka-reader__ link in the __Topology Summary__ section to display information about the __kafka-reader__ topology.</span></span>

    ![Sezione di riepilogo della topologia dell'interfaccia utente Web di Storm](./media/hdinsight-apache-storm-with-kafka/topology-summary.png)

4. <span data-ttu-id="e6723-247">Selezionare il collegamento __logger-bolt__ nella sezione __Bolts (All time)__ (Bolt - Intero periodo) per visualizzare informazioni sulle istanze del componente logger-bolt.</span><span class="sxs-lookup"><span data-stu-id="e6723-247">To display information about the instances of the logger-bolt component, select the __logger-bolt__ link in the __Bolts (All time)__ section.</span></span>

    ![Collegamento logger-bolt nella sezione dei bolt](./media/hdinsight-apache-storm-with-kafka/bolts.png)

5. <span data-ttu-id="e6723-249">Nella sezione __Executors__ (Esecutori) selezionare un collegamento nella colonna __Port__ (Porta) per visualizzare le informazioni di registrazione su questa istanza del componente.</span><span class="sxs-lookup"><span data-stu-id="e6723-249">In the __Executors__ section, select a link in the __Port__ column to display logging information about this instance of the component.</span></span>

    ![Collegamento esecutori](./media/hdinsight-apache-storm-with-kafka/executors.png)

    <span data-ttu-id="e6723-251">Il log contiene un elenco dei dati letti dall'argomento Kafka.</span><span class="sxs-lookup"><span data-stu-id="e6723-251">The log contains a log of the data read from the Kafka topic.</span></span> <span data-ttu-id="e6723-252">Le informazioni contenute nel log sono simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="e6723-252">The information in the log is similar to the following text:</span></span>

        2016-11-04 17:47:14.907 c.m.e.LoggerBolt [INFO] Received data: four score and seven years ago
        2016-11-04 17:47:14.907 STDIO [INFO] the cow jumped over the moon
        2016-11-04 17:47:14.908 c.m.e.LoggerBolt [INFO] Received data: the cow jumped over the moon
        2016-11-04 17:47:14.911 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.911 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.932 STDIO [INFO] snow white and the seven dwarfs
        2016-11-04 17:47:14.932 c.m.e.LoggerBolt [INFO] Received data: snow white and the seven dwarfs
        2016-11-04 17:47:14.969 STDIO [INFO] an apple a day keeps the doctor away
        2016-11-04 17:47:14.970 c.m.e.LoggerBolt [INFO] Received data: an apple a day keeps the doctor away

## <a name="stop-the-topologies"></a><span data-ttu-id="e6723-253">Arrestare le topologie</span><span class="sxs-lookup"><span data-stu-id="e6723-253">Stop the topologies</span></span>

<span data-ttu-id="e6723-254">Dalla sessione SSH nel cluster Storm usare i comandi seguenti per arrestare le topologie di Storm:</span><span class="sxs-lookup"><span data-stu-id="e6723-254">From an SSH session to the Storm cluster, use the following commands to stop the Storm topologies:</span></span>

  ```bash
  storm kill kafka-writer
  storm kill kafka-reader
  ```

## <a name="delete-the-cluster"></a><span data-ttu-id="e6723-255">Eliminare il cluster</span><span class="sxs-lookup"><span data-stu-id="e6723-255">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="e6723-256">Le procedure illustrate in questo documento creano entrambi i cluster nello stesso gruppo di risorse di Azure. È quindi possibile eliminare il gruppo di risorse dal portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e6723-256">Since the steps in this document create both clusters in the same Azure resource group, you can delete the resource group in the Azure portal.</span></span> <span data-ttu-id="e6723-257">Se si elimina il gruppo di risorse, tutte le risorse create seguendo questo documento vengono rimosse.</span><span class="sxs-lookup"><span data-stu-id="e6723-257">Deleting the resource group removes all resources created by following this document.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e6723-258">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e6723-258">Next steps</span></span>

<span data-ttu-id="e6723-259">Per altri esempi di topologie che possono essere usate con Storm in HDInsight, vedere [Esempi di topologie e componenti Storm per Apache Storm in HDInsight](hdinsight-storm-example-topology.md).</span><span class="sxs-lookup"><span data-stu-id="e6723-259">For more example topologies that can be used with Storm on HDInsight, see [Example Storm topologies and components](hdinsight-storm-example-topology.md).</span></span>

<span data-ttu-id="e6723-260">Per informazioni sulla distribuzione e sul monitoraggio di topologie in HDInsight basato su Linux, vedere [Distribuzione e gestione di topologie Apache Storm in HDInsight basato su Linux](hdinsight-storm-deploy-monitor-topology-linux.md).</span><span class="sxs-lookup"><span data-stu-id="e6723-260">For information on deploying and monitoring topologies on Linux-based HDInsight, see [Deploy and manage Apache Storm topologies on Linux-based HDInsight](hdinsight-storm-deploy-monitor-topology-linux.md)</span></span>