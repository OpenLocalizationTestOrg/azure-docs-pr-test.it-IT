---
title: aaaMapReduce e la connessione SSH con Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come i processi toouse SSH toorun MapReduce con Hadoop in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 844678ba-1e1f-4fda-b9ef-34df4035d547
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 9626577687fc5cc119a39d65a9c45298f57f81c2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-with-hadoop-on-hdinsight-with-ssh"></a>Usare MapReduce con Hadoop in HDInsight con SSH

[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

Informazioni su come i processi MapReduce toosubmit un tooHDInsight connessione Secure Shell (SSH).

> [!NOTE]
> Se si ha già familiarità con basati su Linux, Hadoop server, ma si sono tooHDInsight nuovo, vedere [suggerimenti basati su Linux HDInsight](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Prerequisiti

* Un cluster HDInsight (Hadoop in HDInsight) basato su Linux.

  > [!IMPORTANT]
  > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un client SSH. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="ssh"></a>Connettersi con SSH

Connettere il cluster toohello tramite SSH. Ad esempio, hello comando seguente si connette tooa cluster denominato **myhdinsight**:

```bash
ssh admin@myhdinsight-ssh.azurehdinsight.net
```

**Se si utilizza una chiave del certificato per l'autenticazione SSH**, potrebbe essere necessario percorso hello toospecify della chiave privata hello nel sistema client, ad esempio:

```bash
ssh -i ~/mykey.key admin@myhdinsight-ssh.azurehdinsight.net
```

**Se si utilizza una password per l'autenticazione SSH**, è necessario tooprovide password hello, quando richiesto.

Per altre informazioni sull'uso di SSH con HDInsight, vedere l'articolo [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

## <a id="hadoop"></a>Usare i comandi Hadoop

1. Dopo avere connesso toohello cluster HDInsight, toostart un processo MapReduce il comando che segue hello di utilizzo:

    ```bash
    yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-mapreduce-examples.jar wordcount /example/data/gutenberg/davinci.txt /example/data/WordCountOutput
    ```

    Questo comando Avvia hello `wordcount` (classe), contenute in hello `hadoop-mapreduce-examples.jar` file. Usa hello `/example/data/gutenberg/davinci.txt` documento come input e output viene memorizzato in `/example/data/WordCountOutput`.

    > [!NOTE]
    > Per ulteriori informazioni su questi dati di esempio MapReduce hello e di processo, vedere [utilizzare MapReduce in Hadoop in HDInsight](hdinsight-use-mapreduce.md).

2. processo Hello genera dettagli come elabora e restituisce informazioni toohello simile seguente testo al termine il processo di hello:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623

3. Al termine del processo di hello, utilizzare i seguenti file di output di comando toolist hello hello:

    ```bash
    hdfs dfs -ls /example/data/WordCountOutput
    ```

    Con questo comando vengono visualizzati due file: `_SUCCESS` e `part-r-00000`. Hello `part-r-00000` file contiene l'output di hello per questo processo.

    > [!NOTE]
    > Alcuni processi MapReduce possono dividere risultati hello in più **parte-r-# # #** file. In questo caso, utilizzare hello # # # suffisso ordine hello tooindicate dei file hello.

4. l'output di hello tooview, utilizzare hello comando seguente:

    ```bash
    hdfs dfs -cat /example/data/WordCountOutput/part-r-00000
    ```

    Questo comando Visualizza un elenco di parole hello contenuti in hello **wasb://example/data/gutenberg/davinci.txt** file e hello il numero di volte in cui ogni parola si è verificato. Hello testo riportato di seguito è riportato un esempio di hello i dati contenuti nel file hello:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Riepilogo

Come si può notare, i comandi di Hadoop forniscono toorun un modo semplice i processi MapReduce in un cluster HDInsight e visualizzazione output di hello processo.

## <a id="nextsteps"></a>Passaggi successivi

Per informazioni generali sui processi MapReduce in HDInsight:

* [Usare MapReduce in HDInsight Hadoop](hdinsight-use-mapreduce.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)
