---
title: aaaDeploy e gestire le topologie di Apache Storm in HDInsight | Documenti Microsoft
description: Informazioni su come toodeploy, monitorare e gestire le topologie di Apache Storm tramite Dashboard Storm hello in HDInsight. Utilizzare gli strumenti Hadoop per Visual Studio
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 5e542072-f014-42aa-82d6-2694a76df520
ms.service: hdinsight
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 03/01/2017
ms.author: larryfr
ROBOTS: NOINDEX
ms.openlocfilehash: 05f05fe8dd519fe99fb771d36bfc3d28168ca85f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-and-manage-apache-storm-topologies-on-windows-based-hdinsight"></a>Distribuire e gestire topologie Apache Storm in HDInsight basato su Windows

Hello Storm Dashboard consente tooeasily distribuire ed eseguire i cluster di HDInsight tooyour topologie Apache Storm tramite il web browser. È anche possibile utilizzare toomonitor dashboard hello e gestire topologie in esecuzione. Se si utilizza Visual Studio, hello HDInsight Tools per Visual Studio fornisce funzionalità simili in Visual Studio.

Hello Storm Dashboard e le funzionalità di Storm hello hello strumenti HDInsight si basano su hello Storm l'API REST che può essere utilizzato toocreate proprie soluzioni di monitoraggio e gestione.

> [!IMPORTANT]
> passaggi di Hello in questo documento richiedono un elevato numero di cluster HDInsight che usa Windows come sistema operativo hello. Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).
>
> Per informazioni sulla distribuzione e gestione di topologie Storm con un cluster HDInsight che usa Linux, vedere [Distribuzione e gestione di topologie Apache Storm in HDInsight basato su Linux](hdinsight-storm-deploy-monitor-topology-linux.md)

## <a name="prerequisites"></a>Prerequisiti

* **Apache Storm in HDInsight**: per i passaggi relativi alla creazione di un cluster, vedere [Introduzione ad Apache Storm con HDInsight](hdinsight-apache-storm-tutorial-get-started.md).

* Per hello **Dashboard Storm**: un browser web moderna che supporta HTML5.

* Per **Visual Studio** -Azure SDK 2.5.1 o versione successiva e hello strumenti HDInsight per Visual Studio. Vedere [iniziare a usare gli strumenti HDInsight per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md) tooinstall e configurare gli strumenti di HDInsight hello per Visual Studio.

    Una delle seguenti versioni di Visual Studio hello:

  * Visual Studio 2012 con Update 4

  * Visual Studio 2013 con Update 4 o Visual Studio 2013 Community

  * Visual Studio 2015, qualsiasi edizione

  * Visual Studio 2017, qualsiasi edizione

## <a name="storm-dashboard"></a>Storm Dashboard

Hello Storm Dashboard è una pagina web disponibile sul cluster Storm. URL di Hello è **https://&lt;clustername >.azurehdinsight.net/**, dove **clustername** è il nome di hello dell'elevato numero di cluster HDInsight.

Dall'alto hello di hello Storm Dashboard, selezionare **inviare topologia**. Seguire le istruzioni di hello su hello pagina toorun una topologia di esempio o tooupload ed eseguire una topologia in cui è stato creato.

![Hello Invia pagina topologia][storm-dashboard-submit]

### <a name="storm-ui"></a>Interfaccia utente di Storm

Hello Storm Dashboard, selezionare hello **dell'interfaccia utente Storm** collegamento. Consente di visualizzare informazioni sul cluster hello, tooany aggiunta in topologie di esecuzione.

![interfaccia utente di storm Hello][storm-dashboard-ui]

> [!NOTE]
> Con alcune versioni di Internet Explorer, si potrebbe scoprire che hello che Storm UI non comporta l'aggiornamento dopo aver visitato innanzitutto il. Ad esempio, potrebbe non visualizzate topologie nuovo hello è stato inviato o potrebbe mostrare una topologia come attivo quando precedente disattivazione. Microsoft è al corrente di questo problema e sta lavorando a una soluzione.

#### <a name="main-page"></a>Pagina principale

pagina principale di Hello di hello Storm UI fornisce hello le seguenti informazioni:

* **Riepilogo di cluster**: informazioni di base sui cluster Storm hello.

* **Topology summary**: elenco delle topologie in esecuzione. Utilizzare collegamenti hello in questa sezione di tooview ulteriori informazioni sulle topologie specifiche.

* **Riepilogo Supervisore**: informazioni su Supervisore Storm hello.

* **Configurazione nimbus**: configurazione di Nimbus per cluster hello.

#### <a name="topology-summary"></a>Topology summary

Quando si seleziona un collegamento da hello **riepilogo topologia** sezione sono visualizzate le seguenti informazioni sulla topologia di hello hello:

* **Topologia riepilogo**: le informazioni di base relative alla topologia di hello.

* **Azioni di topologia**: azioni di gestione che è possibile eseguire per la topologia hello.

  * **Activate**: riprende l'elaborazione di una topologia disattivata.

  * **Deactivate**: sospende una topologia in esecuzione.

  * **Ribilanciare**: consente di regolare il parallelismo hello della topologia hello. È necessario ribilanciare topologie in esecuzione dopo avere modificato il numero di hello di nodi nel cluster hello. In questo modo hello topologia tooadjust parallelismo toocompensate per hello aumentato o diminuito di numero di nodi nel cluster hello.

      Per ulteriori informazioni, vedere [comprensione parallelismo hello di una topologia di Storm (http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html)](http://storm.apache.org/documentation/Understanding-the-parallelism-of-a-Storm-topology.html).

  * **Kill**: termina una topologia di Storm dopo hello specificato timeout.

* **Statistiche di topologia**: le statistiche relative alla topologia di hello. Usare collegamenti hello hello **finestra** intervallo di tempo di colonna tooset hello per le voci nella pagina hello rimanenti hello.

* **Spouts**: hello spouts utilizzato dalla topologia hello. Usare i collegamenti di hello in questa sezione di tooview ulteriori informazioni su spouts specifico.

* **Bulloni**: hello bulloni utilizzati dalla topologia hello. Usare i collegamenti di hello in questa sezione di tooview ulteriori informazioni su bulloni specifici.

* **Configurazione della topologia**: configurazione di hello della topologia hello selezionato.

#### <a name="spout-and-bolt-summary"></a>Riepilogo di spout e bolt

Selezionando un beccuccio hello **Spouts** o **bulloni** sezioni Visualizza le seguenti informazioni sull'elemento selezionato hello hello:

* **Riepilogo dei componenti**: informazioni di base beccuccio hello o fulmine.

* **Statistiche beccuccio/fulmine**: le statistiche relative hello spout o bullone. Usare collegamenti hello hello **finestra** intervallo di tempo di colonna tooset hello per le voci nella pagina hello rimanenti hello.

* **Statistiche di input** (solo bullone): informazioni su hello flussi utilizzati da fulmine hello di input.

* **Output statistiche**: informazioni sui flussi di hello generato da questo spout o bullone.

* **Executor**: informazioni sulle istanze di hello di beccuccio hello o fulmine. Seleziona hello **porta** voce per tooview un esecutore specifico prodotto un log delle informazioni di diagnostica per questa istanza.

* **Errors**: informazioni su eventuali errori dello spout o del bolt.

## <a name="hdinsight-tools-for-visual-studio"></a>HDInsight Tools per Visual Studio

gli strumenti di HDInsight Hello può essere utilizzato toosubmit c# o ibrida topologie tooyour cluster Storm. Hello alla procedura seguente usa un'applicazione di esempio. Per informazioni sulla creazione di propri topologie utilizzando gli strumenti di HDInsight hello, vedere [c# sviluppare topologie in hello HDInsight Tools per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md).

Utilizzare hello seguendo i passaggi toodeploy tooyour un esempio Storm nel cluster HDInsight, quindi visualizzare e gestire la topologia di hello.

1. Se non è già installato hello versione hello strumenti HDInsight per Visual Studio, vedere [iniziare a usare gli strumenti HDInsight per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

2. Aprire Visual Studio e selezionare **File** > **Nuovo** > **Progetto**.

3. In hello **nuovo progetto** finestra di dialogo espandere **installato** > **modelli**, quindi selezionare **HDInsight**. Selezionare nell'elenco dei modelli di hello **Storm esempio**. Nella parte inferiore di hello della finestra di dialogo hello, digitare un nome per un'applicazione hello.

    ![immagine](./media/hdinsight-storm-deploy-monitor-topology/sample.png)

4. In **Esplora**, fare clic sul progetto hello e selezionare **inviare tooStorm in HDInsight**.

   > [!NOTE]
   > Se richiesto, immettere le credenziali di accesso hello per la sottoscrizione di Azure. Se si dispone di più di una sottoscrizione, accedere toohello uno che contiene l'elevato numero di cluster HDInsight.

5. Selezionare l'elevato numero di cluster HDInsight da hello **Cluster Storm** elenco a discesa e quindi selezionare **Invia**. È possibile controllare se l'invio di hello ha esito positivo tramite hello **Output** finestra.

6. Quando la topologia hello è stata inviata correttamente, hello **Storm topologie** per cluster hello devono essere visualizzati. Selezionare la topologia hello hello elenco tooview informazioni hello in esecuzione sulla topologia.

    ![monitor Visual Studio](./media/hdinsight-storm-deploy-monitor-topology/vsmonitor.png)

   > [!NOTE]
   > È possibile visualizzare **Storm Topologies** anche da **Esplora server**, espandendo **Azure** > **HDInsight** e quindi facendo clic su un cluster Storm in HDInsight e selezionando **View Storm Topologies**.

    Selezionare la forma hello per hello spouts o bulloni tooview informazioni su questi componenti. Viene aperta una nuova finestra per ogni elemento selezionato.

   > [!NOTE]
   > nome Hello della topologia hello è il nome di classe hello della topologia hello (in questo caso, `HelloWord`,) con un timestamp aggiunto.

7. Da hello **topologia riepilogo** visualizzazione, selezionare **Kill** topologia hello toostop.

   > [!NOTE]
   > Topologie di Storm continuano l'esecuzione fino a quando non vengono arrestati o hello cluster verrà eliminato.


## <a name="rest-api"></a>API REST

Hello Storm UI si basa su hello l'API REST per effettuare la gestione e il monitoraggio delle funzionalità tramite l'API REST hello simili. È possibile utilizzare strumenti personalizzati in toocreate hello API REST per la gestione e monitoraggio topologie Storm.

Per altre informazioni, vedere l'articolo relativo all'[API REST dell'interfaccia utente di Storm](https://github.com/apache/storm/blob/0.9.3-branch/STORM-UI-REST-API.md). Hello informazioni seguenti sono specifici toousing hello API REST con Apache Storm in HDInsight.

### <a name="base-uri"></a>URI di base

URI di base per l'API REST di hello nei cluster HDInsight è Hello **https://&lt;clustername >.azurehdinsight.net/stormui/api/v1/**, dove **clustername** è il nome di hello dell'elevato numero di in Cluster HDInsight.

### <a name="authentication"></a>Autenticazione

Toohello richieste API REST è necessario utilizzare **l'autenticazione di base**, pertanto utilizzare nome amministratore del cluster HDInsight hello e una password.

> [!NOTE]
> Poiché l'autenticazione di base viene inviato con testo non crittografato, è necessario **sempre** utilizzare le comunicazioni HTTPS toosecure con cluster hello.

### <a name="return-values"></a>Valori restituiti

Informazioni restituite da hello API REST possono solo essere usata da all'interno di cluster hello o hello di macchine virtuali nella stessa rete virtuale di Azure come cluster hello. Nome di dominio completo hello (FQDN) restituito per i server Zookeeper sono ad esempio, non essere accessibile da Internet hello.

## <a name="next-steps"></a>Passaggi successivi

Ora che si è appreso come topologie toodeploy e monitoraggio tramite hello Storm Dashboard, informazioni su come:

* [Sviluppare c# topologie in hello HDInsight Tools per Visual Studio](hdinsight-storm-develop-csharp-visual-studio-topology.md)

* [Sviluppare topologie basate su Java per Apache Storm in HDInsight](hdinsight-storm-develop-java-topology.md)

Per un elenco di altre topologie di esempio, vedere [Esempi di topologie Storm per Apache Storm in HDInsight](hdinsight-storm-example-topology.md).

[hdinsight-dashboard]: ./media/hdinsight-storm-deploy-monitor-topology/dashboard-link.png
[storm-dashboard-submit]: ./media/hdinsight-storm-deploy-monitor-topology/submit.png
[storm-dashboard-ui]: ./media/hdinsight-storm-deploy-monitor-topology/storm-ui-summary.png
