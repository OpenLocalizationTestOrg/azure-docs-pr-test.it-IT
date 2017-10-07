---
title: aaaUse Hadoop Hive in HDInsight - Azure latino | Documenti Microsoft
description: Informazioni su come inviare tooremotely Pig processi tooHDInsight utilizzando Curl.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 6ce18163-63b5-4df6-9bb6-8fcbd4db05d8
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: e725829ad2adcf3540f44375e3e87b7cdaebd15e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-hive-queries-with-hadoop-in-hdinsight-using-rest"></a>Esecuzione di query Hive con Hadoop in HDInsight tramite REST

[!INCLUDE [hive-selector](../../includes/hdinsight-selector-use-hive.md)]

Informazioni su come toouse hello API REST WebHCat toorun Hive esegue una query con Hadoop in cluster HDInsight di Azure.

[CURL](http://curl.haxx.se/) è toodemonstrate usato come è possibile interagire con HDInsight mediante richieste HTTP non elaborate. Hello [jq](http://stedolan.github.io/jq/) utilità viene restituiti da richieste REST i dati JSON hello tooprocess utilizzato.

> [!NOTE]
> Se si ha già familiarità con i server basati su Linux, Hadoop, ma sono tooHDInsight nuovo, vedere hello [è necessario tooknow su Hadoop in HDInsight basati su Linux](hdinsight-hadoop-linux-information.md) documento.

## <a id="curl"></a>Eseguire query Hive

> [!NOTE]
> Quando si utilizza cURL o qualsiasi altra comunicazione REST con WebHCat, è necessario autenticare le richieste di hello specificando nome utente hello e la password per l'amministratore del cluster HDInsight hello.
>
> Per i comandi hello in questa sezione, sostituire **USERNAME** con hello utente tooauthenticate toohello cluster e sostituire **PASSWORD** con password hello per account utente di hello. Sostituire **CLUSTERNAME** con nome hello del cluster.
>
> Hello API REST è protetto tramite [l'autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication). toohelp assicurarsi che le credenziali non sono in modo sicuro inviato toohello server, richiedere sempre tramite HTTPS (Secure HTTP).

1. Dalla riga di comando, utilizzare hello dopo che è possibile connettersi a cluster di HDInsight tooyour tooverify di comando:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Viene visualizzato un toohello simile di risposta seguente testo:

        {"status":"ok","version":"v1"}

    i parametri di Hello utilizzati in questo comando sono i seguenti:

   * **-u** -nome utente hello e la password utilizzati richiesta hello tooauthenticate.
   * **-G** - indica che è un'operazione GET.

     Hello inizio hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello uguale per tutte le richieste. percorso di Hello, **/status**, indica che la richiesta hello è tooreturn stato WebHCat (noto anche come Templeton) per il server di hello. È inoltre possibile richiedere una versione di hello dell'Hive tramite hello comando seguente:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/version/hive
    ```

     Questa richiesta restituisce un toohello simile di risposta seguente testo:

       {"module":"hive","version":"0.13.0.2.1.6.0-2103"}

2. Hello utilizzare seguenti una tabella denominata toocreate **log4jLogs**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;DROP+TABLE+log4jLogs;CREATE+EXTERNAL+TABLE+log4jLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+ROW+FORMAT+DELIMITED+FIELDS+TERMINATED+BY+' '+STORED+AS+TEXTFILE+LOCATION+'/example/data/';SELECT+t4+AS+sev,COUNT(*)+AS+count+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log'+GROUP+BY+t4;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Hello parametri utilizzati con la richiesta seguente:

   * **-d** - dal `-G` non viene utilizzato, richiesta hello predefinite metodo POST toohello. `-d`Specifica i valori dei dati hello vengono inviati con richiesta di hello.

     * **User.Name** -utente hello che esegue il comando hello.
     * **eseguire** -hello tooexecute istruzioni HiveQL.
     * **statusdir** -directory hello hello stato per questo processo viene scritto.

     Queste istruzioni consentono di eseguire hello seguenti azioni:
   * **DROP TABLE** -hello tabella esiste già, viene eliminato.
   * **CREATE EXTERNAL TABLE** : crea una nuova tabella "external" in Hive. Le tabelle esterne archiviano solo definizione della tabella hello nell'Hive. dati Hello viene lasciati nella posizione originale hello.

     > [!NOTE]
     > Le tabelle esterne da utilizzare quando si prevede di hello sottostante toobe dati aggiornati da un'origine esterna. Ad esempio, un processo di caricamento dati automatizzato o un'altra operazione MapReduce.
     >
     > Eliminazione di una tabella esterna **non** eliminare dati hello e definizione della tabella solo hello.

   * **FORMATO di riga** - come dati hello viene formattati. i campi di Hello in ogni log sono separati da uno spazio.
   * **ARCHIVIATO come file di testo percorso** - hello memorizzati (directory dati di esempio/hello) e a cui è archiviato come testo.
   * **Selezionare** -seleziona un conteggio di tutte le righe in cui colonna **t4** contiene il valore di hello **[errore]**. L'istruzione dovrebbe restituire un valore pari a **3**, poiché sono presenti tre righe contenenti questo valore.

     > [!NOTE]
     > Si noti che gli spazi di hello tra le istruzioni HiveQL vengono sostituiti da hello `+` carattere se usato con Curl. I valori tra virgolette che contengono uno spazio, ad esempio il delimitatore di hello, non devono essere sostituiti da `+`.

   * **INPUT__FILE__NAME come '% 25.log'** - questa istruzione limiti hello ricerca tooonly utilizza file che terminano con. log.

     > [!NOTE]
     > Hello `%25` è un formato di URL codificato hello %, pertanto condizione effettiva hello è `like '%.log'`. % Hello ha toobe URL codificato, viene considerato come un carattere speciale in URL.

     Questo comando deve restituire un ID di processo che può essere utilizzato toocheck hello stato del processo di hello.

       {"id":"job_1415651640909_0026"}

3. stato di hello toocheck del processo di hello, utilizzare hello comando seguente:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Sostituire **JOBID** con valore hello restituito nel passaggio precedente hello. Ad esempio, se hello restituirà valore `{"id":"job_1415651640909_0026"}`, quindi **JOBID** sarebbe `job_1415651640909_0026`.

    Se ha completato il processo di hello, non è stato hello **SUCCEEDED**.

   > [!NOTE]
   > Questa richiesta Curl restituisce un documento di JavaScript Object Notation (JSON) con informazioni sul processo hello. Viene utilizzato Jq tooretrieve hello solo valore di stato.

4. Dopo aver cambiato troppo hello lo stato del processo di hello**SUCCEEDED**, è possibile recuperare i risultati di hello del processo di hello dall'archiviazione Blob di Azure. Hello `statusdir` parametro passato con query hello contiene percorso hello hello del file di output; in questo caso, **esempio/curl**. Questo indirizzo archivia l'output di hello in hello **esempio/curl** directory hello cluster di archiviazione predefinito.

    È possibile elencare e scaricare questi file tramite hello [CLI di Azure](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli). Per ulteriori informazioni sull'utilizzo di hello CLI di Azure con l'archiviazione di Azure, vedere hello [Usa Azure CLI 2.0 con l'archiviazione di Azure](https://docs.microsoft.com/en-us/azure/storage/storage-azure-cli#create-and-manage-blobs) documento.

5. Hello utilizzare seguendo le istruzioni toocreate 'internal' nuova tabella denominata **degli errori**:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="set+hive.execution.engine=tez;CREATE+TABLE+IF+NOT+EXISTS+errorLogs(t1+string,t2+string,t3+string,t4+string,t5+string,t6+string,t7+string)+STORED+AS+ORC;INSERT+OVERWRITE+TABLE+errorLogs+SELECT+t1,t2,t3,t4,t5,t6,t7+FROM+log4jLogs+WHERE+t4+=+'[ERROR]'+AND+INPUT__FILE__NAME+LIKE+'%25.log';SELECT+*+from+errorLogs;" -d statusdir="/example/curl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/hive
    ```

    Queste istruzioni consentono di eseguire hello seguenti azioni:

   * **CREATE TABLE IF NOT EXISTS** : crea una tabella, se non esiste già. Questa istruzione crea una tabella interna, che viene archiviata nel data warehouse di hello Hive e completamente gestita da Hive.

     > [!NOTE]
     > A differenza delle tabelle esterne, eliminazione di una tabella interna Elimina hello anche i dati sottostanti.

   * **ARCHIVIATI AS ORC** -archivia i dati di hello in formato con ottimizzazione per la riga a colonne (ORC). ORC è un formato altamente ottimizzato ed efficiente per l'archiviazione di dati Hive.
   * **INSERT OVERWRITE ... Selezionare** -seleziona le righe da hello **log4jLogs** tabella contenenti **[errore]**, quindi inserisce dati di hello in hello **degli errori** tabella.
   * **Selezionare** -Seleziona tutte le righe da hello nuovo **degli errori** tabella.

6. Utilizzare l'ID di processo hello toocheck hello stato del processo di hello restituito. Una volta completata, utilizzare hello CLI di Azure come descritto in precedenza toodownload e visualizzare i risultati di hello. output di Hello deve contenere tre righe, ciascuna delle quali contiene **[errore]**.

## <a id="nextsteps"></a>Passaggi successivi

Per informazioni generali su Hive con HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)

Se si utilizza Tez con Hive, vedere hello documenti per le informazioni di debug seguenti:

* [Utilizzare hello vista Ambari Tez in HDInsight basati su Linux](hdinsight-debug-ambari-tez-view.md)

Per ulteriori informazioni sull'API REST utilizzato in questo documento hello, vedere hello [WebHCat riferimento](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference) documento.

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


