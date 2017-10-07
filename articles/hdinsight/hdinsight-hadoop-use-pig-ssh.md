---
title: aaaUse Hadoop Pig con SSH in un cluster HDInsight - Azure | Documenti Microsoft
description: Informazioni su come connettersi cluster basati su Linux, Hadoop tooa con SSH, e quindi Usa hello Pig comando toorun latino Pig istruzioni in modo interattivo o come un batch di processo.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b646a93b-4c51-4ba4-84da-3275d9124ebe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 1da303e239b537e6b331b1d33010058582718c90
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-on-a-linux-based-cluster-with-hello-pig-command-ssh"></a>Eseguire i processi di Pig in un cluster basato su Linux con hello comando Pig (SSH)

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Informazioni su come eseguire processi Pig di toointeractively da un cluster di HDInsight tooyour connessione SSH. Hello linguaggio di programmazione Pig latino consente trasformazioni toodescribe di output di hello desiderato tooproduce dati applicato toohello di input.

> [!IMPORTANT]
> Hello passaggi in questo documento richiedono un cluster HDInsight basati su Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a id="ssh"></a>Connettersi con SSH

Utilizzare cluster di HDInsight tooyour tooconnect SSH. esempio Hello collega tooa cluster denominato **myhdinsight** come account hello denominato **sshuser**:

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net

**Se si fornisce una chiave del certificato per l'autenticazione SSH** al momento della creazione del cluster HDInsight hello, potrebbe essere necessario percorso hello toospecify della chiave privata hello nel sistema client.

    ssh sshuser@myhdinsight-ssh.azurehdinsight.net -i ~/mykey.key

**Se è stata specificata una password per l'autenticazione SSH** al momento della creazione del cluster HDInsight hello, fornire una password, hello quando richiesto.

Per altre informazioni sull'uso di SSH con HDInsight, vedere l'articolo [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="pig"></a>Comando Pig hello

1. Una volta connessi, è possibile avviare interfaccia della riga di comando di hello Pig (CLI) utilizzando hello comando seguente:

        pig

    Dopo qualche istante verrà visualizzato un prompt dei comandi `grunt>` .

2. Immettere l'istruzione hello:

        LOGS = LOAD '/example/data/sample.log';

    Il comando Carica contenuto hello del file sample.log hello nei log. È possibile visualizzare il contenuto di hello del file hello utilizzando hello seguente istruzione:

        DUMP LOGS;

3. Trasformare quindi dati hello applicando un livello di registrazione di hello solo tooextract di espressione regolare di ogni record utilizzando hello seguente istruzione:

        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;

    È possibile utilizzare **DUMP** dati hello tooview dopo la trasformazione hello. In questo caso, usare `DUMP LEVELS;`.

4. Continuare l'applicazione di trasformazioni utilizzando le istruzioni di hello nei hello nella tabella seguente:

    | Istruzione Pig Latin | Quale istruzione hello |
    | ---- | ---- |
    | `FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;` | Rimuove le righe che contengono un valore null per il livello di registrazione hello e archivia i risultati di hello in `FILTEREDLEVELS`. |
    | `GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;` | Hello di gruppi di righe dal livello di registrazione e archivia i risultati di hello in `GROUPEDLEVELS`. |
    | `FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;` | Crea un set di dati che contiene ciascun valore univoco del livello di registrazione e il numero di occorrenze. set di dati Hello viene archiviato in `FREQUENCIES`. |
    | `RESULT = order FREQUENCIES by COUNT desc;` | Ordina i livelli di registrazione hello in base al conteggio (decrescente) e archivia in `RESULT`. |

    > [!TIP]
    > Utilizzare `DUMP` risultato hello tooview della trasformazione hello dopo ogni passaggio.

5. È inoltre possibile salvare i risultati di hello di una trasformazione utilizzando hello `STORE` istruzione. Ad esempio, hello istruzione Salva hello `RESULT` toohello `/example/data/pigout` directory di archiviazione hello predefiniti per il cluster:

        STORE RESULT into '/example/data/pigout';

   > [!NOTE]
   > dati Hello viene archiviati nella directory specificata di hello in file denominati `part-nnnnn`. Se esiste già una directory di hello, viene visualizzato un errore.

6. hello tooexit grunt prompt dei comandi, immettere l'istruzione hello:

        QUIT;

### <a name="pig-latin-batch-files"></a>File batch di Pig Latin

È inoltre possibile utilizzare hello Pig comando toorun latino Pig contenuti in un file.

1. Dopo la chiusura prompt grunt hello, seguente hello utilizzare comando toopipe STDIN in un file denominato `pigbatch.pig`. Questo file viene creato nella directory home hello hello account utente SSH.

        cat > ~/pigbatch.pig

2. Digitare o incollare hello le righe seguenti e quindi utilizzare Ctrl + D al termine.

        LOGS = LOAD '/example/data/sample.log';
        LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
        FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
        GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
        FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
        RESULT = order FREQUENCIES by COUNT desc;
        DUMP RESULT;

3. Comando che segue di hello utilizzare hello toorun `pigbatch.pig` file utilizzando il comando di Pig hello.

        pig ~/pigbatch.pig

    Al termine del processo batch hello, vedrai hello seguente output:

        (TRACE,816)
        (DEBUG,434)
        (INFO,96)
        (WARN,11)
        (ERROR,6)
        (FATAL,2)


## <a id="nextsteps"></a>Passaggi successivi

Per informazioni generali su Pig in HDInsight, vedere hello seguente documento:

* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)

Per ulteriori informazioni su altri modi di toowork con Hadoop in HDInsight, vedere hello seguenti documenti:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)
