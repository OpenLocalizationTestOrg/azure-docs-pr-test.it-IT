---
title: hello aaaUse soluzione mappa del servizio in Operations Management Suite | Documenti Microsoft
description: "Mappa del servizio è una soluzione di Operations Management Suite che individua automaticamente i componenti dell'applicazione in Windows e mappe e i sistemi Linux hello la comunicazione tra servizi. Questo articolo fornisce informazioni dettagliate su come distribuire Mapping dei servizi nell'ambiente e su come usarlo in svariati scenari."
services: operations-management-suite
documentationcenter: 
author: daveirwin1
manager: jwhit
editor: tysonn
ms.assetid: 3ceb84cc-32d7-4a7a-a916-8858ef70c0bd
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 11/22/2016
ms.author: daseidma;bwren;dairwin
ms.openlocfilehash: f7c209182c9171cc520192ac13ca4d85174081b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-service-map-solution-in-operations-management-suite"></a>Utilizzare soluzioni di mapping servizio hello in Operations Management Suite
Mappa del servizio consente di individuare automaticamente i componenti dell'applicazione nei sistemi Windows e Linux e mappe hello la comunicazione tra servizi. Con una mappa del servizio, è possibile visualizzare i server in modo hello immaginano: come sistemi interconnessi che offrono servizi critici. Mappa del servizio illustra le connessioni tra server, i processi e le porte su qualsiasi architettura connesso TCP, senza alcuna configurazione diverso da hello installazione di un agente.

Questo articolo descrive i dettagli di hello dell'utilizzo di mappa del servizio. Per informazioni sulla configurazione di Mapping dei servizi e sugli agenti di caricamento, vedere [Configurare la soluzione di elenco dei servizi in Operations Management Suite (OMS)](operations-management-suite-service-map-configure.md).


## <a name="use-cases-make-your-it-processes-dependency-aware"></a>Casi di utilizzo: Riconoscimento delle dipendenze nei processi IT

### <a name="discovery"></a>Individuazione
Mapping dei servizi genera automaticamente una mappa di riferimento delle dipendenze tra server, processi e servizi di terze parti. Consente di individuare e si esegue il mapping di tutte le dipendenze TCP, identificazione connessioni categoria Sorpresa, i sistemi remoti di terze parti che dipendono e aree di scuro tootraditional dipendenze della rete, ad esempio Active Directory. Mappa del servizio individua le connessioni di rete che i sistemi gestiti tentativi toomake, consentono di identificare potenziali errori di configurazione di server, interruzione del servizio e i problemi di rete.

### <a name="incident-management"></a>Gestione di eventi imprevisti
Mappa del servizio consente di eliminare la possibilità di errore hello di isolare il problema visualizzando il modo in cui sono connessi i sistemi e influire su altro. Inoltre connessioni non riuscite tooidentifying, ma consente di identificare i servizi di bilanciamento del carico configurato in modo errato, sorprendente o eccessivo carico servizi critici e client, ad esempio computer di sviluppo per comunicare con sistemi tooproduction inaffidabili. Utilizzando i flussi di lavoro integrati con Operations Management Suite Change Tracking, è possibile vedere se un evento di modifica in un servizio o il computer di back-end illustra causa radice di hello di un evento imprevisto.

### <a name="migration-assurance"></a>Garanzia di migrazione
L'uso di Mapping dei servizi consente di pianificare in modo efficace, accelerare e convalidare le migrazioni di Azure, garantendo che non venga tralasciato nulla e non si verifichino interruzioni impreviste. È possibile scoprire interdipendenti tutti i sistemi che toomigrate necessità insieme, valutare la capacità e la configurazione di sistema e identificare se un sistema in esecuzione è ancora per gli utenti o è un candidato per la rimozione delle autorizzazioni invece di migrazione. Una volta completato spostamento hello, tooverify carico e l'identità del client che i sistemi di test è possibile verificare e i clienti si connettono. Al caso di problemi, le definizioni di pianificazione e firewall di subnet connessioni non riuscite nella mappa del servizio mappe punto toohello sistemi che richiedono una connettività.

### <a name="business-continuity"></a>Continuità aziendale
Se si utilizza Azure Site Recovery e necessario Guida definizione hello sequenza di ripristino per l'ambiente di applicazione, mappa del servizio possono automaticamente mostrano come sistemi si basano su loro tooensure che il piano di ripristino è affidabile. Scelta di un server critico o un gruppo e visualizzando i relativi client, è possibile identificare quali toorecover sistemi front-end dopo che il server di hello è ripristinato e sia disponibile. Osservando le dipendenze di back-end server critici, al contrario, è possibile identificare quali toorecover sistemi prima vengono ripristinati i sistemi lo stato attivo.

### <a name="patch-management"></a>Gestione delle patch
Mappa del servizio migliora l'utilizzo di Operations Management Suite System Update Assessment hello indica che gli altri team e i server dipendono dal servizio, pertanto è possibile notificare ai in anticipo prima di eseguire il sistema per l'applicazione di patch. Mapping dei servizi migliora anche la gestione delle patch in Operations Management Suite indicando se i servizi sono disponibili e connessi correttamente dopo l'applicazione delle patch e il riavvio.


## <a name="mapping-overview"></a>Panoramica sui mapping
Gli agenti di mappa del servizio raccoglieranno informazioni su tutti i processi di connessione TCP su hello server in cui sono stati installati e informazioni dettagliate su hello connessioni in ingresso e in uscita per ogni processo. Nell'elenco di hello nel riquadro di sinistra hello, è possibile selezionare i computer o gruppi che dispongono di mapping servizio agenti toovisualize le relative dipendenze in un intervallo di tempo specificato. Dipendenza macchina esegue il mapping dello stato attivo su un computer specifico e vengono visualizzate tutte le macchine hello client TCP diretti o i server del computer.  Le mappe del gruppo di computer mostrano insiemi di server e le relative dipendenze.

![Panoramica di Mapping dei servizi](media/oms-service-map/service-map-overview.png)

È possibile espandere macchine in hello tooshow di mappa hello processi in esecuzione con le connessioni di rete attive durante l'intervallo di tempo hello selezionato. Quando un computer remoto con un agente di mappa del servizio è espanso tooshow dettagli del processo, vengono visualizzati solo i processi che comunicano con computer lo stato attivo hello. conteggio Hello macchine front-end senza agenti che si connettono nella macchina di hello lo stato attivo è indicato sul lato sinistro di hello dei processi di hello a che si connettono. Computer attivo hello effettua una macchina di back-end tooa di connessione che non dispone di alcun agente, server back-end hello è incluso in un gruppo di porte del Server, insieme a toohello altre connessioni stesso numero di porta.

Per impostazione predefinita, mappa del servizio esegue il mapping Mostra hello ultimi 30 minuti di informazioni sulle dipendenze. Tramite i controlli in fase di hello in alto a sinistra di hello, è possibile eseguire query esegue il mapping per gli intervalli di tempo cronologia di backup tooone ora tooshow come la ricerca delle dipendenze in hello passato (ad esempio, durante un evento imprevisto o prima che si è verificata una modifica). I dati di Mapping dei servizi vengono archiviati per 30 giorni nelle aree di lavoro a pagamento e per 7 giorni nelle aree di lavoro gratuite.

## <a name="status-badges-and-border-coloring"></a>Notifiche di stato e colorazione del bordo
In hello nella parte inferiore di ogni server nella mappa hello può essere un elenco di comunicare informazioni sullo stato relative a server hello badge di stato. badge Hello indicano che alcune informazioni rilevanti per il server di hello da una delle integrazioni di soluzione hello Operations Management Suite. Fare clic su un badge accetta è direttamente toohello i dettagli dello stato di hello nel riquadro di destra hello. Hello attualmente le notifiche di stato disponibili includono gli avvisi, assistenza, le modifiche, sicurezza e aggiornamenti.

A seconda della gravità hello del badge di stato hello, bordi nodo computer possono essere rossa colorata (critica), giallo (avviso) o blu (informativi). colori Hello rappresentano lo stato più grave hello di uno qualsiasi dei badge di stato hello. Un bordo grigio indica un nodo senza indicatori di stato.

![Notifiche di stato](media/oms-service-map/status-badges.png)

## <a name="machine-groups"></a>Gruppi di computer
Gruppi di computer consentono di toosee esegue il mapping incentrato su un set di server, non solo uno in modo da visualizzare tutti i membri di un cluster di server o dell'applicazione a più livelli in una mappa hello.

Gli utenti di selezionare i server che appartengono a un gruppo e scegliere un nome per il gruppo di hello.  È quindi possibile scegliere tooview hello gruppo con tutti i relativi processi e le connessioni o visualizzare solo con processi hello e connessioni direttamente correlati toohello altri membri del gruppo di hello.

![Gruppo di computer](media/oms-service-map/machine-group.png)

### <a name="creating-a-machine-group"></a>Creazione di un gruppo di computer
toocreate un gruppo, selezionare hello o più macchine desiderato nelle macchine hello elenco e fare clic su **aggiungere toogroup**.

![Creare un gruppo](media/oms-service-map/machine-groups-create.png)

È possibile scegliere **Crea nuovo** e assegnare un nome gruppo hello.

![Assegnare un nome al gruppo](media/oms-service-map/machine-groups-name.png)

>[!NOTE]
>Gruppi di computer sono attualmente limitate too10 server, ma contiamo tooincrease questo limite non appena.

### <a name="viewing-a-group"></a>Visualizzazione di un gruppo
Dopo avere creato alcuni gruppi, è possibile visualizzare facendo clic sulla scheda gruppi hello.

![Scheda Gruppi](media/oms-service-map/machine-groups-tab.png)

Selezionare quindi la mappa hello hello Group name tooview per tale gruppo di computer.
![Gruppo di computer](media/oms-service-map/machine-group.png) macchine hello appartenenti al gruppo toohello indicate in bianco nella mappa hello.

Espansione hello gruppo elencherà macchine hello di hello gruppo di computer.

![Computer del gruppo di computer](media/oms-service-map/machine-groups-machines.png)

### <a name="filter-by-processes"></a>Filtrare in base ai processi
È possibile attivare o disattivare visualizzazione mappa hello tra che mostra tutti i processi e le connessioni in gruppo hello e hello solo quelle correlate direttamente toohello gruppo di computer.  visualizzazione predefinita di Hello è tooshow tutti i processi.  È possibile modificare la visualizzazione hello facendo clic sull'icona di filtro hello sopra mappa hello.

![Gruppo di filtri](media/oms-service-map/machine-groups-filter.png)

Quando **tutti i processi** è selezionata, la mappa hello includerà tutti i processi e le connessioni in ognuno dei computer hello in hello gruppo.

![Tutti i processi del gruppo di computer](media/oms-service-map/machine-groups-all.png)

Se si modifica hello vista tooshow solo **connesso al gruppo di processi**, verrà raggruppata mappa hello verso il basso tooonly tali processi e le connessioni che sono direttamente connessi tooother macchine nel gruppo di hello, creazione di una visualizzazione semplificata.

![Processi filtrati del gruppo di computer](media/oms-service-map/machine-groups-filtered.png)
 
### <a name="adding-machines-tooa-group"></a>Aggiungere il gruppo di computer tooa
tooadd macchine tooan di gruppo esistente, verificare hello caselle Avanti macchine toohello desiderato e quindi fare clic su **aggiungere toogroup**.  Quindi, scegliere il gruppo di hello che si vuole tooadd hello macchine.
 
### <a name="removing-machines-from-a-group"></a>Rimozione di computer da un gruppo
Nell'elenco gruppi hello, espandere macchine hello gruppo nome toolist hello in hello gruppo di computer.  Quindi, fare clic su hello i puntini di sospensione menu toohello computer successivo tooremove desiderato e scegliere **rimuovere**.

![Rimuovere il computer dal gruppo](media/oms-service-map/machine-groups-remove.png)

### <a name="removing-or-renaming-a-group"></a>Rimozione o assegnazione di un nuovo nome al gruppo
Fare clic su hello i puntini di sospensione menu successiva toohello nome del gruppo nell'elenco gruppi hello.

![Menu del gruppo di computer](media/oms-service-map/machine-groups-menu.png)


## <a name="role-icons"></a>Icone di ruolo
Alcuni processi svolgono ruoli particolari nei computer: server Web, server applicazioni, database e così via. Mappa del servizio annota processo e le caselle di computer con ruolo icone toohelp identificano un ruolo di hello immediatamente un processo o del server viene riprodotto.

| Icona del ruolo | Descrizione |
|:--|:--|
| ![Server Web](media/oms-service-map/role-web-server.png) | Server Web |
| ![Server app](media/oms-service-map/role-application-server.png) | Server applicazioni |
| ![Server di database](media/oms-service-map/role-database.png) | Server di database |
| ![Server LDAP](media/oms-service-map/role-ldap.png) | Server LDAP |
| ![Server SMB](media/oms-service-map/role-smb.png) | Server SMB |

![Icone di ruolo](media/oms-service-map/role-icons.png)


## <a name="failed-connections"></a>Connessioni non riuscite
Connessioni non riuscite vengono visualizzate nella mappa del servizio viene eseguito il mapping per i processi e i computer, con una linea rossa tratteggiata che indica che un sistema client non è possibile eseguire tooreach una porta o il processo. Connessioni non riuscite vengono segnalate da qualsiasi sistema con un agente di mapping servizio distribuito, se tale sistema è hello una connessione di hello non riuscita durante il tentativo. Mappa del servizio misure di questo processo osservando i socket TCP che non soddisfano tooestablish una connessione. Questo errore potrebbe causare da un firewall, una configurazione errata hello client o server, o un servizio remoto non è disponibile.

![Connessioni non riuscite](media/oms-service-map/failed-connections.png)

Le informazioni sulle connessioni non riuscite facilitano la risoluzione dei problemi, la convalida della migrazione, l'analisi di sicurezza e la comprensione dell'intera architettura. Connessioni non riuscite vengono talvolta innocue, ma spesso puntano direttamente problema tooa, ad esempio un ambiente di failover improvvisamente diventi irraggiungibile o due livelli di applicazione in grado tootalk dopo la migrazione di un cloud.

## <a name="client-groups"></a>Gruppi di client
Gruppi di client disponibili finestre nella mappa hello che rappresentano i computer client che non dispongono di agenti di dipendenza. Un singolo gruppo di Client rappresenta i client hello per un singolo processo o computer.

![Gruppi di client](media/oms-service-map/client-groups.png)

indirizzi IP di hello toosee dei server hello in un gruppo di Client, hello selezionare gruppo. il contenuto di Hello del gruppo di hello è elencato in hello **proprietà gruppo di Client** riquadro.

![Proprietà del gruppo di client](media/oms-service-map/client-group-properties.png)

## <a name="server-port-groups"></a>Gruppi di porte di server
I gruppi di porte di server sono costituiti da caselle che rappresentano le porte sui server privi di agenti di dipendenza. finestra di Hello contiene porta hello del server e un conteggio del numero di hello del server con la porta toothat connessioni. Espandere le connessioni e hello casella toosee hello singoli server. Se nella casella di hello è presente un solo server, è elencato hello nome o indirizzo IP.

![Gruppi di porte di server](media/oms-service-map/server-port-groups.png)

## <a name="context-menu"></a>Menu di scelta rapida
Fare clic su hello i puntini di sospensione (…) nella parte superiore di hello destra di un server consente di visualizzare menu di scelta rapida hello del server.

![Connessioni non riuscite](media/oms-service-map/context-menu.png)

### <a name="load-server-map"></a>Caricare la mappa del server
Fare clic su **carico Server mappa** consente di passare tooa nuova mappa con il server selezionato di hello come nuovo computer lo stato attivo di hello.

### <a name="show-self-links"></a>Mostra collegamenti automatici
Fare clic su **Self-Links Mostra** ridisegna hello server nodo, compresi eventuali self link, quali sono le connessioni TCP che iniziano e finiscono processi all'interno di server hello. Se self Link sono visualizzati, hello troppo le modifiche dei comandi menu**Self-Links nascondere**, in modo che è possibile disattivarli.

## <a name="computer-summary"></a>Riepilogo del computer
Hello **riepilogo macchina** riquadro include una panoramica di un server del sistema operativo, i conteggi di dipendenza e dati da altre soluzioni di Operations Management Suite. Tali dati includono le metriche delle prestazioni, i ticket del Service Desk, il rilevamento delle modifiche, la sicurezza e gli aggiornamenti.

![Riquadro di riepilogo del computer](media/oms-service-map/machine-summary.png)

## <a name="computer-and-process-properties"></a>Proprietà dei computer e dei processi
Quando si passa una mappa della mappa del servizio, è possibile selezionare i computer e i processi toogain un contesto aggiuntivo sulle relative proprietà. Le macchine forniscono informazioni sui nomi DNS, nei indirizzi IPv4, CPU e memoria capacità, tipo di macchina virtuale, il sistema operativo e versione, ultima riavviare ora e ID hello dei relativi agenti di Operations Management Suite e mappa del servizio.

![Riquadro Proprietà del computer](media/oms-service-map/machine-properties.png)

È possibile raccogliere i dettagli dei processi dai metadati del sistema operativo relativi ai processi in esecuzione che includono nome e descrizione del processo, nome utente e dominio, in Windows, nome dell'azienda, nome e versione del prodotto, directory di lavoro, riga dei comandi e ora di inizio del processo.

![Riquadro Proprietà del processo](media/oms-service-map/process-properties.png)

Hello **riepilogo del processo** riquadro fornisce ulteriori informazioni sulla connettività del processo di hello, tra cui la versione, le connessioni in ingresso e in uscita, le porte con binding e connessioni non riuscite.

![Riquadro del riepilogo del processo](media/oms-service-map/process-summary.png)

## <a name="operations-management-suite-alerts-integration"></a>Integrazione degli avvisi in Operations Management Suite
Mappa del servizio si integra con gli avvisi di Operations Management Suite tooshow generati avvisi per il server selezionato di hello nell'intervallo di tempo selezionato hello. server Hello viene visualizzata un'icona, se sono presenti avvisi correnti, hello e **macchina avvisi** riquadro Elenca gli avvisi di hello.

![Riquadro degli avvisi del computer](media/oms-service-map/machine-alerts.png)

tooenable mappa del servizio toodisplay relativi avvisi, creare una regola di avviso che viene generato per un computer specifico. avvisi corretto toocreate:
- Includere una clausola toogroup dal computer (ad esempio, **in base all'intervallo Computer 1 minuto**).
- Scegliere tooalert in base alle metrica misura.

![Configurazione degli avvisi](media/oms-service-map/alert-configuration.png)


## <a name="operations-management-suite-log-events-integration"></a>Integrazione degli eventi del registro in Operations Management Suite
Mappa del servizio si integra con ricerca nei Log tooshow un conteggio di tutti gli eventi di log disponibili per il server selezionato hello durante l'intervallo di tempo hello selezionato. È possibile fare clic su qualsiasi riga hello elenco di eventi conteggi toojump tooLog ricerca e visualizzare hello singolo registro eventi.

![Riquadro degli eventi del registro del computer](media/oms-service-map/log-events.png)

## <a name="operations-management-suite-service-desk-integration"></a>Integrazione del Service Desk in Operations Management Suite
Integrazione di mappa del servizio con connettore di gestione del servizio IT hello avviene automaticamente quando entrambe le soluzioni sono abilitate e configurate nell'area di lavoro di Operations Management Suite. integrazione di Hello nella mappa del servizio è denominato "Service Desk". Per informazioni vedere [Gestire centralmente gli elementi di lavoro ITSM con IT Service Management Connector](https://docs.microsoft.com/azure/log-analytics/log-analytics-itsmc-overview).

Hello **macchina Service Desk** riquadro Elenca tutti gli eventi di gestione dei servizi IT per il server selezionato di hello nell'intervallo di tempo hello selezionato. Se sono presenti elementi correnti e li elenca riquadro macchina Service Desk hello, server Hello Visualizza un'icona.

![Riquadro del Service Desk del computer](media/oms-service-map/service-desk.png)

elemento hello tooopen nella soluzione ITSM connessa, fare clic su **Visualizza elemento di lavoro**.

Fare clic su Dettagli hello tooview dell'elemento hello in Log Search, **Mostra in Log Search**.


## <a name="operations-management-suite-change-tracking-integration"></a>Integrazione del Rilevamento modifiche in Operations Management Suite
L'integrazione del rilevamento delle modifiche in Mapping dei servizi è automatica quando entrambe le soluzioni sono abilitate e configurate nell'area di lavoro Operations Management Suite.

Hello **macchina Change Tracking** riquadro Elenca tutte le modifiche, con hello più recente prima di tutto, insieme a un collegamento di toodrill verso il basso tooLog cercare ulteriori dettagli.

![Riquadro di rilevamento modifiche del computer](media/oms-service-map/change-tracking.png)

immagine che segue Hello è una visualizzazione dettagliata di un evento di modifica configurazione che potrebbero verificarsi dopo aver selezionato **Mostra nel Log Analitica**.

![Evento ConfigurationChange](media/oms-service-map/configuration-change-event.png)


## <a name="operations-management-suite-performance-integration"></a>Integrazione delle prestazioni in Operations Management Suite
Hello **le prestazioni delle macchine** riquadro Visualizza le metriche di prestazioni standard per il server selezionato hello. metriche di Hello includono l'utilizzo della CPU, utilizzo della memoria, byte di rete inviati e ricevuti e un elenco di processi principali hello byte di rete inviati e ricevuti. dati sulle prestazioni di rete hello di tooget, è necessario anche abilitare hello soluzione Wire Data 2.0 in Operations Management Suite.

![Riquadro delle prestazioni del computer](media/oms-service-map/machine-performance.png)


## <a name="operations-management-suite-security-integration"></a>Integrazione della sicurezza in Operations Management Suite
L'integrazione di Sicurezza e controllo in Mapping dei servizi è automatica quando entrambe le soluzioni sono abilitate e configurate nell'area di lavoro Operations Management Suite.

Hello **protezione macchina** riquadro Visualizza i dati hello soluzione Operations Management Suite Security and Audit per server selezionato hello. riquadro Hello elenca un riepilogo di eventuali problemi di sicurezza in attesa per server hello durante l'intervallo di tempo hello selezionato. Fare clic su una delle esercitazioni di problemi di sicurezza hello verso il basso in una ricerca di Log per informazioni dettagliate su di essi.

![Riquadro relativo alla sicurezza dei computer](media/oms-service-map/machine-security.png)


## <a name="operations-management-suite-updates-integration"></a>Integrazione degli aggiornamenti in Operations Management Suite
L'integrazione della Gestione aggiornamenti in Mapping dei servizi è automatica quando entrambe le soluzioni sono abilitate e configurate nell'area di lavoro Operations Management Suite.

Hello **aggiornamenti macchina** riquadro Visualizza i dati da una soluzione di gestione degli aggiornamenti di Operations Management Suite per server selezionato hello hello. riquadro Hello elenca un riepilogo di eventuali aggiornamenti mancanti per il server di hello durante l'intervallo di tempo hello selezionato.

![Riquadro di rilevamento modifiche del computer](media/oms-service-map/machine-updates.png)

## <a name="log-analytics-records"></a>Record di Log Analytics
I dati di inventario di computer e processi di Mapping dei servizi sono disponibili per la [ricerca](../log-analytics/log-analytics-log-searches.md) in Log Analytics. È possibile applicare questo tooscenarios di dati che includono la pianificazione della migrazione, analisi della capacità, l'individuazione e risoluzione dei problemi di prestazioni su richiesta.

Viene generato un record per ogni ora per ogni computer univoco e un processo, inoltre i record di toohello che vengono generati quando un processo o un computer viene avviato o è in-boarded tooService mappati. Questi record dispongono di proprietà di hello in hello le tabelle seguenti. Hello campi e i valori negli eventi ServiceMapComputer_CL hello mappa toofields di hello risorsa macchina in hello ServiceMap API di gestione risorse di Azure. Hello campi e i valori negli eventi ServiceMapProcess_CL hello eseguire il mapping campi toohello di hello risorsa di processo in hello ServiceMap API di gestione risorse di Azure. il campo di ResourceName_s Hello corrisponde il campo nome hello nella risorsa di gestione delle risorse di hello corrispondente. 

>[!NOTE]
>Aumentare le funzionalità di mappa del servizio, questi campi sono toochange soggetto.

Sono disponibili proprietà generata internamente, è possibile usare i computer e processi univoco tooidentify:

- Computer: Utilizzare ResourceId o ResourceName_s toouniquely identificare un computer all'interno di un'area di lavoro di Operations Management Suite.
- Processo: Utilizzare ResourceId toouniquely identificano un processo all'interno di un'area di lavoro di Operations Management Suite. ResourceName_s è univoco nel contesto di hello del computer hello in cui hello processo è in esecuzione (MachineResourceName_s) 

Poiché per un processo specificato e un computer in un intervallo di tempo specificato, possono esistere più record, le query possono restituire più di un record per hello stesso computer o processo. tooinclude hello solo record più recente, aggiungere "| query toohello deduplicazione ResourceId".

### <a name="servicemapcomputercl-records"></a>Record ServiceMapComputer_CL
I record che contengono il tipo *ServiceMapComputer_CL* includono dati di inventario relativi ai server con agenti del modello dei servizi. Tali record sono riportate le hello in hello nella tabella seguente:

| Proprietà | Descrizione |
|:--|:--|
| Tipo | *ServiceMapComputer_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Identificatore univoco per un computer all'interno dell'area di lavoro hello Hello |
| ResourceName_s | Identificatore univoco per un computer all'interno dell'area di lavoro hello Hello |
| ComputerName_s | FQDN del computer Hello |
| Ipv4Addresses_s | Un elenco di indirizzi IPv4 del server hello |
| Ipv6Addresses_s | Un elenco di indirizzi IPv6 del server hello |
| DnsNames_s | Una matrice di nomi DNS |
| OperatingSystemFamily_s | Windows o Linux |
| OperatingSystemFullName_s | nome completo del sistema operativo hello Hello  |
| Bitness_s | numero di bit Hello della macchina di hello (32 bit o 64 bit)  |
| PhysicalMemory_d | memoria fisica di Hello in MB |
| Cpus_d | numero di Hello di CPU |
| CPUSpeed_d | la velocità della CPU in MHz Hello|
| VirtualizationState_s | *sconosciuto*, *fisico*, *virtuale*, *hypervisor* |
| VirtualMachineType_s | *hyperv*, *vmware* e così via |
| VirtualMachineNativeMachineId_g | ID macchina virtuale assegnato dall'hypervisor Hello |
| VirtualMachineName_s | nome Hello di hello VM |
| BootTime_t | fase di avvio Hello |



### <a name="servicemapprocesscl-type-records"></a>Record con tipo ServiceMapProcess_CL
I record con tipo *ServiceMapProcess_CL* includono dati di inventario relativi ai processi con connessione TCP eseguiti sui server con agenti del modello dei servizi. Tali record sono riportate le hello in hello nella tabella seguente:

| Proprietà | Descrizione |
|:--|:--|
| Tipo | *ServiceMapProcess_CL* |
| SourceSystem | *OpsManager* |
| ResourceId | Identificatore univoco per un processo all'interno dell'area di lavoro hello Hello |
| ResourceName_s | Identificatore univoco di Hello per un processo interno macchina hello in cui è in esecuzione|
| MachineResourceName_s | nome del computer hello risorse Hello |
| ExecutableName_s | nome Hello dell'eseguibile del processo hello |
| StartTime_t | ora di inizio Hello processo pool |
| FirstPid_d | Hello PID prima nel pool di processi hello |
| Description_s | Descrizione del processo Hello |
| CompanyName_s | nome di Hello della società hello |
| InternalName_s | nome interno Hello |
| ProductName_s | nome di Hello del prodotto hello |
| ProductVersion_s | versione del prodotto Hello |
| FileVersion_s | versione del file Hello |
| CommandLine_s | riga di comando Hello |
| ExecutablePath _s | file eseguibile di Hello percorso toohello |
| WorkingDirectory_s | directory di lavoro Hello |
| UserName | account Hello quali hello processo è in esecuzione |
| UserDomain | dominio Hello quali hello processo è in esecuzione |


## <a name="sample-log-searches"></a>Ricerche di log di esempio

### <a name="list-all-known-machines"></a>Visualizzare tutti i computer noti
Type=ServiceMapComputer_CL | dedup ResourceId

### <a name="list-hello-physical-memory-capacity-of-all-managed-computers"></a>Capacità di memoria fisica hello elenco di tutti i computer gestiti.
Type=ServiceMapComputer_CL | select PhysicalMemory_d, ComputerName_s | Dedup ResourceId

### <a name="list-computer-name-dns-ip-and-os"></a>Visualizzare nome del computer, DNS, IP e sistema operativo.
Type=ServiceMapComputer_CL | select ComputerName_s, OperatingSystemFullName_s, DnsNames_s, IPv4Addresses_s  | dedup ResourceId

### <a name="find-all-processes-with-sql-in-hello-command-line"></a>Trova tutti i processi con "sql" nella riga di comando hello
Type=ServiceMapProcess_CL CommandLine_s = \*sql\* | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-resource-name"></a>Trovare un computer (record più recente) in base al nome di risorsa
Type=ServiceMapComputer_CL "m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="find-a-machine-most-recent-record-by-ip-address"></a>Trovare un computer, ovvero il record più recente, in base all’indirizzo IP
Type=ServiceMapComputer_CL "10.229.243.232" | dedup ResourceId

### <a name="list-all-known-processes-on-a-specified-machine"></a>Elencare tutti i processi noti su un computer specifico
Type=ServiceMapProcess_CL MachineResourceName_s="m-4b9c93f9-bc37-46df-b43c-899ba829e07b" | dedup ResourceId

### <a name="list-all-computers-running-sql"></a>Visualizzare tutti i computer che eseguono SQL
Type=ServiceMapComputer_CL ResourceName_s IN {Type=ServiceMapProcess_CL \*sql\* | Distinct MachineResourceName_s} | dedup ResourceId | Distinct ComputerName_s

### <a name="list-all-unique-product-versions-of-curl-in-my-datacenter"></a>Elencare tutte le versioni di prodotto univoche di curl nel data center
Type=ServiceMapProcess_CL ExecutableName_s=curl | Distinct ProductVersion_s

### <a name="create-a-computer-group-of-all-computers-running-centos"></a>Creare un gruppo di tutti i computer che eseguono CentOS
Type=ServiceMapComputer_CL OperatingSystemFullName_s = \*CentOS\* | Distinct ComputerName_s


## <a name="rest-api"></a>API REST
Tutti i dati di server, processo e alla dipendenza hello nella mappa del servizio è disponibile tramite hello [API REST di mappa](https://docs.microsoft.com/rest/api/servicemap/).


## <a name="diagnostic-and-usage-data"></a>Dati di diagnostica e di utilizzo
Microsoft raccoglie automaticamente i dati di utilizzo e prestazioni tramite l'utilizzo di hello servizio mappa del servizio. Microsoft utilizza questo tooprovide dati e migliorare la qualità di hello, sicurezza e integrità del servizio di mapping servizio hello. tooprovide accurata ed efficiente la risoluzione dei problemi funzionalità, i dati di hello includono informazioni sulla configurazione di hello del software, ad esempio sistema operativo e versione, l'indirizzo IP, nome DNS e nome della workstation. Microsoft non raccoglie nomi, indirizzi o altre informazioni di contatto.

Per ulteriori informazioni sulla raccolta dei dati e l'utilizzo, vedere hello [informativa sulla Privacy di servizi Online Microsoft](https://go.microsoft.com/fwlink/?LinkId=512132).


## <a name="next-steps"></a>Passaggi successivi
Altre informazioni, vedere [log ricerche](../log-analytics/log-analytics-log-searches.md) nei dati tooretrieve Analitica Log raccolti da una mappa del servizio.


## <a name="troubleshooting"></a>Risoluzione dei problemi
Vedere hello [risoluzione dei problemi di sezione del documento di configurazione di mapping servizio hello](operations-management-suite-service-map-configure.md#troubleshooting).


## <a name="feedback"></a>Commenti e suggerimenti
Per inviare commenti su Mapping dei servizi e sulla relativa documentazione,  Visitare la [pagina per i suggerimenti degli utenti](https://feedback.azure.com/forums/267889-log-analytics/category/184492-service-map), in cui è possibile suggerire funzionalità o votare i suggerimenti esistenti.
