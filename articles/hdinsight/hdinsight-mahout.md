---
title: le indicazioni relative aaaGenerate tramite Mahout HDInsight da PowerShell - Azure | Documenti Microsoft
description: Informazioni su come toouse hello Apache Mahout di machine learning indicazioni di film libreria toogenerate con HDInsight (Hadoop) da uno script di PowerShell in esecuzione nel client.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 07b57208-32aa-4e59-900a-6c934fa1b7a7
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: larryfr
ms.openlocfilehash: 675a2cd8ecaf7fc797d6cd094e4e58f9aca7ed92
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="c5358-103">Generare raccomandazioni di film mediante Apache Mahout con Hadoop in HDInsight (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="c5358-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="c5358-104">Informazioni su come hello toouse [Mahout Apache](http://mahout.apache.org) libreria learning macchina con le raccomandazioni di Azure HDInsight toogenerate film.</span><span class="sxs-lookup"><span data-stu-id="c5358-104">Learn how toouse hello [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight toogenerate movie recommendations.</span></span> <span data-ttu-id="c5358-105">esempio Hello in questo documento usa Azure PowerShell toorun Mahout processi.</span><span class="sxs-lookup"><span data-stu-id="c5358-105">hello example in this document uses Azure PowerShell toorun Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5358-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c5358-106">Prerequisites</span></span>

* <span data-ttu-id="c5358-107">Un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="c5358-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="c5358-108">Per informazioni su come crearne uno, vedere [Introduzione all'uso di Hadoop basato su Linux in HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="c5358-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5358-109">Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="c5358-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c5358-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c5358-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="c5358-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5358-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="c5358-112"><a name="recommendations"></a>Generare raccomandazioni con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5358-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="c5358-113">il processo di Hello in questa sezione funziona tramite Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5358-113">hello job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="c5358-114">Molte delle classi di hello fornite con Mahout attualmente non si collabora con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="c5358-114">Many of hello classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="c5358-115">Per un elenco di classi che non funzionano con Azure PowerShell, vedere hello [Troubleshooting](#troubleshooting) sezione.</span><span class="sxs-lookup"><span data-stu-id="c5358-115">For a list of classes that do not work with Azure PowerShell, see hello [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="c5358-116">Per un esempio di utilizzo di SSH tooconnect tooHDInsight ed esempi di Mahout esecuzione direttamente nel cluster di hello, vedere [generare le indicazioni di film utilizzando Mahout e HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="c5358-116">For an example of using SSH tooconnect tooHDInsight and run Mahout examples directly on hello cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="c5358-117">Una delle funzioni hello fornito da Mahout è un motore di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="c5358-117">One of hello functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="c5358-118">Questo motore accetta i dati in formato hello `userID`, `itemId`, e `prefValue` (hello preferenza agli utenti per l'elemento hello).</span><span class="sxs-lookup"><span data-stu-id="c5358-118">This engine accepts data in hello format of `userID`, `itemId`, and `prefValue` (hello users preference for hello item).</span></span> <span data-ttu-id="c5358-119">Mahout Usa gli utenti di hello dati toodetermine con preferenze simili-item, che possono essere utilizzato toomake indicazioni.</span><span class="sxs-lookup"><span data-stu-id="c5358-119">Mahout uses hello data toodetermine users with like-item preferences, which can be used toomake recommendations.</span></span>

<span data-ttu-id="c5358-120">Hello seguito è riportata una panoramica di come funziona il processo di raccomandazione hello semplificata:</span><span class="sxs-lookup"><span data-stu-id="c5358-120">hello following example is a simplified walk-through of how hello recommendation process works:</span></span>

* <span data-ttu-id="c5358-121">**CO-occorrenza**: Joe, Alice e Bob tutti stato apprezzato *stella attraverso*, *hello Empire colpisce nuovamente*, e *restituzione di hello Jedi*.</span><span class="sxs-lookup"><span data-stu-id="c5358-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *hello Empire Strikes Back*, and *Return of hello Jedi*.</span></span> <span data-ttu-id="c5358-122">Mahout determina che gli utenti come uno di questi film anche hello altri due.</span><span class="sxs-lookup"><span data-stu-id="c5358-122">Mahout determines that users who like any one of these movies also like hello other two.</span></span>

* <span data-ttu-id="c5358-123">**CO-occorrenza**: Bob e Alice anche ritengono *hello Phantom alieni*, *attacco dei cloni di hello*, e *ritorsioni di hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="c5358-123">**co-occurrence**: Bob and Alice also liked *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span> <span data-ttu-id="c5358-124">Mahout determina che gli utenti che ritengono tre filmati precedente hello anche come questi film.</span><span class="sxs-lookup"><span data-stu-id="c5358-124">Mahout determines that users who liked hello previous three movies also like these movies.</span></span>

* <span data-ttu-id="c5358-125">**Indicazione di somiglianza**: Joe perché ritengono hello primi tre film, Mahout esamina filmati che altri utenti con preferenze simili ritengono, ma Joe ha non controllata (ritengono/classificazione).</span><span class="sxs-lookup"><span data-stu-id="c5358-125">**Similarity recommendation**: Because Joe liked hello first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="c5358-126">In questo caso, si consiglia Mahout *hello Phantom alieni*, *attacco dei cloni di hello*, e *ritorsioni di hello Sith*.</span><span class="sxs-lookup"><span data-stu-id="c5358-126">In this case, Mahout recommends *hello Phantom Menace*, *Attack of hello Clones*, and *Revenge of hello Sith*.</span></span>

### <a name="understanding-hello-data"></a><span data-ttu-id="c5358-127">Informazioni sui dati hello</span><span class="sxs-lookup"><span data-stu-id="c5358-127">Understanding hello data</span></span>

<span data-ttu-id="c5358-128">[GroupLens Research][movielens] offre i dati di classificazione dei film in un formato compatibile con Mahout.</span><span class="sxs-lookup"><span data-stu-id="c5358-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="c5358-129">Questi dati sono disponibili in spazio di archiviazione di hello predefinito per il cluster in `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="c5358-129">This data is available on hello default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="c5358-130">Sono disponibili due file, `moviedb.txt` (informazioni su filmati hello) e `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="c5358-130">There are two files, `moviedb.txt` (information about hello movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="c5358-131">Hello `user-ratings.txt` file viene utilizzato durante l'analisi.</span><span class="sxs-lookup"><span data-stu-id="c5358-131">hello `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="c5358-132">Hello `moviedb.txt` file è testo descrittivo tooprovide utilizzato durante la visualizzazione dei risultati dell'analisi hello hello.</span><span class="sxs-lookup"><span data-stu-id="c5358-132">hello `moviedb.txt` file is used tooprovide user-friendly text when displaying hello results of hello analysis.</span></span>

<span data-ttu-id="c5358-133">dati contenuti in utente ratings.txt Hello presenta una struttura di `userID`, `movieID`, `userRating`, e `timestamp`, che indica come elevata ogni utente classificato un filmato.</span><span class="sxs-lookup"><span data-stu-id="c5358-133">hello data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="c5358-134">Di seguito è riportato un esempio di dati hello:</span><span class="sxs-lookup"><span data-stu-id="c5358-134">Here is an example of hello data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a><span data-ttu-id="c5358-135">Eseguire il processo di hello</span><span class="sxs-lookup"><span data-stu-id="c5358-135">Run hello job</span></span>

<span data-ttu-id="c5358-136">Utilizzare hello seguente script di Windows PowerShell toorun un processo che utilizza il motore di raccomandazione Mahout hello con dati film hello:</span><span class="sxs-lookup"><span data-stu-id="c5358-136">Use hello following Windows PowerShell script toorun a job that uses hello Mahout recommendation engine with hello movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="c5358-137">Questo file verranno richieste informazioni sul cluster di HDInsight tooyour tooconnect utilizzati e i processi di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c5358-137">This file prompts you for information that is used tooconnect tooyour HDInsight cluster and run jobs.</span></span> <span data-ttu-id="c5358-138">Può richiedere alcuni minuti per toocomplete processi hello e scaricare i file di output. txt hello.</span><span class="sxs-lookup"><span data-stu-id="c5358-138">It may take several minutes for hello jobs toocomplete and download hello output.txt file.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> <span data-ttu-id="c5358-139">I processi di mahout non rimuovere i dati temporanei creati durante l'elaborazione di processi di hello.</span><span class="sxs-lookup"><span data-stu-id="c5358-139">Mahout jobs do not remove temporary data that is created while processing hello job.</span></span> <span data-ttu-id="c5358-140">Hello `--tempDir` viene specificato in file temporanei di hello esempio processo tooisolate hello in una directory specifica.</span><span class="sxs-lookup"><span data-stu-id="c5358-140">hello `--tempDir` parameter is specified in hello example job tooisolate hello temporary files into a specific directory.</span></span>

<span data-ttu-id="c5358-141">Hello Mahout job non restituisce tooSTDOUT output hello.</span><span class="sxs-lookup"><span data-stu-id="c5358-141">hello Mahout job does not return hello output tooSTDOUT.</span></span> <span data-ttu-id="c5358-142">Al contrario, viene memorizzato nella directory di output specificata hello come **parte-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="c5358-142">Instead, it stores it in hello specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="c5358-143">script Hello Scarica il file troppo**txt** nella directory corrente di hello nella workstation.</span><span class="sxs-lookup"><span data-stu-id="c5358-143">hello script downloads this file too**output.txt** in hello current directory on your workstation.</span></span>

<span data-ttu-id="c5358-144">Hello testo riportato di seguito è riportato un esempio del contenuto di hello di questo file:</span><span class="sxs-lookup"><span data-stu-id="c5358-144">hello following text is an example of hello content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="c5358-145">prima colonna Hello è hello `userID`.</span><span class="sxs-lookup"><span data-stu-id="c5358-145">hello first column is hello `userID`.</span></span> <span data-ttu-id="c5358-146">Hello valori contenuti in ' [' e ']' sono `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="c5358-146">hello values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="c5358-147">script Hello scarica anche hello `moviedb.txt` e `user-ratings.txt` file, che sono necessari tooformat hello output toobe più leggibile.</span><span class="sxs-lookup"><span data-stu-id="c5358-147">hello script also downloads hello `moviedb.txt` and `user-ratings.txt` files, which are needed tooformat hello output toobe more readable.</span></span>

### <a name="view-hello-output"></a><span data-ttu-id="c5358-148">Visualizzazione output di hello</span><span class="sxs-lookup"><span data-stu-id="c5358-148">View hello output</span></span>

<span data-ttu-id="c5358-149">Anche se hello output generato potrebbe essere OK per l'utilizzo in un'applicazione, non è semplice.</span><span class="sxs-lookup"><span data-stu-id="c5358-149">Although hello generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="c5358-150">Hello `moviedb.txt` da hello server può essere utilizzato tooresolve hello `movieId` nome film tooa.</span><span class="sxs-lookup"><span data-stu-id="c5358-150">hello `moviedb.txt` from hello server can be used tooresolve hello `movieId` tooa movie name.</span></span> <span data-ttu-id="c5358-151">Utilizzare hello indicazioni toodisplay allo script di PowerShell con nomi di film seguenti:</span><span class="sxs-lookup"><span data-stu-id="c5358-151">Use hello following PowerShell script toodisplay recommendations with movie names:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

<span data-ttu-id="c5358-152">Utilizzare hello indicazioni hello toodisplay di comando in un formato descrittivo seguente:</span><span class="sxs-lookup"><span data-stu-id="c5358-152">Use hello following command toodisplay hello recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="c5358-153">Hello l'output è simile toohello seguente testo:</span><span class="sxs-lookup"><span data-stu-id="c5358-153">hello output is similar toohello following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, hello (1997)                  1
    Alien: Resurrection (1997)               3
    187 (1997)                               2
    (lines ommitted)

    ---------------------------
    Recommended movies
    ---------------------------

    Movie                                    Score
    -----                                    -----
    Good Will Hunting (1997)                 4.6504064
    Swingers (1996)                          4.6862745
    Wings of hello Dove, hello (1997)            4.6666665
    People vs. Larry Flynt, hello (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="c5358-154"><a name="troubleshooting"></a>Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="c5358-154"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="c5358-155">Impossibile sovrascrivere i file</span><span class="sxs-lookup"><span data-stu-id="c5358-155">Cannot overwrite files</span></span>

<span data-ttu-id="c5358-156">I processi Mahout non eliminano i file temporanei creati durante l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="c5358-156">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="c5358-157">Inoltre, i processi di hello non sovrascrivono i file di output esistente.</span><span class="sxs-lookup"><span data-stu-id="c5358-157">In addition, hello jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="c5358-158">tooavoid errori quando si eseguono processi Mahout, eliminare i file temporanei e di output tra le esecuzioni.</span><span class="sxs-lookup"><span data-stu-id="c5358-158">tooavoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="c5358-159">file hello tooremove creati da hello script precedente in questo documento, usare hello lo script di PowerShell seguente:</span><span class="sxs-lookup"><span data-stu-id="c5358-159">tooremove hello files created by hello earlier scripts in this document, use hello following PowerShell script:</span></span>

```powershell
# Login tooyour Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter hello HDInsight cluster name"
$creds=Get-Credential -Message "Enter hello login for hello cluster"

#Get hello cluster info so we can get hello resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload hello file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have tooget a list and delete one at a time
# Start with hello output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next hello temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="c5358-160"><a name="nopowershell"></a>Classi che non funzionano con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="c5358-160"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="c5358-161">I processi di mahout che utilizzano le seguenti classi hello restituiscono vari messaggi di errore quando viene utilizzata da Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="c5358-161">Mahout jobs that use hello following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="c5358-162">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="c5358-162">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="c5358-163">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="c5358-163">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="c5358-164">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="c5358-164">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="c5358-165">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="c5358-165">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="c5358-166">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="c5358-166">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="c5358-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="c5358-167">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="c5358-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="c5358-168">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="c5358-169">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="c5358-169">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="c5358-170">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="c5358-170">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="c5358-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="c5358-171">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="c5358-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="c5358-172">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="c5358-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="c5358-173">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="c5358-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="c5358-174">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="c5358-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="c5358-175">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="c5358-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="c5358-176">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="c5358-177">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="c5358-177">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="c5358-178">i processi di toorun che utilizzano queste classi, connettere il cluster di HDInsight toohello tramite SSH ed eseguire i processi di hello dalla riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="c5358-178">toorun jobs that use these classes, connect toohello HDInsight cluster using SSH and run hello jobs from hello command line.</span></span> <span data-ttu-id="c5358-179">Per un esempio di utilizzo di SSH toorun Mahout processi, vedere [generare le indicazioni di film utilizzando Mahout e HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="c5358-179">For an example of using SSH toorun Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5358-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c5358-180">Next steps</span></span>

<span data-ttu-id="c5358-181">Ora che si è appreso come toouse Mahout, individuare altri modi di utilizzo dei dati in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c5358-181">Now that you have learned how toouse Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="c5358-182">Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="c5358-182">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="c5358-183">Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="c5358-183">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="c5358-184">MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="c5358-184">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

[build]: http://mahout.apache.org/developers/buildingmahout.html
[aps]: /powershell/azureps-cmdlets-docs
[movielens]: http://grouplens.org/datasets/movielens/
[100k]: http://files.grouplens.org/datasets/movielens/ml-100k.zip
[getstarted]: hdinsight-hadoop-linux-tutorial-get-started.md
[upload]: hdinsight-upload-data.md
[ml]: http://en.wikipedia.org/wiki/Machine_learning
[forest]: http://en.wikipedia.org/wiki/Random_forest
[enableremote]: ./media/hdinsight-mahout/enableremote.png
[connect]: ./media/hdinsight-mahout/connect.png
[hadoopcli]: ./media/hdinsight-mahout/hadoopcli.png
[tools]: https://github.com/Blackmist/hdinsight-tools
