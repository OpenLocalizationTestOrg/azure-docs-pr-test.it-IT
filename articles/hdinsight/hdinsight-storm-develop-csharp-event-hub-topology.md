---
title: eventi aaaProcess dagli hub eventi con Storm - HDInsight di Azure | Documenti Microsoft
description: Informazioni su come dati tooprocess dagli hub di eventi di Azure con una topologia c# Storm create in Visual Studio, utilizzando hello strumenti HDInsight per Visual Studio.
services: hdinsight,notification hubs
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
ms.assetid: 67f9d08c-eea0-401b-952b-db765655dad0
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: 30cd910d80eba066f283197bcbbaf11145bc5524
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="process-events-from-azure-event-hubs-with-storm-on-hdinsight-c"></a>Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (C#)

Informazioni su come toowork con hub di eventi di Azure da Apache Storm in HDInsight. Questo documento viene utilizzato un elevato numero di c# topologia tooread e scrittura dati dagli hub Evbent

> [!NOTE]
> Per la versione Java di questo progetto, vedere [Elaborare eventi dell'hub eventi di Azure con Storm in HDInsight (Java)](hdinsight-storm-develop-java-event-hub-topology.md).

## <a name="scpnet"></a>SCP.NET

passaggi di Hello in questo documento usano SCP.NET, un pacchetto NuGet che rende facile toocreate c# topologie e componenti per l'utilizzo con Storm in HDInsight.

> [!IMPORTANT]
> Anche se hello i passaggi in questo documento si basano su un ambiente di sviluppo Windows con Visual Studio, progetto compilato hello può essere inviato tooa Storm nel cluster HDInsight che utilizza Linux. Solo i cluster basati su Linux creati dopo il 28 ottobre 2016 supportano le topologie SCP.NET.

HDInsight 3.4 e maggiore utilizzo Mono toorun c# topologie. esempio Hello utilizzato in questo documento illustra 3.6 di HDInsight. Se si prevede la creazione di soluzioni di .NET per HDInsight, controllare hello [compatibilità Mono](http://www.mono-project.com/docs/about-mono/compatibility/) documento per potenziali problemi di incompatibilità.

### <a name="cluster-versioning"></a>Controllo delle versioni del cluster

Hello pacchetto Microsoft.SCP.Net.SDK NuGet usato per il progetto deve corrispondere versione principale di hello di Storm installato in HDInsight. HDInsight versioni 3.5 e 3.6 usa Storm versione 1.x, pertanto è necessario usare SCP.NET versione 1.0.x.x con questi cluster.

> [!IMPORTANT]
> esempio Hello in questo documento è previsto un 3.5 HDInsight o 3,6 cluster.
>
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

Le topologie C# devono inoltre puntare a .NET 4.5.

## <a name="how-toowork-with-event-hubs"></a>Come toowork con hub eventi

Microsoft fornisce un set di componenti Java che possono essere utilizzati toocommunicate con hub di eventi da una topologia di Storm. È possibile trovare i file di archivio (JAR) di Java hello che contiene una versione compatibile di HDInsight 3.6 di questi componenti in [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

> [!IMPORTANT]
> Mentre i componenti di hello sono scritti in Java, è possibile utilizzarli da una topologia c#.

in questo esempio viene utilizzato i Hello seguenti componenti:

* __EventHubSpout__: legge i dati dagli Hub eventi.
* __EventHubBolt__: scrive dati tooEvent hub.
* __EventHubSpoutConfig__: tooconfigure EventHubSpout utilizzato.
* __EventHubBoltConfig__: tooconfigure EventHubBolt utilizzato.

### <a name="example-spout-usage"></a>Esempio di uso di uno spout

SCP.NET fornisce metodi per l'aggiunta di una topologia di tooyour EventHubSpout. Questi metodi rendono più semplice tooadd beccuccio rispetto all'utilizzo di metodi generici hello per l'aggiunta di un componente di Java. Hello esempio seguente viene illustrato come toocreate beccuccio utilizzando hello __SetEventHubSpout__ e **EventHubSpoutConfig** metodi forniti da SCP.NET:

```csharp
 topologyBuilder.SetEventHubSpout(
    "EventHubSpout",
    new EventHubSpoutConfig(
        ConfigurationManager.AppSettings["EventHubSharedAccessKeyName"],
        ConfigurationManager.AppSettings["EventHubSharedAccessKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        ConfigurationManager.AppSettings["EventHubEntityPath"],
        eventHubPartitions),
    eventHubPartitions);
```

esempio di Hello precedente crea un nuovo componente di beccuccio denominato __EventHubSpout__e lo configura toocommunicate con un hub eventi. Hello parallelismo per il componente hello è impostato toohello numero di partizioni nell'hub eventi hello. Questa impostazione consente di Storm toocreate un'istanza del componente hello per ogni partizione.

### <a name="example-bolt-usage"></a>Esempio di utilizzo di bolt

Hello utilizzare **JavaComponmentConstructor** toocreate metodo un'istanza di fulmine hello. Hello esempio seguente viene illustrato come toocreate e configurare una nuova istanza di hello **EventHubBolt**:

```csharp
// Java construcvtor for hello Event Hub Bolt
JavaComponentConstructor constructor = JavaComponentConstructor.CreateFromClojureExpr(
    String.Format(@"(org.apache.storm.eventhubs.bolt.EventHubBolt. (org.apache.storm.eventhubs.bolt.EventHubBoltConfig. " +
        @"""{0}"" ""{1}"" ""{2}"" ""{3}"" ""{4}"" {5}))",
        ConfigurationManager.AppSettings["EventHubPolicyName"],
        ConfigurationManager.AppSettings["EventHubPolicyKey"],
        ConfigurationManager.AppSettings["EventHubNamespace"],
        "servicebus.windows.net",
        ConfigurationManager.AppSettings["EventHubName"],
        "true"));

// Set hello bolt toosubscribe toodata from hello spout
topologyBuilder.SetJavaBolt(
    "eventhubbolt",
    constructor,
    partitionCount)
        .shuffleGrouping("Spout");
```

> [!NOTE]
> In questo esempio viene utilizzata un'espressione di Clojure passata come stringa, anziché utilizzare **JavaComponentConstructor** toocreate un **EventHubBoltConfig**, come esempio beccuccio hello. Entrambi i metodi sono validi Utilizzare il metodo hello che ritiene tooyou migliore.

## <a name="download-hello-completed-project"></a>Scaricare il progetto hello completata

È possibile scaricare una versione completa di hello progetto creato in questa esercitazione da [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub). Tuttavia, è comunque necessario tooprovide le impostazioni di configurazione seguendo i passaggi di hello in questa esercitazione.

### <a name="prerequisites"></a>Prerequisiti

* Un [cluster Apache Storm in HDInsight versione 3.5 o 3.6](hdinsight-apache-storm-tutorial-get-started.md).

    > [!WARNING]
    > esempio Hello utilizzato in questo documento richiede Storm in HDInsight versione 3.5 o 3.6. Questo non funziona con le versioni precedenti di HDInsight, a causa di modifiche al nome di classe toobreaking. Per una versione di questo esempio funziona con i cluster precedenti, vedere [GitHub](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub/releases).

* Un [Hub eventi di Azure](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

* Hello [Azure .NET SDK](http://azure.microsoft.com/downloads/).

* Hello [strumenti HDInsight per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Java JDK 1.8 o versione successiva nell'ambiente di sviluppo. Sono disponibili download di JDK da [Oracle](http://www.oracle.com/technetwork/java/javase/downloads/index.html).

  * Hello **JAVA_HOME** directory di toohello punto deve variabile di ambiente contenente Java.
  * Hello **%JAVA_HOME%/bin** directory deve trovarsi nel percorso di hello.

## <a name="download-hello-event-hubs-components"></a>Scaricare i componenti di hello hub eventi

Download hello hub eventi spout e bullone componente da [https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar](https://github.com/hdinsight/mvn-repo/raw/master/org/apache/storm/storm-eventhubs/1.1.0.1/storm-eventhubs-1.1.0.1.jar).

Creare una directory denominata `eventhubspout`e salvarlo nella directory hello hello.

## <a name="configure-event-hubs"></a>Configurare gli hub eventi

Hub eventi è l'origine dati hello per questo esempio. Utilizzare le informazioni di hello nella sezione "Creare un hub eventi" hello di [Introduzione agli hub di eventi](../event-hubs/event-hubs-csharp-ephcs-getstarted.md).

1. Dopo aver creato l'hub di eventi hello, visualizzare hello **EventHub** pannello in hello Azure portale e selezionare **criteri di accesso condiviso**. Selezionare **+ Aggiungi** hello tooadd seguenti criteri:

   | Nome | Autorizzazioni |
   | --- | --- |
   | writer |Invio |
   | reader |Attesa |

    ![Schermata della finestra Criteri di accesso condivisi](./media/hdinsight-storm-develop-csharp-event-hub-topology/sas.png)

2. Seleziona hello **lettore** e **writer** criteri. Copiare e salvare hello chiave primaria per entrambi i criteri, questi valori vengono utilizzati in un secondo momento.

## <a name="configure-hello-eventhubwriter"></a>Configurare hello EventHubWriter

1. Se non è già installato più recente degli strumenti di HDInsight hello hello per Visual Studio, vedere [iniziare a usare gli strumenti HDInsight per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Download soluzione di hello da [eventhub-storm-ibrida](https://github.com/Azure-Samples/hdinsight-dotnet-java-storm-eventhub).

3. In hello **EventHubWriter** progetto, aprire hello **app** file. Utilizzare le informazioni di hello da hub di eventi hello di configurato toofill precedenti valore hello hello seguenti chiavi:

   | Chiave | Valore |
   | --- | --- |
   | EventHubPolicyName |Writer (se è utilizzato un nome diverso per i criteri di hello con *inviare* autorizzazione, utilizzare tale.) |
   | EventHubPolicyKey |chiave di Hello per criteri di writer hello. |
   | EventHubNamespace |spazio dei nomi Hello contenente dell'hub eventi. |
   | EventHubName |Nome dell'hub eventi. |
   | EventHubPartitionCount |numero di Hello di partizioni nell'hub eventi. |

4. Salvare e chiudere hello **app** file.

## <a name="configure-hello-eventhubreader"></a>Configurare hello EventHubReader

1. Aprire hello **EventHubReader** progetto.

2. Aprire hello **app** file per hello **EventHubReader**. Utilizzare le informazioni di hello da hub di eventi hello di configurato toofill precedenti valore hello hello seguenti chiavi:

   | Chiave | Valore |
   | --- | --- |
   | EventHubPolicyName |lettura (se è utilizzato un nome diverso per i criteri di hello con *ascolto* autorizzazione, utilizzare tale.) |
   | EventHubPolicyKey |chiave di Hello per criteri di lettore hello. |
   | EventHubNamespace |spazio dei nomi Hello contenente dell'hub eventi. |
   | EventHubName |Nome dell'hub eventi. |
   | EventHubPartitionCount |numero di Hello di partizioni nell'hub eventi. |

3. Salvare e chiudere hello **app** file.

## <a name="deploy-hello-topologies"></a>Distribuire le topologie di hello

1. Da **Esplora**, hello rapida **EventHubReader** del progetto e selezionare **inviare tooStorm in HDInsight**.

    ![Schermata di Esplora soluzioni con tooStorm invia in HDInsight evidenziato](./media/hdinsight-storm-develop-csharp-event-hub-topology/submittostorm.png)

2. In hello **inviare topologia** la finestra di dialogo, seleziona il **Cluster Storm**. Espandere **configurazioni aggiuntive**selezionare **i percorsi di File Java**selezionare **...** e selezionare hello directory che contiene i file JAR hello che è stato scaricato in precedenza. Infine fare clic su **Submit**.

    ![Schermata della finestra di dialogo Submit Topology (Invia topologia)](./media/hdinsight-storm-develop-csharp-event-hub-topology/submit.png)

3. Quando è stata inviata la topologia hello, hello **Storm topologie Visualizzatore** viene visualizzato. tooview informazioni sulla topologia di hello, seleziona hello **EventHubReader** topologia nel riquadro di sinistra hello.

    ![Schermata Storm Topologies Viewer (Visualizzatore topologie Storm)](./media/hdinsight-storm-develop-csharp-event-hub-topology/topologyviewer.png)

4. Da **Esplora**, hello rapida **EventHubWriter** del progetto e selezionare **inviare tooStorm in HDInsight**.

5. In hello **inviare topologia** la finestra di dialogo, seleziona il **Cluster Storm**. Espandere **configurazioni aggiuntive**selezionare **i percorsi di File Java**selezionare **...** , e le directory hello select che contiene i file JAR hello scaricato in precedenza. Infine fare clic su **Submit**.

6. Quando è stata inviata la topologia hello, aggiornare l'elenco di topologia di hello in hello **Storm topologie Visualizzatore** tooverify che entrambe le topologie sono in esecuzione nel cluster di hello.

7. In **Storm topologie Visualizzatore**selezionare hello **EventHubReader** topologia.

8. componente hello tooopen riepilogo fulmine hello, fare doppio clic su hello **LogBolt** componente nel diagramma hello.

9. In hello **executor** , selezionare uno dei collegamenti hello in hello **porta** colonna. Consente di visualizzare informazioni registrate dal componente hello. informazioni di Hello registrato sono simile toohello seguente testo:

        2017-03-02 14:51:29.255 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,255 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1830978598,"deviceId":"8566ccbc-034d-45db-883d-d8a31f34068e"}
        2017-03-02 14:51:29.283 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,283 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1756413275,"deviceId":"647a5eff-823d-482f-a8b4-b95b35ae570b"}
        2017-03-02 14:51:29.313 m.s.p.TaskHost [INFO] Received C# STDOUT: 2017-03-02 14:51:29,312 [1] INFO  EventHubReader_LogBolt [(null)] - Received data: {"deviceValue":1108478910,"deviceId":"206a68fa-8264-4d61-9100-bfdb68ee8f0a"}

## <a name="stop-hello-topologies"></a>Arrestare le topologie di hello

le topologie hello toostop, selezionare ogni topologia hello **Visualizzatore della topologia Storm**, quindi fare clic su **Kill**.

![Schermata Storm Topology Viewer (Visualizzatore topologie Storm), con il pulsante Kill (Termina) evidenziato](./media/hdinsight-storm-develop-csharp-event-hub-topology/killtopology.png)

## <a name="delete-your-cluster"></a>Eliminare il cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Passaggi successivi

In questo documento, si è appreso come toouse hello Java hub eventi spout e bullone da toowork una topologia c# con i dati in hub eventi di Azure. toolearn informazioni sulla creazione di topologie di c#, vedere l'esempio hello:

* [Sviluppare topologie C# per Apache Storm in HDInsight tramite Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)
* [Guida alla programmazione SCP](hdinsight-storm-scp-programming-guide.md)
* [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md)
