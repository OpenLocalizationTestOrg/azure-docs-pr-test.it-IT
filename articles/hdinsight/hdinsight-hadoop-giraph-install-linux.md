---
title: Installare e usare Giraph in HDInsight (Hadoop) - Azure | Documentazione Microsoft
description: "Informazioni su come installare Giraph nei cluster HDInsight basati su Linux utilizzando azioni di Script. Le azioni di script consentono di personalizzare il cluster durante la creazione, modificando la configurazione del cluster o installando servizi e utilità."
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
ms.openlocfilehash: 6e2f6983e00f874420f7f0907dbc68185f0af713
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-to-process-large-scale-graphs"></a><span data-ttu-id="3153f-104">Installare Giraph nei cluster HDInsight Hadoop e usarlo per elaborare grafici su vasta scala</span><span class="sxs-lookup"><span data-stu-id="3153f-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph to process large-scale graphs</span></span>

<span data-ttu-id="3153f-105">Informazioni su come installare Apache Giraph in un cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3153f-105">Learn how to install Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="3153f-106">La funzione di azione script di HDInsight consente di personalizzare il cluster eseguendo uno script bash.</span><span class="sxs-lookup"><span data-stu-id="3153f-106">The script action feature of HDInsight allows you to customize your cluster by running a bash script.</span></span> <span data-ttu-id="3153f-107">È possibile usare gli script per personalizzare i cluster sia durante che dopo la creazione del cluster.</span><span class="sxs-lookup"><span data-stu-id="3153f-107">Scripts can be used to customize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3153f-108">I passaggi descritti in questo documento richiedono un cluster HDInsight che usa Linux.</span><span class="sxs-lookup"><span data-stu-id="3153f-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="3153f-109">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="3153f-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="3153f-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="3153f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="3153f-111"><a name="whatis"></a>Che cos'è Giraph?</span><span class="sxs-lookup"><span data-stu-id="3153f-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="3153f-112">[Apache Giraph](http://giraph.apache.org/) consente di elaborare grafici con Hadoop e può essere usato con Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="3153f-112">[Apache Giraph](http://giraph.apache.org/) allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="3153f-113">È possibile usare i grafici per modellare le relazioni tra gli oggetti,</span><span class="sxs-lookup"><span data-stu-id="3153f-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="3153f-114">ad esempio le connessioni tra router in una rete di grandi dimensioni, come Internet, oppure le relazioni tra persone iscritte a social network.</span><span class="sxs-lookup"><span data-stu-id="3153f-114">For example, the connections between routers on a large network like the Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="3153f-115">Grazie all'elaborazione del grafico è possibile ottenere informazioni dettagliate sulle relazioni tra gli oggetti in un grafico e in particolare di:</span><span class="sxs-lookup"><span data-stu-id="3153f-115">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="3153f-116">Identificare possibili amici sulla base delle relazioni correnti.</span><span class="sxs-lookup"><span data-stu-id="3153f-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="3153f-117">Identificare la route più breve tra due computer di una rete.</span><span class="sxs-lookup"><span data-stu-id="3153f-117">Identifying the shortest route between two computers in a network.</span></span>

* <span data-ttu-id="3153f-118">Calcolare la posizione in classifica di pagine Web.</span><span class="sxs-lookup"><span data-stu-id="3153f-118">Calculating the page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="3153f-119">I componenti forniti con il cluster HDInsight sono supportati in modo completo e il supporto tecnico Microsoft contribuirà a isolare e risolvere i problemi correlati a questi componenti.</span><span class="sxs-lookup"><span data-stu-id="3153f-119">Components provided with the HDInsight cluster are fully supported - Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="3153f-120">I componenti personalizzati, ad esempio Giraph, ricevono supporto commercialmente ragionevole per semplificare la risoluzione dei problemi.</span><span class="sxs-lookup"><span data-stu-id="3153f-120">Custom components, such as Giraph, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="3153f-121">È possibile che il supporto tecnico Microsoft sia in grado di risolvere il problema.</span><span class="sxs-lookup"><span data-stu-id="3153f-121">Microsoft Support may be able to resolving the issue.</span></span> <span data-ttu-id="3153f-122">In caso contrario, è necessario consultare le community open source, da cui è possibile ottenere supporto approfondito per la tecnologia specifica.</span><span class="sxs-lookup"><span data-stu-id="3153f-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="3153f-123">È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="3153f-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="3153f-124">Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="3153f-124">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-the-script-does"></a><span data-ttu-id="3153f-125">Funzionalità dello script</span><span class="sxs-lookup"><span data-stu-id="3153f-125">What the script does</span></span>

<span data-ttu-id="3153f-126">Lo script esegue le azioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3153f-126">This script performs the following actions:</span></span>

* <span data-ttu-id="3153f-127">Installa Giraph in `/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="3153f-127">Installs Giraph to `/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="3153f-128">Copia il file `giraph-examples.jar` nell'archivio BLOB di Azure (WASB) predefinito del cluster: `/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="3153f-128">Copies the `giraph-examples.jar` file to default storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="3153f-129"><a name="install"></a>Installare Giraph mediante azioni script</span><span class="sxs-lookup"><span data-stu-id="3153f-129"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="3153f-130">Uno script di esempio per l'installazione di Giraph in un cluster HDInsight è disponibile all'indirizzo seguente:</span><span class="sxs-lookup"><span data-stu-id="3153f-130">A sample script to install Giraph on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="3153f-131">Questa sezione fornisce istruzioni su come usare lo script di esempio quando si crea il cluster usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3153f-131">This section provides instructions on how to use the sample script while creating the cluster by using the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="3153f-132">Un'azione script può essere applicata usando uno dei metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="3153f-132">A script action can be applied using any of the following methods:</span></span>
> * <span data-ttu-id="3153f-133">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="3153f-133">Azure PowerShell</span></span>
> * <span data-ttu-id="3153f-134">Interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="3153f-134">The Azure CLI</span></span>
> * <span data-ttu-id="3153f-135">HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="3153f-135">The HDInsight .NET SDK</span></span>
> * <span data-ttu-id="3153f-136">Modelli di Gestione risorse di Azure</span><span class="sxs-lookup"><span data-stu-id="3153f-136">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="3153f-137">È anche possibile applicare azioni script a cluster già in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="3153f-137">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="3153f-138">Per altre informazioni, vedere [Personalizzare cluster HDInsight basati su Linux tramite Azione script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3153f-138">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="3153f-139">Avviare la creazione di un cluster utilizzando la procedura descritta in [Creazione di cluster HDInsight basati su Linux](hdinsight-hadoop-create-linux-clusters-portal.md), ma non completare la creazione.</span><span class="sxs-lookup"><span data-stu-id="3153f-139">Start creating a cluster by using the steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="3153f-140">Nel pannello **Configurazione facoltativa** selezionare **Azioni script** e specificare le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="3153f-140">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="3153f-141">**NOME**: immettere un nome descrittivo per l'azione script.</span><span class="sxs-lookup"><span data-stu-id="3153f-141">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="3153f-142">**URI SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="3153f-142">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="3153f-143">**HEAD**: selezionare questa voce</span><span class="sxs-lookup"><span data-stu-id="3153f-143">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="3153f-144">**LAVORO**: lasciare questa voce deselezionata</span><span class="sxs-lookup"><span data-stu-id="3153f-144">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="3153f-145">**ZOOKEEPER**: lasciare questa voce deselezionata</span><span class="sxs-lookup"><span data-stu-id="3153f-145">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="3153f-146">**PARAMETRI**: lasciare questo campo vuoto</span><span class="sxs-lookup"><span data-stu-id="3153f-146">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="3153f-147">Nella parte inferiore di **Azioni di script** usare il pulsante **Seleziona** per salvare la configurazione.</span><span class="sxs-lookup"><span data-stu-id="3153f-147">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="3153f-148">Usare infine il pulsante **Seleziona** nella parte inferiore del pannello **Configurazione facoltativa** per salvare le informazioni relative alla configurazione facoltativa.</span><span class="sxs-lookup"><span data-stu-id="3153f-148">Finally, use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

4. <span data-ttu-id="3153f-149">Continuare a creare il cluster come descritto nell'argomento relativo alla [creazione di cluster HDInsight basati su Linux](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="3153f-149">Continue creating the cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="3153f-150"><a name="usegiraph"></a>Come si usa Giraph in HDInsight?</span><span class="sxs-lookup"><span data-stu-id="3153f-150"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="3153f-151">Dopo aver creato il cluster, usare la procedura seguente per eseguire l'esempio SimpleShortestPathsComputation incluso in Giraph.</span><span class="sxs-lookup"><span data-stu-id="3153f-151">Once the cluster has been created, use the following steps to run the SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="3153f-152">Viene usata l'implementazione di base di [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) per trovare il percorso più breve tra gli oggetti in un grafico.</span><span class="sxs-lookup"><span data-stu-id="3153f-152">This example uses the basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding the shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="3153f-153">Connettersi al cluster HDInsight usando SSH:</span><span class="sxs-lookup"><span data-stu-id="3153f-153">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="3153f-154">Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="3153f-154">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="3153f-155">Usare il comando seguente per creare un file denominato **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="3153f-155">Use the following command to create a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="3153f-156">Usare il testo seguente come contenuto del file:</span><span class="sxs-lookup"><span data-stu-id="3153f-156">Use the following text as the contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="3153f-157">Questi dati descrivono una relazione tra gli oggetti in un grafico diretto, usando il formato `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="3153f-157">This data describes a relationship between objects in a directed graph, by using the format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="3153f-158">Ogni riga rappresenta una relazione tra un oggetto `source_id` e uno o più oggetti `dest_id`.</span><span class="sxs-lookup"><span data-stu-id="3153f-158">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="3153f-159">Il valore `edge_value` può essere considerato come la potenza o la distanza della connessione tra `source_id` e `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="3153f-159">The `edge_value` can be thought of as the strength or distance of the connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="3153f-160">I dati disegnati usando il valore (o peso) come distanza tra gli oggetti possono essere simili a quelli raffigurati nel diagramma seguente:</span><span class="sxs-lookup"><span data-stu-id="3153f-160">Drawn out, and using the value (or weight) as the distance between objects, the data might look like the following diagram:</span></span>

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="3153f-162">Per salvare il file usare **CTRL+X**, quindi **Y** e infine premere **INVIO** per accettare il nome del file.</span><span class="sxs-lookup"><span data-stu-id="3153f-162">To save the file, use **Ctrl+X**, then **Y**, and finally **Enter** to accept the file name.</span></span>

4. <span data-ttu-id="3153f-163">Usare il codice seguente per archiviare i dati nell'archiviazione primaria del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="3153f-163">Use the following to store the data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="3153f-164">Eseguire l'esempio SimpleShortestPathsComputation con il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="3153f-164">Run the SimpleShortestPathsComputation example using the following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="3153f-165">I parametri usati con questo comando sono descritti nella tabella seguente:</span><span class="sxs-lookup"><span data-stu-id="3153f-165">The parameters used with this command are described in the following table:</span></span>

   | <span data-ttu-id="3153f-166">Parametro</span><span class="sxs-lookup"><span data-stu-id="3153f-166">Parameter</span></span> | <span data-ttu-id="3153f-167">Risultato</span><span class="sxs-lookup"><span data-stu-id="3153f-167">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="3153f-168">File JAR contenente gli esempi.</span><span class="sxs-lookup"><span data-stu-id="3153f-168">The jar file containing the examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="3153f-169">Classe usata per avviare gli esempi.</span><span class="sxs-lookup"><span data-stu-id="3153f-169">The class used to start the examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="3153f-170">L'esempio usato.</span><span class="sxs-lookup"><span data-stu-id="3153f-170">The example that is used.</span></span> <span data-ttu-id="3153f-171">In questo esempio, viene calcolato il percorso più breve tra ID 1 e tutti gli altri ID nel grafico.</span><span class="sxs-lookup"><span data-stu-id="3153f-171">In this example, it computes the shortest path between ID 1 and all other IDs in the graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="3153f-172">Nodo head del cluster.</span><span class="sxs-lookup"><span data-stu-id="3153f-172">The headnode for the cluster.</span></span> |
   | `-vif` |<span data-ttu-id="3153f-173">Formato di input da usare per i dati di input.</span><span class="sxs-lookup"><span data-stu-id="3153f-173">The input format to use for the input data.</span></span> |
   | `-vip` |<span data-ttu-id="3153f-174">File di dati di input.</span><span class="sxs-lookup"><span data-stu-id="3153f-174">The input data file.</span></span> |
   | `-vof` |<span data-ttu-id="3153f-175">Formato di output.</span><span class="sxs-lookup"><span data-stu-id="3153f-175">The output format.</span></span> <span data-ttu-id="3153f-176">In questo caso, ID e valore come testo normale.</span><span class="sxs-lookup"><span data-stu-id="3153f-176">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="3153f-177">Percorso di output.</span><span class="sxs-lookup"><span data-stu-id="3153f-177">The output location.</span></span> |
   | `-w 2` |<span data-ttu-id="3153f-178">Numero di ruoli di lavoro da usare.</span><span class="sxs-lookup"><span data-stu-id="3153f-178">The number of workers to use.</span></span> <span data-ttu-id="3153f-179">In questo esempio, 2.</span><span class="sxs-lookup"><span data-stu-id="3153f-179">In this example, 2.</span></span> |

    <span data-ttu-id="3153f-180">Per altre informazioni su questi e altri parametri usati con gli esempi di Giraph, vedere la [Guida introduttiva a Giraph](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="3153f-180">For more information on these, and other parameters used with Giraph samples, see the [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="3153f-181">Al termine del processo, i risultati vengono archiviati nella directory **/example/out/shortestpaths**.</span><span class="sxs-lookup"><span data-stu-id="3153f-181">Once the job has finished, the results are stored in the **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="3153f-182">I file di output iniziano con **part-m-** e terminano con un numero che indica il primo file, il secondo e così via.</span><span class="sxs-lookup"><span data-stu-id="3153f-182">The output file names begin with **part-m-** and end with a number indicating the first, second, etc. file.</span></span> <span data-ttu-id="3153f-183">Usare il comando seguente per visualizzare l'output:</span><span class="sxs-lookup"><span data-stu-id="3153f-183">Use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="3153f-184">L'output sarà simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="3153f-184">The output should appear similar to the following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="3153f-185">L'esempio SimpleShortestPathComputation è hardcoded in modo da essere avviato con l'ID oggetto 1 e individuare il percorso più breve ad altri oggetti.</span><span class="sxs-lookup"><span data-stu-id="3153f-185">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="3153f-186">L'output è in formato `destination_id` e `distance`.</span><span class="sxs-lookup"><span data-stu-id="3153f-186">The output is in the format of `destination_id` and `distance`.</span></span> <span data-ttu-id="3153f-187">In particolare, `distance` rappresenta il valore (o il peso) dei confini attraversati tra l'oggetto ID 1 e l'ID di destinazione.</span><span class="sxs-lookup"><span data-stu-id="3153f-187">The `distance` is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="3153f-188">Con questa visualizzazione dei dati è possibile verificare i risultati attraversando i percorsi più brevi tra ID 1 e tutti gli altri oggetti.</span><span class="sxs-lookup"><span data-stu-id="3153f-188">Visualizing this data, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="3153f-189">Osservare come il percorso più breve tra ID 1 e ID 4 sia 5,</span><span class="sxs-lookup"><span data-stu-id="3153f-189">The shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="3153f-190">che corrisponde alla distanza totale tra <span style="color:orange">ID 1 e 3</span> e quindi tra <span style="color:red">ID 3 e 4</span>.</span><span class="sxs-lookup"><span data-stu-id="3153f-190">This value is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="3153f-192">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3153f-192">Next steps</span></span>

* <span data-ttu-id="3153f-193">[Installare e usare Hue nei cluster HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3153f-193">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="3153f-194">[Installare Solr in cluster HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="3153f-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
