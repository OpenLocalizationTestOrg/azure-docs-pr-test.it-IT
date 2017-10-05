---
title: Installare e usare Giraph nei cluster Hadoop in HDInsight - Azure | Documentazione Microsoft
description: Informazioni su come personalizzare un cluster HDInsight con Giraph e su come usare Giraph.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 77a1d0e0-55de-4e61-98a0-060914fb7ca0
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: f0eb5c1f457380600463a370043f03e6d655a02c
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a>Installare e usare Giraph nei cluster HDInsight basati su Windows

Informazioni su come personalizzare i cluster HDInsight basati su Windows con Giraph usando Script azione e su come utilizzare Giraph per elaborare grafici su vasta scala. Per informazioni sull'uso di Giraph con un cluster basato su Linux, vedere [Installare Giraph nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).

> [!IMPORTANT]
> I passaggi descritti in questo documento funzionano solo con i cluster HDInsight basati su Windows. HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4. Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Per informazioni su come installare Giraph in un cluster HDInsight basato su Linux, vedere [Installare Giraph nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).


È possibile installare Giraph in qualsiasi tipo di cluster (Hadoop, Storm, HBase, Spark) su Azure HDInsight usando *Azione di script*. Uno script di esempio per l'installazione di Giraph in un cluster HDInsight è disponibile in un BLOB di archiviazione di sola lettura di Azure all'indirizzo [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1). Lo script di esempio funziona solo con cluster HDInsight versione 3.1. Per altre informazioni sulle versioni dei cluster HDInsight, vedere [Versioni cluster HDInsight](hdinsight-component-versioning.md).

**Articoli correlati**

* [Installare Giraph nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight
* [Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.
* [Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-giraph"></a>Che cos'è Giraph?
<a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> consente di elaborare grafici con Hadoop e può essere usato con Azure HDInsight. È possibile usare i grafici per modellare le relazioni tra gli oggetti, ad esempio le connessioni tra router in una rete di grandi dimensioni, come Internet, oppure le relazioni tra persone iscritte a social network, come nel cosiddetto grafico dei social network. Grazie all'elaborazione del grafico è possibile ottenere informazioni dettagliate sulle relazioni tra gli oggetti in un grafico e in particolare di:

* Identificare possibili amici sulla base delle relazioni correnti.
* Identificare la route più breve tra due computer di una rete.
* Calcolare la posizione in classifica di pagine Web.

## <a name="install-giraph-using-portal"></a>Installare Giraph tramite il portale
1. Avviare la creazione di un cluster usando l'opzione **CREAZIONE PERSONALIZZATA**, come descritto in [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md).
2. Nella pagina **Azioni script** della procedura guidata fare clic su **aggiungi azione script** per specificare i dettagli relativi all'azione script, come descritto di seguito:

    ![Usare l'azione script per personalizzare un cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "Usare l'azione script per personalizzare un cluster")

    <table border='1'>
        <tr><th>Proprietà</th><th>Valore</th></tr>
        <tr><td>Nome</td>
            <td>Specificare un nome per l'azione script. Ad esempio, <b>Installare Giraph</b>.</td></tr>
        <tr><td>URI script</td>
            <td>Specificare l'URI (Uniform Resource Identifier) dello script da richiamare per personalizzare il cluster. Ad esempio, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></td></tr>
        <tr><td>Tipo di nodo</td>
            <td>Specificare i nodi in cui viene eseguito lo script di personalizzazione. È possibile scegliere <b>Tutti i nodi</b>, <b>Solo nodi head</b> o <b>Solo nodi di lavoro</b>.
        <tr><td>Parametri</td>
            <td>Specificare i parametri, se richiesti dallo script. Lo script per installare Giraph non richiede alcun parametro, di conseguenza è possibile lasciare vuoto questo campo.</td></tr>
    </table>

    È possibile aggiungere altre azioni script per installare più componenti nel cluster. Dopo aver aggiunto gli script, fare clic sul segno di spunta per avviare la creazione del cluster.

## <a name="use-giraph"></a>Usare Giraph
L'esempio SimpleShortestPathsComputation viene usato per illustrare l'implementazione di base di <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> per trovare il percorso più breve tra oggetti di un grafico. Usare la procedura seguente per caricare i dati e il file JAR di esempio, eseguire un processo con l'esempio SimpleShortestPathsComputation e quindi visualizzare i risultati.

1. Caricare un file di dati di esempio nell'archiviazione BLOB di Azure. Nella workstation locale creare un nuovo file denominato **tiny_graph.txt**. Questo file deve contenere le righe seguenti:

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    Caricare il file tiny_graph.txt nella risorsa di archiviazione primaria per il cluster HDInsight. Per istruzioni su come caricare i dati, vedere [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).

    Questi dati descrivono una relazione tra gli oggetti in un grafico diretto, usando il formato [source\_id, source\_value,[[dest\_id], [edge\_value],...]]. Ogni riga rappresenta una relazione tra un oggetto **source\_id** e uno o più oggetti **dest\_id**. Il valore **edge\_value** (o peso) costituisce la potenza o la distanza della connessione tra **source_id** e **dest\_id**.

    I dati disegnati usando il valore (o peso) come distanza tra gli oggetti sono simili a quelli raffigurati di seguito:

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. Eseguire l'esempio SimpleShortestPathsComputation. Usare i cmdlet di Azure PowerShell seguenti per eseguire l'esempio specificando come input il file tiny_graph.txt.

    > [!IMPORTANT]
    > Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017. La procedura descritta in questo documento usa i nuovi cmdlet HDInsight, compatibili con Azure Resource Manager.
    >
    > Per installare la versione più recente, seguire la procedura descritta in [Come installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) . Se sono presenti script che devono essere modificati per l'uso dei nuovi cmdlet compatibili con Azure Resource Manager, per altre informazioni vedere [Migrazione a strumenti di sviluppo basati su Azure Resource Manager per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) .

    ```powershell
    $clusterName = "clustername"
    # Giraph examples jar
    $jarFile = "wasb:///example/jars/giraph-examples.jar"
    # Arguments for this job
    $jobArguments = "org.apache.giraph.examples.SimpleShortestPathsComputation",
                    "-ca", "mapred.job.tracker=headnodehost:9010",
                    "-vif", "org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat",
                    "-vip", "wasb:///example/data/tiny_graph.txt",
                    "-vof", "org.apache.giraph.io.formats.IdWithValueTextOutputFormat",
                    "-op",  "wasb:///example/output/shortestpaths",
                    "-w", "2"
    # Create the definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run the job, write output to the Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for the job to complete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display the standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    Nell'esempio precedente sostituire **clustername** con il nome del cluster HDInsight in cui è installato Giraph.
3. Visualizzare i risultati. Al termine del processo, i risultati verranno archiviati in due file di output nella cartella **wasb:///example/out/shotestpaths**. I file sono denominati **part-m-00001** e **part-m-00002**. Eseguire la procedura seguente per scaricare e visualizzare l'output:

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select the current subscription
    Select-AzureSubscription $subscriptionName

    # Create the Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download the job output to the workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    Nella directory attuale della workstation verrà creata la struttura di directory **example/output/shortestpaths** e i due file di output verranno scaricati in questo percorso.

    Usare il cmdlet **Cat** per visualizzare i contenuti dei file:

        Cat example/output/shortestpaths/part*

    L'output sarà simile al seguente:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    L'esempio SimpleShortestPathComputation è hardcoded in modo da essere avviato con l'ID oggetto 1 e individuare il percorso più breve ad altri oggetti. L'output dovrebbe quindi essere `destination_id distance`, in cui distance è il valore (o il peso) dei confini attraversati tra l'ID oggetto 1 e l'ID di destinazione.

    Con questa visualizzazione è possibile verificare i risultati attraversando i percorsi più brevi tra l'ID 1 e tutti gli altri oggetti. Notare che il percorso più breve tra l'ID 1 e l'ID 4 è 5, che corrisponde alla distanza totale tra <span style="color:orange">ID 1 e 3</span> e quindi tra <span style="color:red">ID 3 e 4</span>.

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a>Installare Giraph tramite Aure PowerShell
Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  L'esempio illustra come installare Spark tramite Azure PowerShell. È necessario personalizzare lo script da usare [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="install-giraph-using-net-sdk"></a>Installare Giraph tramite .NET SDK
Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). L'esempio illustra come installare Spark tramite .NET SDK. È necessario personalizzare lo script da usare [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="see-also"></a>Vedere anche
* [Installare Giraph nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight
* [Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.
* [Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)
* [Installare e usare Spark nei cluster HDInsight][hdinsight-install-spark]: esempio di azione script sull'installazione di Spark.
* [Installare R nei cluster HDInsight][hdinsight-install-r]: esempio di azione script sull'installazione di R.
* [Installare Solr nei cluster HDInsight](hdinsight-hadoop-solr-install.md): esempio di Azione di script sull'installazione di Solr.

[tools]: https://github.com/Blackmist/hdinsight-tools
[aps]: http://azure.microsoft.com/documentation/articles/install-configure-powershell/

[powershell-install]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
