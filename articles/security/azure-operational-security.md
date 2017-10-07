---
title: Sicurezza operativa aaaAzure | Documenti Microsoft
description: Informazioni su Microsoft Operations Management Suite (OMS), i suoi servizi e il suo funzionamento.
services: security
documentationcenter: na
author: UnifyCloud
manager: swadhwa
editor: TomSh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/27/2017
ms.author: TomSh
ms.openlocfilehash: 85e0c74314ed97a53d395b209e348b779a5d14c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security"></a>Sicurezza operativa di Azure
## <a name="introduction"></a>Introduzione

### <a name="overview"></a>Panoramica
Sappiamo che sicurezza processo cloud hello e come sia importante che trovare informazioni accurate e aggiornate sulla sicurezza di Azure. Uno dei toouse delle ragioni migliore Azure di hello per le applicazioni e servizi è tootake sfruttare hello numerosi strumenti di sicurezza e funzionalità disponibili. Questi strumenti e funzionalità rendono toocreate possibili soluzioni di protezione sulla piattaforma Azure sicura hello. Windows Azure deve garantire riservatezza, integrità e disponibilità dei dati dei clienti, mantenendo allo stesso tempo la totale trasparenza nella rendicontazione.

i clienti toohelp comprendere meglio matrice hello di controlli di sicurezza implementata in Microsoft Azure da parte del cliente sia hello e prospettive operative di Microsoft, questo white paper, "Sicurezza operativa Azure", viene scritto che fornisce un analisi completa sicurezza operativa hello disponibile con Windows Azure.

### <a name="azure-platform"></a>Piattaforma Azure
Azure è una piattaforma di servizio cloud pubblico che supporta un'ampia gamma di sistemi operativi, linguaggi di programmazione, framework, strumenti, database e dispositivi. Azure può eseguire contenitori Linux con integrazione Docker, compilare app con JavaScript, Python, .NET, PHP, Java e Node.js e creare back-end per dispositivi iOS, Android e Windows. Servizio Cloud di Azure supporta hello stesse tecnologie milioni di sviluppatori e professionisti IT si basano su già e attendibile.

Quando si compila, o eseguire la migrazione di risorse IT a, un provider di servizi di cloud pubblico ci si basa sul tooprotect capacità dell'organizzazione che le applicazioni e dati con controlli di hello e servizi hello assicurano toomanage hello del basato su cloud Asset.

Infrastruttura di Azure è progettato da hello tooapplications di funzionalità per l'hosting contemporaneamente milioni di clienti e fornisce una base attendibile in cui le aziende possono soddisfare i requisiti di sicurezza. Inoltre, Azure offre un'ampia gamma di toocontrol possibilità hello e opzioni di protezione configurabili loro in modo che sia possibile personalizzare sicurezza toomeet hello requisiti delle distribuzioni dell'organizzazione. Questo documento offre informazioni sulle modalità con cui le funzionalità di sicurezza di Azure consentono di soddisfare questi requisiti.

### <a name="abstract"></a>Sunto
Sicurezza operativa Azure fa riferimento toohello servizi, i controlli e toousers disponibili funzionalità per la protezione dei dati, applicazioni e altre risorse in Microsoft Azure. Sicurezza operative di Azure si basa su un framework che incorpora informazioni hello ottenute tramite varie funzionalità che sono univoci tooMicrosoft, tra cui Microsoft Security Development Lifecycle (SDL), Microsoft Security Response Center hello hello programma e conoscenza approfondita dei panorama delle minacce alla sicurezza informatica hello.

Questo white paper descrive tooAzure di approccio di Microsoft per sicurezza operativa all'interno della piattaforma cloud di Microsoft Azure hello e include i servizi seguenti:
1.  [Azure Operations Management Suite](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview)

2.  [Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-intro)

3.  [Monitoraggio di Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview)

4.  [Azure Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview)

5.  [Azure Storage analytics](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics)

6.  [Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-whatis)


## <a name="microsoft-operations-management-suite"></a>Microsoft Operations Management Suite

Microsoft Operations Management Suite (OMS) è una soluzione di gestione IT per cloud ibrido hello hello. Utilizzato da solo o tooextend consente la distribuzione esistente di System Center, OMS hello la massima flessibilità e controllo per la gestione basata su cloud dell'infrastruttura.

![Microsoft Operations Management Suite](./media/azure-operational-security/azure-operational-security-fig1.png)

Con OMS, è possibile gestire qualsiasi istanza di qualsiasi cloud, inclusi i cloud locali, Azure, AWS, Windows Server, Linux, VMware e OpenStack, a un costo inferiore rispetto alle soluzioni della concorrenza. Compilato per HelloWorld prima di cloud, OMS offre la un nuovo toomanaging approccio dell'azienda che consente a hello più veloce e più conveniente toomeet nuove attività le problematiche e supportare nuovi carichi di lavoro, le applicazioni e ambienti cloud.

### <a name="oms-services"></a>Servizi OMS

funzionalità di base Hello di OMS viene fornita da un set di servizi in esecuzione in Azure. Ogni servizio fornisce una funzione di gestione specifico, ed è possibile combinare gli scenari di gestione diverso di servizi tooachieve.

| Service  | Descrizione|
| :------------- | :-------------|
| Log Analytics | Monitorare e analizzare hello disponibilità e prestazioni di diverse risorse incluse fisici e macchine virtuali. |
|Automazione | Automatizza i processi manuali ed applica le configurazioni per i computer fisici e le macchine virtuali. |
| Backup | Backup e ripristino dei dati critici. |
| Site Recovery | Offre disponibilità elevata per le applicazioni critiche. |

### <a name="log-analytics"></a>Log Analytics

[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) fornisce servizi di monitoraggio per OMS raccogliendo i dati delle risorse gestite in un repository centrale. Questi dati possono includere gli eventi, dati sulle prestazioni o dati personalizzati forniti tramite hello API. Una volta raccolti, hello sono disponibili dati per gli avvisi, l'analisi e l'esportazione.


Questo metodo consente tooconsolidate dati da diverse origini, pertanto è possibile combinare dati da servizi di Azure esistenti ambiente locale. Inoltre chiaramente separa raccolta hello di dati hello dall'azione di hello eseguita su tali dati in modo che tutte le azioni sono tooall disponibili tipi di dati.


![Log Analytics](./media/azure-operational-security/azure-operational-security-fig2.png)

servizio Registro Analitica Hello gestisce in modo sicuro i dati basati su cloud tramite hello dei seguenti metodi:
-   separazione dei dati
-   conservazione dei dati
-   sicurezza fisica
-   gestione di eventi imprevisti
-   conformità
-   certificazioni degli standard di sicurezza

### <a name="azure-backup"></a>Backup di Azure

[Backup di Azure](http://azure.microsoft.com/documentation/services/backup) fornisce i dati di backup e ripristino di servizi e fa parte di hello OMS suite di prodotti e servizi.
Protegge i dati delle applicazioni e li conserva per anni, senza investimenti di capitali e con costi operativi minimi. È possibile eseguire il backup dei dati dal server Windows fisici e virtuali inoltre tooapplication i carichi di lavoro, ad esempio SQL Server e SharePoint. E può essere utilizzato anche da [System Center Data Protection Manager (DPM)](https://en.wikipedia.org/wiki/System_Center_Data_Protection_Manager) tooreplicate protetti tooAzure dati per la ridondanza e l'archiviazione a lungo termine.


I dati protetti in Backup di Azure vengono archiviati in un insieme di credenziali di backup che si trova in una determinata area geografica. Hello dati vengono replicati all'interno hello stessa area geografica e, in base al tipo di hello dell'insieme di credenziali, possono essere replicati tooanother area per un'ulteriore resilienza.

### <a name="management-solutions"></a>Soluzioni di gestione
[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/oms-security-getting-started) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud.


Le [soluzioni di gestione](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-solutions) sono set predefiniti di logica che implementano un particolare scenario di gestione sfruttando uno o più servizi OMS. Diverse soluzioni sono disponibili da Microsoft e dai partner che è possibile aggiungere facilmente tooyour valore hello tooincrease di sottoscrizione di Azure dell'investimento in OMS. Come partner, è possibile creare la propria toosupport soluzioni le applicazioni e servizi e fornire loro toousers tramite hello Azure Marketplace o modelli di avvio rapido.


![Soluzioni di gestione](./media/azure-operational-security/azure-operational-security-fig4.png)

Un buon esempio di una soluzione che usa più funzionalità aggiuntive di servizi tooprovide è hello [soluzione di gestione degli aggiornamenti](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management). Questa soluzione Usa hello [Log Analitica](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview) agente per Windows e Linux toocollect informazioni sugli aggiornamenti necessari in ogni agente. Scrive questo repository Analitica Log toohello di dati in cui è possibile analizzare con un dashboard incluso.

Quando si crea una distribuzione, i runbook in [automazione di Azure](https://docs.microsoft.com/azure/automation/automation-intro) sono utilizzati tooinstall necessari aggiornamenti. Gestire l'intero processo nel portale di hello e non è necessario tooworry dettagli hello sottostante.

## <a name="azure-security-center"></a>Centro sicurezza di Azure

Il Centro sicurezza di Azure consente di proteggere le risorse di Azure. Integra il monitoraggio della sicurezza e la gestione dei criteri in tutte le sottoscrizioni di Azure. All'interno del servizio di hello, si è in grado di toodefine criteri non solo per le sottoscrizioni di Azure, ma anche contro [gruppi di risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#resource-groups), in modo da essere più granulare.

### <a name="security-policies-and-recommendations"></a>Criteri di sicurezza e raccomandazioni

Un criterio di sicurezza definisce il set di hello dei controlli, sono consigliate per le risorse nel gruppo di risorse o di sottoscrizione specificato hello.

Centro sicurezza PC, definire i criteri in base della società tooyour requisiti di protezione e riservatezza dei dati hello o il tipo di hello delle applicazioni.

![Criteri di sicurezza e raccomandazioni](./media/azure-operational-security/azure-operational-security-fig5.png)


Criteri che sono abilitati automaticamente nel livello di sottoscrizione hello propagano tooall gruppi di risorse all'interno di sottoscrizione hello come illustrato nel diagramma hello sul lato destro di hello:


### <a name="data-collection"></a>Raccolta dei dati

Centro sicurezza PC raccoglie i dati da tooassess le macchine virtuali (VM) lo stato di protezione, fornire consigli sulla sicurezza e ricevere un avviso toothreats. La prima volta che si accede al Centro sicurezza, la raccolta dati viene abilitata in tutte le macchine virtuali della sottoscrizione. È consigliabile la raccolta dei dati, ma è possibile rifiutare esplicitamente disattivando la raccolta dei dati hello criterio Centro sicurezza PC.

### <a name="data-sources"></a>Origini dati

- Centro sicurezza di Azure analizza i dati di hello seguente visibilità tooprovide origini nello stato di sicurezza, identificare le vulnerabilità consiglia le misure di attenuazione e rilevare minacce attive.

-   Servizi di Azure: Utilizza le informazioni di configurazione hello di servizi di Azure è stata distribuita mediante la comunicazione con il provider di risorse del servizio.

- Traffico di rete: usa i metadati del traffico di rete campionati dall'infrastruttura di Microsoft, ad esempio l'IP/porta di origine/destinazione, le dimensioni del pacchetto e il protocollo di rete.

-   Soluzioni partner: usa gli avvisi di sicurezza dalle soluzioni partner integrate, ad esempio firewall e soluzioni antimalware.

-   Macchine virtuali: usa informazioni sulla configurazione e informazioni sugli eventi di sicurezza, ad esempio registri eventi di Windows e log di controllo, log di IIS, messaggi syslog e file di dump di arresto anomalo del sistema dalle macchine virtuali.

### <a name="data-protection"></a>Protezione dati

i clienti toohelp impediranno, rilevano e rispondono toothreats, Centro sicurezza di Azure raccoglie ed elabora i dati relativi alla sicurezza, tra cui informazioni di configurazione, metadati, i registri eventi, i file di dump di arresto anomalo del sistema e altro ancora. Microsoft aderisce toostrict linee guida di conformità e sicurezza, dalla codifica toooperating un servizio.

-   **La separazione dei dati**: dati vengono mantenuti separati logicamente in ogni componente servizio hello. Tutti i dati vengono contrassegnati in base all'organizzazione. Tale contrassegno persiste per tutto hello del ciclo di vita dei dati e viene applicato a ogni livello del servizio hello.

-   **Accesso ai dati**: tooprovide consigli relativi alla sicurezza e provare a potenziali minacce alla sicurezza, il personale di Microsoft possono accedere alle informazioni raccolte o analizzati da servizi di Azure, inclusi i file di dump di arresto anomalo del sistema, elaborare gli eventi di creazione, il disco di macchina virtuale gli snapshot e gli elementi, che possono includere involontariamente i dati dei clienti o dati personali da quelli delle macchine virtuali. È conforme toohello [Microsoft Online Services termini e informativa sulla Privacy](http://www.microsoftvolumelicensing.com/DocumentSearch.aspx?Mode=3&DocumentTypeId=31), lo stato che Microsoft non utilizza i dati dei clienti o derivare da esso per scopi commerciali pubblicitari o simili.

-   **Utilizzo di dati**: Microsoft utilizza i modelli e sulle minacce visualizzata in più tenant tooenhance la funzionalità di rilevamento e prevenzione; avviene in conformità con impegni di privacy hello descritto in questo [sulla Privacy Istruzione](https://www.microsoft.com/privacystatement/OnlineServices/Default.aspx).

### <a name="data-location"></a>Posizione dei dati

Il Centro sicurezza di Azure raccoglie copie temporanee dei file di dump di arresto anomalo del sistema e le analizza per cercare le prove di tentativi di exploit e compromissioni riuscite. Centro sicurezza di Azure esegue l'analisi in hello stessa area geografica come hello dell'area di lavoro e le eliminazioni hello copie temporanee quando l'analisi sono stata completata. Gli elementi di computer vengono archiviati centralmente in hello stessa area come hello macchina virtuale.

-   **Account di archiviazione**: viene specificato un account di archiviazione per ogni area in cui sono in esecuzione macchine virtuali. In questo modo si toostore dati hello stessa area come macchina virtuale hello dal quale hello vengono raccolti i dati.

-   **Centro sicurezza di Azure Storage**: informazioni sugli avvisi di sicurezza, inclusi gli avvisi di partner, indicazioni e lo stato di integrità di protezione viene archiviate in modo centralizzato, attualmente negli Stati Uniti hello. Queste informazioni possono includere informazioni di configurazione correlati e gli eventi di sicurezza raccolti dalle macchine virtuali come tooprovide necessari è con stato integrità avviso, indicazioni o sicurezza hello sicurezza.


## <a name="azure-monitor"></a>Monitoraggio di Azure

Hello [OMS sicurezza](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources) e consente di controllo tooactively IT di monitorare tutte le risorse, che consentono di ridurre al minimo l'impatto di hello di eventi di sicurezza. OMS Security and Audit prevede domini di sicurezza che possono essere usati per il monitoraggio delle risorse. dominio di sicurezza Hello offre accesso rapido toooptions, per la sicurezza del monitoraggio hello domini seguenti sono illustrati in dettaglio:

-   Valutazione di software dannoso
-   Valutazione aggiornamenti
-   Identità e accesso.

Monitoraggio di Azure fornisce puntatori tooinformation su tipi specifici di risorse. Offre una visualizzazione, query, routing, avvisi, scalabilità automatica e l'automazione in entrambi i dati hello dell'infrastruttura di Azure (Log di attività) e ogni singola risorsa di Azure (log di diagnostica).

![Monitoraggio di Azure](./media/azure-operational-security/azure-operational-security-fig6.png)


Le applicazioni cloud sono complesse e hanno molte parti mobili. Il monitoraggio fornisce tooensure dati che l'applicazione resta alto e in esecuzione in uno stato integro. Consente inoltre toostave è impostata su off problemi potenziali o risolvere i problemi oltre quelle.

Inoltre, è possibile utilizzare Monitoraggio dati toogain approfondite sull'applicazione. Tali informazioni possono consentono di prestazioni dell'applicazione tooimprove o manutenibilità o automatizzare le operazioni che altrimenti richiederebbero un intervento manuale.

### <a name="azure-activity-log"></a>Azure Activity Log


È un log che fornisce informazioni approfondite operazioni hello eseguite sulle risorse nella sottoscrizione. Log attività Hello era noto in precedenza come "Registri di controllo" o "I registri operativi", poiché segnala gli eventi di Pannello di controllo per le sottoscrizioni.

![Azure Activity Log](./media/azure-operational-security/azure-operational-security-fig7.png)

Hello registro attività, consentono di determinare hello ' cosa, chi e quando ' per le operazioni (PUT, POST, DELETE) eseguite su risorse hello nella sottoscrizione di scrittura. È anche possibile comprendere lo stato di hello dell'operazione di hello e altre proprietà pertinenti. non include Hello Log attività di lettura (GET) operazioni o per risorse che utilizzano il modello classico hello.

### <a name="azure-diagnostic-logs"></a>Log di diagnostica di Azure

Questi log vengono emessi da una risorsa e forniscono dati completo e frequenti sull'operazione di hello di tale risorsa. contenuto Hello di questi log varia in base al tipo di risorsa.

Ad esempio, i log del sistema eventi di Windows sono una categoria di log di diagnostica per le macchine virtuali, i BLOB e le tabelle, mentre i log della coda sono categorie di log di diagnostica per gli account di archiviazione.

I log di diagnostica diversi da hello [Log attività (precedentemente noto come registro operativo o di Log di controllo)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). log attività Hello fornisce informazioni approfondite operazioni hello eseguite sulle risorse nella sottoscrizione. I log di diagnostica forniscono informazioni approfondite sulle operazioni che la risorsa esegue automaticamente.

### <a name="metrics"></a>Metrica

Monitoraggio di Azure consente tooconsume telemetria toogain visibilità hello prestazioni e l'integrità dei carichi di lavoro in Azure. Hello più importanti dei dati di telemetria di Azure è metriche hello (detto anche i contatori delle prestazioni) generate da Azure più risorse. Monitoraggio di Azure offre diversi modi tooconfigure e utilizzare tali [metriche](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) per il monitoraggio e risoluzione dei problemi. Le metriche sono fonte utile di telemetria e consentono di hello toodo seguenti attività:

-   **Tenere traccia delle prestazioni di hello** della risorsa (ad esempio un'app di macchina virtuale, sito Web o logica) per tracciare la metrica in un grafico del portale e blocco dashboard tooa grafico.

-   **Ricevere notifiche di un problema** che impatti hello delle prestazioni della risorsa quando una metrica supera una determinata soglia.

-   **Configurare le azioni automatiche**, ad esempio il ridimensionamento automatico di una risorsa o l'esecuzione di un runbook quando una metrica supera una determinata soglia.

-   **Eseguire analisi avanzate** o creare report relativi alle tendenze delle prestazioni o di uso della risorsa.

-   **Archivio** hello cronologia delle prestazioni o l'integrità della risorsa per la conformità o a fini di controllo.

### <a name="azure-diagnostics"></a>Diagnostica Azure

È una funzionalità di hello all'interno di Azure che consente la raccolta hello dei dati di diagnostica in un'applicazione distribuita. È possibile utilizzare l'estensione diagnostica hello da varie origini diverse. Sono attualmente supportati [ruoli Web e di lavoro del servizio cloud di Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [macchine virtuali di Azure](https://docs.microsoft.com/azure/virtual-machines/windows/overview) che eseguono Microsoft Windows e [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics). Altri servizi di Azure dispongono di propri strumenti di diagnostica separati.

## <a name="azure-network-watcher"></a>Azure Network Watcher

Il controllo della sicurezza della rete è fondamentale per rilevare le vulnerabilità e garantire la conformità con il modello di governance normativo e della sicurezza IT. Con la visualizzazione di gruppo di sicurezza, è possibile recuperare le regole di sicurezza e il gruppo di sicurezza di rete hello configurato e hello regole di sicurezza efficace. Con l'elenco di hello delle regole applicate, è possibile determinare le porte hello che sono aperti e valutare la vulnerabilità di rete.

[Controllo di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) è un servizio consente toomonitor internazionale e diagnosticare le condizioni a un livello di rete in, a e da Azure. Diagnostica di rete e gli strumenti di visualizzazione disponibili con Watcher di rete consentono di comprendere, diagnosticare e ottenere rete tooyour insights in Azure. Il servizio include l'acquisizione pacchetti, l'hop successivo, la verifica del flusso IP, la visualizzazione dei gruppi di sicurezza e i registri dei flussi dei gruppi di sicurezza di rete. Monitoraggio a livello di scenario è inclusa una visualizzazione di tooend finale delle risorse di rete in Monitoraggio risorse di rete di contrasto tooindividual.

![Azure Network Watcher](./media/azure-operational-security/azure-operational-security-fig8.png)

Watcher di rete presenta attualmente hello seguenti funzionalità:

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview">Log di controllo</a>**-vengono registrate sulle operazioni eseguite come parte della configurazione di hello delle reti. Questi registri possono essere visualizzati nel portale di Azure hello o recuperati utilizzando strumenti quali Power BI o gli strumenti di terze parti. I log di controllo sono disponibili tramite il portale di hello, PowerShell, CLI e API Rest. Per altre informazioni sui log di controllo, vedere l'articolo relativo alle operazioni di controllo con Gestione risorse. I log di controllo sono disponibili per le operazioni eseguite su tutte le risorse di rete.


-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview">Verifica flusso IP</a>** - Controlla se un pacchetto viene accettato o rifiutato in base ai relativi parametri sul flusso di informazioni, costituiti da informazioni a 5 tuple, ovvero l'indirizzo IP di destinazione, l'indirizzo IP di origine, la porta di destinazione, la porta di origine e il protocollo. Se i pacchetti hello viene negato da un gruppo di sicurezza di rete, viene restituito regola hello e gruppo di sicurezza di rete che i pacchetti hello negato.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview">Hop successivo</a>**  -determina hello hop successivo per i pacchetti hello infrastruttura di rete di Azure, consentendo di route definite dall'utente non è configurato correttamente qualsiasi toodiagnose indirizzato.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview">Visualizzazione del gruppo di sicurezza</a>**  -Ottiene le regole di sicurezza efficace e applicato hello che vengono applicate in una macchina virtuale.

-   **<a href="https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview">Registrazione NSG flusso</a>**  -flusso di log per i gruppi di sicurezza di rete consentono di toocapture registri tootraffic correlati che vengono concesse o negate le regole di sicurezza hello gruppo hello. flusso di Hello è definito dalle informazioni tupla con 5: indirizzo IP di origine, IP di destinazione, porta di origine, destinazione porta e protocollo.

## <a name="azure-storage-analytics"></a>Analisi archiviazione di Azure

[Archiviazione Analitica](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) può archiviare le metriche che includono transazioni aggregate le statistiche e dati sulla capacità del servizio di archiviazione tooa richieste. Le transazioni vengono segnalate sia a livello di operazione API hello e a livello di servizio di archiviazione hello, e la capacità è a livello di servizio di archiviazione hello. Dati di metrica possono essere utilizzati tooanalyze utilizzo di servizi di archiviazione, diagnosticare i problemi con le richieste effettuate al servizio di archiviazione hello e tooimprove hello prestazioni delle applicazioni che utilizzano un servizio.

L'[Analisi archiviazione di Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) esegue la registrazione e restituisce i dati delle metriche per un account di archiviazione. È possibile usare questo richieste tootrace dati, analizzare le tendenze di utilizzo e diagnosticare i problemi con l'account di archiviazione. La registrazione Analitica di archiviazione è disponibile per hello [servizi Blob, coda e tabella](https://docs.microsoft.com/azure/storage/storage-introduction). Archiviazione Analitica registra informazioni dettagliate sul servizio di archiviazione tooa richieste riuscite e non riuscite.

Queste informazioni possono essere utilizzati toomonitor singole richieste e toodiagnose problemi con un servizio di archiviazione. Le richieste vengono registrate in base al massimo sforzo. Le voci di log vengono create solo se esistono richieste effettuate per l'endpoint del servizio hello. Per esempio se un account di archiviazione dispone di attività nel relativo endpoint Blob ma non nel relativo endpoint accodamento o tabelle, solo i registri relativi toohello servizio Blob viene creato.

toouse Analitica di archiviazione, è necessario abilitarla singolarmente per ogni servizio desiderato toomonitor. È possibile abilitarla in hello [portale di Azure](https://portal.azure.com/); per informazioni dettagliate, vedere [monitorare un account di archiviazione nel portale di Azure hello](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account). È anche possibile abilitare Analitica di archiviazione a livello di programmazione tramite hello API REST o libreria client hello. Utilizzare hello Set Service Properties operazione tooenable archiviazione Analitica singolarmente per ogni servizio.

dati aggregati Hello viene archiviati in un noto blob (per la registrazione) e in tabelle note (per la metrica), che sono accessibili tramite il servizio Blob di hello e API del servizio tabelle.

Archiviazione Analitica pone un limite di 20 TB sulla quantità hello di dati archiviati che sia indipendenti dal limite totale di hello dell'account di archiviazione. Tutti i log vengono archiviati in [BLOB in blocchi](https://docs.microsoft.com/azure/storage/storage-analytics) all'interno di un contenitore denominato $logs, che viene creato automaticamente quando viene abilitata l'Analisi archiviazione per un account di archiviazione.

Hello seguenti le azioni eseguite da archiviazione Analitica sono fatturabile:

-   BLOB toocreate richieste per la registrazione
-   Entità della tabella toocreate richieste per le metriche.

> [!Note]
> Per altre informazioni sulla fatturazione e sui criteri di conservazione dei dati, vedere [Storage Analytics and Billing](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing) (Analisi archiviazione e fatturazione).
> Per ottenere prestazioni ottimali, si desidera toolimit hello di dischi utilizzati elevata collegata toohello macchina virtuale tooavoid possibili la limitazione delle richieste. Se non tutti i dischi sono in uso elevata a hello contemporaneamente, account di archiviazione hello può supportare un disco numero più grande.

> [!Note]
> Per informazioni sui limiti dell'account di archiviazione, vedere [Obiettivi di scalabilità e prestazioni per Archiviazione di Azure](https://docs.microsoft.com/azure/storage/storage-scalability-targets).


viene registrato i seguenti tipi di richieste autenticate e anonime Hello.

| Autenticata  | Anonima|
| :------------- | :-------------|
| Richieste riuscite | Richieste riuscite |
|Richieste non riuscite, tra cui errori di timeout, limitazione, rete, autorizzazione e di altro tipo | Richieste tramite una firma di accesso condiviso (SAS), incluse le richieste riuscite e non riuscite |
| Richieste tramite una firma di accesso condiviso (SAS), incluse le richieste riuscite e non riuscite |Errori di timeout per client e server |
|   Richiede i dati tooanalytics |    Richieste GET non riuscite con codice di errore 304 (non modificate) |
| Le richieste eseguite dalla stessa Analisi archiviazione, ad esempio, la creazione oppure l'eliminazione di log, non vengono registrate. Un elenco completo dei dati hello registrato è documentato in hello [archiviazione Analitica registrazione minima delle operazioni e messaggi di stato](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) e [formato di archiviazione Analitica Log](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format) argomenti. | Tutte le altre richieste anonime non riuscite non vengono registrate. Un elenco completo dei dati hello registrato è documentato in hello [archiviazione Analitica registrazione minima delle operazioni e messaggi di stato](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-logged-operations-and-status-messages) e [formato di archiviazione Analitica Log](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-log-format). |
## <a name="azure-active-directory"></a>Azure Active Directory

Azure AD include anche una suite completa di funzionalità per la gestione delle identità, tra cui la Multi-Factor Authentication, la registrazione dei dispositivi, la gestione self-service delle password e dei gruppi, la gestione degli account con privilegi, il controllo degli accessi in base al ruolo, il monitoraggio dell'utilizzo dell'applicazione, il controllo avanzato e il monitoraggio e gli avvisi relativi alla sicurezza.

-   Miglioramento della sicurezza delle applicazioni grazie all'autenticazione a più fattori e all'accesso condizionale di Azure AD.

-   Monitoraggio dell'utilizzo delle applicazioni e protezione dell'attività da minacce avanzate, grazie alla creazione di report e al monitoraggio della sicurezza.

Azure Active Directory (Azure AD) include la sicurezza, l’attività e i report di controllo per la directory. [Report di controllo di Azure Active Directory Hello](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) consentono ai clienti con privilegiata tooidentify azioni che si sono verificati in Azure Active Directory. Le azioni con privilegi includono modifiche elevazione (ad esempio, creazione del ruolo o la reimpostazione della password), modificare le configurazioni di criteri (ad esempio criteri password) o configurazione toodirectory modifiche (ad esempio, le modifiche toodomain impostazioni di federazione).

report di Hello forniscono record di controllo hello per nome dell'evento hello, attore hello che ha eseguito l'azione di hello, risorse di destinazione hello interessata dalla modifica hello e hello data e ora (UTC). I clienti sono elenco hello tooretrieve in grado di eventi di controllo per Azure Active Directory tramite hello [portale di Azure](https://portal.azure.com/), come descritto in [consente di visualizzare il log di controllo](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Di seguito è riportato un elenco di report hello inclusi:

| Report sulla sicurezza  | Report sull’attività| Report di controllo |
| :------------- | :-------------| :-------------|
|Accessi da origini sconosciute | Utilizzo dell'applicazione: riepilogo | Report di controllo della Directory |
|Accessi dopo più errori | Utilizzo dell'applicazione: dettagliato |   |
|Accessi da più aree geografiche | Dashboard dell'applicazione |  |
|Accessi da indirizzi IP con attività sospette |Errori di provisioning dell'account |  |
|Attività di accesso irregolare |Dispositivi dell’utente singolo |  |
|Accessi da dispositivi potenzialmente infetti |Attività dell’utente singolo |   |
|Utenti con anomalie dell'attività di accesso |Report attività dei gruppi |   |
| |Report attività di registrazione per la reimpostazione password |   |
| |Attività di reimpostazione password |   | |



dati di Hello di questi report possono essere applicazioni tooyour utile, ad esempio i sistemi SIEM, controllo e strumenti di business intelligence. Hello Azure AD reporting [API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) forniscono l'accesso programmatico toohello dati tramite un set di API basata su REST. È possibile chiamare queste API da numerosi linguaggi di programmazione e strumenti.

Gli eventi in hello report di controllo di Azure AD vengono mantenuti per 180 giorni.

> [!Note]
> Per altre informazioni sulla conservazione dei report, vedere la pagina relativa ai [criteri di conservazione dei report di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Per i clienti che desiderano archiviare loro [eventi di controllo](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) per lunghi periodi di conservazione, hello Reporting API può essere utilizzato tooregularly gli eventi di controllo di pull in un archivio dati separato.

## <a name="summary"></a>Riepilogo

Riepiloghi questo articolo, proteggere la privacy e la protezione dei dati, offrendo al contempo software e servizi che consentono di gestiscono hello infrastruttura IT dell'organizzazione. Microsoft è consapevole che quando si affidano tooothers i relativi dati, necessarie per garantirne la sicurezza. Microsoft aderisce toostrict linee guida di conformità e sicurezza, dalla codifica toooperating un servizio. La sicurezza e la protezione dei dati sono altamente prioritarie per Microsoft.

Questo articolo descrive

-   Come dati vengono raccolti, elaborati e protetti in hello Operations Management Suite (OMS).

-   Come analizzare rapidamente gli eventi tra più origini di dati. Identificare i rischi di sicurezza e comprendere hello ambito e impatto dei danni di hello toomitigate minacce e attacchi di una violazione della sicurezza.

-   Come identificare i modelli di attacco visualizzando il traffico IP dannoso in uscita e i tipi di minaccia pericolosi. Comprendere in condizioni di sicurezza hello dell'intero ambiente indipendentemente dalla piattaforma.

-   Acquisire tutti hello eventi e log dati necessari per un controllo di sicurezza o la conformità. Barra hello tempo e risorse necessari toosupply con un completo, eseguire ricerca ed esportabile eventi e log set di dati di controllo di sicurezza.

<ul>
<li>Raccogliere gli eventi di sicurezza, controllo e analisi delle violazioni tookeep una chiusura dell'occhio gli asset:</li>
<ul>
<li>Comportamento di sicurezza</li>
<li>Errori rilevanti</li>
<li>Riepilogo delle minacce</li>
</ul>
</ul>

## <a name="next-steps"></a>Passaggi successivi

- [Progettazione e sicurezza operativa](https://www.microsoft.com/trustcenter/security/designopsecurity)

Microsoft progettare i servizi e di software con protezione presente toohelp verificare che l'infrastruttura cloud sia resiliente adeguato da attacchi.

- [Operations Management Suite | Sicurezza e Conformità](https://www.microsoft.com/cloud-platform/security-and-compliance)

Utilizzare Microsoft protezione dati e l'analisi tooperform più intelligente ed efficace il rilevamento delle minacce.

- [Pianificazione di Centro sicurezza di Azure e operazioni](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide) un set di passaggi e attività che è possibile seguire toooptimize requisiti di sicurezza dell'organizzazione e il modello di gestione di cloud in base all'utilizzo di centro di sicurezza.

