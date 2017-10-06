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
# <a name="run-hive-queries-using-powershell"></a>Esecuzione di query Hive usando PowerShell
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Questo documento viene fornito un esempio dell'utilizzo di Azure PowerShell in query hello il gruppo di risorse di Azure in modalità toorun Hive in un Hadoop nel cluster HDInsight.

> [!NOTE]
> Questo documento non fornisce una descrizione dettagliata delle operazioni eseguite le istruzioni HiveQL hello utilizzate negli esempi di hello. Per informazioni su hello HiveQL utilizzato in questo esempio, vedere [utilizzare Hive con Hadoop in HDInsight](hdinsight-use-hive.md).

**Prerequisiti**

* **Un cluster Azure HDInsight**: non è importante se il cluster di hello è Windows o basata su Linux.

  > [!IMPORTANT]
  > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* **Workstation con Azure PowerShell**.

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]

## <a name="run-hive-queries-using-azure-powershell"></a>Eseguire query Hive usando Azure PowerShell

Azure PowerShell fornisce *cmdlet* che consentono di tooremotely eseguire query di Hive in HDInsight. Internamente, i cmdlet di hello supportano chiamate REST troppo[WebHCat](https://cwiki.apache.org/confluence/display/Hive/WebHCat) nel cluster HDInsight hello.

i cmdlet seguenti Hello vengono utilizzati durante l'esecuzione di query Hive in un cluster HDInsight remoto:

* **AzureRmAccount aggiungere**: esegue l'autenticazione di Azure PowerShell tooyour sottoscrizione di Azure
* **Nuovo AzureRmHDInsightHiveJobDefinition**: crea un *definizione del processo* utilizzando hello specificato istruzioni HiveQL
* **Inizio AzureRmHDInsightJob**: invia hello processo definizione tooHDInsight, avvia il processo di hello e restituisce un *processo* oggetto che può essere utilizzato toocheck hello stato del processo di hello
* **Attesa AzureRmHDInsightJob**: utilizza hello oggetto toocheck hello stato del processo del processo di hello. È in attesa fino a quando non viene completato il processo di hello o viene superato il tempo di attesa hello.
* **Get-AzureRmHDInsightJobOutput**: utilizzato l'output di hello tooretrieve del processo di hello
* **Invoke-AzureRmHDInsightHiveJob**: utilizzare le istruzioni HiveQL toorun. Questa query di hello cmdlet blocchi viene completata, quindi restituisce i risultati di hello
* **Utilizzare AzureRmHDInsightCluster**: set hello toouse cluster corrente per hello **Invoke AzureRmHDInsightHiveJob** comando

Hello passaggi seguenti viene illustrato come toouse questi toorun cmdlet un processo del cluster HDInsight:

1. Utilizzando un editor, salvare hello seguente di codice come **hivejob.ps1**.

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=5-42)]

2. Quindi, aprire un nuovo prompt dei comandi di **Azure PowerShell** . Modificare il percorso toohello directory di hello **hivejob.ps1** file, quindi utilizzare lo script di comando toorun hello seguente hello:

        .\hivejob.ps1

    Quando si esegue lo script hello, verrà richiesta tooenter hello cluster nome e hello HTTPS/credenziali dell'account amministratore per il cluster hello. Potrebbe essere richiesta toolog in tooyour sottoscrizione di Azure.

3. Al termine del processo di hello, verrà restituito toohello di informazioni simili seguente testo:

        Display hello standard output...
        2012-02-03      18:35:34        SampleClass0    [ERROR] incorrect       id
        2012-02-03      18:55:54        SampleClass1    [ERROR] incorrect       id
        2012-02-03      19:25:27        SampleClass4    [ERROR] incorrect       id

4. Come accennato in precedenza, **Invoke-Hive** possono essere utilizzati toorun una query e attesa di risposta hello. Utilizzare i seguenti script toosee funzionamento tra Invoke-Hive hello:

    [!code-powershell[main](../../powershell_scripts/hdinsight/use-hive/use-hive.ps1?range=50-71)]

    output di Hello è simile hello seguente testo:

        2012-02-03    18:35:34    SampleClass0    [ERROR]    incorrect    id
        2012-02-03    18:55:54    SampleClass1    [ERROR]    incorrect    id
        2012-02-03    19:25:27    SampleClass4    [ERROR]    incorrect    id

   > [!NOTE]
   > Per le query HiveQL più lungo, è possibile utilizzare hello Azure PowerShell **stringhe di tipo Here** cmdlet o HiveQL i file di script. Hello seguente mostra come hello toouse **Invoke-Hive** cmdlet toorun un file di script HiveQL. file di script deve essere HiveQL Hello caricato toowasb: / /.
   >
   > `Invoke-AzureRmHDInsightHiveJob -File "wasb://<ContainerName>@<StorageAccountName>/<Path>/query.hql"`
   >
   > Per altre informazioni su **Here-Strings**, vedere <a href="http://technet.microsoft.com/library/ee692792.aspx" target="_blank">Using Windows PowerShell "Here-Strings"</a> (Uso di Here-Strings di Windows PowerShell).

## <a name="troubleshooting"></a>Risoluzione dei problemi

Se viene restituita alcuna informazione quando hello processo viene completato, potrebbe essersi verificato un errore durante l'elaborazione. informazioni sull'errore tooview per questo processo, aggiungere hello successivo alla fine di hello toohello **hivejob.ps1** file, salvarlo e quindi eseguirla nuovamente.

```powershell
# Print hello output of hello Hive job.
Get-AzureRmHDInsightJobOutput `
        -Clustername $clusterName `
        -JobId $job.JobId `
        -HttpCredential $creds `
        -DisplayOutputType StandardError
```

Questo cmdlet restituisce informazioni hello scritte tooSTDERR nel server di hello quando è stato eseguito il processo di hello.

## <a name="summary"></a>Riepilogo

Come si può notare, Azure PowerShell offre un modo semplice di toorun query Hive in un cluster HDInsight, hello di monitoraggio dello stato del processo e recuperare l'output di hello.

## <a name="next-steps"></a>Passaggi successivi

Per informazioni generali su Hive in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)
