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
# <a name="use-azure-powershell-toorun-pig-jobs-with-hdinsight"></a>Utilizzare i processi di Azure PowerShell toorun Pig con HDInsight

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Questo documento viene fornito un esempio dell'utilizzo di Azure PowerShell toosubmit Pig processi tooa Hadoop nel cluster HDInsight. Pig consente i processi MapReduce toowrite tramite un linguaggio (alfabeto latino Pig) che modella le trasformazioni dei dati, anziché eseguire il mapping e ridurre le funzioni.

> [!NOTE]
> Questo documento non fornisce una descrizione dettagliata delle operazioni eseguite istruzioni Pig latino hello utilizzate negli esempi di hello. Per informazioni su hello Pig latini utilizzato in questo esempio, vedere [usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md).

## <a id="prereq"></a>Prerequisiti

* **Un cluster Azure HDInsight**

  > [!IMPORTANT]
  > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Workstation con Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a id="powershell"></a>Eseguire processi Pig mediante PowerShell

Azure PowerShell fornisce *cmdlet* che consentono di tooremotely eseguire processi di Pig in HDInsight. Internamente, PowerShell Usa le chiamate REST troppo[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) in esecuzione nel cluster HDInsight hello.

i cmdlet seguenti Hello vengono utilizzati durante l'esecuzione di processi Pig in un cluster HDInsight remoto:

* **Account di accesso AzureRmAccount**: esegue l'autenticazione di Azure PowerShell tooyour sottoscrizione di Azure
* **Nuovo AzureRmHDInsightPigJobDefinition**: crea un *definizione del processo* utilizzando hello specificato Pig latino istruzioni
* **Inizio AzureRmHDInsightJob**: invia hello processo definizione tooHDInsight, avvia il processo di hello e restituisce un *processo* oggetto che può essere utilizzato toocheck hello stato del processo di hello
* **Attesa AzureRmHDInsightJob**: utilizza hello oggetto toocheck hello stato del processo del processo di hello. È in attesa fino a quando non è stato completato il processo di hello o è stato superato il tempo di attesa hello.
* **Get-AzureRmHDInsightJobOutput**: utilizzato l'output di hello tooretrieve del processo di hello

Hello passaggi seguenti viene illustrato come toouse questi toorun cmdlet un processo il cluster HDInsight.

1. Utilizzando un editor, salvare hello seguente di codice come **pigjob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-pig/use-pig.ps1?range=5-51)]

1. Aprire un nuovo prompt dei comandi di Windows PowerShell. Modificare il percorso toohello directory di hello **pigjob.ps1** file, quindi utilizzare lo script di comando toorun hello seguente hello:

        .\pigjob.ps1

    Si è richiesta toolog in tooyour sottoscrizione di Azure. Quindi, viene richiesto per nome dell'account HTTPs/Admin hello e una password per il cluster HDInsight hello.

2. Al termine del processo di hello, deve restituire toohello di informazioni simili seguente testo:

        Start hello Pig job ...
        Wait for hello Pig job toocomplete ...
        Display hello standard output ...
        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="troubleshooting"></a>Risoluzione dei problemi

Se viene restituita alcuna informazione quando hello processo viene completato, potrebbe essersi verificato un errore durante l'elaborazione. informazioni sull'errore tooview per questo processo, aggiungere hello successivo comando toohello hello **pigjob.ps1** file, salvarlo e quindi eseguirla nuovamente.

    # Print hello output of hello Pig job.
    Write-Host "Display hello standard error output ..." -ForegroundColor Green
    Get-AzureRmHDInsightJobOutput `
            -Clustername $clusterName `
            -JobId $pigJob.JobId `
            -HttpCredential $creds `
            -DisplayOutputType StandardError

Vengono restituite le informazioni di hello che è stato scritto tooSTDERR nel server di hello quando è stato eseguito il processo di hello e può essere utile determinare perché il processo di hello non è riuscito.

## <a id="summary"></a>Riepilogo
Come si può notare, Azure PowerShell fornisce un modo semplice di toorun processi Pig in un cluster HDInsight, lo stato del processo di monitoraggio hello e output di hello recuperare.

## <a id="nextsteps"></a>Passaggi successivi
Per informazioni generali su Pig in HDInsight:

* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)
