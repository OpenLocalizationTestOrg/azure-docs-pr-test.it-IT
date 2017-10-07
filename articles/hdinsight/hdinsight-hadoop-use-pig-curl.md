---
title: aaaUse Hadoop Pig in HDInsight - Azure con | Documenti Microsoft
description: Informazioni su come cluster di toouse REST toorun Pig Latin i processi in un Hadoop in HDInsight di Azure.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: ed5e10d1-4f47-459c-a0d6-7ff967b468c4
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 760139e3caad9103d8c9d34e7f548d476014b5ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-pig-jobs-with-hadoop-on-hdinsight-by-using-rest"></a>Eseguire processi Pig con Hadoop in HDInsight tramite REST

[!INCLUDE [pig-selector](../../includes/hdinsight-selector-use-pig.md)]

Informazioni su come toorun latino Pig processi rendendo cluster Azure HDInsight tooan di richieste REST. CURL è toodemonstrate usato come è possibile interagire con HDInsight mediante l'API REST WebHCat hello.

> [!NOTE]
> Se si ha già familiarità con i server basati su Linux, Hadoop, ma sono tooHDInsight nuovo, vedere [suggerimenti basati su Linux di HDInsight](hdinsight-hadoop-linux-information.md).

## <a id="prereq"></a>Prerequisiti

* Un cluster Azure HDInsight (Hadoop in HDInsight) (basato su Linux o basato su Windows)

  > [!IMPORTANT]
  > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Curl](http://curl.haxx.se/)

* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Eseguire processi Pig mediante Curl

> [!NOTE]
> Hello API REST è protetto tramite [l'autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication). Verificare sempre le richieste utilizzando tooensure HTTPS (Secure HTTP) che le credenziali vengono inviate in modo sicuro toohello server.
>
> Quando si utilizzano i comandi di hello in questa sezione, sostituire `USERNAME` con hello utente tooauthenticate toohello cluster e sostituire `PASSWORD` con password hello per account utente di hello. Sostituire `CLUSTERNAME` con nome hello del cluster.
>


1. Dalla riga di comando, utilizzare hello dopo che è possibile connettersi a cluster di HDInsight tooyour tooverify di comando:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Si dovrebbe ricevere hello risposta JSON seguente:

        {"status":"ok","version":"v1"}

    i parametri di Hello utilizzati in questo comando sono i seguenti:

    * **-u**: nome utente hello e la password utilizzati richiesta hello tooauthenticate
    * **-G**: indica che è una richiesta GET.

     Hello inizio hello URL, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello uguale per tutte le richieste. percorso di Hello, **/status**, indica che la richiesta hello stato tooreturn hello di WebHCat (noto anche come Templeton) per il server di hello.

2. Utilizzare hello seguente codice toosubmit un cluster di toohello processo Pig latino:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d execute="LOGS=LOAD+'/example/data/sample.log';LEVELS=foreach+LOGS+generate+REGEX_EXTRACT($0,'(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)',1)+as+LOGLEVEL;FILTEREDLEVELS=FILTER+LEVELS+by+LOGLEVEL+is+not+null;GROUPEDLEVELS=GROUP+FILTEREDLEVELS+by+LOGLEVEL;FREQUENCIES=foreach+GROUPEDLEVELS+generate+group+as+LOGLEVEL,COUNT(FILTEREDLEVELS.LOGLEVEL)+as+count;RESULT=order+FREQUENCIES+by+COUNT+desc;DUMP+RESULT;" -d statusdir="/example/pigcurl" https://CLUSTERNAME.azurehdinsight.net/templeton/v1/pig
    ```

    i parametri di Hello utilizzati in questo comando sono i seguenti:

    * **-d**: perché `-G` non viene utilizzato, richiesta hello predefinite metodo POST toohello. `-d`Specifica i valori dei dati hello vengono inviati con richiesta di hello.

    * **User.Name**: hello utente che esegue il comando hello
    * **eseguire**: hello Pig latino istruzioni tooexecute
    * **statusdir**: directory hello hello stato per questo processo viene scritto

    > [!NOTE]
    > Si noti che gli spazi di hello in latino Pig istruzioni vengono sostituiti da hello `+` carattere se usato con Curl.

    Questo comando deve restituire un ID di processo che può essere utilizzato toocheck hello stato del processo di hello, ad esempio:

        {"id":"job_1415651640909_0026"}

3. stato hello toocheck del processo di hello, utilizzare hello comando seguente

     ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

     Sostituire `JOBID` con valore hello restituito nel passaggio precedente hello. Ad esempio, se hello restituirà valore `{"id":"job_1415651640909_0026"}`, quindi `JOBID` è `job_1415651640909_0026`.

    Se ha completato il processo di hello, non è stato hello **SUCCEEDED**.

    > [!NOTE]
    > Questa richiesta Curl restituisce documenti JavaScript Object Notation (JSON) con informazioni sul processo hello e jq è usato tooretrieve hello solo valore di stato.

## <a id="results"></a>Visualizzare risultati

Quando hello cambiato lo stato del processo di hello troppo**SUCCEEDED**, è possibile recuperare i risultati di hello di hello processo. Hello `statusdir` parametro passato con query hello contiene percorso hello hello del file di output; in questo caso, `/example/pigcurl`.

HDInsight è possibile utilizzare l'archiviazione di Azure o archivio Azure Data Lake come archivio dati predefinito di hello. Esistono vari modi tooget dati hello a seconda di quale utilizzare. Per ulteriori informazioni, vedere hello archiviazione sezione hello [HDInsight basati su Linux informazioni](hdinsight-hadoop-linux-information.md#hdfs-azure-storage-and-data-lake-store) documento.

## <a id="summary"></a>Riepilogo

Come illustrato in questo documento, è possibile utilizzare un toorun di richiesta HTTP non elaborato, monitoraggio e visualizzare i risultati dei processi Pig hello il cluster HDInsight.

Per ulteriori informazioni sull'interfaccia REST hello usata in questo articolo, vedere hello [WebHCat riferimento](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).

## <a id="nextsteps"></a>Passaggi successivi

Per informazioni generali su Pig in HDInsight:

* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)
