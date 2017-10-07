---
title: aaaGet avviato con un esempio di HBase in HDInsight - Azure | Documenti Microsoft
description: Seguire questa toostart esempio Apache HBase con hadoop in HDInsight. Creare tabelle dalla shell di HBase hello e di eseguire le query utilizzando l'Hive.
keywords: hbasecommand, esempio di hbase
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 4d6a2658-6b19-4268-95ee-822890f5a33a
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/17/2017
ms.author: jgao
ms.openlocfilehash: 43419780142b320b16180a2b1f25020dee2f7a11
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-an-apache-hbase-example-in-hdinsight"></a>Iniziare a usare un esempio di Apache HBase in HDInsight

Informazioni su come toocreate un cluster HBase in HDInsight, creare tabelle di HBase ed eseguire query di tabelle tramite Hive. Per informazioni generali su HBase, vedere [Panoramica di HDInsight HBase][hdinsight-hbase-overview].

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="prerequisites"></a>Prerequisiti
Prima di iniziare cercando in questo esempio di HBase, è necessario disporre di hello seguenti elementi:

* **Una sottoscrizione di Azure**. Vedere [Ottenere una versione di valutazione gratuita di Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).
* [Secure Shell (SSH)](hdinsight-hadoop-linux-use-ssh-unix.md). 
* [curl](http://curl.haxx.se/download.html).

## <a name="create-hbase-cluster"></a>Nome del cluster HBase
Hello procedura riportata di seguito utilizza un toocreate modello di gestione risorse di Azure una versione 3.4 HBase basati su Linux cluster e hello dipendenti di archiviazione di Azure account predefinito. parametri di hello toounderstand utilizzati nella procedura hello e altri metodi di creazione del cluster, vedere [cluster basati su Linux creare Hadoop in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).

1. Fare clic su hello seguente immagine tooopen hello modello hello portale di Azure. Hello modello si trova in un contenitore di blob pubblici. 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-hbase-linux%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hbase-tutorial-get-started-linux/deploy-to-azure.png" alt="Deploy tooAzure"></a>
2. Da hello **distribuzione personalizzata** pannello immettere hello seguenti valori:
   
   * **Sottoscrizione**: selezionare la sottoscrizione di Azure che è usato toocreate hello cluster.
   * **Gruppo di risorse**: creare un nuovo gruppo di Azure Resource Manager o usarne uno esistente.
   * **Percorso**: specificare il percorso di hello hello del gruppo di risorse. 
   * **ClusterName**: immettere un nome per il cluster di HBase hello.
   * **Nome account di accesso e la password del cluster**: nome di account di accesso predefinito hello **admin**.
   * **Nome utente SSH e password**: nome utente predefinito hello **sshuser**.  È possibile rinominarlo.
     
     Gli altri parametri sono facoltativi.  
     
     Ogni cluster ha una dipendenza dall'account di Archiviazione di Azure. Dopo l'eliminazione di un cluster, i dati di hello mantengono nell'account di archiviazione hello. nome dell'account di archiviazione di Hello cluster predefinito è il nome del cluster hello "archivio" aggiunto. È hardcoded nella sezione di hello modello variabili.
3. Selezionare **accetto le condizioni indicate in precedenza toohello**, quindi fare clic su **acquisto**. Sono necessari circa 20 minuti toocreate un cluster.

> [!NOTE]
> Dopo l'eliminazione di un cluster HBase, è possibile creare un altro cluster HBase tramite hello stesso contenitore di blob predefinito. il nuovo cluster di Hello preleva da tabelle di HBase hello creato nel cluster originale hello. tooavoid incoerenze, è consigliabile disabilitare le tabelle di hello HBase prima di eliminare il cluster hello.
> 
> 

## <a name="create-tables-and-insert-data"></a>Creare tabelle e inserire dati
È possibile utilizzare SSH tooconnect tooHBase cluster e utilizzare la Shell di HBase toocreate HBase tabelle, inserire i dati e i dati di query. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

Per la maggior parte degli utenti, i dati vengono visualizzati in formato tabulare hello:

![Tabella con dati HBase di HDInsight][img-hbase-sample-data-tabular]

In HBase (un'implementazione di BigTable), hello stesso dati ha un aspetto simile:

![Dati BigTable HBase di HDInsight][img-hbase-sample-data-bigtable]


**hello toouse shell di HBase**

1. Da SSH, eseguire hello HBase comando seguente:
   
    ```bash
    hbase shell
    ```

2. Creare un HBase con famiglie di due colonne:

    ```hbaseshell   
    create 'Contacts', 'Personal', 'Office'
    list
    ```
3. Inserire alcuni dati:
    
    ```hbaseshell   
    put 'Contacts', '1000', 'Personal:Name', 'John Dole'
    put 'Contacts', '1000', 'Personal:Phone', '1-425-000-0001'
    put 'Contacts', '1000', 'Office:Phone', '1-425-000-0002'
    put 'Contacts', '1000', 'Office:Address', '1111 San Gabriel Dr.'
    scan 'Contacts'
    ```
   
    ![Shell HBase Hadoop di HDInsight][img-hbase-shell]
4. Ottenere una singola riga
   
    ```hbaseshell
    get 'Contacts', '1000'
    ```
   
    Hello stesso risultati verrà visualizzato come tramite comando analisi hello perché è presente solo una riga.
   
    Per ulteriori informazioni sullo schema di tabella HBase hello, vedere [tooHBase introduzione progettazione Schema][hbase-schema]. Per altri comandi HBase, vedere la [guida di riferimento di Apache HBase][hbase-quick-start].
5. Uscire dalla shell hello
   
    ```hbaseshell
    exit
    ```

**toobulk caricare i dati nella tabella HBase di hello contatti**

HBase include diversi metodi di caricamento dei dati nelle tabelle.  Per altre informazioni, vedere [Caricamento bulk](http://hbase.apache.org/book.html#arch.bulk.load).

Un file di dati di esempio è disponibile in un contenitore BLOB pubblico, *wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt*.  è contenuto Hello hello del file di dati:

    8396    Calvin Raji      230-555-0191    230-555-0191    5415 San Gabriel Dr.
    16600   Karen Wu         646-555-0113    230-555-0192    9265 La Paz
    4324    Karl Xie         508-555-0163    230-555-0193    4912 La Vuelta
    16891   Jonn Jackson     674-555-0110    230-555-0194    40 Ellis St.
    3273    Miguel Miller    397-555-0155    230-555-0195    6696 Anchor Drive
    3588    Osa Agbonile     592-555-0152    230-555-0196    1873 Lion Circle
    10272   Julia Lee        870-555-0110    230-555-0197    3148 Rose Street
    4868    Jose Hayes       599-555-0171    230-555-0198    793 Crawford Street
    4761    Caleb Alexander  670-555-0141    230-555-0199    4775 Kentucky Dr.
    16443   Terry Chander    998-555-0171    230-555-0200    771 Northridge Drive

Facoltativamente, è possibile creare un file di testo e caricare l'account di archiviazione propria tooyour file hello. Per istruzioni hello, vedere [caricare dati per i processi di Hadoop in HDInsight][hdinsight-upload-data].

> [!NOTE]
> Questa procedura utilizza una tabella HBase contatti hello creata nell'ultima procedura hello.
> 

1. SSH, eseguire hello successivo comando tootransform hello tooStoreFiles del file di dati e archiviano in un percorso relativo specificato da Dimporttsv.bulk.output.  Se si utilizza la Shell di HBase, utilizzare hello uscita comando tooexit.

    ```bash   
    hbase org.apache.hadoop.hbase.mapreduce.ImportTsv -Dimporttsv.columns="HBASE_ROW_KEY,Personal:Name,Personal:Phone,Office:Phone,Office:Address" -Dimporttsv.bulk.output="/example/data/storeDataFileOutput" Contacts wasb://hbasecontacts@hditutorialdata.blob.core.windows.net/contacts.txt
    ```

2. Eseguire i seguenti dati di comando tooupload hello dalla tabella di HBase toohello /example/data/storeDataFileOutput hello:
   
    ```bash
    hbase org.apache.hadoop.hbase.mapreduce.LoadIncrementalHFiles /example/data/storeDataFileOutput Contacts
    ```

3. È possibile aprire la shell di HBase hello e utilizzare il contenuto delle tabelle hello hello analisi comando toolist.

## <a name="use-hive-tooquery-hbase"></a>Usare l'Hive tooquery HBase

È possibile eseguire query sui dati nelle tabelle HBase tramite Hive. In questa sezione si crea una tabella Hive che esegue il mapping di tabella HBase toohello e lo Usa dati hello tooquery nella tabella HBase.

1. Aprire **PuTTY**e connettersi toohello cluster.  Vedere le istruzioni di hello nella procedura precedente hello.
2. Dalla sessione SSH hello, utilizzare hello comando toostart Beeline seguenti:

    ```bash
    beeline -u 'jdbc:hive2://localhost:10001/;transportMode=http' -n admin
    ```

    Per altre informazioni su Beeline, vedere [Usare Hive con Hadoop in HDInsight con Beeline](hdinsight-hadoop-use-hive-beeline.md).
       
3. Eseguire hello toocreate script HiveQL seguente una tabella Hive che esegue il mapping di tabella HBase toohello. Assicurarsi di aver creato una tabella di esempio hello a cui fa riferimento in precedenza in questa esercitazione utilizzando la shell di HBase hello prima di eseguire questa istruzione.

    ```hiveql   
    CREATE EXTERNAL TABLE hbasecontacts(rowkey STRING, name STRING, homephone STRING, officephone STRING, officeaddress STRING)
    STORED BY 'org.apache.hadoop.hive.hbase.HBaseStorageHandler'
    WITH SERDEPROPERTIES ('hbase.columns.mapping' = ':key,Personal:Name,Personal:Phone,Office:Phone,Office:Address')
    TBLPROPERTIES ('hbase.table.name' = 'Contacts');
    ```

4. Eseguire hello HiveQL script tooquery hello dati nella tabella HBase hello seguenti:

    ```hiveql   
    SELECT count(rowkey) FROM hbasecontacts;
    ```

## <a name="use-hbase-rest-apis-using-curl"></a>Usare le API REST HBase mediante Curl

Hello API REST è protetto tramite [l'autenticazione di base](http://en.wikipedia.org/wiki/Basic_access_authentication). È sempre deve effettuare richieste tramite HTTPS (Secure HTTP) toohelp assicurarsi che le credenziali vengono inviate in modo sicuro toohello server.

2. Utilizzare hello comando toolist hello HBase le tabelle esistenti seguenti:

    ```bash
    curl -u <UserName>:<Password> \
    -G https://<ClusterName>.azurehdinsight.net/hbaserest/
    ```

3. Utilizzare hello comando toocreate una nuova tabella HBase con gruppi di due colonne seguenti:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/schema" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"@name\":\"Contact1\",\"ColumnSchema\":[{\"name\":\"Personal\"},{\"name\":\"Office\"}]}" \
    -v
    ```

    schema Hello viene fornito in formato JSon hello.
4. Utilizzare hello comando che segue tooinsert alcuni dati:

    ```bash   
    curl -u <UserName>:<Password> \
    -X PUT "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/false-row-key" \
    -H "Accept: application/json" \
    -H "Content-Type: application/json" \
    -d "{\"Row\":[{\"key\":\"MTAwMA==\",\"Cell\": [{\"column\":\"UGVyc29uYWw6TmFtZQ==\", \"$\":\"Sm9obiBEb2xl\"}]}]}" \
    -v
    ```
   
    È necessario base64 codificare i valori hello specificati nell'opzione -d hello. Nell'esempio hello:
   
   * MTAwMA==: 1000
   * UGVyc29uYWw6TmFtZQ==: Personal:Name
   * Sm9obiBEb2xl: John Dole
     
     [chiave di riga false](https://hbase.apache.org/apidocs/org/apache/hadoop/hbase/rest/package-summary.html#operation_cell_store_single) tooinsert consente più valori (batch).
5. Utilizzare hello tooget comando una riga seguente:
   
    ```bash 
    curl -u <UserName>:<Password> \
    -X GET "https://<ClusterName>.azurehdinsight.net/hbaserest/Contacts1/1000" \
    -H "Accept: application/json" \
    -v
    ```

Per altre informazioni sulle API REST HBase, vedere la [Apache HBase Reference Guide](https://hbase.apache.org/book.html#_rest)(Guida di riferimento di Apache HBase).

> [!NOTE]
> Thrift non è supportato da HBase in HDInsight.
>
> Quando si utilizza Curl o qualsiasi altra comunicazione REST con WebHCat, è necessario autenticare le richieste di hello specificando nome utente hello e la password per l'amministratore del cluster HDInsight hello. Inoltre, è necessario utilizzare il nome del cluster hello come parte di hello Uniform Resource Identifier (URI) utilizzato toosend hello richieste toohello server:
> 
>   
>        curl -u <UserName>:<Password> \
>        -G https://<ClusterName>.azurehdinsight.net/templeton/v1/status
>   
>    Si dovrebbe ricevere un toohello simile di risposta seguente risposta:
>   
>        {"status":"ok","version":"v1"}
   


## <a name="check-cluster-status"></a>Controllare lo stato del cluster
HBase in HDInsight viene fornito con un'interfaccia utente Web per il monitoraggio dei cluster. Utilizza hello dell'interfaccia utente Web, è possibile richiedere informazioni sulle aree o le statistiche.

**hello tooaccess UI Master HBase**

1. Sign in hello hello dell'interfaccia utente Web Ambari in https://&lt;Clustername >. cluster>.azurehdinsight.NET.
2. Fare clic su **HBase** dal menu a sinistra di hello.
3. Fare clic su **collegamenti rapidi** nella parte superiore della pagina hello toohello punto attivo Zookeeper nodo collegamento, hello e quindi fare clic su **HBase Master UI**.  Hello dell'interfaccia utente viene aperto in un'altra scheda del browser:

  ![Interfaccia utente master HBase di HDInsight](./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hmaster-ui.png)

  Hello UI HBase Master contiene hello le sezioni seguenti:

  - server di zona
  - master di backup
  - tables
  - attività
  - attributi di software

## <a name="delete-hello-cluster"></a>Eliminare il cluster hello
tooavoid incoerenze, è consigliabile disabilitare le tabelle di hello HBase prima di eliminare il cluster hello.

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a>Risoluzione dei problemi

Se si verificano problemi di creazione dei cluster HDInsight, vedere i [requisiti dei controlli di accesso](hdinsight-administer-use-portal-linux.md#create-clusters).

## <a name="next-steps"></a>Passaggi successivi
In questo articolo è stato illustrato come un cluster HBase toocreate e come visualizzare e tabelle toocreate hello dati in tali tabelle da hello shell di HBase. È stato inoltre descritto come toouse un Hive eseguire query sui dati in HBase tabelle e come toouse hello toocreate HBase in c# le API REST di una tabella HBase e recuperare dati dalla tabella di hello.

toolearn informazioni, vedere:

* [Panoramica di HDInsight HBase][hdinsight-hbase-overview]: HBase è un database NoSQL open source Apache basato su Hadoop che fornisce un accesso casuale e coerenza assoluta a grandi quantità di dati non strutturati e semistrutturati.

[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hbase-reference]: http://hbase.apache.org/book.html#importtsv
[hbase-schema]: http://0b4af6cdc2f0c5998459-c0245c5c937c5dedcca3f1764ecc9b2f.r43.cf2.rackcdn.com/9353-login1210_khurana.pdf
[hbase-quick-start]: http://hbase.apache.org/book.html#quickstart





[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-versions]: hdinsight-component-versioning.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md
[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/
[azure-portal]: https://portal.azure.com/
[azure-create-storageaccount]: http://azure.microsoft.com/documentation/articles/storage-create-storage-account/

[img-hdinsight-hbase-cluster-quick-create]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-quick-create.png
[img-hdinsight-hbase-hive-editor]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-hive-editor.png
[img-hdinsight-hbase-file-browser]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-file-browser.png
[img-hbase-shell]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-shell.png
[img-hbase-sample-data-tabular]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-tabular.png
[img-hbase-sample-data-bigtable]: ./media/hdinsight-hbase-tutorial-get-started-linux/hdinsight-hbase-contacts-bigtable.png
