---
title: Usare Pig di Hadoop con PowerShell in HDInsight - Azure | Microsoft Docs
description: Informazioni su come inviare processi Pig a un cluster Hadoop in HDInsight con Azure PowerShell.
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
ms.openlocfilehash: 28904b07609ffb40a8195278fd1afd3957896733
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="use-azure-powershell-to-run-pig-jobs-with-hdinsight"></a><span data-ttu-id="d12b5-103">Usare Azure PowerShell per eseguire processi Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="d12b5-103">Use Azure PowerShell to run Pig jobs with HDInsight</span></span>

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

<span data-ttu-id="d12b5-104">Questo documento fornisce un esempio di come usare Azure PowerShell per inviare processi Pig in un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d12b5-104">This document provides an example of using Azure PowerShell to submit Pig jobs to a Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="d12b5-105">Pig consente di scrivere processi MapReduce usando un linguaggio (Pig Latin) che modella le trasformazioni di dati, anziché eseguire il mapping e la riduzione delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="d12b5-105">Pig allows you to write MapReduce jobs by using a language (Pig Latin) that models data transformations, rather than map and reduce functions.</span></span>

> [!NOTE]
> <span data-ttu-id="d12b5-106">Questo documento non fornisce una descrizione dettagliata delle operazioni eseguite dalle istruzioni Pig Latin usate negli esempi.</span><span class="sxs-lookup"><span data-stu-id="d12b5-106">This document does not provide a detailed description of what the Pig Latin statements used in the examples do.</span></span> <span data-ttu-id="d12b5-107">Per informazioni sul codice Pig Latin usato in questo esempio, vedere [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md).</span><span class="sxs-lookup"><span data-stu-id="d12b5-107">For information about the Pig Latin used in this example, see [Use Pig with Hadoop on HDInsight](hdinsight-use-pig.md).</span></span>

## <span data-ttu-id="d12b5-108"><a id="prereq"></a>Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d12b5-108"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="d12b5-109">**Un cluster Azure HDInsight**</span><span class="sxs-lookup"><span data-stu-id="d12b5-109">**An Azure HDInsight cluster**</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="d12b5-110">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="d12b5-110">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="d12b5-111">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="d12b5-111">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="d12b5-112">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="d12b5-112">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <span data-ttu-id="d12b5-113"><a id="powershell"></a>Eseguire processi Pig mediante PowerShell</span><span class="sxs-lookup"><span data-stu-id="d12b5-113"><a id="powershell"></a>Run Pig jobs using PowerShell</span></span>

<span data-ttu-id="d12b5-114">Azure PowerShell fornisce *cmdlet* che consentono di eseguire in modalità remota processi Pig in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d12b5-114">Azure PowerShell provides *cmdlets* that allow you to remotely run Pig jobs on HDInsight.</span></span> <span data-ttu-id="d12b5-115">PowerShell internamente usa le chiamate REST verso [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) in esecuzione nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d12b5-115">Internally, PowerShell uses REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) running on the HDInsight cluster.</span></span>

<span data-ttu-id="d12b5-116">Durante l'esecuzione di processi Pig in un cluster HDInsight remoto, vengono usati i seguenti cmdlet:</span><span class="sxs-lookup"><span data-stu-id="d12b5-116">The following cmdlets are used when running Pig jobs on a remote HDInsight cluster:</span></span>

* <span data-ttu-id="d12b5-117">**Login-AzureRmAccount**: autentica Azure PowerShell nella sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="d12b5-117">**Login-AzureRmAccount**: Authenticates Azure PowerShell to your Azure Subscription</span></span>
* <span data-ttu-id="d12b5-118">**New-AzureRmHDInsightPigJobDefinition**: crea una *definizione del processo* usando le istruzioni Pig Latin specificate</span><span class="sxs-lookup"><span data-stu-id="d12b5-118">**New-AzureRmHDInsightPigJobDefinition**: Creates a *job definition* by using the specified Pig Latin statements</span></span>
* <span data-ttu-id="d12b5-119">**Start-AzureRmHDInsightJob**: invia la definizione del processo a HDInsight, avvia il processo e restituisce un oggetto *job* che può essere usato per verificare lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="d12b5-119">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="d12b5-120">**Wait-AzureRmHDInsightJob**: usa l'oggetto job per verificare lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="d12b5-120">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="d12b5-121">Attende che il processo venga completato o che scada il periodo di attesa previsto.</span><span class="sxs-lookup"><span data-stu-id="d12b5-121">It waits until the job has completed, or the wait time has been exceeded.</span></span>
* <span data-ttu-id="d12b5-122">**Get-AzureRmHDInsightJobOutput**: viene usato per recuperare l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="d12b5-122">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>

<span data-ttu-id="d12b5-123">La seguente procedura illustra come usare questi cmdlet per eseguire un processo nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d12b5-123">The following steps demonstrate how to use these cmdlets to run a job on your HDInsight cluster.</span></span>

1. <span data-ttu-id="d12b5-124">Usando un editor, salvare il seguente codice come **pigjob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="d12b5-124">Using an editor, save the following code as **pigjob.ps1**.</span></span>

    <span data-ttu-id="d12b5-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span><span class="sxs-lookup"><span data-stu-id="d12b5-125">[!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]</span></span>

1. <span data-ttu-id="d12b5-126">Aprire un nuovo prompt dei comandi di Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d12b5-126">Open a new Windows PowerShell command prompt.</span></span> <span data-ttu-id="d12b5-127">Passare al percorso del file **pigjob.ps1** , quindi usare il seguente comando per eseguire lo script:</span><span class="sxs-lookup"><span data-stu-id="d12b5-127">Change directories to the location of the **pigjob.ps1** file, then use the following command to run the script:</span></span>

        .\pigjob.ps1

    <span data-ttu-id="d12b5-128">Viene richiesto di accedere alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d12b5-128">You are prompted to log in to your Azure subscription.</span></span> <span data-ttu-id="d12b5-129">Vengono quindi richiesti il nome dell'account HTTPS/Amministratore e la password per il cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="d12b5-129">Then, you are asked for the HTTPs/Admin account name and password for the HDInsight cluster.</span></span>

2. <span data-ttu-id="d12b5-130">Quando viene completato, il processo restituisce informazioni simili alle seguenti:</span><span class="sxs-lookup"><span data-stu-id="d12b5-130">When the job completes, it should return information similar to the following text:</span></span>

        Start the Pig job ...
        Wait for the Pig job to complete ...
        Display the standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <span data-ttu-id="d12b5-131"><a id="troubleshooting"></a>Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="d12b5-131"><a id="troubleshooting"></a>Troubleshooting</span></span>

<span data-ttu-id="d12b5-132">Se al termine del processo non vengono restituite informazioni, potrebbe essersi verificato un errore durante l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="d12b5-132">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="d12b5-133">Per visualizzare informazioni relative all'errore per questo processo, aggiungere il seguente comando alla fine del file **pigjob.ps1** , salvare il file, quindi eseguirlo nuovamente.</span><span class="sxs-lookup"><span data-stu-id="d12b5-133">To view error information for this job, add the following command to the end of the **pigjob.ps1** file, save it, and then run it again.</span></span>

    # Print the output of the Pig job.
    Write-Host "Display the standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

<span data-ttu-id="d12b5-134">Vengono restituite le informazioni scritte in STDERR nel server durante l'esecuzione del processo. Tali informazioni possono essere utili per determinare la causa del problema.</span><span class="sxs-lookup"><span data-stu-id="d12b5-134">This returns the information that was written to STDERR on the server when you ran the job, and it may help determine why the job is failing.</span></span>

## <span data-ttu-id="d12b5-135"><a id="summary"></a>Riepilogo</span><span class="sxs-lookup"><span data-stu-id="d12b5-135"><a id="summary"></a>Summary</span></span>
<span data-ttu-id="d12b5-136">Come è possibile notare, Azure PowerShell fornisce un modo semplice per eseguire processi Pig in un cluster HDInsight, monitorare lo stato del processo e recuperare l'output.</span><span class="sxs-lookup"><span data-stu-id="d12b5-136">As you can see, Azure PowerShell provides an easy way to run Pig jobs on an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <span data-ttu-id="d12b5-137"><a id="nextsteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d12b5-137"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="d12b5-138">Per informazioni generali su Pig in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d12b5-138">For general information about Pig in HDInsight:</span></span>

* [<span data-ttu-id="d12b5-139">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d12b5-139">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="d12b5-140">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="d12b5-140">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="d12b5-141">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d12b5-141">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="d12b5-142">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="d12b5-142">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
