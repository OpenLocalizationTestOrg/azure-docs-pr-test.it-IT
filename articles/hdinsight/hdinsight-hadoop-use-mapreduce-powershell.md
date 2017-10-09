---
title: aaaUse MapReduce e PowerShell con Hadoop - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse tooremotely di PowerShell eseguire i processi MapReduce con Hadoop in HDInsight.
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
ms.openlocfilehash: 59524f0e8813d4c017f92bccb2e50d4c018acf71
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a><span data-ttu-id="7fb22-103">Esecuzione di processi MapReduce con Hadoop in HDInsight mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fb22-103">Run MapReduce jobs with Hadoop on HDInsight using PowerShell</span></span>

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

<span data-ttu-id="7fb22-104">Questo documento viene fornito un esempio dell'utilizzo di Azure PowerShell toorun un processo MapReduce in un Hadoop nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7fb22-104">This document provides an example of using Azure PowerShell toorun a MapReduce job in a Hadoop on HDInsight cluster.</span></span>

## <span data-ttu-id="7fb22-105"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7fb22-105"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="7fb22-106">**Un cluster Azure HDInsight (Hadoop in HDInsight)**</span><span class="sxs-lookup"><span data-stu-id="7fb22-106">**An Azure HDInsight (Hadoop on HDInsight) cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7fb22-107">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="7fb22-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7fb22-108">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7fb22-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7fb22-109">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="7fb22-109">**A workstation with Azure PowerShell**.</span></span>

## <span data-ttu-id="7fb22-110"><a id="powershell"></a>Eseguire un processo MapReduce con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7fb22-110"><a id="powershell"></a>Run a MapReduce job using Azure PowerShell</span></span>

<span data-ttu-id="7fb22-111">Azure PowerShell fornisce *cmdlet* che consentono di tooremotely eseguire i processi MapReduce in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7fb22-111">Azure PowerShell provides *cmdlets* that allow you tooremotely run MapReduce jobs on HDInsight.</span></span> <span data-ttu-id="7fb22-112">Internamente, questa operazione viene eseguita tramite le chiamate REST troppo[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (precedentemente denominato Templeton) in esecuzione su hello cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7fb22-112">Internally, this is accomplished by using REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (formerly called Templeton) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="7fb22-113">i cmdlet seguenti Hello vengono utilizzati durante l'esecuzione di processi MapReduce in un cluster HDInsight remoto.</span><span class="sxs-lookup"><span data-stu-id="7fb22-113">hello following cmdlets are used when running MapReduce jobs in a remote HDInsight cluster.</span></span>

* <span data-ttu-id="7fb22-114">**Account di accesso AzureRmAccount**: esegue l'autenticazione di Azure PowerShell tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb22-114">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription.</span></span>

* <span data-ttu-id="7fb22-115">**Nuovo AzureRmHDInsightMapReduceJobDefinition**: crea un nuovo *definizione del processo* utilizzando hello specificato le informazioni di MapReduce.</span><span class="sxs-lookup"><span data-stu-id="7fb22-115">**New-AzureRmHDInsightMapReduceJobDefinition**: Creates a new *job definition* by using hello specified MapReduce information.</span></span>

* <span data-ttu-id="7fb22-116">**Inizio AzureRmHDInsightJob**: invia hello processo definizione tooHDInsight, avvia il processo di hello e restituisce un *processo* oggetto che può essere utilizzato toocheck hello stato del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="7fb22-116">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job.</span></span>

* <span data-ttu-id="7fb22-117">**Attesa AzureRmHDInsightJob**: utilizza hello oggetto toocheck hello stato del processo del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="7fb22-117">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="7fb22-118">È in attesa fino a quando non viene completato il processo di hello o viene superato il tempo di attesa hello.</span><span class="sxs-lookup"><span data-stu-id="7fb22-118">It waits until hello job completes or hello wait time is exceeded.</span></span>

* <span data-ttu-id="7fb22-119">**Get-AzureRmHDInsightJobOutput**: utilizzato l'output di hello tooretrieve del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="7fb22-119">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job.</span></span>

<span data-ttu-id="7fb22-120">Hello passaggi seguenti viene illustrato come toouse questi toorun cmdlet un processo del cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7fb22-120">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster.</span></span>

1. <span data-ttu-id="7fb22-121">Utilizzando un editor, salvare hello seguente di codice come **mapreducejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="7fb22-121">Using an editor, save hello following code as **mapreducejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. <span data-ttu-id="7fb22-122">Quindi, aprire un nuovo prompt dei comandi di **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="7fb22-122">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="7fb22-123">Modificare il percorso toohello directory di hello **mapreducejob.ps1** file, quindi utilizzare lo script di comando toorun hello seguente hello:</span><span class="sxs-lookup"><span data-stu-id="7fb22-123">Change directories toohello location of hello **mapreducejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\mapreducejob.ps1

    <span data-ttu-id="7fb22-124">Quando si esegue uno script di hello, richiesto per il nome di hello del cluster HDInsight hello e nome dell'account HTTPS/Admin hello e la password per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7fb22-124">When you run hello script, you are prompted for hello name of hello HDInsight cluster and hello HTTPS/Admin account name and password for hello cluster.</span></span> <span data-ttu-id="7fb22-125">Potrebbe essere richiesta tooauthenticate tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7fb22-125">You may also be prompted tooauthenticate tooyour Azure subscription.</span></span>

3. <span data-ttu-id="7fb22-126">Al termine del processo di hello, viene visualizzato toohello simili di output il testo seguente:</span><span class="sxs-lookup"><span data-stu-id="7fb22-126">When hello job completes, you receive output similar toohello following text:</span></span>

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    <span data-ttu-id="7fb22-127">Questo output indica che il processo di hello è stata completata correttamente.</span><span class="sxs-lookup"><span data-stu-id="7fb22-127">This output indicates that hello job completed successfully.</span></span>

    > [!NOTE]
    > <span data-ttu-id="7fb22-128">Se hello **ExitCode** è un valore diverso da 0, vedere [risoluzione dei problemi](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="7fb22-128">If hello **ExitCode** is a value other than 0, see [Troubleshooting](#troubleshooting).</span></span>

    <span data-ttu-id="7fb22-129">In questo esempio viene inoltre archiviato hello scaricato i file tooan **txt** file nella directory hello eseguiti script hello da.</span><span class="sxs-lookup"><span data-stu-id="7fb22-129">This example also stores hello downloaded files tooan **output.txt** file in hello directory that you run hello script from.</span></span>

### <a name="view-output"></a><span data-ttu-id="7fb22-130">Visualizzare l’output</span><span class="sxs-lookup"><span data-stu-id="7fb22-130">View output</span></span>

<span data-ttu-id="7fb22-131">Aprire hello **txt** file in un hello toosee editor di testo parole e conta prodotti dal processo hello.</span><span class="sxs-lookup"><span data-stu-id="7fb22-131">Open hello **output.txt** file in a text editor toosee hello words and counts produced by hello job.</span></span>

> [!NOTE]
> <span data-ttu-id="7fb22-132">file di output di Hello di un processo MapReduce non sono modificabili.</span><span class="sxs-lookup"><span data-stu-id="7fb22-132">hello output files of a MapReduce job are immutable.</span></span> <span data-ttu-id="7fb22-133">Pertanto, se si esegue nuovamente questo esempio, è necessario nome hello toochange hello del file di output.</span><span class="sxs-lookup"><span data-stu-id="7fb22-133">So if you rerun this sample, you need toochange hello name of hello output file.</span></span>

## <span data-ttu-id="7fb22-134"><a id="troubleshooting"></a>Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="7fb22-134"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="7fb22-135">Se viene restituita alcuna informazione quando hello processo viene completato, potrebbe essersi verificato un errore durante l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="7fb22-135">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="7fb22-136">informazioni sull'errore tooview per questo processo, aggiungere hello successivo comando toohello hello **mapreducejob.ps1** file, salvarlo e quindi eseguirla nuovamente.</span><span class="sxs-lookup"><span data-stu-id="7fb22-136">tooview error information for this job, add hello following command toohello end of hello **mapreducejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="7fb22-137">Questo cmdlet restituisce le informazioni di hello che è stato scritto tooSTDERR nel server di hello quando è stato eseguito il processo di hello e può essere utile determinare perché il processo di hello non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="7fb22-137">This cmdlet returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="7fb22-138"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7fb22-138"><a id="summary"></a>Summary</span></span>

<span data-ttu-id="7fb22-139">Come si può notare, Azure PowerShell fornisce toorun un modo semplice i processi MapReduce in un cluster HDInsight, lo stato del processo di monitoraggio hello e output di hello recuperare.</span><span class="sxs-lookup"><span data-stu-id="7fb22-139">As you can see, Azure PowerShell provides an easy way toorun MapReduce jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="7fb22-140"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7fb22-140"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="7fb22-141">Per informazioni generali sui processi MapReduce in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7fb22-141">For general information about MapReduce jobs in HDInsight:</span></span>

* [<span data-ttu-id="7fb22-142">Usare MapReduce in HDInsight Hadoop</span><span class="sxs-lookup"><span data-stu-id="7fb22-142">Use MapReduce on HDInsight Hadoop</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="7fb22-143">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7fb22-143">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="7fb22-144">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7fb22-144">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="7fb22-145">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7fb22-145">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
