---
title: aaaUse MapReduce e Curl con Hadoop in HDInsight - Azure | Documenti Microsoft
description: Informazioni su come tooremotely eseguire i processi MapReduce con Hadoop in HDInsight mediante Curl.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: bc6daf37-fcdc-467a-a8a8-6fb2f0f773d1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: 16920205bacf9699f88090568099e0508a172b3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="run-mapreduce-jobs-with-hadoop-on-hdinsight-using-rest"></a>Esecuzione di processi MapReduce con Hadoop in HDInsight tramite REST

Informazioni su come toouse hello API REST WebHCat toorun MapReduce i processi in un Hadoop nel cluster HDInsight. CURL è toodemonstrate usato come è possibile interagire con HDInsight con i processi MapReduce toorun le richieste HTTP non elaborati.

> [!NOTE]
> Se si ha già familiarità con i server basati su Linux, Hadoop, ma sono tooHDInsight nuovo, vedere hello [è necessario tooknow su basati su Linux, Hadoop in HDInsight](hdinsight-hadoop-linux-information.md) documento.


## <a id="prereq"></a>Prerequisiti

* Un cluster Hadoop in HDInsight
* [Curl](http://curl.haxx.se/)
* [jq](http://stedolan.github.io/jq/)

## <a id="curl"></a>Eseguire processi MapReduce mediante Curl

> [!NOTE]
> Quando si utilizza Curl o qualsiasi altra comunicazione REST con WebHCat, è necessario autenticare le richieste di hello, fornendo la password e nome utente dell'amministratore del cluster HDInsight hello. È necessario utilizzare il nome del cluster hello come parte dell'URI utilizzato toosend hello richieste toohello server hello.
>
> Per i comandi hello in questa sezione, sostituire **USERNAME** cluster toohello tooauthenticate utente hello e **PASSWORD** con password hello per account utente di hello. Sostituire **CLUSTERNAME** con nome hello del cluster.
>
> Hello API REST vengono protetti tramite [l'autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication). È consigliabile eseguire sempre le richieste utilizzando HTTPS tooensure che le credenziali vengono inviate in modo sicuro toohello server.


1. Dalla riga di comando, utilizzare hello dopo che è possibile connettersi a cluster di HDInsight tooyour tooverify di comando:

    ```bash
    curl -u USERNAME:PASSWORD -G https://CLUSTERNAME.azurehdinsight.net/templeton/v1/status
    ```

    Si dovrebbe ricevere un toohello simile di risposta JSON seguente:

        {"status":"ok","version":"v1"}

    i parametri di Hello utilizzati in questo comando sono i seguenti:

   * **-u**: indica il nome di utente hello e la password utilizzati richiesta hello tooauthenticate
   * **-G**: indica che questa operazione è una richiesta GET

     Hello inizio hello URI, **https://CLUSTERNAME.azurehdinsight.net/templeton/v1**, hello uguale per tutte le richieste.

2. un processo MapReduce, toosubmit utilizzare hello comando seguente:

    ```bash
    curl -u USERNAME:PASSWORD -d user.name=USERNAME -d jar=/example/jars/hadoop-mapreduce-examples.jar -d class=wordcount -d arg=/example/data/gutenberg/davinci.txt -d arg=/example/data/CurlOut https://CLUSTERNAME.azurehdinsight.net/templeton/v1/mapreduce/jar
    ```

    fine Hello di hello URI (mapreduce/jar) indica WebHCat che questa richiesta viene avviato un processo MapReduce da una classe in un file jar. i parametri di Hello utilizzati in questo comando sono i seguenti:

   * **-d**: `-G` non viene utilizzato, in modo richiesta hello predefinite metodo POST toohello. `-d`Specifica i valori dei dati hello vengono inviati con richiesta di hello.
    * **User.Name**: hello utente che esegue il comando hello
    * **file JAR**: è stato eseguito il percorso di hello del file jar hello contenente toobe di classe
    * **classe**: hello classe che contiene la logica MapReduce hello
    * **arg**: hello argomenti toobe passato toohello il processo MapReduce. In questo caso, hello input directory hello e di file di testo che vengono usate per l'output di hello

     Questo comando deve restituire un ID di processo che può essere utilizzato toocheck hello stato del processo di hello:

       {"id":"job_1415651640909_0026"}

3. stato di hello toocheck del processo di hello, utilizzare hello comando seguente:

    ```bash
    curl -G -u USERNAME:PASSWORD -d user.name=USERNAME https://CLUSTERNAME.azurehdinsight.net/templeton/v1/jobs/JOBID | jq .status.state
    ```

    Sostituire hello **JOBID** con valore hello restituito nel passaggio precedente hello. Ad esempio, se hello restituirà valore `{"id":"job_1415651640909_0026"}`, quindi hello JOBID sarebbe `job_1415651640909_0026`.

    Se il processo di hello è stato completato, lo stato di hello restituito è `SUCCEEDED`.

   > [!NOTE]
   > Questa richiesta Curl restituisce un documento JSON con informazioni sul processo hello. Viene utilizzato Jq tooretrieve hello solo valore di stato.

4. Quando hello cambiato lo stato del processo di hello troppo`SUCCEEDED`, è possibile recuperare i risultati di hello del processo di hello dall'archiviazione Blob di Azure. Hello `statusdir` parametro che viene passata con query hello contiene il percorso di hello hello del file di output. In questo esempio, è il percorso di hello `/example/curl`. Questo indirizzo archivia l'output di hello del processo di hello in spazio di archiviazione di hello cluster predefinito in `/example/curl`.

È possibile elencare e scaricare questi file tramite hello [CLI di Azure 2.0](https://docs.microsoft.com/cli/azure/install-azure-cli). Per ulteriori informazioni sull'uso di BLOB da hello CLI di Azure, vedere hello [Using hello Azure CLI 2.0 con l'archiviazione di Azure](../storage/common/storage-azure-cli.md#create-and-manage-blobs) documento.

## <a id="nextsteps"></a>Passaggi successivi

Per informazioni generali sui processi MapReduce in HDInsight:

* [Usare MapReduce con Hadoop in HDInsight](hdinsight-use-mapreduce.md)

Per informazioni su altre modalità d'uso di Hadoop in HDInsight:

* [Usare Hive con Hadoop in HDInsight](hdinsight-use-hive.md)
* [Usare Pig con Hadoop in HDInsight](hdinsight-use-pig.md)

Per ulteriori informazioni sull'interfaccia REST hello utilizzato in questo articolo, vedere hello [WebHCat riferimento](https://cwiki.apache.org/confluence/display/Hive/WebHCat+Reference).
