---
title: aaaUse Hadoop Hive e Desktop remoto in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come cluster di tooconnect tooHadoop in HDInsight mediante Desktop remoto e quindi eseguire le query Hive usando hello Hive interfaccia della riga di comando.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 8c228e35-d58a-4f22-917a-1d20c9da89b4
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: f86ffc1be33a8b0b2346d1a1388e5dfa6d0f8777
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hive-with-hadoop-on-hdinsight-with-remote-desktop"></a>Uso di Hive con Hadoop in HDInsight con Desktop remoto
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

In questo articolo si apprenderà come tooconnect tooan HDInsight cluster tramite Desktop remoto e quindi eseguire Hive esegue una query utilizzando hello Hive interfaccia della riga di comando (CLI).

> [!IMPORTANT]
> Desktop remoto è disponibile solo nei cluster HDInsight che usa Windows come sistema operativo hello. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Per HDInsight 3.4 o successiva, vedere [utilizzare Hive con HDInsight e Beeline](hdinsight-hadoop-use-hive-beeline.md) per informazioni sull'esecuzione di query Hive direttamente nel cluster hello dalla riga di comando.

## <a id="prereq"></a>Prerequisiti
passaggi di hello toocomplete in questo articolo, è necessario seguente hello:

* Un cluster HDInsight (Hadoop in HDInsight) basato su Windows
* Un computer client che esegue Windows 10, Windows 8 o Windows 7

## <a id="connect"></a>Connettersi con Desktop remoto
Abilitare Desktop remoto per il cluster HDInsight hello e quindi connettersi tooit seguendo le istruzioni di hello in [connettersi tooHDInsight cluster tramite RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).

## <a id="hive"></a>Utilizzare il comando di Hive hello
Quando si è connessi toohello desktop per il cluster HDInsight hello, usare hello seguendo i passaggi toowork con Hive:

1. Dal desktop di HDInsight hello, avviare hello **della riga di comando Hadoop**.
2. Immettere hello hello toostart comando CLI Hive seguenti:

        %hive_home%\bin\hive

    Quando è stata avviata hello CLI, verrà visualizzato il prompt di Hive CLI hello: `hive>`.
3. Tramite hello CLI, immettere hello seguendo le istruzioni toocreate una nuova tabella denominata **log4jLogs** utilizzando dati di esempio:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Queste istruzioni consentono di eseguire hello seguenti azioni:

   * **DROP TABLE**: Elimina tabella hello e file di dati hello hello tabella esiste già.
   * **CREATE EXTERNAL TABLE**: crea una nuova tabella "external" in Hive. Le tabelle esterne archiviano solo definizione della tabella hello nell'Hive (Buongiorno dati viene lasciati nella posizione originale hello).

     > [!NOTE]
     > Tabelle esterne devono essere utilizzate quando si prevede di hello toobe dati aggiornati da un'origine esterna (ad esempio, un processo di caricamento automatico dei dati) o da un'altra operazione MapReduce sottostante, ma è sempre che dati più recenti di hello toouse una query Hive.
     >
     > Eliminazione di una tabella esterna **non** eliminare dati hello e definizione della tabella solo hello.
     >
     >
   * **FORMATO di riga**: indica Hive formattazione dati hello. In questo caso, i campi di hello in ogni log sono separati da uno spazio.
   * **ARCHIVIATO come file di testo percorso**: indica Hive in cui si hello dati archiviati (directory dati di esempio/hello) e a cui è archiviato come testo.
   * **Selezionare**: seleziona un conteggio di tutte le righe in cui colonna **t4** contiene il valore di hello **[errore]**. Dovrebbe restituire un valore pari a **3** , poiché sono presenti tre righe contenenti questo valore.
   * **INPUT__FILE__NAME come '%.log'** - indica a Hive che si dovrebbero restituire solo i dati da file che terminano con .log. Questo limita hello ricerca toohello sample.log file contenente dati hello e si impedisce la restituzione di dati da altri esempio i file di dati che non corrispondono allo schema di hello che è definiti.
4. Hello utilizzare seguendo le istruzioni toocreate 'internal' nuova tabella denominata **degli errori**:

        CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
        INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';

    Queste istruzioni consentono di eseguire hello seguenti azioni:

   * **CREATE TABLE IF NOT EXISTS**: crea una tabella, se non esiste già. Poiché hello **esterno** parola chiave non viene usato, si tratta di una tabella interna, che viene archiviata nel data warehouse di hello Hive e completamente gestita da Hive.

     > [!NOTE]
     > A differenza di **esterno** tabelle, anche l'eliminazione di una tabella interna Elimina hello dati sottostanti.
     >
     >
   * **ARCHIVIATI AS ORC**: archivia i dati di hello in formato a colonne (ORC) con ottimizzazione per la riga. Questo è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.
   * **INSERT OVERWRITE ... Selezionare**: Seleziona le righe da hello **log4jLogs** tabella contenenti **[errore]**, quindi inserisce dati di hello in hello **degli errori** tabella.

     tooverify che solo le righe che contengono **[errore]** nella colonna t4 sono stata archiviata toohello **degli errori** tabella, utilizzare hello seguente istruzione tooreturn tutte le righe di hello **degli errori**:

       SELECT * from errorLogs;

     Dovrebbero essere restituite tre righe di dati, tutte contenenti **[ERROR]** nella colonna t4.

## <a id="summary"></a>Riepilogo
Come si può notare, hello hello comando Hive fornisce toointeractively un modo più semplice eseguire query Hive in un cluster HDInsight, hello di monitoraggio dello stato del processo e recuperare l'output di hello.

## <a id="nextsteps"></a>Passaggi successivi
Per informazioni generali su Hive in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)

Se si utilizza Tez con Hive, vedere hello documenti per le informazioni di debug seguenti:

* [Utilizzare hello Tez UI in HDInsight basati su Windows](hdinsight-debug-tez-ui.md)
* [Utilizzare hello vista Ambari Tez in HDInsight basati su Linux](hdinsight-debug-ambari-tez-view.md)

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md





[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
