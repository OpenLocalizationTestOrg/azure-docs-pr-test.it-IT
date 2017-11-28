---
title: aaaUse Hadoop Hive in HDInsight - Azure PowerShell | Documenti Microsoft
description: Utilizzare le query Hive toorun di PowerShell in Hadoop in HDInsight.
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
ms.openlocfilehash: 9e0b72a25c5b12431f837b1a34a63ecc06223528
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-powershell"></a><span data-ttu-id="cc7bc-103">Esecuzione di query Hive usando PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc7bc-103">Run Hive queries using PowerShell</span></span>
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

<span data-ttu-id="cc7bc-104">Questo documento viene fornito un esempio dell'utilizzo di Azure PowerShell in query hello il gruppo di risorse di Azure in modalità toorun Hive in un Hadoop nel cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-104">This document provides an example of using Azure PowerShell in hello Azure Resource Group mode toorun Hive queries in a Hadoop on HDInsight cluster.</span></span>

> [!NOTE]
> <span data-ttu-id="cc7bc-105">Questo documento non fornisce una descrizione dettagliata delle operazioni eseguite le istruzioni HiveQL hello utilizzate negli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-105">This document does not provide a detailed description of what hello HiveQL statements that are used in hello examples do.</span></span> <span data-ttu-id="cc7bc-106">Per informazioni su hello HiveQL utilizzato in questo esempio, vedere [utilizzare Hive con Hadoop in HDInsight](hdinsight-use-hive.md).</span><span class="sxs-lookup"><span data-stu-id="cc7bc-106">For information on hello HiveQL that is used in this example, see [Use Hive with Hadoop on HDInsight](hdinsight-use-hive.md).</span></span>

<span data-ttu-id="cc7bc-107">**Prerequisiti**</span><span class="sxs-lookup"><span data-stu-id="cc7bc-107">**Prerequisites**</span></span>

* <span data-ttu-id="cc7bc-108">**Un cluster Azure HDInsight**: non è importante se il cluster di hello è Windows o basata su Linux.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-108">**An Azure HDInsight cluster**: It does not matter whether hello cluster is Windows or Linux-based.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="cc7bc-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="cc7bc-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="cc7bc-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="cc7bc-111">**Workstation con Azure PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-111">**A workstation with Azure PowerShell**.</span></span>

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a><span data-ttu-id="cc7bc-112">Eseguire query Hive usando Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="cc7bc-112">Run Hive queries using Azure PowerShell</span></span>

<span data-ttu-id="cc7bc-113">Azure PowerShell fornisce *cmdlet* che consentono di tooremotely eseguire query di Hive in HDInsight.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-113">Azure PowerShell provides *cmdlets* that allow you tooremotely run Hive queries on HDInsight.</span></span> <span data-ttu-id="cc7bc-114">Internamente, i cmdlet di hello supportano chiamate REST troppo[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) nel cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-114">Internally, hello cmdlets make REST calls too[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) on hello HDInsight cluster.</span></span>

<span data-ttu-id="cc7bc-115">i cmdlet seguenti Hello vengono utilizzati durante l'esecuzione di query Hive in un cluster HDInsight remoto:</span><span class="sxs-lookup"><span data-stu-id="cc7bc-115">hello following cmdlets are used when running Hive queries in a remote HDInsight cluster:</span></span>

* <span data-ttu-id="cc7bc-116">**AzureRmAccount aggiungere**: esegue l'autenticazione di Azure PowerShell tooyour sottoscrizione di Azure</span><span class="sxs-lookup"><span data-stu-id="cc7bc-116">**Add-AzureRmAccount**: Authenticates Azure PowerShell tooyour Azure subscription</span></span>
* <span data-ttu-id="cc7bc-117">**Nuovo AzureRmHDInsightHiveJobDefinition**: crea un *definizione del processo* utilizzando hello specificato istruzioni HiveQL</span><span class="sxs-lookup"><span data-stu-id="cc7bc-117">**New-AzureRmHDInsightHiveJobDefinition**: Creates a *job definition* by using hello specified HiveQL statements</span></span>
* <span data-ttu-id="cc7bc-118">**Inizio AzureRmHDInsightJob**: invia hello processo definizione tooHDInsight, avvia il processo di hello e restituisce un *processo* oggetto che può essere utilizzato toocheck hello stato del processo di hello</span><span class="sxs-lookup"><span data-stu-id="cc7bc-118">**Start-AzureRmHDInsightJob**: Sends hello job definition tooHDInsight, starts hello job, and returns a *job* object that can be used toocheck hello status of hello job</span></span>
* <span data-ttu-id="cc7bc-119">**Attesa AzureRmHDInsightJob**: utilizza hello oggetto toocheck hello stato del processo del processo di hello.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-119">**Wait-AzureRmHDInsightJob**: Uses hello job object toocheck hello status of hello job.</span></span> <span data-ttu-id="cc7bc-120">È in attesa fino a quando non viene completato il processo di hello o viene superato il tempo di attesa hello.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-120">It waits until hello job completes or hello wait time is exceeded.</span></span>
* <span data-ttu-id="cc7bc-121">**Get-AzureRmHDInsightJobOutput**: utilizzato l'output di hello tooretrieve del processo di hello</span><span class="sxs-lookup"><span data-stu-id="cc7bc-121">**Get-AzureRmHDInsightJobOutput**: Used tooretrieve hello output of hello job</span></span>
* <span data-ttu-id="cc7bc-122">**Invoke-AzureRmHDInsightHiveJob**: utilizzare le istruzioni HiveQL toorun.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-122">**Invoke-AzureRmHDInsightHiveJob**: Used toorun HiveQL statements.</span></span> <span data-ttu-id="cc7bc-123">Questa query di hello cmdlet blocchi viene completata, quindi restituisce i risultati di hello</span><span class="sxs-lookup"><span data-stu-id="cc7bc-123">This cmdlet blocks hello query completes, then returns hello results</span></span>
* <span data-ttu-id="cc7bc-124">**Utilizzare AzureRmHDInsightCluster**: set hello toouse cluster corrente per hello **Invoke AzureRmHDInsightHiveJob** comando</span><span class="sxs-lookup"><span data-stu-id="cc7bc-124">**Use-AzureRmHDInsightCluster**: Sets hello current cluster toouse for hello **Invoke-AzureRmHDInsightHiveJob** command</span></span>

<span data-ttu-id="cc7bc-125">Hello passaggi seguenti viene illustrato come toouse questi toorun cmdlet un processo del cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cc7bc-125">hello following steps demonstrate how toouse these cmdlets toorun a job in your HDInsight cluster:</span></span>

1. <span data-ttu-id="cc7bc-126">Utilizzando un editor, salvare hello seguente di codice come **hivejob.ps1**.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-126">Using an editor, save hello following code as **hivejob.ps1**.</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. <span data-ttu-id="cc7bc-127">Quindi, aprire un nuovo prompt dei comandi di **Azure PowerShell** .</span><span class="sxs-lookup"><span data-stu-id="cc7bc-127">Open a new **Azure PowerShell** command prompt.</span></span> <span data-ttu-id="cc7bc-128">Modificare il percorso toohello directory di hello **hivejob.ps1** file, quindi utilizzare lo script di comando toorun hello seguente hello:</span><span class="sxs-lookup"><span data-stu-id="cc7bc-128">Change directories toohello location of hello **hivejob.ps1** file, then use hello following command toorun hello script:</span></span>

        .\hivejob.ps1

    <span data-ttu-id="cc7bc-129">Quando si esegue lo script hello, verrà richiesta tooenter hello cluster nome e hello HTTPS/credenziali dell'account amministratore per il cluster hello.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-129">When hello script runs, you are prompted tooenter hello cluster name and hello HTTPS/Admin account credentials for hello cluster.</span></span> <span data-ttu-id="cc7bc-130">Potrebbe essere richiesta toolog in tooyour sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-130">You may also be prompted toolog in tooyour Azure subscription.</span></span>

3. <span data-ttu-id="cc7bc-131">Al termine del processo di hello, verrà restituito toohello di informazioni simili seguente testo:</span><span class="sxs-lookup"><span data-stu-id="cc7bc-131">When hello job completes, it returns information similar toohello following thext:</span></span>

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. <span data-ttu-id="cc7bc-132">Come accennato in precedenza, **Invoke-Hive** possono essere utilizzati toorun una query e attesa di risposta hello.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-132">As mentioned earlier, **Invoke-Hive** can be used toorun a query and wait for hello response.</span></span> <span data-ttu-id="cc7bc-133">Utilizzare i seguenti script toosee funzionamento tra Invoke-Hive hello:</span><span class="sxs-lookup"><span data-stu-id="cc7bc-133">Use hello following script toosee how Invoke-Hive works:</span></span>

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    <span data-ttu-id="cc7bc-134">output di Hello è simile hello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="cc7bc-134">hello output looks like hello following text:</span></span>

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > <span data-ttu-id="cc7bc-135">Per le query HiveQL più lungo, è possibile utilizzare hello Azure PowerShell **stringhe di tipo Here** cmdlet o HiveQL i file di script.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-135">For longer HiveQL queries, you can use hello Azure PowerShell **Here-Strings** cmdlet or HiveQL script files.</span></span> <span data-ttu-id="cc7bc-136">Hello seguente mostra come hello toouse **Invoke-Hive** cmdlet toorun un file di script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-136">hello following snippet shows how toouse hello **Invoke-Hive** cmdlet toorun a HiveQL script file.</span></span> <span data-ttu-id="cc7bc-137">file di script deve essere HiveQL Hello caricato toowasb: / /.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-137">hello HiveQL script file must be uploaded toowasb://.</span></span>
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > <span data-ttu-id="cc7bc-138">Per altre informazioni su **Here-Strings**, vedere <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell "Here-Strings"</a> (Uso di Here-Strings di Windows PowerShell).</span><span class="sxs-lookup"><span data-stu-id="cc7bc-138">For more information about **Here-Strings**, see <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell Here-Strings</a>.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="cc7bc-139">Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="cc7bc-139">Troubleshooting</span></span>

<span data-ttu-id="cc7bc-140">Se viene restituita alcuna informazione quando hello processo viene completato, potrebbe essersi verificato un errore durante l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-140">If no information is returned when hello job completes, an error may have occurred during processing.</span></span> <span data-ttu-id="cc7bc-141">informazioni sull'errore tooview per questo processo, aggiungere hello successivo alla fine di hello toohello **hivejob.ps1** file, salvarlo e quindi eseguirla nuovamente.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-141">tooview error information for this job, add hello following toohello end of hello **hivejob.ps1** file, save it, and then run it again.</span></span>

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

<span data-ttu-id="cc7bc-142">Questo cmdlet restituisce informazioni hello scritte tooSTDERR nel server di hello quando è stato eseguito il processo di hello.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-142">This cmdlet returns hello information that is written tooSTDERR on hello server when you ran hello job.</span></span>

## <a name="summary"></a><span data-ttu-id="cc7bc-143">Riepilogo</span><span class="sxs-lookup"><span data-stu-id="cc7bc-143">Summary</span></span>

<span data-ttu-id="cc7bc-144">Come si può notare, Azure PowerShell offre un modo semplice di toorun query Hive in un cluster HDInsight, hello di monitoraggio dello stato del processo e recuperare l'output di hello.</span><span class="sxs-lookup"><span data-stu-id="cc7bc-144">As you can see, Azure PowerShell provides an easy way toorun Hive queries in an HDInsight cluster, monitor hello job status, and retrieve hello output.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cc7bc-145">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cc7bc-145">Next steps</span></span>

<span data-ttu-id="cc7bc-146">Per informazioni generali su Hive in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cc7bc-146">For general information about Hive in HDInsight:</span></span>

* [<span data-ttu-id="cc7bc-147">Usare Hive con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cc7bc-147">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="cc7bc-148">Per informazioni su altre modalità d'uso di Hadoop in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="cc7bc-148">For information about other ways you can work with Hadoop on HDInsight:</span></span>

* [<span data-ttu-id="cc7bc-149">Usare Pig con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cc7bc-149">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="cc7bc-150">Usare MapReduce con Hadoop in HDInsight</span><span class="sxs-lookup"><span data-stu-id="cc7bc-150">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)
