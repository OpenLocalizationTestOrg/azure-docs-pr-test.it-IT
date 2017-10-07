---
title: cluster aaaUse inserire il Spark toosubmit processi tooSpark in Azure HDInsight | Documenti Microsoft
description: "Informazioni su come toouse API REST di Apache Spark toosubmit Spark i processi in modalità remota cluster Azure HDInsight tooan."
keywords: apache spark rest api,livy spark
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2817b779-1594-486b-8759-489379ca907d
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/25/2017
ms.author: nitinme
ms.openlocfilehash: 417213b5f1db1522373188002fe05117faea5243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-spark-rest-api-toosubmit-remote-jobs-tooan-hdinsight-spark-cluster"></a>Utilizzare l'API REST di Apache Spark toosubmit processi remoti tooan cluster HDInsight Spark

Informazioni su come inserire il, hello Apache Spark l'API REST che è usato toosubmit remoto toouse processi cluster Azure HDInsight Spark tooan. Per informazioni dettagliate, vedere [Livy](https://github.com/cloudera/hue/tree/master/apps/spark/java#welcome-to-livy-the-rest-spark-server).

È possibile utilizzare la shell inserire il toorun interattiva Spark o inviare toobe processi batch eseguiti Spark. In questo articolo parla mediante processi batch di inserire il toosubmit. frammenti di codice Hello in questo articolo usare cURL toomake endpoint di inserire il Spark toohello chiamate API REST.

**Prerequisiti:**

* Un cluster Apache Spark in HDInsight. Per istruzioni, vedere l'articolo relativo alla [creazione di cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md).

* [cURL](http://curl.haxx.se/). In questo articolo Usa toodemonstrate cURL come toomake API REST chiama su un cluster di HDInsight Spark.

## <a name="submit-a-livy-spark-batch-job"></a>Inviare un processo batch Livy Spark
Prima di inviare un processo batch, è necessario caricare i file jar applicazione hello nell'archiviazione cluster hello associato hello cluster. È possibile utilizzare [ **AzCopy**](../storage/common/storage-use-azcopy.md), un'utilità della riga di comando, toodo in modo. Esistono vari altri client è possibile utilizzare dati tooupload. Altre informazioni in merito sono disponibili in [Caricare dati per processi Hadoop in HDInsight](hdinsight-upload-data.md).

    curl -k --user "<hdinsight user>:<user password>" -v -H <content-type> -X POST -d '{ "file":"<path tooapplication jar>", "className":"<classname in jar>" }' 'https://<spark_cluster_name>.azurehdinsight.net/livy/batches'

**Esempi**:

* Se il file jar hello nell'archiviazione cluster hello (WASB)
  
        curl -k --user "admin:mypassword1!" -v -H 'Content-Type: application/json' -X POST -d '{ "file":"wasb://mycontainer@mystorageaccount.blob.core.windows.net/data/SparkSimpleTest.jar", "className":"com.microsoft.spark.test.SimpleFile" }' "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Se si desidera toopass hello nome del file jar e hello classname come parte di un file di input (in questo esempio, txt)
  
        curl -k  --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"

## <a name="get-information-on-livy-spark-batches-running-on-hello-cluster"></a>Ottenere informazioni su Spark inserire il batch in esecuzione nel cluster hello
    curl -k --user "<hdinsight user>:<user password>" -v -X GET "https://<spark_cluster_name>.azurehdinsight.net/livy/batches"

**Esempi**:

* Se si desidera che tutti i batch di inserire il Spark hello in esecuzione nel cluster hello tooretrieve:
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
* Se si desidera un batch specifico con un determinato batchId tooretrieve
  
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="delete-a-livy-spark-batch-job"></a>Eliminare un processo batch Livy Spark
    curl -k --user "<hdinsight user>:<user password>" -v -X DELETE "https://<spark_cluster_name>.azurehdinsight.net/livy/batches/{batchId}"

**Esempio**:

    curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/{batchId}"

## <a name="livy-spark-and-high-availability"></a>Livy Spark e disponibilità elevata
Inserire il fornisce disponibilità elevata per i processi di Spark in esecuzione nel cluster hello. Ecco alcuni esempi.

* Se il servizio di inserire il hello diventa inattivo dopo l'invio di un processo in modalità remota tooa Spark cluster, hello processo continua toorun in background hello. Quando inserire il backup, viene ripristinato lo stato di hello del processo hello e dei report di nuovo.
* Notebook Jupyter per HDInsight sono supportate da inserire il nel back-end hello. Se un blocco per Appunti è in esecuzione un processo di Spark e hello servizio inserire il Ottiene riavviato, notebook hello continua celle di codice hello toorun. 

## <a name="show-me-an-example"></a>Mostra un esempio
In questa sezione è esaminare il processo batch toosubmit di esempi toouse Spark inserire il, monitorare lo stato di avanzamento hello del processo di hello e quindi eliminarlo. viene usato in questo esempio di applicazione Hello è hello una sviluppate nell'articolo hello [creare un'applicazione Scala autonoma e toorun nel cluster di HDInsight Spark](hdinsight-apache-spark-create-standalone-application.md). Questa procedura Hello presuppone che:

* Già stata copiata su hello applicazione jar toohello account di archiviazione associato hello cluster.
* È necessario CuRL installato nel computer di hello in cui si sta provando questa procedura.

Eseguire hello alla procedura seguente:

1. Segnalare il problema verificare innanzitutto che Spark inserire il è in esecuzione nel cluster hello. È possibile eseguire questa operazione ottenendo un elenco di batch in esecuzione. Se si esegue un processo di inserire il hello prima volta, l'output di hello deve restituire zero.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    È necessario ottenere un toohello simile output frammento di codice seguente:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:47:53 GMT
        < Content-Length: 34
        <
        {"from":0,"total":0,"sessions":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Si noti come viene visualizzato hello ultima riga di output di hello **totale: 0**, che non suggerisce nessun batch in esecuzione.

2. Inviare ora un processo batch. Hello frammento di codice seguente viene utilizzato un nome di file di input (txt) toopass hello jar e il nome di classe hello come parametri. Se si eseguono questi passaggi da un computer Windows, utilizzando un file di input è hello approccio consigliato.
   
        curl -k --user "admin:mypassword1!" -v -H "Content-Type: application/json" -X POST --data @C:\Temp\input.txt "https://mysparkcluster.azurehdinsight.net/livy/batches"
   
    Hello parametri nel file hello **input.txt** sono definite come segue:
   
        { "file":"wasb:///example/jars/SparkSimpleApp.jar", "className":"com.microsoft.spark.example.WasbIOTest" }
   
    Verrà visualizzato un toohello simile output frammento di codice seguente:
   
        < HTTP/1.1 201 Created
        < Content-Type: application/json; charset=UTF-8
        < Location: /0
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:51:30 GMT
        < Content-Length: 36
        <
        {"id":0,"state":"starting","log":[]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Si noti come ultima riga di hello dell'output di hello afferma **stato: avvio**. Indica anche **id:0**. In questo caso, **0** è hello ID del batch.

3. È ora possibile recuperare lo stato di hello di questo batch specifico utilizzando l'ID del batch hello.
   
        curl -k --user "admin:mypassword1!" -v -X GET "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Verrà visualizzato un toohello simile output frammento di codice seguente:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Fri, 20 Nov 2015 23:54:42 GMT
        < Content-Length: 509
        <
        {"id":0,"state":"success","log":["\t diagnostics: N/A","\t ApplicationMaster host: 10.0.0.4","\t ApplicationMaster RPC port: 0","\t queue: default","\t start time: 1448063505350","\t final status: SUCCEEDED","\t tracking URL: http://hn0-myspar.lpel1gnnvxne3gwzqkfq5u5uzh.jx.internal.cloudapp.net:8088/proxy/application_1447984474852_0002/","\t user: root","15/11/20 23:52:47 INFO Utils: Shutdown hook called","15/11/20 23:52:47 INFO Utils: Deleting directory /tmp/spark-b72cd2bf-280b-4c57-8ceb-9e3e69ac7d0c"]}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    output di Hello illustrato **stato: operazione riuscita**, che suggerisce che il processo di hello è stata completata.

4. Se si desidera, è ora possibile eliminare i batch di hello.
   
        curl -k --user "admin:mypassword1!" -v -X DELETE "https://mysparkcluster.azurehdinsight.net/livy/batches/0"
   
    Verrà visualizzato un toohello simile output frammento di codice seguente:
   
        < HTTP/1.1 200 OK
        < Content-Type: application/json; charset=UTF-8
        < Server: Microsoft-IIS/8.5
        < X-Powered-By: ARR/2.5
        < X-Powered-By: ASP.NET
        < Date: Sat, 21 Nov 2015 18:51:54 GMT
        < Content-Length: 17
        <
        {"msg":"deleted"}* Connection #0 toohost mysparkcluster.azurehdinsight.net left intact
   
    Hello l'ultima riga dell'output di hello mostra che batch hello è stata eliminata. Anche l'eliminazione di un processo, mentre è in esecuzione, Termina processo hello. Se si elimina un processo che è stata completata, completato o in caso contrario, Elimina le informazioni di processo hello completamente.

## <a name="using-livy-spark-on-hdinsight-35-clusters"></a>Uso di Livy Spark nei cluster HDInsight 3.5

Cluster HDInsight 3.5, per impostazione predefinita, disabilita l'utilizzo del file di dati di esempio di file locale percorsi tooaccess o JAR. Si consiglia di hello toouse `wasb://` percorso invece tooaccess JAR o dati di esempio di file dal cluster hello. Se si desidera toouse di percorso locale, è necessario aggiornare di conseguenza configurazione Ambari hello. toodo in modo:

1. Passare toohello Ambari portale per i cluster di hello. interfaccia utente Web Ambari Hello è disponibile il cluster HDInsight in https://**CLUSTERNAME**. azurehdidnsight.net, dove CLUSTERNAME è il nome di hello del cluster.

2. Hello riquadro di spostamento sinistro, fare clic su **inserire il**, quindi fare clic su **configurazioni**.

3. In **inserire il predefinito** aggiungere il nome di proprietà hello `livy.file.local-dir-whitelist` e impostarne il valore troppo**"/"** se si desidera tooallow accesso completo toofile sistema. Se si desidera tooallow accesso tooa solo di directory specifico, fornire directory toothat del percorso di hello come valore hello.

## <a name="submitting-livy-jobs-for-a-cluster-within-an-azure-virtual-network"></a>Invio di processi Livy per un cluster all'interno di una rete virtuale di Azure

Se ci si connette tooan cluster HDInsight Spark da all'interno di una rete virtuale di Azure, è possibile connettersi direttamente tooLivy nel cluster hello. In tal caso, hello URL per l'endpoint di inserire il `http://<IP address of hello headnode>:8998/batches`. In questo caso, **8998** hello porta in cui inserire il viene eseguito sul nodo head del cluster di hello. Per altre informazioni sull'accesso ai servizi sulle porte non pubbliche, vedere [Porte usate dai servizi Hadoop su HDInsight](hdinsight-hadoop-port-settings-for-services.md).

## <a name="troubleshooting"></a>Risoluzione dei problemi

Ecco alcuni problemi che potrebbero verificarsi durante l'utilizzo di inserire il per i cluster di tooSpark invio processo remoto.

### <a name="using-an-external-jar-from-hello-additional-storage-is-not-supported"></a>Utilizzo di un jar esterna dalla memoria aggiuntiva hello non è supportato

**Problema:** se il processo di inserire il Spark fa riferimento a un jar esterno dall'account di archiviazione aggiuntive hello associato hello cluster, il processo di hello non riesce.

**Risoluzione:** assicurarsi che si desidera toouse è disponibile in spazio di archiviazione predefinito hello associato al cluster HDInsight hello file jar di hello.





## <a name="next-step"></a>Passaggio successivo

* [Gestire le risorse di cluster di hello Apache Spark in HDInsight di Azure](hdinsight-apache-spark-resource-manager.md)
* [Tenere traccia ed eseguire il debug di processi in esecuzione nel cluster Apache Spark in Azure HDInsight](hdinsight-apache-spark-job-debugging.md)

