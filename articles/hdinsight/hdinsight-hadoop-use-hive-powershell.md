---
title: Usare Hive di Hadoop con PowerShell in HDInsight - Azure | Microsoft Docs
description: Usare PowerShell per eseguire query Hive in Hadoop in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cb795b7c-bcd0-497a-a7f0-8ed18ef49195
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: e1cb2e4a1fc82fb43082e79a5feba71b81b3eaa8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="7b1c9-103">Esecuzione di query Hive usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b1c9-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="7b1c9-104">Questo documento fornisce un esempio di come usare Azure PowerShell nel gruppo di risorse Azure per eseguire query Hive in un cluster Hadoop in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-104">This document provides an example of using Azure PowerShell in the Azure Resource Group mode to run Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="7b1c9-105">Questo documento non fornisce una descrizione dettagliata delle operazioni eseguite dalle istruzioni HiveQL usate negli esempi.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-105">This document does not provide a detailed description of what the HiveQL statements that are used in the examples do.</span></span> <span data-ttu-id="7b1c9-106">Per informazioni sul codice HiveQL usato in questo esempio, vedere [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="7b1c9-106">For information on the HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="7b1c9-107">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="7b1c9-107">**Prerequisites**</span></span>

* <span data-ttu-id="7b1c9-108">**Un cluster Azure HDInsight**: non è importante che il cluster sia basato su Windows o su Linux.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-108">**An Azure HDInsight cluster**: It does not matter whether the cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="7b1c9-109">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7b1c9-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7b1c9-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="7b1c9-111">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="7b1c9-112">Eseguire query Hive usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b1c9-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="7b1c9-113">Azure PowerShell fornisce *cmdlet* che consentono di eseguire in modalità remota query Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-113">Azure PowerShell provides *cmdlets* that allow you to remotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="7b1c9-114">I cmdlet effettuano internamente chiamate REST a [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) sul cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-114">Internally, the cmdlets make REST calls to [WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on the HDInsight cluster.</span></span>

<span data-ttu-id="7b1c9-115">Durante l'esecuzione di query Hive in un cluster HDInsight remoto, vengono usati i seguenti cmdlet:</span><span class="sxs-lookup"><span data-stu-id="7b1c9-115">The following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="7b1c9-116">**Add-AzureRmAccount**: autentica Azure PowerShell nella sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="7b1c9-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell to your Azure subscription</span></span>
* <span data-ttu-id="7b1c9-117">**New-AzureRmHDInsightHiveJobDefinition**: crea una *definizione del processo* usando le istruzioni HiveQL specificate.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using the specified HiveQL statements</span></span>
* <span data-ttu-id="7b1c9-118">**Start-AzureRmHDInsightJob**: invia la definizione del processo a HDInsight, avvia il processo e restituisce un oggetto *job* che può essere usato per verificare lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-118">**Start-AzureRmHDInsightJob**: Sends the job definition to HDInsight, starts the job, and returns a *job* object that can be used to check the status of the job</span></span>
* <span data-ttu-id="7b1c9-119">**Wait-AzureRmHDInsightJob**: usa l'oggetto job per verificare lo stato del processo.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-119">**Wait-AzureRmHDInsightJob**: Uses the job object to check the status of the job.</span></span> <span data-ttu-id="7b1c9-120">Attende che il processo venga completato o che scada il periodo di attesa previsto.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-120">It waits until the job completes or the wait time is exceeded.</span></span>
* <span data-ttu-id="7b1c9-121">**Get-AzureRmHDInsightJobOutput**: viene usato per recuperare l'output del processo.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-121">**Get-AzureRmHDInsightJobOutput**: Used to retrieve the output of the job</span></span>
* <span data-ttu-id="7b1c9-122">**Invoke-AzureRmHDInsightHiveJob**: viene usato per eseguire istruzioni HiveQL.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-122">**Invoke-AzureRmHDInsightHiveJob**: Used to run HiveQL statements.</span></span> <span data-ttu-id="7b1c9-123">Questo cmdlet blocca il completamento della query, quindi restituisce i risultati</span><span class="sxs-lookup"><span data-stu-id="7b1c9-123">This cmdlet blocks the query completes, then returns the results</span></span>
* <span data-ttu-id="7b1c9-124">**Use-AzureRmHDInsightCluster**: imposta il cluster corrente per l'uso per il comando **Invoke-AzureRmHDInsightHiveJob**.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-124">**Use-AzureRmHDInsightCluster**: Sets the current cluster to use for the **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="7b1c9-125">La seguente procedura illustra come usare questi cmdlet per eseguire un processo nel cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7b1c9-125">The following steps demonstrate how to use these cmdlets to run a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="7b1c9-126">Usando un editor, salvare il seguente codice come **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-126">Using an editor, save the following code as **hivejob.ps1**.</span></span>

    <span data-ttu-id="7b1c9-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span><span class="sxs-lookup"><span data-stu-id="7b1c9-127">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]</span></span>

2. <span data-ttu-id="7b1c9-128">Quindi, aprire un nuovo prompt dei comandi di **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="7b1c9-128">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="7b1c9-129">Passare al percorso del file **hivejob.ps1** , quindi usare il seguente comando per eseguire lo script:</span><span class="sxs-lookup"><span data-stu-id="7b1c9-129">Change directories to the location of the **hivejob.ps1** file, then use the following command to run the script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="7b1c9-130">Quando viene eseguito lo script, viene richiesto di immettere il nome cluster e le credenziali dell'account HTTPS/Admin per il cluster.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-130">When the script runs, you are prompted to enter the cluster name and the HTTPS/Admin account credentials for the cluster.</span></span> <span data-ttu-id="7b1c9-131">Può anche essere richiesto di eseguire l'accesso alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-131">You may also be prompted to log in to your Azure subscription.</span></span>

3. <span data-ttu-id="7b1c9-132">Al termine, il processo restituisce informazioni simili al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="7b1c9-132">When the job completes, it returns information similar to the following thext:</span></span>

        Display the standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="7b1c9-133">Come accennato in precedenza, **Invoke-Hive** può essere usato per eseguire una query e attendere la risposta.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-133">As mentioned earlier, **Invoke-Hive** can be used to run a query and wait for the response.</span></span> <span data-ttu-id="7b1c9-134">Usare lo script seguente per verificare il funzionamento di Invoke-Hive:</span><span class="sxs-lookup"><span data-stu-id="7b1c9-134">Use the following script to see how Invoke-Hive works:</span></span>

    <span data-ttu-id="7b1c9-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span><span class="sxs-lookup"><span data-stu-id="7b1c9-135">[!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]</span></span>

    <span data-ttu-id="7b1c9-136">L'output ha un aspetto simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="7b1c9-136">The output looks like the following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="7b1c9-137">Per query HiveQL più lunghe, è possibile usare il cmdlet **Here-Strings** di Azure PowerShell o un file di script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-137">For longer HiveQL queries, you can use the Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="7b1c9-138">Nel frammento di codice seguente viene illustrato come usare il cmdlet **Invoke-Hive** per eseguire un file di script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-138">The following snippet shows how to use the **Invoke-Hive** cmdlet to run a HiveQL script file.</span></span> <span data-ttu-id="7b1c9-139">Il file di script HiveQL deve essere caricato in wasb://.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-139">The HiveQL script file must be uploaded to wasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="7b1c9-140">Per altre informazioni su **Here-Strings**, vedere <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell "Here-Strings"</a> (Uso di Here-Strings di Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="7b1c9-140">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7b1c9-141">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="7b1c9-141">Troubleshooting</span></span>

<span data-ttu-id="7b1c9-142">Se al termine del processo non vengono restituite informazioni, potrebbe essersi verificato un errore durante l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-142">If no information is returned when the job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="7b1c9-143">Per visualizzare informazioni relative all'errore per questo processo, aggiungere quanto segue alla fine del file **hivejob.ps1** , salvare il file, quindi eseguirlo nuovamente.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-143">To view error information for this job, add the following to the end of the **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print the output of the Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="7b1c9-144">Questo cmdlet restituisce le informazioni scritte in STDERR nel server durante l'esecuzione del processo.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-144">This cmdlet returns the information that is written to STDERR on the server when you ran the job.</span></span>

## <a name="summary"></a><span data-ttu-id="7b1c9-145">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="7b1c9-145">Summary</span></span>

<span data-ttu-id="7b1c9-146">Come è possibile notare, Azure PowerShell fornisce un modo semplice per eseguire query Hive in un cluster HDInsight, monitorare lo stato del processo e recuperare l'output.</span><span class="sxs-lookup"><span data-stu-id="7b1c9-146">As you can see, Azure PowerShell provides an easy way to run Hive queries in an HDInsight cluster, monitor the job status, and retrieve the output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b1c9-147">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7b1c9-147">Next steps</span></span>

<span data-ttu-id="7b1c9-148">Per informazioni generali su Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7b1c9-148">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="7b1c9-149">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b1c9-149">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="7b1c9-150">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="7b1c9-150">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="7b1c9-151">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b1c9-151">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="7b1c9-152">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="7b1c9-152">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
