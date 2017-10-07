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
# <a name="develop-apache-storm-topologies-using-python-on-hdinsight"></a>Sviluppare topologie Apache Storm con Python in HDInsight

Informazioni su come toocreate una topologia di Apache Storm che utilizza i componenti di Python. Apache Storm supporta più lingue, consentendo anche componenti toocombine da diversi linguaggi, in una topologia. Hello framework luminoso (introdotto con Storm 0.10.0) consente tooeasily creare soluzioni che utilizzano componenti di Python.

> [!IMPORTANT]
> informazioni di Hello in questo documento è state testate con Storm in HDInsight 3.6. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

codice Hello per questo progetto è disponibile all'indirizzo [https://github.com/Azure-Samples/hdinsight-python-storm-wordcount](https://github.com/Azure-Samples/hdinsight-python-storm-wordcount).

## <a name="prerequisites"></a>Prerequisiti

* Python 2.7 o versione successiva

* Java JDK 1.8 o versione successiva

* Maven 3

* (Facoltativo) Un ambiente locale di sviluppo Storm. Un ambiente di Storm locale è necessario solo se si desidera toorun della topologia hello in locale. Per altre informazioni, vedere [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Impostazione di un ambiente di sviluppo).

## <a name="storm-multi-language-support"></a>Supporto per più linguaggi in Storm

Apache Storm è stato progettato toowork con componenti scritti utilizzando qualsiasi linguaggio di programmazione. i componenti di Hello è necessario comprendere come toowork con hello [definizione Thrift per Storm](https://github.com/apache/storm/blob/master/storm-core/src/storm.thrift). Per Python, un modulo viene fornito come parte del progetto di Apache Storm hello che consente di interfaccia tooeasily con Storm. Questo modulo è disponibile all'indirizzo [https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py](https://github.com/apache/storm/blob/master/storm-multilang/python/src/main/resources/resources/storm.py).

Storm è un processo di linguaggio che viene eseguito su hello Java Virtual Machine (JVM). I componenti scritti in altri linguaggi vengono eseguiti come sottoprocessi. Hello Storm comunica con questi sottoprocessi utilizzando i messaggi JSON inviati stdin/stdout. Sono disponibili ulteriori informazioni sulla comunicazione tra i componenti in hello [multilingue protocollo](https://storm.apache.org/documentation/Multilang-protocol.html) documentazione.

## <a name="python-with-hello-flux-framework"></a>Python con framework luminoso hello

framework luminoso Hello consente topologie Storm toodefine separatamente dai componenti di hello. framework luminoso Hello Usa topologia di Storm YAML toodefine hello. testo Hello è riportato un esempio di come un componente di Python nel documento YAML hello tooreference:

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

classe Hello `FluxShellSpout` è usato toostart hello `sentencespout.py` script che implementa beccuccio hello.

Flusso prevede hello Python script toobe hello `/resources` directory all'interno di file jar hello contenente topologia hello. Pertanto in questo esempio Archivia script Python hello in hello `/multilang/resources` directory. Hello `pom.xml` include il file utilizzando il seguente XML hello:

```xml
<!-- include hello Python components -->
<resource>
    <directory>${basedir}/multilang</directory>
    <filtering>false</filtering>
</resource>
```

Come accennato in precedenza, non c'è un `storm.py` file che implementa definizione Thrift hello per Storm. Hello luminoso framework include `storm.py` automaticamente quando hello progetto viene compilato, pertanto non è tooworry inseriti.

## <a name="build-hello-project"></a>Compilare il progetto hello

Dalla radice del progetto hello hello utilizzare hello comando seguente:

```bash
mvn clean compile package
```

Questo comando crea un `target/WordCount-1.0-SNAPSHOT.jar` file che contiene hello compilato topologia.

## <a name="run-hello-topology-locally"></a>Eseguire topologia hello in locale

topologia di hello toorun localmente, utilizzare hello comando seguente:

```bash
storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -l -R /topology.yaml
```

> [!NOTE]
> Tale comando richiede un ambiente locale di sviluppo Storm. Per altre informazioni, vedere [Setting up a development environment](http://storm.apache.org/releases/1.0.1/Setting-up-development-environment.html) (Impostazione di un ambiente di sviluppo)

Una volta avviata topologia hello, emette informazioni toohello console locale toohello simile seguente testo:


    24302 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24302 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting the
    24302 [Thread-28] INFO  o.a.s.t.ShellBolt - ShellLog pid:2437, name:counter-bolt Emitting years:160
    24302 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=the, count=599}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=seven, count=302}
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=dwarfs, count=143}
    24303 [Thread-25-sentence-spout-executor[4 4]] INFO  o.a.s.s.ShellSpout - ShellLog pid:2436, name:sentence-spout Emiting hello cow jumped over hello moon
    24303 [Thread-30] INFO  o.a.s.t.ShellBolt - ShellLog pid:2438, name:splitter-bolt Emitting cow
    24303 [Thread-17-log-executor[3 3]] INFO  o.a.s.f.w.b.LogInfoBolt - {word=four, count=160}


topologia hello toostop, utilizzare __Ctrl + C__.

## <a name="run-hello-storm-topology-on-hdinsight"></a>Eseguire topologia Storm hello in HDInsight

1. Comando che segue di hello utilizzare hello toocopy `WordCount-1.0-SNAPSHOT.jar` file tooyour Storm nel cluster HDInsight:

    ```bash
    scp target\WordCount-1.0-SNAPSHOT.jar sshuser@mycluster-ssh.azurehdinsight.net
    ```

    Sostituire `sshuser` con utente SSH hello per il cluster. Sostituire `mycluster` con il nome del cluster hello. È possibile password hello tooenter richiesta per l'utente SSH hello.

    Per altre informazioni sull'uso di SSH e SCP, vedere [Connettersi a HDInsight (Hadoop) con SSH](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Dopo che è stati caricati file hello, connettere il cluster di toohello tramite SSH:

    ```bash
    ssh sshuser@mycluster-ssh.azurehdinsight.net
    ```

3. Dalla sessione SSH hello, utilizzare hello seguendo topologia hello toostart di comando cluster hello:

    ```bash
    storm jar WordCount-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux -r -R /topology.yaml
    ```

3. È possibile utilizzare topologia hello tooview Storm UI di hello in cluster hello. Hello Storm UI si trova in https://mycluster.azurehdinsight.net/stormui. Sostituire `mycluster` con il nome del cluster.

> [!NOTE]
> Una volta avviata, l'esecuzione di una topologia Storm procede fino a quando non viene arrestata. topologia di hello toostop, utilizzare uno dei seguenti metodi hello:
>
> * Hello `storm kill TOPOLOGYNAME` comando dalla riga di comando hello
> * Hello **Kill** pulsante hello Storm UI.


## <a name="next-steps"></a>Passaggi successivi

Vedere i seguenti documenti per altri toouse modi Python con HDInsight hello:

* [Come toouse Python per lo streaming di processi MapReduce](hdinsight-hadoop-streaming-python.md)
* [Come toouse Python utente definite funzioni (funzione definita dall'utente) in Pig e Hive](hdinsight-python.md)
