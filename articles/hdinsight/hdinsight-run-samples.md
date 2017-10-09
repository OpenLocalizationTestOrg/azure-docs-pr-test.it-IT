---
title: esempi di hello aaaRun Hadoop in HDInsight - Azure | Documenti Microsoft
description: Introduzione all'uso del servizio Azure HDInsight hello con hello esempi forniti. Usare script PowerShell che eseguono programmi MapReduce su cluster di dati.
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a><span data-ttu-id="9a615-104">Eseguire esempi di Hadoop MapReduce in HDInsight basato su Windows</span><span class="sxs-lookup"><span data-stu-id="9a615-104">Run Hadoop MapReduce samples in Windows-based HDInsight</span></span>
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="9a615-105">Toohelp iniziare in esecuzione processi MapReduce in Hadoop cluster con Azure HDInsight è disponibile un set di campioni.</span><span class="sxs-lookup"><span data-stu-id="9a615-105">A set of samples are provided toohelp you get started running MapReduce jobs on Hadoop clusters using Azure HDInsight.</span></span> <span data-ttu-id="9a615-106">Questi esempi vengono resi disponibili in ogni hello HDInsight cluster gestiti creato.</span><span class="sxs-lookup"><span data-stu-id="9a615-106">These samples are made available on each of hello HDInsight managed clusters that you create.</span></span> <span data-ttu-id="9a615-107">In questi esempi di esecuzione di acquisire familiarità con Azure PowerShell cmdlet toorun processi nel cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="9a615-107">Running these samples familiarize you with using Azure PowerShell cmdlets toorun jobs on Hadoop clusters.</span></span>

* <span data-ttu-id="9a615-108">[**Conteggio delle parole**][hdinsight-sample-wordcount]: conta le occorrenze delle parole in un file di testo.</span><span class="sxs-lookup"><span data-stu-id="9a615-108">[**Word count**][hdinsight-sample-wordcount]: Counts word occurrences in a text file.</span></span>
* <span data-ttu-id="9a615-109">[**Conteggio parole streaming c#**][hdinsight-sample-csharp-streaming]: conta le occorrenze di word in un file di testo utilizzando hello Hadoop streaming di interfaccia.</span><span class="sxs-lookup"><span data-stu-id="9a615-109">[**C# streaming word count**][hdinsight-sample-csharp-streaming]: Counts word occurrences in a text file using hello Hadoop streaming interface.</span></span>
* <span data-ttu-id="9a615-110">[**Estimator pi**][hdinsight-sample-pi-estimator]: Usa una statistica (quasi Monte Carlo) tooestimate hello valore del metodo di pi greco.</span><span class="sxs-lookup"><span data-stu-id="9a615-110">[**Pi estimator**][hdinsight-sample-pi-estimator]: Uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span>
* <span data-ttu-id="9a615-111">[**Graysort da 10 GB**][hdinsight-sample-10gb-graysort]: esegue un ordinamento GraySort per utilizzo generico in un file da 10 GB usando HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9a615-111">[**10-GB Graysort**][hdinsight-sample-10gb-graysort]: Run a general-purpose GraySort on a 10 GB file by using HDInsight.</span></span> <span data-ttu-id="9a615-112">Esistono tre processi toorun: Teragen toogenerate hello dati, Terasort toosort hello e tooconfirm Teravalidate che dati hello siano stati ordinati correttamente.</span><span class="sxs-lookup"><span data-stu-id="9a615-112">There are three jobs toorun: Teragen toogenerate hello data, Terasort toosort hello data, and Teravalidate tooconfirm that hello data has been properly sorted.</span></span>

> [!NOTE]
> <span data-ttu-id="9a615-113">codice sorgente Hello è reperibile in hello appendice.</span><span class="sxs-lookup"><span data-stu-id="9a615-113">hello source code can be found in hello Appendix.</span></span>

<span data-ttu-id="9a615-114">Documentazione aggiuntiva molto esista nel web hello per le tecnologie correlate Hadoop, ad esempio la programmazione basata su Java MapReduce e streaming e documentazione sui cmdlet di hello utilizzabili in Windows PowerShell scripting.</span><span class="sxs-lookup"><span data-stu-id="9a615-114">Much additional documentation exists on hello web for Hadoop-related technologies, such as Java-based MapReduce programming and streaming, and documentation about hello cmdlets that are used in Windows PowerShell scripting.</span></span> <span data-ttu-id="9a615-115">Per altre informazioni su queste risorse, vedere:</span><span class="sxs-lookup"><span data-stu-id="9a615-115">For more information about these resources, see:</span></span>

* [<span data-ttu-id="9a615-116">Sviluppare programmi MapReduce Java per Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a615-116">Develop Java MapReduce programs for Hadoop in HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [<span data-ttu-id="9a615-117">Inviare processi Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a615-117">Submit Hadoop jobs in HDInsight</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* <span data-ttu-id="9a615-118">[Introduzione tooAzure HDInsight][hdinsight-introduction]</span><span class="sxs-lookup"><span data-stu-id="9a615-118">[Introduction tooAzure HDInsight][hdinsight-introduction]</span></span>

<span data-ttu-id="9a615-119">Molte persone preferiscono oggi Hive e Pig rispetto a MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9a615-119">Nowadays, many people choose Hive and Pig over MapReduce.</span></span>  <span data-ttu-id="9a615-120">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="9a615-120">For more information, see:</span></span>

* [<span data-ttu-id="9a615-121">Usare Hive in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a615-121">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="9a615-122">Usare Pig in HDInsight</span><span class="sxs-lookup"><span data-stu-id="9a615-122">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="9a615-123">**Prerequisiti**:</span><span class="sxs-lookup"><span data-stu-id="9a615-123">**Prerequisites**:</span></span>

* <span data-ttu-id="9a615-124">**Una sottoscrizione di Azure**.</span><span class="sxs-lookup"><span data-stu-id="9a615-124">**An Azure subscription**.</span></span> <span data-ttu-id="9a615-125">Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="9a615-125">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="9a615-126">**Un cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="9a615-126">**an HDInsight cluster**.</span></span> <span data-ttu-id="9a615-127">Per istruzioni su hello vari modi in cui è possibile creare cluster di questo tipo, vedere [cluster creare Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9a615-127">For instructions on hello various ways in which such clusters can be created, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="9a615-128">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="9a615-128">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9a615-129">Il supporto di Azure PowerShell per la gestione delle risorse HDInsight tramite Azure Service Manager è **deprecato** e verrà rimosso dal 1° gennaio 2017.</span><span class="sxs-lookup"><span data-stu-id="9a615-129">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="9a615-130">Hello passaggi in questo documento usa hello nuovi cmdlet di HDInsight che funzionano con Gestione risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="9a615-130">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="9a615-131">Seguire i passaggi di hello in [installare e configurare Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello più recente di Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a615-131">Follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="9a615-132">Se si dispone di script che toobe necessità modificato toouse hello nuovi cmdlet che funzionano con Gestione risorse di Azure, vedere [di strumenti di migrazione tooAzure sviluppo basato su Gestione risorse per i cluster HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="9a615-132">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).</span></span>

## <span data-ttu-id="9a615-133"><a name="hdinsight-sample-wordcount"></a>Conteggio delle parole: Java</span><span class="sxs-lookup"><span data-stu-id="9a615-133"><a name="hdinsight-sample-wordcount"></a>Word count - Java</span></span>
<span data-ttu-id="9a615-134">un progetto di MapReduce toosubmit, creare innanzitutto la definizione di un processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9a615-134">toosubmit a MapReduce project, you first create a MapReduce job definition.</span></span> <span data-ttu-id="9a615-135">Nella definizione di processo hello, è necessario specificare i file jar di programma MapReduce hello e hello del file jar di hello, che è **wasb:///example/jars/hadoop-mapreduce-examples.jar**, nome della classe hello e hello argomenti.</span><span class="sxs-lookup"><span data-stu-id="9a615-135">In hello job definition, you specify hello MapReduce program jar file and hello location of hello jar file, which is **wasb:///example/jars/hadoop-mapreduce-examples.jar**, hello class name, and hello arguments.</span></span>  <span data-ttu-id="9a615-136">il programma MapReduce di Hello wordcount accetta due argomenti: file di origine hello parole toocount utilizzato e il percorso di hello per l'output.</span><span class="sxs-lookup"><span data-stu-id="9a615-136">hello wordcount MapReduce program takes two arguments: hello source file that is used toocount words, and hello location for output.</span></span>

<span data-ttu-id="9a615-137">codice sorgente Hello è reperibile in hello [appendice](#apendix-a---the-word-count-MapReduce-program-in-java).</span><span class="sxs-lookup"><span data-stu-id="9a615-137">hello source code can be found in hello [Appendix A](#apendix-a---the-word-count-MapReduce-program-in-java).</span></span>

<span data-ttu-id="9a615-138">Per procedure hello sviluppo MapReduce un linguaggio di programmazione, vedere - [MapReduce Java di sviluppare applicazioni per Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)</span><span class="sxs-lookup"><span data-stu-id="9a615-138">For hello procedure of developing a Java MapReduce program, see - [Develop Java MapReduce programs for Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)</span></span>

<span data-ttu-id="9a615-139">**un processo MapReduce il conteggio word toosubmit**</span><span class="sxs-lookup"><span data-stu-id="9a615-139">**toosubmit a word count MapReduce job**</span></span>

1. <span data-ttu-id="9a615-140">Aprire **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="9a615-140">Open **Windows PowerShell ISE**.</span></span> <span data-ttu-id="9a615-141">Per istruzioni, vedere [Installare e configurare Azure PowerShell][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="9a615-141">For instructions, see [Install and configure Azure PowerShell][powershell-install-configure].</span></span>
2. <span data-ttu-id="9a615-142">Hello incollare lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="9a615-142">Paste hello following PowerShell script:</span></span>

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    <span data-ttu-id="9a615-143">il processo MapReduce Hello produce un file denominato *parte-r-00000*, che contiene le parole e conta hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-143">hello MapReduce job produces a file named *part-r-00000*, which contains words and hello counts.</span></span> <span data-ttu-id="9a615-144">script di Hello utilizza hello **findstr** comando toolist hello tutte le parole che contiene *"there"*.</span><span class="sxs-lookup"><span data-stu-id="9a615-144">hello script uses hello **findstr** command toolist all hello words that contains *"there"*.</span></span>
3. <span data-ttu-id="9a615-145">Impostare hello innanzitutto tre variabili ed eseguire script hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-145">Set hello first three variables, and run hello script.</span></span>

## <span data-ttu-id="9a615-146"><a name="hdinsight-sample-csharp-streaming"></a>Conteggio delle parole: flusso in C#</span><span class="sxs-lookup"><span data-stu-id="9a615-146"><a name="hdinsight-sample-csharp-streaming"></a>Word count - C# streaming</span></span>
<span data-ttu-id="9a615-147">Hadoop fornisce un flusso tooMapReduce API, che consente di toowrite mappa e ridurre le funzioni in linguaggi diversi da Java.</span><span class="sxs-lookup"><span data-stu-id="9a615-147">Hadoop provides a streaming API tooMapReduce, which enables you toowrite map and reduce functions in languages other than Java.</span></span>

> [!NOTE]
> <span data-ttu-id="9a615-148">passaggi di Hello in questa esercitazione si applicano solo tooWindows basato su cluster di HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9a615-148">hello steps in this tutorial apply only tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="9a615-149">Per un esempio di flusso per cluster HDInsight basati su Linux, vedere [Sviluppare programmi di streaming Python per HDInsight](hdinsight-hadoop-streaming-python.md).</span><span class="sxs-lookup"><span data-stu-id="9a615-149">For an example of streaming for Linux-based HDInsight clusters, see [Develop Python streaming programs for HDInsight](hdinsight-hadoop-streaming-python.md).</span></span>

<span data-ttu-id="9a615-150">Nell'esempio hello mapper hello e riduttore hello sono eseguibili, leggono l'input hello da [stdin] [ stdin-stdout-stderr] (riga per riga) e crea l'output di hello troppo[stdout] [stdin-stdout-stderr].</span><span class="sxs-lookup"><span data-stu-id="9a615-150">In hello example, hello mapper and hello reducer are executables that read hello input from [stdin][stdin-stdout-stderr] (line-by-line) and emit hello output too[stdout][stdin-stdout-stderr].</span></span> <span data-ttu-id="9a615-151">programma Hello conta tutte le parole nel testo hello hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-151">hello program counts all hello words in hello text.</span></span>

<span data-ttu-id="9a615-152">Quando un file eseguibile specificato per **BizTalk Mapper**, ogni attività mapper avvia hello eseguibile come un processo distinto quando viene inizializzato il mapper hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-152">When an executable is specified for **mappers**, each mapper task launches hello executable as a separate process when hello mapper is initialized.</span></span> <span data-ttu-id="9a615-153">Esegue attività mapper hello, converte l'input in righe e feed hello righe toohello [stdin] [ stdin-stdout-stderr] del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-153">As hello mapper task runs, it converts its input into lines, and feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="9a615-154">In hello frattempo mapper hello raccoglie output orientato alla riga hello da stdout hello del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-154">In hello meantime, hello mapper collects hello line-oriented output from hello stdout of hello process.</span></span> <span data-ttu-id="9a615-155">Converte ogni riga in una coppia chiave/valore, che viene raccolto nell'output di hello del mapper hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-155">It converts each line into a key/value pair, which is collected as hello output of hello mapper.</span></span> <span data-ttu-id="9a615-156">Per impostazione predefinita, il prefisso di hello di una riga di toohello primo carattere di tabulazione è chiave hello e resto hello della riga di hello (esclusa hello carattere di tabulazione) è il valore di hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-156">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span> <span data-ttu-id="9a615-157">Se non è presente alcun carattere di tabulazione nella riga hello, riga intera viene considerata come chiave hello e hello valore è null.</span><span class="sxs-lookup"><span data-stu-id="9a615-157">If there is no Tab character in hello line, entire line is considered as hello key, and hello value is null.</span></span>

<span data-ttu-id="9a615-158">Quando un file eseguibile specificato per **riduttori**, ogni attività riduttore avvia hello eseguibile come un processo distinto quando viene inizializzato riduttore hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-158">When an executable is specified for **reducers**, each reducer task launches hello executable as a separate process when hello reducer is initialized.</span></span> <span data-ttu-id="9a615-159">Hello riduttore attività viene eseguita, relativo coppie chiave/valore di input viene convertito in righe e feed di hello righe toohello [stdin] [ stdin-stdout-stderr] del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-159">As hello reducer task runs, it converts its input key/values pairs into lines, and it feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="9a615-160">In hello frattempo riduttore hello raccoglie output orientato alla riga hello dalla hello [stdout] [ stdin-stdout-stderr] del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-160">In hello meantime, hello reducer collects hello line-oriented output from hello [stdout][stdin-stdout-stderr] of hello process.</span></span> <span data-ttu-id="9a615-161">Converte ogni coppia chiave/valore tooa di riga, che viene raccolto nell'output di hello del reducer hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-161">It converts each line tooa key/value pair, which is collected as hello output of hello reducer.</span></span> <span data-ttu-id="9a615-162">Per impostazione predefinita, il prefisso di hello di una riga di toohello primo carattere di tabulazione è chiave hello e resto hello della riga di hello (esclusa hello carattere di tabulazione) è il valore di hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-162">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span>

<span data-ttu-id="9a615-163">**processo di conteggio toosubmit c# streaming word**</span><span class="sxs-lookup"><span data-stu-id="9a615-163">**toosubmit a C# streaming word count job**</span></span>

* <span data-ttu-id="9a615-164">Attenersi alla procedura hello in [Word count - Java](#word-count-java)e sostituire la definizione di processo hello con hello seguente riga:</span><span class="sxs-lookup"><span data-stu-id="9a615-164">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    <span data-ttu-id="9a615-165">file di output di Hello dovrà essere:</span><span class="sxs-lookup"><span data-stu-id="9a615-165">hello output file shall be:</span></span>

        example/data/StreamingOutput/wc.txt/part-00000

## <span data-ttu-id="9a615-166"><a name="hdinsight-sample-pi-estimator"></a>Calcolo del Pi greco</span><span class="sxs-lookup"><span data-stu-id="9a615-166"><a name="hdinsight-sample-pi-estimator"></a>PI estimator</span></span>
<span data-ttu-id="9a615-167">Usa una statistica estimator pi Hello (quasi Monte Carlo) tooestimate hello valore del metodo di pi greco.</span><span class="sxs-lookup"><span data-stu-id="9a615-167">hello pi estimator uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="9a615-168">Punti posizionati in modo casuale all'interno di un'unità quadrati anche rientrano in un cerchio figurare all'interno di tale quadrato con un'area toohello uguale probabilità del cerchio hello, pi/4.</span><span class="sxs-lookup"><span data-stu-id="9a615-168">Points placed at random inside of a unit square also fall within a circle inscribed within that square with a probability equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="9a615-169">il valore di Hello di pi greco può essere stimato dal valore hello 4R, dove R è il rapporto di hello del numero di hello di punti che si trovano all'interno di hello cerchio toohello numero totale di punti che si trovano all'interno di quadrato di hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-169">hello value of pi can be estimated from hello value of 4R, where R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="9a615-170">esempio hello di dimensioni maggiore Hello di punti utilizzati stima più accurata hello hello è.</span><span class="sxs-lookup"><span data-stu-id="9a615-170">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="9a615-171">script Hello fornito per questo esempio invia un processo jar Hadoop e viene impostato toorun con un valore 16 mappe, ognuno dei quali è necessario toocompute 10 milioni di esempio punti dai valori di parametro hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-171">hello script provided for this sample submits a Hadoop jar job and is set up toorun with a value 16 maps, each of which is required toocompute 10 million sample points by hello parameter values.</span></span> <span data-ttu-id="9a615-172">Questi parametri i valori possono essere modificate tooimprove hello stimato valore di pi greco.</span><span class="sxs-lookup"><span data-stu-id="9a615-172">These parameter values can be changed tooimprove hello estimated value of pi.</span></span> <span data-ttu-id="9a615-173">Per riferimento, hello primi 10 cifre decimali di pi greco sono 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="9a615-173">For reference, hello first 10 decimal places of pi are 3.1415926535.</span></span>

<span data-ttu-id="9a615-174">**un processo di stima pi toosubmit**</span><span class="sxs-lookup"><span data-stu-id="9a615-174">**toosubmit a pi estimator job**</span></span>

* <span data-ttu-id="9a615-175">Attenersi alla procedura hello in [Word count - Java](#word-count-java)e sostituire la definizione di processo hello con hello seguente riga:</span><span class="sxs-lookup"><span data-stu-id="9a615-175">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <span data-ttu-id="9a615-176"><a name="hdinsight-sample-10gb-graysort"></a>Graysort da 10 GB</span><span class="sxs-lookup"><span data-stu-id="9a615-176"><a name="hdinsight-sample-10gb-graysort"></a>10-GB Graysort</span></span>
<span data-ttu-id="9a615-177">In questo esempio vengono usati solo 10 GB di dati, in modo da consentire un'esecuzione relativamente rapida.</span><span class="sxs-lookup"><span data-stu-id="9a615-177">This sample uses a modest 10GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="9a615-178">Usa applicazioni MapReduce hello sviluppate da Owen O'Malley e Arun Murthy confermati benchmark ordinamento terabyte hello annuale utilizzo generale ("daytona") nel 2009 con una frequenza di 0.578 TB/min (100 TB in 173 minuti).</span><span class="sxs-lookup"><span data-stu-id="9a615-178">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy that won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009 with a rate of 0.578TB/min (100TB in 173 minutes).</span></span> <span data-ttu-id="9a615-179">Per ulteriori informazioni su questo e altri ordinamento benchmark, vedere hello [Sortbenchmark](http://sortbenchmark.org/) sito.</span><span class="sxs-lookup"><span data-stu-id="9a615-179">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="9a615-180">In questo esempio vengono utilizzati tre set di programmi MapReduce:</span><span class="sxs-lookup"><span data-stu-id="9a615-180">This sample uses three sets of MapReduce programs:</span></span>

1. <span data-ttu-id="9a615-181">**TeraGen** è un programma MapReduce che è possibile utilizzare le righe di hello toogenerate di toosort di dati.</span><span class="sxs-lookup"><span data-stu-id="9a615-181">**TeraGen** is a MapReduce program that you can use toogenerate hello rows of data toosort.</span></span>
2. <span data-ttu-id="9a615-182">**TeraSort** Campiona i dati di input hello e utilizza i dati di hello toosort MapReduce in totale dell'ordine.</span><span class="sxs-lookup"><span data-stu-id="9a615-182">**TeraSort** samples hello input data and uses MapReduce toosort hello data into a total order.</span></span> <span data-ttu-id="9a615-183">TeraSort è un ordinamento standard delle funzioni di MapReduce, ad eccezione di un partitioner che utilizza un elenco ordinato di chiavi di n-1 campionate che definiscono l'intervallo di chiavi hello per ogni riduzione.</span><span class="sxs-lookup"><span data-stu-id="9a615-183">TeraSort is a standard sort of MapReduce functions, except for a custom partitioner that uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="9a615-184">In particolare, tutte le chiavi questo tipo di esempio [i-1] < = chiave < [i] di esempio vengono inviati tooreduce i.</span><span class="sxs-lookup"><span data-stu-id="9a615-184">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="9a615-185">Ciò garantisce che l'output di hello di ridurre i sono tutti minore di output di hello di ridurre i + 1.</span><span class="sxs-lookup"><span data-stu-id="9a615-185">This guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>
3. <span data-ttu-id="9a615-186">**TeraValidate** è un programma MapReduce che convalida l'output di hello globale viene ordinato.</span><span class="sxs-lookup"><span data-stu-id="9a615-186">**TeraValidate** is a MapReduce program that validates that hello output is globally sorted.</span></span> <span data-ttu-id="9a615-187">Crea una mappa per ogni file nella directory di output di hello e ogni mappa garantisce che ogni chiave è minore o uguale toohello precedente.</span><span class="sxs-lookup"><span data-stu-id="9a615-187">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="9a615-188">funzione mappa Hello genera anche i record di hello prima e ultima chiavi di ogni file e hello reduce (funzione) garantisce che hello prima chiave del file i è maggiore di hello chiave ultimo di i-1 file.</span><span class="sxs-lookup"><span data-stu-id="9a615-188">hello map function also generates records of hello first and last keys of each file, and hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="9a615-189">I problemi vengano segnalati come output di hello ridurre con chiavi hello che non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="9a615-189">Any problems are reported as an output of hello reduce with hello keys that are out of order.</span></span>

<span data-ttu-id="9a615-190">input Hello e formato di output, utilizzato da tutte e tre le applicazioni, legge e scrive i file di testo hello in formato corretto hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-190">hello input and output format, used by all three applications, reads and writes hello text files in hello right format.</span></span> <span data-ttu-id="9a615-191">output di Hello di hello ridurre replica impostati too1, anziché predefinito hello 3, perché concorso benchmark hello non richiede che i dati di output di hello essere replicati nel toomultiple nodi.</span><span class="sxs-lookup"><span data-stu-id="9a615-191">hello output of hello reduce has replication set too1, instead of hello default 3, because hello benchmark contest does not require that hello output data be replicated on toomultiple nodes.</span></span>

<span data-ttu-id="9a615-192">Esempio hello, ogni tooone corrispondente di programmi MapReduce hello descritto nell'introduzione di hello, sono necessari tre attività:</span><span class="sxs-lookup"><span data-stu-id="9a615-192">Three tasks are required by hello sample, each corresponding tooone of hello MapReduce programs described in hello introduction:</span></span>

1. <span data-ttu-id="9a615-193">Generare dati di hello per l'ordinamento eseguendo hello **TeraGen** processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9a615-193">Generate hello data for sorting by running hello **TeraGen** MapReduce job.</span></span>
2. <span data-ttu-id="9a615-194">Ordinare i dati di hello eseguendo hello **TeraSort** processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9a615-194">Sort hello data by running hello **TeraSort** MapReduce job.</span></span>
3. <span data-ttu-id="9a615-195">Verificare che i dati hello siano stati ordinati correttamente eseguendo hello **TeraValidate** processo MapReduce.</span><span class="sxs-lookup"><span data-stu-id="9a615-195">Confirm that hello data has been correctly sorted by running hello **TeraValidate** MapReduce job.</span></span>

<span data-ttu-id="9a615-196">**processi di hello toosubmit**</span><span class="sxs-lookup"><span data-stu-id="9a615-196">**toosubmit hello jobs**</span></span>

* <span data-ttu-id="9a615-197">Attenersi alla procedura hello in [Word count - Java](#word-count-java), e utilizzare hello seguendo le definizioni dei processi:</span><span class="sxs-lookup"><span data-stu-id="9a615-197">Follow hello procedure in [Word count - Java](#word-count-java), and use hello following job definitions:</span></span>

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a><span data-ttu-id="9a615-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="9a615-198">Next steps</span></span>
<span data-ttu-id="9a615-199">Da questo articolo e gli articoli di hello in ognuno degli esempi di hello, si è appreso come esempi hello toorun incluso hello cluster HDInsight tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="9a615-199">From this article and hello articles in each of hello samples, you learned how toorun hello samples included with hello HDInsight clusters by using Azure PowerShell.</span></span> <span data-ttu-id="9a615-200">Per le esercitazioni sull'uso Pig, Hive e MapReduce con HDInsight, vedere hello seguenti argomenti:</span><span class="sxs-lookup"><span data-stu-id="9a615-200">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="9a615-201">[Introduzione all'uso di Hadoop con Hive in uso di HDInsight tooanalyze palmari mobili][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="9a615-201">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="9a615-202">[Usare Pig con Hadoop in HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="9a615-202">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="9a615-203">[Usare Hive con Hadoop in HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="9a615-203">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="9a615-204">[Inviare processi Hadoop in HDInsight][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="9a615-204">[Submit Hadoop Jobs in HDInsight][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="9a615-205">[Documentazione di Azure HDInsight SDK][hdinsight-sdk-documentation]</span><span class="sxs-lookup"><span data-stu-id="9a615-205">[Azure HDInsight SDK documentation][hdinsight-sdk-documentation]</span></span>

## <a name="appendix-a---hello-word-count-source-code"></a><span data-ttu-id="9a615-206">Appendice A - hello codice sorgente conteggio di Word</span><span class="sxs-lookup"><span data-stu-id="9a615-206">Appendix A - hello Word count source code</span></span>

```java
package org.apache.hadoop.examples;
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
    extends Mapper<Object, Text, Text, IntWritable>{

private final static IntWritable one = new IntWritable(1);
private Text word = new Text();

public void map(Object key, Text value, Context context
                ) throws IOException, InterruptedException {
    StringTokenizer itr = new StringTokenizer(value.toString());
    while (itr.hasMoreTokens()) {
    word.set(itr.nextToken());
    context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
    extends Reducer<Text,IntWritable,Text,IntWritable> {
private IntWritable result = new IntWritable();

public void reduce(Text key, Iterable<IntWritable> values,
                    Context context
                    ) throws IOException, InterruptedException {
    int sum = 0;
    for (IntWritable val : values) {
    sum += val.get();
    }
    result.set(sum);
    context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
Configuration conf = new Configuration();
String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
if (otherArgs.length != 2) {
    System.err.println("Usage: wordcount <in> <out>");
    System.exit(2);
    }
Job job = new Job(conf, "word count");
job.setJarByClass(WordCount.class);
job.setMapperClass(TokenizerMapper.class);
job.setCombinerClass(IntSumReducer.class);
job.setReducerClass(IntSumReducer.class);
job.setOutputKeyClass(Text.class);
job.setOutputValueClass(IntWritable.class);
FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
    }
```

## <a name="appendix-b---hello-word-count-streaming-source-code"></a><span data-ttu-id="9a615-207">Appendice B - Conteggio parole hello streaming codice sorgente</span><span class="sxs-lookup"><span data-stu-id="9a615-207">Appendix B - hello word count streaming source code</span></span>
<span data-ttu-id="9a615-208">programma MapReduce Hello utilizza un'applicazione cat.exe hello come testo hello toostream interfaccia mapping nella console di hello e un'applicazione hello wc.exe come hello ridurre il numero di hello toocount di interfaccia di parole che sono state trasmesse da un documento.</span><span class="sxs-lookup"><span data-stu-id="9a615-208">hello MapReduce program uses hello cat.exe application as a mapping interface toostream hello text into hello console and hello wc.exe application as hello reduce interface toocount hello number of words that are streamed from a document.</span></span> <span data-ttu-id="9a615-209">Mapper hello sia riduttore di caratteri, riga per riga, di lettura dal flusso di input standard hello (stdin) e scrivere il flusso di output standard toohello (stdout).</span><span class="sxs-lookup"><span data-stu-id="9a615-209">Both hello mapper and reducer read characters, line-by-line, from hello standard input stream (stdin) and write toohello standard output stream (stdout).</span></span>

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

<span data-ttu-id="9a615-210">Hello codice mapper hello cat.cs file utilizza un [StreamReader] [ streamreader] caratteri hello tooread hello in arrivo flusso toohello della console di, che quindi scrive hello flusso toohello flusso di output standard dell'oggetto con hello statico [console. WriteLine] [ console-writeline] metodo.</span><span class="sxs-lookup"><span data-stu-id="9a615-210">hello mapper code in hello cat.cs file uses a [StreamReader][streamreader] object tooread hello characters of hello incoming stream toohello console, which then writes hello stream toohello standard output stream with hello static [Console.Writeline][console-writeline] method.</span></span>

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

<span data-ttu-id="9a615-211">Hello codice riduttore hello wc.cs file utilizza un [StreamReader] [ streamreader] tooread caratteri dell'oggetto da hello flusso di input standard che sono stati output mapper cat.exe hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-211">hello reducer code in hello wc.cs file uses a [StreamReader][streamreader]   object tooread characters from hello standard input stream that have been output by hello cat.exe mapper.</span></span> <span data-ttu-id="9a615-212">Durante la lettura di caratteri hello con hello [console. WriteLine] [ console-writeline] (metodo), vengono contate le parole hello contando spazi e caratteri di fine della riga alla fine di hello di ogni parola.</span><span class="sxs-lookup"><span data-stu-id="9a615-212">As it reads hello characters with hello [Console.Writeline][console-writeline] method, it counts hello words by counting spaces and end-of-line characters at hello end of each word.</span></span> <span data-ttu-id="9a615-213">Viene quindi scritto come flusso di output standard hello toohello totale con hello [console. WriteLine] [ console-writeline] metodo.</span><span class="sxs-lookup"><span data-stu-id="9a615-213">It then writes hello total toohello standard output stream with hello [Console.Writeline][console-writeline] method.</span></span>

## <a name="appendix-c---hello-pi-estimator-source-code"></a><span data-ttu-id="9a615-214">Appendice C - hello codice sorgente di pi greco estimator</span><span class="sxs-lookup"><span data-stu-id="9a615-214">Appendix C - hello Pi estimator source code</span></span>
<span data-ttu-id="9a615-215">estimator pi Hello codice Java che contiene funzioni di BizTalk mapper e del reducer hello è disponibile per l'ispezione riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="9a615-215">hello pi estimator Java code that contains hello mapper and reducer functions is available for inspection below.</span></span> <span data-ttu-id="9a615-216">programma mapper Hello genera un numero specificato di punti posizionato in modo casuale all'interno di un quadrato dell'unità e quindi conta il numero di hello di tali punti di un cerchio hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-216">hello mapper program generates a specified number of points placed at random inside of a unit square and then counts hello number of those points that are inside hello circle.</span></span> <span data-ttu-id="9a615-217">programma riduttore Hello accumula punti conteggiati mediante BizTalk Mapper hello e quindi stima valore hello di pi greco dalla formula 4R hello, dove R è il rapporto di hello del numero di hello di punti conteggiati all'interno di hello cerchio toohello numero totale di punti che si trovano all'interno di quadrato di hello.</span><span class="sxs-lookup"><span data-stu-id="9a615-217">hello reducer program accumulates points counted by hello mappers and then estimates hello value of pi from hello formula 4R, where R is hello ratio of hello number of points counted inside hello circle toohello total number of points that are within hello square.</span></span>

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a><span data-ttu-id="9a615-218">Appendice D - codice sorgente di hello 10gb graysort</span><span class="sxs-lookup"><span data-stu-id="9a615-218">Appendix D - hello 10gb graysort source code</span></span>
<span data-ttu-id="9a615-219">codice Hello per il programma TeraSort MapReduce hello viene presentato per un controllo in questa sezione.</span><span class="sxs-lookup"><span data-stu-id="9a615-219">hello code for hello TeraSort MapReduce program is presented for inspection in this section.</span></span>

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
