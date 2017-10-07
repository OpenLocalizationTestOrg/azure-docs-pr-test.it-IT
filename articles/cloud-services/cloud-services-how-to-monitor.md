---
title: aaaHow toomonitor un servizio cloud | Documenti Microsoft
description: Informazioni su come toomonitor servizi cloud tramite hello portale di Azure classico.
services: cloud-services
documentationcenter: 
author: thraka
manager: timlt
editor: 
ms.assetid: 5c48d2fb-b8ea-420f-80df-7aebe2b66b1b
ms.service: cloud-services
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/07/2015
ms.author: adegeo
ms.openlocfilehash: ee98c56e0b98b85d75a5c1d796800069c4f06d20
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomonitor-cloud-services"></a>Come tooMonitor dei servizi Cloud
[!INCLUDE [disclaimer](../../includes/disclaimer.md)]

È possibile monitorare `key` metriche delle prestazioni per i servizi cloud nel portale di Azure classico hello. È possibile impostare hello dettagliati per ogni ruolo del servizio e livello di monitoraggio toominimal e personalizzabili hello monitoraggio consente di visualizzare. Dati di monitoraggio dettagliato viene archiviati in un account di archiviazione, è possibile accedere all'esterno di hello portale. 

Visualizzazioni dei monitoraggi nel portale di Azure classico hello sono altamente configurabili. È possibile scegliere le metriche hello desiderato nell'elenco delle metriche hello hello toomonitor **monitoraggio** pagina ed è possibile scegliere quali tooplot metriche in grafici metriche hello **monitoraggio** hello e pagina dashboard. 

## <a name="concepts"></a>Concetti
Per impostazione predefinita, monitoraggio minimo viene fornito per un nuovo servizio cloud utilizzando i contatori delle prestazioni raccolti da hello per le istanze di ruoli di hello (macchine virtuali) del sistema operativo host. le metriche minime Hello sono limitate tooCPU percentuale, dati in entrata, dati in uscita, velocità effettiva di lettura disco e velocità effettiva di scrittura su disco. Tramite la configurazione di monitoraggio dettagliato, è possibile ricevere metriche aggiuntive basate sui dati delle prestazioni nelle macchine virtuali hello (istanze del ruolo). le metriche dettagliate Hello consentono un'analisi ravvicinata dei problemi che si verificano durante operazioni dell'applicazione.

Per impostazione predefinita, dati del contatore delle prestazioni da istanze del ruolo sono campionati e trasferiti dall'istanza del ruolo hello a intervalli di 3 minuti. Quando si abilita il monitoraggio dettagliato, i dati dei contatori delle prestazioni raw hello sono aggregati per ogni istanza del ruolo e tra le istanze del ruolo per ogni ruolo a intervalli di 5 minuti, 1 ora e 12 ore. dati aggregati Hello viene eliminati dopo 10 giorni.

Dopo aver attivato il monitoraggio dettagliato, hello aggregata i dati di monitoraggio vengono archiviati nelle tabelle nell'account di archiviazione. tooenable dettagliato di monitoraggio per un ruolo, è necessario configurare una stringa di connessione di diagnostica che si collega toohello account di archiviazione. È possibile usare account di archiviazione diversi per i diversi ruoli.

Abilitazione aumenta di monitoraggio dettagliato i costi di archiviazione correlato toodata archiviazione, il trasferimento dei dati e le transazioni di archiviazione. Il monitoraggio minimo non richiede un account di archiviazione. dati Hello per le metriche di hello esposte a livello di monitoraggio minimo hello non vengono archiviati nell'account di archiviazione, anche se si imposta hello tooverbose livello di monitoraggio.

## <a name="how-to-configure-monitoring-for-cloud-services"></a>Procedura: Configurare il monitoraggio per i servizi cloud
Utilizzare hello seguendo procedure tooconfigure dettagliato o minimo monitoraggio nel portale di Azure classico hello. 

### <a name="before-you-begin"></a>Prima di iniziare
* Creare un *classico* hello toostore account di archiviazione dati di monitoraggio. È possibile usare account di archiviazione diversi per i diversi ruoli. Per ulteriori informazioni, vedere [come un account di archiviazione toocreate](../storage/common/storage-create-storage-account.md#create-a-storage-account).
* Abilitare Diagnostica Azure per i ruoli del servizio cloud. Vedere [Configurazione della diagnostica per i servizi cloud](cloud-services-dotnet-diagnostics.md).

Verificare che sia presente nella configurazione dei ruoli hello stringa di connessione di diagnostica hello. È possibile abilitare il monitoraggio dettagliato fino a quando non si abilita diagnostica di Azure e include una stringa di connessione di diagnostica nella configurazione del ruolo hello.   

> [!NOTE]
> Progetti destinati a Azure SDK 2.5 non include automaticamente stringa di connessione di diagnostica hello nel modello di progetto hello. Per questi progetti, è necessario toomanually aggiungere una configurazione del ruolo toohello connessione stringa hello diagnostica.
> 
> 

**toomanually aggiungere configurazione tooRole stringa di connessione diagnostica**

1. Progetto servizio Cloud hello aperto in Visual Studio
2. Fare doppio clic su hello **ruolo** tooopen hello progettazione ruoli e selezionare hello **impostazioni** scheda
3. Cercare un’impostazione denominata **Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString**. 
4. Se questa impostazione non è presente, fare clic su hello **Aggiungi impostazione** tooadd pulsante Modifica e configurazione di toohello hello tipo per hello nuova impostazione troppo**ConnectionString**
5. Impostare il valore di hello per hello di stringa di connessione facendo clic su hello **...**  pulsante. Verrà aperta una finestra di dialogo consentono di tooselect un account di archiviazione.
   
    ![Impostazioni di Visual Studio](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioDiagnosticsConnectionString.png)

### <a name="toochange-hello-monitoring-level-tooverbose-or-minimal"></a>hello toochange monitoraggio livello tooverbose o minima
1. In hello [portale di Azure classico](https://manage.windowsazure.com/)aprire hello **configura** pagina per la distribuzione del servizio cloud hello.
2. In **Livello** fare clic su **Dettagliato** o **Minimo**. 
3. Fare clic su **Salva**.

Dopo l'attivazione del monitoraggio dettagliato, è consigliabile iniziare a visualizzare i dati di monitoraggio di hello portale di Azure classico nell'ora hello hello.

dati del contatore delle prestazioni raw Hello e dati di monitoraggio aggregati vengono archiviati nell'account di archiviazione hello nelle tabelle qualificati da hello ID di distribuzione per i ruoli di hello. 

## <a name="how-to-receive-alerts-for-cloud-service-metrics"></a>Procedura: Ricevere avvisi per le metriche dei servizi cloud
È possibile ricevere avvisi basati sulle metriche di monitoraggio del servizio cloud. In hello **servizi di gestione** hello di pagina del portale di Azure classico, è possibile creare una regola tootrigger un avviso quando metrica hello scelta raggiunge un valore specificato. È anche possibile scegliere toohave messaggio di posta elettronica inviato quando viene attivato l'avviso hello. Per altre informazioni, vedere [Procedura: Ricevere notifiche di avviso e gestire le relative regole in Azure](http://go.microsoft.com/fwlink/?LinkId=309356).

## <a name="how-to-add-metrics-toohello-metrics-table"></a>Procedura: aggiungere una tabella delle metriche di metriche toohello
1. In hello [portale di Azure classico](http://manage.windowsazure.com/)aprire hello **monitoraggio** pagina per il servizio cloud hello.
   
    Per impostazione predefinita, tabella delle metriche hello consente di visualizzare un subset delle metriche disponibili hello. Figura Hello Mostra le metriche dettagliate hello predefinito per un servizio cloud, che è limitato toohello contatore delle prestazioni Memoria\Mbyte disponibili, con dati aggregati a livello di ruolo hello. Utilizzare **Aggiungi metriche** tooselect aggiuntive aggregazione e le metriche a livello di ruolo toomonitor in hello portale di Azure classico.
   
    ![Visualizzazione dettagliata](./media/cloud-services-how-to-monitor/CloudServices_DefaultVerboseDisplay.png)
2. tabella delle metriche di tooadd metriche toohello:
   
   1. Fare clic su **Aggiungi metriche** tooopen **Scegli metriche**, come illustrato di seguito.
      
       metrica disponibile prima di Hello è espanso tooshow le opzioni disponibili. Per ogni metrica, opzione top hello Visualizza dati di monitoraggio aggregati per tutti i ruoli. Inoltre, è possibile scegliere i singoli ruoli dati toodisplay per.
      
       ![Aggiungi Metriche](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics.png)
   2. tooselect metriche toodisplay
      
      * Fare clic su hello freccia giù per hello tooexpand metrica hello opzioni di monitoraggio.
      * Casella di controllo selezionare hello per ogni monitoraggio opzione da toodisplay.
        
        È possibile visualizzare le metriche too50 nella tabella delle metriche hello.
        
        > [!TIP]
        > Nel monitoraggio dettagliato, elenco metriche hello può contenere decine di metriche. toodisplay una barra di scorrimento, passa il mouse sul lato destro hello della finestra di dialogo hello. elenco di hello toofilter, fare clic sull'icona di ricerca hello e immettere il testo nella casella di ricerca hello, come illustrato di seguito.
        > 
        > 
        
        ![Ricerca Aggiungi metriche](./media/cloud-services-how-to-monitor/CloudServices_AddMetrics_Search.png)
3. Dopo aver completato la selezione delle metriche, fare clic su OK (segno di spunta).
   
    salve le metriche selezionate vengono aggiunte toohello tabella delle metriche, come illustrato di seguito.
   
    ![monitor metriche](./media/cloud-services-how-to-monitor/CloudServices_Monitor_UpdatedMetrics.png)
4. toodelete una metrica dalla tabella delle metriche hello, fare clic su tooselect metrica hello e quindi fare clic su **Elimina metrica**. (Selezionando una metrica viene visualizzata solo l'opzione **Delete Metric** .)

### <a name="tooadd-custom-metrics-toohello-metrics-table"></a>tabella delle metriche di tooadd metriche personalizzate toohello
Hello **Verbose** monitoraggio livello fornisce un elenco di criteri predefiniti che è possibile monitorare nel portale di hello. Inoltre toothese è possibile monitorare le metriche personalizzate o i contatori delle prestazioni definiti dall'applicazione tramite il portale di hello.

Hello passaggi seguenti presuppongono che è stata attivata **Verbose** livello di monitoraggio e aver configurato l'applicazione toocollect e il trasferimento di contatori delle prestazioni personalizzati. 

contatori delle prestazioni personalizzati toodisplay hello in hello portale necessaria la configurazione di hello tooupdate in wad-control-container:

1. Aprire blob wad-control-container hello nell'account di archiviazione di diagnostica. È possibile utilizzare Visual Studio o qualsiasi altro toodo archiviazione Esplora questo.
   
    ![Esplora server di Visual Studio.](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioBlobExplorer.png)
2. Passare il percorso di blob hello usando il modello di hello **RoleName/DeploymentId/RoleInstance** configurazione hello toofind per l'istanza del ruolo. 
   
    ![Esplora archivi di Visual Studio.](./media/cloud-services-how-to-monitor/CloudServices_Monitor_VisualStudioStorage.png)
3. Scaricare il file di configurazione hello per l'istanza del ruolo e aggiornarlo tooinclude contatori di prestazioni personalizzati. Ad esempio toomonitor *byte scritti su disco/sec* per hello *unità C* aggiungere seguenti hello in **PerformanceCounters\Subscriptions** nodo
   
    ```xml
    <PerformanceCounterConfiguration>
    <CounterSpecifier>\LogicalDisk(C:)\Disk Write Bytes/sec</CounterSpecifier>
    <SampleRateInSeconds>180</SampleRateInSeconds>
    </PerformanceCounterConfiguration>
    ```
4. Salvare le modifiche di hello e caricamento hello configurazione file indietro toohello stesso percorso sovrascrivendo hello file esistente nel blob hello.
5. Attiva/Disattiva modalità tooVerbose in hello configurazione del portale classico di Azure. Se fosse già in modalità dettagliata sarà necessario tooverbose di tootoggle toominimal e viceversa.
6. contatore delle prestazioni personalizzato Hello saranno ora disponibili in hello **Aggiungi metriche** la finestra di dialogo. 

## <a name="how-to-customize-hello-metrics-chart"></a>Procedura: personalizzare grafico delle metriche hello
1. Nella tabella delle metriche hello, selezionare backup too6 metriche tooplot nel grafico delle metriche hello. tooselect una metrica, fare clic su casella di controllo hello sul lato sinistro. tooremove una metrica dal grafico delle metriche hello, deselezionare la casella di controllo nella tabella delle metriche hello.
   
    Quando si seleziona la metrica nella tabella delle metriche hello, metriche hello vengono aggiunte grafico delle metriche toohello. In una visualizzazione "narrow", un **n ulteriori** elenco a discesa contiene le intestazioni di metriche che non si adattano visualizzazione hello.
2. tooswitch tra la visualizzazione di valori relativi (valore finale solo per ogni metrica) e i valori assoluti (asse Y visualizzato), selezionare relativo o assoluto nella parte superiore di hello del grafico hello.
   
    ![Relative o Absolute](./media/cloud-services-how-to-monitor/CloudServices_Monitor_RelativeAbsolute.png)
3. grafico delle metriche di toochange hello ora intervallo hello Visualizza, selezionare 1 ora, 24 ore o giorni 7 nella parte superiore di hello del grafico hello.
   
    ![Visualizzazione del periodo monitorato](./media/cloud-services-how-to-monitor/CloudServices_Monitor_DisplayPeriod.png)
   
    Nel grafico delle metriche di hello dashboard, il metodo hello per le metriche del tracciato è diverso. È disponibile un set di metriche standard e le metriche vengono aggiunti o rimossi selezionando intestazione metrica hello.

### <a name="toocustomize-hello-metrics-chart-on-hello-dashboard"></a>grafico delle metriche di hello toocustomize dashboard hello
1. Aprire il dashboard di hello per il servizio cloud hello.
2. Aggiungere o rimuovere metriche dal grafico hello:
   
   * una casella di controllo hello metrica, selezionare la metrica hello nelle intestazioni grafico hello tooplot. In una visualizzazione "narrow", fare clic su hello freccia giù per  ***n* ?? metriche** tooplot non è possibile visualizzare un'area di intestazione hello metrica del grafico.
   * toodelete una metrica che viene tracciata sul grafico hello, casella di controllo crittografato hello relativa intestazione.
   
3. Passare dalla visualizzazione **relativa** a quella **assoluta**.
4. Scegliere 1 ora, 24 ore o 7 giorni di dati toodisplay.

## <a name="how-to-access-verbose-monitoring-data-outside-hello-azure-classic-portal"></a>Procedura: accedere ai dati di monitoraggio dettagliato di fuori di hello portale di Azure classico
Dati di monitoraggio dettagliato viene archiviati nelle tabelle negli account di archiviazione hello specificato per ogni ruolo. Per ogni distribuzione del servizio cloud, sei tabelle vengono create per il ruolo di hello. Vengono create due tabelle per ogni intervallo di tempo (5 minuti, 1 ora e 12 ore). Una di queste tabelle vengono archiviate le aggregazioni a livello di ruolo; Hello altre aggregazioni di archivi di tabella per le istanze del ruolo. 

i nomi delle tabelle di Hello hanno hello seguente formato:

```
WAD*deploymentID*PT*aggregation_interval*[R|RI]Table
```

dove:

* *deploymentID* è hello GUID assegnato toohello distribuzione del servizio cloud
* *aggregation_interval* = 5M, 1H o 12H
* aggregazioni a livello di ruolo = R
* aggregazioni per le istanze del ruolo = RI

Ad esempio, hello nelle tabelle seguenti archivia dati di monitoraggio dettagliato aggregati a intervalli di 1 ora:

```
WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRTable (hourly aggregations for hello role)

WAD8b7c4233802442b494d0cc9eb9d8dd9fPT1HRITable (hourly aggregations for role instances)
```
