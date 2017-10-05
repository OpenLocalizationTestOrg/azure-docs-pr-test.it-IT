---
title: Generare raccomandazioni da PowerShell con HDInsight basato su Mahout - Azure | Microsoft Docs
description: Informazioni su come usare la libreria di Machine Learning Apache Mahout per generare raccomandazioni di film con HDInsight (Hadoop) da uno script PowerShell in esecuzione sul client dell'utente.
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
ms.openlocfilehash: 934de9ca2df48b29ef7a56d5729d59d77875ea7b
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/18/2017
---
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a><span data-ttu-id="63cf7-103">Generare raccomandazioni di film mediante Apache Mahout con Hadoop in HDInsight (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="63cf7-103">Generate movie recommendations by using Apache Mahout with Hadoop in HDInsight (PowerShell)</span></span>

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

<span data-ttu-id="63cf7-104">Informazioni su come usare la libreria di Machine Learning [Apache Mahout](http://mahout.apache.org) con Azure HDInsight per generare raccomandazioni di film.</span><span class="sxs-lookup"><span data-stu-id="63cf7-104">Learn how to use the [Apache Mahout](http://mahout.apache.org) machine learning library with Azure HDInsight to generate movie recommendations.</span></span> <span data-ttu-id="63cf7-105">L'esempio riportato in questo documento usa Azure PowerShell per eseguire i processi Mahout.</span><span class="sxs-lookup"><span data-stu-id="63cf7-105">The example in this document uses Azure PowerShell to run Mahout jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="63cf7-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="63cf7-106">Prerequisites</span></span>

* <span data-ttu-id="63cf7-107">Un cluster HDInsight basato su Linux.</span><span class="sxs-lookup"><span data-stu-id="63cf7-107">A Linux-based HDInsight cluster.</span></span> <span data-ttu-id="63cf7-108">Per informazioni su come crearne uno, vedere [Introduzione all'uso di Hadoop basato su Linux in HDInsight][getstarted].</span><span class="sxs-lookup"><span data-stu-id="63cf7-108">For information about creating one, see [Get started using Linux-based Hadoop in HDInsight][getstarted].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="63cf7-109">Linux è l'unico sistema operativo usato in HDInsight versione 3.4 o successiva.</span><span class="sxs-lookup"><span data-stu-id="63cf7-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="63cf7-110">Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="63cf7-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* [<span data-ttu-id="63cf7-111">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="63cf7-111">Azure PowerShell</span></span>](/powershell/azure/overview)

## <span data-ttu-id="63cf7-112"><a name="recommendations"></a>Generare raccomandazioni con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="63cf7-112"><a name="recommendations"></a>Generate recommendations by using Azure PowerShell</span></span>

> [!WARNING]
> <span data-ttu-id="63cf7-113">Il processo in questa sezione funziona con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63cf7-113">The job in this section works by using Azure PowerShell.</span></span> <span data-ttu-id="63cf7-114">Molte delle classi offerte da Mahout attualmente non funzionano con Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="63cf7-114">Many of the classes provided with Mahout do not currently work with Azure PowerShell.</span></span> <span data-ttu-id="63cf7-115">Per l'elenco delle classi che non funzionano con Azure PowerShell, vedere la sezione [Risoluzione dei problemi](#troubleshooting).</span><span class="sxs-lookup"><span data-stu-id="63cf7-115">For a list of classes that do not work with Azure PowerShell, see the [Troubleshooting](#troubleshooting) section.</span></span>
>
> <span data-ttu-id="63cf7-116">Per un esempio su come usare SSH per connettersi a HDInsight ed eseguire esempi Mahout direttamente nel cluster, vedere [Generare raccomandazioni mediante Mahout e HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="63cf7-116">For an example of using SSH to connect to HDInsight and run Mahout examples directly on the cluster, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

<span data-ttu-id="63cf7-117">Una delle funzioni fornite da Mahout è un motore di raccomandazione.</span><span class="sxs-lookup"><span data-stu-id="63cf7-117">One of the functions that is provided by Mahout is a recommendation engine.</span></span> <span data-ttu-id="63cf7-118">Questo motore accetta i dati nei formati `userID`, `itemId` e `prefValue` (la preferenza degli utenti per l'elemento).</span><span class="sxs-lookup"><span data-stu-id="63cf7-118">This engine accepts data in the format of `userID`, `itemId`, and `prefValue` (the users preference for the item).</span></span> <span data-ttu-id="63cf7-119">Mahout usa i dati per determinare gli utenti con preferenze di elementi simili, che possono essere usate per le raccomandazioni.</span><span class="sxs-lookup"><span data-stu-id="63cf7-119">Mahout uses the data to determine users with like-item preferences, which can be used to make recommendations.</span></span>

<span data-ttu-id="63cf7-120">Nell'esempio seguente viene illustrata una procedura dettagliata semplificata del funzionamento del processo di raccomandazione:</span><span class="sxs-lookup"><span data-stu-id="63cf7-120">The following example is a simplified walk-through of how the recommendation process works:</span></span>

* <span data-ttu-id="63cf7-121">**Co-occorrenza**: a Joe, Alice e Bob piacciono *Guerre stellari*, *L'Impero colpisce ancora* e *Il ritorno dello Jedi*.</span><span class="sxs-lookup"><span data-stu-id="63cf7-121">**co-occurrence**: Joe, Alice, and Bob all liked *Star Wars*, *The Empire Strikes Back*, and *Return of the Jedi*.</span></span> <span data-ttu-id="63cf7-122">Mahout determina che agli utenti a cui piace uno di questi film piacciono anche gli altri due.</span><span class="sxs-lookup"><span data-stu-id="63cf7-122">Mahout determines that users who like any one of these movies also like the other two.</span></span>

* <span data-ttu-id="63cf7-123">**Co-occorrenza**: a Bob e Alice piacciono anche *La minaccia fantasma*, *L'attacco dei cloni* e *La vendetta dei Sith*.</span><span class="sxs-lookup"><span data-stu-id="63cf7-123">**co-occurrence**: Bob and Alice also liked *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span> <span data-ttu-id="63cf7-124">Mahout determina che agli utenti a cui piacciono i tre film precedenti piacciono anche questi tre.</span><span class="sxs-lookup"><span data-stu-id="63cf7-124">Mahout determines that users who liked the previous three movies also like these movies.</span></span>

* <span data-ttu-id="63cf7-125">**Raccomandazione per somiglianza**: poiché a Joe piacciono i primi tre film, Mahout cerca i film che piacciono ad altri utenti con preferenze simili ma che Joe non ha guardato o per i quali non ha ancora espresso una preferenza o una valutazione.</span><span class="sxs-lookup"><span data-stu-id="63cf7-125">**Similarity recommendation**: Because Joe liked the first three movies, Mahout looks at movies that others with similar preferences liked, but Joe has not watched (liked/rated).</span></span> <span data-ttu-id="63cf7-126">In questo caso, Mahout raccomanda *La minaccia fantasma*, *L'attacco dei cloni* e *La vendetta dei Sith*.</span><span class="sxs-lookup"><span data-stu-id="63cf7-126">In this case, Mahout recommends *The Phantom Menace*, *Attack of the Clones*, and *Revenge of the Sith*.</span></span>

### <a name="understanding-the-data"></a><span data-ttu-id="63cf7-127">Informazioni sui dati</span><span class="sxs-lookup"><span data-stu-id="63cf7-127">Understanding the data</span></span>

<span data-ttu-id="63cf7-128">[GroupLens Research][movielens] offre i dati di classificazione dei film in un formato compatibile con Mahout.</span><span class="sxs-lookup"><span data-stu-id="63cf7-128">[GroupLens Research][movielens] provides rating data for movies in a format that is compatible with Mahout.</span></span> <span data-ttu-id="63cf7-129">Questi dati sono disponibili nello spazio di archiviazione predefinito del cluster in `/HdiSamples//HdiSamples/MahoutMovieData`.</span><span class="sxs-lookup"><span data-stu-id="63cf7-129">This data is available on the default storage for your cluster at `/HdiSamples//HdiSamples/MahoutMovieData`.</span></span>

<span data-ttu-id="63cf7-130">Sono disponibili due file, `moviedb.txt` (informazioni sui film) e `user-ratings.txt`.</span><span class="sxs-lookup"><span data-stu-id="63cf7-130">There are two files, `moviedb.txt` (information about the movies) and `user-ratings.txt`.</span></span> <span data-ttu-id="63cf7-131">Il file `user-ratings.txt` viene usato durante l'analisi.</span><span class="sxs-lookup"><span data-stu-id="63cf7-131">The `user-ratings.txt` file is used during analysis.</span></span> <span data-ttu-id="63cf7-132">Il file `moviedb.txt` viene usato per generare testo descrittivo quando si visualizzano i risultati dell'analisi.</span><span class="sxs-lookup"><span data-stu-id="63cf7-132">The `moviedb.txt` file is used to provide user-friendly text when displaying the results of the analysis.</span></span>

<span data-ttu-id="63cf7-133">I dati contenuti in user-ratings.txt presentano una struttura `userID`, `movieID`, `userRating` e `timestamp` che indica come ogni utente ha classificato un film.</span><span class="sxs-lookup"><span data-stu-id="63cf7-133">The data contained in user-ratings.txt has a structure of `userID`, `movieID`, `userRating`, and `timestamp`, which tells us how highly each user rated a movie.</span></span> <span data-ttu-id="63cf7-134">Di seguito è riportato un esempio dei dati:</span><span class="sxs-lookup"><span data-stu-id="63cf7-134">Here is an example of the data:</span></span>

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-the-job"></a><span data-ttu-id="63cf7-135">Eseguire il processo</span><span class="sxs-lookup"><span data-stu-id="63cf7-135">Run the job</span></span>

<span data-ttu-id="63cf7-136">Usare lo script Windows PowerShell seguente per eseguire un processo che usi il motore di raccomandazione Mahout con i dati del film:</span><span class="sxs-lookup"><span data-stu-id="63cf7-136">Use the following Windows PowerShell script to run a job that uses the Mahout recommendation engine with the movie data:</span></span>

> [!NOTE]
> <span data-ttu-id="63cf7-137">Il file richiede le informazioni usate per connettersi al cluster HDInsight ed eseguire i processi.</span><span class="sxs-lookup"><span data-stu-id="63cf7-137">This file prompts you for information that is used to connect to your HDInsight cluster and run jobs.</span></span> <span data-ttu-id="63cf7-138">Potrebbero volerci diversi minuti per completare i processi e scaricare il file output.txt.</span><span class="sxs-lookup"><span data-stu-id="63cf7-138">It may take several minutes for the jobs to complete and download the output.txt file.</span></span>

<span data-ttu-id="63cf7-139">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]</span><span class="sxs-lookup"><span data-stu-id="63cf7-139">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]</span></span>

> [!NOTE]
> <span data-ttu-id="63cf7-140">I processi Mahout non rimuovono i dati temporanei creati durante l'elaborazione del processo.</span><span class="sxs-lookup"><span data-stu-id="63cf7-140">Mahout jobs do not remove temporary data that is created while processing the job.</span></span> <span data-ttu-id="63cf7-141">Nel processo di esempio è specificato il parametro `--tempDir` per isolare i file temporanei in una directory specifica.</span><span class="sxs-lookup"><span data-stu-id="63cf7-141">The `--tempDir` parameter is specified in the example job to isolate the temporary files into a specific directory.</span></span>

<span data-ttu-id="63cf7-142">Il processo Mahout non restituisce l'output in STDOUT,</span><span class="sxs-lookup"><span data-stu-id="63cf7-142">The Mahout job does not return the output to STDOUT.</span></span> <span data-ttu-id="63cf7-143">ma lo archivia nella directory di output specificata come **part-r-00000**.</span><span class="sxs-lookup"><span data-stu-id="63cf7-143">Instead, it stores it in the specified output directory as **part-r-00000**.</span></span> <span data-ttu-id="63cf7-144">Lo script scaricherà questo file in **output.txt** nella directory corrente nella workstation.</span><span class="sxs-lookup"><span data-stu-id="63cf7-144">The script downloads this file to **output.txt** in the current directory on your workstation.</span></span>

<span data-ttu-id="63cf7-145">Il testo seguente riporta un esempio del contenuto di questo file:</span><span class="sxs-lookup"><span data-stu-id="63cf7-145">The following text is an example of the content of this file:</span></span>

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

<span data-ttu-id="63cf7-146">La prima colonna rappresenta il valore `userID`.</span><span class="sxs-lookup"><span data-stu-id="63cf7-146">The first column is the `userID`.</span></span> <span data-ttu-id="63cf7-147">I valori racchiusi tra "[" e "]" sono `movieId`:`recommendationScore`.</span><span class="sxs-lookup"><span data-stu-id="63cf7-147">The values contained in '[' and ']' are `movieId`:`recommendationScore`.</span></span>

<span data-ttu-id="63cf7-148">Lo script scarica anche i file `moviedb.txt` e `user-ratings.txt` , necessari per formattare l'output in modo più leggibile.</span><span class="sxs-lookup"><span data-stu-id="63cf7-148">The script also downloads the `moviedb.txt` and `user-ratings.txt` files, which are needed to format the output to be more readable.</span></span>

### <a name="view-the-output"></a><span data-ttu-id="63cf7-149">Visualizzare l'output</span><span class="sxs-lookup"><span data-stu-id="63cf7-149">View the output</span></span>

<span data-ttu-id="63cf7-150">Anche se l'output generato risulta appropriato per l'uso in un'applicazione, non è facilmente leggibile.</span><span class="sxs-lookup"><span data-stu-id="63cf7-150">Although the generated output might be OK for use in an application, it's not user-friendly.</span></span> <span data-ttu-id="63cf7-151">Il `moviedb.txt` dal server può essere utilizzato per risolvere il `movieId` nel nome di un film.</span><span class="sxs-lookup"><span data-stu-id="63cf7-151">The `moviedb.txt` from the server can be used to resolve the `movieId` to a movie name.</span></span> <span data-ttu-id="63cf7-152">Usare lo script PowerShell seguente per vedere le raccomandazioni con i nomi dei film:</span><span class="sxs-lookup"><span data-stu-id="63cf7-152">Use the following PowerShell script to display recommendations with movie names:</span></span>

<span data-ttu-id="63cf7-153">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]</span><span class="sxs-lookup"><span data-stu-id="63cf7-153">[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]</span></span>

<span data-ttu-id="63cf7-154">Usare il comando seguente per visualizzare le indicazioni in un formato semplice:</span><span class="sxs-lookup"><span data-stu-id="63cf7-154">Use the following command to display the recommendations in a user-friendly format:</span></span> 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

<span data-ttu-id="63cf7-155">L'output è simile al testo seguente:</span><span class="sxs-lookup"><span data-stu-id="63cf7-155">The output is similar to the following text:</span></span>

    Reading movies descriptions
    Reading rated movies
    Reading recommendations
    Rated movies
    ---------------------------
    Movie                                    Rating
    -----                                    ------
    Devil's Own, The (1997)                  1
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
    Wings of the Dove, The (1997)            4.6666665
    People vs. Larry Flynt, The (1996)       4.834559
    Everyone Says I Love You (1996)          4.707071
    Secrets & Lies (1996)                    4.818182
    That Thing You Do! (1996)                4.75
    Grosse Pointe Blank (1997)               4.8235292
    Donnie Brasco (1997)                     4.6792455
    Lone Star (1996)                         4.7099237

## <span data-ttu-id="63cf7-156"><a name="troubleshooting"></a>Risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="63cf7-156"><a name="troubleshooting"></a>Troubleshooting</span></span>

### <a name="cannot-overwrite-files"></a><span data-ttu-id="63cf7-157">Impossibile sovrascrivere i file</span><span class="sxs-lookup"><span data-stu-id="63cf7-157">Cannot overwrite files</span></span>

<span data-ttu-id="63cf7-158">I processi Mahout non eliminano i file temporanei creati durante l'elaborazione.</span><span class="sxs-lookup"><span data-stu-id="63cf7-158">Mahout jobs do not clean up temporary files that were created during processing.</span></span> <span data-ttu-id="63cf7-159">Inoltre, i processi non sovrascrivono un file di output esistente.</span><span class="sxs-lookup"><span data-stu-id="63cf7-159">In addition, the jobs do not overwrite existing output file.</span></span>

<span data-ttu-id="63cf7-160">Per evitare errori durante l'esecuzione dei processi Mahout, eliminare i file temporanei e di output da un'esecuzione all'altra.</span><span class="sxs-lookup"><span data-stu-id="63cf7-160">To avoid errors when running Mahout jobs, delete temporary and output files between runs.</span></span> <span data-ttu-id="63cf7-161">Utilizzare il seguente script PowerShell per rimuovere i file creati dagli script precedenti in questo documento:</span><span class="sxs-lookup"><span data-stu-id="63cf7-161">To remove the files created by the earlier scripts in this document, use the following PowerShell script:</span></span>

```powershell
# Login to your Azure subscription
# Is there an active Azure subscription?
$sub = Get-AzureRmSubscription -ErrorAction SilentlyContinue
if(-not($sub))
{
    Add-AzureRmAccount
}

# Get cluster info
$clusterName = Read-Host -Prompt "Enter the HDInsight cluster name"
$creds=Get-Credential -Message "Enter the login for the cluster"

#Get the cluster info so we can get the resource group, storage, etc.
$clusterInfo = Get-AzureRmHDInsightCluster -ClusterName $clusterName
$resourceGroup = $clusterInfo.ResourceGroup
$storageAccountName = $clusterInfo.DefaultStorageAccount.split('.')[0]
$container = $clusterInfo.DefaultStorageContainer
$storageAccountKey = (Get-AzureRmStorageAccountKey `
    -Name $storageAccountName `
-ResourceGroupName $resourceGroup)[0].Value

#Create a storage context and upload the file
$context = New-AzureStorageContext `
    -StorageAccountName $storageAccountName `
    -StorageAccountKey $storageAccountKey

#Azure PowerShell can't delete blobs using wildcard,
#so have to get a list and delete one at a time
# Start with the output
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/out"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
# Next the temp files
$blobs = Get-AzureStorageBlob -Container $container -Context $context -Prefix "example/temp"
foreach($blob in $blobs)
{
    Remove-AzureStorageBlob -Blob $blob.Name -Container $container -context $context
}
```

### <span data-ttu-id="63cf7-162"><a name="nopowershell"></a>Classi che non funzionano con Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="63cf7-162"><a name="nopowershell"></a>Classes that do not work with Azure PowerShell</span></span>

<span data-ttu-id="63cf7-163">I processi Mahout che usano le classi seguenti restituiscono una serie di messaggi di errore quando vengono usati da Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="63cf7-163">Mahout jobs that use the following classes return various error messages when used from Windows PowerShell:</span></span>

* <span data-ttu-id="63cf7-164">org.apache.mahout.utils.clustering.ClusterDumper</span><span class="sxs-lookup"><span data-stu-id="63cf7-164">org.apache.mahout.utils.clustering.ClusterDumper</span></span>
* <span data-ttu-id="63cf7-165">org.apache.mahout.utils.SequenceFileDumper</span><span class="sxs-lookup"><span data-stu-id="63cf7-165">org.apache.mahout.utils.SequenceFileDumper</span></span>
* <span data-ttu-id="63cf7-166">org.apache.mahout.utils.vectors.lucene.Driver</span><span class="sxs-lookup"><span data-stu-id="63cf7-166">org.apache.mahout.utils.vectors.lucene.Driver</span></span>
* <span data-ttu-id="63cf7-167">org.apache.mahout.utils.vectors.arff.Driver</span><span class="sxs-lookup"><span data-stu-id="63cf7-167">org.apache.mahout.utils.vectors.arff.Driver</span></span>
* <span data-ttu-id="63cf7-168">org.apache.mahout.text.WikipediaToSequenceFile</span><span class="sxs-lookup"><span data-stu-id="63cf7-168">org.apache.mahout.text.WikipediaToSequenceFile</span></span>
* <span data-ttu-id="63cf7-169">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span><span class="sxs-lookup"><span data-stu-id="63cf7-169">org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles</span></span>
* <span data-ttu-id="63cf7-170">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span><span class="sxs-lookup"><span data-stu-id="63cf7-170">org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer</span></span>
* <span data-ttu-id="63cf7-171">org.apache.mahout.classifier.sgd.TrainLogistic</span><span class="sxs-lookup"><span data-stu-id="63cf7-171">org.apache.mahout.classifier.sgd.TrainLogistic</span></span>
* <span data-ttu-id="63cf7-172">org.apache.mahout.classifier.sgd.RunLogistic</span><span class="sxs-lookup"><span data-stu-id="63cf7-172">org.apache.mahout.classifier.sgd.RunLogistic</span></span>
* <span data-ttu-id="63cf7-173">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="63cf7-173">org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic</span></span>
* <span data-ttu-id="63cf7-174">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="63cf7-174">org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic</span></span>
* <span data-ttu-id="63cf7-175">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span><span class="sxs-lookup"><span data-stu-id="63cf7-175">org.apache.mahout.classifier.sgd.RunAdaptiveLogistic</span></span>
* <span data-ttu-id="63cf7-176">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span><span class="sxs-lookup"><span data-stu-id="63cf7-176">org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer</span></span>
* <span data-ttu-id="63cf7-177">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span><span class="sxs-lookup"><span data-stu-id="63cf7-177">org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator</span></span>
* <span data-ttu-id="63cf7-178">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span><span class="sxs-lookup"><span data-stu-id="63cf7-178">org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator</span></span>
* <span data-ttu-id="63cf7-179">org.apache.mahout.classifier.df.tools.Describe</span><span class="sxs-lookup"><span data-stu-id="63cf7-179">org.apache.mahout.classifier.df.tools.Describe</span></span>

<span data-ttu-id="63cf7-180">Per eseguire i processi che usano queste classi, connettersi al cluster HDInsight usando SSH ed eseguire i processi dalla riga di comando.</span><span class="sxs-lookup"><span data-stu-id="63cf7-180">To run jobs that use these classes, connect to the HDInsight cluster using SSH and run the jobs from the command line.</span></span> <span data-ttu-id="63cf7-181">Per un esempio su come usare SSH per eseguire processi Mahout, vedere [Generare raccomandazioni mediante Mahout e HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span><span class="sxs-lookup"><span data-stu-id="63cf7-181">For an example of using SSH to run Mahout jobs, see [Generate movie recommendations using Mahout and HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="63cf7-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="63cf7-182">Next steps</span></span>

<span data-ttu-id="63cf7-183">A questo punto, dopo aver appreso come usare Mahout, trovare altri modi per usare i dati in HDInsight:</span><span class="sxs-lookup"><span data-stu-id="63cf7-183">Now that you have learned how to use Mahout, discover other ways of working with data on HDInsight:</span></span>

* [<span data-ttu-id="63cf7-184">Hive con HDInsight</span><span class="sxs-lookup"><span data-stu-id="63cf7-184">Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="63cf7-185">Pig con HDInsight</span><span class="sxs-lookup"><span data-stu-id="63cf7-185">Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="63cf7-186">MapReduce con HDInsight</span><span class="sxs-lookup"><span data-stu-id="63cf7-186">MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

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
