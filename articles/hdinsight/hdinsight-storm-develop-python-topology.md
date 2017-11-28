---
title: aaaApache Storm con componenti di Python - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toocreate una topologia di Apache Storm che utilizza i componenti di Python.
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
ms.openlocfilehash: 143c639623f1992f913900a7c52d6e3f03c701e2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a><span data-ttu-id="b3fac-104">Sviluppare topologie Apache Storm con Python in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3fac-104">Develop Apache Storm topologies using Python on HDInsight</span></span>

<span data-ttu-id="b3fac-105">Informazioni su come toocreate una topologia di Apache Storm che utilizza i componenti di Python.</span><span class="sxs-lookup"><span data-stu-id="b3fac-105">Learn how toocreate an Apache Storm topology that uses Python components.</span></span> <span data-ttu-id="b3fac-106">Apache Storm supporta più lingue, consentendo anche componenti toocombine da diversi linguaggi, in una topologia.</span><span class="sxs-lookup"><span data-stu-id="b3fac-106">Apache Storm supports multiple languages, even allowing you toocombine components from several languages in one topology.</span></span> <span data-ttu-id="b3fac-107">Hello framework luminoso (introdotto con Storm 0.10.0) consente tooeasily creare soluzioni che utilizzano componenti di Python.</span><span class="sxs-lookup"><span data-stu-id="b3fac-107">hello Flux framework (introduced with Storm 0.10.0) allows you tooeasily create solutions that use Python components.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b3fac-108">informazioni di Hello in questo documento è state testate con Storm in HDInsight 3.6.</span><span class="sxs-lookup"><span data-stu-id="b3fac-108">hello information in this document was tested using Storm on HDInsight 3.6.</span></span> <span data-ttu-id="b3fac-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="b3fac-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b3fac-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b3fac-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

<span data-ttu-id="b3fac-111">codice Hello per questo progetto è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span><span class="sxs-lookup"><span data-stu-id="b3fac-111">hello code for this project is available at [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b3fac-112">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b3fac-112">Prerequisites</span></span>

* <span data-ttu-id="b3fac-113">Python 2.7 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="b3fac-113">Python 2.7 or higher</span></span>

* <span data-ttu-id="b3fac-114">Java JDK 1.8 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="b3fac-114">Java JDK 1.8 or higher</span></span>

* <span data-ttu-id="b3fac-115">Maven 3</span><span class="sxs-lookup"><span data-stu-id="b3fac-115">Maven 3</span></span>

* <span data-ttu-id="b3fac-116">(Facoltativo) Un ambiente locale di sviluppo Storm.</span><span class="sxs-lookup"><span data-stu-id="b3fac-116">(Optional) A local Storm development environment.</span></span> <span data-ttu-id="b3fac-117">Un ambiente di Storm locale è necessario solo se si desidera toorun della topologia hello in locale.</span><span class="sxs-lookup"><span data-stu-id="b3fac-117">A local Storm environment is only needed if you want toorun hello topology locally.</span></span> <span data-ttu-id="b3fac-118">Per altre informazioni, vedere [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Impostazione di un ambiente di sviluppo).</span><span class="sxs-lookup"><span data-stu-id="b3fac-118">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html).</span></span>

## <a name="storm-multi-language-support"></a><span data-ttu-id="b3fac-119">Supporto per più linguaggi in Storm</span><span class="sxs-lookup"><span data-stu-id="b3fac-119">Storm multi-language support</span></span>

<span data-ttu-id="b3fac-120">Apache Storm è stato progettato toowork con componenti scritti utilizzando qualsiasi linguaggio di programmazione.</span><span class="sxs-lookup"><span data-stu-id="b3fac-120">Apache Storm was designed toowork with components written using any programming language.</span></span> <span data-ttu-id="b3fac-121">i componenti di Hello è necessario comprendere come toowork con hello [definizione Thrift per Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span><span class="sxs-lookup"><span data-stu-id="b3fac-121">hello components must understand how toowork with hello [Thrift definition for Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift).</span></span> <span data-ttu-id="b3fac-122">Per Python, un modulo viene fornito come parte del progetto di Apache Storm hello che consente di interfaccia tooeasily con Storm.</span><span class="sxs-lookup"><span data-stu-id="b3fac-122">For Python, a module is provided as part of hello Apache Storm project that allows you tooeasily interface with Storm.</span></span> <span data-ttu-id="b3fac-123">Questo modulo è disponibile all'indirizzo [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span><span class="sxs-lookup"><span data-stu-id="b3fac-123">You can find this module at [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).</span></span>

<span data-ttu-id="b3fac-124">Storm è un processo di linguaggio che viene eseguito su hello Java Virtual Machine (JVM).</span><span class="sxs-lookup"><span data-stu-id="b3fac-124">Storm is a Java process that runs on hello Java Virtual Machine (JVM).</span></span> <span data-ttu-id="b3fac-125">I componenti scritti in altri linguaggi vengono eseguiti come sottoprocessi.</span><span class="sxs-lookup"><span data-stu-id="b3fac-125">Components written in other languages are executed as subprocesses.</span></span> <span data-ttu-id="b3fac-126">Hello Storm comunica con questi sottoprocessi utilizzando i messaggi JSON inviati stdin/stdout.</span><span class="sxs-lookup"><span data-stu-id="b3fac-126">hello Storm communicates with these subprocesses using JSON messages sent over stdin/stdout.</span></span> <span data-ttu-id="b3fac-127">Sono disponibili ulteriori informazioni sulla comunicazione tra i componenti in hello [multilingue protocollo](https://storm.apache.org/documentation/Multilang-protocol.html) documentazione.</span><span class="sxs-lookup"><span data-stu-id="b3fac-127">More details on communication between components can be found in hello [Multi-lang Protocol](https://storm.apache.org/documentation/Multilang-protocol.html) documentation.</span></span>

## <a name="python-with-hello-flux-framework"></a><span data-ttu-id="b3fac-128">Python con framework luminoso hello</span><span class="sxs-lookup"><span data-stu-id="b3fac-128">Python with hello Flux framework</span></span>

<span data-ttu-id="b3fac-129">framework luminoso Hello consente topologie Storm toodefine separatamente dai componenti di hello.</span><span class="sxs-lookup"><span data-stu-id="b3fac-129">hello Flux framework allows you toodefine Storm topologies separately from hello components.</span></span> <span data-ttu-id="b3fac-130">framework luminoso Hello Usa topologia di Storm YAML toodefine hello.</span><span class="sxs-lookup"><span data-stu-id="b3fac-130">hello Flux framework uses YAML toodefine hello Storm topology.</span></span> <span data-ttu-id="b3fac-131">testo Hello è riportato un esempio di come un componente di Python nel documento YAML hello tooreference:</span><span class="sxs-lookup"><span data-stu-id="b3fac-131">hello following text is an example of how tooreference a Python component in hello YAML document:</span></span>

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

<span data-ttu-id="b3fac-132">classe Hello `FluxShellSpout` è usato toostart hello `sentencespout.py` script che implementa beccuccio hello.</span><span class="sxs-lookup"><span data-stu-id="b3fac-132">hello class `FluxShellSpout` is used toostart hello `sentencespout.py` script that implements hello spout.</span></span>

<span data-ttu-id="b3fac-133">Flusso prevede hello Python script toobe hello `/resources` directory all'interno di file jar hello contenente topologia hello.</span><span class="sxs-lookup"><span data-stu-id="b3fac-133">Flux expects hello Python scripts toobe in hello `/resources` directory inside hello jar file that contains hello topology.</span></span> <span data-ttu-id="b3fac-134">Pertanto in questo esempio Archivia script Python hello in hello `/multilang/resources` directory.</span><span class="sxs-lookup"><span data-stu-id="b3fac-134">So this example stores hello Python scripts in hello `/multilang/resources` directory.</span></span> <span data-ttu-id="b3fac-135">Hello `pom.xml` include il file utilizzando il seguente XML hello:</span><span class="sxs-lookup"><span data-stu-id="b3fac-135">hello `pom.xml` includes this file using hello following XML:</span></span>

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

<span data-ttu-id="b3fac-136">Come accennato in precedenza, non c'è un `storm.py` file che implementa definizione Thrift hello per Storm.</span><span class="sxs-lookup"><span data-stu-id="b3fac-136">As mentioned earlier, there is a `storm.py` file that implements hello Thrift definition for Storm.</span></span> <span data-ttu-id="b3fac-137">Hello luminoso framework include `storm.py` automaticamente quando hello progetto viene compilato, pertanto non è tooworry inseriti.</span><span class="sxs-lookup"><span data-stu-id="b3fac-137">hello Flux framework includes `storm.py` automatically when hello project is built, so you don't have tooworry about including it.</span></span>

## <a name="build-hello-project"></a><span data-ttu-id="b3fac-138">Compilare il progetto hello</span><span class="sxs-lookup"><span data-stu-id="b3fac-138">Build hello project</span></span>

<span data-ttu-id="b3fac-139">Dalla radice del progetto hello hello utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b3fac-139">From hello root of hello project, use hello following command:</span></span>

```bash
mvn clean compile package
```

<span data-ttu-id="b3fac-140">Questo comando crea un `target/WordCount-1.0-SNAPSHOT.jar` file che contiene hello compilato topologia.</span><span class="sxs-lookup"><span data-stu-id="b3fac-140">This command creates a `target/WordCount-1.0-SNAPSHOT.jar` file that contains hello compiled topology.</span></span>

## <a name="run-hello-topology-locally"></a><span data-ttu-id="b3fac-141">Eseguire topologia hello in locale</span><span class="sxs-lookup"><span data-stu-id="b3fac-141">Run hello topology locally</span></span>

<span data-ttu-id="b3fac-142">topologia di hello toorun localmente, utilizzare hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="b3fac-142">toorun hello topology locally, use hello following command:</span></span>

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> <span data-ttu-id="b3fac-143">Tale comando richiede un ambiente locale di sviluppo Storm.</span><span class="sxs-lookup"><span data-stu-id="b3fac-143">This command requires a local Storm development environment.</span></span> <span data-ttu-id="b3fac-144">Per altre informazioni, vedere [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Impostazione di un ambiente di sviluppo)</span><span class="sxs-lookup"><span data-stu-id="b3fac-144">For more information, see [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html)</span></span>

<span data-ttu-id="b3fac-145">Una volta avviata topologia hello, emette informazioni toohello console locale toohello simile seguente testo:</span><span class="sxs-lookup"><span data-stu-id="b3fac-145">Once hello topology starts, it emits information toohello local console similar toohello following text:</span></span>


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


<span data-ttu-id="b3fac-146">topologia hello toostop, utilizzare __Ctrl + C__.</span><span class="sxs-lookup"><span data-stu-id="b3fac-146">toostop hello topology, use __Ctrl + C__.</span></span>

## <a name="run-hello-storm-topology-on-hdinsight"></a><span data-ttu-id="b3fac-147">Eseguire topologia Storm hello in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b3fac-147">Run hello Storm topology on HDInsight</span></span>

1. <span data-ttu-id="b3fac-148">Comando che segue di hello utilizzare hello toocopy `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm nel cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b3fac-148">Use hello following command toocopy hello `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm on HDInsight cluster:</span></span>

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="b3fac-149">Sostituire `sshuser` con utente SSH hello per il cluster.</span><span class="sxs-lookup"><span data-stu-id="b3fac-149">Replace `sshuser` with hello SSH user for your cluster.</span></span> <span data-ttu-id="b3fac-150">Sostituire `mycluster` con il nome del cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b3fac-150">Replace `mycluster` with hello cluster name.</span></span> <span data-ttu-id="b3fac-151">È possibile password hello tooenter richiesta per l'utente SSH hello.</span><span class="sxs-lookup"><span data-stu-id="b3fac-151">You may be prompted tooenter hello password for hello SSH user.</span></span>

    <span data-ttu-id="b3fac-152">Per altre informazioni sull'uso di SSH e SCP, vedere [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b3fac-152">For more information on using SSH and SCP, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b3fac-153">Dopo che è stati caricati file hello, connettere il cluster di toohello tramite SSH:</span><span class="sxs-lookup"><span data-stu-id="b3fac-153">Once hello file has been uploaded, connect toohello cluster using SSH:</span></span>

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. <span data-ttu-id="b3fac-154">Dalla sessione SSH hello, utilizzare hello seguendo topologia hello toostart di comando cluster hello:</span><span class="sxs-lookup"><span data-stu-id="b3fac-154">From hello SSH session, use hello following command toostart hello topology on hello cluster:</span></span>

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. <span data-ttu-id="b3fac-155">È possibile utilizzare topologia hello tooview Storm UI di hello in cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b3fac-155">You can use hello Storm UI tooview hello topology on hello cluster.</span></span> <span data-ttu-id="b3fac-156">Hello Storm UI si trova in https://mycluster.azurehdinsight.net/stormui.</span><span class="sxs-lookup"><span data-stu-id="b3fac-156">hello Storm UI is located at https://mycluster.azurehdinsight.net/stormui.</span></span> <span data-ttu-id="b3fac-157">Sostituire `mycluster` con il nome del cluster.</span><span class="sxs-lookup"><span data-stu-id="b3fac-157">Replace `mycluster` with your cluster name.</span></span>

> [!NOTE]
> <span data-ttu-id="b3fac-158">Una volta avviata, l'esecuzione di una topologia Storm procede fino a quando non viene arrestata.</span><span class="sxs-lookup"><span data-stu-id="b3fac-158">Once started, a Storm topology runs until stopped.</span></span> <span data-ttu-id="b3fac-159">topologia di hello toostop, utilizzare uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="b3fac-159">toostop hello topology, use one of hello following methods:</span></span>
>
> * <span data-ttu-id="b3fac-160">Hello `storm kill TOPOLOGYNAME` comando dalla riga di comando hello</span><span class="sxs-lookup"><span data-stu-id="b3fac-160">hello `storm kill TOPOLOGYNAME` command from hello command line</span></span>
> * <span data-ttu-id="b3fac-161">Hello **Kill** pulsante hello Storm UI.</span><span class="sxs-lookup"><span data-stu-id="b3fac-161">hello **Kill** button in hello Storm UI.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b3fac-162">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b3fac-162">Next steps</span></span>

<span data-ttu-id="b3fac-163">Vedere i seguenti documenti per altri toouse modi Python con HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="b3fac-163">See hello following documents for other ways toouse Python with HDInsight:</span></span>

* [<span data-ttu-id="b3fac-164">Come toouse Python per lo streaming di processi MapReduce</span><span class="sxs-lookup"><span data-stu-id="b3fac-164">How toouse Python for streaming MapReduce jobs</span></span>](hdinsight-hadoop-streaming-python.md)
* [<span data-ttu-id="b3fac-165">Come toouse Python utente definite funzioni (funzione definita dall'utente) in Pig e Hive</span><span class="sxs-lookup"><span data-stu-id="b3fac-165">How toouse Python User Defined Functions (UDF) in Pig and Hive</span></span>](hdinsight-python.md)
