---
title: aaaUse Hadoop Hive nella Console di Query in HDInsight - Azure hello | Documenti Microsoft
description: Informazioni su come toouse hello basata sul web Console Query toorun query Hive in un HDInsight Hadoop cluster dal browser.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5ae074b0-f55e-472d-94a7-005b0e79f779
ms.service: hdinsight
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 01/12/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 621882082c9a07655d34b8dc980b8e47dd04b745
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-query-console"></a>Esecuzione di query Hive utilizzando hello Console di Query
[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

In questo articolo si apprenderà come query Hive in un HDInsight Hadoop toouse hello HDInsight Query Console toorun cluster dal browser.

> [!IMPORTANT]
> Hello Console Query HDInsight è disponibile solo in cluster HDInsight basati su Windows. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Per HDInsight 3.4 o versione successiva, vedere [Run Hive queries in Ambari Hive View](hdinsight-hadoop-use-hive-ambari-view.md) (Eseguire query Hive nella vista Ambari Hive) per informazioni sull'esecuzione di query Hive da un Web browser.

## <a id="prereq"></a>Prerequisiti
passaggi di hello toocomplete in questo articolo, sarà necessario seguente hello.

* Un cluster HDInsight Hadoop basato su Windows
* Un Web browser moderno

## <a id="run"></a>Esecuzione di query Hive utilizzando hello Console di Query
1. Aprire un web browser e passare troppo**https://CLUSTERNAME.azurehdinsight.net**, dove **CLUSTERNAME** hello nome del cluster HDInsight. Se richiesto, immettere nome utente hello e la password usata al momento della creazione del cluster di hello.
2. Selezionare i collegamenti hello nella parte superiore di hello della pagina hello, **Editor Hive**. Consente di visualizzare un form che può essere utilizzati tooenter hello HiveQL istruzioni che si desidera toorun nel cluster HDInsight hello.

    ![editor dell'hive Hello](./media/hdinsight-hadoop-use-hive-query-console/queryconsole.png)

    Sostituire il testo hello `Select * from hivesampletable` con hello seguendo le istruzioni HiveQL:

        set hive.execution.engine=tez;
        DROP TABLE log4jLogs;
        CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
        ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
        STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
        SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

    Queste istruzioni consentono di eseguire hello seguenti azioni:

   * **DROP TABLE**: Elimina tabella hello e file di dati hello hello tabella esiste già.
   * **CREATE EXTERNAL TABLE**: crea una nuova tabella "external" in Hive. Le tabelle esterne archiviano solo definizione della tabella hello nell'Hive; dati Hello viene lasciati nella posizione originale hello.

     > [!NOTE]
     > Tabelle esterne devono essere utilizzate quando si prevede di hello toobe dati aggiornati da un'origine esterna (ad esempio, un processo di caricamento automatico dei dati) o da un'altra operazione MapReduce sottostante, ma è sempre che dati più recenti di hello toouse una query Hive.
     >
     > Eliminazione di una tabella esterna **non** eliminare dati hello e definizione della tabella solo hello.
     >
     >
   * **FORMATO di riga**: indica Hive formattazione dati hello. In questo caso, i campi di hello in ogni log sono separati da uno spazio.
   * **ARCHIVIATO come file di testo percorso**: indica Hive in cui si hello dati archiviati (directory dati di esempio/hello) e a cui è archiviato come testo
   * **Selezionare**: selezionare un conteggio di tutte le righe in cui colonna **t4** contiene il valore di hello **[errore]**. Dovrebbe restituire un valore pari a **3** , poiché sono presenti tre righe contenenti questo valore.
   * **INPUT__FILE__NAME come '%.log'** - indica a Hive che si dovrebbero restituire solo i dati da file che terminano con .log. Questo limita hello ricerca toohello sample.log file contenente dati hello e si impedisce la restituzione di dati da altri esempio i file di dati che non corrispondono allo schema di hello che è definiti.
3. Fare clic su **Submit**. Hello **sessione del processo** in hello nella parte inferiore della pagina hello deve visualizzare i dettagli per il processo di hello.
4. Quando hello **stato** campo modifiche troppo**completato**selezionare **Visualizza dettagli** per processo hello. Nella pagina dettagli hello hello **Output processo** contiene `[ERROR]    3`. È possibile utilizzare hello **scaricare** pulsante sotto toodownload questo campo, un file che contiene l'output di hello del processo di hello.

## <a id="summary"></a>Riepilogo
Come si può notare, hello Console di Query fornisce un modo semplice di toorun esegue una query Hive in un cluster HDInsight, monitorare lo stato del processo hello e recuperare l'output di hello.

Selezionare toolearn ulteriori informazioni sull'utilizzo dei processi di Console di Query Hive toorun Hive, **Introduzione** nella parte superiore di hello di hello Console di Query, quindi utilizzare gli esempi di hello forniti. Ogni esempio vengono illustrati il processo di hello dell'utilizzo di dati tooanalyze Hive, tra cui una spiegazione sulle istruzioni HiveQL hello utilizzate nell'esempio hello.

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



[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
