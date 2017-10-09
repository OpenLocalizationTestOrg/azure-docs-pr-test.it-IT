---
title: Panoramica di factory di connesso aaaAzure IoT Suite | Documenti Microsoft
description: Una descrizione di hello Azure IoT Suite connesso soluzione factory preconfigurato.
services: 
suite: iot-suite
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 
ms.service: iot-suite
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: dobett
ms.openlocfilehash: 929b5ed41ef7d82c9b4480d02aa3f0db38931919
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-connected-factory-preconfigured-solution"></a>Introduzione a soluzioni factory preconfigurato hello connesso

Azure IoT Suite [preconfigurato soluzioni] [ lnk-preconfigured-solutions] combinare più Azure IoT servizi toodeliver end-to-end soluzioni che implementano i comuni scenari di business IoT. Hello *factory connesso* soluzione preconfigurata si connette i dispositivi industriali tooand monitoraggi. È possibile utilizzare hello soluzione tooanalyze hello flusso di dati dai dispositivi e toodrive operativo produttività e la redditività.

Questa esercitazione viene illustrato il modo in cui tooprovision hello connesse factory preconfigurato soluzione. Illustra anche funzionalità di base della soluzione hello preconfigurato hello. Molte di queste funzionalità accessibili dalla soluzione hello *dashboard* che distribuisce come parte della soluzione preconfigurata hello:

![Dashboard della soluzione preconfigurata di connected factory][img-cf-home]

toocomplete questa esercitazione, è necessaria una sottoscrizione di Azure attiva.

> [!NOTE]
> Se non si dispone di un account, è possibile creare un account di valutazione gratuita in pochi minuti. Per informazioni dettagliate, vedere la pagina relativa alla [versione di valutazione gratuita di Azure][lnk_free_trial].
> 
> 

## <a name="provision-hello-solution"></a>Eseguire il provisioning hello soluzione

1. Accedere utilizzando le credenziali dell'account Azure tooazureiotsuite.com e fare clic su "**+**" toocreate una soluzione.
2. Fare clic su **selezionare** su hello **factory connesso** riquadro.
3. Immettere un valore in **Nome soluzione** per la soluzione preconfigurata di connected factory.
4. Seleziona hello **sottoscrizione** e **area** si desidera toouse tooprovision hello soluzione.
5. Fare clic su **crea soluzione** hello toobegin processo di provisioning. Questo processo è in genere richiede diversi minuti toorun.

### <a name="while-you-wait-for-hello-provisioning-process-toocomplete"></a>Durante l'attesa per hello toocomplete processo di provisioning

1. Fare clic sul riquadro hello per la soluzione con **Provisioning** stato.
2. Hello preavviso **Provisioning stati** come servizi di Azure vengono distribuiti nella sottoscrizione di Azure.
3. Una volta al termine del provisioning, hello modifiche allo stato troppo**pronto**.
4. Fare clic su dettagli di hello riquadro toosee hello della soluzione nel riquadro di destra hello.

> [!NOTE]
> Se si verificano problemi di distribuzione di soluzioni hello preconfigurato, esaminare [le autorizzazioni nel sito azureiotsuite.com hello] [ lnk-permissions] hello e [connesso domande frequenti sulla factory](iot-suite-faq-cf.md). Se persistono problemi hello, creare un ticket di servizio in hello [portale][lnk-portal].

Sono presenti dettagli che ci si aspetta toosee che non sono elencati per la soluzione? è possibile inviare suggerimenti sulle funzionalità usando i [suggerimenti degli utenti](https://feedback.azure.com/forums/321918-azure-iot).

## <a name="scenario-overview"></a>Panoramica dello scenario

Quando si distribuisce hello connesso factory preconfigurato soluzione, viene popolato preliminarmente con le risorse che consentono di toostep tramite uno scenario comune industriale. In questo scenario, le factory diverse connesso report soluzione toohello toocompute necessari valori dei dati di hello efficienza di apparecchiature (OEE) e indicatori di prestazioni chiave (KPI). Hello nelle sezioni seguenti illustrano come fare per:

* Monitorare stabilimenti, linee di produzione, OEE delle postazioni e valori KPI
* Analizzare i dati di telemetria hello generati da tali dispositivi utilizzando Azure ora serie Insights
* Agire sui problemi toofix avvisi

Una funzionalità chiave di questo scenario è che è possibile eseguire in modalità remota tutte queste azioni dal dashboard di soluzione hello. Non è necessario dispositivi toohello accesso fisico.

## <a name="view-hello-solution-dashboard"></a>Dashboard di soluzione hello View

dashboard di soluzione Hello consente soluzione hello distribuito toomanage. Si tratta di una rappresentazione gerarchica della configurazione globale degli stabilimenti. È ad esempio possibile visualizzare OEE e KPI, pubblicare nuovi nodi per la telemetria e attivare avvisi.

1. Quando il provisioning di hello è completato e riquadro hello per la soluzione preconfigurata indica **pronto**, scegliere **avviare** tooopen portale soluzione factory connesso in una nuova scheda.

    ![Avviare la soluzione hello preconfigurato][img-launch-solution]

1. Per impostazione predefinita, il portale di soluzione hello Mostra hello *dashboard*. toonavigate tooother aree del portale di hello, utilizzare il menu di hello sulla parte sinistra della pagina hello hello.

    ![Dashboard della soluzione preconfigurata di connected factory][cf-img-menu]

dashboard Hello Visualizza hello le seguenti informazioni:

* Oggetto **elenco Factory** pannello che mostra lo stato di hello, la posizione e configurazione di produzione corrente nella soluzione hello. Quando si esegue prima soluzione hello, esistono numerosi dispositivi simulati. simulazione di linea di produzione Hello è composta da tre reale OPC UA server per ogni linea di produzione che eseguano attività simulata e condividere i dati. Per ulteriori informazioni su OPC UA, vedere hello [connesso domande frequenti sulla factory](iot-suite-faq-cf.md).
* Oggetto **mappa** che consente di visualizzare hello posizione di ogni dispositivo connesso toohello soluzione. soluzione hello è possibile utilizzare informazioni tooplot di hello API di Bing mappe nella mappa hello. Se la sottoscrizione è abilitata per l'API di Bing Mappe per le aziende, questa funzionalità viene usata automaticamente. In caso contrario, vedere hello [domande frequenti su] [ lnk-faq] toolearn come toomake hello dinamici della mappa.
* Un pannello degli **avvisi** che visualizza gli avvisi generati quando un valore OEE/KPI o di telemetria supera una soglia specifica.
* Un **efficienza apparecchiature** pannello che mostra i valori OEE hello per l'intera azienda hello o hello factory/produzione riga/stazione si sta visualizzando. Questo valore viene aggregato dal livello di organizzazione toohello visualizzazione hello stazione. Figura OEE Hello e i relativi elementi costitutivi possono essere ulteriormente analizzati.
* **Indicatori di prestazioni chiave** pannello che visualizza il numero di hello di unità prodotte e di energia utilizzata dall'intera azienda hello o hello factory/produzione/stazione si sta visualizzando. Questi valori vengono aggregati da un livello di organizzazione toohello visualizzazione stazione.

## <a name="view-factories"></a>Visualizzare gli stabilimenti

Hello *factory* pannello Mostra hello posizione geografica di tutte le factory hello nei soluzione hello, stato e configurazione di produzione corrente. Dall'elenco di percorsi hello, è possibile passare toohello altri livelli nella gerarchia di soluzione hello. righe Hello hello elenco sono collegamenti ipertestuali che collegano i dettagli delle linee di produzione hello in tale posizione. È quindi possibile toodrill i dettagli di linea di produzione hello e toohello visualizzazione a livello di espansione verso il basso. È inoltre possibile applicare un elenco di filtri toohello.

![Stabilimenti della soluzione preconfigurata di connected factory][cf-img-factories] 

1. Hello **pannello Factory** Mostra hello elenco di factory per questa soluzione.

2. elenco di factory Hello viene inizialmente sei factory creata dal processo di provisioning hello. È possibile aggiungere soluzioni toohello altri dispositivi simulati e fisico.

3. dettagli di hello tooview di una factory, fare clic su riga hello nell'elenco di factory hello.

4. dettagli di hello tooview di una linea di produzione, fare clic su riga hello hello elenco.

5. hello tooview pubblicato nodi OPC UA una stazione in linea di produzione hello, fare clic sulla riga hello hello elenco.

6. Dettagli tooview in un nodo specifico nella stazione hello, fare clic su riga hello hello elenco. Questa azione avvia il pannello contesto hello con visualizzazioni ora serie Insights. Fare clic su questi ulteriori analisi di grafici toodo nell'ambiente di hello ora serie Insights explorer.

## <a name="view-map"></a>Visualizzare la mappa

Se la sottoscrizione ha accesso toohello API di Bing mappe, hello *factory* mappa Mostra la posizione geografica hello e lo stato di tutte le factory hello in soluzione hello. toodrill i dettagli di percorso hello, fare clic su percorsi hello visualizzati nella mappa hello.

![Mappa della soluzione preconfigurata di connected factory][cf-img-map]

## <a name="view-alerts"></a>Visualizzare gli avvisi

Hello **avviso** pannello mostra gli avvisi generati a causa di tooa segnalati valore o un valore calcolato di OEE/KPI superare la soglia configurata. Questo consente di visualizzare gli avvisi a ogni livello della gerarchia di hello, dalla visualizzazione globale toohello hello stazione visualizzazione a livello. avvisi di Hello contengono una descrizione dell'avviso hello, data, ora, posizione e numero di occorrenze. È possibile ottenere informazioni dettagliate nei dati toohello che ha determinato avviso hello utilizzando hello dati di Insights di serie di tempo. Hello ora serie Insights dati viene visualizzati nella hello avvisi, se applicabile. Se si è un amministratore, è possibile eseguire le azioni predefinite agli avvisi di hello, ad esempio:

* Avviso di hello Chiudi.
* Confermare l'avviso hello.

È anche possibile eseguire operazioni più complesse. Ad esempio, per hello pressione OPC UA nodo di hello Assembly, è possibile:

* Visualizzare informazioni di supporto in una pagina Web in una nuova finestra del browser.
* Mitigare causa hello dell'avviso hello chiamando un metodo OPC UA sul dispositivo hello.
* Esclusione di disponibilità hello di azioni predefinite hello.

    ![Avvisi della soluzione preconfigurata di connected factory][cf-img-alerts]

> [!NOTE]
> Gli avvisi vengono generati da regole che vengono specificate in un file di configurazione nella soluzione hello preconfigurato. Queste regole possono generare avvisi quando hello OEE o cifre di indicatore KPI o i valori del nodo UA OPC superano la soglia configurata.

1. Hello **pannello avvisi** Mostra hello gli avvisi generati in questa soluzione.

2. dettagli di hello tooview di un avviso, fare clic su avviso hello nel Pannello di hello avvisi.

3. toofurther analizzare i dati di avviso hello, fare clic su grafico hello nell'ambiente di hello pannello avviso tooopen hello ora serie Insights explorer.

4. avviso di hello tooaddress, sono disponibili nel Pannello di avviso hello diverse azioni. Scegliere hello opzione appropriata per l'utente e fare clic su hello eseguire pulsante di comando di azione.

## <a name="view-overall-equipment-efficiency"></a>Visualizzare il valore di OEE (Overall Equipment Efficiency)

Tariffe OEE hello l'efficienza del processo di produzione di hello utilizzando una chiave parametri operativi correlate alla produzione. OEE è uno standard misura calcolata moltiplicando la tariffa di disponibilità hello, velocità delle prestazioni e la percentuale di qualità: OEE = disponibilità x qualità delle prestazioni x.

![OEE della soluzione preconfigurata di connected factory][cf-img-oee]

1. tooview OEE di qualsiasi livello di gerarchia hello, passare toohello di visualizzazione desiderata. OEE per la visualizzazione viene visualizzato nel Pannello di hello insieme a tutti gli elementi che costituiscono hello percentuale OEE hello.

2. toofurther analizzare hello OEE di qualsiasi livello di dati della gerarchia hello, fare clic su hello OEE, disponibilità, prestazioni o la percentuale di qualità. Contesto verrà visualizzato un pannello con tempo serie Insights spenta visualizzazioni che mostrano i dati da hello ultima ora, ultime 24 ore e ultimi 7 giorni.

    ![Visualizzazione TSI della soluzione preconfigurata di connected factory][cf-img-tsi-visualization]

3. toofurther analizzare i dati di avviso hello, fare clic su grafico hello nel Pannello di avviso di hello. Questa azione apre l'ambiente di hello ora serie Insights explorer.

    ![Ambiente di esplorazione TSI della soluzione preconfigurata di connected factory][cf-img-tsi-explorer]

## <a name="view-key-performance-indicators"></a>Visualizzare gli indicatori di prestazioni chiave

soluzione Hello fornisce due indicatori di prestazioni chiave, *unità per ora* e *energia nelle kWh*.

![KPI della soluzione preconfigurata di connected factory][cf-img-kpi]

1. tooview unità per ogni ora o energia usata per qualsiasi livello nella gerarchia di hello, passare toohello di visualizzazione desiderata. unità di Hello per ora e di energia usate visualizzato nel Pannello di hello.

2. tooanalyze unità per ogni ora o energia usata per qualsiasi livello nella gerarchia di hello ulteriormente, fare clic su misuratore hello in hello **indicatori di prestazioni chiave** pannello. Verrà visualizzato un pannello di contesto con visualizzazioni ora serie Insights con tecnologia consentendo dati tooview hello ultima ora, hello ultime 24 ore e ultimi 7 giorni.

## <a name="scenario-review"></a>Analisi dello scenario

In questo scenario, i valori OEE e indicatori KPI di factory, nel dashboard di hello è stata monitorata. Quindi utilizzato tooprovide ora serie approfondimenti più informazioni toohelp esaminare ulteriormente i dati di telemetria hello per toohelp OEE e indicatori KPI con il rilevamento di anomalie. Sono stati usati anche i problemi di hello pannello avviso tooview con le factory e avviso di hello azioni disponibili tooyou tooresolve hello è stato utilizzato.

## <a name="other-features"></a>Altre funzionalità

Hello le sezioni seguenti vengono descritte alcune funzionalità aggiuntive di hello connesso factory soluzione che non sono descritti nello scenario precedente hello.

## <a name="apply-filters"></a>Applicare filtri

1. Fare clic su hello **freccia di espansione** toodisplay un elenco dei filtri disponibili nel Pannello di percorsi di factory hello o pannello avvisi hello.

2. Pannello filtri Hello è visualizzato per l'utente. 

    ![Filtri della soluzione preconfigurata di connected factory][cf-img-alert-filter]

3. Scegliere Filtro hello necessari. È inoltre possibile tootype testo libero nei campi filtro hello.

4. Hello filtro viene applicato automaticamente. lo stato del filtro Hello viene inoltre visualizzato nel dashboard di hello tramite un grafico a imbuto consente di visualizzare nella factory hello e segnala le tabelle.

    ![Filtri della soluzione preconfigurata di connected factory][cf-img-alert-filter-funnel]

    > [!NOTE]
    > Un filtro attivo non influisce sulla hello visualizzato valori OEE e indicatori KPI, ma solo di filtrare il contenuto di elenco hello.

5. tooclear un filtro, fare clic su grafico a imbuto hello e fare clic su filtro nel riquadro del contesto filtro hello. testo Hello **tutti** viene visualizzato nella factory hello e gli avvisi di tabelle.

## <a name="browse-an-opc-ua-server"></a>Esplorare un server OPC UA

Quando si distribuisce la soluzione hello preconfigurato, automaticamente effettuato il provisioning di server OPC UA simulati che è possibile esplorare tramite browser soluzione hello Questi server sono *server OPC UA simulati* . Server simulato semplificano automaticamente tooexperiment con la soluzione hello preconfigurato senza hello necessità toodeploy reale server fisici. Se si desidera tooconnect una soluzione di toohello server OPC UA reale, vedere hello [connettere la soluzione di factory preconfigurato OPC UA dispositivo connesso toohello] [ lnk-connect-cf] esercitazione.

1. Fare clic su hello **icona factory** nella barra di navigazione del dashboard hello.

    ![Browser dei server della soluzione preconfigurata di connected factory][cf-img-server-browser]

2. Scegliere uno dei server hello da elenco preconfigurato hello. Questo elenco Mostra i server hello che vengono distribuiti automaticamente nella soluzione hello preconfigurato.

    ![Selezione del server della soluzione preconfigurata di connected factory][cf-img-server-choice]

3. Fare clic su **Connect** (Connetti). Verrà visualizzata una finestra di dialogo di sicurezza. Per la simulazione di hello è sicuro tooclick **continua**

4. tooexpand uno qualsiasi dei nodi di hello nell'albero di server hello, farvi clic sopra. I nodi che pubblicano i dati di telemetria hanno un segno di spunta accanto.

    ![Albero dei server della soluzione preconfigurata di connected factory][cf-img-server-tree]

5. Fare doppio clic su un elemento di tooread, scrivere, pubblicare o chiamare tale nodo. Hello azioni disponibili tooyou dipendono le autorizzazioni e gli attributi di hello del nodo hello. Hello lettura opzione toodisplays un pannello del contesto che mostra il valore di hello di nodo specifico hello. Hello scrivere opzione consente di visualizzare un pannello del contesto in cui è possibile immettere un nuovo valore. opzione di chiamata Hello Visualizza un nodo in cui è possibile immettere i parametri di hello per chiamata hello.

## <a name="publish-a-node"></a>Pubblicare un nodo

Quando si Esplora un *server OPC UA simulato*, è anche possibile scegliere toopublish nuovi nodi. È possibile analizzare i dati di telemetria hello da questi nodi nella soluzione hello. Questi *simulato Server OPC UA* renderlo tooexperiment semplice con la soluzione hello preconfigurato senza distribuire i dispositivi fisici reali.

1. Sfoglia tooa nodo nell'albero del server OPC UA browser che si desidera toopublish hello.

2. Fare clic sul nodo hello.

3. Scegliere **Publish** (Pubblica).

    ![Pubblicare un nodo nella soluzione di connected factory][cf-img-publish-node]

4. Verrà visualizzato un pannello di contesto che indica che hello pubblicazione ha avuto esito positivo. nodo Hello viene visualizzato nella visualizzazione di livello stazione hello con un segno di spunta.

    ![Pubblicazione eseguita nella soluzione preconfigurata di connected factory][cf-img-publish-success]

## <a name="command-and-control"></a>Comando e controllo

factory connesso Hello consente di comando e controllare i dispositivi di settore direttamente dal cloud hello. È possibile utilizzare questo tooalerts toorespond funzionalità generato per dispositivo hello. Ad esempio, è possibile inviare un dispositivo toohello comando dal cloud hello. È possibile trovare i comandi disponibili hello in hello **StationCommands** nodo nell'albero di browser server OPC UA hello. In questo scenario, si apre una versione valvola sulla stazione di assembly hello di una linea di produzione Monaco. funzionalità di comando e controllo di hello toouse, è necessario essere in hello **amministratore** ruolo per hello preconfigurato distribuzione della soluzione.

1. Sfoglia toohello **StationCommands** nodo nell'albero del browser server OPC UA hello.

2. Scegliere il comando hello che si desidera utilizzare.

3. Fare clic sul nodo hello.

4. Scegliere **Call** (Chiama).

    ![Comando di chiamata della soluzione preconfigurata di connected factory][cf-img-call-command]

5. Viene indicato quale metodo si sta toocall ed eventuali dettagli del parametro è applicabile, viene visualizzato un riquadro contesto.

6. Scegliere **Call** (Chiama).

    ![Contesto di chiamata della soluzione preconfigurata di connected factory][cf-img-call-context]

7. Pannello contesto Hello è tooinform aggiornato che hello chiamata al metodo ha avuto esito positivo. È possibile verificare chiamata hello ha avuto esito positivo, leggere il valore di hello del nodo di pressione hello aggiornati in seguito chiamata hello.

    ![Chiamata eseguita nella soluzione preconfigurata di connected factory][cf-img-call-success]


## <a name="behind-hello-scenes"></a>Background hello

Quando si distribuisce una soluzione preconfigurata, il processo di distribuzione hello crea più risorse hello Azure sottoscrizione selezionata. È possibile visualizzare queste risorse in Azure hello [portale][lnk-portal]. il processo di distribuzione Hello crea un **gruppo di risorse** con un nome basato sul nome hello scelto per la soluzione preconfigurata:

![Soluzione preconfigurata in hello portale di Azure][img-cf-portal]

È possibile visualizzare le impostazioni di hello di ogni risorsa selezionandolo nell'elenco di hello delle risorse nel gruppo di risorse hello.

È anche possibile visualizzare il codice sorgente hello per soluzione hello preconfigurato. Hello factory connesso preconfigurato soluzione codice sorgente è in hello [azure iot-connessione-factory] [ lnk-cfgithub] repository GitHub:

Al termine, è possibile eliminare la soluzione hello preconfigurato dalla sottoscrizione di Azure su hello [azureiotsuite.com] [ lnk-azureiotsuite] sito. Questo sito consente tooeasily Elimina che tutte le risorse che è sono eseguito il provisioning durante la creazione di soluzioni hello preconfigurato di hello.

> [!NOTE]
> tooensure di eliminare tutti gli elementi correlati soluzione toohello preconfigurato, l'eliminazione hello [azureiotsuite.com] [ lnk-azureiotsuite] sito. Non eliminare il gruppo di risorse hello nel portale di hello.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver distribuito una soluzione appropriata preconfigurato, è possibile continuare introduzione IoT Suite leggendo hello seguenti articoli:

* [Procedura dettagliata per la soluzione preconfigurata di connected factory][lnk-rm-walkthrough]
* [Connettere la soluzione di factory connesso preconfigurato toohello dispositivo][lnk-connect-cf]
* [Autorizzazioni nel sito azureiotsuite.com hello][lnk-permissions]

[img-cf-home]:media/iot-suite-connected-factory-overview/cf-dashboard.png
[img-launch-solution]: media/iot-suite-connected-factory-overview/launch-cf.png
[cf-img-menu]: media/iot-suite-connected-factory-overview/cf-dashboard-menu.png
[cf-img-factories]:media/iot-suite-connected-factory-overview/cf-dashboard-factory.png
[cf-img-map]:media/iot-suite-connected-factory-overview/cf-dashboard-map.png
[cf-img-alerts]:media/iot-suite-connected-factory-overview/cf-dashboard-alerts.png
[cf-img-oee]:media/iot-suite-connected-factory-overview/cf-dashboard-oee.png
[cf-img-kpi]:media/iot-suite-connected-factory-overview/cf-dashboard-kpi.png
[cf-img-tsi-visualization]:media/iot-suite-connected-factory-overview/cf-dashboard-tsi.png
[cf-img-tsi-explorer]:media/iot-suite-connected-factory-overview/tsi-explorer.png
[cf-img-server-browser]: media/iot-suite-connected-factory-overview/cf-dashboard-browser.png
[cf-img-server-choice]: media/iot-suite-connected-factory-overview/cf-select-server.png
[cf-img-server-tree]:media/iot-suite-connected-factory-overview/cf-server-tree.png
[cf-img-publish-node]:media/iot-suite-connected-factory-overview/cf-publish-node1.png
[cf-img-publish-success]:media/iot-suite-connected-factory-overview/cf-publish-success.png
[cf-img-call-command]:media/iot-suite-connected-factory-overview/cf-command-and-control-call.png
[cf-img-call-context]:media/iot-suite-connected-factory-overview/cf-command-and-control-call-button.png
[cf-img-call-success]:media/iot-suite-connected-factory-overview/cf-command-and-control-succeed.png
[img-cf-portal]:media/iot-suite-connected-factory-overview/cf-resource-group.png
[cf-img-alert-filter]:media/iot-suite-connected-factory-overview/cf-filter.png
[cf-img-alert-filter-funnel]:media/iot-suite-connected-factory-overview/cf-filter-funnel.png

[lnk_free_trial]: http://azure.microsoft.com/pricing/free-trial/
[lnk-preconfigured-solutions]: iot-suite-what-are-preconfigured-solutions.md
[lnk-azureiotsuite]: https://www.azureiotsuite.com
[lnk-portal]: http://portal.azure.com/
[lnk-cfgithub]: https://github.com/Azure/azure-iot-connected-factory
[lnk-rm-walkthrough]: iot-suite-connected-factory-sample-walkthrough.md
[lnk-connect-cf]: iot-suite-connected-factory-gateway-deployment.md
[lnk-permissions]: iot-suite-permissions.md
[lnk-faq]: iot-suite-faq.md