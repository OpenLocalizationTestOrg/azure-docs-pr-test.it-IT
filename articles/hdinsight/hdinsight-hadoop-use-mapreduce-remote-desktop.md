---
title: aaaMapReduce e Desktop remoto con Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come toouse Desktop remoto tooconnect tooHadoop HDInsight e l'esecuzione dei processi di MapReduce.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9d3a7b34-7def-4c2e-bb6c-52682d30dee8
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: bdbbcf59ca86dd1b170471aa9e12334a04c23667
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-mapreduce-in-hadoop-on-hdinsight-with-remote-desktop"></a>Uso di MapReduce con Hadoop in HDInsight con Desktop remoto
[!INCLUDE [mapreduce-selector](../../includes/hdinsight-selector-use-mapreduce.md)]

In questo articolo verrà informazioni su come tooconnect tooa Hadoop in HDInsight cluster tramite Desktop remoto e quindi eseguire i processi MapReduce utilizzando i comandi di Hadoop hello.

> [!IMPORTANT]
> Desktop re,moto è disponibile solo nei cluster HDInsight basati su Windows. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Per HDInsight 3.4 o successiva, vedere [utilizzare MapReduce con SSH](hdinsight-hadoop-use-mapreduce-ssh.md) per informazioni sulla connessione cluster HDInsight toohello e in esecuzione processi di MapReduce.

## <a id="prereq"></a>Prerequisiti
passaggi di hello toocomplete in questo articolo, è necessario seguente hello:

* Un cluster HDInsight (Hadoop in HDInsight) basato su Windows
* Un computer client che esegue Windows 10, Windows 8 o Windows 7

## <a id="connect"></a>Connettersi con Desktop remoto
Abilitare Desktop remoto per il cluster HDInsight hello e quindi connettersi tooit seguendo le istruzioni di hello in [connettersi tooHDInsight cluster tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hadoop"></a>Utilizzare il comando di Hadoop hello
Quando si è connessi toohello desktop per il cluster HDInsight hello, utilizzare hello seguendo i passaggi toorun un processo MapReduce tramite il comando di Hadoop hello:

1. Dal desktop di HDInsight hello, avviare hello **della riga di comando Hadoop**. Si apre un nuovo prompt in hello **c:\apps\dist\hadoop-&lt;numero di versione >** directory.

   > [!NOTE]
   > numero di versione di Hello cambia in caso di aggiornamento Hadoop. Hello **HADOOP_HOME** variabile di ambiente può essere il percorso di hello toofind utilizzato. Ad esempio, `cd %HADOOP_HOME%` modifiche directory toohello directory Hadoop, senza la necessità di un numero di versione di hello tooknow.
   >
   >
2. hello toouse **Hadoop** toorun un processo MapReduce di esempio di comando, utilizzare hello comando seguente:

        hadoop jar hadoop-mapreduce-examples.jar wordcount wasb:///example/data/gutenberg/davinci.txt wasb:///example/data/WordCountOutput

    Verrà avviata hello **wordcount** (classe), contenute in hello **hadoop-mapreduce-examples.jar** file nella directory corrente hello. Usa come input, hello **wasb://example/data/gutenberg/davinci.txt** documento e l'output è memorizzato nel: **wasb: / / / esempio/data/WordCountOutput**.

   > [!NOTE]
   > Per ulteriori informazioni su questi dati di esempio MapReduce hello e di processo, vedere <a href="hdinsight-use-mapreduce.md">utilizzare MapReduce di HDInsight Hadoop</a>.
   >
   >
3. processo Hello genera dettagli come l'elaborazione e restituisce toohello informazioni simili che seguono. una volta completato il processo di hello:

        File Input Format Counters
        Bytes Read=1395666
        File Output Format Counters
        Bytes Written=337623
4. Una volta completato il processo di hello, utilizzare hello i seguenti file di comando toolist hello output è archiviati in **wasb://example/data/WordCountOutput**:

        hadoop fs -ls wasb:///example/data/WordCountOutput

    In questo modo, vengono visualizzati due file: **_SUCCESS** e **part-r-00000**. Hello **parte-r-00000** file contiene l'output di hello per questo processo.

   > [!NOTE]
   > Alcuni processi MapReduce possono dividere risultati hello in più **parte-r-# # #** file. In questo caso, utilizzare hello # # # suffisso ordine hello tooindicate dei file hello.
   >
   >
5. l'output di hello tooview, utilizzare hello comando seguente:

        hadoop fs -cat wasb:///example/data/WordCountOutput/part-r-00000

    Consente di visualizzare un elenco di parole hello contenuti in hello **wasb://example/data/gutenberg/davinci.txt** file, con numero di hello di volte in cui ogni parola si è verificato. Hello Ecco un esempio di dati hello che saranno contenuti nel file hello:

        wreathed        3
        wreathing       1
        wreaths         1
        wrecked         3
        wrenching       1
        wretched        6
        wriggling       1

## <a id="summary"></a>Riepilogo
Come si può notare, hello Hadoop comando fornisce toorun un modo semplice i processi MapReduce in un cluster HDInsight e visualizzazione output di hello processo.

## <a id="nextsteps"></a>Passaggi successivi
Per informazioni generali sui processi MapReduce in HDInsight:

* [Usare MapReduce in HDInsight Hadoop](hdinsight-use-mapreduce.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)
