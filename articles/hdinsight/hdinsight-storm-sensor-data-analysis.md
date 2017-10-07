---
title: dati del sensore aaaAnalyze con Apache Storm e HBase | Documenti Microsoft
description: Informazioni su come tooconnect tooApache Storm con una rete virtuale. Utilizzare Storm con dati del sensore tooprocess HBase da un hub eventi e visualizzarla con D3.js.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: a9a1ac8e-5708-4833-b965-e453815e671f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/09/2017
ms.author: larryfr
ms.openlocfilehash: e54fe9ffc720b0089f90e302b24a9438bd43999a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="analyze-sensor-data-with-apache-storm-event-hub-and-hbase-in-hdinsight-hadoop"></a>Analizzare i dati del sensore con Apache Storm, hub eventi e HBase in HDInsight (Hadoop)

Informazioni su come toouse Apache Storm HDInsight tooprocess dei dati del sensore di Hub di eventi di Azure. Hello dati vengono quindi archiviati in Apache HBase in HDInsight e visualizzato tramite D3.js.

modello di gestione risorse di Azure Hello utilizzato in questo documento illustra come toocreate più risorse di Azure in un gruppo di risorse. Hello modello consente di creare una rete virtuale di Azure, due cluster HDInsight (Storm e HBase) e un'App Web di Azure. Un'implementazione di node.js di un dashboard web in tempo reale viene automaticamente distribuito toohello web app.

> [!NOTE]
> informazioni di Hello in questo documento e un esempio in questo documento richiedono HDInsight versione 3.6.
>
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

## <a name="prerequisites"></a>Prerequisiti

* Una sottoscrizione di Azure.
* [Node.js](http://nodejs.org/): dashboard web di hello toopreview utilizzate in ambiente di sviluppo locale.
* [Java e hello JDK 1.7](http://www.oracle.com/technetwork/java/javase/downloads/index.html): utilizzata una topologia di Storm toodevelop hello.
* [Maven](http://maven.apache.org/what-is-maven.html): progetto di hello toobuild e compilazione utilizzato.
* [GIT](http://git-scm.com/): progetto hello toodownload utilizzato da GitHub.
* Un **SSH** client: tooconnect toohello HDInsight basati su Linux cluster usati. Per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).


> [!IMPORTANT]
> Non è necessario un cluster HDInsight esistente. procedura di Hello in questo documento consente di creare hello seguenti risorse:
> 
> * Una rete virtuale di Azure
> * Un cluster Storm in HDInsight (basato su Linux con due nodi del ruolo di lavoro)
> * Un cluster HBase in HDInsight (basato su Linux con due nodi del ruolo di lavoro)
> * Un'App Web di Azure che ospita dashboard web hello

## <a name="architecture"></a>Architettura

![diagramma dell'architettura](./media/hdinsight-storm-sensor-data-analysis/devicesarchitecture.png)

Questo esempio è costituito da hello seguenti componenti:

* **Hub eventi di Azure**: include i dati raccolti dai sensori.
* **Storm in HDInsight**: assicura l'elaborazione in tempo reale dei dati provenienti dall'hub eventi.
* **HBase in HDInsight**: fornisce un archivio dati NoSQL persistente per i dati, dopo l'elaborazione tramite Storm.
* **Servizio di rete virtuale Azure**: consente di proteggere le comunicazioni tra hello Storm in HDInsight e HBase nei cluster HDInsight.
  
  > [!NOTE]
  > Una rete virtuale è obbligatoria quando si utilizza l'API client di HBase Java hello. Non è esposta tramite il gateway pubblica hello per cluster HBase. Cluster HBase l'installazione e Storm nella stessa rete virtuale consente di hello hello cluster Storm (o qualsiasi altro sistema sulla rete virtuale hello) toodirectly accedere tramite l'API del client.

* **Sito Web del dashboard**: dashboard di esempio che rappresenta graficamente i dati in tempo reale.
  
  * sito Web di Hello viene implementato in Node.js.
  * [Socket.IO](http://socket.io/) utilizzato per la comunicazione in tempo reale tra topologia Storm hello e hello.
    
    > [!NOTE]
    > L'uso di Socket.io per la comunicazione è un dettaglio di implementazione. È possibile usare qualsiasi framework di comunicazione, ad esempio WebSocket o SignalR non elaborato.

  * [D3.js](http://d3js.org/) toograph utilizzati hello dati del sito Web toohello inviato.

> [!IMPORTANT]
> Due cluster sono necessari, perché non esiste alcun cluster di HDInsight un metodo supportato toocreate Storm sia HBase.

Hello topologia legge i dati provenienti dall'Hub eventi tramite hello [org.apache.storm.eventhubs.spout.EventHubSpout](http://storm.apache.org/releases/0.10.1/javadocs/org/apache/storm/eventhubs/spout/class-use/EventHubSpout.html) classe e scrive i dati in HBase tramite hello [org.apache.storm.hbase.bolt.HBaseBolt](https://storm.apache.org/releases/1.0.1/javadocs/org/apache/storm/hbase/bolt/HBaseBolt.html) classe. La comunicazione con il sito hello viene eseguita utilizzando [socket.io client.java](https://github.com/nkzawa/socket.io-client.java).

Hello seguente diagramma illustra il layout di hello della topologia hello:

![diagramma della topologia](./media/hdinsight-storm-sensor-data-analysis/sensoranalysis.png)

> [!NOTE]
> Questo diagramma è una visualizzazione semplificata della topologia hello. Per ogni partizione dell'hub eventi viene creata un'istanza di ogni componente. Queste istanze vengono distribuite tra i nodi nel cluster hello hello e dati viene instradati tra di essi, come indicato di seguito:
> 
> * I dati dal parser di toohello beccuccio hello sono con carico bilanciato.
> * Dati da hello parser toohello Dashboard e HBase vengono raggruppati per ID dispositivo, in modo che i messaggi da hello stesso dispositivo sempre flusso toohello stesso componente.

### <a name="topology-components"></a>Componenti della topologia

* **Hub di eventi Spout**: beccuccio hello è fornito come parte della versione di Apache Storm 0.10.0 e versioni successive.
  
  > [!NOTE]
  > beccuccio Hub eventi Hello utilizzato in questo esempio richiede un elevato numero di versione di cluster HDInsight 3.5 o 3.6.

* **ParserBolt.java**: dati hello emesso dal beccuccio hello JSON non elaborati e in alcuni casi più di un evento viene generato alla volta. Questo fulmine legge dati hello generati da hello spout e analizza il messaggio JSON hello. fulmine Hello genera quindi i dati di hello come una tupla che contiene più campi.
* **DashboardBolt.java**: questo componente viene illustrato come toouse hello Socket.io di libreria client per i dati toosend Java nel dashboard in tempo reale toohello web.
* **No-hbase.yaml**: hello definizione della topologia utilizzata durante l'esecuzione in modalità locale. Non usa componenti HBase.
* **con hbase.yaml**: hello usato quando si esegue la topologia hello in cluster hello definizione della topologia. Usa componenti HBase.
* **DEV.Properties**: hello informazioni di configurazione per beccuccio Hub eventi hello fulmine HBase e componenti del dashboard.

## <a name="prepare-your-environment"></a>Preparare l'ambiente

Prima di usare questo esempio, è necessario creare un Hub di eventi di Azure, la topologia di Storm hello letta.

### <a name="configure-event-hub"></a>Configurare l'hub eventi

Hub eventi è l'origine dati hello per questo esempio. Utilizzare hello seguendo i passaggi toocreate un Hub eventi.

1. Da hello [portale di Azure](https://portal.azure.com)selezionare **+ nuovo** -> **Internet of Things** -> **hub eventi**.
2. In hello **creare Namespace** seguire hello seguenti attività:
   
   1. Immettere un **nome** per spazio dei nomi hello.
   2. Selezione di un piano tariffario. **Basic** è sufficiente per questo esempio.
   3. Seleziona hello Azure **sottoscrizione** toouse.
   4. Selezionare un gruppo di risorse esistente o crearne uno nuovo.
   5. Seleziona hello **percorso** per hello Hub eventi.
   6. Selezionare **Pin toodashboard**, quindi fare clic su **crea**.

3. Al termine del processo di creazione di hello, hello informazioni hub eventi per lo spazio dei nomi viene visualizzato. Da qui, scegliere **+ Aggiungi hub eventi**. In hello **creare Hub eventi** sezione, immettere un nome di **sensordata**, quindi selezionare **crea**. Lasciare hello altri campi valori predefiniti di hello.
4. Dall'hub di eventi hello visualizzare dello spazio dei nomi, seleziona **hub eventi**. Seleziona hello **sensordata** voce.
5. Hello sensordata Hub eventi, selezionare **criteri di accesso condiviso**. Hello utilizzare **+ Aggiungi** hello tooadd collegamento seguenti criteri:

    | Nome criterio | Claims |
    | ----- | ----- |
    | devices | Invio |
    | storm | Attesa |

1. Selezionare entrambi i criteri e prendere nota di hello **chiave primaria** valore. È necessario il valore di hello per entrambi i criteri in passaggi futuri.

## <a name="download-and-configure-hello-project"></a>Scaricare e configurare il progetto hello

Utilizzare hello seguente progetto hello toodownload da GitHub.

    git clone https://github.com/Blackmist/hdinsight-eventhub-example

Al termine del comando di hello, è necessario hello seguente struttura di directory:

    hdinsight-eventhub-example/
        TemperatureMonitor/ - this contains hello topology
            resources/
                log4j2.xml - set logging toominimal.
                no-hbase.yaml - topology definition without hbase components.
                with-hbase.yaml - topology definition with hbase components.
            src/main/java/com/microsoft/examples/bolts/
                ParserBolt.java - parses JSON data into tuples
                DashboardBolt.java - sends data over Socket.IO toohello web dashboard.
        dashboard/nodejs/ - this is hello node.js web dashboard.
        SendEvents/ - utilities toosend fake sensor data.

> [!NOTE]
> Questo documento non va nei dettagli toofull di codice hello inclusi in questo esempio. Tuttavia, il codice hello è completamente impostata come commento.

tooconfigure hello progetto tooread dall'Hub di eventi, aprire hello `hdinsight-eventhub-example/TemperatureMonitor/dev.properties` file e aggiungere il toohello informazioni Hub eventi seguenti righe:

```bash
eventhub.read.policy.name: your_read_policy_name
eventhub.read.policy.key: your_key_here
eventhub.namespace: your_namespace_here
eventhub.name: your_event_hub_name
eventhub.partitions: 2
```

## <a name="compile-and-test-locally"></a>Compilare ed eseguire il test in locale

> [!IMPORTANT]
> Utilizzando la topologia hello locale richiede un ambiente di sviluppo Storm funzionante. Per altre informazioni, vedere [Setting up a development environment](http://storm.apache.org/releases/1.1.0/Setting-up-development-environment.html) (Impostazione di un ambiente di sviluppo) in Apache.org.

> [!WARNING]
> Se si utilizza un ambiente di sviluppo di Windows, si potrebbe ricevere un `java.io.IOException` quando si esegue la topologia hello in locale. In questo caso, spostare sulla topologia di hello toorunning in HDInsight.

Prima di testare, è necessario avviare l'output di hello dashboard tooview hello della topologia hello e generare dati toostore in Hub eventi.

> [!IMPORTANT]
> componente di HBase Hello di questa topologia non è attivo durante il test in locale. Hello API Java per cluster HBase hello non è accessibile dall'esterno hello rete virtuale di Azure che contiene il cluster hello.

### <a name="start-hello-web-application"></a>Avviare l'applicazione web hello

1. Aprire un prompt dei comandi e passare alla directory troppo`hdinsight-eventhub-example/dashboard`. Utilizzare hello dipendenze hello tooinstall di comando necessari per un'applicazione hello web seguente:
   
    ```bash
    npm install
    ```

2. Utilizzare hello dopo l'applicazione web di comando toostart hello:
   
    ```bash
    node server.js
    ```
   
    Viene visualizzato un toohello simile messaggio seguente testo:
   
        Server listening at port 3000

3. Aprire un web browser e immettere `http://localhost:3000/` come indirizzo hello. Viene visualizzato un toohello simile pagina seguente immagine:
   
    ![dashboard Web](./media/hdinsight-storm-sensor-data-analysis/emptydashboard.png)
   
    Lasciare il prompt dei comandi aperto. Al termine del test, utilizzare Ctrl-C toostop hello web server.

### <a name="generate-data"></a>Generare i dati

> [!NOTE]
> Hello passaggi in questa sezione utilizzano Node. js in modo che possono essere utilizzati su qualsiasi piattaforma. Per altri esempi di linguaggio, vedere hello `SendEvents` directory.

1. Aprire un nuovo prompt dei comandi, una shell o terminal e passare alla directory troppo`hdinsight-eventhub-example/SendEvents/nodejs`. dipendenze di hello tooinstall necessarie per un'applicazione hello, utilizzare hello comando seguente:

    ```bash
    npm install
    ```

2. Aprire hello `app.js` file in un editor di testo e aggiungere hello informazioni Hub eventi è ottenuto in precedenza:
   
    ```javascript
    // ServiceBus Namespace
    var namespace = 'YourNamespace';
    // Event Hub Name
    var hubname ='sensordata';
    // Shared access Policy name and key (from Event Hub configuration)
    var my_key_name = 'devices';
    var my_key = 'YourKey';
    ```
   
   > [!NOTE]
   > Questo esempio si presuppone che si usa `sensordata` come nome hello dell'Hub di eventi. E che `devices` come nome hello del criterio di hello un `Send` attestazione.

3. Comando che segue di hello utilizzare tooinsert nuove voci in Hub eventi:
   
    ```bash
    node app.js
    ```
   
    Viene visualizzato più righe di output che contengono dati hello inviati tooEvent Hub:
   
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"0","Temperature":7}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"1","Temperature":39}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"2","Temperature":86}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"3","Temperature":29}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"4","Temperature":30}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"5","Temperature":5}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"6","Temperature":24}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"7","Temperature":40}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"8","Temperature":43}
        {"TimeStamp":"2015-02-10T14:43.05.00320Z","DeviceId":"9","Temperature":84}

### <a name="build-and-start-hello-topology"></a>Compilare e avviare topologia hello

1. Aprire un nuovo prompt dei comandi e passare alla directory troppo`hdinsight-eventhub-example/TemperatureMonitor`. toobuild e pacchetto hello topologia, usare hello comando seguente: 

    ```bash
    mvn clean package
    ```

2. toostart hello topologia in modalità locale, usare hello comando seguente:

    ```bash
    storm jar target/TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --local --filter dev.properties resources/no-hbase.yaml
    ```

    * `--local`topologia di hello viene avviato in modalità locale.
    * `--filter`Usa hello `dev.properties` file toopopulate parametri nella definizione della topologia hello.
    * `resources/no-hbase.yaml`Usa hello `no-hbase.yaml` definizione della topologia.
 
   Una volta avviata, topologia hello legge le voci da Hub di eventi e li invia dashboard toohello in esecuzione sul computer locale. È necessario visualizzare le righe vengono visualizzati nel dashboard web hello, simile toohello seguente immagine:
   
    ![dashboard con dati](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

2. Durante l'esecuzione di dashboard hello utilizzare hello `node app.js` comando hello precedente passaggi toosend nuovi dati tooEvent hub. Poiché i valori della temperatura hello generati in modo casuale, grafico hello deve aggiornare le modifiche di grandi dimensioni tooshow della temperatura.
   
   > [!NOTE]
   > È necessario essere in hello **hdinsight-eventhub-esempio/SendEvents/Nodejs** directory quando si utilizza hello `node app.js` comando.

3. Dopo la verifica degli aggiornamenti di dashboard hello, topologia hello stop utilizzando Ctrl + C. È possibile utilizzare anche i server web locale hello toostop di Ctrl + C.

## <a name="create-a-storm-and-hbase-cluster"></a>Creare un cluster Storm e HBase

Hello i passaggi in questa sezione viene utilizzata una [modello di Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md) toocreate un cluster di rete virtuale di Azure e un elevato numero di e HBase in rete virtuale hello. modello di Hello, inoltre, crea un'App Web di Azure e distribuisce una copia del dashboard hello al suo interno.

> [!NOTE]
> Una rete virtuale viene utilizzata in modo che topologia hello in esecuzione nel cluster Storm hello può comunicare direttamente con i cluster di HBase hello tramite API Java HBase hello.

modello di gestione risorse di Hello utilizzato in questo documento si trova in un contenitore di blob pubblici in **https://hditutorialdata.blob.core.windows.net/armtemplates/create-linux-based-hbase-storm-cluster-in-vnet-3.6.json**.

1. Fare clic su hello seguente pulsante toosign in tooAzure e il modello di gestione risorse hello Apri nel portale di Azure hello.
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fhditutorialdata.blob.core.windows.net%2Farmtemplates%2Fcreate-linux-based-hbase-storm-cluster-in-vnet-3.6.json" target="_blank"><img src="./media/hdinsight-storm-sensor-data-analysis/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. Da hello **distribuzione personalizzata** immettere hello seguenti valori:
   
    ![Parametri di HDInsight](./media/hdinsight-storm-sensor-data-analysis/parameters.png)
   
   * **Nome del Cluster di base**: questo valore viene utilizzato come nome di base per i cluster Storm e HBase hello hello. Ad esempio, se si immette **abc** verranno creati un cluster Storm denominato **storm-abc** e un cluster HBase denominato **hbase-abc**.
   * **Nome utente di accesso del cluster**: nome utente amministratore di hello per i cluster Storm e HBase hello.
   * **Password di account di accesso cluster**: password dell'utente per i cluster Storm e HBase hello hello admin.
   * **Nome utente SSH**: hello toocreate utente SSH per i cluster Storm e HBase hello.
   * **Password SSH**: password hello per utente SSH hello per i cluster Storm e HBase hello.
   * **Percorso**: area hello creati in cluster hello.
     
     Fare clic su **OK** parametri hello toosave.

3. Hello utilizzare **nozioni di base** sezione toocreate un gruppo di risorse o selezionarne uno esistente.
4. In hello **percorso del gruppo di risorse** menu a discesa, seleziona hello nello stesso percorso come selezionato per hello **percorso** parametro hello **impostazioni** sezione.
5. Leggere le condizioni di hello e quindi selezionare **accetto le condizioni indicate in precedenza toohello**.
6. Infine, controllare **Pin toodashboard** e quindi selezionare **acquisto**. Sono necessari circa 20 minuti toocreate cluster hello.

Dopo avere create le risorse di hello, informazioni sui gruppi di risorse hello.

![Gruppo di risorse per la rete virtuale hello e cluster](./media/hdinsight-storm-sensor-data-analysis/groupblade.png)

> [!IMPORTANT]
> Si noti che sono nomi hello dei cluster HDInsight hello **storm BASENAME** e **hbase BASENAME**, dove BASENAME è nome hello toohello modello specificato. Utilizzare questi nomi in un passaggio successivo durante la connessione toohello cluster. È anche nota che hello nome del sito dashboard hello **basename dashboard**. Questo valore viene usato più avanti in questo documento.

## <a name="configure-hello-dashboard-bolt"></a>Configurare fulmine Dashboard hello

i dashboard di toohello dati toosend distribuiti come un'app web, è necessario modificare hello seguente riga hello `dev.properties`file:

```yaml
dashboard.uri: http://localhost:3000
```

Modifica `http://localhost:3000` troppo`http://BASENAME-dashboard.azurewebsites.net` e salvare il file hello. Sostituire **BASENAME** con il nome di base hello specificato nel passaggio precedente hello. È anche possibile utilizzare il gruppo di risorse hello creato in precedenza hello tooselect dashboard e visualizzare URL hello.

## <a name="create-hello-hbase-table"></a>Creare una tabella HBase hello

toostore dati in HBase, è innanzitutto necessario creare una tabella. Creazione preliminare di Storm deve toowrite per le risorse, in quanto durante il tentativo toocreate risorse all'interno di una topologia di Storm possono generare più istanze durante il tentativo toocreate hello stessa risorsa. Creare risorse hello esterne topologia hello e utilizzare Storm per analitica e di lettura/scrittura.

1. Utilizzare cluster HBase toohello tooconnect SSH utilizzando hello SSH e la password utente fornite toohello modello durante la creazione del cluster. Ad esempio, se la connessione utilizzando hello `ssh` comando, utilizzare la seguente sintassi hello:
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```
   
    Sostituire `sshuser` con nome utente di hello SSH forniti durante la creazione di cluster hello. Sostituire `clustername` con il nome del cluster HBase hello.

2. Dalla sessione SSH hello, avviare la shell di HBase hello.
   
    ```bash
    hbase shell
    ```
   
    Una volta caricate shell hello, vedrai un `hbase(main):001:0>` prompt dei comandi.

3. Dalla shell di HBase hello, immettere hello toocreate comando dati del sensore una tabella toostore hello seguenti:
   
    ```hbase
    create 'SensorData', 'cf'
    ```

4. Verificare che la tabella hello è stata creata utilizzando hello comando seguente:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Vengono restituite informazioni toohello simile esempio seguente, che indica che sono disponibili 0 righe nella tabella hello.
   
        ROW                   COLUMN+CELL                                       0 row(s) in 0.1900 seconds

5. Immettere `exit` tooexit hello shell di HBase:

## <a name="configure-hello-hbase-bolt"></a>Configurare fulmine HBase hello

tooHBase toowrite dal cluster Storm hello, è necessario fornire fulmine HBase hello con i dettagli di configurazione hello del cluster HBase.

1. Utilizzare uno dei seguenti quorum di esempi tooretrieve hello Zookeeper per il cluster HBase hello:

    ```bash
    CLUSTERNAME='your_HDInsight_cluster_name'
    curl -u admin -sS -G "https://$CLUSTERNAME.azurehdinsight.net/api/v1/clusters/$CLUSTERNAME/services/HBASE/components/HBASE_MASTER" | jq '.metrics.hbase.master.ZookeeperQuorum'
    ```

    > [!NOTE]
    > Sostituire `your_HDInsight_cluster_name` con nome hello del cluster HDInsight. Per ulteriori informazioni sull'installazione hello `jq` utilità, vedere [https://stedolan.github.io/jq/](https://stedolan.github.io/jq/).
    >
    > Quando richiesto, immettere la password di hello per account di accesso amministratore hello HDInsight.

    ```powershell
    $clusterName = 'your_HDInsight_cluster_name`
    $creds = Get-Credential -UserName "admin" -Message "Enter hello HDInsight login"
    $resp = Invoke-WebRequest -Uri "https://$clusterName.azurehdinsight.net/api/v1/clusters/$clusterName/services/HBASE/components/HBASE_MASTER" -Credential $creds
    $respObj = ConvertFrom-Json $resp.Content
    $respObj.metrics.hbase.master.ZookeeperQuorum
    ```

    > [!NOTE]
    > Sostituire ' your_HDInsight_cluster_name con nome hello del cluster HDInsight. Quando richiesto, immettere la password di hello per account di accesso amministratore hello HDInsight.
    >
    > Questo esempio richiede Azure PowerShell. Per altre informazioni sull'uso di Azure PowerShell, vedere [Getting started with Azure PowerShell](https://docs.microsoft.com/en-us/powershell/scripting/Getting-Started-with-Windows-PowerShell?view=powershell-6) (Introduzione ad Azure PowerShell)

    informazioni di Hello restituite da questi esempi sono simile toohello seguente testo:

    `zk2-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk0-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181,zk3-hbase.mf0yeg255m4ubit1auvj1tutvh.ex.internal.cloudapp.net:2181`

    Queste informazioni vengono utilizzate da toocommunicate Storm con cluster HBase hello.

2. Modificare hello `dev.properties` file e aggiungere hello Zookeeper quorum informazioni toohello seguente riga:

    ```yaml
    hbase.zookeeper.quorum: your_hbase_quorum
    ```

## <a name="build-package-and-deploy-hello-solution-toohdinsight"></a>Pacchetto, compilare e distribuire hello soluzione tooHDInsight

Nell'ambiente di sviluppo, utilizzare hello cluster storm passaggi toodeploy hello Storm topologia toohello seguente.

1. Da hello `TemperatureMonitor` directory seguenti hello utilizzare comando tooperform una nuova compilazione e creare un pacchetto di file JAR dal progetto:
   
        mvn clean package
   
    Questo comando crea un file denominato `TemperatureMonitor-1.0-SNAPSHOT.jar in hello ` nella directory "target" del progetto.

2. Hello di utilizzare scp tooupload `TemperatureMonitor-1.0-SNAPSHOT.jar` e `dev.properties` cluster Storm tooyour di file. In hello seguente esempio, sostituire `sshuser` con utente SSH hello specificato durante la creazione di cluster di hello e `clustername` con nome hello del cluster Storm. Quando richiesto, immettere la password di hello per utente SSH hello.
   
    ```bash
    scp target/TemperatureMonitor-1.0-SNAPSHOT.jar dev.properties sshuser@clustername-ssh.azurehdinsight.net:
    ```

   > [!NOTE]
   > Potrebbe richiedere alcuni minuti file hello tooupload.

    Per ulteriori informazioni sull'utilizzo di hello `scp` e `ssh` i comandi con HDInsight, vedere [utilizzo di SSH con HDInsight](./hdinsight-hadoop-linux-use-ssh-unix.md)

3. Dopo aver hello file è stato caricato, connettersi cluster Storm toohello tramite SSH.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Sostituire `sshuser` con nome utente di hello SSH. Sostituire `clustername` con il nome del cluster Storm hello.

4. toostart hello topologia, usare hello comando dalla sessione SSH hello seguente:
   
    ```bash
    storm jar TemperatureMonitor-1.0-SNAPSHOT.jar org.apache.storm.flux.Flux --remote --filter dev.properties -R /with-hbase.yaml
    ```

    * `--remote`Invia hello topologia toohello servizio Nimbus, che distribuisce i nodi del Supervisore toohello cluster hello.
    * `--filter`Usa hello `dev.properties` file toopopulate parametri nella definizione della topologia hello.
    * `-R /with-hbase.yaml`Usa hello `with-hbase.yaml` topologia inclusa nel pacchetto hello.

5. Dopo l'avvio della topologia di hello, aprire un sito Web toohello browser è stato pubblicato in Azure, quindi utilizzare hello `node app.js` comando toosend dati tooEvent Hub. Informazioni di hello web dashboard aggiornamento toodisplay hello dovrebbe.
   
    ![dashboard](./media/hdinsight-storm-sensor-data-analysis/datadashboard.png)

## <a name="view-hbase-data"></a>Visualizzare i dati di HBase

Utilizzare i seguenti passaggi tooconnect tooHBase hello e verificare che siano stati scritti dati hello toohello tabella:

1. Utilizzare cluster HBase di toohello tooconnect SSH.
   
    ```bash
    ssh sshuser@clustername-ssh.azurehdinsight.net
    ```

    Sostituire `sshuser` con nome utente di hello SSH. Sostituire `clustername` con il nome del cluster HBase hello.

2. Dalla sessione SSH hello, avviare la shell di HBase hello.
   
    ```bash
    hbase shell
    ```
   
    Una volta caricate shell hello, vedrai un `hbase(main):001:0>` prompt dei comandi.

3. Visualizza le righe dalla tabella hello:
   
    ```hbase
    scan 'SensorData'
    ```
   
    Questo comando restituisce informazioni toohello simile seguendo il testo, che indica che è dati nella tabella hello.
   
        hbase(main):002:0> scan 'SensorData'
        ROW                             COLUMN+CELL
        \x00\x00\x00\x00               column=cf:temperature, timestamp=1467290788277, value=\x00\x00\x00\x04
        \x00\x00\x00\x00               column=cf:timestamp, timestamp=1467290788277, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x01               column=cf:temperature, timestamp=1467290788348, value=\x00\x00\x00M
        \x00\x00\x00\x01               column=cf:timestamp, timestamp=1467290788348, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x02               column=cf:temperature, timestamp=1467290788268, value=\x00\x00\x00R
        \x00\x00\x00\x02               column=cf:timestamp, timestamp=1467290788268, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x03               column=cf:temperature, timestamp=1467290788269, value=\x00\x00\x00#
        \x00\x00\x00\x03               column=cf:timestamp, timestamp=1467290788269, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x04               column=cf:temperature, timestamp=1467290788356, value=\x00\x00\x00>
        \x00\x00\x00\x04               column=cf:timestamp, timestamp=1467290788356, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x05               column=cf:temperature, timestamp=1467290788326, value=\x00\x00\x00\x0D
        \x00\x00\x00\x05               column=cf:timestamp, timestamp=1467290788326, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x06               column=cf:temperature, timestamp=1467290788253, value=\x00\x00\x009
        \x00\x00\x00\x06               column=cf:timestamp, timestamp=1467290788253, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x07               column=cf:temperature, timestamp=1467290788229, value=\x00\x00\x00\x12
        \x00\x00\x00\x07               column=cf:timestamp, timestamp=1467290788229, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x08               column=cf:temperature, timestamp=1467290788336, value=\x00\x00\x00\x16
        \x00\x00\x00\x08               column=cf:timestamp, timestamp=1467290788336, value=2015-02-10T14:43.05.00320Z
        \x00\x00\x00\x09               column=cf:temperature, timestamp=1467290788246, value=\x00\x00\x001
        \x00\x00\x00\x09               column=cf:timestamp, timestamp=1467290788246, value=2015-02-10T14:43.05.00320Z
        10 row(s) in 0.1800 seconds
   
   > [!NOTE]
   > Questa operazione di analisi restituisce un massimo di 10 righe dalla tabella hello.

## <a name="delete-your-clusters"></a>Eliminare i cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

toodelete hello cluster, archiviazione e app web in una sola volta, Elimina gruppo di risorse hello che li contiene.

## <a name="next-steps"></a>Passaggi successivi

Per altri esempi di topologie Storm con HDInsight, vedere [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md).

Per ulteriori informazioni su Apache Storm, vedere hello [Apache Storm](https://storm.incubator.apache.org/) sito.

Per ulteriori informazioni su HBase in HDInsight, vedere hello [HBase di HDInsight Panoramica](hdinsight-hbase-overview.md).

Per ulteriori informazioni su Socket.io, vedere hello [socket.io](http://socket.io/) sito.

Per altre informazioni su D3.js, vedere [D3.js - Data Driven Documents](http://d3js.org/).

Per altre informazioni sulla creazione di topologie in Java, vedere [Sviluppo di topologie basate su Java per Apache Storm in HDInsight](hdinsight-storm-develop-java-topology.md).

Per altre informazioni sulla creazione di topologie in .NET, vedere [Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

[azure-portal]: https://portal.azure.com
