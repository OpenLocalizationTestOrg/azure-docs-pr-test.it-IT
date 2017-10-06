---
title: aaaHive con gli strumenti di Data Lake (Hadoop) per Visual Studio - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come toouse hello Data Lake tools per Visual Studio toorun Apache Hive query con Apache Hadoop in HDInsight di Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2b3e672a-1195-4fa5-afb7-b7b73937bfbe
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: dc76974c02cf68bcf701b2b155842c9e9c5cb988
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-using-hello-data-lake-tools-for-visual-studio"></a>Esecuzione di query Hive con strumenti di Data Lake hello per Visual Studio

Informazioni su come toouse hello Data Lake strumenti per Apache Hive tooquery di Visual Studio. gli strumenti di Data Lake Hello consentono tooeasily creare, inviare e monitorare tooHadoop query Hive in HDInsight di Azure.

## <a id="prereq"></a>Prerequisiti

* Un cluster Azure HDInsight (Hadoop in HDInsight)

  > [!IMPORTANT]
  > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Visual Studio (una delle seguenti versioni di hello):

    * Visual Studio 2013 Community/Professional/Premium/Ultimate con Update 4

    * Visual Studio 2015, qualsiasi edizione

    * Visual Studio 2017, qualsiasi edizione

* Strumenti HDInsight per Visual Studio o Azure Data Lake Tools per Visual Studio. Vedere [iniziare a usare gli strumenti di Visual Studio Hadoop per HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md) per informazioni sull'installazione e configurazione di strumenti hello.

## <a id="run"></a>Esecuzione di query Hive utilizzando hello Visual Studio

1. Aprire **Visual Studio** e scegliere **Nuovo** > **Progetto** > **Azure Data Lake** > **HIVE** > **Applicazione Hive**. Specificare un nome per questo progetto.

2. Aprire hello **Script.hql** file che viene creato con questo progetto e Incolla in hello seguendo le istruzioni HiveQL:

   ```hiveql
   set hive.execution.engine=tez;
   DROP TABLE log4jLogs;
   CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
   ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
   STORED AS TEXTFILE LOCATION '/example/data/';
   SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND  INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
   ```

    Queste istruzioni consentono di eseguire hello seguenti azioni:

   * `DROP TABLE`: Hello tabella esiste, questa istruzione eliminata.

   * `CREATE EXTERNAL TABLE`: crea una nuova tabella "esterna" in Hive. Le tabelle esterne archiviano solo la definizione di tabella hello nell'Hive (Buongiorno dati viene lasciati nella posizione originale hello).

     > [!NOTE]
     > Le tabelle esterne da utilizzare quando si prevede di hello sottostante toobe dati aggiornati da un'origine esterna. Ad esempio, un processo MapReduce o un servizio di Azure.
     >
     > Eliminazione di una tabella esterna **non** eliminare dati hello e definizione della tabella solo hello.

   * `ROW FORMAT`: Indica la formattazione di dati hello Hive. In questo caso, i campi di hello in ogni log sono separati da uno spazio.

   * `STORED AS TEXTFILE LOCATION`: Indica Hive dove hello memorizzati (directory dati di esempio/hello) e a cui è archiviato come testo.

   * `SELECT`: Selezionare un conteggio di tutte le righe in cui colonna `t4` contiene il valore di hello `[ERROR]`. L'istruzione dovrebbe restituire un valore pari a `3`, poiché sono presenti tre righe contenenti questo valore.

   * `INPUT__FILE__NAME LIKE '%.log'`: indica a Hive che si dovrebbero restituire solo i dati da file che terminano con .log. Questa clausola limita hello toohello sample.log file di ricerca contiene dati hello.

3. Dalla barra degli strumenti hello, selezionare hello **HDInsight Cluster** che si desidera toouse per questa query. Selezionare **Invia** istruzioni hello toorun come un processo Hive.

   ![Barra di invio](./media/hdinsight-hadoop-use-hive-visual-studio/toolbar.png)

4. Hello **Hive riepilogo** viene visualizzata e visualizza le informazioni sull'esecuzione del processo hello. Hello utilizzare **aggiornamento** collegamento toorefresh hello informazioni sul processo finché hello **lo stato del processo** cambia troppo**completato**.

   ![riepilogo del processo che mostra un processo completato](./media/hdinsight-hadoop-use-hive-visual-studio/jobsummary.png)

5. Hello utilizzare **Output processo** collegamento di output di hello tooview del processo. Visualizza `[ERROR] 3`, ovvero il valore di hello restituito dalla query.

6. È anche possibile eseguire query Hive senza creare un progetto. Usando **Esplora server**, espandere **Azure** > **HDInsight**, fare clic con il pulsante destro del mouse sul server HDInsight, quindi scegliere **Scrivi una query Hive**.

7. In hello **temp.hql** documento che viene visualizzata, aggiungere hello seguendo le istruzioni HiveQL:

   ```hiveql
   set hive.execution.engine=tez;
   CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
   INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
   ```

    Queste istruzioni consentono di eseguire hello seguenti azioni:

   * `CREATE TABLE IF NOT EXISTS`: crea una tabella, se non esiste già. Poiché hello `EXTERNAL` parola chiave non viene utilizzato, l'istruzione seguente crea una tabella interna. Le tabelle interne vengono archiviate nel data warehouse di hello Hive e vengono gestite dall'Hive.

     > [!NOTE]
     > A differenza di `EXTERNAL` tabelle, anche l'eliminazione di una tabella interna Elimina hello dati sottostanti.

   * `STORED AS ORC`: Archivia hello dati in formato di riga con ottimizzazione per la colonna (ORC). ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.

   * `INSERT OVERWRITE ... SELECT`: Consente di selezionare le righe da hello `log4jLogs` tabella contenenti `[ERROR]`, quindi inserisce dati di hello in hello `errorLogs` tabella.

8. Dalla barra degli strumenti hello, selezionare **Invia** processo hello toorun. Hello utilizzare **lo stato del processo** toodetermine processo hello è stata completata.

9. tooverify che hello processo creato tabella hello, utilizzare **Esplora Server** espandere **Azure** > **HDInsight** > cluster HDInsight > **Database hive** > **predefinito**. Hello **degli errori** tabella e hello **log4jLogs** sono elencati nella tabella.

## <a id="nextsteps"></a>Passaggi successivi

Come si può notare, gli strumenti di HDInsight hello per Visual Studio forniscono un modo semplice di toowork con query Hive in HDInsight.

Per informazioni generali su Hive in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)

* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)

Per ulteriori informazioni sugli strumenti di HDInsight hello per Visual Studio:

* [Introduzione all'uso di HDInsight Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md)

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

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx

[image-hdi-hive-powershell]: ./media/hdinsight-use-hive/HDI.HIVE.PowerShell.png
[img-hdi-hive-powershell-output]: ./media/hdinsight-use-hive/HDI.Hive.PowerShell.Output.png
[image-hdi-hive-architecture]: ./media/hdinsight-use-hive/HDI.Hive.Architecture.png
