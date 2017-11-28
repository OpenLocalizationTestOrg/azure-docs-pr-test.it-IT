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
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="d6444-103">Usare Caffe in Azure HDInsight Spark per l'apprendimento avanzato distribuito</span><span class="sxs-lookup"><span data-stu-id="d6444-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="d6444-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="d6444-104">Introduction</span></span>

<span data-ttu-id="d6444-105">Formazione sta influenzando tutti i dati da toomanufacturing tootransportation sanitari e altro ancora.</span><span class="sxs-lookup"><span data-stu-id="d6444-105">Deep learning is impacting everything from healthcare tootransportation toomanufacturing, and more.</span></span> <span data-ttu-id="d6444-106">Le aziende si affidano toodeep apprendimento toosolve problemi, ad esempio [immagine classificazione](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [il riconoscimento vocale](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html)riconoscimento dell'oggetto e computer di conversione.</span><span class="sxs-lookup"><span data-stu-id="d6444-106">Companies are turning toodeep learning toosolve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="d6444-107">A questo scopo vengono usati [diversi framework molto diffusi](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), tra cui [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano e così via. Caffe è uno dei hello più famoso Framework non simbolico rete neurale (imperativo) e ampiamente utilizzate in numerose aree, tra cui visione per computer.</span><span class="sxs-lookup"><span data-stu-id="d6444-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of hello most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="d6444-108">[CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) unisce Caffe e Apache Spark e permette di usare facilmente l'apprendimento avanzato in un cluster Hadoop esistente insieme a pipeline ETL Spark, riducendo così la latenza e la complessità del sistema per l'apprendimento end-to-end.</span><span class="sxs-lookup"><span data-stu-id="d6444-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="d6444-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) è hello solo offerta Hadoop cloud completamente gestito che fornisce ottimizzato cluster analitiche Apri origine per Spark, Hive, MapReduce, HBase, Storm, Kafka e R Server supportato da un contratto di servizio con disponibilità del 99,9%.</span><span class="sxs-lookup"><span data-stu-id="d6444-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is hello only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="d6444-110">Ognuna di queste tecnologie di Big Data e applicazioni ISV consente una semplice distribuzione come cluster gestito, con funzionalità di sicurezza e monitoraggio di livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="d6444-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="d6444-111">Alcuni utenti sono richiede informazioni complete di apprendimento su HDInsight, ovvero il prodotto di PaaS Hadoop Microsoft toouse.</span><span class="sxs-lookup"><span data-stu-id="d6444-111">Some users are asking us about how toouse deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="d6444-112">Abbiamo altre tooshare hello futuro, ma attualmente desideriamo toosummarize blog di documentazione tecnico su come toouse Caffe in HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="d6444-112">We will have more tooshare in hello future, but today we want toosummarize a technical blog on how toouse Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="d6444-113">L'installazione del framework Caffe può risultare piuttosto difficile.</span><span class="sxs-lookup"><span data-stu-id="d6444-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="d6444-114">In questo blog, si verrà illustrata la modalità tooinstall [Caffe in Spark](https://github.com/yahoo/CaffeOnSpark) per un cluster HDInsight, quindi utilizzare hello incorporato MNIST demo toodemostrate come toouse formazione distribuito tramite HDInsight Spark su CPU.</span><span class="sxs-lookup"><span data-stu-id="d6444-114">In this blog, we will first illustrate how tooinstall [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use hello built-in MNIST demo toodemostrate how toouse Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="d6444-115">Esistono quattro passaggi principali tooget, funziona in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6444-115">There are four major steps tooget it work on HDInsight.</span></span>

1. <span data-ttu-id="d6444-116">Installare le dipendenze necessarie hello in tutti i nodi di hello</span><span class="sxs-lookup"><span data-stu-id="d6444-116">Install hello required dependencies on all hello nodes</span></span>
2. <span data-ttu-id="d6444-117">Compilare Caffe in Spark per HDInsight nel nodo head hello</span><span class="sxs-lookup"><span data-stu-id="d6444-117">Build Caffe on Spark for HDInsight on hello head node</span></span>
3. <span data-ttu-id="d6444-118">Distribuire i nodi di lavoro di hello necessarie librerie tooall hello</span><span class="sxs-lookup"><span data-stu-id="d6444-118">Distribute hello required libraries tooall hello worker nodes</span></span>
4. <span data-ttu-id="d6444-119">Creare un modello di Caffe ed eseguirlo in modalità distribuita.</span><span class="sxs-lookup"><span data-stu-id="d6444-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="d6444-120">Poiché HDInsight è una soluzione PaaS, offre funzionalità della piattaforma ideale - è piuttosto semplice tooperform alcune attività.</span><span class="sxs-lookup"><span data-stu-id="d6444-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy tooperform some tasks.</span></span> <span data-ttu-id="d6444-121">Una delle funzionalità di hello frequentemente utilizzati in questo post di blog viene chiamata [genera Script azione](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), con cui è possibile eseguire i comandi shell toocustomize i nodi del cluster (nodo head, il nodo di lavoro o nodo edge).</span><span class="sxs-lookup"><span data-stu-id="d6444-121">One of hello features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands toocustomize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-hello-required-dependencies-on-all-hello-nodes"></a><span data-ttu-id="d6444-122">Passaggio 1: Installare le dipendenze necessarie hello in tutti i nodi di hello</span><span class="sxs-lookup"><span data-stu-id="d6444-122">Step 1:  Install hello required dependencies on all hello nodes</span></span>

<span data-ttu-id="d6444-123">tooget avviato, è necessario dipendenze hello tooinstall che è necessario.</span><span class="sxs-lookup"><span data-stu-id="d6444-123">tooget started, we need tooinstall hello dependencies we need.</span></span> <span data-ttu-id="d6444-124">sito Caffe Hello e [CaffeOnSpark sito](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offre alcuni wiki molto utile per l'installazione di dipendenze di hello per Spark in modalità YARN (vale a dire la modalità di hello per HDInsight Spark), ma dobbiamo tooadd alcune altre dipendenze per la piattaforma di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d6444-124">hello Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing hello dependencies for Spark on YARN mode (which is hello mode for HDInsight Spark), but we need tooadd a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="d6444-125">Verrà azione script hello come indicato di seguito e viene eseguito in tutti i nodi head hello e i nodi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="d6444-125">We will use hello script action as below and run it on all hello head nodes and worker nodes.</span></span> <span data-ttu-id="d6444-126">L'esecuzione dell'azione script richiede circa 20 minuti, perché le dipendenze dipendono anche da altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="d6444-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="d6444-127">È necessario inserirlo in una posizione che è accessibile tooyour cluster HDInsight, ad esempio un percorso di GitHub o un account di archiviazione BLOB di hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="d6444-127">You should put it in some location that is accessible tooyour HDInsight cluster, such as a GitHub location or hello default BLOB storage account.</span></span>

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


<span data-ttu-id="d6444-128">Sono disponibili due passaggi nell'azione script hello precedente.</span><span class="sxs-lookup"><span data-stu-id="d6444-128">There are two steps in hello script action above.</span></span> <span data-ttu-id="d6444-129">primo passaggio Hello è tooinstall tutti hello librerie necessarie.</span><span class="sxs-lookup"><span data-stu-id="d6444-129">hello first step is tooinstall all hello required libraries.</span></span> <span data-ttu-id="d6444-130">Tali librerie includono le librerie necessarie per la compilazione di Caffe (ad esempio gflags glog) sia in esecuzione Caffe (ad esempio numpy) hello.</span><span class="sxs-lookup"><span data-stu-id="d6444-130">Those libraries include hello necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="d6444-131">Si sta usando libatlas per l'ottimizzazione della CPU, ma è possibile seguire sempre hello CaffeOnSpark wiki sull'installazione di altre librerie di ottimizzazione, ad esempio MKL o CUDA (per GPU).</span><span class="sxs-lookup"><span data-stu-id="d6444-131">We are using libatlas for CPU optimization, but you can always follow hello CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="d6444-132">secondo passaggio Hello è toodownload, compilare e installare protobuf 2.5.0 per Caffe durante la fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d6444-132">hello second step is toodownload, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="d6444-133">Protobuf 2.5.0 [è necessario](https://github.com/yahoo/CaffeOnSpark/issues/87), tuttavia questa versione non è disponibile come pacchetto su 16 Ubuntu, pertanto è necessario toocompile dal codice sorgente hello.</span><span class="sxs-lookup"><span data-stu-id="d6444-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need toocompile it from hello source code.</span></span> <span data-ttu-id="d6444-134">Esistono inoltre alcune risorse su Internet di hello sul toocompile, ad esempio [questo](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span><span class="sxs-lookup"><span data-stu-id="d6444-134">There are also a few resources on hello Internet on how toocompile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="d6444-135">toosimply iniziare, è sufficiente eseguire questa azione script contro il lavoro di hello tooall cluster i nodi di nodi e head (per HDInsight 3.5).</span><span class="sxs-lookup"><span data-stu-id="d6444-135">toosimply get started, you can just run this script action against your cluster tooall hello worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="d6444-136">È possibile eseguire le azioni script hello per un cluster in esecuzione o è anche possibile eseguire le azioni script hello durante la fase di disposizione hello cluster.</span><span class="sxs-lookup"><span data-stu-id="d6444-136">You can either run hello script actions for a running cluster, or you can also run hello script actions during hello cluster provision time.</span></span> <span data-ttu-id="d6444-137">Per ulteriori informazioni sulle azioni script hello, vedere la documentazione di hello [qui](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span><span class="sxs-lookup"><span data-stu-id="d6444-137">For more details on hello script actions, please see hello documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Script azioni tooInstall dipendenze](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-hello-head-node"></a><span data-ttu-id="d6444-139">Passaggio 2: Compilazione Caffe in Spark per HDInsight nel nodo head hello</span><span class="sxs-lookup"><span data-stu-id="d6444-139">Step 2: Build Caffe on Spark for HDInsight on hello head node</span></span>

<span data-ttu-id="d6444-140">secondo passaggio Hello è toobuild Caffe nel nodo head hello e quindi distribuire i nodi di lavoro compilato hello librerie tooall hello.</span><span class="sxs-lookup"><span data-stu-id="d6444-140">hello second step is toobuild Caffe on hello headnode, and then distribute hello compiled libraries tooall hello worker nodes.</span></span> <span data-ttu-id="d6444-141">In questo passaggio, è necessario troppo[ssh nel nodo head](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), seguire semplicemente hello [processo di compilazione CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), e di seguito è riportato uno script di hello è possibile utilizzare toobuild CaffeOnSpark con alcuni passaggi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="d6444-141">In this step, you will need too[ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow hello [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is hello script you can use toobuild CaffeOnSpark with a few additional steps.</span></span> 

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

<span data-ttu-id="d6444-142">Potrebbe essere necessario toodo più quali hello nella documentazione di CaffeOnSpark viene dichiarato.</span><span class="sxs-lookup"><span data-stu-id="d6444-142">You may need toodo more than what hello documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="d6444-143">modifiche di Hello sono:</span><span class="sxs-lookup"><span data-stu-id="d6444-143">hello changes are:</span></span>
- <span data-ttu-id="d6444-144">Modificare solo tooCPU e utilizzare libatlas per questo scopo specifico.</span><span class="sxs-lookup"><span data-stu-id="d6444-144">Change tooCPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="d6444-145">Inserire hello DataSet toohello archiviazione BLOB, che è un percorso condiviso che è accessibile tooall nodi di lavoro per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="d6444-145">Put hello datasets toohello BLOB storage, which is a shared location that is accessible tooall worker nodes for later use.</span></span>
- <span data-ttu-id="d6444-146">PUT hello compilati archiviazione tooBLOB di librerie Caffe e successivamente si copierà i nodi di hello tooall librerie utilizzando l'ora di ulteriore compilazione tooavoid azioni script.</span><span class="sxs-lookup"><span data-stu-id="d6444-146">Put hello compiled Caffe libraries tooBLOB storage, and later you will copy those libraries tooall hello nodes using script actions tooavoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="d6444-147">Risoluzione dei problemi: eccezione Ant BuildException ed esecuzione che restituisce 2</span><span class="sxs-lookup"><span data-stu-id="d6444-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="d6444-148">Quando si tenta innanzitutto toobuild CaffeOnSpark, talvolta indicherà</span><span class="sxs-lookup"><span data-stu-id="d6444-148">When first trying toobuild CaffeOnSpark, sometimes it will say</span></span>

    failed tooexecute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="d6444-149">Repository di codice hello semplicemente pulita per marca"normale" e quindi eseguire "apportare compilazione" per risolvere questo problema, purché si disponga di dipendenze corrette hello.</span><span class="sxs-lookup"><span data-stu-id="d6444-149">Simply clean hello code repository by "make clean" and then run "make build" will solve this issue, as long as you have hello correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="d6444-150">Risoluzione dei problemi: timeout della connessione al repository Maven</span><span class="sxs-lookup"><span data-stu-id="d6444-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="d6444-151">Maven fornisce talvolta l'errore di timeout di connessione hello, toobelow simile:</span><span class="sxs-lookup"><span data-stu-id="d6444-151">Sometimes maven gives me hello connection time out error, similar toobelow:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request too{s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="d6444-152">Verrà OK attendere per qualche minuto e quindi tenta codice hello toorebuild, pertanto potrebbe essere Maven in qualche modo limiti hello il traffico proveniente da un determinato indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="d6444-152">It will be OK after waiting for a few minutes and then just try toorebuild hello code, so it might be Maven somehow limits hello traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="d6444-153">Risoluzione dei problemi: test non superato per Caffe</span><span class="sxs-lookup"><span data-stu-id="d6444-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="d6444-154">Probabilmente, verrà visualizzato un errore del test quando si esegue hello controllo finale per CaffeOnSpark, simile con seguente.</span><span class="sxs-lookup"><span data-stu-id="d6444-154">You probably will see a test failure when doing hello final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="d6444-155">Si tratta di prabably correlati con codifica UTF-8, ma dovrebbe influire sull'utilizzo di hello di Caffe</span><span class="sxs-lookup"><span data-stu-id="d6444-155">This is prabably related with UTF-8 encoding, but should not impact hello usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-hello-required-libraries-tooall-hello-worker-nodes"></a><span data-ttu-id="d6444-156">Passaggio 3: Distribuire i nodi di lavoro di hello necessarie librerie tooall hello</span><span class="sxs-lookup"><span data-stu-id="d6444-156">Step 3: Distribute hello required libraries tooall hello worker nodes</span></span>

<span data-ttu-id="d6444-157">passaggio successivo Hello è librerie hello toodistribute (fondamentalmente hello librerie in CaffeOnSpark/caffe-public/distribuzione/lib/e CaffeOnSpark/caffe-distri/distribuzione/lib /) nodi hello tooall.</span><span class="sxs-lookup"><span data-stu-id="d6444-157">hello next step is toodistribute hello libraries (basically hello libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) tooall hello nodes.</span></span> <span data-ttu-id="d6444-158">Nel passaggio 2, tali librerie si mette in archiviazione BLOB e in questo passaggio, si utilizzerà toocopy azioni script è tooall hello nodi head e lavoro.</span><span class="sxs-lookup"><span data-stu-id="d6444-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions toocopy it tooall hello head nodes and worker nodes.</span></span>

<span data-ttu-id="d6444-159">toodo, questa semplice eseguire un'azione di script come indicato di seguito (è necessario tooyour specifico cluster di toopoint toohello posizione corretta):</span><span class="sxs-lookup"><span data-stu-id="d6444-159">toodo this, simple run a script action as below (you need toopoint toohello right location specific tooyour cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="d6444-160">Poiché nel passaggio 2, inserirlo in archiviazione BLOB che è nodi hello tooall accessibile hello, in questo passaggio è appena sufficiente copiarla nodi hello tooall.</span><span class="sxs-lookup"><span data-stu-id="d6444-160">Because in step 2, we put it on hello BLOB storage which is accessible tooall hello nodes, in this step we just simply copy it tooall hello nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="d6444-161">Passaggio 4: Creare un modello di Caffe ed eseguirlo in modalità distribuita</span><span class="sxs-lookup"><span data-stu-id="d6444-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="d6444-162">Dopo aver eseguito hello sopra passaggi, Caffe è stato installato nel nodo head hello e siamo toogo valido.</span><span class="sxs-lookup"><span data-stu-id="d6444-162">After running hello above steps, Caffe is alreay installed on hello headnode and we are good toogo.</span></span> <span data-ttu-id="d6444-163">passaggio successivo Hello è un modello Caffe toowrite.</span><span class="sxs-lookup"><span data-stu-id="d6444-163">hello next step is toowrite a Caffe model.</span></span> 

<span data-ttu-id="d6444-164">Caffe utilizza un "architecture espressivo", in cui per la composizione di un modello, è solo necessario toodefine un file di configurazione e senza codifica (nella maggior parte dei casi).</span><span class="sxs-lookup"><span data-stu-id="d6444-164">Caffe is using an "expressive architecture", where for composing a model, you just need toodefine a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="d6444-165">Di seguito viene illustrato il modello nel dettaglio.</span><span class="sxs-lookup"><span data-stu-id="d6444-165">So let's take a look there.</span></span> 

<span data-ttu-id="d6444-166">modello di Hello che si eseguirà il training oggi è un modello di esempio per il training MNIST.</span><span class="sxs-lookup"><span data-stu-id="d6444-166">hello model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="d6444-167">database MNIST Hello di cifre scritte a mano dispone di un set di training di 60.000 esempi e un set di test degli esempi di 10.000.</span><span class="sxs-lookup"><span data-stu-id="d6444-167">hello MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="d6444-168">Si tratta di un subset di un set più grande disponibile da NIST.</span><span class="sxs-lookup"><span data-stu-id="d6444-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="d6444-169">cifre Hello sono stati normalizzati dimensioni e al centro in un'immagine di dimensioni fisse.</span><span class="sxs-lookup"><span data-stu-id="d6444-169">hello digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="d6444-170">CaffeOnSpark include alcuni set di dati di script toodownload hello e convertirli in formato corretto hello.</span><span class="sxs-lookup"><span data-stu-id="d6444-170">CaffeOnSpark has some scripts toodownload hello dataset and convert it into hello right format.</span></span>

<span data-ttu-id="d6444-171">CaffeOnSpark include alcuni esempi di topologia di rete per il training di MNIST.</span><span class="sxs-lookup"><span data-stu-id="d6444-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="d6444-172">Ha una struttura di suddivisione di architettura di rete hello (topologia hello della rete hello) e l'ottimizzazione nice.</span><span class="sxs-lookup"><span data-stu-id="d6444-172">It has a nice design of splitting hello network architecture (hello topology of hello network) and optimization.</span></span> <span data-ttu-id="d6444-173">In questo caso sono necessari i due file descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="d6444-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="d6444-174">file "Risolutore" Hello (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) viene utilizzato per supervisione ottimizzazione hello e generare gli aggiornamenti di parametro.</span><span class="sxs-lookup"><span data-stu-id="d6444-174">hello "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing hello optimization and generating parameter updates.</span></span> <span data-ttu-id="d6444-175">Ad esempio, definisce se CPU o GPU deve essere utilizzato, novità momentum hello, sarà il numero di iterazioni, e così via. Definisce inoltre la topologia di rete neurone deve hello l'utilizzo di programma (ovvero secondo file hello che dobbiamo).</span><span class="sxs-lookup"><span data-stu-id="d6444-175">For example, it defines whether CPU or GPU will be used, what's hello momentum, how many iterations will be, etc. It also defines which neuron network topology should hello program use (which is hello second file we need).</span></span> <span data-ttu-id="d6444-176">Per ulteriori informazioni su Risolutore, consultare troppo[Caffe documentazione](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="d6444-176">For more information about Solver, please refer too[Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="d6444-177">Per questo esempio, poiché si sta usando CPU anziché GPU, si dovrebbe modifica hello ultima riga:</span><span class="sxs-lookup"><span data-stu-id="d6444-177">For this example, since we are using CPU rather than GPU, we should change hello last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configurazione di Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="d6444-179">È possibile modificare le altre righe in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="d6444-179">You can change other lines as needed.</span></span>

<span data-ttu-id="d6444-180">secondo file di Hello (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) definisce come rete neurone hello è simile, hello rilevanti input e file di output.</span><span class="sxs-lookup"><span data-stu-id="d6444-180">hello second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how hello neuron network looks like, and hello relevant input and output file.</span></span> <span data-ttu-id="d6444-181">È anche necessario tooupdate hello tooreflect hello training dati percorso.</span><span class="sxs-lookup"><span data-stu-id="d6444-181">We also need tooupdate hello file tooreflect hello training data location.</span></span> <span data-ttu-id="d6444-182">Modificare hello seguente parte in lenet_memory_train_test.prototxt (necessario tooyour specifico cluster di toopoint toohello posizione corretta):</span><span class="sxs-lookup"><span data-stu-id="d6444-182">Change hello following part in lenet_memory_train_test.prototxt (you need toopoint toohello right location specific tooyour cluster):</span></span>

- <span data-ttu-id="d6444-183">modificare anche le file:/Users/mridul/bigml/demodl/mnist_train_lmdb"hello" "wasb: / / / progetti/machine_learning/image_dataset/mnist_train_lmdb"</span><span class="sxs-lookup"><span data-stu-id="d6444-183">change hello "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" too"wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="d6444-184">modificare "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" troppo "wasb: / / / progetti/machine_learning/image_dataset/mnist_test_lmdb"</span><span class="sxs-lookup"><span data-stu-id="d6444-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" too"wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Configurazione di Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="d6444-186">Per ulteriori informazioni su come toodefine hello rete, verificare hello [documentazione Caffe MNIST set di dati](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span><span class="sxs-lookup"><span data-stu-id="d6444-186">For more information on how toodefine hello network, please check hello [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="d6444-187">A scopo di hello del blog, si utilizza questo semplice esempio MNIST.</span><span class="sxs-lookup"><span data-stu-id="d6444-187">For hello purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="d6444-188">È consigliabile eseguire il comando hello seguito dal nodo head hello:</span><span class="sxs-lookup"><span data-stu-id="d6444-188">You should run hello command below from hello head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="d6444-189">Fondamentalmente distribuisce hello necessario file filati contenitore tooeach (lenet_memory_solver.prototxt e lenet_memory_train_test.prototxt) e impostare hello percorso appropriato di ogni driver/executor di Spark tooLD_LIBRARY_PATH, definito in hello codice frammento e punti toohello posizione precedente con CaffeOnSpark librerie.</span><span class="sxs-lookup"><span data-stu-id="d6444-189">Basically it distributes hello required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) tooeach YARN container, and also set hello relevant PATH of each Spark driver/executor tooLD_LIBRARY_PATH, which is defined in hello previous code snippet and points toohello location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="d6444-190">Monitoraggio e risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="d6444-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="d6444-191">Poiché si sta utilizzando la modalità YARN cluster, nel qual caso sarà driver Spark hello contenitore arbitrario tooan pianificato (e un nodo di lavoro arbitrario) dovrebbe essere visualizzato solo nella console di hello, l'output qualcosa di simile a:</span><span class="sxs-lookup"><span data-stu-id="d6444-191">Since we are using YARN cluster mode, in which case hello Spark driver will be scheduled tooan arbitrary container (and an arbitrary worker node) you should only see in hello console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="d6444-192">Se si desidera tooknow cosa è successo, in genere è necessario un registro del driver di tooget hello Spark, che è disponibili altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="d6444-192">If you want tooknow what happened, you usually need tooget hello Spark driver's log, which has more information.</span></span> <span data-ttu-id="d6444-193">In questo caso, è necessario toogo toohello dell'interfaccia utente YARN toofind hello YARN log rilevanti.</span><span class="sxs-lookup"><span data-stu-id="d6444-193">In this case, you need toogo toohello YARN UI toofind hello relevant YARN logs.</span></span> <span data-ttu-id="d6444-194">È possibile ottenere hello dell'interfaccia utente YARN dall'URL:</span><span class="sxs-lookup"><span data-stu-id="d6444-194">You can get hello YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![Interfaccia utente di Yarn](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="d6444-196">È possibile esaminare il numero di risorse allocate per questa applicazione specifica.</span><span class="sxs-lookup"><span data-stu-id="d6444-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="d6444-197">È possibile fare clic su collegamento "Utilità di pianificazione" hello, e quindi si noterà che per questa applicazione, esistono 9 contenitori in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="d6444-197">You can click hello "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="d6444-198">Chiediamo YARN tooprovide 8 executor e un altro contenitore è per il processo di driver.</span><span class="sxs-lookup"><span data-stu-id="d6444-198">We ask YARN tooprovide 8 executors, and another container is for driver process.</span></span> 

![Utilità di pianificazione di YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="d6444-200">Se sono presenti errori, potrebbe essere toocheck hello driver log o i registri di contenitore.</span><span class="sxs-lookup"><span data-stu-id="d6444-200">You may want toocheck hello  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="d6444-201">Per i registri di driver, è possibile fare clic su ID applicazione hello nell'interfaccia utente di YARN, quindi fare clic sul pulsante "Logs" hello.</span><span class="sxs-lookup"><span data-stu-id="d6444-201">For driver logs, you can click hello application ID in YARN UI, then click hello "Logs" button.</span></span> <span data-ttu-id="d6444-202">Hello driver log vengono scritti in stderr.</span><span class="sxs-lookup"><span data-stu-id="d6444-202">hello driver logs are written into stderr.</span></span>

![Interfaccia utente 2 di YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="d6444-204">Ad esempio, è possibile riscontrare alcuni errore hello seguito dai registri di driver hello, che indica di che allocare un numero eccessivo di executor.</span><span class="sxs-lookup"><span data-stu-id="d6444-204">For example, you might see some of hello error below from hello driver logs, indicating you allocate too many executors.</span></span>

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

<span data-ttu-id="d6444-205">In alcuni casi, il problema di hello può verificarsi in executor piuttosto che i driver.</span><span class="sxs-lookup"><span data-stu-id="d6444-205">Sometimes, hello issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="d6444-206">In questo caso, è necessario toocheck hello contenitore registri.</span><span class="sxs-lookup"><span data-stu-id="d6444-206">In this case, you need toocheck hello container logs.</span></span> <span data-ttu-id="d6444-207">È possibile ottenere sempre i log del contenitore hello e quindi ottenere il contenitore non riuscito di hello.</span><span class="sxs-lookup"><span data-stu-id="d6444-207">You can always get hello container logs, and then get hello failed container.</span></span> <span data-ttu-id="d6444-208">Ad esempio, durante l'esecuzione di Caffe si può verificare questo errore:</span><span class="sxs-lookup"><span data-stu-id="d6444-208">For example, you might meet this failure when running Caffe.</span></span>

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

<span data-ttu-id="d6444-209">In questo caso, è necessario l'ID di contenitore non è stato possibile hello tooget (in hello prima di case, è container_1485916338528_0008_05_000005).</span><span class="sxs-lookup"><span data-stu-id="d6444-209">In this case, you need tooget hello failed container ID (in hello above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="d6444-210">È necessario toorun</span><span class="sxs-lookup"><span data-stu-id="d6444-210">Then you need toorun</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="d6444-211">dal nodo head hello.</span><span class="sxs-lookup"><span data-stu-id="d6444-211">from hello headnode.</span></span> <span data-ttu-id="d6444-212">L'errore del contenitore è dovuto all'uso della modalità GPU in lenet_memory_solver.prototxt, che invece prevede l'uso della modalità CPU.</span><span class="sxs-lookup"><span data-stu-id="d6444-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written tooSTDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="d6444-213">Risultati</span><span class="sxs-lookup"><span data-stu-id="d6444-213">Getting results</span></span>

<span data-ttu-id="d6444-214">Poiché si sta assegnando 8 executor e topologia di rete hello è semplice, sono necessari solo risultati di circa 30 minuti toorun hello.</span><span class="sxs-lookup"><span data-stu-id="d6444-214">Since we are allocating 8 executors, and hello network topology is simple, it should only take around 30 minutes toorun hello result.</span></span> <span data-ttu-id="d6444-215">Dalla riga di comando hello, è possibile vedere che abbiamo inserire toowasb:///mnist.model modello hello e hello risultati tooa cartella wasb: / / / mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="d6444-215">From hello command line, you can see that we put hello model toowasb:///mnist.model, and put hello results tooa folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="d6444-216">È possibile ottenere risultati hello eseguendo</span><span class="sxs-lookup"><span data-stu-id="d6444-216">You can get hello results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="d6444-217">e ottenere un risultato hello analogo:</span><span class="sxs-lookup"><span data-stu-id="d6444-217">and hello result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="d6444-218">etichetta hello è numero hello hello modello identifica Hello SampleID corrisponde al rappresenta hello ID nel set di dati MNIST hello.</span><span class="sxs-lookup"><span data-stu-id="d6444-218">hello SampleID represents hello ID in hello MNIST dataset, and hello label is hello number that hello model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="d6444-219">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="d6444-219">Conclusion</span></span>

<span data-ttu-id="d6444-220">In questa documentazione, si è tentato tooinstall CaffeOnSpark con l'esecuzione di un semplice esempio.</span><span class="sxs-lookup"><span data-stu-id="d6444-220">In this documentation, you have tried tooinstall CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="d6444-221">HDInsight è una piattaforma di calcolo distribuito completo cloud gestiti ed è hello migliore per l'esecuzione di machine learning e carichi di lavoro analitica avanzate in grandi set di dati e per l'apprendimento completa distribuita, è possibile utilizzare Caffe in formazione tooperform HDInsight Spark attività.</span><span class="sxs-lookup"><span data-stu-id="d6444-221">HDInsight is a full managed cloud distributed compute platform, and is hello best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark tooperform deep learning tasks.</span></span>


## <span data-ttu-id="d6444-222"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="d6444-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="d6444-223">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="d6444-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="d6444-224">Scenari</span><span class="sxs-lookup"><span data-stu-id="d6444-224">Scenarios</span></span>
* [<span data-ttu-id="d6444-225">Spark con Machine Learning: utilizzare Spark in HDInsight per l'analisi della temperatura di compilazione utilizzando dati HVAC</span><span class="sxs-lookup"><span data-stu-id="d6444-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="d6444-226">Spark con Machine Learning: usare Spark in HDInsight risultati dell'ispezione alimentare toopredict</span><span class="sxs-lookup"><span data-stu-id="d6444-226">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="d6444-227">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="d6444-227">Manage resources</span></span>
* [<span data-ttu-id="d6444-228">Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure</span><span class="sxs-lookup"><span data-stu-id="d6444-228">Manage resources for hello Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

