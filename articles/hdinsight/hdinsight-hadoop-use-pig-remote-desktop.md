---
title: aaaUse Hadoop Pig con Desktop remoto in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse hello Pig comando toorun latino Pig le istruzioni da un cluster di Hadoop basato su Windows tooa connessione Desktop remoto in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: e034a286-de0f-465f-8bf1-3d085ca6abed
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/17/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 2a4565fa827cd45fdbe6194b0486df93a6561084
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-from-a-remote-desktop-connection"></a>Eseguire processi Pig da una connessione Desktop remoto
[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Questo documento fornisce una procedura dettagliata per l'utilizzo di istruzioni hello Pig comando toorun latino Pig da un cluster di HDInsight basati su Windows tooa connessione Desktop remoto. Alfabeto latino Pig consente toocreate MapReduce applicazioni descrivendo le trasformazioni dei dati, anziché eseguire il mapping e ridurre le funzioni.

> [!IMPORTANT]
> Desktop remoto è disponibile solo nei cluster HDInsight che usa Windows come sistema operativo hello. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Per HDInsight 3.4 o successiva, vedere [usare Pig con HDInsight e SSH](hdinsight-hadoop-use-pig-ssh.md) per informazioni sull'esecuzione di Pig in modo interattivo i processi direttamente nel hello cluster da una riga di comando.

## <a id="prereq"></a>Prerequisiti
passaggi di hello toocomplete in questo articolo, sarà necessario seguente hello.

* Un cluster HDInsight (Hadoop in HDInsight) basato su Windows
* Un computer client che esegue Windows 10, Windows 8 o Windows 7

## <a id="connect"></a>Connettersi con Desktop remoto
Abilitare Desktop remoto per il cluster HDInsight hello e quindi connettersi tooit seguendo le istruzioni di hello in [connettersi tooHDInsight cluster tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="pig"></a>Comando Pig hello
1. Dopo aver creato una connessione Desktop remoto, avviare hello **della riga di comando Hadoop** utilizzando icona hello sul desktop di hello.
2. Utilizzare hello toostart hello Pig comando seguente:

        %pig_home%\bin\pig

    Verrà visualizzato un prompt dei comandi `grunt>` .
3. Immettere l'istruzione hello:

        LOGS = LOAD 'wasb:///example/data/sample.log';

    Il comando Carica contenuto hello del file sample.log hello in file log hello. È possibile visualizzare il contenuto di hello del file hello utilizzando hello comando seguente:

        DUMP LOGS;
4. Trasformare i dati di hello applicando un livello di registrazione di hello solo tooextract di espressione regolare di ogni record:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    È possibile utilizzare **DUMP** dati hello tooview dopo la trasformazione hello. In questo caso, `DUMP LEVELS;`.
5. Continuare l'applicazione di trasformazioni utilizzando hello seguendo le istruzioni. Utilizzare `DUMP` risultato hello tooview della trasformazione hello dopo ogni passaggio.

    <table>
    <tr>
    <th>Istruzione</th><th>Risultato</th>
    </tr>
    <tr>
    <td>FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;</td><td>Rimuove le righe che contengono un valore null per il livello di registrazione hello e archivia i risultati di hello in FILTEREDLEVELS.</td>
    </tr>
    <tr>
    <td>GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;</td><td>Hello di gruppi di righe dal livello di registrazione e archivia i risultati di hello in GROUPEDLEVELS.</td>
    </tr>
    <tr>
    <td>FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;</td><td>Crea un nuovo set di dati che contiene ciascun valore univoco del livello di registrazione e il numero di occorrenze. I risultati vengono memorizzati in FREQUENCIES</td>
    </tr>
    <tr>
    <td>RESULT = order FREQUENCIES by COUNT desc;</td><td>Ordina i livelli di registrazione hello conteggio (decrescente) e archivia nel risultato</td>
    </tr>
    </table>
6.È inoltre possibile salvare i risultati di hello di una trasformazione utilizzando hello `STORE` istruzione. Ad esempio, hello comando seguente salva hello `RESULT` toohello **/example/data/pigout** directory nel contenitore di archiviazione hello predefinito per il cluster:

        STORE RESULT into 'wasb:///example/data/pigout'

   > [!NOTE]
   > dati Hello viene archiviati nella directory specificata di hello in file denominati **parte nnnnn**. Se esiste già una directory di hello, si riceverà un messaggio di errore.
   >
   >
7. hello tooexit grunt prompt dei comandi, immettere l'istruzione hello.

        QUIT;

### <a name="pig-latin-batch-files"></a>File batch di Pig Latin
Inoltre, è possibile utilizzare hello Pig comando toorun latino Pig contenuta in un file.

1. Dopo la chiusura prompt grunt hello, aprire **blocco note** e creare un nuovo file denominato **pigbatch.pig** in hello **PIG_HOME %** directory.
2. Tipo o a seguito di hello Incolla righe in hello **pigbatch.pig** file e quindi salvarlo:

        LOGS = LOAD 'wasb:///example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;
3. Hello utilizzare seguente hello toorun **pigbatch.pig** file utilizzando il comando di pig hello.

        pig %PIG_HOME%\pigbatch.pig

    Al termine del processo batch hello, verrà visualizzato dopo l'output, che deve essere hello stesso come quando si utilizza hello `DUMP RESULT;` nei passaggi precedenti hello:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)

## <a id="summary"></a>Riepilogo
Come si può notare, hello comando Pig consente toointeractively consentono di eseguire operazioni di MapReduce o eseguire processi latino Pig archiviate in un file batch.

## <a id="nextsteps"></a>Passaggi successivi
Per informazioni generali su Pig in HDInsight:

* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)
