---
title: eventi aaaProcess dagli hub eventi con Storm in HDInsight mediante Java | Documenti Microsoft
description: Informazioni su come creare i dati di hub eventi con una topologia di Java Storm tooprocess con Maven.
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 453fa7b0-c8a6-413e-8747-3ac3b71bed86
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/13/2017
ms.author: larryfr
ms.openlocfilehash: 6506f5bc8f6ab0e29350c071a3f84433382038e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-java"></a>Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)

Informazioni su come toouse hub di eventi di Azure con Storm in HDInsight. In questo esempio utilizza i componenti basati su Java tooread e scrittura dati in hub eventi di Azure.

Hub eventi di Azure consente tooprocess enormi quantità di dati da siti Web, applicazioni e dispositivi. Hello beccuccio Hub eventi rende facile toouse Apache Storm in HDInsight tooanalyze questi dati in tempo reale. È anche possibile scrivere dati tooEvent hub dal Storm utilizzando hello bullone hub eventi.

## <a name="prerequisites"></a>Prerequisiti

* Un cluster Apache Storm in HDInsight versione 3.6. Per altre informazioni, vedere [Introduzione a Storm in un cluster HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md).

    > [!IMPORTANT]
    > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* Un [Hub eventi di Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* [Oracle Java Developer Kit (JDK) versione 8](http://www.oracle.com/technetwork/java/javase/downloads/index.html) o equivalente, ad esempio [OpenJDK](http://openjdk.java.net/).

* [Maven](https://maven.apache.org/download.cgi): Maven è un sistema di compilazione per progetti Java.

* Un editor di testo o un IDE (Integrated Development Environment).

    > [!NOTE]
    > È possibile che l'editor di testo o l'ambiente IDE offra funzionalità specifiche per l'uso di Maven non descritte in questo documento. Per informazioni sulle funzionalità di hello dell'ambiente di modifica, vedere la documentazione di hello per prodotto hello in uso.

    * Un client SSH. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* Hello `ssh` e `scp` comandi. Questi sono i cluster di HDInsight toohello file toocopy utilizzato. In Windows, è possibile ottenerli con Bash in Windows 10.

## <a name="understanding-hello-example"></a>Esempio hello comprensione

Hello [eventhub hdinsight-java-storm](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub) esempio contiene due topologie:

Hello `resources/writer.yaml` topologia scrive dati casuali tooan Hub di eventi di Azure. dati Hello sono generati da hello `DeviceSpout` componente, ed è un ID dispositivo casuale e il valore del dispositivo. Simula quindi un dispositivo hardware che genera un ID stringa e un valore numerico.

Tre `resources/reader.yaml` topologia legge i dati provenienti dall'Hub di eventi (dati hello scritti da EventHubWriter,) analizza i dati JSON hello e quindi Registra hello `deviceId` e `deviceValue` dati.

dati Hello sono formattati come un documento JSON prima che venga scritto tooEvent Hub e durante la lettura dal lettore hello viene analizzata da JSON e in tuple. il formato JSON Hello è come segue:

    { "deviceId": "unique identifier", "deviceValue": some value }

### <a name="project-configuration"></a>Configurazione del progetto

Hello `POM.xml` file contiene informazioni di configurazione per il progetto di Maven. GetStringLayout Hello sono:

#### <a name="event-hub-components"></a>Componenti di Hub eventi

componente Hello che legge e scrive gli hub di eventi tooAzure si trova nella hello [HDInsight repository](https://github.com/hdinsight/mvn-rep). Hello seguenti sezioni in hello `POM.xml` carico hello componenti del file di questo repository

```xml
<repositories>
    <repository>
        <id>hdinsight-examples</id>
        <url>http://raw.github.com/hdinsight/mvn-repo/master</url>
    </repository>
</repositories>
```

#### <a name="hello-eventhubs-storm-spout-dependency"></a>Hello EventHubs Storm Spout dipendenza

```xml
<dependency>
    <groupId>com.microsoft</groupId>
    <artifactId>eventhubs</artifactId>
    <version>${storm.eventhub.version}</version>
</dependency>
```

Questo codice xml definisce una dipendenza per il pacchetto eventhubs hello, che contiene un beccuccio per la lettura dagli hub eventi e un fulmine per la scrittura di tooit.

```xml
</source>
    <target>1.8</target>
    </configuration>
</plugin>
```

Questo codice xml consente di configurare output di hello progetto toogenerate per Java 8, viene utilizzato da HDInsight 3.5 o versioni successive.

#### <a name="hello-maven-shade-plugin"></a>Hello maven-sfumatura-plug-in

```xml
<!-- build an uber jar -->
<plugin>
<groupId>org.apache.maven.plugins</groupId>
<artifactId>maven-shade-plugin</artifactId>
<version>2.3</version>
<configuration>
    <transformers>
    <!-- Keep us from getting a can't overwrite file error -->
    <transformer implementation="org.apache.maven.plugins.shade.resource.ApacheLicenseResourceTransformer"/>
    <transformer implementation="org.apache.maven.plugins.shade.resource.ServicesResourceTransformer"/>
    </transformers>
    <!-- Keep us from getting a bad signature error -->
    <filters>
    <filter>
        <artifact>*:*</artifact>
        <excludes>
            <exclude>META-INF/*.SF</exclude>
            <exclude>META-INF/*.DSA</exclude>
            <exclude>META-INF/*.RSA</exclude>
        </excludes>
    </filter>
    </filters>
</configuration>
<executions>
    <execution>
    <phase>package</phase>
    <goals>
        <goal>shade</goal>
    </goals>
    </execution>
</executions>
</plugin>
```

Questo codice xml consente di configurare output di hello toopackage soluzione hello in un file jar uber. file jar Hello contiene sia il codice di progetto hello dipendenze richieste. Viene usato anche per:

* Rinominare i file di licenza per le dipendenze di hello.
* Escludere sicurezza/firme.
* Verificare che più implementazioni di hello stessa interfaccia vengono uniti in una sola voce.

Queste impostazioni di configurazione impediscono il verificarsi di errori in fase di runtime.

#### <a name="topology-definitions"></a>Definizioni di topologia

Questo esempio viene utilizzato hello [flusso](https://storm.apache.org/releases/1.1.0/flux.html) framework. Il framework utilizza le topologie di hello toodefine YAML. Il vantaggio principale di Hello è che non si è rigido topologia hello nel codice di linguaggio di codifica. Poiché è una definizione di hello YAML, è possibile modificarlo prima di inviare una topologia hello, senza la necessità di toorecompile tutti gli elementi.

__writer.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubwriter"

components:
  # Configure hello Event Hub spout
  - id: "eventhubbolt-config"
    className: "org.apache.storm.eventhubs.bolt.EventHubBoltConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.write.policy.name}"
      - "${eventhub.write.policy.key}"
      - "${eventhub.namespace}"
      - "servicebus.windows.net"
      - "${eventhub.name}"

spouts:
  - id: "device-emulator-spout"
    className: "com.microsoft.example.DeviceSpout"
    parallelism: ${eventhub.partitions}

bolts:
  - id: "eventhub-bolt"
    className: "org.apache.storm.eventhubs.bolt.EventHubBolt"
    constructorArgs:
      - ref: "eventhubbolt-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

# How data flows through hello components
streams:
  - name: "spout -> eventhub" # just a string used for logging
    from: "device-emulator-spout"
    to: "eventhub-bolt"
    grouping:
        type: SHUFFLE

  - name: "spout -> logger"
    from: "device-emulator-spout"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

__reader.yaml__:

```yaml
---
# Topology that reads from Event Hubs
name: "eventhubreader"

components:
  # Configure hello Event Hub spout
  - id: "eventhubspout-config"
    className: "org.apache.storm.eventhubs.spout.EventHubSpoutConfig"
    constructorArgs:
      # These are populated from hello .properties file when hello topology is started
      - "${eventhub.read.policy.name}"
      - "${eventhub.read.policy.key}"
      - "${eventhub.namespace}"
      - "${eventhub.name}"
      - ${eventhub.partitions}

spouts:
  - id: "eventhub-spout"
    className: "org.apache.storm.eventhubs.spout.EventHubSpout"
    constructorArgs:
      - ref: "eventhubspout-config" # config declared in components section
    # parallelism hint. This should be hello same as hello number of partitions for your Event Hub, so we read it from hello dev.properties file passed at run time.
    parallelism: ${eventhub.partitions}

bolts:
  # Log information
  - id: "log-bolt"
    className: "org.apache.storm.flux.wrappers.bolts.LogInfoBolt"
    parallelism: 1

  # Parses from JSON into tuples
  - id: "parser-bolt"
    className: "com.microsoft.example.ParserBolt"
    parallelism: ${eventhub.partitions}

# How data flows through hello components
streams:
  - name: "spout -> parser" # just a string used for logging
    from: "eventhub-spout"
    to: "parser-bolt"
    grouping:
        type: SHUFFLE

  - name: "parser -> log-bolt"
    from: "parser-bolt"
    to: "log-bolt"
    grouping:
        type: SHUFFLE
```

#### <a name="tell-hello-topology-about-event-hub"></a>Informare topologia hello Hub eventi

In fase di esecuzione hello `dev.properties` file è utilizzato toopass hello Hub eventi configurazione toohello topologia. Hello esempio seguente è contenuto predefinito hello del file hello:

```yaml
eventhub.write.policy.name: writer
eventhub.write.policy.key: your_key_here
eventhub.read.policy.name: reader
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: storm
eventhub.partitions: 2
```

## <a name="configure-environment-variables"></a>Configurare le variabili di ambiente

Hello seguenti variabili di ambiente possono essere impostate durante l'installazione di Java e hello JDK nella workstation di sviluppo. Tuttavia, è necessario verificare che esistano e che contengono i valori corretti di hello per il sistema.

* **JAVA_HOME** -deve puntare toohello directory in cui è installato Java runtime environment (JRE) di hello. Ad esempio, in una distribuzione di Unix o Linux, deve essere un valore simile troppo`/usr/lib/jvm/java-7-oracle`. In Windows, avrebbe un valore simile troppo`c:\Program Files (x86)\Java\jre1.7`
* **PERCORSO** -deve contenere hello seguenti percorsi:

  * **JAVA_HOME** (o percorso equivalente hello)
  * **JAVA_HOME\bin** (o percorso equivalente hello)
  * directory di Hello in cui è installato Maven

## <a name="configure-event-hub"></a>Configurare l'hub eventi

Hub eventi è l'origine dati hello per questo esempio. Utilizzare hello seguendo i passaggi toocreate un Hub eventi.

1. Da hello [portale di Azure classico](https://manage.windowsazure.com)selezionare **NEW** > **Bus di servizio** > **Hub eventi**  >  **Creazione personalizzata**.

2. In hello **aggiungere un nuovo Hub eventi** schermata, immettere un **nome Hub eventi**. Seleziona hello **area** toocreate hello hub, quindi creare uno spazio dei nomi o selezionarne uno esistente. Infine, fare clic su hello **freccia** toocontinue.

    ![procedura guidata - pagina 1](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz1.png)

   > [!NOTE]
   > Selezionare hello stesso **percorso** come l'elevato numero di latenza tooreduce di HDInsight server e i costi.

3. In hello **configurare Hub eventi** immettere hello **numero di partizione** e **memorizzazione dei messaggi** valori. Per questo esempio usare un numero di partizioni pari a 10 e un valore di conservazione dei messaggi pari a 1. Si noti il numero di partizioni hello perché questo valore è necessario in un secondo momento.

    ![procedura guidata - pagina 2](./media/hdinsight-storm-develop-csharp-event-hub-topology/wiz2.png)

4. Una volta hub eventi hello hello creati, selezionare lo spazio dei nomi, selezionare **hub eventi**, quindi selezionare l'hub di eventi hello creato in precedenza.
5. Selezionare **configura**, quindi creare due nuovi criteri di accesso utilizzando hello le seguenti informazioni:

    <table>
    <tr><th>Nome</th><th>Autorizzazioni</th></tr>
    <tr><td>Writer</td><td>Invio</td></tr>
    <tr><td>Reader</td><td>Attesa</td></tr>
    </table>

    Dopo aver creato le autorizzazioni di hello, selezionare hello **salvare** icona hello parte inferiore della pagina hello. Questi criteri di accesso condiviso sono utilizzati tooread e scrivere tooEvent Hub.

    ![criteri](./media/hdinsight-storm-develop-csharp-event-hub-topology/policy.png)

6. Dopo aver salvato i criteri di hello, usare hello **generatore di chiavi di accesso condiviso** nella parte inferiore di hello della chiave di hello pagina tooretrieve hello per hello **writer** e **lettore** criteri. Salvare queste chiavi.

## <a name="download-and-build-hello-project"></a>Scaricare e compilare il progetto hello

1. Scaricare il progetto di hello da GitHub: [eventhub hdinsight-java-storm](https://github.com/Azure-Samples/hdinsight-java-storm-eventhub). È possibile scaricare il pacchetto di hello come archivio zip o utilizzare [git](https://git-scm.com/) tooclone il progetto hello in locale.

2. Modificare hello `dev.properties` file con la configurazione di hello per l'Hub di eventi.

3. Utilizzare hello seguente progetto hello toobuild e del pacchetto:

        mvn package

    Questo comando Scarica le dipendenze richieste, le compilazioni, e quindi i pacchetti hello progetto. output di Hello viene archiviato in hello **/destinazione** directory come **EventHubExample-1.0-SNAPSHOT.jar**.

## <a name="test-locally"></a>Test in locale

Poiché queste topologie solo leggere e scrivere tooEvent hub, è possibile eseguirne il test in locale se dispone di un [ambiente di sviluppo Storm](http://storm.apache.org/releases/current/Setting-up-development-environment.html). Utilizzare hello seguendo i passaggi toorun localmente nell'ambiente di sviluppo hello:

1. Eseguire writer hello:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /writer.yaml --filter dev.properties

2. Eseguire la lettura hello:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local -R /reader.yaml --filter dev.properties

> [!TIP]
> * `--local`: Topologia di hello esecuzione in modalità locale (non distribuite).
> * `-R /writer.yaml`: Caricare la definizione di topologia hello da hello `resources` sotto forma di file jar hello. Se la topologia hello è un file hello file System locale, specificare hello percorso tooit come ultimo parametro hello.
> * `--filter dev.properties`: Utilizzare il contenuto di hello del `dev.properties` toofill valori hello in definizioni di topologia hello. ad esempio `${eventhub.read.policy.name}`.

Output è connesso toohello console durante l'esecuzione in locale. Utilizzare __Ctrl + C__ topologia hello toostop.

## <a name="deploy-hello-topologies"></a>Distribuire le topologie di hello

1. Utilizzare SCP toocopy hello jar pacchetto tooyour cluster HDInsight. Sostituire il nome utente con utente SSH hello per il cluster. Sostituire CLUSTERNAME con nome hello del cluster HDInsight:

        scp ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.

    Se si utilizza una password per l'account SSH, si è password hello tooenter richiesta. Se si utilizza una chiave SSH con l'account di hello, potrebbe essere necessario hello toouse `-i` parametro toospecify hello percorso toohello file di chiave. Ad esempio, `scp -i ~/.ssh/id_rsa ./target/EventHubExample-1.0-SNAPSHOT.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:.`

    Questo comando copia hello toohello home directory del file dell'utente di SSH nel cluster hello.

2. Al termine il caricamento di file hello, utilizzare cluster di HDInsight toohello tooconnect SSH. Sostituire **USERNAME** nome hello dell'accesso SSH. Sostituire **CLUSTERNAME** con il nome del cluster HDInsight:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    > [!NOTE]
    > Se si utilizza una password per l'account SSH, si è password hello tooenter richiesta. Se si utilizza una chiave SSH con l'account di hello, potrebbe essere necessario hello toouse `-i` parametro toospecify hello percorso toohello file di chiave. esempio Hello carica hello della chiave privata `~/.ssh/id_rsa`:
    >
    > `ssh -i ~/.ssh/id_rsa USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`

3. Utilizzare hello topologie hello toostart di comando seguente:

        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /writer.yaml --filter dev.properties
        storm jar EventHubExample-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote -R /reader.yaml --filter dev.properties

    > [!TIP]
    > * `--remote`: Invia hello topologia toohello servizio Nimbus, che avvia su nodi di lavoro hello cluster hello.

4. dati registrato hello tooview, visitare toohttps://CLUSTERNAME.azurehdinsight.net/stormui, in cui __CLUSTERNAME__ hello nome del cluster HDInsight. Selezionare le topologie di hello e drill-down toohello componenti. Seleziona hello __porta__ voce per un'istanza di un componente di tooview le informazioni registrate.

5. Utilizzare hello topologie di hello toostop i comandi seguenti:

        storm kill reader
        storm kill writer

## <a name="delete-your-cluster"></a>Eliminare il cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Passaggi successivi

* [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md)
