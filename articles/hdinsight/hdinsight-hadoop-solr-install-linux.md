---
title: aaaUse genera Script azione tooinstall Solr in HDInsight basati su Linux - Azure | Documenti Microsoft
description: Informazioni su come i cluster usando le azioni Script tooinstall Solr in HDInsight Hadoop basati su Linux.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a>Installare e usare Solr nei cluster Hadoop di HDInsight

Informazioni su come tooinstall Solr in Azure HDInsight utilizzando l'azione di Script. Solr è una piattaforma di ricerca avanzata e offre funzionalità di ricerca di livello aziendale per i dati gestiti da Hadoop.

> [!IMPORTANT]
    > passaggi di Hello in questo documento richiedono un cluster HDInsight che utilizza Linux. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

> [!IMPORTANT]
> script di esempio Hello utilizzato in questo documento viene installato 4.9 Solr con una configurazione specifica. Se si desidera che tooconfigure hello Solr cluster con raccolte diverse, le partizioni, schemi, le repliche, e così via, è necessario modificare script hello e file binari di Solr.

## <a name="whatis"></a>Che cos'è Solr

[Apache Solr](http://lucene.apache.org/solr/features.html) è una piattaforma di ricerca aziendale che permette di eseguire ricerche full-text avanzate sui dati. Mentre Hadoop consente di archiviare e gestire grandi quantità di dati, Solr Apache fornisce funzionalità di ricerca di hello tooquickly recuperare i dati hello.

> [!WARNING]
> I componenti forniti con i cluster di HDInsight hello sono completamente supportati da Microsoft.
>
> I componenti personalizzati, ad esempio Solr, ricevano supporto commercialmente ragionevole toohelp toofurther per risolvere il problema di hello. Supporto tecnico Microsoft potrebbe non essere in grado di tooresolve problemi con componenti personalizzati. Community di origine aprire hello tooengage potrebbe essere necessario per ottenere assistenza. È ad esempio possibile ricorrere a molti siti di community, come il [forum MSDN per HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight) o [http://stackoverflow.com](http://stackoverflow.com). Anche per i progetti Apache sono disponibili siti specifici in [http://apache.org](http://apache.org), ad esempio [Hadoop](http://hadoop.apache.org/).

## <a name="what-hello-script-does"></a>Quali script hello esegue

Questo script esegue hello cluster di HDInsight toohello le modifiche seguenti:

* Installa Solr 4.9 in `/usr/hdp/current/solr`
* Crea un utente, **solrusr**, ovvero hello toorun utilizzati Solr servizio
* Set **solruser** come proprietario di hello di`/usr/hdp/current/solr`
* Aggiunge una configurazione [Upstart](http://upstart.ubuntu.com/) che avvia automaticamente Solr.

## <a name="install"></a>Installare R mediante azioni script

Un tooinstall di script di esempio Solr in un cluster HDInsight è disponibile in hello seguente posizione:

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

toocreate un cluster con Solr installato, utilizzare hello passaggi hello [cluster HDInsight creare](hdinsight-hadoop-create-linux-clusters-portal.md) documento. Durante il processo di creazione di hello, utilizzare hello seguendo i passaggi tooinstall Solr:

1. Da hello __riepilogo Cluster__ blade, settings__ select__Advanced, __Script azioni__. Utilizzare hello modulo hello toopopulate di informazioni seguenti:

   * **NOME**: immettere un nome descrittivo per l'azione script hello.
   * **URI SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh
   * **HEAD**: selezionare questa opzione
   * **RUOLO DI LAVORO**: selezionare questa opzione
   * **ZOOKEEPER**: selezionare questa opzione tooinstall nel nodo Zookeeper hello
   * **PARAMETRI**: lasciare questo campo vuoto

2. Nella parte inferiore di hello di hello **Script azioni** blade, utilizzare hello **selezionare** configurazione hello toosave dei pulsanti. Infine, utilizzare hello **Avanti** pulsante tooreturn toohello __riepilogo di Cluster__

3. Da hello __riepilogo Cluster__ selezionare __crea__ cluster hello toocreate.

## <a name="usesolr"></a>Come si usa Solr in HDInsight

> [!IMPORTANT]
> passaggi di Hello in questa sezione illustrano le funzionalità di base Solr. Per ulteriori informazioni sull'utilizzo di Solr, vedere hello [Solr Apache sito](http://lucene.apache.org/solr/).

### <a name="index-data"></a>Dati dell'indice

Utilizzare i seguenti passaggi tooadd esempio dati tooSolr hello e quindi eseguire una query:

1. Connettere il cluster di HDInsight toohello tramite SSH:

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

     > [!IMPORTANT]
     > Passaggi più avanti in questo documento usano un SSL tunnel tooconnect toohello Solr interfaccia utente web. toouse questi passaggi, è necessario stabilire un SSL tunnel e quindi configurare toouse il browser è.
     >
     > Per ulteriori informazioni, vedere hello [usare SSH Tunneling con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

2. Utilizzare hello dati di esempio dell'indice Solr toohave i comandi seguenti:

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    Hello output seguente viene restituito toohello console:

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    Hello `post.jar` utilità aggiunge hello **solr.xml** e **monitor.xml** indice toohello documenti.
  
3. Utilizzare hello comando tooquery hello Solr REST API seguenti:

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    Questo comando Cerca **collection1** per tutti i documenti corrispondenti  **\*:\***  (codificato come \*% 3A\* nella stringa di query hello). Hello seguente documento JSON è un esempio di risposta hello:

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-hello-solr-dashboard"></a>Tramite il dashboard di Solr hello

dashboard Solr Hello è un'interfaccia utente che consente di toowork con Solr attraverso il web browser web. dashboard Solr Hello non è esposta direttamente su Internet di hello dal cluster HDInsight. È possibile utilizzare un tooaccess tunnel SSH è. Per ulteriori informazioni sull'utilizzo di un tunnel SSH, vedere hello [usare SSH Tunneling con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.

Dopo aver stabilito un tunnel SSH, utilizzare hello dashboard Solr hello toouse di passaggi seguente:

1. Determinare il nome host hello per nodo head primario hello:

   1. Usare SSH tooconnect toohello nodo head del cluster. ad esempio `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.

       Per ulteriori informazioni sull'utilizzo di SSH, vedere hello [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

   2. Utilizzare hello comando tooget hello nome host completo seguente:

        ```bash
        hostname -f
        ```

        Questo comando restituisce un toohello simile valore dopo il nome host:

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        Salvare il valore di hello restituito, perché è usato in un secondo momento.

2. Nel browser, connettersi troppo**http://HOSTNAME:8983/solr / #/**, dove **HOSTNAME** nome hello è determinato nei passaggi precedenti hello.

    Hello richiesta è instradata tramite hello SSH tunnel toohello Solr interfaccia utente web sul cluster. verrà visualizzata la pagina di Hello simile toohello seguente immagine:

    ![Immagine del dashboard di Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. Nel riquadro di sinistra hello, utilizzare hello **selettore Core** elenco a discesa tooselect **collection1**. Sotto **collection1** dovrebbero essere visualizzate diverse voci.

4. Le voci di hello seguente **collection1**selezionare **Query**. Utilizzare hello seguente pagina di ricerca di valori toopopulate hello:

   * In hello **q** testo immettere  **\*:**\*. Questa query restituisce tutti i documenti indicizzati hello in Solr. Se si desidera toosearch una stringa specifica all'interno dei documenti hello, è possibile immettere qui la stringa.
   * In hello **wt** casella di testo, il formato di output di hello selezionare. Il valore predefinito è **json**.

     Infine, selezionare hello **Esegui Query** pulsante nella parte inferiore di hello del pate ricerca hello.

     ![Utilizzare l'azione Script toocustomize un cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     output di Hello restituisce hello due documenti aggiunti toohello indicizzare in precedenza. l'output è simile toohello seguente documento JSON Hello:

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a>Avviare e arrestare Solr

Utilizzare i seguenti comandi toomanually arrestare e avviare Solr hello:

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a>Eseguire il backup dei dati indicizzati

Utilizzare hello seguendo i passaggi tooback backup Solr dati toohello spazio di archiviazione predefinito per il cluster:

1. Connettere il cluster toohello tramite SSH, quindi utilizzare hello dopo il nome di comando tooget hello host per il nodo head hello:

    ```bash
    hostname -f
    ```

2. Utilizzare hello successivo comando toocreate uno snapshot dei dati indicizzato hello. Sostituire **HOSTNAME** con nome hello restituito dal comando precedente hello:

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    risposta Hello è simile toohello XML seguente:

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. Passare alla directory troppo`/usr/hdp/current/solr/example/solr`. Per ogni raccolta è presente una sottodirectory. Ogni raccolta di directory contiene un `data` directory che contiene snapshot hello per la raccolta di hello.

4. toocreate un archivio compresso della cartella snapshot hello, utilizzare hello comando seguente:

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    Sostituire hello `snapshot.20150806185338855` valori con nome hello dello snapshot hello per la raccolta.

    Questo comando crea un archivio denominato **snapshot.20150806185338855.tgz**, che contiene il contenuto di hello di hello **snapshot.20150806185338855** directory.

5. È quindi possibile archiviare archiviazione primaria di hello archivio toohello cluster utilizzando hello comando seguente:

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

Per altre informazioni sulle operazioni di backup e ripristino di Solr, vedere [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).

## <a name="next-steps"></a>Passaggi successivi

* [Installare Giraph in cluster HDInsight](hdinsight-hadoop-giraph-install-linux.md). Utilizzare cluster personalizzazione tooinstall che cluster Giraph in HDInsight Hadoop. Giraph consente grafico tooperform elaborazione tramite Hadoop e può essere utilizzato con Azure HDInsight.

* [Installare Hue nei cluster HDInsight](hdinsight-hadoop-hue-linux.md). Utilizzare cluster personalizzazione tooinstall tonalità nei cluster HDInsight Hadoop. La tonalità corrisponde che toointeract utilizzato da un set di applicazioni Web con un cluster Hadoop.

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
