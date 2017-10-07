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
# <a name="generate-movie-recommendations-by-using-apache-mahout-with-hadoop-in-hdinsight-powershell"></a>Generare raccomandazioni di film mediante Apache Mahout con Hadoop in HDInsight (PowerShell)

[!INCLUDE [mahout-selector](../../includes/hdinsight-selector-mahout.md)]

Informazioni su come hello toouse [Mahout Apache](http://mahout.apache.org) libreria learning macchina con le raccomandazioni di Azure HDInsight toogenerate film. esempio Hello in questo documento usa Azure PowerShell toorun Mahout processi.

## <a name="prerequisites"></a>Prerequisiti

* Un cluster HDInsight basato su Linux. Per informazioni su come crearne uno, vedere [Introduzione all'uso di Hadoop basato su Linux in HDInsight][getstarted].

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Azure PowerShell](/powershell/azure/overview)

## <a name="recommendations"></a>Generare raccomandazioni con Azure PowerShell

> [!WARNING]
> il processo di Hello in questa sezione funziona tramite Azure PowerShell. Molte delle classi di hello fornite con Mahout attualmente non si collabora con Azure PowerShell. Per un elenco di classi che non funzionano con Azure PowerShell, vedere hello [Troubleshooting](#troubleshooting) sezione.
>
> Per un esempio di utilizzo di SSH tooconnect tooHDInsight ed esempi di Mahout esecuzione direttamente nel cluster di hello, vedere [generare le indicazioni di film utilizzando Mahout e HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

Una delle funzioni hello fornito da Mahout è un motore di raccomandazione. Questo motore accetta i dati in formato hello `userID`, `itemId`, e `prefValue` (hello preferenza agli utenti per l'elemento hello). Mahout Usa gli utenti di hello dati toodetermine con preferenze simili-item, che possono essere utilizzato toomake indicazioni.

Hello seguito è riportata una panoramica di come funziona il processo di raccomandazione hello semplificata:

* **CO-occorrenza**: Joe, Alice e Bob tutti stato apprezzato *stella attraverso*, *hello Empire colpisce nuovamente*, e *restituzione di hello Jedi*. Mahout determina che gli utenti come uno di questi film anche hello altri due.

* **CO-occorrenza**: Bob e Alice anche ritengono *hello Phantom alieni*, *attacco dei cloni di hello*, e *ritorsioni di hello Sith*. Mahout determina che gli utenti che ritengono tre filmati precedente hello anche come questi film.

* **Indicazione di somiglianza**: Joe perché ritengono hello primi tre film, Mahout esamina filmati che altri utenti con preferenze simili ritengono, ma Joe ha non controllata (ritengono/classificazione). In questo caso, si consiglia Mahout *hello Phantom alieni*, *attacco dei cloni di hello*, e *ritorsioni di hello Sith*.

### <a name="understanding-hello-data"></a>Informazioni sui dati hello

[GroupLens Research][movielens] offre i dati di classificazione dei film in un formato compatibile con Mahout. Questi dati sono disponibili in spazio di archiviazione di hello predefinito per il cluster in `/HdiSamples//HdiSamples/MahoutMovieData`.

Sono disponibili due file, `moviedb.txt` (informazioni su filmati hello) e `user-ratings.txt`. Hello `user-ratings.txt` file viene utilizzato durante l'analisi. Hello `moviedb.txt` file è testo descrittivo tooprovide utilizzato durante la visualizzazione dei risultati dell'analisi hello hello.

dati contenuti in utente ratings.txt Hello presenta una struttura di `userID`, `movieID`, `userRating`, e `timestamp`, che indica come elevata ogni utente classificato un filmato. Di seguito è riportato un esempio di dati hello:

    196    242    3    881250949
    186    302    3    891717742
    22    377    1    878887116
    244    51    2    880606923
    166    346    1    886397596

### <a name="run-hello-job"></a>Eseguire il processo di hello

Utilizzare hello seguente script di Windows PowerShell toorun un processo che utilizza il motore di raccomandazione Mahout hello con dati film hello:

> [!NOTE]
> Questo file verranno richieste informazioni sul cluster di HDInsight tooyour tooconnect utilizzati e i processi di esecuzione. Può richiedere alcuni minuti per toocomplete processi hello e scaricare i file di output. txt hello.

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=5-98)]

> [!NOTE]
> I processi di mahout non rimuovere i dati temporanei creati durante l'elaborazione di processi di hello. Hello `--tempDir` viene specificato in file temporanei di hello esempio processo tooisolate hello in una directory specifica.

Hello Mahout job non restituisce tooSTDOUT output hello. Al contrario, viene memorizzato nella directory di output specificata hello come **parte-r-00000**. script Hello Scarica il file troppo**txt** nella directory corrente di hello nella workstation.

Hello testo riportato di seguito è riportato un esempio del contenuto di hello di questo file:

    1    [234:5.0,347:5.0,237:5.0,47:5.0,282:5.0,275:5.0,88:5.0,515:5.0,514:5.0,121:5.0]
    2    [282:5.0,210:5.0,237:5.0,234:5.0,347:5.0,121:5.0,258:5.0,515:5.0,462:5.0,79:5.0]
    3    [284:5.0,285:4.828125,508:4.7543354,845:4.75,319:4.705128,124:4.7045455,150:4.6938777,311:4.6769233,248:4.65625,272:4.649266]
    4    [690:5.0,12:5.0,234:5.0,275:5.0,121:5.0,255:5.0,237:5.0,895:5.0,282:5.0,117:5.0]

prima colonna Hello è hello `userID`. Hello valori contenuti in ' [' e ']' sono `movieId`:`recommendationScore`.

script Hello scarica anche hello `moviedb.txt` e `user-ratings.txt` file, che sono necessari tooformat hello output toobe più leggibile.

### <a name="view-hello-output"></a>Visualizzazione output di hello

Anche se hello output generato potrebbe essere OK per l'utilizzo in un'applicazione, non è semplice. Hello `moviedb.txt` da hello server può essere utilizzato tooresolve hello `movieId` nome film tooa. Utilizzare hello indicazioni toodisplay allo script di PowerShell con nomi di film seguenti:

[!code-powershell[main](../../powershell_scripts/hdinsight/mahout/use-mahout.ps1?range=106-180)]

Utilizzare hello indicazioni hello toodisplay di comando in un formato descrittivo seguente: 

```powershell
.\show-recommendation.ps1 -userId 4 -userDataFile .\user-ratings.txt -movieFile .\moviedb.txt -recommendationFile .\output.txt
```

Hello l'output è simile toohello seguente testo:

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

## <a name="troubleshooting"></a>Risoluzione dei problemi

### <a name="cannot-overwrite-files"></a>Impossibile sovrascrivere i file

I processi Mahout non eliminano i file temporanei creati durante l'elaborazione. Inoltre, i processi di hello non sovrascrivono i file di output esistente.

tooavoid errori quando si eseguono processi Mahout, eliminare i file temporanei e di output tra le esecuzioni. file hello tooremove creati da hello script precedente in questo documento, usare hello lo script di PowerShell seguente:

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

### <a name="nopowershell"></a>Classi che non funzionano con Azure PowerShell

I processi di mahout che utilizzano le seguenti classi hello restituiscono vari messaggi di errore quando viene utilizzata da Windows PowerShell:

* org.apache.mahout.utils.clustering.ClusterDumper
* org.apache.mahout.utils.SequenceFileDumper
* org.apache.mahout.utils.vectors.lucene.Driver
* org.apache.mahout.utils.vectors.arff.Driver
* org.apache.mahout.text.WikipediaToSequenceFile
* org.apache.mahout.clustering.streaming.tools.ResplitSequenceFiles
* org.apache.mahout.clustering.streaming.tools.ClusterQualitySummarizer
* org.apache.mahout.classifier.sgd.TrainLogistic
* org.apache.mahout.classifier.sgd.RunLogistic
* org.apache.mahout.classifier.sgd.TrainAdaptiveLogistic
* org.apache.mahout.classifier.sgd.ValidateAdaptiveLogistic
* org.apache.mahout.classifier.sgd.RunAdaptiveLogistic
* org.apache.mahout.classifier.sequencelearning.hmm.BaumWelchTrainer
* org.apache.mahout.classifier.sequencelearning.hmm.ViterbiEvaluator
* org.apache.mahout.classifier.sequencelearning.hmm.RandomSequenceGenerator
* org.apache.mahout.classifier.df.tools.Describe

i processi di toorun che utilizzano queste classi, connettere il cluster di HDInsight toohello tramite SSH ed eseguire i processi di hello dalla riga di comando hello. Per un esempio di utilizzo di SSH toorun Mahout processi, vedere [generare le indicazioni di film utilizzando Mahout e HDInsight (SSH)](hdinsight-hadoop-mahout-linux-mac.md).

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come toouse Mahout, individuare altri modi di utilizzo dei dati in HDInsight:

* [Hive con HDInsight](hdinsight-use-hive.md)
* [Pig con HDInsight](hdinsight-use-pig.md)
* [MapReduce con HDInsight](hdinsight-use-mapreduce.md)

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
