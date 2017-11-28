---
title: aaaUse Hadoop Pig in HDInsight - Azure PowerShell | Documenti Microsoft
description: Informazioni su come cluster di toosubmit Pig processi tooa Hadoop in HDInsight con Azure PowerShell.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 737089c1-b494-4387-9def-7b4dac3be532
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: 771617df203011eaec715a0dba6f5014a42877f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a><span data-ttu-id="81b4c-103">Utilizzare i processi di Azure PowerShell toorun Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="81b4c-103">Use Azure PowerShell toorun Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="81b4c-104">Questo documento viene fornito un esempio dell'utilizzo di Azure PowerShell toosubmit Pig processi tooa Hadoop nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81b4c-104">This document provides an example of using Azure PowerShell toosubmit Pig jobs tooa Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="81b4c-105">Pig consente i processi MapReduce toowrite tramite un linguaggio (alfabeto latino Pig) che modella le trasformazioni dei dati, anziché eseguire il mapping e ridurre le funzioni.</span><span class="sxs-lookup"><span data-stu-id="81b4c-105">Pig allows you toowrite MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="81b4c-106">Questo documento non fornisce una descrizione dettagliata delle operazioni eseguite istruzioni Pig latino hello utilizzate negli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="81b4c-106">This document does not provide a detailed description of what hello Pig Latin statements used in hello examples do.</span></span> <span data-ttu-id="81b4c-107">Per informazioni su hello Pig latini utilizzato in questo esempio, vedere [usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="81b4c-107">For information about hello Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="81b4c-108"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="81b4c-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="81b4c-109">**Un cluster Azure HDInsight**</span><span class="sxs-lookup"><span data-stu-id="81b4c-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="81b4c-110">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="81b4c-110">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="81b4c-111">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="81b4c-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="81b4c-112">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="81b4c-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="81b4c-113"><a id="powershell"></a>Eseguire processi Pig mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="81b4c-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="81b4c-114">Azure PowerShell fornisce *cmdlet* che consentono di tooremotely eseguire processi di Pig in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81b4c-114">Azure PowerShell provides *cmdlets* that allow you tooremotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="81b4c-115">Internamente, PowerShell Usa le chiamate REST troppo[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) in esecuzione nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="81b4c-115">Internally, PowerShell uses REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on hello HDInsight cluster.</span></span>

<span data-ttu-id="81b4c-116">i cmdlet seguenti Hello vengono utilizzati durante l'esecuzione di processi Pig in un cluster HDInsight remoto:</span><span class="sxs-lookup"><span data-stu-id="81b4c-116">hello following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="81b4c-117">**Account di accesso AzureRmAccount**: esegue l'autenticazione di Azure PowerShell tooyour sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="81b4c-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure Subscription</span></span>
* <span data-ttu-id="81b4c-118">**Nuovo AzureRmHDInsightPigJobDefinition**: crea un *definizione del processo* utilizzando hello specificato Pig latino istruzioni</span><span class="sxs-lookup"><span data-stu-id="81b4c-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using hello specified Pig Latin statements</span></span>
* <span data-ttu-id="81b4c-119">**Inizio AzureRmHDInsightJob**: invia hello processo definizione tooHDInsight, avvia il processo di hello e restituisce un *processo* oggetto che può essere utilizzato toocheck hello stato del processo di hello</span><span class="sxs-lookup"><span data-stu-id="81b4c-119">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="81b4c-120">**Attesa AzureRmHDInsightJob**: utilizza hello oggetto toocheck hello stato del processo del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="81b4c-120">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="81b4c-121">È in attesa fino a quando non è stato completato il processo di hello o è stato superato il tempo di attesa hello.</span><span class="sxs-lookup"><span data-stu-id="81b4c-121">It waits until hello job has completed, or hello wait time has been exceeded.</span></span>
* <span data-ttu-id="81b4c-122">**Get-AzureRmHDInsightJobOutput**: utilizzato l'output di hello tooretrieve del processo di hello</span><span class="sxs-lookup"><span data-stu-id="81b4c-122">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>

<span data-ttu-id="81b4c-123">Hello passaggi seguenti viene illustrato come toouse questi toorun cmdlet un processo il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="81b4c-123">hello following steps demonstrate how toouse these cmdlets toorun a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="81b4c-124">Utilizzando un editor, salvare hello seguente di codice come **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="81b4c-124">Using an editor, save hello following code as **pigjob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. <span data-ttu-id="81b4c-125">Aprire un nuovo prompt dei comandi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="81b4c-125">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="81b4c-126">Modificare il percorso toohello directory di hello **pigjob.ps1** file, quindi utilizzare lo script di comando toorun hello seguente hello:</span><span class="sxs-lookup"><span data-stu-id="81b4c-126">Change directories toohello location of hello **pigjob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="81b4c-127">Si è richiesta toolog in tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="81b4c-127">You are prompted toolog in tooyour Azure subscription.</span></span> <span data-ttu-id="81b4c-128">Quindi, viene richiesto per nome dell'account HTTPs/Admin hello e una password per il cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="81b4c-128">Then, you are asked for hello HTTPs/Admin account name and password for hello HDInsight cluster.</span></span>

2. <span data-ttu-id="81b4c-129">Al termine del processo di hello, deve restituire toohello di informazioni simili seguente testo:</span><span class="sxs-lookup"><span data-stu-id="81b4c-129">When hello job completes, it should return information similar toohello following text:</span></span>

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="81b4c-130"><a id="troubleshooting"></a>Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="81b4c-130"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="81b4c-131">Se viene restituita alcuna informazione quando hello processo viene completato, potrebbe essersi verificato un errore durante l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="81b4c-131">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="81b4c-132">informazioni sull'errore tooview per questo processo, aggiungere hello successivo comando toohello hello **pigjob.ps1** file, salvarlo e quindi eseguirla nuovamente.</span><span class="sxs-lookup"><span data-stu-id="81b4c-132">tooview error information for this job, add hello following command toohello end of hello **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="81b4c-133">Vengono restituite le informazioni di hello che è stato scritto tooSTDERR nel server di hello quando è stato eseguito il processo di hello e può essere utile determinare perché il processo di hello non è riuscito.</span><span class="sxs-lookup"><span data-stu-id="81b4c-133">This returns hello information that was written tooSTDERR on hello server when you ran hello job, and it may help determine why hello job is failing.</span></span>

## <span data-ttu-id="81b4c-134"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="81b4c-134"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="81b4c-135">Come si può notare, Azure PowerShell fornisce un modo semplice di toorun processi Pig in un cluster HDInsight, lo stato del processo di monitoraggio hello e output di hello recuperare.</span><span class="sxs-lookup"><span data-stu-id="81b4c-135">As you can see, Azure PowerShell provides an easy way toorun Pig jobs on an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <span data-ttu-id="81b4c-136"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="81b4c-136"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="81b4c-137">Per informazioni generali su Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="81b4c-137">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="81b4c-138">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="81b4c-138">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="81b4c-139">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="81b4c-139">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="81b4c-140">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="81b4c-140">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="81b4c-141">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="81b4c-141">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
