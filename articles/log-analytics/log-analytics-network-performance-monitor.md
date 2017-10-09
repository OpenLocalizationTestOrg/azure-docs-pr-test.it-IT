---
title: soluzione di monitoraggio delle prestazioni in Azure Log Analitica aaaNetwork | Documenti Microsoft
description: Monitoraggio prestazioni di rete in Azure Log Analitica consente di monitorare le prestazioni di hello del reti aggiuntivo quasi reale tempo-toodetect e individuare i colli di bottiglia delle prestazioni.
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: 5b9c9c83-3435-488c-b4f6-7653003ae18a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.openlocfilehash: e074948221fdd003c640861d759c4ce69ced1cd7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="network-performance-monitor-solution-in-log-analytics"></a>Soluzione di monitoraggio delle prestazioni di rete in Log Analytics

![Simbolo di Monitoraggio prestazioni rete](./media/log-analytics-network-performance-monitor/npm-symbol.png)

Questo documento descrive come tooset-up e utilizzare hello soluzione di monitoraggio delle prestazioni di rete in Analitica di Log, che consente di monitorare le prestazioni di hello del reti aggiuntivo quasi reale tempo-toodetect e individuare i colli di bottiglia delle prestazioni. Con hello soluzione di monitoraggio delle prestazioni di rete, è possibile monitorare hello perdita e la latenza tra due reti, server o subnet. Monitoraggio delle prestazioni di rete rileva problemi di rete come traffico blackholing, routing gli errori e problemi che i metodi di monitoraggio rete convenzionale non sono in grado di toodetect. Il monitoraggio delle prestazioni di rete genera avvisi e invia notifiche quando viene superata una soglia per un collegamento di rete. Tali soglie possono essere appresi automaticamente dal sistema hello oppure è possibile configurare le regole di avviso personalizzato toouse. Monitoraggio delle prestazioni di rete garantisce tempestiva individuazione di problemi di prestazioni di rete e che localizza origine hello del hello problema tooa particolare segmento di rete o del dispositivo.

È possibile rilevare problemi di rete con i dashboard di soluzione hello che visualizza le informazioni riepilogative sulla rete, tra cui recenti eventi di integrità della rete, i collegamenti di rete non integri e i collegamenti della subnet che si trova ad affrontare la latenza e la perdita di pacchetti elevata. È possibile drill-down in un rete tooview hello corrente integrità stato del collegamento i collegamenti della subnet, nonché collegamenti a nodi. È anche possibile visualizzare tendenze cronologiche di hello di perdita e la latenza di rete hello, subnet e a livello di nodo per nodo. È possibile rilevare i problemi di rete temporanei visualizzando i grafici sulle tendenze cronologiche relative a perdita di pacchetti e latenza e individuare colli di bottiglia di rete su una mappa topologica. grafico interattivo topologia Hello consente le route di rete hop-by-hop hello toovisualize e determinare hello origine del problema hello. Ad esempio altre soluzioni, è possibile utilizzare la ricerca dei registri per vari analitica report personalizzati di toocreate requisiti in base ai dati di hello raccolti dal Monitor di prestazioni di rete.

soluzione Hello utilizza le transazioni sintetiche come errori di rete toodetect un meccanismo principale. Pertanto, è possibile usarla senza tener conto del particolare fornitore o modello di un dispositivo di rete. Funziona in ambienti ibridi, cloud (IaaS) e locali. soluzione Hello individua automaticamente la topologia di rete hello e vari percorsi nella rete.

Rete tipica monitoraggio prodotti lo stato attivo sul monitoraggio hello rete integrità dei dispositivi (router, commutatori e così via) ma non forniscono informazioni dettagliate sui qualità effettiva di hello della connettività di rete tra due punti, monitoraggio delle prestazioni della rete.

### <a name="using-hello-solution-standalone"></a>Utilizza hello soluzione autonomo
Se si desidera qualità hello toomonitor delle connessioni di rete tra i carichi di lavoro critici, reti, Datacenter o siti di office, quindi si hello Network Performance Monitor soluzione consente autonomamente toomonitor integrità tra:

* più data center o uffici remoti connessi con tramite una rete pubblica o privata
* carichi di lavoro critici che eseguono applicazioni line-of-business
* servizi cloud pubblico come Microsoft Azure o reti di Amazon Web Services (AWS) e in locale, se si hanno IaaS (VM) disponibili e i gateway configurato tooallow comunicazione tra reti locali e cloud
* Reti locali e Azure quando si usa ExpressRoute

### <a name="using-hello-solution-with-other-networking-tools"></a>Utilizzo di soluzioni hello con altri strumenti di rete
Se si desidera toomonitor un'applicazione line of business, è possibile utilizzare hello soluzione di monitoraggio delle prestazioni di rete come un strumenti di rete tooother soluzione complementare. Una rete lenta può comportare tooslow applicazioni e monitoraggio delle prestazioni di rete possono contribuire a esaminare i problemi delle prestazioni dell'applicazione sono causati da problemi di rete sottostanti. Poiché hello soluzione non richiede alcun toonetwork accedere ai dispositivi, amministratore dell'applicazione hello non necessario toorely in una rete team tooprovide informazioni come rete hello è influire sulle applicazioni.

Inoltre, se già investire in altri strumenti di monitoraggio di rete, quindi soluzione hello può integrare questi strumenti poiché più tradizionali soluzioni di monitoraggio di rete non forniscono informazioni dettagliate sui metriche delle prestazioni di rete end-to-end come perdita e la latenza.  Hello soluzione di monitoraggio delle prestazioni di rete consente di colmare il vuoto.

## <a name="installing-and-configuring-agents-for-hello-solution"></a>L'installazione e configurazione di agenti per la soluzione hello
Usare gli agenti tooinstall di processi di base di hello in [tooLog computer Windows di connettersi Analitica](log-analytics-windows-agents.md) e [tooLog connettere Operations Manager Analitica](log-analytics-om-agents.md).

> [!NOTE]
> Si sarà necessario agenti tooinstall almeno 2 nell'ordine toohave sufficiente toodiscover dati e monitorare le risorse di rete. In caso contrario, la soluzione hello rimarrà in uno stato di configurazione fino a quando non si installa e configura gli agenti aggiuntivi.
>
>

### <a name="where-tooinstall-hello-agents"></a>Dove tooinstall hello agenti
Prima di installare gli agenti, considerare la topologia di hello della rete e le parti di hello rete toomonitor. Si consiglia di installare più di un agente per ogni subnet che si desidera toomonitor. In altre parole, per ogni subnet che si desidera toomonitor, scegliere due o più macchine virtuali o i server e installare l'agente di hello su di essi.

Se si è certi di topologia hello della rete, installare gli agenti di hello nei server con carichi di lavoro critiche in cui si desidera toomonitor le prestazioni della rete di hello. Ad esempio, è consigliabile tookeep traccia di una connessione di rete tra un server Web e un server che esegue SQL Server. In questo esempio, viene installato un agente su entrambi i server.

Gli agenti di monitorano la connettività di rete (collegamenti) tra gli host, non hello degli stessi host. In questo caso, toomonitor un collegamento di rete, è necessario installare gli agenti su entrambi gli endpoint del collegamento.

### <a name="configure-agents"></a>Configurazione degli agenti

Se si prevede di protocollo ICMP toouse hello per le transazioni sintetiche, è necessario hello tooenable alle regole firewall per l'utilizzo in modo affidabile ICMP:

```
netsh advfirewall firewall add rule name="NPMDICMPV4Echo" protocol="icmpv4:8,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6Echo" protocol="icmpv6:128,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4DestinationUnreachable" protocol="icmpv4:3,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6DestinationUnreachable" protocol="icmpv6:1,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV4TimeExceeded" protocol="icmpv4:11,any" dir=in action=allow
netsh advfirewall firewall add rule name="NPMDICMPV6TimeExceeded" protocol="icmpv6:3,any" dir=in action=allow
```


Se si prevede di hello toouse protocollo TCP è necessario tooopen porte del firewall per tali tooensure computer in grado di comunicare gli agenti. È necessario toodownload e poi eseguire hello [script di PowerShell EnableRules.ps1](https://gallery.technet.microsoft.com/OMS-Network-Performance-04a66634) senza parametri in una finestra di PowerShell con privilegi amministrativi.

script Hello crea le chiavi del Registro di sistema necessarie per hello monitoraggio delle prestazioni di rete e crea Windows firewall le connessioni TCP regole tooallow agenti toocreate tra loro. le chiavi del Registro di sistema di Hello create dallo script hello inoltre specificano se eseguire il debug toolog hello registri e hello il percorso file di log di hello. Definisce inoltre la porta TCP hello agente utilizzata per la comunicazione. i valori Hello per queste chiavi vengono impostati automaticamente dallo script hello in modo da non modificare manualmente queste chiavi.

porta Hello aperta per impostazione predefinita è 8084. È possibile utilizzare una porta personalizzata, fornendo il parametro hello `portNumber` toohello script. Tuttavia, hello stessa porta deve essere utilizzata in tutti i computer hello in cui viene eseguito uno script di hello.

> [!NOTE]
> Hello EnableRules.ps1 script consente di configurare regole firewall di Windows solo in computer hello in cui viene eseguito uno script hello. Se si dispone di un firewall di rete, assicurarsi che consente il traffico destinato alla porta TCP hello utilizzata dal monitoraggio delle prestazioni di rete.
>
>

## <a name="configuring-hello-solution"></a>Configurazione di soluzione hello
Utilizzare hello tooinstall le informazioni seguenti e configurare la soluzione hello.

1. soluzione di monitoraggio delle prestazioni di rete Hello acquisisce i dati dai computer che eseguono Windows Server 2008 SP 1 o versioni successive o Windows 7 SP1 o versioni successive, che sono hello stesso i requisiti di hello Microsoft Monitoring Agent (MMA). Gli agenti NPM possono essere eseguiti anche in sistemi operativi desktop/client Windows (Windows 10, Windows 8.1, Windows 8 e Windows 7).
    >[!NOTE]
    >gli agenti di Hello per sistemi operativi Windows server supportano sia TCP e ICMP come protocolli hello per transazione sintetica. Tuttavia, gli agenti di hello per sistemi operativi client Windows supportano solo ICMP come protocollo di hello per transazione sintetica.

2. Aggiungere hello Network Performance Monitor soluzione tooyour area di lavoro da [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.NetworkMonitoringOMS?tab=Overview) o tramite il processo di hello descritto in [soluzioni aggiungere Log Analitica da hello Solutions Gallery](log-analytics-add-solutions.md).  
   ![Simbolo del monitoraggio delle prestazioni di rete](./media/log-analytics-network-performance-monitor/npm-symbol.png)
3. Nel portale OMS hello, verrà visualizzato un nuovo riquadro denominato **Network Performance Monitor** con un messaggio hello *soluzione richiede una configurazione aggiuntiva*. È necessario che le reti tooadd soluzione hello tooconfigure in base alle subnet e i nodi che vengono individuati dagli agenti. Fare clic su **Network Performance Monitor** toostart la configurazione di rete predefinita hello.  
   ![La soluzione richiede configurazione aggiuntiva](./media/log-analytics-network-performance-monitor/npm-config.png)

### <a name="configure-hello-solution-with-a-default-network"></a>Configurare la soluzione hello con una rete predefinita
Nella pagina di configurazione hello, si noterà una singola rete denominata **predefinito**. Quando non sono definite le reti, tutte le subnet individuate automaticamente hello vengono inserite nella rete predefinita hello.

Quando si crea una rete, si aggiunge un tooit subnet e subnet viene rimosso dalla rete predefinita hello. Se si elimina una rete, tutte le relative subnet vengono automaticamente restituite rete predefinita toohello.

In altre parole, rete predefinita hello è il contenitore di hello per tutte le subnet hello che non sono presenti in qualsiasi rete definita dall'utente. È possibile modificare o eliminare la rete predefinita hello. Rimane sempre nel sistema hello. Tuttavia, è possibile creare tutte le reti necessarie.

Nella maggior parte dei casi, le subnet hello all'interno dell'organizzazione verranno disposti su più di una rete ed è necessario crearne uno o più reti toologically raggruppare le subnet.

### <a name="create-new-networks"></a>Creazione di nuove reti
Una rete del monitoraggio delle prestazioni di rete è un contenitore per le subnet. È possibile creare una rete con qualsiasi nome desiderato e aggiungere le subnet toohello rete. Ad esempio, è possibile creare una rete denominata *Building1* e quindi aggiungere le subnet oppure è possibile creare una rete denominata *DMZ* e quindi aggiungere tutte le subnet appartenenti rete toothis di toodemilitarized zona.

#### <a name="toocreate-a-new-network"></a>toocreate una nuova rete
1. Fare clic su **Aggiungi rete** e quindi digitare il nome di rete hello e una descrizione.
2. Selezionare una o più subnet e quindi fare clic su **Aggiungi**.
3. Fare clic su **salvare** configurazione hello toosave.  
   ![aggiunta della rete](./media/log-analytics-network-performance-monitor/npm-add-network.png)

### <a name="wait-for-data-aggregation"></a>Attesa dell'aggregazione dei dati
Dopo avere salvato la configurazione hello per la prima volta, soluzione hello avvia la raccolta delle informazioni di perdita e la latenza dei pacchetti di rete tra i nodi di hello in cui sono installati gli agenti. Questo processo può richiedere del tempo, talvolta oltre 30 minuti. Durante questo stato, il riquadro di monitoraggio delle prestazioni di rete hello nella pagina di panoramica hello Visualizza un messaggio che informa *aggregazione dei dati nel processo*.

![aggregazione dei dati in corso](./media/log-analytics-network-performance-monitor/npm-aggregation.png)

Quando sono stati caricati dati hello, si noterà dati che Mostra riquadro venga aggiornato di monitoraggio delle prestazioni di rete hello.

![Riquadro Monitoraggio delle prestazioni di rete](./media/log-analytics-network-performance-monitor/npm-tile.png)

Fare clic su dashboard di monitoraggio delle prestazioni di rete di hello riquadro tooview hello.

![Dashboard di monitoraggio delle prestazioni di rete](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="edit-monitoring-settings-for-subnets"></a>Modifica delle impostazioni di monitoraggio per le subnet
Sono elencate tutte le subnet in cui è stato installato almeno un agente su hello **subnet** scheda nella pagina di configurazione hello.

#### <a name="tooenable-or-disable-monitoring-for-particular-subnetworks"></a>tooenable o disattivazione del monitoraggio per una determinata subnet
1. Hello selezionare o deselezionare la casella successiva toohello **ID subnet** e infine verificare che **utilizzare per il monitoraggio** è selezionata o deselezionata, a seconda dei casi. È possibile selezionare o deselezionare più subnet. Se disabilitato, non vengono monitorate subnet come gli agenti di hello saranno aggiornate toostop il ping di altri agenti.
2. Scegliere a cui si desidera toomonitor per una determinata subnet selezionando subnet hello dall'elenco di hello e lo spostamento di nodi di hello hello nodi necessari tra elenchi hello contenente nodi non monitorati e monitorati.
   È possibile aggiungere un oggetto personalizzato **descrizione** toohello subnet, se si preferisce.
3. Fare clic su **salvare** configurazione hello toosave.  
   ![modifica della subnet](./media/log-analytics-network-performance-monitor/npm-edit-subnet.png)

### <a name="choose-nodes-toomonitor"></a>Scegliere i nodi toomonitor
Sono elencati tutti i nodi che hanno installato un agente di hello in hello **nodi** scheda.

#### <a name="tooenable-or-disable-monitoring-for-nodes"></a>tooenable o disattivazione del monitoraggio per i nodi
1. Selezionare o deselezionare i nodi di hello che desidera toomonitor o arrestare il monitoraggio.
2. Fare clic su **Usa per il monitoraggio** oppure deselezionare l'opzione in base alle esigenze.
3. Fare clic su **Save**.  
   ![abilitazione del monitoraggio dei nodi](./media/log-analytics-network-performance-monitor/npm-enable-node-monitor.png)

### <a name="set-monitoring-rules"></a>Set di regole di monitoraggio
Monitoraggio delle prestazioni di rete genera eventi di integrità sulla connettività hello tra una coppia di nodi o collegamenti di rete o subnet quando viene superata la soglia. Tali soglie possono essere appresi automaticamente dal sistema hello oppure è possibile configurare le regole di avviso personalizzate.

Hello *regola predefinita* viene creato dal sistema hello e crea un evento ogni volta che la perdita o latenza tra qualsiasi coppia di reti o subnet collegamenti soglia appresi sistema hello di violazioni di integrità. È possibile scegliere una regola predefinita di toodisable hello e creare le regole di monitoraggio personalizzate

#### <a name="toocreate-custom-monitoring-rules"></a>le regole di monitoraggio personalizzati toocreate
1. Fare clic su **Aggiungi regola** in hello **monitoraggio** scheda e immettere il nome della regola hello e una descrizione.
2. Selezionare la coppia hello di rete o subnet toomonitor collegamenti dagli elenchi di hello.
3. Selezionare innanzitutto rete hello in cui hello è contenuto prima subnet/s di interesse dall'elenco a discesa rete hello, quindi hello subnet/s dall'elenco a discesa subnet corrispondente hello.
   Selezionare **tutte le subnet** se si desidera toomonitor tutti hello subnet in un collegamento di rete. Analogamente, selezionare hello altre subnet/s di interesse. E, è possibile fare clic su **aggiungere eccezione** tooexclude il monitoraggio per subnet particolare collega dalla selezione hello apportate.
4. Scegliere tra i protocolli TCP e ICMP per l'esecuzione di transazioni sintetiche.
5. Se non si desidera toocreate gli eventi di integrità per gli elementi di hello è selezionata, quindi deselezionare **il monitoraggio dello stato su collegamenti hello coperti da questa regola**.
6. Scegliere le condizioni di monitoraggio.
   È possibile impostare soglie personalizzate per la generazione di eventi di integrità digitando i valori di soglia. Ogni volta che il valore di hello della condizione di hello è superiore alla relativa soglia selezionata per coppia di hello/subnet di rete selezionata, viene generato un evento di integrità.
7. Fare clic su **salvare** configurazione hello toosave.  
   ![creazione di una regola di monitoraggio personalizzata](./media/log-analytics-network-performance-monitor/npm-monitor-rule.png)

Dopo avere salvato una regola di monitoraggio, è possibile integrarla con Gestione avvisi facendo clic su **Crea avviso**. Una regola di avviso viene creata automaticamente con la query di ricerca hello e altri necessari parametri automaticamente compilato in. Utilizza una regola di avviso, è possibile ricevere avvisi, basate su e-mail inoltre di avvisi toohello esistenti all'interno di NPM. Gli avvisi possono anche attivare azioni correttive con i runbook oppure possono essere integrati con le soluzione di gestione esistenti usando i webhook. È possibile fare clic su **avviso gestire** le impostazioni degli avvisi di tooedit hello.

### <a name="choose-hello-right-protocol-icmp-or-tcp"></a>Scegliere ICMP protocol hello destro o TCP

Monitoraggio delle prestazioni di rete (NPM) usa le metriche delle prestazioni di rete di transazioni sintetiche toocalculate come latenza di collegamento e di perdita di pacchetti. toounderstand questo meglio, prendere in considerazione la fine di un collegamento di rete connessa tooone un agente NPM. Questo NPM agente invia probe pacchetti tooa secondo NPM agente connesso tooanother fine della rete hello. risposte agente secondo Hello con pacchetti di risposta. Questo processo viene ripetuto più volte. Misurando il numero di hello di risposte e tempo impiegato tooreceive ogni risposta, agente NPM prima hello consente di valutare la latenza di collegamento e pacchetti ignorati.

Hello formato, una dimensione e una sequenza di questi pacchetti è determinato dal protocollo hello che si sceglie la creazione di regole di monitoraggio. Basata sul protocollo di pacchetti hello, hello dispositivi di rete intermedi (router, commutatori e così via) potrebbe elaborare questi pacchetti in modo diverso. Di conseguenza, la scelta del protocollo influisce sulla precisione hello dei risultati di hello. E, la scelta del protocollo determina inoltre se è necessario eseguire operazioni manuali dopo aver distribuito una soluzione NPM hello.

NPM offre che Hello scelta tra i protocolli ICMP e TCP per l'esecuzione di transazioni sintetiche.
Se si sceglie ICMP quando si crea una regola di transazione sintetica, viene utilizzato dagli agenti NPM hello latenza di rete hello toocalculate messaggi ECHO ICMP e la perdita di pacchetti. ECHO ICMP utilizza hello stesso messaggio di inviato dall'utilità Ping convenzionale hello. Quando si utilizza TCP come protocollo di hello, gli agenti NPM inviano pacchetti TCP SYN rete hello. È seguito da un handshake TCP completamento e quindi rimuovendo connessione hello utilizzando pacchetti RST.

#### <a name="points-tooconsider-before-choosing-hello-protocol"></a>Punti tooconsider prima di scegliere il protocollo hello
Prendere in considerazione le seguenti informazioni prima di scegliere un protocollo toouse hello:

##### <a name="discovering-multiple-network-routes"></a>Individuazione di più route di rete
TCP offre una maggiore precisione nell'individuazione di più route e necessita di un minor numero di agenti in ogni subnet. Ad esempio, uno o due agenti con TCP possono individuare tutti i percorsi ridondanti tra subnet. Tuttavia, è necessario diversi agenti utilizzando ICMP tooachieve simile risultati. Con ICMP, se si dispone di *N* numero di route tra due subnet, è necessario usare più di 5*N* agenti nella subnet di origine o destinazione.

##### <a name="accuracy-of-results"></a>Precisione dei risultati
Router e switch tendono tooassign inferiore priorità tooICMP ECHO pacchetti confrontati tooTCP pacchetti. In alcuni casi, quando i dispositivi di rete un carico eccessivo, hello ottenuto da TCP maggiormente riflettono hello perdita e la latenza che per le applicazioni si è verificato. Questo errore si verifica perché la maggior parte del traffico hello flussi su TCP. In questi casi, ICMP fornisce meno accurate tooTCP risultati confrontati.

##### <a name="firewall-configuration"></a>Configurazione del firewall
Protocollo TCP richiede che i pacchetti TCP inviati tooa porta di destinazione. porta predefinita Hello utilizzata dagli agenti di NPM è 8084, tuttavia è possibile modificare questa quando si configurano gli agenti. In tal caso, è necessario che il firewall di rete o le regole di gruppo (in Azure) consente il traffico sulla porta hello tooensure. È inoltre necessario toomake che è configurato tale firewall locale hello nei computer hello in cui sono installati gli agenti tooallow traffico su questa porta.

È possibile utilizzare le regole del firewall di tooconfigure gli script di PowerShell nei computer che eseguono Windows, tuttavia è necessario tooconfigure firewall di rete manualmente.

Il protocollo ICMP invece non opera tramite porta. Nella maggior parte degli scenari aziendali, è consentito il traffico ICMP tramite hello firewall tooallow che toouse strumenti di diagnostica di rete desiderato hello utilità Ping. In tal caso, se è possibile eseguire il Ping di un computer da un altro, è possibile utilizzare protocollo ICMP hello senza tooconfigure firewall manualmente.

> [!NOTE]
> In caso di dubbi quali toouse di protocollo, scegliere toostart ICMP con. Se non si è soddisfatti dei risultati di hello, è possibile passare sempre tooTCP in un secondo momento.


#### <a name="how-tooswitch-hello-protocol"></a>Come tooswitch hello protocollo

Se si sceglie toouse ICMP durante la distribuzione, è possibile passare tooTCP in qualsiasi momento mediante la modifica della regola di monitoraggio predefinite hello.

##### <a name="tooedit-hello-default-monitoring-rule"></a>regola di monitoraggio tooedit hello predefinito
1.  Passare troppo**le prestazioni della rete** > **monitoraggio** > **configura** > **Monitor** e quindi fare clic su **regola predefinita**.
2.  Scorrere toohello **protocollo** sezione e selezionare il protocollo di hello che si desidera toouse.
3.  Fare clic su **salvare** impostazione hello tooapply.

Anche se la regola predefinita di hello utilizza un protocollo specifico, è possibile creare nuove regole con un protocollo diverso. È anche possibile creare una combinazione di regole in cui alcune regole hello utilizzare ICMP e un altro utilizza TCP.




## <a name="data-collection-details"></a>Informazioni dettagliate sulla raccolta di dati
Monitoraggio delle prestazioni di rete utilizza i pacchetti di handshake TCP SYN-SYNACK-ACK quando TCP non è selezionata e risposta ECHO ICMP di ECHO ICMP ICMP viene scelto come hello protocollo toocollect perdita di informazioni e sulla latenza. Traceroute è anche informazioni sulla topologia tooget utilizzato.

Hello nella tabella seguente illustra i metodi di raccolta dati e altri dettagli sulla modalità di raccolta dati per il monitoraggio delle prestazioni di rete.

| Piattaforma | Agente diretto | Agente SCOM | Archiviazione di Azure | SCOM obbligatorio? | Dati dell'agente SCOM inviati con il gruppo di gestione | frequenza della raccolta |
| --- | --- | --- | --- | --- | --- | --- |
| Windows | &#8226; | &#8226; |  |  |  |Handshake TCP/messaggi ICMP ECHO ogni 5 secondi, dati inviati ogni 3 minuti |

soluzione Hello Usa transazioni sintetiche tooassess hello integrità rete hello. Agenti OMS installati vari nella fase i pacchetti hello rete exchange TCP o Echo ICMP (a seconda di hello protocollo selezionato per il monitoraggio) tra loro. Nel processo di hello, gli agenti informazioni hello round trip ora e dei pacchetti perdita, se presente. Periodicamente, ogni agente esegue inoltre una toofind gli agenti di traccia route tooother che tutti hello route diversi nella rete hello che devono essere verificate. Con questi dati, gli agenti di hello possono dedurre la latenza di rete hello e valori di perdite di pacchetti. test di Hello vengono ripetuti ogni cinque secondi e i dati vengono aggregati per un periodo di tre minuti dagli agenti hello prima di caricarlo servizio Analitica Log toohello.

> [!NOTE]
> Anche se gli agenti comunicano tra loro spesso, non generano un intenso traffico di rete durante l'esecuzione dei test hello. Gli agenti si basano solo sul TCP SYN-SYNACK-ACK handshake pacchetti toodetermine hello perdita e la latenza, nessun dato pacchetti vengono scambiati. Durante questo processo, gli agenti comunicano tra loro solo quando necessario ed è con ottimizzazione per la topologia di comunicazione agente hello tooreduce il traffico di rete.
>
>

## <a name="using-hello-solution"></a>Utilizzo di soluzione hello
Questa sezione vengono illustrate tutte le funzioni di dashboard hello e come toouse li.

### <a name="solution-overview-tile"></a>Riquadro Panoramica della soluzione
Dopo avere abilitato la soluzione di monitoraggio delle prestazioni di rete hello, riquadro soluzione hello nella pagina Overview di OMS hello fornisce una rapida panoramica dello stato di rete hello. Visualizza un grafico ad anello che mostra il numero di collegamenti subnet corretti e non corretti hello. Quando si fa clic su riquadro hello, viene aperto il dashboard di soluzione hello.

![Riquadro Monitoraggio delle prestazioni di rete](./media/log-analytics-network-performance-monitor/npm-tile.png)

### <a name="network-performance-monitor-solution-dashboard"></a>Dashboard della soluzione di monitoraggio delle prestazioni di rete
Hello **rete riepilogo** pannello viene visualizzato un riepilogo delle reti hello con le relative dimensioni. È seguito da riquadri che mostrano il numero totale di collegamenti di rete, i collegamenti di subnet e i percorsi nel sistema hello (un percorso è costituito da indirizzi IP di hello dei due host con gli agenti e tutti gli hop hello tra di esse).

Hello **eventi di integrità della rete superiore** pannello fornisce un elenco di avvisi e gli eventi di integrità più recente nel sistema hello e l'ora di hello dall'evento hello è rimasta attiva. Un evento di stato o un avviso viene generato ogni volta che la perdita di pacchetti hello o della latenza di un collegamento di rete o subnet supera una soglia.

Hello **collegamenti di rete non integri Top** pannello viene visualizzato un elenco di collegamenti di rete non integri. Si tratta di collegamenti di rete hello che dispongono di uno o più eventi di integrità negativo per tali un determinato momento hello.

Hello **i collegamenti della subnet con perdita più alto** e **i collegamenti della subnet con latenza più** pannelli Mostra i collegamenti della subnet superiore hello dalla perdita di pacchetti e le prime rispettivamente i collegamenti della subnet dalla latenza. In determinati collegamenti di rete ci si può aspettare una latenza elevata o una certa perdita di pacchetti. Tali collegamenti vengono visualizzati in elenchi dei primi 10 hello ma non sono contrassegnati come non integro.

Hello **query comuni** pannello contiene un set di query di ricerca che recuperano rete non elaborata direttamente i dati di monitoraggio. È possibile usare queste query come punto di partenza per creare le proprie query per l'elaborazione di report personalizzati.

![Dashboard di monitoraggio delle prestazioni di rete](./media/log-analytics-network-performance-monitor/npm-dash01.png)

### <a name="drill-down-for-depth"></a>Drill-down in profondità
È possibile scegliere diversi collegamenti in hello soluzione dashboard toodrill discesa più profondo in qualsiasi area di interesse. Ad esempio, quando viene visualizzato un avviso o un collegamento di rete non integri visualizzate nel dashboard di hello, è possibile fare clic tooinvestigate ulteriormente. Verrà visualizzata tooa pagina che elenca tutti i collegamenti della subnet hello per il collegamento di rete specifica hello. È stato in grado di toosee hello perdita, latenza e l'integrità di ciascun collegamento di subnet e rapidamente scoprire quali i collegamenti della subnet causano il problema di hello. È quindi possibile fare clic su **visualizzare collegamenti del nodo** collegano tutti i collegamenti del nodo hello per subnet non integri hello toosee. Quindi, è possibile vedere i collegamenti da nodo a nodo singoli e trovare i collegamenti del nodo di tipo non integro hello.

È possibile fare clic su **topologia vista** topologia hop-by-hop di hello tooview delle route hello tra i nodi di origine e destinazione hello. Hello route non integro o hop sono visualizzati in rosso in modo che è possibile identificare rapidamente hello problema tooa determinata porzione della rete hello.

![drill-down dei dati](./media/log-analytics-network-performance-monitor/npm-drill.png)

### <a name="network-state-recorder"></a>Utilità di registrazione dello stato di rete

Ogni visualizzazione mostra uno snapshot dell'integrità della rete in un determinato momento. Per impostazione predefinita, viene mostrato lo stato più recente di hello. barra Hello nella parte superiore di hello di hello pagina Mostra hello punto nel tempo per cui viene visualizzato lo stato di hello. È possibile scegliere toogo nuovamente nello snapshot hello tempo e visualizzare l'integrità di rete facendo clic sulla barra di hello su **azioni**. È anche possibile scegliere tooenable o disabilitare l'aggiornamento automatico per qualsiasi pagina durante la visualizzazione di stato più recente di hello.

![Stato della rete](./media/log-analytics-network-performance-monitor/network-state.png)

#### <a name="trend-charts"></a>Grafici delle tendenze
In ogni livello di drill-down, è possibile visualizzare la tendenza hello di perdita e la latenza di un collegamento di rete. I grafici di tendenza sono disponibili anche per i collegamenti della subnet e del nodo. È possibile modificare l'intervallo di tempo hello per hello grafico tooplot tramite controllo della fase di hello nella parte superiore di hello del grafico hello.

Grafici di tendenza mostrano una prospettiva cronologica delle prestazioni di hello di un collegamento di rete. Alcuni problemi di rete sono di natura temporanee e sarebbero toocatch rigido solo esaminando lo stato corrente di hello della rete hello. Infatti problemi possono superficie rapidamente e scompaiono prima qualcuno, solo tooreappear in un secondo momento nel tempo. Tali problemi temporanei possono essere difficili per gli amministratori di applicazioni perché quelli rilascia spesso area come inspiegabili aumenta nel tempo di risposta dell'applicazione, anche quando tutti i componenti applicazione toorun vengono visualizzati in modo uniforme.

Esaminando un grafico di tendenza in cui il problema di hello verrà visualizzato come un improvviso picco di perdita di latenza o pacchetti di rete, è possibile rilevare facilmente questi tipi di problemi.

![grafico di tendenza](./media/log-analytics-network-performance-monitor/npm-trend.png)

#### <a name="hop-by-hop-topology-map"></a>Mappa topologica hop-by-hop
Mostra Performance Monitor hello topologia hop-by-hop di route tra due nodi in una mappa interattiva della topologia di rete. È possibile visualizzare la mappa della topologia hello selezionando un nodo di collegamento e quindi fare clic su **topologia vista**. Inoltre, è possibile visualizzare mappa topologica hello facendo **percorsi** riquadro nel dashboard di hello. Quando fa clic su **percorsi** nel dashboard di hello, è necessario tooselect hello nodi di origine e di destinazione dal pannello sinistro hello e quindi fare clic su **tracciare** route hello tooplot tra i nodi di hello due.

mappa della topologia Hello Visualizza route quanti sono tra hello due nodi e i percorsi hello eseguire pacchetti di dati. Colli di bottiglia delle prestazioni vengono contrassegnati in rosso nella mappa della topologia di hello. È possibile individuare una connessione di rete difettosa oppure un dispositivo di rete difettosa esaminando gli elementi di colori rossi nella mappa della topologia di hello.

Quando si fa clic su un nodo o un passaggio del mouse su di essa nella mappa della topologia di hello, si noterà proprietà hello del nodo hello come nome di dominio completo e l'indirizzo IP. Fare clic su un toosee hop è l'indirizzo IP. È possibile scegliere toofilter route specifiche mediante i filtri di hello nel riquadro azione comprimibile hello. E, è anche possibile semplificare le topologie di rete hello nascondendo passaggi intermedi di hello con dispositivo di scorrimento di hello nel riquadro azioni hello. È possibile ingrandire o fuori mappa topologica hello utilizzando la rotellina del mouse.

Si noti che topologia hello illustrato nella mappa hello topologia layer 3 e non contiene connessioni e i dispositivi di livello 2.

![mappa topologica hop-by-hop](./media/log-analytics-network-performance-monitor/npm-topology.png)

#### <a name="fault-localization"></a>Individuazione degli errori
Monitoraggio delle prestazioni di rete è in grado di toofind hello colli di bottiglia senza connessione toohello dispositivi di rete. In base ai dati hello raccolti dalla rete hello e applicando algoritmi avanzati sul grafico della rete hello, monitoraggio delle prestazioni di rete effettua una stima delle parti di hello di rete che sono probabilmente hello origine del problema hello probabilistica.

Questo approccio è utile toodetermine colli di bottiglia hello quando toohops di accesso non è disponibile perché non richiede toobe eventuali dati raccolti dai dispositivi di rete hello, ad esempio commutatori o router. Ciò è utile anche quando hop hello tra due nodi non sono presenti nel controllo amministrativo. Ad esempio, hop hello possono essere router ISP.

### <a name="log-analytics-search"></a>Ricerca di Log Analytics
Tutti i dati esposti graficamente tramite il dashboard di monitoraggio delle prestazioni di rete hello e pagine di drill-down è disponibile anche in modo nativo in ricerca di Log Analitica. È possibile eseguire query sui dati hello utilizzando hello linguaggio di query di ricerca e creare report personalizzati esportando tooExcel dati hello o Power BI. Hello **query comuni** blade nel dashboard di hello dispone di alcune query utili che è possibile utilizzare come punto di partenza per la creazione di query e report personalizzati hello.

![query di ricerca](./media/log-analytics-network-performance-monitor/npm-queries.png)

## <a name="investigate-hello-root-cause-of-a-health-alert"></a>Ricercare hello di causa principale di un avviso di stato
Ora che è detto di monitoraggio delle prestazioni di rete, verrà ora esaminata una semplice indagine in hello causa radice per un evento di integrità.

1. Nella pagina di panoramica hello, si otterrà una panoramica immediata dell'integrità di hello della rete osservando hello **Network Performance Monitor** riquadro. Si noti che subnet hello 6 collegamenti da monitorare, 2 sono non integro. Questo rende necessaria un'analisi. Fare clic su hello riquadro tooview hello soluzione o un dashboard.  
   ![Riquadro Monitoraggio delle prestazioni di rete](./media/log-analytics-network-performance-monitor/npm-investigation01.png)
2. Nell'immagine di esempio hello riportata di seguito, si noterà che è presente un evento di stato di un collegamento di rete che non è integro. Decide di problema hello tooinvestigate e fare clic su hello **DMZ2 DMZ1** toofind di collegamento di rete out radice hello problema hello.  
   ![esempio di collegamento di rete non integro](./media/log-analytics-network-performance-monitor/npm-investigation02.png)
3. pagina di drill-down Hello Mostra tutti i collegamenti della subnet hello in **DMZ2 DMZ1** collegamento di rete. Si noterà che per entrambi i collegamenti della subnet hello, latenza hello ha superato soglia hello effettua il collegamento di rete hello non integro. È inoltre possibile visualizzare le tendenze di latenza hello di entrambi i collegamenti della subnet hello. È possibile utilizzare hello tempi di controllo di selezione in toofocus grafico hello in hello intervallo di tempo. È possibile visualizzare l'ora di hello del giorno hello quando latenza ha raggiunto il massimo. In un secondo momento, è possibile cercare i registri di hello per questo problema hello tooinvestigate periodo di tempo. Fare clic su **visualizzare collegamenti del nodo** toodrill verso il basso ulteriormente.  
   ![esempio di collegamenti della subnet non integri](./media/log-analytics-network-performance-monitor/npm-investigation03.png)
4. Pagina precedente toohello simile, pagina di hello drill-down per il collegamento di subnet particolare hello sono elencati i collegamenti che costituiscono nodi. È possibile eseguire azioni simili in questo caso, come nel passaggio precedente hello. Fare clic su **topologia vista** topologia hello tooview tra i nodi di hello 2.  
   ![esempio di collegamenti del nodo non integri](./media/log-analytics-network-performance-monitor/npm-investigation04.png)
5. Tutti i percorsi di hello tra i nodi di hello 2 selezionato vengono tracciati in mappa topologica hello. È possibile visualizzare topologia hop-by-hop hello di route tra due nodi nella mappa della topologia di hello. Offre un quadro preciso del numero route esistono tra due nodi hello e quali percorsi hello pacchetti di dati vengono eseguite. I colli di bottiglia delle prestazioni di rete sono contrassegnati in rosso. È possibile individuare una connessione di rete difettosa oppure un dispositivo di rete difettosa esaminando gli elementi di colori rossi nella mappa della topologia di hello.  
   ![esempio di visualizzazione della topologia non integra](./media/log-analytics-network-performance-monitor/npm-investigation05.png)
6. perdita Hello, latenza e hello numero di hop in ogni percorso può essere esaminati nei hello **azione** riquadro. Usare hello scrollbar tooview hello dettagli di tali percorsi non integro.  Usa hello filtri tooselect hello percorsi con hop integro hello in modo che la topologia di hello per solo hello selezionati percorsi viene tracciata. È possibile utilizzare il toozoom rotellina del mouse avanti o indietro mappa topologica hello.

   In hello sotto l'immagine è possibile visualizzare chiaramente hello causa radice di hello problema aree toohello sezione specifica di rete hello esaminando i percorsi di hello e hop di colore rosso. Facendo clic su un nodo nella mappa topologica hello, vengono visualizzate le proprietà di hello del nodo di hello, tra cui hello FQDN e indirizzo IP. Facendo clic su un hop Mostra l'indirizzo IP hello dell'hop hello.  
   ![topologia non integra - esempio di dettagli del percorso](./media/log-analytics-network-performance-monitor/npm-investigation06.png)

## <a name="provide-feedback"></a>Fornire commenti e suggerimenti

- **UserVoice** -è possibile registrare le proprie idee per le funzionalità di monitoraggio delle prestazioni di rete che si desidera toowork in. Visitare la [pagina UserVoice](https://feedback.azure.com/forums/267889-log-analytics/category/188146-network-monitoring).
- **Partecipa alla coorte**: l'aggiunta di nuovi clienti alla coorte è sempre motivo di grande interesse. Come parte di esso, sarà di accedere anticipatamente funzionalità toonew e contribuire a migliorare le prestazioni di rete. Per partecipare, compilare questo [sondaggio rapido](https://aka.ms/npmcohort).

## <a name="next-steps"></a>Passaggi successivi
* [Ricerca dei registri](log-analytics-log-searches.md) tooview dettagliate record dei dati delle prestazioni di rete.
