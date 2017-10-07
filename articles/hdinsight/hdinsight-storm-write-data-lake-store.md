---
title: aaaApache Storm scrivere tooStorage/Data Lake Store - HDInsight di Azure | Documenti Microsoft
description: "Informazioni su come toouse hello archiviazione toohello HDFS compatibile di Apache Storm toowrite per HDInsight. Archiviazione Azure o archivio Azure Data Lake fornire archiviazione hello HDFS comptabile per HDInsight. Questo documento e hello associato esempio illustrano come componente HdfsBolt hello può essere utilizzati toowrite toohello predefinito archiviazione di un elevato numero di cluster HDInsight."
services: hdinsight
documentationcenter: na
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 1df98653-a6c8-4662-a8c6-5d288fc4f3a6
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: d76159a9ecd1be18e519511cfdb3bcfd18ae4d33
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="write-toohdfs-from-apache-storm-on-hdinsight"></a>Scrivere tooHDFS da Apache Storm in HDInsight

Informazioni sull'utilizzo toouse Storm toowrite dati toohello archiviazione HDFS compatibile da Apache Storm in HDInsight. HDInsight può usare sia Archiviazione di Azure che Azure Data Lake Store come archivio compatibile con HDFS. Storm fornisce un [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) componente che scrive dati tooHDFS. Questo documento vengono fornite informazioni sulla scrittura di tipo tooeither di archiviazione da hello HdfsBolt. 

> [!IMPORTANT]
> esempio Hello topologia utilizzata in questo documento si basa sui componenti inclusi in Storm in HDInsight. Potrebbe essere necessario toowork modifica con l'archivio Azure Data Lake se utilizzato con altri cluster Apache Storm.

## <a name="get-hello-code"></a>Ottenere il codice hello

è disponibile come download dal progetto Hello contenente questa topologia [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store).

toocompile questo progetto, è necessario hello seguente configurazione per l'ambiente di sviluppo:

* [Java JDK 1.8](https://www.oracle.com/technetwork/java/javase/downloads/jdk7-downloads-1880260.html) o versione successiva. Per HDInsight 3.5 o una versione successiva è necessario Java 8.

* [Maven 3.x](https://maven.apache.org/download.cgi)

Hello seguenti variabili di ambiente possono essere impostate durante l'installazione di Java e hello JDK nella workstation di sviluppo. Tuttavia, è necessario verificare che esistano e che contengono i valori corretti di hello per il sistema.

* `JAVA_HOME`-deve puntare toohello directory in cui hello JDK è installato.
* `PATH`-deve contenere hello seguenti percorsi:
  
    * `JAVA_HOME`(o percorso equivalente hello).
    * `JAVA_HOME\bin`(o percorso equivalente hello).
    * directory di Hello in cui è installato Maven.

## <a name="how-toouse-hello-hdfsbolt-with-hdinsight"></a>Come toouse hello HdfsBolt con HDInsight

> [!IMPORTANT]
> Prima di utilizzare hello HdfsBolt con Storm in HDInsight, è innanzitutto necessario utilizzare un file jar di script azione toocopy necessarie in hello `extpath` per Storm. Per ulteriori informazioni, vedere hello [cluster hello configura](#configure) sezione.

Hello HdfsBolt utilizza lo schema di file hello fornire toounderstand modalità toowrite tooHDFS. Con HDInsight, utilizzare uno dei seguenti schemi hello:

* `wasb://`: usato con l'account di archiviazione di Azure.
* `adl://`: usato con Azure Data Lake Store.

Hello nella tabella seguente vengono forniti esempi dell'utilizzo dello schema di file hello per scenari diversi:

| Schema | Note |
| ----- | ----- |
| `wasb:///` | account di archiviazione predefinito Hello è un contenitore blob in un account di archiviazione di Azure |
| `adl:///` | account di archiviazione predefinito Hello è una directory nell'archivio Azure Data Lake. Durante la creazione del cluster, specificare la directory hello in archivio Data Lake che sarà radice hello HDFS del cluster hello. Ad esempio, hello `/clusters/myclustername/` directory. |
| `wasb://CONTAINER@ACCOUNT.blob.core.windows.net/` | Un account di archiviazione di Azure (aggiuntive) non predefinito associato hello cluster. |
| `adl://STORENAME/` | radice Hello hello archivio Data Lake usati dal cluster hello. Questo schema consente tooaccess dati che si trovano all'esterno della directory contenente il sistema di hello cluster file hello. |

Per ulteriori informazioni, vedere hello [HdfsBolt](http://storm.apache.org/releases/1.1.0/javadocs/org/apache/storm/hdfs/bolt/HdfsBolt.html) riferimento all'indirizzo Apache.org.

### <a name="example-configuration"></a>Configurazione di esempio

YAML seguente Hello è un estratto dal hello `resources/writetohdfs.yaml` file incluso nell'esempio hello. Questo file definisce topologia Storm hello utilizzando hello [flusso](https://storm.apache.org/releases/1.1.0/flux.html) framework per Apache Storm.

```yaml
components:
  - id: "syncPolicy"
    className: "org.apache.storm.hdfs.bolt.sync.CountSyncPolicy"
    constructorArgs:
      - 1000

  - id: "rotationPolicy"
    className: "org.apache.storm.hdfs.bolt.rotation.NoRotationPolicy"

  - id: "fileNameFormat"
    className: "org.apache.storm.hdfs.bolt.format.DefaultFileNameFormat"
    configMethods:
      - name: "withPath"
        args: ["${hdfs.write.dir}"]
      - name: "withExtension"
        args: [".txt"]

  - id: "recordFormat"
    className: "org.apache.storm.hdfs.bolt.format.DelimitedRecordFormat"
    configMethods:
      - name: "withFieldDelimiter"
        args: ["|"]

# spout definitions
spouts:
  - id: "tick-spout"
    className: "com.microsoft.example.TickSpout"
    parallelism: 1


# bolt definitions
bolts:
  - id: "hdfs-bolt"
    className: "org.apache.storm.hdfs.bolt.HdfsBolt"
    configMethods:
      - name: "withConfigKey"
        args: ["hdfs.config"]
      - name: "withFsUrl"
        args: ["${hdfs.url}"]
      - name: "withFileNameFormat"
        args: [ref: "fileNameFormat"]
      - name: "withRecordFormat"
        args: [ref: "recordFormat"]
      - name: "withRotationPolicy"
        args: [ref: "rotationPolicy"]
      - name: "withSyncPolicy"
        args: [ref: "syncPolicy"]
```

Questo YAML definisce hello seguenti elementi:

* `syncPolicy`: Definisce quando i file vengono sincronizzati scaricati toohello sistema di file. In questo esempio, ogni 1000 tuple.
* `fileNameFormat`: Definisce hello percorso e il nome modello toouse durante la scrittura di file. In questo esempio viene specificato un percorso di hello in fase di esecuzione utilizzando un filtro e l'estensione del file hello è `.txt`.
* `recordFormat`: Definisce formato interno di hello del file hello scritti. In questo esempio, i campi delimitati hello `|` carattere.
* `rotationPolicy`: Definisce quando toorotate file. In questo esempio, non viene eseguita alcuna rotazione.
* `hdfs-bolt`: Usa hello componenti precedenti come parametri di configurazione per hello `HdfsBolt` classe.

Per ulteriori informazioni sul framework luminoso hello, vedere [https://storm.apache.org/releases/1.1.0/flux.html](https://storm.apache.org/releases/1.1.0/flux.html).

## <a name="configure-hello-cluster"></a>Configurare il cluster hello

Per impostazione predefinita, Storm in HDInsight non include componenti hello HdfsBolt utilizza toocommunicate con archiviazione di Azure o archivio Data Lake in classpath elevato del numero. Azione tooadd lo script seguente hello utilizzare toohello questi componenti `extlib` directory per Storm sul cluster:

| Script URI | Nodi tooapply a | I parametri | | `https://000aarperiscus.blob.core.windows.net/certs/stormextlib.sh` | Nimbus, Supervisore | None |

Per informazioni sull'uso di questo script con il cluster, vedere hello [HDInsight personalizzare cluster tramite le azioni script](./hdinsight-hadoop-customize-cluster-linux.md) documento.

## <a name="build-and-package-hello-topology"></a>Compilare e assemblare topologia hello

1. Scaricare il progetto di esempio hello da [https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store ](https://github.com/Azure-Samples/hdinsight-storm-azure-data-lake-store) tooyour ambiente di sviluppo.

2. Da un prompt dei comandi, terminale o una sessione della shell, modifica directory toohello radice hello scaricato progetto. toobuild e pacchetto hello topologia, usare hello comando seguente:
   
        mvn compile package
   
    Una volta completata la compilazione di hello e dei pacchetti, è una nuova directory denominata `target`, che contiene un file denominato `StormToHdfs-1.0-SNAPSHOT.jar`. Questo file contiene la topologia hello compilato.

## <a name="deploy-and-run-hello-topology"></a>Distribuire ed eseguire topologia hello

1. Utilizzare hello seguendo il cluster di HDInsight toohello comando toocopy hello topologia. Sostituire **utente** con nome utente di hello SSH utilizzato per la creazione di cluster hello. Sostituire **CLUSTERNAME** con nome hello del cluster di hello.
   
        scp target\StormToHdfs-1.0-SNAPSHOT.jar USER@CLUSTERNAME-ssh.azurehdinsight.net:StormToHdfs1.0-SNAPSHOT.jar
   
    Quando richiesto, immettere la password di hello utilizzati durante la creazione utente SSH hello per cluster hello. Se si utilizza una chiave pubblica anziché una password, potrebbe essere necessario hello toouse `-i` parametro toospecify hello percorso toohello corrispondente chiave privata.
   
   > [!NOTE]
   > Per altre informazioni sull'uso di `scp` con HDInsight, vedere [Use SSH with HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md) (Uso di SSH con HDInsight).

2. Una volta completato il caricamento di hello, utilizzare hello dopo i cluster di HDInsight toohello tooconnect tramite SSH. Sostituire **utente** con nome utente di hello SSH utilizzato per la creazione di cluster hello. Sostituire **CLUSTERNAME** con nome hello del cluster di hello.
   
        ssh USER@CLUSTERNAME-ssh.azurehdinsight.net
   
    Quando richiesto, immettere la password di hello utilizzati durante la creazione utente SSH hello per cluster hello. Se si utilizza una chiave pubblica anziché una password, potrebbe essere necessario hello toouse `-i` parametro toospecify hello percorso toohello corrispondente chiave privata.
   
   Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

3. Una volta connessi, utilizzare hello comando che segue toocreate un file denominato `dev.properties`:

        nano dev.properties

4. Hello utilizzo successivo di testo come contenuto di hello di hello `dev.properties` file:

        hdfs.write.dir: /stormdata/
        hdfs.url: wasb:///

    > [!IMPORTANT]
    > Questo esempio si presuppone che il cluster utilizza un account di archiviazione di Azure come spazio di archiviazione predefinito hello. Se il cluster usa Azure Data Lake Store, usare invece `hdfs.url: adl:///`.
    
    file hello toosave, usare __Ctrl + X__, quindi __Y__e infine __invio__. valori Hello in questo file impostare l'URL dell'archivio Data Lake hello e nome della directory hello che vengono scritti dati.

3. Utilizzare hello topologia hello toostart di comando seguente:
   
        storm jar StormToHdfs-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writetohdfs.yaml --filter dev.properties

    Questo comando avvia una topologia di hello con framework luminoso hello inviandolo nodo Nimbus toohello del cluster di hello. topologia Hello è definita da hello `writetohdfs.yaml` file incluso nel file jar hello. Hello `dev.properties` file viene passato come un filtro e vengono letti i valori hello contenuti nel file hello dalla topologia hello.

## <a name="view-output-data"></a>Visualizzare i dati di output

dati hello tooview, utilizzare hello comando seguente:

    hdfs dfs -ls /stormdata/

Viene visualizzato un elenco dei file hello creati da questa topologia.

Hello elenco riportato di seguito è riportato un esempio di dati hello restituiti dai comandi precedenti hello:

    Found 30 items
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-0-1488568403092.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-1-1488568404567.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-10-1488568408678.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-11-1488568411636.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-12-1488568411884.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-13-1488568412603.txt
    -rw-r-----+  1 sshuser sshuser       5120 2017-03-03 19:13 /stormdata/hdfs-bolt-3-14-1488568415055.txt

## <a name="stop-hello-topology"></a>Arrestare la topologia hello

Topologie di Storm eseguire finché non viene interrotto o hello cluster verrà eliminato. toostop hello topologia, usare hello comando seguente:

    storm kill hdfswriter

## <a name="delete-your-cluster"></a>Eliminare il cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come toouse Storm toowrite tooAzure archiviazione e l'archivio Azure Data Lake, individuare altri [Storm esempi per HDInsight](hdinsight-storm-example-topology.md).

