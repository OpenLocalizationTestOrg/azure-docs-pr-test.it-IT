---
title: aaaUse Hadoop Pig in HDInsight | Documenti Microsoft
description: Informazioni su come toouse Pig con Hadoop in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a>Usare Pig con Hadoop in HDInsight

Informazioni su come toouse [Pig Apache](http://pig.apache.org/) con HDInsight...

Pig è una piattaforma che consente la creazione di programmi per Hadoop usando un linguaggio procedurale denominato *Pig Latin*. Pig è un tooJava alternativo per la creazione di *MapReduce* soluzioni e è incluso in Azure HDInsight. Utilizzare hello hello toodiscover tabella vari modi Pig può essere utilizzato con HDInsight seguenti:

| **Usare questo** se si desidera... | ...una shell **interattiva** | ...elaborazione**batch** | ...con questo **sistema operativo cluster** | ...da questo **sistema operativo client** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X o Windows |
| [API REST](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux o Windows |Linux, Unix, Mac OS X o Windows |
| [.NET SDK per Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux o Windows |Windows (per ora) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux o Windows |Windows |
| [Desktop remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 e 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="why"></a>Perché usare Pig

Una delle sfide hello l'elaborazione dei dati tramite il Framework MapReduce in Hadoop implementa la logica di elaborazione usando solo una mappa e una funzione di riduzione. Per un'elaborazione complessa, è spesso hanno toobreak l'elaborazione in più operazioni MapReduce che vengono concatenati risultato hello desiderato tooachieve.

Pig consente l'elaborazione come una serie di trasformazioni che hello flussi di dati tramite l'output di hello desiderato tooproduce toodefine.

Pig latino Hello consente si toodescribe hello flusso di dati da un input non elaborato, tramite una o più trasformazioni, tooproduce output di hello desiderato. I programmi in Pig Latin seguono questo modello generale:

* **Carico**: leggere dati toobe modificato dal file system di hello

* **Trasformare**: modificare dati hello

* **Eseguire il dump o archiviare**: schermata toohello dati di Output o se archiviarlo per l'elaborazione

### <a name="user-defined-functions"></a>Funzioni definite dall'utente

Latino Pig supporta anche le funzioni definite dall'utente (UDF), che consente di tooinvoke i componenti esterni che implementano la logica di difficile toomodel in latino Pig.

Per altre informazioni su Pig Latin, vedere il [manuale di riferimento di Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) e il [manuale di riferimento di Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).

Per un esempio di utilizzo di funzioni definite dall'utente con Pig, vedere hello seguenti documenti:

* [Usare DataFu con Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu è una raccolta di utili funzioni definite dall'utente gestite mediante Apache
* [Usare Python con Pig e Hive in HDInsight](hdinsight-python.md)
* [Usare C# con Hive e Pig in HDInsight](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <a id="data"></a>Dati di esempio

HDInsight fornisce vari set di dati esempio, che vengono archiviati in hello `/example/data` e `/HdiSamples` directory. Queste directory sono in spazio di archiviazione di hello predefinito per il cluster. esempio Pig Hello in questo documento usa hello *log4j* file `/example/data/sample.log`.

Ogni log nel file hello è costituito da una riga di campi che contiene un `[LOG LEVEL]` campo tooshow hello hello tipo e il livello di gravità, ad esempio:

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

Nell'esempio precedente hello, il livello di registrazione di hello è errore.

> [!NOTE]
> È anche possibile generare un file log4j utilizzando hello [Log4j Apache](http://en.wikipedia.org/wiki/Log4j) strumento di registrazione e quindi caricare il blob tooyour file. Vedere [tooHDInsight caricare dati](hdinsight-upload-data.md) per le istruzioni. Per altre informazioni sul modo in cui HDInsight usa l'archiviazione BLOB di Azure, vedere [Usare l'archiviazione BLOB di Azure con HDInsight](hdinsight-hadoop-use-blob-storage.md).

## <a id="job"></a>Processo di esempio

il processo Pig latino seguente Hello carica hello `sample.log` file dall'archiviazione di hello predefinito per il cluster HDInsight. Quindi esegue una serie di trasformazioni che produce un numero di procedura molte volte ogni dati di input di livello hello durante l'esecuzione di log. i risultati di Hello vengono scritti tooSTDOUT.

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

Hello immagine seguente mostra un riepilogo delle quali ogni trasformazione toohello dati.

![Rappresentazione grafica di trasformazioni hello][image-hdi-pig-data-transformation]

## <a id="run"></a>Esegui processo Pig latino hello

HDInsight è in grado di eseguire processi Pig Latin in vari modi. Utilizzare hello seguente toodecide tabella quale metodo si adatta alle proprie esigenze, quindi seguire il collegamento hello per una procedura dettagliata.

| **Usare questo** se si desidera... | ...una shell **interattiva** | ...elaborazione**batch** | ...con questo **sistema operativo cluster** | ...da questo **client** |
|:--- |:---:|:---:|:--- |:--- |
| [SSH](hdinsight-hadoop-use-pig-ssh.md) |✔ |✔ |Linux |Linux, Unix, Mac OS X o Windows |
| [Curl](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |✔ |Linux o Windows |Linux, Unix, Mac OS X o Windows |
| [.NET SDK per Hadoop](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |✔ |Linux o Windows |Windows (per ora) |
| [Windows PowerShell](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |✔ |Linux o Windows |Windows |
| [Desktop remoto](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 e 3.3) |✔ |✔ |Windows |Windows |

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="pig-and-sql-server-integration-services"></a>Pig e SQL Server Integration Services

È possibile utilizzare SQL Server Integration Services (SSIS) toorun un processo Pig. Hello Azure Feature Pack per SSIS fornisce hello seguenti dei componenti che funzionano con i processi Pig in HDInsight.

* [Attività di Pig di Azure HDInsight][pigtask]

* [Gestione connessione della sottoscrizione di Azure][connectionmanager]

Altre informazioni su hello Azure Feature Pack per SSIS [qui][ssispack].

## <a id="nextsteps"></a>Passaggi successivi
Ora che si è appreso come toouse Pig con HDInsight, utilizzare hello seguendo i collegamenti tooexplore toowork altri modi con Azure HDInsight.

* [Caricare dati tooHDInsight][hdinsight-upload-data]
* [Usare Hive con HDInsight][hdinsight-use-hive]
* [Usare Sqoop con Hadoop in HDInsight](hdinsight-use-sqoop.md)
* [Usare Oozie con HDInsight](hdinsight-use-oozie.md)
* [Usare processi MapReduce con HDInsight][hdinsight-use-mapreduce]

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
