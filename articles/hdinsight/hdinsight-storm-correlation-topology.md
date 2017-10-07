---
title: eventi aaaCorrelate nel tempo con Storm e HBase in HDInsight
description: Informazioni su come toocorrelate eventi che arrivano in momenti diversi tramite Storm e HBase in HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 17d11479-2d02-4790-8d29-05fb38351479
ms.service: hdinsight
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/07/2017
ms.author: larryfr
ms.custom: H1Hack27Feb2017,hdinsightactive
ms.openlocfilehash: f915eef77bbda5b02bfd02ad0b5a4923ff2f4f26
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="correlate-events-that-arrive-at-different-times-using-storm-and-hbase"></a>Correlare eventi che arrivano in momenti diversi tramite Storm e HBase

Utilizzando un archivio dati permanente con Apache Storm, è possibile correlare le voci di dati che arrivano in momenti diversi. Ad esempio, collegamento eventi di accesso e disconnessione per un toocalculate sessione utente come sessione hello di lunga durata.

Nel presente documento, si apprenderà come toocreate una topologia c# tempesta di base che tiene traccia di eventi di accesso e disconnessione per le sessioni utente e viene calcolata hello durata della sessione hello. topologia di Hello utilizza HBase come archivio dati persistente. HBase consente inoltre query batch tooperform nella raccolta di informazioni aggiuntive hello dati cronologici tooproduce. ad esempio il numero di sessioni utente avviate o terminate in un determinato periodo di tempo.

## <a name="prerequisites"></a>Prerequisiti

* Visual Studio e hello gli strumenti HDInsight per Visual Studio. Per ulteriori informazioni, vedere [iniziare a usare gli strumenti di HDInsight hello per Visual Studio](hdinsight-hadoop-visual-studio-tools-get-started.md).

* Cluster Apache Storm in HDInsight, basato su Windows.

  > [!WARNING]
  > Mentre SCP.NET topologie sono supportate nei cluster basati su Linux Storm creato dopo il 10/28/2016, hello HBase SDK per il pacchetto .NET disponibile a partire da 28/10/2016 non funziona correttamente in HDInsight basati su Linux

* Cluster Apache HBase in HDInsight, basato su Linux o su Windows.

  > [!IMPORTANT]
  > Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).

* [Java](https://java.com) 1.7 o versione successiva nell'ambiente di sviluppo. Java è topologia hello toopackage utilizzato quando è cluster HDInsight toohello inviato.

  * Hello **JAVA_HOME** directory di toohello punto deve variabile di ambiente contenente Java.
  * Hello **%JAVA_HOME%/bin** directory deve trovarsi nel percorso hello

## <a name="architecture"></a>Architettura

![Diagramma di flusso di dati hello attraverso topologia hello](./media/hdinsight-storm-correlation-topology/correlationtopology.png)

Correlazione di eventi, è necessario un identificatore comune per l'origine evento hello. Ad esempio, un ID utente, ID di sessione o altro dato che è un) univoci e b) incluso in tutti i dati inviati tooStorm. Questo esempio viene utilizzato un toorepresent valore GUID un ID sessione.

Questo esempio è costituito da due cluster di HDInsight:

* HBase: archivio dati permanente per i dati cronologici
* Storm: utilizzare i dati in arrivo tooingest

dati Hello viene generati in modo casuale dalla topologia Storm hello ed è costituito da hello seguenti elementi:

* ID di sessione: un GUID che identifica in modo univoco ogni sessione
* Evento: un evento START o END. Per questo esempio, l'evento START si verifica sempre prima dell'evento END
* Ora: hello ora di hello evento.

Questi dati vengono elaborati e archiviati in HBase.

### <a name="storm-topology"></a>Topologia Storm

Quando si avvia una sessione, un **avviare** evento viene ricevuto dalla topologia hello e registrato tooHBase. Quando un **fine** viene ricevuto l'evento, la topologia hello recupera hello **avviare** evento e calcola il tempo di hello tra gli eventi di hello due. Questo **durata** valore verrà quindi archiviato in HBase insieme hello **fine** informazioni sull'evento.

> [!IMPORTANT]
> Durante questa topologia illustra modello di base hello, una soluzione di produzione sarà necessario progettazione tootake per hello seguenti scenari:
>
> * Eventi che arrivano nell'ordine errato
> * Eventi duplicati
> * Eventi eliminati

topologia di esempio Hello è costituita da hello seguenti componenti:

* Session.cs: simula una sessione utente tramite la creazione di un ID di sessione casuale, inizio hello tempo e la durata della sessione hanno una durata.

* Spout.cs: crea 100 sessioni, genera un evento di inizio, hello casuale timeout in attesa per ogni sessione e quindi genera un evento di fine. Quindi ricicli terminata sessioni toogenerate nuovi.

* HBaseLookupBolt.cs: Usa toolook ID di sessione hello le informazioni di sessione da HBase. Quando viene elaborato un evento di fine, trova hello corrispondente evento di inizio e hello durata della sessione hello viene calcolata.

* HBaseBolt.cs: archivia le informazioni in HBase.

* TypeHelper.cs: Consente con conversione del tipo durante la lettura / scrittura tooHBase.

### <a name="hbase-schema"></a>Schema HBase

In HBase, hello vengono archiviati in una tabella con hello/impostazioni di schema seguente:

* Chiave di riga: hello ID sessione è usato come chiave hello per le righe in questa tabella.

* Famiglia di colonna: nome della famiglia hello è 'cf'. Le colonne memorizzate in questo gruppo sono le seguenti:

  * event: START o END.

  * ora: si è verificato il tempo di hello in millisecondi che hello evento.

  * durata: hello di lunghezza compresa tra eventi di inizio e di fine.

* Le versioni: famiglia 'cf' hello è impostata tooretain 5 versioni di ogni riga.

  > [!NOTE]
  > Le versioni sono un registro dei valori precedentemente memorizzati per una chiave di riga specifica. Per impostazione predefinita, HBase restituisce solo il valore di hello per la versione più recente di hello di una riga. In questo caso, hello stessa riga viene utilizzata per tutti gli eventi (inizio, fine) ogni versione di una riga viene identificato dal valore di timestamp hello. Le versioni forniscono una visualizzazione cronologica degli eventi registrati per un ID specifico.

## <a name="download-hello-project"></a>Scaricare il progetto hello

progetto di esempio Hello può essere scaricato da [https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation](https://github.com/Azure-Samples/hdinsight-storm-dotnet-event-correlation).

Questo download contiene hello c# progetti seguenti:

* CorrelationTopology: topologia Storm di C# che casualmente genera eventi di inizio e di fine per le sessioni utente. La durata di ogni sessione è compresa tra 1 e 5 minuti.

* SessionInfo: Applicazione console c# che crea una tabella HBase hello e fornisce query di esempio tooreturn informazioni sui dati di sessione.

## <a name="create-hello-table"></a>Creare la tabella hello

1. Aprire hello **SessionInfo** progetto in Visual Studio.

2. In **Esplora**, hello rapida **SessionInfo** del progetto e selezionare **proprietà**.

    ![Schermata del menu con le proprietà selezionate](./media/hdinsight-storm-correlation-topology/selectproperties.png)

3. Selezionare **impostazioni**, quindi hello set seguenti valori:

   * HBaseClusterURL: cluster di HBase tooyour URL hello. Ad esempio, https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: account utente di amministrazione/HTTP hello per il cluster

   * HBaseClusterPassword: password di hello per l'account utente di amministrazione/HTTP hello

   * HBaseTableName: nome di hello hello tabella toouse con questo esempio

   * HBaseTableColumnFamily: nome della famiglia colonna hello

     ![Finestra di dialogo delle impostazioni di connessione](./media/hdinsight-storm-correlation-topology/settings.png)

4. Eseguire la soluzione hello. Quando richiesto, selezionare una tabella di hello toocreate chiave "c" hello sul cluster HBase.

## <a name="build-and-deploy-hello-storm-topology"></a>Compilare e distribuire una topologia di Storm hello

1. Aprire hello **CorrelationTopology** soluzione in Visual Studio.

2. In **Esplora**, hello rapida **CorrelationTopology** del progetto e scegliere Proprietà.

3. Nella finestra Proprietà hello selezionare **impostazioni** e immettere i valori di configurazione hello per questo progetto. primi 5 Hello sono hello stessi valori utilizzati per hello **SessionInfo** progetto:

   * HBaseClusterURL: cluster di HBase tooyour URL hello. Ad esempio, https://myhbasecluster.azurehdinsight.net.

   * HBaseClusterUserName: hello admin/HTTP account utente per il cluster.

   * HBaseClusterPassword: password di hello per l'account utente di amministrazione/HTTP hello.

   * HBaseTableName: hello Nome hello tabella toouse con questo esempio. Questo valore è hello stesso nome di tabella utilizzato nel progetto SessionInfo hello.

   * HBaseTableColumnFamily: nome della famiglia hello colonna. Questo valore è hello stesso nome della famiglia di colonna utilizzato nel progetto SessionInfo hello.

   > [!IMPORTANT]
   > Non modificare hello HBaseTableColumnNames, come valori predefiniti di hello sono nomi hello utilizzati dal **SessionInfo** tooretrieve dati.

4. Salvare le proprietà di hello, quindi compilare il progetto hello.

5. In **Esplora**, fare clic sul progetto hello e selezionare **inviare tooStorm in HDInsight**. Se richiesto, immettere le credenziali di hello per la sottoscrizione di Azure.

   ![Immagine di hello inviare la voce di menu toostorm](./media/hdinsight-storm-correlation-topology/submittostorm.png)

6. In hello **inviare topologia** finestra di dialogo, cluster Storm hello selezionare desiderato toodeploy questa topologia.

   > [!NOTE]
   > Hello prima volta che si invia una topologia, potrebbe richiedere alcuni secondi nome hello tooretrieve dei cluster HDInsight.

7. Dopo aver caricato e inviato toohello cluster topologia hello, hello **vista topologia Storm** aprirà e visualizzerà hello in esecuzione sulla topologia. dati hello toorefresh, seleziona hello **CorrelationTopology** e utilizzare il pulsante di aggiornamento hello hello in alto a destra della pagina hello.

   ![Immagine di vista della topologia hello](./media/hdinsight-storm-correlation-topology/topologyview.png)

   Quando inizia la topologia di hello la generazione di dati, hello valore hello **emessa** colonna viene incrementato.

   > [!NOTE]
   > Se hello **vista topologia Storm** non viene aperto automaticamente, usare hello seguendo i passaggi tooopen:
   >
   > 1. Da **Esplora soluzioni** espandere **Azure**, quindi **HDInsight**.
   > 2. È in esecuzione nel cluster che hello topologia Storm di hello pulsante destro del mouse e quindi selezionare **visualizzazione Storm topologie**

## <a name="query-hello-data"></a>Eseguire query sui dati hello

Una volta dati sono stato emesso, utilizzare hello passaggi tooquery hello dati seguenti.

1. Restituire toohello **SessionInfo** progetto. Se non in esecuzione, avviare una nuova istanza.

2. Quando richiesto, selezionare **s** toosearch per eventi di avvio. Si tooenter richiesta un inizio e fine ora toodefine un intervallo di tempo, vengono restituiti solo gli eventi tra questi due volte.

    Seguente hello utilizzare formato quando si immette inizio hello e di fine: hh: mm e 'M'' o 'pm'. Ad esempio, 11:20 pm.

    gli eventi tooreturn registrato, viene utilizzato da un'ora di inizio prima hello Storm topologia è stata distribuita e un'ora di fine dell'ora. Restituisce i dati Hello contengano toohello di voci simili seguente testo:

        Session e6992b3e-79be-4991-afcf-5cb47dd1c81c started at 6/5/2015 6:10:15 PM. Timestamp = 1433527820737

Ricerca di hello works gli eventi di fine stesso come eventi di avvio. Tuttavia, gli eventi di fine vengono generati in modo casuale compreso tra 1 e 5 minuti dopo l'evento di inizio hello. È possibile tootry qualche tempo intervalli toofind hello gli eventi di fine. Inoltre, gli eventi di fine contengano durata hello della sessione hello - differenza hello hello evento ora inizio e fine evento. Di seguito è riportato un esempio di dati per gli eventi END:

    Session fc9fa8e6-6892-4073-93b3-a587040d892e lasted 2 minutes, and ended at 6/5/2015 6:12:15 PM

> [!NOTE]
> Anche se si immette i valori di ora hello sono nell'ora locale, ora hello restituito dalla query hello è in UTC.

## <a name="stop-hello-topology"></a>Arrestare la topologia hello

Quando si è pronti toostop topologia di hello, restituire toohello **CorrelationTopology** progetto in Visual Studio. In hello **vista topologia Storm**, selezionare la topologia hello e quindi usare hello **Kill** pulsante nella parte superiore di hello della vista della topologia hello.

## <a name="delete-your-cluster"></a>Eliminare il cluster

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="next-steps"></a>Passaggi successivi

Per altri esempi di Storm, vedere [Topologie di esempio per Storm in HDInsight](hdinsight-storm-example-topology.md).
