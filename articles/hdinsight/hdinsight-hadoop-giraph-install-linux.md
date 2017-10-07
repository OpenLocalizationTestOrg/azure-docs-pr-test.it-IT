---
title: aaaInstall e utilizzare Giraph in HDInsight (Hadoop) - Azure | Documenti Microsoft
description: "Informazioni su come i cluster usando le azioni Script tooinstall Giraph in HDInsight basati su Linux. Azioni script consentono di cluster hello toocustomize durante la creazione, modifica della configurazione del cluster o l'installazione di servizi e le utilità."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a><span data-ttu-id="1d839-104">Installare Giraph nei cluster HDInsight Hadoop e usare i grafici di Giraph tooprocess su larga scala</span><span class="sxs-lookup"><span data-stu-id="1d839-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph tooprocess large-scale graphs</span></span>

<span data-ttu-id="1d839-105">Informazioni su come tooinstall Giraph Apache in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1d839-105">Learn how tooinstall Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="1d839-106">Hello script azione di HDInsight consente toocustomize il cluster eseguendo uno script bash.</span><span class="sxs-lookup"><span data-stu-id="1d839-106">hello script action feature of HDInsight allows you toocustomize your cluster by running a bash script.</span></span> <span data-ttu-id="1d839-107">Gli script possono essere utilizzato toocustomize cluster durante e dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="1d839-107">Scripts can be used toocustomize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1d839-108">passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux.</span><span class="sxs-lookup"><span data-stu-id="1d839-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="1d839-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="1d839-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1d839-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1d839-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="1d839-111"><a name="whatis"></a>Che cos'è Giraph?</span><span class="sxs-lookup"><span data-stu-id="1d839-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="1d839-112">[Apache Giraph](http://giraph.apache.org/) consente grafico tooperform elaborazione tramite Hadoop e può essere utilizzato con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1d839-112">[Apache Giraph](http://giraph.apache.org/) allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="1d839-113">È possibile usare i grafici per modellare le relazioni tra gli oggetti,</span><span class="sxs-lookup"><span data-stu-id="1d839-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="1d839-114">Ad esempio, le connessioni hello tra i router in una rete di grandi dimensioni come hello Internet o le relazioni tra gli utenti su social network.</span><span class="sxs-lookup"><span data-stu-id="1d839-114">For example, hello connections between routers on a large network like hello Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="1d839-115">Elaborazione Graph consente tooreason sulle relazioni hello tra gli oggetti in un grafico, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="1d839-115">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="1d839-116">Identificare possibili amici sulla base delle relazioni correnti.</span><span class="sxs-lookup"><span data-stu-id="1d839-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="1d839-117">Identificazione hello itinerario più breve tra due computer in una rete.</span><span class="sxs-lookup"><span data-stu-id="1d839-117">Identifying hello shortest route between two computers in a network.</span></span>

* <span data-ttu-id="1d839-118">Calcolare il numero di dimensioni di hello pagina delle pagine Web.</span><span class="sxs-lookup"><span data-stu-id="1d839-118">Calculating hello page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="1d839-119">I componenti forniti con i cluster di HDInsight hello sono completamente supportati: supporto di Microsoft consente tooisolate e risolvere i problemi correlati toothese componenti.</span><span class="sxs-lookup"><span data-stu-id="1d839-119">Components provided with hello HDInsight cluster are fully supported - Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="1d839-120">I componenti personalizzati, ad esempio Giraph, ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-120">Custom components, such as Giraph, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="1d839-121">Supporto Microsoft potrebbe essere in grado di tooresolving problema di hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-121">Microsoft Support may be able tooresolving hello issue.</span></span> <span data-ttu-id="1d839-122">In caso contrario, è necessario consultare le community open source, da cui è possibile ottenere supporto approfondito per la tecnologia specifica.</span><span class="sxs-lookup"><span data-stu-id="1d839-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="1d839-123">È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="1d839-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-hello-script-does"></a><span data-ttu-id="1d839-124">Quali script hello esegue</span><span class="sxs-lookup"><span data-stu-id="1d839-124">What hello script does</span></span>

<span data-ttu-id="1d839-125">Questo script esegue hello seguenti azioni:</span><span class="sxs-lookup"><span data-stu-id="1d839-125">This script performs hello following actions:</span></span>

* <span data-ttu-id="1d839-126">Installa troppo Giraph`/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="1d839-126">Installs Giraph too`/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="1d839-127">Hello copie `giraph-examples.jar` toodefault archiviazione (WASB) per il cluster di file:`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="1d839-127">Copies hello `giraph-examples.jar` file toodefault storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="1d839-128"><a name="install"></a>Installare Giraph mediante azioni script</span><span class="sxs-lookup"><span data-stu-id="1d839-128"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="1d839-129">Un tooinstall di script di esempio Giraph in un cluster HDInsight è disponibile in hello seguente posizione:</span><span class="sxs-lookup"><span data-stu-id="1d839-129">A sample script tooinstall Giraph on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="1d839-130">In questa sezione vengono fornite istruzioni su come toouse hello script di esempio durante la creazione di cluster hello utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="1d839-130">This section provides instructions on how toouse hello sample script while creating hello cluster by using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="1d839-131">Un'azione di script può essere applicata utilizzando uno dei seguenti metodi hello:</span><span class="sxs-lookup"><span data-stu-id="1d839-131">A script action can be applied using any of hello following methods:</span></span>
> * <span data-ttu-id="1d839-132">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="1d839-132">Azure PowerShell</span></span>
> * <span data-ttu-id="1d839-133">Hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="1d839-133">hello Azure CLI</span></span>
> * <span data-ttu-id="1d839-134">Hello HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="1d839-134">hello HDInsight .NET SDK</span></span>
> * <span data-ttu-id="1d839-135">Modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="1d839-135">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="1d839-136">È inoltre possibile applicare tooalready azioni script i cluster in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="1d839-136">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="1d839-137">Per altre informazioni, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1d839-137">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="1d839-138">Avviare la creazione di un cluster attenendosi alla procedura hello in [cluster HDInsight basati su Linux creare](hdinsight-hadoop-create-linux-clusters-portal.md), ma non completare la creazione.</span><span class="sxs-lookup"><span data-stu-id="1d839-138">Start creating a cluster by using hello steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="1d839-139">In hello **configurazione facoltativa** pannello seleziona **azioni Script**e fornire hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="1d839-139">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="1d839-140">**NOME**: immettere un nome descrittivo per l'azione script hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-140">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="1d839-141">**URI SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="1d839-141">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="1d839-142">**HEAD**: selezionare questa voce</span><span class="sxs-lookup"><span data-stu-id="1d839-142">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="1d839-143">**LAVORO**: lasciare questa voce deselezionata</span><span class="sxs-lookup"><span data-stu-id="1d839-143">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="1d839-144">**ZOOKEEPER**: lasciare questa voce deselezionata</span><span class="sxs-lookup"><span data-stu-id="1d839-144">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="1d839-145">**PARAMETRI**: lasciare questo campo vuoto</span><span class="sxs-lookup"><span data-stu-id="1d839-145">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="1d839-146">Nella parte inferiore di hello di hello **azioni Script**, utilizzare hello **selezionare** configurazione hello toosave dei pulsanti.</span><span class="sxs-lookup"><span data-stu-id="1d839-146">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="1d839-147">Infine, utilizzare hello **selezionare** pulsante nella parte inferiore di hello di hello **configurazione facoltativa** informazioni di configurazione facoltativa hello toosave blade.</span><span class="sxs-lookup"><span data-stu-id="1d839-147">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

4. <span data-ttu-id="1d839-148">Continuare con la creazione di cluster hello come descritto in [cluster HDInsight basati su Linux creare](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="1d839-148">Continue creating hello cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="1d839-149"><a name="usegiraph"></a>Come si usa Giraph in HDInsight?</span><span class="sxs-lookup"><span data-stu-id="1d839-149"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="1d839-150">Dopo aver creato il cluster hello, utilizzare hello passaggi toorun hello SimpleShortestPathsComputation esempio incluso in Giraph seguente.</span><span class="sxs-lookup"><span data-stu-id="1d839-150">Once hello cluster has been created, use hello following steps toorun hello SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="1d839-151">Questo esempio viene utilizzato basic hello [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementazione per trovare il percorso più breve di hello tra gli oggetti in un grafico.</span><span class="sxs-lookup"><span data-stu-id="1d839-151">This example uses hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding hello shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="1d839-152">Connettere il cluster di HDInsight toohello tramite SSH:</span><span class="sxs-lookup"><span data-stu-id="1d839-152">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="1d839-153">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1d839-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="1d839-154">Comando che segue hello utilizzare toocreate un file denominato **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="1d839-154">Use hello following command toocreate a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="1d839-155">Utilizzare hello segue testo come contenuto di hello di questo file:</span><span class="sxs-lookup"><span data-stu-id="1d839-155">Use hello following text as hello contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="1d839-156">Questi dati descrivono una relazione tra gli oggetti in un grafico diretto, utilizzando il formato di hello `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="1d839-156">This data describes a relationship between objects in a directed graph, by using hello format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="1d839-157">Ogni riga rappresenta una relazione tra un oggetto `source_id` e uno o più oggetti `dest_id`.</span><span class="sxs-lookup"><span data-stu-id="1d839-157">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="1d839-158">Hello `edge_value` può essere considerato come livello di attendibilità hello o una distanza di connessione hello tra `source_id` e `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="1d839-158">hello `edge_value` can be thought of as hello strength or distance of hello connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="1d839-159">Disegnare out, e utilizza il valore hello (o peso) come distanza hello tra oggetti, dati hello potrebbero essere simile hello seguente diagramma:</span><span class="sxs-lookup"><span data-stu-id="1d839-159">Drawn out, and using hello value (or weight) as hello distance between objects, hello data might look like hello following diagram:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="1d839-161">file hello toosave, usare **Ctrl + X**, quindi **Y**e infine **invio** tooaccept nome del file hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-161">toosave hello file, use **Ctrl+X**, then **Y**, and finally **Enter** tooaccept hello file name.</span></span>

4. <span data-ttu-id="1d839-162">Utilizzare hello seguente dati hello toostore nell'account di archiviazione primario per il cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="1d839-162">Use hello following toostore hello data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="1d839-163">Eseguire l'esempio SimpleShortestPathsComputation hello utilizzando hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d839-163">Run hello SimpleShortestPathsComputation example using hello following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="1d839-164">parametri di Hello utilizzati con questo comando vengono descritti in hello nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="1d839-164">hello parameters used with this command are described in hello following table:</span></span>

   | <span data-ttu-id="1d839-165">.</span><span class="sxs-lookup"><span data-stu-id="1d839-165">Parameter</span></span> | <span data-ttu-id="1d839-166">Risultato</span><span class="sxs-lookup"><span data-stu-id="1d839-166">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="1d839-167">file jar Hello contenente esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-167">hello jar file containing hello examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="1d839-168">classe Hello utilizzato negli esempi di hello toostart.</span><span class="sxs-lookup"><span data-stu-id="1d839-168">hello class used toostart hello examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="1d839-169">esempio Hello utilizzato.</span><span class="sxs-lookup"><span data-stu-id="1d839-169">hello example that is used.</span></span> <span data-ttu-id="1d839-170">In questo esempio calcola percorso più breve di hello tra ID 1 e tutti gli altri ID grafico hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-170">In this example, it computes hello shortest path between ID 1 and all other IDs in hello graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="1d839-171">nodo head Hello per cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-171">hello headnode for hello cluster.</span></span> |
   | `-vif` |<span data-ttu-id="1d839-172">Hello toouse di formato di input per i dati di input hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-172">hello input format toouse for hello input data.</span></span> |
   | `-vip` |<span data-ttu-id="1d839-173">file di dati di input Hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-173">hello input data file.</span></span> |
   | `-vof` |<span data-ttu-id="1d839-174">formato di output di Hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-174">hello output format.</span></span> <span data-ttu-id="1d839-175">In questo caso, ID e valore come testo normale.</span><span class="sxs-lookup"><span data-stu-id="1d839-175">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="1d839-176">percorso di output di Hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-176">hello output location.</span></span> |
   | `-w 2` |<span data-ttu-id="1d839-177">numero di Hello di toouse processi di lavoro.</span><span class="sxs-lookup"><span data-stu-id="1d839-177">hello number of workers toouse.</span></span> <span data-ttu-id="1d839-178">In questo esempio, 2.</span><span class="sxs-lookup"><span data-stu-id="1d839-178">In this example, 2.</span></span> |

    <span data-ttu-id="1d839-179">Per ulteriori informazioni su questi e altri parametri utilizzati con Giraph esempi, vedere hello [delle Guide rapide Giraph](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="1d839-179">For more information on these, and other parameters used with Giraph samples, see hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="1d839-180">Al termine il processo di hello, risultati di hello vengono archiviati in hello **/example/out/shotestpaths** directory.</span><span class="sxs-lookup"><span data-stu-id="1d839-180">Once hello job has finished, hello results are stored in hello **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="1d839-181">Hello nomi file di output iniziano con **parte-m -** e terminare con un numero che indica in primo luogo, in secondo luogo, hello file e così via.</span><span class="sxs-lookup"><span data-stu-id="1d839-181">hello output file names begin with **part-m-** and end with a number indicating hello first, second, etc. file.</span></span> <span data-ttu-id="1d839-182">Utilizzare hello output hello tooview del comando seguente:</span><span class="sxs-lookup"><span data-stu-id="1d839-182">Use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="1d839-183">output di Hello risulterà simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="1d839-183">hello output should appear similar toohello following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="1d839-184">esempio SimpleShortestPathComputation Hello è hardcoded toostart con ID 1 oggetto e trovare gli oggetti tooother percorso più brevi hello.</span><span class="sxs-lookup"><span data-stu-id="1d839-184">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="1d839-185">output di Hello è nel formato hello `destination_id` e `distance`.</span><span class="sxs-lookup"><span data-stu-id="1d839-185">hello output is in hello format of `destination_id` and `distance`.</span></span> <span data-ttu-id="1d839-186">Hello `distance` è hello valore (o peso), dei bordi hello percorsi compreso tra 1 ID oggetto e hello ID di destinazione.</span><span class="sxs-lookup"><span data-stu-id="1d839-186">hello `distance` is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="1d839-187">Visualizzazione dei dati, è possibile verificare i risultati di hello viaggiando percorsi più brevi hello tra ID 1 e tutti gli altri oggetti.</span><span class="sxs-lookup"><span data-stu-id="1d839-187">Visualizing this data, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="1d839-188">percorso più breve di Hello tra ID 1 e 4 ID è 5.</span><span class="sxs-lookup"><span data-stu-id="1d839-188">hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="1d839-189">Questo valore è hello totale distanza <span style="color:orange">ID 1 e 3</span>e quindi <span style="color:red">ID 3 e 4</span>.</span><span class="sxs-lookup"><span data-stu-id="1d839-189">This value is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="1d839-191">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1d839-191">Next steps</span></span>

* <span data-ttu-id="1d839-192">[Installare e usare Hue nei cluster HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1d839-192">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="1d839-193">[Installare Solr in cluster HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="1d839-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
