---
title: Apache Storm con componenti Python - Azure HDInsight | Microsoft Docs
description: Informazioni su come creare una topologia Apache Storm che usa componenti Python.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
keywords: apache storm python
ms.assetid: edd0ec4f-664d-4266-910c-6ecc94172ad8
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: python
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: 305c4060ad81458b254e66a4bad6dfd7bf69b28d
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="a0c8f-104">Sviluppare topologie Apache Storm con Python in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a0c8f-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="a0c8f-105">Informazioni su come creare una topologia Apache Storm che usa componenti Python.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-105">Learn how to create an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="a0c8f-106">Apache Storm supporta più linguaggi, consentendo di combinare in un'unica topologia componenti in più lingue.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-106">Apache Storm supports multiple languages, even allowing you to combine components from several languages in one topology.</span></span> <span data-ttu-id="a0c8f-107">Il framework Flux, introdotto con Storm 0.10.0, consente di creare facilmente soluzioni che usino i componenti Python.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-107">The Flux framework (introduced with Storm 0.10.0) allows you to easily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a0c8f-108">Le informazioni contenute in questo documento sono state testate usando Storm in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-108">The information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="a0c8f-109">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a0c8f-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a0c8f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="a0c8f-111">Il codice per l'esempio seguente è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="a0c8f-111">The code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0c8f-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="a0c8f-112">Prerequisites</span></span>

* <span data-ttu-id="a0c8f-113">Python 2.7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a0c8f-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="a0c8f-114">Java JDK 1.8 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="a0c8f-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="a0c8f-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="a0c8f-115">Maven 3</span></span>

* <span data-ttu-id="a0c8f-116">(Facoltativo) Un ambiente locale di sviluppo Storm.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="a0c8f-117">L'ambiente locale di Storm è necessario solo se si vuole eseguire la topologia in locale.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-117">A local Storm environment is only needed if you want to run the topology locally.</span></span> <span data-ttu-id="a0c8f-118">Per altre informazioni, vedere [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Impostazione di un ambiente di sviluppo).</span><span class="sxs-lookup"><span data-stu-id="a0c8f-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="a0c8f-119">Supporto per più linguaggi in Storm</span><span class="sxs-lookup"><span data-stu-id="a0c8f-119">Storm multi-language support</span></span>

<span data-ttu-id="a0c8f-120">Apache Storm è stato progettato per funzionare con componenti scritti con qualsiasi linguaggio di programmazione.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-120">Apache Storm was designed to work with components written using any programming language.</span></span> <span data-ttu-id="a0c8f-121">I componenti devono poter lavorare con la [definizione Thrift per Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="a0c8f-121">The components must understand how to work with the [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="a0c8f-122">Per Python viene fornito un modulo, come parte del progetto Apache Storm, che consente di interfacciarsi facilmente con Storm.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-122">For Python, a module is provided as part of the Apache Storm project that allows you to easily interface with Storm.</span></span> <span data-ttu-id="a0c8f-123">Questo modulo è disponibile all'indirizzo [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="a0c8f-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="a0c8f-124">Storm è un processo Java che viene eseguito su Java Virtual Machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="a0c8f-124">Storm is a Java process that runs on the Java Virtual Machine (JVM).</span></span> <span data-ttu-id="a0c8f-125">I componenti scritti in altri linguaggi vengono eseguiti come sottoprocessi.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="a0c8f-126">Storm comunica con tali sottoprocessi tramite messaggi JSON inviati tramite stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-126">The Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="a0c8f-127">Altri dettagli sulla comunicazione tra i componenti sono disponibili nella documentazione relativa al [protocollo Multi-lang](https://storm.apache.org/documentation/Multilang-protocol.html) .</span><span class="sxs-lookup"><span data-stu-id="a0c8f-127">More details on communication between components can be found in the [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-the-flux-framework"></a><span data-ttu-id="a0c8f-128">Python con il framework Flux</span><span class="sxs-lookup"><span data-stu-id="a0c8f-128">Python with the Flux framework</span></span>

<span data-ttu-id="a0c8f-129">Il framework Flux consente di definire topologie Storm in modo separato rispetto ai componenti.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-129">The Flux framework allows you to define Storm topologies separately from the components.</span></span> <span data-ttu-id="a0c8f-130">Il Flux framework usa YAML per definire la topologia Storm.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-130">The Flux framework uses YAML to define the Storm topology.</span></span> <span data-ttu-id="a0c8f-131">Il testo seguente è un esempio di come fare riferimento a un componente Python nel documento YAML:</span><span class="sxs-lookup"><span data-stu-id="a0c8f-131">The following text is an example of how to reference a Python component in the YAML document:</span></span>

```yaml
# Spout definitions
spouts:
  - id: "sentence-spout"
    className: "org.apache.storm.flux.wrappers.spouts.FluxShellSpout"
    constructorArgs:
      # Command line
      - ["python", "sentencespout.py"]
      # Output field(s)
      - ["sentence"]
    # parallelism hint
    parallelism: 1
```

<span data-ttu-id="a0c8f-132">La classe `FluxShellSpout` viene usata per avviare lo script `sentencespout.py` che implementa lo spout.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-132">The class `FluxShellSpout` is used to start the `sentencespout.py` script that implements the spout.</span></span>

<span data-ttu-id="a0c8f-133">Flux prevede che gli script Python siano nella directory `/resources` all'interno del file con estensione jar che contiene la topologia.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-133">Flux expects the Python scripts to be in the `/resources` directory inside the jar file that contains the topology.</span></span> <span data-ttu-id="a0c8f-134">Pertanto in questo esempio gli script Python vengono archiviati nella directory `/multilang/resources`.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-134">So this example stores the Python scripts in the `/multilang/resources` directory.</span></span> <span data-ttu-id="a0c8f-135">`pom.xml` include il file usando il codice XML seguente:</span><span class="sxs-lookup"><span data-stu-id="a0c8f-135">The `pom.xml` includes this file using the following XML:</span></span>

```xml
<!-- include the Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="a0c8f-136">Come accennato in precedenza, un file `storm.py` implementa la definizione Thrift per Storm.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-136">As mentioned earlier, there is a `storm.py` file that implements the Thrift definition for Storm.</span></span> <span data-ttu-id="a0c8f-137">Il framework Flux include automaticamente `storm.py` quando viene compilato il progetto, quindi non è necessario preoccuparsi di includerlo manualmente.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-137">The Flux framework includes `storm.py` automatically when the project is built, so you don't have to worry about including it.</span></span>

## <a name="build-the-project"></a><span data-ttu-id="a0c8f-138">Compilare il progetto</span><span class="sxs-lookup"><span data-stu-id="a0c8f-138">Build the project</span></span>

<span data-ttu-id="a0c8f-139">Dalla radice del progetto, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a0c8f-139">From the root of the project, use the following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="a0c8f-140">Tale comando crea un file `target/WordCount-1.0-SNAPSHOT.jar` che contiene la topologia compilata.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains the compiled topology.</span></span>

## <a name="run-the-topology-locally"></a><span data-ttu-id="a0c8f-141">Eseguire la topologia in locale</span><span class="sxs-lookup"><span data-stu-id="a0c8f-141">Run the topology locally</span></span>

<span data-ttu-id="a0c8f-142">Per eseguire la topologia in locale, usare il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="a0c8f-142">To run the topology locally, use the following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="a0c8f-143">Tale comando richiede un ambiente locale di sviluppo Storm.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="a0c8f-144">Per altre informazioni, vedere [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Impostazione di un ambiente di sviluppo)</span><span class="sxs-lookup"><span data-stu-id="a0c8f-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="a0c8f-145">Una volta avviata, la topologia emette informazioni alla console locale simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="a0c8f-145">Once the topology starts, it emits information to the local console similar to the following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting the cow jumped over the moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="a0c8f-146">Per arrestare la topologia, usare __CTRL+C__.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-146">To stop the topology, use __Ctrl + C__.</span></span>

## <a name="run-the-storm-topology-on-hdinsight"></a><span data-ttu-id="a0c8f-147">Eseguire la topologia Storm in HDInsight</span><span class="sxs-lookup"><span data-stu-id="a0c8f-147">Run the Storm topology on HDInsight</span></span>

1. <span data-ttu-id="a0c8f-148">Usare il comando seguente per copiare il file `WordCount-1.0-SNAPSHOT.jar` nel cluster Storm in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a0c8f-148">Use the following command to copy the `WordCount-1.0-SNAPSHOT.jar` file to your Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="a0c8f-149">Sostituire `sshuser` con l'utente SSH del cluster.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-149">Replace `sshuser` with the SSH user for your cluster.</span></span> <span data-ttu-id="a0c8f-150">Sostituire `mycluster` con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-150">Replace `mycluster` with the cluster name.</span></span> <span data-ttu-id="a0c8f-151">È possibile che venga richiesto di immettere la password per l'utente SSH.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-151">You may be prompted to enter the password for the SSH user.</span></span>

    <span data-ttu-id="a0c8f-152">Per altre informazioni sull'uso di SSH e SCP, vedere [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a0c8f-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a0c8f-153">Una volta completato il caricamento del file, connettersi al cluster tramite SSH:</span><span class="sxs-lookup"><span data-stu-id="a0c8f-153">Once the file has been uploaded, connect to the cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="a0c8f-154">Nella sessione SSH usare il comando seguente per avviare la topologia nel cluster:</span><span class="sxs-lookup"><span data-stu-id="a0c8f-154">From the SSH session, use the following command to start the topology on the cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="a0c8f-155">Per visualizzare la topologia nel cluster, è possibile usare l'interfaccia utente di Storm.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-155">You can use the Storm UI to view the topology on the cluster.</span></span> <span data-ttu-id="a0c8f-156">L'interfaccia utente di Storm è disponibile all'indirizzo https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-156">The Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="a0c8f-157">Sostituire `mycluster` con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="a0c8f-158">Una volta avviata, l'esecuzione di una topologia Storm procede fino a quando non viene arrestata.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="a0c8f-159">Per arrestare la topologia, è possibile usare uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="a0c8f-159">To stop the topology, use one of the following methods:</span></span>
>
> * <span data-ttu-id="a0c8f-160">Il comando `storm kill TOPOLOGYNAME` dalla riga di comando</span><span class="sxs-lookup"><span data-stu-id="a0c8f-160">The `storm kill TOPOLOGYNAME` command from the command line</span></span>
> * <span data-ttu-id="a0c8f-161">Il pulsante **Termina** nell'interfaccia utente di Storm.</span><span class="sxs-lookup"><span data-stu-id="a0c8f-161">The **Kill** button in the Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="a0c8f-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="a0c8f-162">Next steps</span></span>

<span data-ttu-id="a0c8f-163">Vedere i documenti seguenti per altri modi di usare Python con HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a0c8f-163">See the following documents for other ways to use Python with HDInsight:</span></span>

* [<span data-ttu-id="a0c8f-164">Come usare Python per il flusso di processi MapReduce</span><span class="sxs-lookup"><span data-stu-id="a0c8f-164">How to use Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="a0c8f-165">Come usare funzioni definite dall'utente Python in Pig e Hive</span><span class="sxs-lookup"><span data-stu-id="a0c8f-165">How to use Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
