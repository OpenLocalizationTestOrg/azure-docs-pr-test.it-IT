---
title: aaaDeploy e gestire le topologie di Apache Storm in HDInsight basati su Linux | Documenti Microsoft
description: Informazioni su come toodeploy, monitorare e gestire le topologie di Apache Storm tramite Dashboard Storm hello in HDInsight basati su Linux. Utilizzare gli strumenti Hadoop per Visual Studio
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 35086e62-d6d8-4ccf-8cae-00073464a1e1
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/16/2017
ms.author: larryfr
ms.openlocfilehash: 3a1edb773089cc596fea423710aa88cf83c7b841
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-hdinsight"></a>Distribuire e gestire topologie Apache Storm in HDInsight

In questo documento, nozioni di base hello di gestione e monitoraggio topologie di Storm in esecuzione su Storm nei cluster HDInsight.

> [!IMPORTANT]
> Hello passaggi in questo articolo richiedono un elevato numero di basati su Linux nel cluster HDInsight. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). 
>
> Per informazioni sulla distribuzione e sul monitoraggio di topologie in HDInsight basato su Windows, vedere [Distribuire e gestire le topologie di Apache Storm in HDInsight basato su Windows](hdinsight-storm-deploy-monitor-topology.md)


## <a name="prerequisites"></a>Prerequisiti

* **Storm basato su Linux in cluster HDInsight**: per i passaggi relativi alla creazione di un cluster, vedere [Introduzione ad Apache Storm in HDInsight](hdinsight-apache-storm-tutorial-get-started-linux.md) .

* (Facoltativo) **Familiarità con SSH e SCP**: per altre informazioni, vedere [Usare SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

* (Facoltativo) **Visual Studio**: Azure SDK 2.5.1 o versione successiva e hello Data Lake Tools per Visual Studio. Per altre informazioni, vedere [Introduzione all'uso di Data Lake Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    Una delle seguenti versioni di Visual Studio hello:

  * Visual Studio 2012 con [Update 4](http://www.microsoft.com/download/details.aspx?id=39305)

  * Visual Studio 2013 con [Update 4](http://www.microsoft.com/download/details.aspx?id=44921) o [Visual Studio 2013 Community](http://go.microsoft.com/fwlink/?LinkId=517284)
  * [Visual Studio 2015](https://www.visualstudio.com/downloads/)

  * Visual Studio 2015, qualsiasi edizione

  * Visual Studio 2017, qualsiasi edizione. Data Lake Tools per Visual Studio 2017 vengono installati come parte di hello del carico di lavoro di Azure.

## <a name="submit-a-topology-visual-studio"></a>Inviare una topologia: Visual Studio

gli strumenti di HDInsight Hello può essere utilizzato toosubmit c# o ibrida topologie tooyour cluster Storm. Hello alla procedura seguente usa un'applicazione di esempio. Per informazioni sulla creazione di propri topologie utilizzando gli strumenti di HDInsight hello, vedere [c# sviluppare topologie in hello HDInsight Tools per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

1. Se non è già installato più recente degli strumenti di Data Lake hello hello per Visual Studio, vedere [iniziare a usare Data Lake Tools per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

    > [!NOTE]
    > Hello Data Lake Tools per Visual Studio sono state in precedenza denominato hello HDInsight Tools per Visual Studio.
    >
    > Data Lake Tools per Visual Studio sono inclusi in hello __carico di lavoro di Azure__ per Visual Studio 2017.

2. Aprire Visual Studio e selezionare **File** > **Nuovo** > **Progetto**.

3. In hello **nuovo progetto** finestra di dialogo espandere **installato** > **modelli**, quindi selezionare **HDInsight**. Selezionare nell'elenco dei modelli di hello **Storm esempio**. Nella parte inferiore di hello della finestra di dialogo hello, digitare un nome per un'applicazione hello.

    ![immagine](./media/hdinsight-storm-deploy-monitor-topology-linux/sample.png)

4. In **Esplora**, fare clic sul progetto hello e selezionare **inviare tooStorm in HDInsight**.

   > [!NOTE]
   > Se richiesto, immettere le credenziali di accesso hello per la sottoscrizione di Azure. Se si dispone di più di una sottoscrizione, accedere toohello uno che contiene l'elevato numero di cluster HDInsight.

5. Selezionare l'elevato numero di cluster HDInsight da hello **Cluster Storm** elenco a discesa e quindi selezionare **Invia**. È possibile controllare se l'invio di hello ha esito positivo tramite hello **Output** finestra.

## <a name="submit-a-topology-ssh-and-hello-storm-command"></a>Inviare una topologia: SSH e hello Storm comando

1. Utilizzare cluster di HDInsight toohello tooconnect SSH. Sostituire **USERNAME** nome hello dell'accesso SSH. Sostituire **CLUSTERNAME** con il nome del cluster HDInsight:

        ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net

    Per ulteriori informazioni sull'utilizzo di SSH tooconnect tooyour HDInsight cluster, vedere [utilizzo di SSH con HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).

2. Utilizzare hello comando toostart una topologia di esempio seguente:

        storm jar /usr/hdp/current/storm-client/contrib/storm-starter/storm-starter-topologies-*.jar org.apache.storm.starter.WordCountTopology WordCount

    Questo comando avvia una topologia di hello esempio WordCount su cluster hello. Questa topologia generare in modo casuale frasi e occorrenza hello conteggio di ogni parola nella frase hello.

   > [!NOTE]
   > Quando si inviano cluster toohello topologia, è prima necessario copiare i file jar hello contenente cluster hello prima di utilizzare hello `storm` comando. toocopy hello toohello cluster di file è possibile utilizzare hello `scp` comando. Ad esempio, `scp FILENAME.jar USERNAME@CLUSTERNAME-ssh.azurehdinsight.net:FILENAME.jar`
   >
   > Esempio WordCount Hello e altri esempi di starter storm, sono già inclusi nel cluster in `/usr/hdp/current/storm-client/contrib/storm-starter/`.

## <a name="submit-a-topology-programmatically"></a>Inviare una topologia: a livello di programmazione

A livello di codice, è possibile distribuire una topologia tooStorm in HDInsight mediante la comunicazione con hello servizio Nimbus ospitato nel cluster. [https://github.com/Azure-Samples/hdinsight-Java-deploy-Storm-Topology](https://github.com/Azure-Samples/hdinsight-java-deploy-storm-topology) viene fornito un esempio di applicazione Java che illustra come toodeploy e avviare una topologia tramite il servizio Nimbus hello.

## <a name="monitor-and-manage-visual-studio"></a>Monitorare e gestire: Visual Studio

Quando una topologia è stata inviata tramite Visual Studio, hello **Storm topologie** visualizzare per il cluster hello viene visualizzato. Selezionare la topologia hello hello elenco tooview informazioni hello in esecuzione sulla topologia.

![monitor Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

> [!NOTE]
> È possibile visualizzare **Storm Topologies** anche da **Esplora server**, espandendo **Azure** > **HDInsight** e quindi facendo clic su un cluster Storm in HDInsight e selezionando **View Storm Topologies**.

Selezionare la forma hello per hello spouts o bulloni tooview informazioni su questi componenti. Viene aperta una nuova finestra per ogni elemento selezionato.

### <a name="deactivate-and-reactivate"></a>Disattivare e riattivare

La disattivazione di una topologia comporta la sua sospensione finché non viene terminata o riattivata. tooperform queste operazioni, utilizzare hello __disattiva__ e __riattivare__ pulsanti nella parte superiore di hello di hello __topologia riepilogo__.

### <a name="rebalance"></a>Ribilanciare

Una topologia di ribilanciamento consente parallelismo di hello sistema toorevise hello della topologia hello. Ad esempio, se è stato ridimensionato hello cluster tooadd altre note, il ribilanciamento consente una topologia toosee hello nuovi nodi.

toorebalance una topologia, utilizzare hello __ribilanciare__ pulsante nella parte superiore di hello di hello __topologia riepilogo__.

> [!WARNING]
> Ribilanciamento innanzitutto una topologia Disattiva topologia hello, vengono ridistribuiti worker in modo uniforme tra cluster hello e quindi restituisce infine hello topologia toohello stato prima di ribilanciamento si è verificato. Pertanto, se la topologia hello era attiva, diventa nuovamente attiva. Se invece era disattivata, rimarrà disattivata.

### <a name="kill-a-topology"></a>Terminare una topologia

Topologie di Storm continuano l'esecuzione fino a quando non vengono arrestati o hello cluster verrà eliminato. toostop una topologia, utilizzare hello __Kill__ pulsante nella parte superiore di hello di hello __topologia riepilogo__.

## <a name="monitor-and-manage-ssh-and-hello-storm-command"></a>Monitorare e gestire: SSH e hello Storm comando

Hello `storm` utilità consente toowork con esecuzione topologie dalla riga di comando hello. Per visualizzare l'elenco completo dei comandi, usare `storm -h` .

### <a name="list-topologies"></a>Visualizzare l'elenco delle topologie

Tutte le topologie in esecuzione, utilizzare hello toolist di comando seguente:

    storm list

Questo comando restituisce toohello di informazioni simili seguente testo:

    Topology_name        Status     Num_tasks  Num_workers  Uptime_secs
    -------------------------------------------------------------------
    WordCount            ACTIVE     29         2            263

### <a name="deactivate-and-reactivate"></a>Disattivare e riattivare

La disattivazione di una topologia comporta la sua sospensione finché non viene terminata o riattivata. Utilizzare hello successivo comando toodeactivate e riattivare:

    storm Deactivate TOPOLOGYNAME

    storm Activate TOPOLOGYNAME

### <a name="kill-a-running-topology"></a>Terminare una topologia in esecuzione

Una volta avviate, le topologie Storm continueranno a rimanere in esecuzione finché non vengono arrestate. toostop una topologia, utilizzare hello comando seguente:

    storm kill TOPOLOGYNAME

### <a name="rebalance"></a>Ribilanciare

Una topologia di ribilanciamento consente parallelismo di hello sistema toorevise hello della topologia hello. Ad esempio, se è stato ridimensionato hello cluster tooadd altre note, il ribilanciamento consente una topologia toosee hello nuovi nodi.

> [!WARNING]
> Ribilanciamento innanzitutto una topologia Disattiva topologia hello, vengono ridistribuiti worker in modo uniforme tra cluster hello e quindi restituisce infine hello topologia toohello stato prima di ribilanciamento si è verificato. Pertanto, se la topologia hello era attiva, diventa nuovamente attiva. Se invece era disattivata, rimarrà disattivata.

    storm rebalance TOPOLOGYNAME

## <a name="monitor-and-manage-storm-ui"></a>Monitorare e gestire: interfaccia utente di Storm

Ciao Storm UI fornisce un'interfaccia web per l'utilizzo con l'esecuzione di topologie ed è incluso nel cluster HDInsight. hello tooview dell'interfaccia utente Storm, utilizzare un tooopen browser web **https://CLUSTERNAME.azurehdinsight.net/stormui**, dove **CLUSTERNAME** hello nome del cluster.

> [!NOTE]
> Se richiesto tooprovide un nome utente e una password, immettere Amministrazione cluster hello (amministratore) e la password utilizzati quando la creazione di cluster di hello.

### <a name="main-page"></a>Pagina principale

pagina principale di Hello di hello Storm UI fornisce hello le seguenti informazioni:

* **Riepilogo di cluster**: informazioni di base sui cluster Storm hello.
* **Topology summary**: elenco delle topologie in esecuzione. Utilizzare collegamenti hello in questa sezione di tooview ulteriori informazioni sulle topologie specifiche.
* **Riepilogo Supervisore**: informazioni su Supervisore Storm hello.
* **Configurazione nimbus**: configurazione di Nimbus per cluster hello.

### <a name="topology-summary"></a>Topology summary

Quando si seleziona un collegamento da hello **riepilogo topologia** sezione sono visualizzate le seguenti informazioni sulla topologia di hello hello:

* **Topologia riepilogo**: le informazioni di base relative alla topologia di hello.
* **Azioni di topologia**: azioni di gestione che è possibile eseguire per la topologia hello.

  * **Activate**: riprende l'elaborazione di una topologia disattivata.
  * **Deactivate**: sospende una topologia in esecuzione.
  * **Ribilanciare**: consente di regolare il parallelismo hello della topologia hello. È necessario ribilanciare topologie in esecuzione dopo avere modificato il numero di hello di nodi nel cluster hello. Questa operazione consente hello topologia tooadjust parallelismo toocompensate per hello aumentato o diminuito di numero di nodi nel cluster hello.

    Per ulteriori informazioni, vedere <a href="http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html" target="_blank">comprensione parallelismo hello di una topologia di Storm</a>.
  * **Kill**: termina una topologia di Storm dopo hello specificato timeout.
* **Statistiche di topologia**: le statistiche relative alla topologia di hello. tooset hello periodo di tempo per hello rimanenti voci nella pagina di hello, utilizzare i collegamenti di hello hello **finestra** colonna.
* **Spouts**: hello spouts utilizzato dalla topologia hello. Usare i collegamenti di hello in questa sezione di tooview ulteriori informazioni su spouts specifico.
* **Bulloni**: hello bulloni utilizzati dalla topologia hello. Usare i collegamenti di hello in questa sezione di tooview ulteriori informazioni su bulloni specifici.
* **Configurazione della topologia**: configurazione di hello della topologia hello selezionato.

### <a name="spout-and-bolt-summary"></a>Riepilogo di spout e bolt

Selezionando un beccuccio hello **Spouts** o **bulloni** sezioni Visualizza le seguenti informazioni sull'elemento selezionato hello hello:

* **Riepilogo dei componenti**: informazioni di base beccuccio hello o fulmine.
* **Statistiche beccuccio/fulmine**: le statistiche relative hello spout o bullone. tooset hello periodo di tempo per hello rimanenti voci nella pagina di hello, utilizzare i collegamenti di hello hello **finestra** colonna.
* **Statistiche di input** (solo bullone): informazioni su hello flussi utilizzati da fulmine hello di input.
* **Output statistiche**: informazioni sui flussi di hello generato da questo spout o bullone.
* **Executor**: informazioni sulle istanze di hello di beccuccio hello o fulmine. Seleziona hello **porta** voce per tooview un esecutore specifico prodotto un log delle informazioni di diagnostica per questa istanza.
* **Errors**: informazioni su eventuali errori dello spout o del bolt.

## <a name="monitor-and-manage-rest-api"></a>Monitorare e gestire: API REST

Hello Storm UI si basa su hello l'API REST per effettuare la gestione e il monitoraggio delle funzionalità tramite l'API REST hello simili. È possibile utilizzare strumenti personalizzati in toocreate hello API REST per la gestione e monitoraggio topologie Storm.

Per altre informazioni, vedere l'articolo relativo all'[API REST dell'interfaccia utente di Storm](http://storm.apache.org/releases/0.9.6/STORM-UI-REST-API.html). Hello informazioni seguenti sono specifici toousing hello API REST con Apache Storm in HDInsight.

> [!IMPORTANT]
> Hello Storm REST API non è disponibile pubblicamente su internet hello e deve essere accessibile tramite un SSH tunnel toohello HDInsight nodo head del cluster. Per informazioni sulla creazione e utilizzo di un tunnel SSH, vedere [tooaccess usare SSH Tunneling Ambari web dell'interfaccia utente, ResourceManager, JobHistory, NameNode, Oozie e altre interfacce utente web](hdinsight-linux-ambari-ssh-tunnel.md).

### <a name="base-uri"></a>URI di base

Hello URI di base per l'API REST di hello nei cluster HDInsight basati su Linux sono disponibili sul nodo head di hello in **https://HEADNODEFQDN:8744/api/v1/**. nome di dominio Hello del nodo head hello viene generato durante la creazione del cluster e non è statico.

È possibile trovare il nome di dominio completo hello (FQDN) per nodo head del cluster hello in diversi modi:

* **Da una sessione SSH**: utilizzare il comando hello `headnode -f` da un cluster di toohello sessione SSH.
* **Ambari Web**: selezionare **servizi** dalla parte superiore di hello della pagina di hello, quindi selezionare **Storm**. Da hello **riepilogo** , selezionare **Server dell'interfaccia utente di Storm**. Hello FQDN hello del nodo di cui è in esecuzione dell'interfaccia utente Storm hello e l'API REST è nella parte superiore di hello della pagina hello.
* **Dall'API REST Ambari**: utilizzare il comando hello `curl -u admin:PASSWORD -G "https://CLUSTERNAME.azurehdinsight.net/api/v1/clusters/CLUSTERNAME/services/STORM/components/STORM_UI_SERVER"` eseguono tooretrieve informazioni nodo hello hello Storm UI e l'API REST. Sostituire **PASSWORD** con password di amministratore hello per cluster hello. Sostituire **CLUSTERNAME** con il nome del cluster hello. In risposta hello, voce "host_name" hello contiene hello nome di dominio completo del nodo hello.

### <a name="authentication"></a>Autenticazione

Toohello richieste API REST è necessario utilizzare **l'autenticazione di base**, pertanto utilizzare nome amministratore del cluster HDInsight hello e una password.

> [!NOTE]
> Poiché l'autenticazione di base viene inviato con testo non crittografato, è necessario **sempre** utilizzare le comunicazioni HTTPS toosecure con cluster hello.

### <a name="return-values"></a>Valori restituiti

Informazioni restituite da hello API REST possono solo essere usata da all'interno di cluster hello o hello di macchine virtuali nella stessa rete virtuale di Azure come cluster hello. Nome di dominio completo hello (FQDN) restituito per i server Zookeeper è ad esempio, non essere accessibile da Internet hello.

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come topologie toodeploy e monitoraggio tramite hello Storm Dashboard, informazioni su come troppo[topologie basate sul linguaggio di sviluppo utilizzando Maven](hdinsight-storm-develop-java-topology.md).

Per un elenco di altre topologie di esempio, vedere [Esempi di topologie Storm per Apache Storm in HDInsight](hdinsight-storm-example-topology.md).
