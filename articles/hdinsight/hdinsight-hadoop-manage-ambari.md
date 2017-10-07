---
title: aaaMonitor e la gestione di Azure HDInsight con Ambari Web UI | Documenti Microsoft
description: "Informazioni su come toouse Ambari toomonitor e gestire cluster HDInsight basati su Linux. Nel presente documento, si apprenderà come cluster di hello toouse dell'interfaccia utente Web Ambari incluso in HDInsight."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4787f3cc-a650-4dc3-9d96-a19a67aad046
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: d422c40e63345d7054839a625e115c50dad040f9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hdinsight-clusters-by-using-hello-ambari-web-ui"></a>Gestire cluster HDInsight con Ambari Web UI hello

[!INCLUDE [ambari-selector](../../includes/hdinsight-ambari-selector.md)]

Ambari Apache semplifica la gestione hello e monitoraggio di un cluster Hadoop fornendo un web toouse semplice interfaccia utente e REST API. Ambari è incluso nei cluster HDInsight basati su Linux ed è utilizzato toomonitor hello cluster e apportare modifiche di configurazione.

In questo documento viene illustrato come toouse hello dell'interfaccia utente Web Ambari con un cluster HDInsight.

## <a id="whatis"></a>Cos'è Ambari?

[Apache Ambari](http://ambari.apache.org) semplifica la gestione di Hadoop, fornendo un'interfaccia utente Web di facile utilizzo. È possibile usare Ambari per creare, gestire e monitorare cluster Hadoop. Gli sviluppatori possono integrare queste funzionalità nelle proprie applicazioni utilizzando hello [API REST Ambari](https://github.com/apache/ambari/blob/trunk/ambari-server/docs/api/v1/index.md).

interfaccia utente Web Ambari Hello viene fornito per impostazione predefinita con i cluster HDInsight che utilizzano il sistema operativo Linux di hello.

> [!IMPORTANT]
> Linux è hello solo sistema operativo utilizzato in HDInsight versione 3.4 o successiva. Per altre informazioni, vedere la sezione relativa al [ritiro di HDInsight in Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement). 

## <a name="connectivity"></a>Connettività

interfaccia utente Web Ambari Hello è disponibile nel cluster HDInsight in HTTPS://CLUSTERNAME.azurehdidnsight.net, in cui **CLUSTERNAME** hello nome del cluster.

> [!IMPORTANT]
> Connessione tooAmbari in HDInsight richiede HTTPS. Quando richiesto per l'autenticazione, utilizzare nome dell'account admin hello e la password forniti quando è stato creato il cluster di hello.

## <a name="ssh-tunnel-proxy"></a>Tunnel SSH (proxy)

Mentre Ambari per il cluster è accessibile direttamente su Internet hello, alcuni collegamenti da hello dell'interfaccia utente Web Ambari (ad esempio toohello JobTracker) non sono esposte in hello internet. tooaccess questi servizi, è necessario creare un tunnel SSH. Per altre informazioni, vedere [Usare il tunneling SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).

## <a name="ambari-web-ui"></a>Interfaccia utente Web Ambari

Durante la connessione dell'interfaccia utente Web Ambari toohello, verrà richiesta tooauthenticate toohello pagina. Utilizzare l'utente di amministrazione cluster hello (impostazione predefinita Admin) e la password utilizzati durante la creazione del cluster.

Quando si apre la pagina hello, si noti la barra hello nella parte superiore di hello. Questa barra contiene seguente hello informazioni e i controlli:

![ambari-nav](./media/hdinsight-hadoop-manage-ambari/ambari-nav.png)

* **Logo Ambari** -apre hello dashboard in cui può essere utilizzato toomonitor hello cluster.

* **Cluster ops # nome** -Visualizza il numero di hello di operazioni Ambari in corso. Se si seleziona il nome del cluster hello o **ops #** Visualizza un elenco di operazioni in background.

* **gli avvisi #** -consente di visualizzare gli avvisi o gli avvisi critici, se presente, per il cluster hello.

* **Dashboard** -dashboard hello Visualizza.

* **Servizi** -informazioni e impostazioni di configurazione per i servizi cluster hello hello.

* **Host** -informazioni e impostazioni di configurazione per i nodi nel cluster hello hello.

* **Alerts** : log di informazioni, avvertenze e avvisi critici.

* **Amministrazione** -stack di Software e servizi installate nel cluster hello, informazioni sull'account di servizio e di sicurezza Kerberos.

* **Pulsante admin** : gestione di Ambari, impostazioni utente e disconnessione.

## <a name="monitoring"></a>Monitoraggio

### <a name="alerts"></a>Avvisi

Hello elenco seguente contiene hello comuni avviso utilizzato da Ambari:

* **OK**
* **Warning**
* **CRITICAL**
* **UNKNOWN**

Avvisi di diverso da **OK** causare hello **avvisi #** voce nella parte superiore di hello totale hello pagina toodisplay hello degli avvisi. Selezionando questa voce consente di visualizzare gli avvisi di hello e il relativo stato.

Gli avvisi sono organizzati in diversi gruppi predefiniti, che possono essere visualizzati da hello **avvisi** pagina.

![pagina degli avvisi](./media/hdinsight-hadoop-manage-ambari/alerts.png)

È possibile gestire i gruppi di hello utilizzando hello **azioni** menu e selezionando **Gestisci gruppi avviso**.

![finestra di dialogo Manage Alert Groups](./media/hdinsight-hadoop-manage-ambari/manage-alerts.png)

È anche possibile gestire metodi avvisi e creare le notifiche di avviso da hello **azioni** menu selezionando __gestire le notifiche di avviso__. Questa opzione consente di visualizzare le notifiche correnti e di creare nuove notifiche. È possibile inviare notifiche tramite **EMAIL** o **SNMP** al verificarsi di specifiche combinazioni di avviso/gravità. Ad esempio, è possibile inviare un messaggio di posta elettronica quando uno degli avvisi di hello in hello **YARN predefinito** gruppo troppo**critico**.

![finestra di dialogo Create Alert](./media/hdinsight-hadoop-manage-ambari/create-alert-notification.png)

Infine, la selezione __Gestione impostazioni di avviso__ da hello __azioni__ menu consente numero hello tooset deve occorrenze di un avviso prima che venga inviata una notifica. Questa impostazione può essere utilizzato tooprevent notifiche per errori temporanei.

### <a name="cluster"></a>HDInsight

Hello **metriche** scheda dashboard hello contiene una serie di widget che rendono lo stato di hello toomonitor semplice del cluster a colpo d'occhio. Widget diversi, ad esempio **CPU Usage**, forniscono informazioni aggiuntive quando vengono selezionati.

![dashboard con metriche](./media/hdinsight-hadoop-manage-ambari/metrics.png)

Hello **Heatmaps** scheda Visualizza le metriche come heatmaps colorato, passando da toored verde.

![dashboard con mappe termiche](./media/hdinsight-hadoop-manage-ambari/heatmap.png)

Per ulteriori informazioni sui nodi hello all'interno di cluster hello, selezionare **host**. Selezionare quindi nodo specifico di hello che si è interessati.

![dettagli dell'host](./media/hdinsight-hadoop-manage-ambari/host-details.png)

### <a name="services"></a>Services

Hello **servizi** barra laterale dashboard hello offre una visione rapida stato hello dei servizi di hello in esecuzione nel cluster hello. Icone diverse sono stato tooindicate utilizzato o azioni da intraprendere. Ad esempio, viene visualizzato un simbolo di riciclo giallo se un servizio deve toobe riciclato.

![barra laterale dei servizi](./media/hdinsight-hadoop-manage-ambari/service-bar.png)

> [!NOTE]
> servizi di Hello visualizzati diversi tra versioni e i tipi di cluster HDInsight. servizi Hello visualizzati qui potrebbero essere diversi da servizi di hello visualizzati per il cluster.

Selezione di un servizio consente di visualizzare informazioni più dettagliate sul servizio hello.

![informazioni di riepilogo sul servizio](./media/hdinsight-hadoop-manage-ambari/service-details.png)

#### <a name="quick-links"></a>Collegamenti rapidi

Alcuni servizi di visualizzare un **collegamenti rapidi** collegamento nella parte superiore di hello della pagina hello. Può trattarsi di web specifico del servizio utilizzato tooaccess le interfacce utente, ad esempio:

* **Job History** : cronologia dei processi MapReduce.
* **Resource Manager** : interfaccia utente di gestione risorse di YARN.
* **NameNode** : interfaccia utente NameNode del file system distribuito Hadoop (HDFS).
* **Oozie Web UI** : interfaccia utente Oozie.

Selezionare uno dei seguenti collegamenti per aprire una nuova scheda nel browser, che consente di visualizzare la pagina selezionata hello.

> [!NOTE]
> Se si seleziona hello **collegamenti rapidi** voce per un servizio può restituire un errore "server non trovato". Se si verifica questo errore, è necessario utilizzare un tunnel SSH quando si utilizza hello **collegamenti rapidi** voce per questo servizio. Per informazioni, vedere [Usare il tunneling SSH con HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).

## <a name="management"></a>gestione

### <a name="ambari-users-groups-and-permissions"></a>Utenti, gruppi e autorizzazioni Ambari

L'uso di utenti, gruppi e autorizzazioni è supportato con un cluster HDInsight [aggiunto al dominio](hdinsight-domain-joined-introduction.md). Per informazioni sull'utilizzo dell'interfaccia utente Gestione Ambari hello in un cluster di dominio, vedere [la gestione dei cluster HDInsight dominio](hdinsight-domain-joined-introduction.md).

> [!WARNING]
> Non modificare la password di hello di watchdog di hello Ambari (hdinsightwatchdog) il cluster HDInsight basati su Linux. La modifica di interruzioni di password hello hello azioni script toouse di capacità o eseguire le operazioni di ridimensionamento con il cluster.

### <a name="hosts"></a>Hosts

Hello **host** pagina vengono elencati tutti gli host cluster hello. gli host toomanage, seguire questi passaggi.

![pagina Hosts](./media/hdinsight-hadoop-manage-ambari/hosts.png)

> [!NOTE]
> Non usare le procedure per aggiungere, rimuovere o ripristinare un host con cluster HDInsight.

1. Selezionare un host di hello che si desidera toomanage.

2. Hello utilizzare **azioni** azione hello tooselect di menu che si desidera tooperform:

   * **Avviare tutti i componenti** -avviare tutti i componenti nell'host di hello.

   * **Arrestare tutti i componenti** -Arresta tutti i componenti su host di hello.

   * **Riavviare tutti i componenti** : arrestare e avviare tutti i componenti nell'host di hello.

   * **Attivare la modalità di manutenzione** -Elimina gli avvisi per host hello. Questa modalità deve essere abilitata se si eseguono azioni che generano avvisi, come l'arresto e l'avvio di un servizio.

   * **Disattivare la modalità di manutenzione** -restituisce hello avvisi toonormal host.

   * **Arrestare** -DataNode si arresta o NodeManagers nell'host di hello.

   * **Avviare** -avvia DataNode o NodeManagers nell'host di hello.

   * **Riavviare** -arresta e avvia DataNode o NodeManagers nell'host di hello.

   * **Rimuovere le autorizzazioni** -rimuove un host dal cluster hello.

     > [!NOTE]
     > Non usare questa azione nei cluster HDInsight.

   * **Recommission** -aggiunge un cluster di toohello host eliminato in precedenza.

     > [!NOTE]
     > Non usare questa azione nei cluster HDInsight.

### <a id="service"></a>Services

Da hello **Dashboard** o **servizi** pagina, utilizzare hello **azioni** pulsante nella parte inferiore di hello dell'elenco di hello di servizi toostop e avviare tutti i servizi.

![Service Actions](./media/hdinsight-hadoop-manage-ambari/service-actions.png)

> [!WARNING]
> Mentre **Aggiungi servizio** è elencato in questo menu, non può essere cluster HDInsight toohello di tooadd utilizzati servizi. È necessario aggiungere nuovi servizi.utilizzando un'azione di Script durante il provisioning del cluster. Per altre informazioni su come utilizzare le azioni di script, vedere [Personalizzare cluster HDInsight mediante l'azione script](hdinsight-hadoop-customize-cluster-linux.md).

Durante la hello **azioni** pulsante possibile riavviare tutti i servizi, spesso si desidera toostart, arrestare o riavviare un servizio specifico. Utilizzare hello seguenti passaggi viene tooperform azioni in un singolo servizio:

1. Da hello **Dashboard** o **servizi** pagina, selezionare un servizio.

2. Dall'alto hello di hello **riepilogo** scheda, utilizzare hello **azioni servizio** pulsante e selezionare hello azione tootake. Verrà riavviato il servizio di hello in tutti i nodi.

    ![azione del servizio](./media/hdinsight-hadoop-manage-ambari/individual-service-actions.png)

   > [!NOTE]
   > Il riavvio di alcuni servizi durante l'esecuzione di cluster hello potrebbe generare avvisi. tooavoid degli avvisi, è possibile utilizzare hello **azioni servizio** pulsante tooenable **modalità manutenzione** per servizio hello prima di eseguire il riavvio di hello.

3. Dopo aver selezionata un'azione, hello **op #** voce nella parte superiore di hello di hello pagina incrementi tooshow in corso un'operazione in background. Se configurato toodisplay, viene visualizzato l'elenco di hello delle operazioni in background.

   > [!NOTE]
   > Se è stata abilitata **modalità manutenzione** per il servizio di hello, ricordare toodisable usando hello **azioni servizio** pulsante una volta completata l'operazione di hello.

tooconfigure un servizio, utilizzare hello alla procedura seguente:

1. Da hello **Dashboard** o **servizi** pagina, selezionare un servizio.

2. Seleziona hello **configurazioni** configurazione corrente di hello scheda viene visualizzata. insieme a un elenco delle configurazioni precedenti.

    ![configurazioni](./media/hdinsight-hadoop-manage-ambari/service-configs.png)

3. Utilizzare la configurazione hello campi visualizzati toomodify hello e quindi selezionare **salvare**. Oppure selezionare una configurazione precedente e quindi selezionare **impostare come corrente** tooroll nuovamente le impostazioni precedenti toohello.

## <a name="ambari-views"></a>Viste di Ambari

Ambari viste consentono agli sviluppatori elementi dell'interfaccia utente tooplug in hello dell'interfaccia utente Web Ambari utilizzando hello [Ambari viste Framework](https://cwiki.apache.org/confluence/display/AMBARI/Views). HDInsight fornisce hello seguenti viste con tipi di cluster Hadoop:

* Gestore delle code yarn: gestore delle code hello fornisce un'interfaccia utente semplice per la visualizzazione e modifica di YARN code.

* Visualizzazione di hive: hello vista Hive consente query Hive toorun direttamente dal browser web. Si può salvare le query, visualizzare i risultati, salvare i risultati di archiviazione cluster toohello o scaricare risultati tooyour locale sistema. Per altre informazioni sull'uso delle viste di Hive, vedere l'argomento relativo all' [uso delle viste Hive con HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).

* Tez: hello Tez visualizzazione consente di toobetter comprendere e ottimizzare i processi. È possibile visualizzare informazioni sulle modalità di esecuzione dei processi Tez e sulle risorse usate.
