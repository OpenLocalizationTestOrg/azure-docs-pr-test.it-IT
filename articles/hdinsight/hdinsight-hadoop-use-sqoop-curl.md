---
title: aaaUse Hadoop Sqoop in HDInsight - Azure latino | Documenti Microsoft
description: Informazioni su come tooremotely inviare Sqoop processi tooHDInsight utilizzando Curl.
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 39798321-78ca-428c-bcfe-322e49af4059
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: d9c09a6704ab6c5f48be50ed6d6314ec406df8ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-sqoop-jobs-with-hadoop-in-hdinsight-with-curl"></a>Esecuzione di processi Sqoop con Hadoop in HDInsight mediante Curl
[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

Informazioni su come cluster di toouse Curl toorun Sqoop processi in un Hadoop in HDInsight.

CURL è toodemonstrate usato come è possibile interagire con HDInsight con toorun di richieste HTTP non elaborato, monitoraggio e recuperare risultati di hello dei processi Sqoop. Questo procedimento funziona tramite hello API REST WebHCat (precedentemente noto come Templeton) fornita da cluster HDInsight.

> [!NOTE]
> Se si ha già familiarità con i server basati su Linux, Hadoop, ma sono tooHDInsight nuovo, vedere [informazioni sull'uso di HDInsight su Linux](hdinsight-hadoop-linux-information.md).
> 
> 

## <a name="prerequisites"></a>Prerequisiti
passaggi di hello toocomplete in questo articolo, è necessario seguente hello:

* Un cluster Hadoop in HDInsight (basato su Linux o su Windows)
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a name="submit-sqoop-jobs-by-using-curl"></a>Inviare processi Sqoop mediante Azure Curl
> [!NOTE]
> Quando si utilizza Curl o qualsiasi altra comunicazione REST con WebHCat, è necessario autenticare le richieste di hello specificando nome utente hello e la password per l'amministratore del cluster HDInsight hello. È inoltre necessario utilizzare il nome del cluster hello come parte di hello Uniform Resource Identifier (URI) utilizzato toosend hello richieste toohello server.
> 
> Per i comandi hello in questa sezione, sostituire **USERNAME** con hello utente tooauthenticate toohello cluster e sostituire **PASSWORD** con password hello per account utente di hello. Sostituire **CLUSTERNAME** con nome hello del cluster.
> 
> Hello API REST è protetto tramite [l'autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication). È consigliabile eseguire sempre le richieste tramite HTTPS (Secure HTTP) toohelp assicurarsi che le credenziali vengono inviate in modo sicuro toohello server.
> 
> 

1. Dalla riga di comando, utilizzare hello dopo che è possibile connettersi a cluster di HDInsight tooyour tooverify di comando:
   
        curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
   
    Verrà visualizzato di seguito toohello simile risposta:
   
        {"status":"ok","version":"v1"}
   
    i parametri di Hello utilizzati in questo comando sono i seguenti:
   
   * **-u** -nome utente hello e la password utilizzati richiesta hello tooauthenticate.
   * **-G** : indica che si tratta di una richiesta GET.
     
     Hello inizio hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, sarà hello uguale per tutte le richieste. percorso di Hello, **/status**, indica che la richiesta hello è tooreturn stato WebHCat (noto anche come Templeton) per il server di hello. 
2. Utilizzare hello toosubmit un processo sqoop seguenti:

        curl -u USERNAME:PASSWORD -d user.name=USERNAME -d command="export --connect jdbc:sqlserver://SQLDATABASESERVERNAME.database.windows.net;user=USERNAME@SQLDATABASESERVERNAME;password=PASSWORD;database=SQLDATABASENAME --table log4jlogs --export-dir /tutorials/usesqoop/data --input-fields-terminated-by \0x20 -m 1" -d statusdir="wasb:///example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/sqoop

    i parametri di Hello utilizzati in questo comando sono i seguenti:

    * **-d** - dal `-G` non viene utilizzato, richiesta hello predefinite metodo POST toohello. `-d`Specifica i valori dei dati hello vengono inviati con richiesta di hello.

        * **User.Name** -utente hello che esegue il comando hello.

        * **comando** -hello tooexecute comando Sqoop.

        * **statusdir** -directory hello hello stato per il processo verrà scritto.

    Questo comando deve restituire un ID di processo che può essere utilizzato toocheck hello stato del processo di hello.

        {"id":"job_1415651640909_0026"}

1. stato di hello toocheck del processo di hello, utilizzare hello comando seguente. Sostituire **JOBID** con valore hello restituito nel passaggio precedente hello. Ad esempio, se hello restituirà valore `{"id":"job_1415651640909_0026"}`, quindi **JOBID** sarebbe `job_1415651640909_0026`.
   
        curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
   
    Se il completamento del processo di hello, sarà stato hello **SUCCEEDED**.
   
   > [!NOTE]
   > Questa richiesta Curl restituisce un documento di JavaScript Object Notation (JSON) con informazioni sul processo hello; viene utilizzato jq tooretrieve hello solo valore di stato.
   > 
   > 
2. Dopo aver cambiato troppo hello lo stato del processo di hello**SUCCEEDED**, è possibile recuperare i risultati di hello del processo di hello dall'archiviazione Blob di Azure. Hello `statusdir` parametro passato con query hello contiene percorso hello hello del file di output; in questo caso, **wasb: / / / esempio/curl**. Questo indirizzo archivia l'output di hello del processo di hello in hello **esempio/curl** directory nel contenitore di archiviazione predefinito hello utilizzato dal cluster HDInsight.
   
    È possibile elencare e scaricare questi file tramite hello [CLI di Azure](../cli-install-nodejs.md). Ad esempio, file toolist **esempio/curl**, utilizzare hello comando seguente:
   
        azure storage blob list <container-name> example/curl
   
    toodownload un file, usare nomi hello seguenti:
   
        azure storage blob download <container-name> <blob-name> <destination-file>
   
   > [!NOTE]
   > È necessario specificare nome account di archiviazione hello che contiene il blob di hello utilizzando hello `-a` e `-k` parametri o set hello **AZURE\_archiviazione\_ACCOUNT** e **AZURE\_archiviazione\_accesso\_chiave** le variabili di ambiente. Vedere <a href="hdinsight-upload-data.md" target="_blank" per altre informazioni.
   > 
   > 

## <a name="limitations"></a>Limitazioni
* Eseguire l'esportazione bulk - HDInsight basati su Linux con, hello Sqoop connettore utilizzato tooexport dati tooMicrosoft SQL Server o Database SQL di Azure attualmente non supporta inserimenti bulk.
* Divisione in batch - con HDInsight basati su Linux, quando si utilizza hello `-batch` passare quando l'esecuzione di inserimenti, Sqoop eseguirà più inserimenti anziché l'invio in batch le operazioni di inserimento hello.

## <a name="summary"></a>Riepilogo
Come illustrato in questo documento, è possibile utilizzare un toorun di richiesta HTTP non elaborato, monitoraggio e visualizzare i risultati dei processi Sqoop hello il cluster HDInsight.

Per ulteriori informazioni sull'interfaccia REST hello usata in questo articolo, vedere hello <a href="https://sqoop.apache.org/docs/1.99.3/RESTAPI.html" target="_blank">Guida API REST Sqoop</a>.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni generali su Hive con HDInsight:

* [Usare Sqoop con Hadoop in HDInsight](hdinsight-use-sqoop.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)

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




[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


