---
title: aaaUse Caffe in Azure HDInsight Spark per l'apprendimento completa distribuita | Documenti Microsoft
description: Usare Caffe in Azure HDInsight Spark per l'apprendimento avanzato distribuito
services: hdinsight
documentationcenter: 
author: xiaoyongzhu
manager: asadk
editor: cgronlun
tags: azure-portal
ms.assetid: 71dcd1ad-4cad-47ad-8a9d-dcb7fa3c2ff9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/17/2017
ms.author: xiaoyzhu
ms.openlocfilehash: d6476a7ed3a0df38538e845d7d5404067b01113c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a>Usare Caffe in Azure HDInsight Spark per l'apprendimento avanzato distribuito


## <a name="introduction"></a>Introduzione

Formazione sta influenzando tutti i dati da toomanufacturing tootransportation sanitari e altro ancora. Le aziende si affidano toodeep apprendimento toosolve problemi, ad esempio [immagine classificazione](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [il riconoscimento vocale](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)riconoscimento dell'oggetto e computer di conversione. 

A questo scopo vengono usati [diversi framework molto diffusi](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), tra cui [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano e così via. Caffe è uno dei hello più famoso Framework non simbolico rete neurale (imperativo) e ampiamente utilizzate in numerose aree, tra cui visione per computer. [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) unisce Caffe e Apache Spark e permette di usare facilmente l'apprendimento avanzato in un cluster Hadoop esistente insieme a pipeline ETL Spark, riducendo così la latenza e la complessità del sistema per l'apprendimento end-to-end.

[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) è hello solo offerta Hadoop cloud completamente gestito che fornisce ottimizzato cluster analitiche Apri origine per Spark, Hive, MapReduce, HBase, Storm, Kafka e R Server supportato da un contratto di servizio con disponibilità del 99,9%. Ognuna di queste tecnologie di Big Data e applicazioni ISV consente una semplice distribuzione come cluster gestito, con funzionalità di sicurezza e monitoraggio di livello aziendale.

Alcuni utenti sono richiede informazioni complete di apprendimento su HDInsight, ovvero il prodotto di PaaS Hadoop Microsoft toouse. Abbiamo altre tooshare hello futuro, ma attualmente desideriamo toosummarize blog di documentazione tecnico su come toouse Caffe in HDInsight Spark.

L'installazione del framework Caffe può risultare piuttosto difficile. In questo blog, si verrà illustrata la modalità tooinstall [Caffe in Spark](https://github.com/yahoo/CaffeOnSpark) per un cluster HDInsight, quindi utilizzare hello incorporato MNIST demo toodemostrate come toouse formazione distribuito tramite HDInsight Spark su CPU.

Esistono quattro passaggi principali tooget, funziona in HDInsight.

1. Installare le dipendenze necessarie hello in tutti i nodi di hello
2. Compilare Caffe in Spark per HDInsight nel nodo head hello
3. Distribuire i nodi di lavoro di hello necessarie librerie tooall hello
4. Creare un modello di Caffe ed eseguirlo in modalità distribuita.

Poiché HDInsight è una soluzione PaaS, offre funzionalità della piattaforma ideale - è piuttosto semplice tooperform alcune attività. Una delle funzionalità di hello frequentemente utilizzati in questo post di blog viene chiamata [genera Script azione](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), con cui è possibile eseguire i comandi shell toocustomize i nodi del cluster (nodo head, il nodo di lavoro o nodo edge).

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a>Passaggio 1: Installare le dipendenze necessarie hello in tutti i nodi di hello

tooget avviato, è necessario dipendenze hello tooinstall che è necessario. sito Caffe Hello e [CaffeOnSpark sito](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offre alcuni wiki molto utile per l'installazione di dipendenze di hello per Spark in modalità YARN (vale a dire la modalità di hello per HDInsight Spark), ma dobbiamo tooadd alcune altre dipendenze per la piattaforma di HDInsight. Verrà azione script hello come indicato di seguito e viene eseguito in tutti i nodi head hello e i nodi di lavoro. L'esecuzione dell'azione script richiede circa 20 minuti, perché le dipendenze dipendono anche da altri pacchetti. È necessario inserirlo in una posizione che è accessibile tooyour cluster HDInsight, ad esempio un percorso di GitHub o un account di archiviazione BLOB di hello predefinito.

    #!/bin/bash
    #Please be aware that installing hello below will add additional 20 mins toocluster creation because of hello dependencies
    #installing all dependencies, including hello ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all hello nodes

    sudo apt-get install -y libprotobuf-dev libleveldb-dev libsnappy-dev libopencv-dev libhdf5-serial-dev protobuf-compiler maven libatlas-base-dev libgflags-dev libgoogle-glog-dev liblmdb-dev build-essential  libboost-all-dev python-numpy python-scipy python-matplotlib ipython ipython-notebook python-pandas python-sympy python-nose

    #install protobuf
    wget https://github.com/google/protobuf/releases/download/v2.5.0/protobuf-2.5.0.tar.gz
    sudo tar xzvf protobuf-2.5.0.tar.gz -C /tmp/
    cd /tmp/protobuf-2.5.0/
    sudo ./configure
    sudo make
    sudo make check
    sudo make install
    sudo ldconfig
    echo "protobuf installation done"


Sono disponibili due passaggi nell'azione script hello precedente. primo passaggio Hello è tooinstall tutti hello librerie necessarie. Tali librerie includono le librerie necessarie per la compilazione di Caffe (ad esempio gflags glog) sia in esecuzione Caffe (ad esempio numpy) hello. Si sta usando libatlas per l'ottimizzazione della CPU, ma è possibile seguire sempre hello CaffeOnSpark wiki sull'installazione di altre librerie di ottimizzazione, ad esempio MKL o CUDA (per GPU).

secondo passaggio Hello è toodownload, compilare e installare protobuf 2.5.0 per Caffe durante la fase di esecuzione. Protobuf 2.5.0 [è necessario](https://github.com/yahoo/CaffeOnSpark/issues/87), tuttavia questa versione non è disponibile come pacchetto su 16 Ubuntu, pertanto è necessario toocompile dal codice sorgente hello. Esistono inoltre alcune risorse su Internet di hello sul toocompile, ad esempio [questo](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)

toosimply iniziare, è sufficiente eseguire questa azione script contro il lavoro di hello tooall cluster i nodi di nodi e head (per HDInsight 3.5). È possibile eseguire le azioni script hello per un cluster in esecuzione o è anche possibile eseguire le azioni script hello durante la fase di disposizione hello cluster. Per ulteriori informazioni sulle azioni script hello, vedere la documentazione di hello [qui](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)

![Script azioni tooInstall dipendenze](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a>Passaggio 2: Compilazione Caffe in Spark per HDInsight nel nodo head hello

secondo passaggio Hello è toobuild Caffe nel nodo head hello e quindi distribuire i nodi di lavoro compilato hello librerie tooall hello. In questo passaggio, è necessario troppo[ssh nel nodo head](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), seguire semplicemente hello [processo di compilazione CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), e di seguito è riportato uno script di hello è possibile utilizzare toobuild CaffeOnSpark con alcuni passaggi aggiuntivi. 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need toobe updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want tooupdate those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up hello environment before building (especially when rebuiding), or there will be errors such as "failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #hello build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put hello already compiled CaffeOnSpark libraries toowasb storage, then read back tooeach node using script actions. This is because CaffeOnSpark requires all hello nodes have hello libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

Potrebbe essere necessario toodo più quali hello nella documentazione di CaffeOnSpark viene dichiarato. modifiche di Hello sono:
- Modificare solo tooCPU e utilizzare libatlas per questo scopo specifico.
- Inserire hello DataSet toohello archiviazione BLOB, che è un percorso condiviso che è accessibile tooall nodi di lavoro per un uso successivo.
- PUT hello compilati archiviazione tooBLOB di librerie Caffe e successivamente si copierà i nodi di hello tooall librerie utilizzando l'ora di ulteriore compilazione tooavoid azioni script.


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a>Risoluzione dei problemi: eccezione Ant BuildException ed esecuzione che restituisce 2

Quando si tenta innanzitutto toobuild CaffeOnSpark, talvolta indicherà

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

Repository di codice hello semplicemente pulita per marca"normale" e quindi eseguire "apportare compilazione" per risolvere questo problema, purché si disponga di dipendenze corrette hello.

### <a name="troubleshooting-maven-repository-connection-time-out"></a>Risoluzione dei problemi: timeout della connessione al repository Maven

Maven fornisce talvolta l'errore di timeout di connessione hello, toobelow simile:

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

Verrà OK attendere per qualche minuto e quindi tenta codice hello toorebuild, pertanto potrebbe essere Maven in qualche modo limiti hello il traffico proveniente da un determinato indirizzo IP.


### <a name="troubleshooting-test-failure-for-caffe"></a>Risoluzione dei problemi: test non superato per Caffe

Probabilmente, verrà visualizzato un errore del test quando si esegue hello controllo finale per CaffeOnSpark, simile con seguente. Si tratta di prabably correlati con codifica UTF-8, ma dovrebbe influire sull'utilizzo di hello di Caffe

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a>Passaggio 3: Distribuire i nodi di lavoro di hello necessarie librerie tooall hello

passaggio successivo Hello è librerie hello toodistribute (fondamentalmente hello librerie in CaffeOnSpark/caffe-public/distribuzione/lib/e CaffeOnSpark/caffe-distri/distribuzione/lib /) nodi hello tooall. Nel passaggio 2, tali librerie si mette in archiviazione BLOB e in questo passaggio, si utilizzerà toocopy azioni script è tooall hello nodi head e lavoro.

toodo, questa semplice eseguire un'azione di script come indicato di seguito (è necessario tooyour specifico cluster di toopoint toohello posizione corretta):

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

Poiché nel passaggio 2, inserirlo in archiviazione BLOB che è nodi hello tooall accessibile hello, in questo passaggio è appena sufficiente copiarla nodi hello tooall.

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a>Passaggio 4: Creare un modello di Caffe ed eseguirlo in modalità distribuita

Dopo aver eseguito hello sopra passaggi, Caffe è stato installato nel nodo head hello e siamo toogo valido. passaggio successivo Hello è un modello Caffe toowrite. 

Caffe utilizza un "architecture espressivo", in cui per la composizione di un modello, è solo necessario toodefine un file di configurazione e senza codifica (nella maggior parte dei casi). Di seguito viene illustrato il modello nel dettaglio. 

modello di Hello che si eseguirà il training oggi è un modello di esempio per il training MNIST. database MNIST Hello di cifre scritte a mano dispone di un set di training di 60.000 esempi e un set di test degli esempi di 10.000. Si tratta di un subset di un set più grande disponibile da NIST. cifre Hello sono stati normalizzati dimensioni e al centro in un'immagine di dimensioni fisse. CaffeOnSpark include alcuni set di dati di script toodownload hello e convertirli in formato corretto hello.

CaffeOnSpark include alcuni esempi di topologia di rete per il training di MNIST. Ha una struttura di suddivisione di architettura di rete hello (topologia hello della rete hello) e l'ottimizzazione nice. In questo caso sono necessari i due file descritti di seguito. 

file "Risolutore" Hello (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) viene utilizzato per supervisione ottimizzazione hello e generare gli aggiornamenti di parametro. Ad esempio, definisce se CPU o GPU deve essere utilizzato, novità momentum hello, sarà il numero di iterazioni, e così via. Definisce inoltre la topologia di rete neurone deve hello l'utilizzo di programma (ovvero secondo file hello che dobbiamo). Per ulteriori informazioni su Risolutore, consultare troppo[Caffe documentazione](http://caffe.berkeleyvision.org/tutorial/solver.html).

Per questo esempio, poiché si sta usando CPU anziché GPU, si dovrebbe modifica hello ultima riga:

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configurazione di Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

È possibile modificare le altre righe in base alle esigenze.

secondo file di Hello (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) definisce come rete neurone hello è simile, hello rilevanti input e file di output. È anche necessario tooupdate hello tooreflect hello training dati percorso. Modificare hello seguente parte in lenet_memory_train_test.prototxt (necessario tooyour specifico cluster di toopoint toohello posizione corretta):

- modificare anche le file:/Users/mridul/bigml/demodl/mnist_train_lmdb"hello" "wasb: / / / progetti/machine_learning/image_dataset/mnist_train_lmdb"
- modificare "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" troppo "wasb: / / / progetti/machine_learning/image_dataset/mnist_test_lmdb"

![Configurazione di Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

Per ulteriori informazioni su come toodefine hello rete, verificare hello [documentazione Caffe MNIST set di dati](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)

A scopo di hello del blog, si utilizza questo semplice esempio MNIST. È consigliabile eseguire il comando hello seguito dal nodo head hello:

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

Fondamentalmente distribuisce hello necessario file filati contenitore tooeach (lenet_memory_solver.prototxt e lenet_memory_train_test.prototxt) e impostare hello percorso appropriato di ogni driver/executor di Spark tooLD_LIBRARY_PATH, definito in hello codice frammento e punti toohello posizione precedente con CaffeOnSpark librerie. 

## <a name="monitoring-and-troubleshooting"></a>Monitoraggio e risoluzione dei problemi

Poiché si sta utilizzando la modalità YARN cluster, nel qual caso sarà driver Spark hello contenitore arbitrario tooan pianificato (e un nodo di lavoro arbitrario) dovrebbe essere visualizzato solo nella console di hello, l'output qualcosa di simile a:

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

Se si desidera tooknow cosa è successo, in genere è necessario un registro del driver di tooget hello Spark, che è disponibili altre informazioni. In questo caso, è necessario toogo toohello dell'interfaccia utente YARN toofind hello YARN log rilevanti. È possibile ottenere hello dell'interfaccia utente YARN dall'URL: 

    https://yourclustername.azurehdinsight.net/yarnui
   
![Interfaccia utente di Yarn](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

È possibile esaminare il numero di risorse allocate per questa applicazione specifica. È possibile fare clic su collegamento "Utilità di pianificazione" hello, e quindi si noterà che per questa applicazione, esistono 9 contenitori in esecuzione. Chiediamo YARN tooprovide 8 executor e un altro contenitore è per il processo di driver. 

![Utilità di pianificazione di YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

Se sono presenti errori, potrebbe essere toocheck hello driver log o i registri di contenitore. Per i registri di driver, è possibile fare clic su ID applicazione hello nell'interfaccia utente di YARN, quindi fare clic sul pulsante "Logs" hello. Hello driver log vengono scritti in stderr.

![Interfaccia utente 2 di YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

Ad esempio, è possibile riscontrare alcuni errore hello seguito dai registri di driver hello, che indica di che allocare un numero eccessivo di executor.

    17/02/01 07:26:06 ERROR ApplicationMaster: User class threw exception: java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
    java.lang.IllegalStateException: Insufficient training data. Please adjust hyperparameters or increase dataset.
        at com.yahoo.ml.caffe.CaffeOnSpark.trainWithValidation(CaffeOnSpark.scala:261)
        at com.yahoo.ml.caffe.CaffeOnSpark$.main(CaffeOnSpark.scala:42)
        at com.yahoo.ml.caffe.CaffeOnSpark.main(CaffeOnSpark.scala)
        at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
        at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
        at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
        at java.lang.reflect.Method.invoke(Method.java:498)
        at org.apache.spark.deploy.yarn.ApplicationMaster$$anon$2.run(ApplicationMaster.scala:627)

In alcuni casi, il problema di hello può verificarsi in executor piuttosto che i driver. In questo caso, è necessario toocheck hello contenitore registri. È possibile ottenere sempre i log del contenitore hello e quindi ottenere il contenitore non riuscito di hello. Ad esempio, durante l'esecuzione di Caffe si può verificare questo errore:

    17/02/01 07:12:05 WARN YarnAllocator: Container marked as failed: container_1485916338528_0008_05_000005 on host: 10.0.0.14. Exit status: 134. Diagnostics: Exception from container-launch.
    Container id: container_1485916338528_0008_05_000005
    Exit code: 134
    Exception message: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

    Stack trace: ExitCodeException exitCode=134: /bin/bash: line 1: 12230 Aborted                 (core dumped) LD_LIBRARY_PATH=/usr/hdp/current/hadoop-client/lib/native:/usr/hdp/current/hadoop-client/lib/native/Linux-amd64-64:/home/xiaoyzhu/CaffeOnSpark/caffe-public/distribute/lib:/home/xiaoyzhu/CaffeOnSpark/caffe-distri/distribute/lib /usr/lib/jvm/java-8-openjdk-amd64/bin/java -server -Xmx4608m '-Dhdp.version=' '-Detwlogger.component=sparkexecutor' '-DlogFilter.filename=SparkLogFilters.xml' '-DpatternGroup.filename=SparkPatternGroups.xml' '-Dlog4jspark.root.logger=INFO,console,RFA,ETW,Anonymizer' '-Dlog4jspark.log.dir=/var/log/sparkapp/${user.name}' '-Dlog4jspark.log.file=sparkexecutor.log' '-Dlog4j.configuration=file:/usr/hdp/current/spark2-client/conf/log4j.properties' '-Djavax.xml.parsers.SAXParserFactory=com.sun.org.apache.xerces.internal.jaxp.SAXParserFactoryImpl' -Djava.io.tmpdir=/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/tmp '-Dspark.driver.port=43942' '-Dspark.history.ui.port=18080' '-Dspark.ui.port=0' -Dspark.yarn.app.container.log.dir=/mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005 -XX:OnOutOfMemoryError='kill %p' org.apache.spark.executor.CoarseGrainedExecutorBackend --driver-url spark://CoarseGrainedScheduler@10.0.0.13:43942 --executor-id 4 --hostname 10.0.0.14 --cores 3 --app-id application_1485916338528_0008 --user-class-path file:/mnt/resource/hadoop/yarn/local/usercache/xiaoyzhu/appcache/application_1485916338528_0008/container_1485916338528_0008_05_000005/__app__.jar > /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stdout 2> /mnt/resource/hadoop/yarn/log/application_1485916338528_0008/container_1485916338528_0008_05_000005/stderr

        at org.apache.hadoop.util.Shell.runCommand(Shell.java:933)
        at org.apache.hadoop.util.Shell.run(Shell.java:844)
        at org.apache.hadoop.util.Shell$ShellCommandExecutor.execute(Shell.java:1123)
        at org.apache.hadoop.yarn.server.nodemanager.DefaultContainerExecutor.launchContainer(DefaultContainerExecutor.java:225)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:317)
        at org.apache.hadoop.yarn.server.nodemanager.containermanager.launcher.ContainerLaunch.call(ContainerLaunch.java:83)
        at java.util.concurrent.FutureTask.run(FutureTask.java:266)
        at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1142)
        at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:617)
        at java.lang.Thread.run(Thread.java:745)


    Container exited with a non-zero exit code 134

In questo caso, è necessario l'ID di contenitore non è stato possibile hello tooget (in hello prima di case, è container_1485916338528_0008_05_000005). È necessario toorun 

    yarn logs -containerId container_1485916338528_0008_03_000005

dal nodo head hello. L'errore del contenitore è dovuto all'uso della modalità GPU in lenet_memory_solver.prototxt, che invece prevede l'uso della modalità CPU.

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a>Risultati

Poiché si sta assegnando 8 executor e topologia di rete hello è semplice, sono necessari solo risultati di circa 30 minuti toorun hello. Dalla riga di comando hello, è possibile vedere che abbiamo inserire toowasb:///mnist.model modello hello e hello risultati tooa cartella wasb: / / / mnist_features_result.

È possibile ottenere risultati hello eseguendo

    hadoop fs -cat hdfs:///mnist_features_result/*

e ottenere un risultato hello analogo:

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

etichetta hello è numero hello hello modello identifica Hello SampleID corrisponde al rappresenta hello ID nel set di dati MNIST hello.


## <a name="conclusion"></a>Conclusioni

In questa documentazione, si è tentato tooinstall CaffeOnSpark con l'esecuzione di un semplice esempio. HDInsight è una piattaforma di calcolo distribuito completo cloud gestiti ed è hello migliore per l'esecuzione di machine learning e carichi di lavoro analitica avanzate in grandi set di dati e per l'apprendimento completa distribuita, è possibile utilizzare Caffe in formazione tooperform HDInsight Spark attività.


## <a name="seealso"></a>Vedere anche
* [Panoramica: Apache Spark su Azure HDInsight](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a>Scenari
* [Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a>Gestire risorse
* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)

