---
title: Usare Caffe in Azure HDInsight Spark per l'apprendimento avanzato distribuito | Microsoft Docs
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
ms.openlocfilehash: 14b7808c9534bce3049422d6bce1e8914b2c2fbc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-caffe-on-azure-hdinsight-spark-for-distributed-deep-learning"></a><span data-ttu-id="93b3a-103">Usare Caffe in Azure HDInsight Spark per l'apprendimento avanzato distribuito</span><span class="sxs-lookup"><span data-stu-id="93b3a-103">Use Caffe on Azure HDInsight Spark for distributed deep learning</span></span>


## <a name="introduction"></a><span data-ttu-id="93b3a-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="93b3a-104">Introduction</span></span>

<span data-ttu-id="93b3a-105">Gli effetti dell'apprendimento avanzato si possono rintracciare in ogni campo, dalla sanità ai trasporti, fino al settore manifatturiero.</span><span class="sxs-lookup"><span data-stu-id="93b3a-105">Deep learning is impacting everything from healthcare to transportation to manufacturing, and more.</span></span> <span data-ttu-id="93b3a-106">Le aziende si affidano all'apprendimento avanzato per risolvere problemi quali la [classificazione di immagini](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), il [riconoscimento vocale](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), il riconoscimento di oggetti e la traduzione automatica.</span><span class="sxs-lookup"><span data-stu-id="93b3a-106">Companies are turning to deep learning to solve hard problems, like [image classification](http://blogs.microsoft.com/next/2015/12/10/microsoft-researchers-win-imagenet-computer-vision-challenge/), [speech recognition](http://googleresearch.blogspot.jp/2015/08/the-neural-networks-behind-google-voice.html), object recognition, and machine translation.</span></span> 

<span data-ttu-id="93b3a-107">A questo scopo vengono usati [diversi framework molto diffusi](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), tra cui [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano e così via. Caffe è un framework per reti neurali non simbolico (imperativo) tra i più famosi ed è largamente usato in molti campi, tra cui la visione artificiale.</span><span class="sxs-lookup"><span data-stu-id="93b3a-107">There are [many popular frameworks](https://en.wikipedia.org/wiki/Comparison_of_deep_learning_software), including [Microsoft Cognitive Toolkit](https://www.microsoft.com/en-us/research/product/cognitive-toolkit/), [Tensorflow](https://www.tensorflow.org/), MXNet, Theano, etc. Caffe is one of the most famous non-symbolic (imperative) neural network frameworks, and widely used in many areas including computer vision.</span></span> <span data-ttu-id="93b3a-108">[CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) unisce Caffe e Apache Spark e permette di usare facilmente l'apprendimento avanzato in un cluster Hadoop esistente insieme a pipeline ETL Spark, riducendo così la latenza e la complessità del sistema per l'apprendimento end-to-end.</span><span class="sxs-lookup"><span data-stu-id="93b3a-108">Furthermore, [CaffeOnSpark](http://yahoohadoop.tumblr.com/post/139916563586/caffeonspark-open-sourced-for-distributed-deep) combines Caffe with Apache Spark, in which case deep learning can be easily used on an existing Hadoop cluster together with Spark ETL pipelines, reducing system complexity and latency for end-to-end learning.</span></span>

<span data-ttu-id="93b3a-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) è l'unica soluzione Hadoop cloud completamente gestita che fornisce cluster di analisi open source ottimizzati per Spark, Hive, MapReduce, HBase, Storm, Kafka ed R Server, con un contratto di servizio che garantisce la disponibilità al 99,9%.</span><span class="sxs-lookup"><span data-stu-id="93b3a-109">[HDInsight](https://azure.microsoft.com/en-us/services/hdinsight/) is the only fully-managed cloud Hadoop offering that provides optimized open source analytic clusters for Spark, Hive, MapReduce, HBase, Storm, Kafka, and R Server backed by a 99.9% SLA.</span></span> <span data-ttu-id="93b3a-110">Ognuna di queste tecnologie di Big Data e applicazioni ISV consente una semplice distribuzione come cluster gestito, con funzionalità di sicurezza e monitoraggio di livello aziendale.</span><span class="sxs-lookup"><span data-stu-id="93b3a-110">Each of these big data technologies and ISV applications are easily deployable as managed clusters with enterprise-level security and monitoring.</span></span>

<span data-ttu-id="93b3a-111">Le informazioni richieste dagli utenti sull'uso dell'apprendimento avanzato in HDInsight, ovvero il prodotto Hadoop PaaS di Microsoft,</span><span class="sxs-lookup"><span data-stu-id="93b3a-111">Some users are asking us about how to use deep learning on HDInsight, which is Microsoft's PaaS Hadoop product.</span></span> <span data-ttu-id="93b3a-112">saranno presto disponibili. Questo articolo offre invece un riepilogo, sotto forma di blog tecnico, sull'uso di Caffe in HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="93b3a-112">We will have more to share in the future, but today we want to summarize a technical blog on how to use Caffe on HDInsight Spark.</span></span>

<span data-ttu-id="93b3a-113">L'installazione del framework Caffe può risultare piuttosto difficile.</span><span class="sxs-lookup"><span data-stu-id="93b3a-113">If you have installed Caffe before, you will notice that installing this framework is a little bit challenging.</span></span> <span data-ttu-id="93b3a-114">Viene illustrato prima di tutto come installare [Caffe in Spark](https://github.com/yahoo/CaffeOnSpark) per un cluster HDInsight. Successivamente, si usa la demo MNIST incorporata per dimostrare come usare l'apprendimento avanzato distribuito con HDInsight Spark nelle CPU.</span><span class="sxs-lookup"><span data-stu-id="93b3a-114">In this blog, we will first illustrate how to install [Caffe on Spark](https://github.com/yahoo/CaffeOnSpark) for an HDInsight cluster, then use the built-in MNIST demo to demostrate how to use Distributed Deep Learning using HDInsight Spark on CPUs.</span></span>

<span data-ttu-id="93b3a-115">Per l'uso in HDInsight è necessario eseguire questi quattro passaggi principali:</span><span class="sxs-lookup"><span data-stu-id="93b3a-115">There are four major steps to get it work on HDInsight.</span></span>

1. <span data-ttu-id="93b3a-116">Installare le dipendenze necessarie in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="93b3a-116">Install the required dependencies on all the nodes</span></span>
2. <span data-ttu-id="93b3a-117">Compilare Caffe in Spark per HDInsight nel nodo head.</span><span class="sxs-lookup"><span data-stu-id="93b3a-117">Build Caffe on Spark for HDInsight on the head node</span></span>
3. <span data-ttu-id="93b3a-118">Distribuire le librerie necessarie in tutti i nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="93b3a-118">Distribute the required libraries to all the worker nodes</span></span>
4. <span data-ttu-id="93b3a-119">Creare un modello di Caffe ed eseguirlo in modalità distribuita.</span><span class="sxs-lookup"><span data-stu-id="93b3a-119">Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="93b3a-120">HDInsight è una soluzione PaaS che offre ottime funzionalità di piattaforma. Alcune attività risultano quindi molto semplici da eseguire.</span><span class="sxs-lookup"><span data-stu-id="93b3a-120">Since HDInsight is a PaaS solution, it offers great platform features - so it is quite easy to perform some tasks.</span></span> <span data-ttu-id="93b3a-121">Una delle funzionalità più usate in questo articolo è l'[azione script](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), che permette di eseguire i comandi della shell per personalizzare i nodi del cluster, ovvero il nodo head, il nodo del ruolo di lavoro e il nodo perimetrale.</span><span class="sxs-lookup"><span data-stu-id="93b3a-121">One of the features that we heavily use in this blog post is called [Script Action](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux), with which you can execute shell commands to customize cluster nodes (head node, worker node, or edge node).</span></span>

## <a name="step-1--install-the-required-dependencies-on-all-the-nodes"></a><span data-ttu-id="93b3a-122">Passaggio 1: Installare le dipendenze necessarie in tutti i nodi</span><span class="sxs-lookup"><span data-stu-id="93b3a-122">Step 1:  Install the required dependencies on all the nodes</span></span>

<span data-ttu-id="93b3a-123">Per iniziare, occorre installare le dipendenze necessarie.</span><span class="sxs-lookup"><span data-stu-id="93b3a-123">To get started, we need to install the dependencies we need.</span></span> <span data-ttu-id="93b3a-124">Il sito di Caffe e il [sito di CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offrono alcuni wiki molti utili per l'installazione delle dipendenze per Spark in modalità YARN, ovvero la modalità per HDInsight Spark, ma è necessario aggiungere altre dipendenze per la piattaforma HDInsight.</span><span class="sxs-lookup"><span data-stu-id="93b3a-124">The Caffe site and [CaffeOnSpark site](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn) offers some very useful wiki for installing the dependencies for Spark on YARN mode (which is the mode for HDInsight Spark), but we need to add a few more dependencies for HDInsight platform.</span></span> <span data-ttu-id="93b3a-125">L'azione script verrà usata come indicato di seguito ed eseguita in tutti i nodi head e i nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="93b3a-125">We will use the script action as below and run it on all the head nodes and worker nodes.</span></span> <span data-ttu-id="93b3a-126">L'esecuzione dell'azione script richiede circa 20 minuti, perché le dipendenze dipendono anche da altri pacchetti.</span><span class="sxs-lookup"><span data-stu-id="93b3a-126">This script action will take about 20 minutes, as those dependencies also depend on other packages.</span></span> <span data-ttu-id="93b3a-127">Inserirla in un percorso che sia accessibile al cluster HDInsight, ad esempio l'account di archiviazione BLOB predefinito o un percorso GitHub.</span><span class="sxs-lookup"><span data-stu-id="93b3a-127">You should put it in some location that is accessible to your HDInsight cluster, such as a GitHub location or the default BLOB storage account.</span></span>

    #!/bin/bash
    #Please be aware that installing the below will add additional 20 mins to cluster creation because of the dependencies
    #installing all dependencies, including the ones mentioned in http://caffe.berkeleyvision.org/install_apt.html, as well a few packages that are not included in HDInsight, such as gflags, glog, lmdb, numpy
    #It seems numpy will only needed during compilation time, but for safety purpose we install them on all the nodes

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


<span data-ttu-id="93b3a-128">L'azione script precedente prevede due passaggi.</span><span class="sxs-lookup"><span data-stu-id="93b3a-128">There are two steps in the script action above.</span></span> <span data-ttu-id="93b3a-129">Il primo passaggio consiste nell'installare tutte le librerie necessarie.</span><span class="sxs-lookup"><span data-stu-id="93b3a-129">The first step is to install all the required libraries.</span></span> <span data-ttu-id="93b3a-130">Sono incluse le librerie necessarie sia per la compilazione di Caffe, ad esempio gflags e glog, che per la sua esecuzione, ad esempio numpy.</span><span class="sxs-lookup"><span data-stu-id="93b3a-130">Those libraries include the necessary libraries for both compiling Caffe(such as gflags, glog) and running Caffe (such as numpy).</span></span> <span data-ttu-id="93b3a-131">Per l'ottimizzazione della CPU si userà libatlas, ma è anche possibile seguire il wiki di CaffeOnSpark sull'installazione di altre librerie di ottimizzazione, come MKL o CUDA per GPU.</span><span class="sxs-lookup"><span data-stu-id="93b3a-131">We are using libatlas for CPU optimization, but you can always follow the CaffeOnSpark wiki on installing other optimization libraries, such as MKL or CUDA (for GPU).</span></span>

<span data-ttu-id="93b3a-132">Il secondo passaggio consiste nello scaricare, compilare e installare protobuf 2.5.0 per Caffe durante la fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="93b3a-132">The second step is to download, compile, and install protobuf 2.5.0 for Caffe during runtime.</span></span> <span data-ttu-id="93b3a-133">Protobuf 2.5.0 [è necessario](https://github.com/yahoo/CaffeOnSpark/issues/87), tuttavia questa versione non è disponibile come pacchetto in Ubuntu 16. È quindi necessario compilarlo dal codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="93b3a-133">Protobuf 2.5.0 [is required](https://github.com/yahoo/CaffeOnSpark/issues/87), however this version is not available as a package on Ubuntu 16, so we need to compile it from the source code.</span></span> <span data-ttu-id="93b3a-134">In Internet è anche possibile reperire alcune risorse che illustrano come compilarlo, ad esempio [questa](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html).</span><span class="sxs-lookup"><span data-stu-id="93b3a-134">There are also a few resources on the Internet on how to compile it, such as [this](http://jugnu-life.blogspot.com/2013/09/install-protobuf-25-on-ubuntu.html)</span></span>

<span data-ttu-id="93b3a-135">Per iniziare direttamente, è possibile eseguire l'azione script nel cluster per tutti i nodi del ruolo di lavoro e i nodi head, per HDInsight 3.5.</span><span class="sxs-lookup"><span data-stu-id="93b3a-135">To simply get started, you can just run this script action against your cluster to all the worker nodes and head nodes (for HDInsight 3.5).</span></span> <span data-ttu-id="93b3a-136">Le azioni script per un cluster possono essere eseguite quando questo è in esecuzione oppure durante la fase di provisioning del cluster.</span><span class="sxs-lookup"><span data-stu-id="93b3a-136">You can either run the script actions for a running cluster, or you can also run the script actions during the cluster provision time.</span></span> <span data-ttu-id="93b3a-137">Per informazioni dettagliate sulle azioni script, vedere la documentazione [qui](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions).</span><span class="sxs-lookup"><span data-stu-id="93b3a-137">For more details on the script actions, please see the documentation [here](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux#view-history-promote-and-demote-script-actions)</span></span>

![Azioni script per l'installazione delle dipendenze](./media/hdinsight-deep-learning-caffe-spark/Script-Action-1.png)


## <a name="step-2-build-caffe-on-spark-for-hdinsight-on-the-head-node"></a><span data-ttu-id="93b3a-139">Passaggio 2: Compilare Caffe in Spark per HDInsight nel nodo head</span><span class="sxs-lookup"><span data-stu-id="93b3a-139">Step 2: Build Caffe on Spark for HDInsight on the head node</span></span>

<span data-ttu-id="93b3a-140">Il secondo passaggio consiste nel compilare Caffe nel nodo head e quindi distribuire le librerie compilate in tutti i nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="93b3a-140">The second step is to build Caffe on the headnode, and then distribute the compiled libraries to all the worker nodes.</span></span> <span data-ttu-id="93b3a-141">In questo passaggio è necessario accedere tramite [SSH al nodo head](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix) e quindi seguire il [processo di compilazione di CaffeOnSpark](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn). Di seguito è riportato lo script che è possibile usare per compilare CaffeOnSpark con alcuni passaggi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="93b3a-141">In this step, you will need to [ssh into your headnode](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-linux-use-ssh-unix), then simply follow the [CaffeOnSpark build process](https://github.com/yahoo/CaffeOnSpark/wiki/GetStarted_yarn), and below is the script you can use to build CaffeOnSpark with a few additional steps.</span></span> 

    #!/bin/bash
    git clone https://github.com/yahoo/CaffeOnSpark.git --recursive
    export CAFFE_ON_SPARK=$(pwd)/CaffeOnSpark

    pushd ${CAFFE_ON_SPARK}/caffe-public/
    cp Makefile.config.example Makefile.config
    echo "INCLUDE_DIRS += ${JAVA_HOME}/include" >> Makefile.config
    #Below configurations might need to be updated based on actual cases. For example, if you are using GPU, or using a different BLAS library, you may want to update those settings accordingly.
    echo "CPU_ONLY := 1" >> Makefile.config
    echo "BLAS := atlas" >> Makefile.config
    echo "INCLUDE_DIRS += /usr/include/hdf5/serial/" >> Makefile.config
    echo "LIBRARY_DIRS += /usr/lib/x86_64-linux-gnu/hdf5/serial/" >> Makefile.config
    popd

    #compile CaffeOnSpark
    pushd ${CAFFE_ON_SPARK}
    #always clean up the environment before building (especially when rebuiding), or there will be errors such as "failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2"
    make clean 
    #the build step usually takes 20~30 mins, since it has a lot maven dependencies
    make build 
    popd
    export LD_LIBRARY_PATH=${CAFFE_ON_SPARK}/caffe-public/distribute/lib:${CAFFE_ON_SPARK}/caffe-distri/distribute/lib

    hadoop fs -mkdir -p wasb:///projects/machine_learning/image_dataset

    ${CAFFE_ON_SPARK}/scripts/setup-mnist.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/mnist_*_lmdb wasb:///projects/machine_learning/image_dataset/

    ${CAFFE_ON_SPARK}/scripts/setup-cifar10.sh
    hadoop fs -put -f ${CAFFE_ON_SPARK}/data/cifar10_*_lmdb wasb:///projects/machine_learning/image_dataset/

    #put the already compiled CaffeOnSpark libraries to wasb storage, then read back to each node using script actions. This is because CaffeOnSpark requires all the nodes have the libarries
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-public/distribute/lib/
    hadoop fs -mkdir -p /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-distri/distribute/lib/* /CaffeOnSpark/caffe-distri/distribute/lib/
    hadoop fs -put CaffeOnSpark/caffe-public/distribute/lib/* /CaffeOnSpark/caffe-public/distribute/lib/

<span data-ttu-id="93b3a-142">Potrebbe essere necessario eseguire operazioni aggiuntive rispetto a quanto indicato nella documentazione di CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="93b3a-142">You may need to do more than what the documentation of CaffeOnSpark says.</span></span> <span data-ttu-id="93b3a-143">È necessario apportare le modifiche seguenti:</span><span class="sxs-lookup"><span data-stu-id="93b3a-143">The changes are:</span></span>
- <span data-ttu-id="93b3a-144">Passare alla sola CPU e usare libatlas per questo scopo specifico.</span><span class="sxs-lookup"><span data-stu-id="93b3a-144">Change to CPU only and use libatlas for this particular purpose.</span></span>
- <span data-ttu-id="93b3a-145">Inserire i set di dati nell'archivio BLOB, che offre un percorso condiviso accessibile a tutti i nodi del ruolo di lavoro per un uso successivo.</span><span class="sxs-lookup"><span data-stu-id="93b3a-145">Put the datasets to the BLOB storage, which is a shared location that is accessible to all worker nodes for later use.</span></span>
- <span data-ttu-id="93b3a-146">Inserire le librerie Caffe compilate nell'archivio BLOB e copiarle successivamente in tutti i nodi usando le azioni script, per evitare tempi di compilazione aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="93b3a-146">Put the compiled Caffe libraries to BLOB storage, and later you will copy those libraries to all the nodes using script actions to avoid additional compilation time.</span></span>


### <a name="troubleshooting-an-ant-buildexception-has-occured-exec-returned-2"></a><span data-ttu-id="93b3a-147">Risoluzione dei problemi: eccezione Ant BuildException ed esecuzione che restituisce 2</span><span class="sxs-lookup"><span data-stu-id="93b3a-147">Troubleshooting: An Ant BuildException has occured: exec returned: 2</span></span>

<span data-ttu-id="93b3a-148">Quando si tenta per la prima volta di compilare CaffeOnSpark, si può ricevere il messaggio di errore seguente:</span><span class="sxs-lookup"><span data-stu-id="93b3a-148">When first trying to build CaffeOnSpark, sometimes it will say</span></span>

    failed to execute goal org.apache.maven.plugins:maven-antrun-plugin:1.7:run (proto) on project caffe-distri: An Ant BuildException has occured: exec returned: 2

<span data-ttu-id="93b3a-149">Per risolvere questo problema è sufficiente pulire il repository del codice con il comando "make clean" e quindi eseguire il comando "make build", purché le dipendenze siano corrette.</span><span class="sxs-lookup"><span data-stu-id="93b3a-149">Simply clean the code repository by "make clean" and then run "make build" will solve this issue, as long as you have the correct dependencies.</span></span>

### <a name="troubleshooting-maven-repository-connection-time-out"></a><span data-ttu-id="93b3a-150">Risoluzione dei problemi: timeout della connessione al repository Maven</span><span class="sxs-lookup"><span data-stu-id="93b3a-150">Troubleshooting: Maven repository connection time out</span></span>

<span data-ttu-id="93b3a-151">A volte, Maven restituisce un errore di timeout della connessione simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="93b3a-151">Sometimes maven gives me the connection time out error, similar to below:</span></span>

    Retry:
    [INFO] Downloading: https://repo.maven.apache.org/maven2/com/twitter/chill_2.11/0.8.0/chill_2.11-0.8.0.jar
    Feb 01, 2017 5:14:49 AM org.apache.maven.wagon.providers.http.httpclient.impl.execchain.RetryExec execute
    INFO: I/O exception (java.net.SocketException) caught when processing request to {s}->https://repo.maven.apache.org:443: Connection timed out (Read failed)

<span data-ttu-id="93b3a-152">Il problema si risolve dopo un'attesa di alcuni minuti e poi è sufficiente provare a ricompilare il codice. È possibile che Maven limiti in qualche modo il traffico da un determinato indirizzo IP.</span><span class="sxs-lookup"><span data-stu-id="93b3a-152">It will be OK after waiting for a few minutes and then just try to rebuild the code, so it might be Maven somehow limits the traffic from a given IP address.</span></span>


### <a name="troubleshooting-test-failure-for-caffe"></a><span data-ttu-id="93b3a-153">Risoluzione dei problemi: test non superato per Caffe</span><span class="sxs-lookup"><span data-stu-id="93b3a-153">Troubleshooting: Test failure for Caffe</span></span>

<span data-ttu-id="93b3a-154">Durante il controllo finale per CaffeOnSpark, potrebbe essere visualizzato un errore di test non superato simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="93b3a-154">You probably will see a test failure when doing the final check for CaffeOnSpark, similar with below.</span></span> <span data-ttu-id="93b3a-155">Si tratta probabilmente di un problema legato alla codifica UTF-8, ma non dovrebbe influire sull'utilizzo di Caffe.</span><span class="sxs-lookup"><span data-stu-id="93b3a-155">This is prabably related with UTF-8 encoding, but should not impact the usage of Caffe</span></span>

    Run completed in 32 seconds, 78 milliseconds.
    Total number of tests run: 7
    Suites: completed 5, aborted 0
    Tests: succeeded 6, failed 1, canceled 0, ignored 0, pending 0
    *** 1 TEST FAILED ***

## <a name="step-3-distribute-the-required-libraries-to-all-the-worker-nodes"></a><span data-ttu-id="93b3a-156">Passaggio 3: Distribuire le librerie necessarie in tutti i nodi del ruolo di lavoro</span><span class="sxs-lookup"><span data-stu-id="93b3a-156">Step 3: Distribute the required libraries to all the worker nodes</span></span>

<span data-ttu-id="93b3a-157">Il passaggio successivo consiste nel distribuire in tutti i nodi le librerie disponibili in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/.</span><span class="sxs-lookup"><span data-stu-id="93b3a-157">The next step is to distribute the libraries (basically the libraries in CaffeOnSpark/caffe-public/distribute/lib/ and CaffeOnSpark/caffe-distri/distribute/lib/) to all the nodes.</span></span> <span data-ttu-id="93b3a-158">Nel passaggio 2 tali librerie sono state inserite nell'archivio BLOB. In questo passaggio si usano le azioni script per copiarlo in tutti i nodi head e i nodi del ruolo di lavoro.</span><span class="sxs-lookup"><span data-stu-id="93b3a-158">In Step 2, we put those libraries on BLOB storage, and in this step, we will use script actions to copy it to all the head nodes and worker nodes.</span></span>

<span data-ttu-id="93b3a-159">A tale scopo, è sufficiente eseguire un'azione di script come indicato di seguito, puntando al percorso specifico del cluster:</span><span class="sxs-lookup"><span data-stu-id="93b3a-159">To do this, simple run a script action as below (you need to point to the right location specific to your cluster):</span></span>

    #!/bin/bash
    hadoop fs -get wasb:///CaffeOnSpark /home/changetoyourusername/

<span data-ttu-id="93b3a-160">Dato che nel passaggio 2 le librerie sono state inserite nell'archivio BLOB, che è accessibile a tutti i nodi, in questo passaggio è sufficiente copiarlo in tutti i nodi.</span><span class="sxs-lookup"><span data-stu-id="93b3a-160">Because in step 2, we put it on the BLOB storage which is accessible to all the nodes, in this step we just simply copy it to all the nodes.</span></span>

## <a name="step-4-compose-a-caffe-model-and-run-it-distributely"></a><span data-ttu-id="93b3a-161">Passaggio 4: Creare un modello di Caffe ed eseguirlo in modalità distribuita</span><span class="sxs-lookup"><span data-stu-id="93b3a-161">Step 4: Compose a Caffe model and run it distributely</span></span>

<span data-ttu-id="93b3a-162">Dopo aver eseguito i passaggi precedenti, Caffe è installato nel nodo head ed è possibile procedere.</span><span class="sxs-lookup"><span data-stu-id="93b3a-162">After running the above steps, Caffe is alreay installed on the headnode and we are good to go.</span></span> <span data-ttu-id="93b3a-163">Il passaggio successivo consiste nello scrivere un modello di Caffe.</span><span class="sxs-lookup"><span data-stu-id="93b3a-163">The next step is to write a Caffe model.</span></span> 

<span data-ttu-id="93b3a-164">Caffe fa uso di un'architettura espressiva in cui, per creare un modello, è sufficiente definire un file di configurazione, nella maggior parte dei casi senza alcuna codifica.</span><span class="sxs-lookup"><span data-stu-id="93b3a-164">Caffe is using an "expressive architecture", where for composing a model, you just need to define a configuration file, and without coding at all (in most cases).</span></span> <span data-ttu-id="93b3a-165">Di seguito viene illustrato il modello nel dettaglio.</span><span class="sxs-lookup"><span data-stu-id="93b3a-165">So let's take a look there.</span></span> 

<span data-ttu-id="93b3a-166">Il modello di cui si esegue il training in questo articolo è un modello di esempio per il training di MNIST.</span><span class="sxs-lookup"><span data-stu-id="93b3a-166">The model we will train today is a sample model for MNIST training.</span></span> <span data-ttu-id="93b3a-167">Il database MNIST di cifre scritte a mano ha un set di training di 60.000 esempi e un set di test di 10.000 esempi.</span><span class="sxs-lookup"><span data-stu-id="93b3a-167">The MNIST database of handwritten digits has a training set of 60,000 examples, and a test set of 10,000 examples.</span></span> <span data-ttu-id="93b3a-168">Si tratta di un subset di un set più grande disponibile da NIST.</span><span class="sxs-lookup"><span data-stu-id="93b3a-168">It is a subset of a larger set available from NIST.</span></span> <span data-ttu-id="93b3a-169">Le dimensioni delle cifre sono state normalizzate e le cifre sono state inserite al centro in un'immagine di dimensioni fisse.</span><span class="sxs-lookup"><span data-stu-id="93b3a-169">The digits have been size-normalized and centered in a fixed-size image.</span></span> <span data-ttu-id="93b3a-170">CaffeOnSpark offre diversi script per scaricare il set di dati e convertirlo nel formato corretto.</span><span class="sxs-lookup"><span data-stu-id="93b3a-170">CaffeOnSpark has some scripts to download the dataset and convert it into the right format.</span></span>

<span data-ttu-id="93b3a-171">CaffeOnSpark include alcuni esempi di topologia di rete per il training di MNIST.</span><span class="sxs-lookup"><span data-stu-id="93b3a-171">CaffeOnSpark provides some network topologies example for MNIST training.</span></span> <span data-ttu-id="93b3a-172">Suddivide in modo utile l'architettura di rete, ovvero la topologia della rete, e ne consente l'ottimizzazione.</span><span class="sxs-lookup"><span data-stu-id="93b3a-172">It has a nice design of splitting the network architecture (the topology of the network) and optimization.</span></span> <span data-ttu-id="93b3a-173">In questo caso sono necessari i due file descritti di seguito.</span><span class="sxs-lookup"><span data-stu-id="93b3a-173">In this case, There are two files required:</span></span> 

<span data-ttu-id="93b3a-174">Il file "solver" (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) viene usato per supervisionare l'ottimizzazione e per generare aggiornamenti dei parametri.</span><span class="sxs-lookup"><span data-stu-id="93b3a-174">the "Solver" file (${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt) is used for overseeing the optimization and generating parameter updates.</span></span> <span data-ttu-id="93b3a-175">Indica ad esempio se usare la CPU o la GPU, il momento, il numero di iterazioni e così via, oltre a definire quale topologia di rete neurale debba essere usata dal programma, ovvero il secondo file necessario.</span><span class="sxs-lookup"><span data-stu-id="93b3a-175">For example, it defines whether CPU or GPU will be used, what's the momentum, how many iterations will be, etc. It also defines which neuron network topology should the program use (which is the second file we need).</span></span> <span data-ttu-id="93b3a-176">Per altre informazioni sul file "solver", vedere la [documentazione di Caffe](http://caffe.berkeleyvision.org/tutorial/solver.html).</span><span class="sxs-lookup"><span data-stu-id="93b3a-176">For more information about Solver, please refer to [Caffe documentation](http://caffe.berkeleyvision.org/tutorial/solver.html).</span></span>

<span data-ttu-id="93b3a-177">Dato che in questo esempio si usa la CPU anziché la GPU, occorre modificare l'ultima riga come indicato di seguito:</span><span class="sxs-lookup"><span data-stu-id="93b3a-177">For this example, since we are using CPU rather than GPU, we should change the last line to:</span></span>

    # solver mode: CPU or GPU
    solver_mode: CPU

![Configurazione di Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-1.png)

<span data-ttu-id="93b3a-179">È possibile modificare le altre righe in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="93b3a-179">You can change other lines as needed.</span></span>

<span data-ttu-id="93b3a-180">Il secondo file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) definisce l'aspetto della rete neurale e il relativo file di input e di output.</span><span class="sxs-lookup"><span data-stu-id="93b3a-180">The second file (${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt) defines how the neuron network looks like, and the relevant input and output file.</span></span> <span data-ttu-id="93b3a-181">Il file deve essere aggiornato in base al percorso dei dati di training.</span><span class="sxs-lookup"><span data-stu-id="93b3a-181">We also need to update the file to reflect the training data location.</span></span> <span data-ttu-id="93b3a-182">Nel file lenet_memory_train_test.prototxtt modificare la parte seguente, puntando al percorso specifico del cluster:</span><span class="sxs-lookup"><span data-stu-id="93b3a-182">Change the following part in lenet_memory_train_test.prototxt (you need to point to the right location specific to your cluster):</span></span>

- <span data-ttu-id="93b3a-183">Modificare "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" in "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb".</span><span class="sxs-lookup"><span data-stu-id="93b3a-183">change the "file:/Users/mridul/bigml/demodl/mnist_train_lmdb" to "wasb:///projects/machine_learning/image_dataset/mnist_train_lmdb"</span></span>
- <span data-ttu-id="93b3a-184">Modificare "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" in "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb".</span><span class="sxs-lookup"><span data-stu-id="93b3a-184">change "file:/Users/mridul/bigml/demodl/mnist_test_lmdb/" to "wasb:///projects/machine_learning/image_dataset/mnist_test_lmdb"</span></span>

![Configurazione di Caffe](./media/hdinsight-deep-learning-caffe-spark/Caffe-2.png)

<span data-ttu-id="93b3a-186">Per altre informazioni su come definire la rete, vedere la [documentazione di Caffe sul set di dati MNIST](http://caffe.berkeleyvision.org/gathered/examples/mnist.html).</span><span class="sxs-lookup"><span data-stu-id="93b3a-186">For more information on how to define the network, please check the [Caffe documentation on MNIST dataset](http://caffe.berkeleyvision.org/gathered/examples/mnist.html)</span></span>

<span data-ttu-id="93b3a-187">Ai fini di questo articolo, viene usato questo semplice esempio di MNIST.</span><span class="sxs-lookup"><span data-stu-id="93b3a-187">For the purpose of this blog, we just use this simple MNIST example.</span></span> <span data-ttu-id="93b3a-188">Eseguire il comando seguente dal nodo head:</span><span class="sxs-lookup"><span data-stu-id="93b3a-188">You should run the command below from the head node:</span></span>

    spark-submit --master yarn --deploy-mode cluster --num-executors 8 --files ${CAFFE_ON_SPARK}/data/lenet_memory_solver.prototxt,${CAFFE_ON_SPARK}/data/lenet_memory_train_test.prototxt --conf spark.driver.extraLibraryPath="${LD_LIBRARY_PATH}" --conf spark.executorEnv.LD_LIBRARY_PATH="${LD_LIBRARY_PATH}" --class com.yahoo.ml.caffe.CaffeOnSpark ${CAFFE_ON_SPARK}/caffe-grid/target/caffe-grid-0.1-SNAPSHOT-jar-with-dependencies.jar -train -features accuracy,loss -label label -conf lenet_memory_solver.prototxt -devices 1 -connection ethernet -model wasb:///mnist.model -output wasb:///mnist_features_result

<span data-ttu-id="93b3a-189">Il comando distribuisce i file lenet_memory_solver.prototxt e lenet_memory_train_test.prototxt necessari a tutti i contenitori YARN e imposta il relativo percorso di ogni driver o executor Spark su LD_LIBRARY_PATH, definito nel frammento di codice precedente, che punta al percorso delle librerie di CaffeOnSpark.</span><span class="sxs-lookup"><span data-stu-id="93b3a-189">Basically it distributes the required files (lenet_memory_solver.prototxt and lenet_memory_train_test.prototxt) to each YARN container, and also set the relevant PATH of each Spark driver/executor to LD_LIBRARY_PATH, which is defined in the previous code snippet and points to the location that has CaffeOnSpark libraries.</span></span> 

## <a name="monitoring-and-troubleshooting"></a><span data-ttu-id="93b3a-190">Monitoraggio e risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="93b3a-190">Monitoring and troubleshooting</span></span>

<span data-ttu-id="93b3a-191">Nella modalità cluster YARN usata il driver Spark viene pianificato in un contenitore arbitrario e un nodo del ruolo di lavoro arbitrario. L'output visualizzato nella console dovrebbe quindi essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="93b3a-191">Since we are using YARN cluster mode, in which case the Spark driver will be scheduled to an arbitrary container (and an arbitrary worker node) you should only see in the console outputting something like:</span></span>

    17/02/01 23:22:16 INFO Client: Application report for application_1485916338528_0015 (state: RUNNING)

<span data-ttu-id="93b3a-192">Per conoscere i dettagli, in genere è necessario ottenere il log del driver Spark, che contiene altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="93b3a-192">If you want to know what happened, you usually need to get the Spark driver's log, which has more information.</span></span> <span data-ttu-id="93b3a-193">In questo caso è necessario passare all'interfaccia utente di YARN per trovare i relativi log.</span><span class="sxs-lookup"><span data-stu-id="93b3a-193">In this case, you need to go to the YARN UI to find the relevant YARN logs.</span></span> <span data-ttu-id="93b3a-194">L'interfaccia utente di YARN è disponibile all'URL seguente:</span><span class="sxs-lookup"><span data-stu-id="93b3a-194">You can get the YARN UI by this URL:</span></span> 

    https://yourclustername.azurehdinsight.net/yarnui
   
![Interfaccia utente di Yarn](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-1.png)

<span data-ttu-id="93b3a-196">È possibile esaminare il numero di risorse allocate per questa applicazione specifica.</span><span class="sxs-lookup"><span data-stu-id="93b3a-196">You can take a look at how many resources are allocated for this particular application.</span></span> <span data-ttu-id="93b3a-197">Facendo clic sul collegamento "Scheduler" (Utilità di pianificazione) si noterà che per questa applicazione vengono eseguiti nove contenitori.</span><span class="sxs-lookup"><span data-stu-id="93b3a-197">You can click the "Scheduler" link, and then you will see that for this application, there are 9 containers running.</span></span> <span data-ttu-id="93b3a-198">È stato chiesto a YARN di fornire otto executor, il nono contenitore è destinato al processo del driver.</span><span class="sxs-lookup"><span data-stu-id="93b3a-198">We ask YARN to provide 8 executors, and another container is for driver process.</span></span> 

![Utilità di pianificazione di YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-Scheduler.png)

<span data-ttu-id="93b3a-200">In caso di errore è consigliabile controllare i log del driver o del contenitore.</span><span class="sxs-lookup"><span data-stu-id="93b3a-200">You may want to check the  driver logs or container logs if there are failures.</span></span> <span data-ttu-id="93b3a-201">Per i log del driver, è possibile fare clic sull'ID applicazione nell'interfaccia utente di YARN e quindi fare clic sul pulsante "Logs" (Log).</span><span class="sxs-lookup"><span data-stu-id="93b3a-201">For driver logs, you can click the application ID in YARN UI, then click the "Logs" button.</span></span> <span data-ttu-id="93b3a-202">I log del driver sono scritti in STDERR.</span><span class="sxs-lookup"><span data-stu-id="93b3a-202">The driver logs are written into stderr.</span></span>

![Interfaccia utente 2 di YARN](./media/hdinsight-deep-learning-caffe-spark/YARN-UI-2.png)

<span data-ttu-id="93b3a-204">Ad esempio, l'errore seguente nei log del driver indica che sono stati allocati troppi executor.</span><span class="sxs-lookup"><span data-stu-id="93b3a-204">For example, you might see some of the error below from the driver logs, indicating you allocate too many executors.</span></span>

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

<span data-ttu-id="93b3a-205">In alcuni casi il problema si può verificare negli executor anziché nei driver.</span><span class="sxs-lookup"><span data-stu-id="93b3a-205">Sometimes, the issue can happen in executors rather than drivers.</span></span> <span data-ttu-id="93b3a-206">In tal caso è necessario controllare i log del contenitore.</span><span class="sxs-lookup"><span data-stu-id="93b3a-206">In this case, you need to check the container logs.</span></span> <span data-ttu-id="93b3a-207">È sempre possibile ottenere il log del contenitore del driver e quindi il contenitore in stato di errore.</span><span class="sxs-lookup"><span data-stu-id="93b3a-207">You can always get the container logs, and then get the failed container.</span></span> <span data-ttu-id="93b3a-208">Ad esempio, durante l'esecuzione di Caffe si può verificare questo errore:</span><span class="sxs-lookup"><span data-stu-id="93b3a-208">For example, you might meet this failure when running Caffe.</span></span>

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

<span data-ttu-id="93b3a-209">In tal caso è necessario ottenere l'ID del contenitore in stato di errore. Nell'esempio precedente si tratta di container_1485916338528_0008_05_000005.</span><span class="sxs-lookup"><span data-stu-id="93b3a-209">In this case, you need to get the failed container ID (in the above case, it is container_1485916338528_0008_05_000005).</span></span> <span data-ttu-id="93b3a-210">Quindi è necessario eseguire</span><span class="sxs-lookup"><span data-stu-id="93b3a-210">Then you need to run</span></span> 

    yarn logs -containerId container_1485916338528_0008_03_000005

<span data-ttu-id="93b3a-211">dal nodo head.</span><span class="sxs-lookup"><span data-stu-id="93b3a-211">from the headnode.</span></span> <span data-ttu-id="93b3a-212">L'errore del contenitore è dovuto all'uso della modalità GPU in lenet_memory_solver.prototxt, che invece prevede l'uso della modalità CPU.</span><span class="sxs-lookup"><span data-stu-id="93b3a-212">After checking container failure, it is caused by using GPU mode (where you should use CPU mode instead) in lenet_memory_solver.prototxt.</span></span>

    17/02/01 07:10:48 INFO LMDB: Batch size:100
    WARNING: Logging before InitGoogleLogging() is written to STDERR
    F0201 07:10:48.309725 11624 common.cpp:79] Cannot use GPU in CPU-only Caffe: check mode.


## <a name="getting-results"></a><span data-ttu-id="93b3a-213">Risultati</span><span class="sxs-lookup"><span data-stu-id="93b3a-213">Getting results</span></span>

<span data-ttu-id="93b3a-214">Con l'allocazione di otto executor in una topologia di rete così semplice, saranno sufficienti circa 30 minuti per ottenere i risultati.</span><span class="sxs-lookup"><span data-stu-id="93b3a-214">Since we are allocating 8 executors, and the network topology is simple, it should only take around 30 minutes to run the result.</span></span> <span data-ttu-id="93b3a-215">Dalla riga di comando si noterà che il modello è stato inserito in wasb:///mnist.model e i risultati sono stati inseriti in una cartella denominata wasb:///mnist_features_result.</span><span class="sxs-lookup"><span data-stu-id="93b3a-215">From the command line, you can see that we put the model to wasb:///mnist.model, and put the results to a folder named wasb:///mnist_features_result.</span></span>

<span data-ttu-id="93b3a-216">Per ottenere i risultati, eseguire:</span><span class="sxs-lookup"><span data-stu-id="93b3a-216">You can get the results by running</span></span>

    hadoop fs -cat hdfs:///mnist_features_result/*

<span data-ttu-id="93b3a-217">I risultati avranno un aspetto simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="93b3a-217">and the result looks like:</span></span>

    {"SampleID":"00009597","accuracy":[1.0],"loss":[0.028171852],"label":[2.0]}
    {"SampleID":"00009598","accuracy":[1.0],"loss":[0.028171852],"label":[6.0]}
    {"SampleID":"00009599","accuracy":[1.0],"loss":[0.028171852],"label":[1.0]}
    {"SampleID":"00009600","accuracy":[0.97],"loss":[0.0677709],"label":[5.0]}
    {"SampleID":"00009601","accuracy":[0.97],"loss":[0.0677709],"label":[0.0]}
    {"SampleID":"00009602","accuracy":[0.97],"loss":[0.0677709],"label":[1.0]}
    {"SampleID":"00009603","accuracy":[0.97],"loss":[0.0677709],"label":[2.0]}
    {"SampleID":"00009604","accuracy":[0.97],"loss":[0.0677709],"label":[3.0]}
    {"SampleID":"00009605","accuracy":[0.97],"loss":[0.0677709],"label":[4.0]}

<span data-ttu-id="93b3a-218">SampleID rappresenta l'ID nel set di dati MNIST e l'etichetta è il numero identificato dal modello.</span><span class="sxs-lookup"><span data-stu-id="93b3a-218">The SampleID represents the ID in the MNIST dataset, and the label is the number that the model identifies.</span></span>


## <a name="conclusion"></a><span data-ttu-id="93b3a-219">Conclusione</span><span class="sxs-lookup"><span data-stu-id="93b3a-219">Conclusion</span></span>

<span data-ttu-id="93b3a-220">Questo documento ha illustrato come installare CaffeOnSpark tramite l'esecuzione di un semplice esempio.</span><span class="sxs-lookup"><span data-stu-id="93b3a-220">In this documentation, you have tried to install CaffeOnSpark with running a simple example.</span></span> <span data-ttu-id="93b3a-221">HDInsight è una piattaforma cloud di calcolo distribuito completamente gestita. È la soluzione ideale per l'esecuzione di carichi di lavoro di apprendimento automatico e analisi avanzata in set di dati di grandi dimensioni, nonché per l'apprendimento avanzato distribuito. Per l'esecuzione di attività di apprendimento avanzato è possibile usare Caffe in HDInsight Spark.</span><span class="sxs-lookup"><span data-stu-id="93b3a-221">HDInsight is a full managed cloud distributed compute platform, and is the best place for running machine learning and advanced analytics workloads on large data set, and for distributed deep learning, you can use Caffe on HDInsight Spark to perform deep learning tasks.</span></span>


## <span data-ttu-id="93b3a-222"><a name="seealso"></a>Vedere anche</span><span class="sxs-lookup"><span data-stu-id="93b3a-222"><a name="seealso"></a>See also</span></span>
* [<span data-ttu-id="93b3a-223">Panoramica: Apache Spark su Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="93b3a-223">Overview: Apache Spark on Azure HDInsight</span></span>](hdinsight-apache-spark-overview.md)

### <a name="scenarios"></a><span data-ttu-id="93b3a-224">Scenari</span><span class="sxs-lookup"><span data-stu-id="93b3a-224">Scenarios</span></span>
* [<span data-ttu-id="93b3a-225">Spark con Machine Learning: usare Spark in HDInsight per l'analisi della temperatura di compilazione tramite dati HVAC</span><span class="sxs-lookup"><span data-stu-id="93b3a-225">Spark with Machine Learning: Use Spark in HDInsight for analyzing building temperature using HVAC data</span></span>](hdinsight-apache-spark-ipython-notebook-machine-learning.md)
* [<span data-ttu-id="93b3a-226">Spark con Machine Learning: usare Spark in HDInsight per prevedere i risultati del controllo degli alimenti</span><span class="sxs-lookup"><span data-stu-id="93b3a-226">Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)

### <a name="manage-resources"></a><span data-ttu-id="93b3a-227">Gestire risorse</span><span class="sxs-lookup"><span data-stu-id="93b3a-227">Manage resources</span></span>
* [<span data-ttu-id="93b3a-228">Gestire le risorse del cluster Apache Spark in Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="93b3a-228">Manage resources for the Apache Spark cluster in Azure HDInsight</span></span>](hdinsight-apache-spark-resource-manager.md)

