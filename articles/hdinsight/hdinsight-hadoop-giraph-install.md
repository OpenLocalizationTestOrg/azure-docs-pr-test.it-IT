---
title: cluster aaaInstall e utilizzare Giraph in Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come cluster di HDInsight toocustomize con Giraph e come toouse Giraph.
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
ms.openlocfilehash: bd473faca9d3c87c29d7566a18fc94211c50f059
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-giraph-on-windows-based-hdinsight-clusters"></a>Installare e usare Giraph nei cluster HDInsight basati su Windows

Informazioni su come toocustomize Windows basato su cluster HDInsight con Giraph mediante l'azione di Script e come toouse Giraph tooprocess su larga scala grafici. Per informazioni sull'uso di Giraph con un cluster basato su Linux, vedere [Installare Giraph nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md).

> [!IMPORTANT]
> Hello passaggi di questa operazione solo documenti con i cluster HDInsight basati su Windows. HDInsight è disponibile in Windows solo per le versioni precedenti a HDInsight 3.4. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). Per informazioni su come tooinstall Giraph in un cluster HDInsight basati su Linux, vedere [Giraph installare nei cluster HDInsight Hadoop (Linux)](hdinsight-hadoop-giraph-install-linux.md).


È possibile installare Giraph in qualsiasi tipo di cluster (Hadoop, Storm, HBase, Spark) su Azure HDInsight usando *Azione di script*. Un tooinstall di script di esempio Giraph in un cluster HDInsight è disponibile da un blob di archiviazione di Azure di sola lettura in [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1). script di esempio Hello funziona solo con versione 3.1 del cluster HDInsight. Per altre informazioni sulle versioni dei cluster HDInsight, vedere [Versioni cluster HDInsight](hdinsight-component-versioning.md).

**Articoli correlati**

* [Installare Giraph nei cluster Hadoop di HDInsight (Linux)](hdinsight-hadoop-giraph-install-linux.md)
* [Creare cluster Hadoop in HDInsight](hdinsight-provision-clusters.md): informazioni generali sulla creazione di cluster HDInsight
* [Personalizzare cluster HDInsight mediante l'azione Script][hdinsight-cluster-customize]: informazioni generali sulla personalizzazione di cluster HDInsight tramite Azione script.
* [Sviluppare script di Azione script per HDInsight](hdinsight-hadoop-script-actions.md)

## <a name="what-is-giraph"></a>Che cos'è Giraph?
<a href="http://giraph.apache.org/" target="_blank">Apache Giraph</a> consente grafico tooperform elaborazione tramite Hadoop e può essere utilizzato con Azure HDInsight. Grafici modellare relazioni tra oggetti, ad esempio le connessioni hello tra i router in una rete di grandi dimensioni come hello Internet, o relazioni tra gli utenti nel social network (talvolta definito tooas un grafico di social networking). Elaborazione Graph consente tooreason sulle relazioni hello tra gli oggetti in un grafico, ad esempio:

* Identificare possibili amici sulla base delle relazioni correnti.
* Identificazione hello itinerario più breve tra due computer in una rete.
* Calcolare il numero di dimensioni di hello pagina delle pagine Web.

## <a name="install-giraph-using-portal"></a>Installare Giraph tramite il portale
1. Avviare la creazione di un cluster tramite hello **creazione personalizzata** opzione, come descritto in [cluster creare Hadoop in HDInsight](hdinsight-provision-clusters.md).
2. In hello **azioni Script** pagina della procedura guidata hello, fare clic su **aggiungere script azione** tooprovide i dettagli sulla azione script hello, come illustrato di seguito:

    ![Utilizzare l'azione Script toocustomize un cluster](./media/hdinsight-hadoop-giraph-install/hdi-script-action-giraph.png "toocustomize azione Script Usa un cluster")

    <table border='1'>
        <tr><th>Proprietà</th><th>Valore</th></tr>
        <tr><td>Nome</td>
            <td>Specificare un nome per l'azione script hello. Ad esempio, <b>Installare Giraph</b>.</td></tr>
        <tr><td>URI script</td>
            <td>Specificare hello Uniform Resource Identifier (URI) toohello script che è richiamato toocustomize hello cluster. Ad esempio, <i>https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1</i></td></tr>
        <tr><td>Tipo di nodo</td>
            <td>Specificare i nodi di hello in cui viene eseguito uno script di personalizzazione di hello. È possibile scegliere <b>Tutti i nodi</b>, <b>Solo nodi head</b> o <b>Solo nodi di lavoro</b>.
        <tr><td>parameters</td>
            <td>Specificare i parametri di hello, se richiesti dallo script hello. Hello script tooinstall Giraph non richiede alcun parametro, pertanto è possibile lasciare vuoto questo.</td></tr>
    </table>

    È possibile aggiungere più di uno script azione tooinstall più componenti nel cluster hello. Dopo aver aggiunto gli script hello, fare clic su hello segno di spunta toostart la creazione di cluster hello.

## <a name="use-giraph"></a>Usare Giraph
Utilizziamo hello SimpleShortestPathsComputation esempio toodemonstrate hello basic <a href = "http://people.apache.org/~edwardyoon/documents/pregel.pdf">Pregel</a> implementazione per trovare il percorso più breve di hello tra gli oggetti in un grafico. Utilizzare hello seguendo i passaggi tooupload hello esempio hello e dati esempio jar, eseguire un processo utilizzando l'esempio SimpleShortestPathsComputation hello e quindi visualizzare i risultati di hello.

1. Caricare un tooAzure di file di dati di esempio nell'archiviazione Blob. Nella workstation locale creare un nuovo file denominato **tiny_graph.txt**. Deve contenere hello seguenti righe:

        [0,0,[[1,1],[3,3]]]
        [1,0,[[0,1],[2,2],[3,1]]]
        [2,0,[[1,2],[4,4]]]
        [3,0,[[0,3],[1,1],[4,4]]]
        [4,0,[[3,4],[2,4]]]

    Caricare hello tiny_graph.txt file toohello archiviazione primaria per il cluster HDInsight. Per istruzioni su come visualizzare dati tooupload, [caricare dati per i processi di Hadoop in HDInsight](hdinsight-upload-data.md).

    Questi dati descrivono una relazione tra gli oggetti in un grafico diretto, utilizzando il formato di hello [origine\_id, origine\_valore, [[dest\_id], [edge\_valore],...]]. Ogni riga rappresenta una relazione tra un oggetto **source\_id** e uno o più oggetti **dest\_id**. Hello **bordo\_valore** (o peso) può essere considerato come livello di attendibilità hello o una distanza di connessione hello tra **source_id** e **dest\_id**.

    Disegnare out, e utilizza il valore di hello (o peso) come distanza hello tra oggetti, hello di sopra dei dati può essere simile al seguente:

    ![tiny_graph.txt drawn as circles with lines of varying distance between](./media/hdinsight-hadoop-giraph-install/giraph-graph.png)
2. Eseguire l'esempio SimpleShortestPathsComputation hello. Utilizzare hello seguendo l'esempio hello toorun i cmdlet di Azure PowerShell utilizzando file tiny_graph.txt hello come input.

    > [!IMPORTANT]
    > Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** ed è stato rimosso dal 1° gennaio 2017. Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.
    >
    > Eseguire le operazioni di hello in [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello più recente di Azure PowerShell. Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) per ulteriori informazioni.

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
    # Create hello definition
    $jobDefinition = New-AzureHDInsightMapReduceJobDefinition
        -JarFile $jarFile
        -ClassName "org.apache.giraph.GiraphRunner"
        -Arguments $jobArguments

    # Run hello job, write output toohello Azure PowerShell window
    $job = Start-AzureHDInsightJob -Cluster $clusterName -JobDefinition $jobDefinition
    Write-Host "Wait for hello job toocomplete ..." -ForegroundColor Green
    Wait-AzureHDInsightJob -Job $job
    Write-Host "STDERR"
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardError
    Write-Host "Display hello standard output ..." -ForegroundColor Green
    Get-AzureHDInsightJobOutput -Cluster $clusterName -JobId $job.JobId -StandardOutput
    ```

    In hello esempio precedente, sostituire **clustername** con nome hello del cluster HDInsight con Giraph installato.
3. Visualizzare i risultati di hello. Al termine dell'operazione processo hello hello risultati verranno archiviati in due file di output di hello **wasb: / / / esempio/out/shotestpaths** cartella. file Hello sono denominati **parte-m-00001** e **parte-m-00002**. Eseguire hello output di hello toodownload e visualizzare i passaggi seguenti:

    ```powershell
    $subscriptionName = "<SubscriptionName>"       # Azure subscription name
    $storageAccountName = "<StorageAccountName>"   # Azure Storage account name
    $containerName = "<ContainerName>"             # Blob storage container name

    # Select hello current subscription
    Select-AzureSubscription $subscriptionName

    # Create hello Storage account context object
    $storageAccountKey = Get-AzureStorageKey $storageAccountName | %{ $_.Primary }
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $storageAccountKey

    # Download hello job output toohello workstation
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00001 -Context $storageContext -Force
    Get-AzureStorageBlobContent -Container $containerName -Blob example/output/shortestpaths/part-m-00002 -Context $storageContext -Force
    ```

    Verrà creata hello **output/esempio/shortestpaths** struttura di directory nella directory corrente di hello nelle workstation e i file toothat percorso di download hello due output.

    Hello utilizzare **Cat** cmdlet toodisplay hello contenuto file hello:

        Cat example/output/shortestpaths/part*

    output di Hello risulterà simile toohello seguenti:

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    esempio SimpleShortestPathComputation Hello è hardcoded toostart con ID 1 oggetto e trovare gli oggetti tooother percorso più brevi hello. Pertanto l'output di hello deve essere letto come `destination_id distance`, dove distanza è hello valore (o peso), dei bordi hello percorsi tra l'oggetto ID 1 e ID di destinazione hello.

    Questa visualizzazione, è possibile verificare i risultati di hello viaggiando percorsi più brevi hello tra ID 1 e tutti gli altri oggetti. Si noti che il percorso più breve tra ID 1 e ID 4 hello sono 5. Si tratta di hello distanza totale tra <span style="color:orange">ID 1 e 3</span>e quindi <span style="color:red">ID 3 e 4</span>.

    ![Drawing of objects as circles with shortest paths drawn between](./media/hdinsight-hadoop-giraph-install/giraph-graph-out.png)

## <a name="install-giraph-using-aure-powershell"></a>Installare Giraph tramite Aure PowerShell
Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).  esempio Hello viene illustrato come tooinstall Spark con Azure PowerShell. È necessario toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

## <a name="install-giraph-using-net-sdk"></a>Installare Giraph tramite .NET SDK
Vedere [Personalizzare cluster HDInsight usando l'azione script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell). esempio Hello viene illustrato come tooinstall Spark usando hello .NET SDK. È necessario toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/giraphconfigactionv01/giraph-installer-v01.ps1).

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
