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
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-powershell"></a>Esecuzione di processi MapReduce con Hadoop in HDInsight mediante PowerShell

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Questo documento viene fornito un esempio dell'utilizzo di Azure PowerShell toorun un processo MapReduce in un Hadoop nel cluster HDInsight.

## <a id="prereq"></a>Prerequisiti

* **Un cluster Azure HDInsight (Hadoop in HDInsight)**

  > [!IMPORTANT]
  > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Workstation con Azure PowerShell**.

## <a id="powershell"></a>Eseguire un processo MapReduce con Azure PowerShell

Azure PowerShell fornisce *cmdlet* che consentono di tooremotely eseguire i processi MapReduce in HDInsight. Internamente, questa operazione viene eseguita tramite le chiamate REST troppo[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) (precedentemente denominato Templeton) in esecuzione su hello cluster HDInsight.

i cmdlet seguenti Hello vengono utilizzati durante l'esecuzione di processi MapReduce in un cluster HDInsight remoto.

* **Account di accesso AzureRmAccount**: esegue l'autenticazione di Azure PowerShell tooyour sottoscrizione di Azure.

* **Nuovo AzureRmHDInsightMapReduceJobDefinition**: crea un nuovo *definizione del processo* utilizzando hello specificato le informazioni di MapReduce.

* **Inizio AzureRmHDInsightJob**: invia hello processo definizione tooHDInsight, avvia il processo di hello e restituisce un *processo* oggetto che può essere utilizzato toocheck hello stato del processo di hello.

* **Attesa AzureRmHDInsightJob**: utilizza hello oggetto toocheck hello stato del processo del processo di hello. È in attesa fino a quando non viene completato il processo di hello o viene superato il tempo di attesa hello.

* **Get-AzureRmHDInsightJobOutput**: utilizzato l'output di hello tooretrieve del processo di hello.

Hello passaggi seguenti viene illustrato come toouse questi toorun cmdlet un processo del cluster HDInsight.

1. Utilizzando un editor, salvare hello seguente di codice come **mapreducejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-mapreduce/use-mapreduce.ps1?range=5-69)]

2. Quindi, aprire un nuovo prompt dei comandi di **Azure PowerShell** . Modificare il percorso toohello directory di hello **mapreducejob.ps1** file, quindi utilizzare lo script di comando toorun hello seguente hello:

        .\mapreducejob.ps1

    Quando si esegue uno script di hello, richiesto per il nome di hello del cluster HDInsight hello e nome dell'account HTTPS/Admin hello e la password per il cluster hello. Potrebbe essere richiesta tooauthenticate tooyour sottoscrizione di Azure.

3. Al termine del processo di hello, viene visualizzato toohello simili di output il testo seguente:

        Cluster         : CLUSTERNAME
        ExitCode        : 0
        Name            : wordcount
        PercentComplete : map 100% reduce 100%
        Query           :
        State           : Completed
        StatusDirectory : f1ed2028-afe8-402f-a24b-13cc17858097
        SubmissionTime  : 12/5/2014 8:34:09 PM
        JobId           : job_1415949758166_0071

    Questo output indica che il processo di hello è stata completata correttamente.

    > [!NOTE]
    > Se hello **ExitCode** è un valore diverso da 0, vedere [risoluzione dei problemi](#troubleshooting).

    In questo esempio viene inoltre archiviato hello scaricato i file tooan **txt** file nella directory hello eseguiti script hello da.

### <a name="view-output"></a>Visualizzare l’output

Aprire hello **txt** file in un hello toosee editor di testo parole e conta prodotti dal processo hello.

> [!NOTE]
> file di output di Hello di un processo MapReduce non sono modificabili. Pertanto, se si esegue nuovamente questo esempio, è necessario nome hello toochange hello del file di output.

## <a id="troubleshooting"></a>Risoluzione dei problemi

Se viene restituita alcuna informazione quando hello processo viene completato, potrebbe essersi verificato un errore durante l'elaborazione. informazioni sull'errore tooview per questo processo, aggiungere hello successivo comando toohello hello **mapreducejob.ps1** file, salvarlo e quindi eseguirla nuovamente.

```powershell
# Print hello output of hello WordCount job.
Write-Host "Display hello standard output ..." -ForegroundColor Green
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $wordCountJob.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Questo cmdlet restituisce le informazioni di hello che è stato scritto tooSTDERR nel server di hello quando è stato eseguito il processo di hello e può essere utile determinare perché il processo di hello non è riuscito.

## <a id="summary"></a>Riepilogo

Come si può notare, Azure PowerShell fornisce toorun un modo semplice i processi MapReduce in un cluster HDInsight, lo stato del processo di monitoraggio hello e output di hello recuperare.

## <a id="nextsteps"></a>Passaggi successivi

Per informazioni generali sui processi MapReduce in HDInsight:

* [Usare MapReduce in HDInsight Hadoop](hdinsight-use-mapreduce.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)
