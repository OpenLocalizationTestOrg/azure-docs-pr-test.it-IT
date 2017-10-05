---
title: Usare MapReduce e PowerShell con Hadoop - Azure HDInsight | Microsoft Docs
description: "Informazioni su come usare PowerShell per eseguire in modalità remota processi MapReduce con Hadoop in HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 21b56d32-1785-4d44-8ae8-94467c12cfba
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: c3801573808709f29cb1e563ac803f225a28cafc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="b7d3e-103">Esecuzione di processi MapReduce con Hadoop in HDInsight mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7d3e-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="b7d3e-104">Questo documento fornisce un esempio di come usare Azure PowerShell per eseguire un processo MapReduce in un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-104">This document provides an example of using Azure PowerShell to run a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="b7d3e-105"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b7d3e-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="b7d3e-106">**Un cluster Azure HDInsight (Hadoop in HDInsight)**</span><span class="sxs-lookup"><span data-stu-id="b7d3e-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="b7d3e-107">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b7d3e-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="b7d3e-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="b7d3e-109">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="b7d3e-110"><a id="powershell"></a>Eseguire un processo MapReduce con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7d3e-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="b7d3e-111">Azure PowerShell fornisce *cmdlet* che consentono di eseguire in modalità remota processi MapReduce in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-111">Azure PowerShell provides *cmdlets* that allow you to remotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="b7d3e-112">Questo risultato si ottiene internamente usando chiamate REST a [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (chiamato in precedenza Templeton) in esecuzione nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-112">Internally, this is accomplished by using REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on the HDInsight cluster.</span></span>

<span data-ttu-id="b7d3e-113">Durante l'esecuzione di processi MapReduce in un cluster HDInsight remoto, vengono usati i seguenti cmdlet.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-113">The following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="b7d3e-114">**Login-AzureRmAccount**: autentica Azure PowerShell nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription.</span></span>

* <span data-ttu-id="b7d3e-115">**New-AzureRmHDInsightMapReduceJobDefinition**: crea una nuova *definizione di processo* usando le informazioni MapReduce specificate.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using the specified MapReduce information.</span></span>

* <span data-ttu-id="b7d3e-116">**Start-AzureRmHDInsightJob**: invia la definizione del processo a HDInsight, avvia il processo e restituisce un oggetto *job* che può essere usato per verificare lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-116">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job.</span></span>

* <span data-ttu-id="b7d3e-117">**Wait-AzureRmHDInsightJob**: usa l'oggetto job per verificare lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-117">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="b7d3e-118">Attende che il processo venga completato o che scada il periodo di attesa previsto.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-118">It waits until the job completes or the wait time is exceeded.</span></span>

* <span data-ttu-id="b7d3e-119">**Get-AzureRmHDInsightJobOutput**: viene usato per recuperare l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-119">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job.</span></span>

<span data-ttu-id="b7d3e-120">La seguente procedura illustra come usare questi cmdlet per eseguire un processo nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-120">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="b7d3e-121">Usando un editor, salvare il seguente codice come **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-121">Using an editor, save the following code as **mapreducejob.ps1**.</span></span>

    <span data-ttu-id="b7d3e-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span><span class="sxs-lookup"><span data-stu-id="b7d3e-122">[!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]</span></span>

2. <span data-ttu-id="b7d3e-123">Quindi, aprire un nuovo prompt dei comandi di **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="b7d3e-123">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="b7d3e-124">Passare al percorso del file **mapreducejob.ps1** , quindi usare il seguente comando per eseguire lo script.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-124">Change directories to the location of the **mapreducejob.ps1** file, then use the following command to run the script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="b7d3e-125">Quando si esegue lo script viene chiesto il nome del cluster HDInsight e il nome dell'account Admin/HTTPS e la password per il cluster.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-125">When you run the script, you are prompted for the name of the HDInsight cluster and the HTTPS/Admin account name and password for the cluster.</span></span> <span data-ttu-id="b7d3e-126">Potrebbe anche essere richiesta l'autenticazione alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-126">You may also be prompted to authenticate to your Azure subscription.</span></span>

3. <span data-ttu-id="b7d3e-127">Al termine del processo, viene visualizzato un output simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="b7d3e-127">When the job completes, you receive output similar to the following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="b7d3e-128">Questo output indica che il processo è stato completato correttamente.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-128">This output indicates that the job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b7d3e-129">Se **ExitCode** è un valore diverso da 0, vedere [Risoluzione dei problemi](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="b7d3e-129">If the **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="b7d3e-130">Questo esempio consente anche di archiviare i file scaricati in un file **output.txt** nella directory in cui viene eseguito lo script.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-130">This example also stores the downloaded files to an **output.txt** file in the directory that you run the script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="b7d3e-131">Visualizzare l’output</span><span class="sxs-lookup"><span data-stu-id="b7d3e-131">View output</span></span>

<span data-ttu-id="b7d3e-132">Per vedere le parole e i numeri generati dal processo, aprire il file **output.txt** in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-132">Open the **output.txt** file in a text editor to see the words and counts produced by the job.</span></span>

> [!NOTE]
> <span data-ttu-id="b7d3e-133">I file di output di un processo MapReduce non sono modificabili.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-133">The output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="b7d3e-134">Se pertanto si esegue di nuovo l'esempio, è necessario cambiare il nome del file di output.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-134">So if you rerun this sample, you need to change the name of the output file.</span></span>

## <span data-ttu-id="b7d3e-135"><a id="troubleshooting"></a>Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="b7d3e-135"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="b7d3e-136">Se al termine del processo non vengono restituite informazioni, potrebbe essersi verificato un errore durante l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-136">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="b7d3e-137">Per visualizzare informazioni relative all'errore per questo processo, aggiungere il seguente comando alla fine del file **mapreducejob.ps1** , salvare il file, quindi eseguirlo nuovamente.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-137">To view error information for this job, add the following command to the end of the **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the WordCount job.
Write-Host "Display the standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="b7d3e-138">Questo cmdlet restituisce le informazioni scritte in STDERR nel server durante l'esecuzione del processo, che possono essere utili per determinare la causa del problema.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-138">This cmdlet returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="b7d3e-139"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="b7d3e-139"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="b7d3e-140">Come è possibile notare, Azure PowerShell fornisce un modo semplice per eseguire processi MapReduce in un cluster HDInsight, monitorare lo stato del processo e recuperare l'output.</span><span class="sxs-lookup"><span data-stu-id="b7d3e-140">As you can see, Azure PowerShell provides an easy way to run MapReduce jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="b7d3e-141"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b7d3e-141"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="b7d3e-142">Per informazioni generali sui processi MapReduce in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b7d3e-142">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="b7d3e-143">Usare MapReduce in HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="b7d3e-143">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="b7d3e-144">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="b7d3e-144">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="b7d3e-145">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7d3e-145">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="b7d3e-146">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7d3e-146">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
