---
title: Panoramica della sicurezza operativa aaaAzure | Documenti Microsoft
description: In questo articolo viene fornita una panoramica della sicurezza operativa Azure hello.
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: b91c7889660b32e4933c305007692bd6e1ded05f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-overview"></a>Panoramica sulla sicurezza operativa di Azure
Sicurezza operativa Azure fa riferimento toohello servizi, i controlli e toousers disponibili funzionalità per la protezione dei dati, applicazioni e altre risorse in Microsoft Azure. [Sicurezza operativa Azure](https://docs.microsoft.com/azure/security/azure-operational-security) è un framework che incorpora knowledge hello ottenuto tramite un'ampia gamma di funzionalità che sono univoci tooMicrosoft, tra cui Microsoft Security Development Lifecycle (SDL), Microsoft Security hello hello Programma Response Center e sensibilizzare complete panorama delle minacce sicurezza informatica hello.

Panoramica della sicurezza operativa Azure viene descritta la hello seguenti aree:

- Azure Operations Management Suite
-   Centro sicurezza di Azure
-   Monitoraggio di Azure
-   Azure Network Watcher
-   Analisi archiviazione di Azure
-   Azure Active Directory

## <a name="azure-operations-management-suite"></a>Azure Operations Management Suite
Il reparto IT è responsabile della gestione dei dati, tra cui hello stabilità e sicurezza di questi sistemi, applicazioni e dell'infrastruttura Data Center. Ottenere informazioni di sicurezza in ad aumentare gli ambienti IT complessi spesso richiede, tuttavia, le organizzazioni toocobble uniscono i dati da più sistemi di sicurezza e la gestione.

[Microsoft Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud.

OMS è una soluzione di gestione IT basata sul cloud con molte offerte, quali l'Automazione IT, Sicurezza e Conformità, Log Analytics e Backup e Ripristino. Di conseguenza, è un toomanage aiuto perfetto e proteggere l'infrastruttura IT, ovvero in locale e nel cloud hello.

funzionalità di base Hello di OMS viene fornita da un set di servizi in esecuzione in Azure. Ogni servizio fornisce una funzione di gestione specifico, ed è possibile combinare gli scenari di gestione diverso di servizi tooachieve. Lo strumento include:

-   Log Analytics
-   Automazione
-   Backup
-   Site Recovery

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) fornisce servizi di monitoraggio per OMS raccogliendo i dati delle risorse gestite in un repository centrale. Questi dati possono includere gli eventi, dati sulle prestazioni o dati personalizzati forniti tramite hello API. Una volta raccolti, hello sono disponibili dati per gli avvisi, l'analisi e l'esportazione. Questo metodo consente tooconsolidate dati da diverse origini in modo è possibile combinare dati da servizi di Azure con l'ambiente locale esistente. Inoltre chiaramente separa raccolta hello di dati hello dall'azione di hello eseguita su tali dati in modo che tutte le azioni sono tooall disponibili tipi di dati.

### <a name="automation"></a>Automazione
Microsoft [automazione di Azure](https://docs.microsoft.com/azure/automation/automation-intro) offre un modo per gli utenti tooautomate hello manuale, con esecuzione prolungata, soggette a errori e ripetute spesso le attività che sono in genere eseguite in un ambiente cloud e aziendali. Consente di risparmiare tempo e aumenta l'affidabilità di hello delle normali attività amministrative e anche le pianifica toobe automaticamente eseguiti a intervalli regolari. È possibile automatizzare i processi utilizzando runbook o automatizzare la gestione della configurazione tramite Configurazione dello stato desiderato.

### <a name="backup"></a>Backup
[Backup di Azure](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup) servizio hello basato su Azure è possibile utilizzare tooback (o proteggere) e il ripristino dei dati nel cloud di Microsoft hello. Backup di Azure sostituisce la soluzione di backup locale o esterna esistente con una soluzione basata sul cloud affidabile, sicura e conveniente. Backup di Azure offre più i componenti disponibili per download e distribuzione su computer appropriato hello, server, o nel cloud hello. componente Hello o agent, da distribuire dipende da ciò che si desidera tooprotect. Tutti i componenti di Backup di Azure (indipendentemente dal fatto per la protezione dei dati in locale o nel cloud hello) possono essere utilizzato tooback le credenziali di servizi di ripristino dati tooa in Azure. Vedere hello [tabella i componenti di Azure Backup](https://docs.microsoft.com/azure/backup/backup-introduction-to-azure-backup#which-azure-backup-components-should-i-use).

### <a name="site-recovery"></a>Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) fornisce la continuità aziendale gestendo la replica locale virtuale e tooAzure macchine fisiche o tooa di sito secondario. Se il sito primario non è disponibile, è possibile failover posizione secondaria toohello in modo che gli utenti possono continuare a lavorare e failback quando i sistemi restituiscono tooworking ordine. funzionalità di rilevamento minacce intelligente ed efficace.

## <a name="azure-active-directory"></a>Azure Active Directory
[Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-enable-sso-scenario) è una soluzione IDaaS (Identity as a Service) Microsoft completa che offre i vantaggi seguenti:

-   Abilitazione della gestione delle identità e degli accessi come servizio cloud.
-   Gestione centrale dell'accesso, accesso Single Sign-On (SSO) e creazione di report.
-   Supporta la gestione di accesso integrato per [migliaia di applicazioni](https://azure.microsoft.com/marketplace/active-directory/) nella raccolta di applicazione hello, tra cui Salesforce, Google Apps, Box, Concur e più.

Azure AD include anche un insieme completo di [funzionalità per la gestione delle identità](https://docs.microsoft.com/azure/security/security-identity-management-overview#security-monitoring-alerts-and-machine-learning-based-reports), tra cui l'[autenticazione a più fattori](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication), la [registrazione dei dispositivi]( https://docs.microsoft.com/azure/active-directory/active-directory-device-registration-overview), la [gestione self-service delle password](https://azure.microsoft.com/resources/videos/self-service-password-reset-azure-ad/), e dei [gruppi](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-update-your-own-password), la [gestione degli account con privilegi](https://docs.microsoft.com/azure/active-directory/active-directory-privileged-identity-management-configure), il [controllo degli accessi in base al ruolo](https://docs.microsoft.com/azure/active-directory/role-based-access-control-what-is), il [monitoraggio dell'utilizzo dell'applicazione](https://docs.microsoft.com/azure/active-directory/connect-health/active-directory-aadconnect-health), il [controllo avanzato](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-activity-audit-logs) e il [monitoraggio e avvisi relativi alla sicurezza](https://docs.microsoft.com/azure/operations-management-suite/oms-security-responding-alerts).

Con Azure Active Directory, tutte le applicazioni pubblicate per i partner e clienti (business o consumer) hanno hello stesse funzionalità di gestione di identità e accessi. In questo modo si toosignificantly ridurre i costi operativi.

## <a name="azure-security-center"></a>Centro sicurezza di Azure
[Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-get-started) consente di impedire, rilevare e rispondere toothreats con una maggiore visibilità e controllo sui hello protezione delle risorse di Azure. Offre funzionalità integrate di monitoraggio della sicurezza e gestione dei criteri tra le sottoscrizioni, facilita il rilevamento delle minacce che altrimenti passerebbero inosservate e funziona con un ampio ecosistema di soluzioni di sicurezza.

Il [Centro sicurezza](https://docs.microsoft.com/azure/security-center/security-center-linux-virtual-machine) consente di proteggere i dati delle macchine virtuali di Azure visualizzando le impostazioni di sicurezza delle VM e monitorando le minacce. Il Centro sicurezza può monitorare nelle macchine virtuali quanto segue:

-   Le regole di configurazione delle impostazioni di sicurezza del sistema operativo (sistema operativo) con hello consigliati
-   Aggiornamenti della sicurezza del sistema e altri aggiornamenti di importanza critica eventualmente mancanti
-   Consigli per la protezione degli endpoint
-   Convalida della crittografia del disco
-   Attacchi basati sulla rete

Centro sicurezza di Azure Usa [controllo di accesso basato sui ruoli (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure), che fornisce [ruoli predefiniti](https://docs.microsoft.com/azure/active-directory/role-based-access-built-in-roles) che può essere assegnato toousers, gruppi e i servizi in Azure.

Centro sicurezza PC valuta configurazione hello di problemi di sicurezza di risorse tooidentify e vulnerabilità. Centro sicurezza PC, visualizzare solo le informazioni correlate tooa risorse quando l'utente viene assegnato hello ruolo di proprietario, collaboratore o lettore per il gruppo hello sottoscrizione o la risorsa a cui appartiene una risorsa.

>[!Note]
>Vedere [autorizzazioni nel Centro protezione Azure](https://docs.microsoft.com/azure/security-center/security-center-permissions) toolearn informazioni sui ruoli e le operazioni consentite in Centro sicurezza PC.

Centro sicurezza PC utilizza Microsoft Monitoring Agent hello: si tratta dello stesso agente usato dal servizio di Operations Management Suite e Log Analitica hello hello. Dati raccolti dall'agente vengono archiviati in entrambi un Analitica Log esistente [dell'area di lavoro](https://docs.microsoft.com/azure/log-analytics/log-analytics-manage-access) associato alla sottoscrizione di Azure o di un nuovo aree di lavoro, tenendo conto hello geolocation di hello macchina virtuale.

## <a name="azure-monitor"></a>Monitoraggio di Azure
I problemi di prestazioni nell'app cloud possono avere un impatto sull'azienda. Con più componenti interconnessi e versioni frequenti, possono verificarsi in qualsiasi momento riduzioni delle prestazioni. Quando si sviluppa un'app, gli utenti in genere individuano problemi non trovati nei test. Si deve sapere immediatamente su questi problemi e di strumenti per la diagnosi e risoluzione dei problemi di hello.

[Monitoraggio di Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-azure-monitor) è lo strumento di base per il monitoraggio dei servizi eseguiti in Azure. Fornisce dati a livello di infrastruttura sulla velocità effettiva di hello di un servizio e hello circostanti ambiente. Se si gestiscono le App in Azure, decidere se tooscale verso l'alto o verso il basso le risorse, quindi il monitoraggio di Azure offre è utilizzare toostart.

Inoltre, è possibile utilizzare Monitoraggio dati toogain approfondite sull'applicazione. Tali informazioni possono consentono di prestazioni dell'applicazione tooimprove o manutenibilità o automatizzare le operazioni che altrimenti richiederebbero un intervento manuale. Sono inclusi:

-   Azure Activity Log
-   Log di diagnostica di Azure
-   Metriche
-   Diagnostica Azure

### <a name="azure-activity-log"></a>Azure Activity Log
È un log che fornisce informazioni approfondite operazioni hello eseguite sulle risorse nella sottoscrizione. Hello [Log attività](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) era noto in precedenza come "Registri di controllo" o "I registri operativi", poiché segnala gli eventi di Pannello di controllo per le sottoscrizioni.

### <a name="azure-diagnostic-logs"></a>Log di diagnostica di Azure
[I log di diagnostica Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) vengono emessi da una risorsa e vengono forniti dati completo e frequenti sull'operazione di hello di tale risorsa. contenuto Hello di questi log varia in base al tipo di risorsa.

Ad esempio, i log del sistema eventi di Windows sono una categoria di log di diagnostica per le macchine virtuali, i BLOB e le tabelle, mentre i log della coda sono categorie di log di diagnostica per gli account di archiviazione.

I log di diagnostica diversi da hello [Log attività (precedentemente noto come registro operativo o di Log di controllo)](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs). log attività Hello fornisce informazioni approfondite operazioni hello eseguite sulle risorse nella sottoscrizione. I log di diagnostica forniscono informazioni approfondite sulle operazioni che la risorsa esegue automaticamente.

### <a name="metrics"></a>Metrica
Monitoraggio di Azure consente tooconsume telemetria toogain visibilità hello prestazioni e l'integrità dei carichi di lavoro in Azure. Hello più importanti dei dati di telemetria di Azure è metriche hello (detto anche i contatori delle prestazioni) generate da Azure più risorse. Monitoraggio di Azure offre diversi modi tooconfigure e utilizzare tali [metriche](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-metrics) per il monitoraggio e risoluzione dei problemi.

### <a name="azure-diagnostics"></a>Diagnostica Azure
È una funzionalità di hello all'interno di Azure che consente la raccolta hello dei dati di diagnostica in un'applicazione distribuita. È possibile utilizzare l'estensione diagnostica hello da varie origini diverse. Sono attualmente supportati [ruoli Web e di lavoro del servizio cloud di Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service), [macchine virtuali di Azure](https://docs.microsoft.com/azure/vs-azure-tools-configure-roles-for-cloud-service) che eseguono Microsoft Windows e [Service Fabric](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics).


## <a name="network-watcher"></a>Network Watcher
Per creare una rete end-to-end in Azure è possibile orchestrare e comporre varie risorse di rete individuali, quali rete virtuale, ExpressRoute, gateway applicazione, servizi di bilanciamento del carico e altro ancora. Il monitoraggio è disponibile in ogni hello risorse di rete.

rete di Hello end tooend può avere configurazioni complesse e le interazioni tra le risorse, creazione di scenari complessi che richiedono basata sullo scenario di monitoraggio tramite Watcher di rete.

[Network Watcher](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) semplificherà il monitoraggio e la diagnosi della rete di Azure. Gli strumenti di diagnostica e di visualizzazione disponibili con enable Watcher di rete è tootake remoto acquisizioni di pacchetti in una macchina virtuale di Azure ottenere informazioni dettagliate sull'utilizzo dei registri di flusso del traffico di rete e diagnosticare Gateway VPN e connessioni.

Watcher di rete presenta attualmente hello seguenti funzionalità:

- [Topologia](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -fornisce un hello con visualizzazione a livello di rete diversi interconnessioni e le associazioni tra le risorse di rete in un gruppo di risorse.
-   [Acquisizione pacchetti variabile](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview): acquisisce i dati dei pacchetti all'interno e all'esterno di una macchina virtuale. Filtri di opzioni e ottimizzare i controlli, ad esempio si trova ora in grado di tooset avanzati e versatilità di fornire i limiti delle dimensioni. Hello pacchetto possono essere archiviati in un archivio blob o su disco locale di hello in formato CAP.
-   [Verifica dei flussi IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview): controlla se un pacchetto viene accettato o rifiutato in base ai parametri di pacchetto costituiti da informazioni a 5 tuple sul flusso, ovvero l'indirizzo IP di destinazione, l'indirizzo IP di origine, la porta di destinazione, la porta di origine e il protocollo. Se i pacchetti hello viene negato da un gruppo di sicurezza, hello regola e gruppo di pacchetti hello negato.
-   [Hop successivo](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -determina hello hop successivo per i pacchetti hello infrastruttura di rete di Azure, consentendo di route definite dall'utente non è configurato correttamente qualsiasi toodiagnose indirizzato.
-   [Visualizzazione del gruppo di sicurezza](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -Ottiene le regole di sicurezza efficace e applicato hello che vengono applicate in una macchina virtuale.
-   [Flusso di NSG registrazione](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) -flusso di log per i gruppi di sicurezza di rete consentono di toocapture registri tootraffic correlati che vengono concesse o negate le regole di sicurezza hello gruppo hello. flusso di Hello è definito dalle informazioni tupla con 5: indirizzo IP di origine, IP di destinazione, porta di origine, destinazione porta e protocollo.
-   [Gateway di rete virtuale e la risoluzione dei problemi di connessione](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -fornisce hello possibilità tootroubleshoot gateway di rete virtuale e le connessioni.
-   [Limiti della sottoscrizione di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) -consente l'utilizzo delle risorse di rete tooview rispetto ai limiti.
-   [Configurazione del Log di diagnostica](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview) : fornisce un unico riquadro tooenable o disabilitare i log di diagnostica per le risorse di rete in un gruppo di risorse.

toolearn più watcher di rete tooconfigure vedere, [configurare watcher di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-create).

## <a name="developer-operations-devops"></a>Developer Operations (DevOps)
Sviluppo di applicazioni tooDevOps precedente, i team sono stati responsabile della raccolta di requisiti di business per un programma software e la scrittura di codice. Un team QA separato verifica quindi il programma hello in un ambiente di sviluppo isolato, se sono stati soddisfatti i requisiti e le versioni hello codice per operazioni toodeploy. i team di distribuzione Hello vengono ulteriormente frammentati in gruppi silo come rete e di database. Ogni volta che un programma software "generato su parete hello" team indipendenti di tooan aggiunge i colli di bottiglia.

[DevOps](https://www.visualstudio.com/learn/what-is-devops/) consente ai team toodeliver soluzioni più sicure, la qualità più rapida ed economiche. I clienti si aspettano un'esperienza affidabile e dinamica quando usano software e servizi.  I team devono scorrere rapidamente gli aggiornamenti software, misurato hello impatto degli aggiornamenti di hello e rispondere rapidamente con nuovi problemi tooaddress iterazioni di sviluppo o fornire maggior valore.  Piattaforme cloud come Microsoft Azure hanno rimosso i colli di bottiglia tradizionali e hanno contribuito a rendere agevole l'infrastruttura. Software di interfaccia in ogni azienda come hello fattore di differenziazione e fattore dei risultati delle operazioni aziendali. Nessuna organizzazione, developer o lavoro IT può o evitare lo spostamento di hello DevOps.

Esperti DevOps maturi adottano numerosi hello ottimali. Queste procedure [coinvolgere persone](https://www.visualstudio.com/learn/what-is-devops-culture/) tooform strategie in base a scenari aziendali hello.  Gli strumenti consentono di automatizzare hello varie procedure consigliate:

-   [Gestione di progetto e di pianificazione Agile](https://www.visualstudio.com/learn/what-is-agile/) tecniche sono utilizzati tooplan e isolare il lavoro in sprint, la capacità del team di gestire e consentono ai team di adattarsi rapidamente alle esigenze aziendali toochanging.
-   [Controllo della versione, in genere con Git](https://www.visualstudio.com/learn/what-is-git/), consente ai team che si trovano ovunque nell'origine di hello world tooshare e l'integrazione con software development tools tooautomate hello pipeline di tipo versione.
-   [Integrazione continua](https://www.visualstudio.com/learn/what-is-continuous-integration/) unità hello in corso l'unione e il test di codice, con un conseguente toofinding difetti in anticipo.  Altri vantaggi includono meno tempo impiegato per contrastare problemi di unione e feedback veloci per i team di sviluppo.
-   [Il recapito continuo](https://www.visualstudio.com/learn/what-is-continuous-delivery/) di soluzioni software tooproduction e ambienti di test consentono alle organizzazioni di correggere i bug e modifica tooever business di rispondere rapidamente requisiti.
-   Il [Monitoraggio](https://www.visualstudio.com/learn/what-is-monitoring/) delle applicazioni in esecuzione, inclusi gli ambienti di produzione per l'integrità dell'applicazione, così come l'uso da parte dell'utente, aiutano le organizzazioni a formulare un'ipotesi e a convalidare rapidamente o disapprovare le strategie.  I dati completi acquisiti e archiviati in vari formati di registrazione.
-   [Infrastruttura come codice (IaC)](https://www.visualstudio.com/learn/what-is-infrastructure-as-code/) è una procedura consigliata, che consente l'automazione hello e convalida della creazione e disinstallazione delle reti e macchine virtuali toohelp con distribuzione sicura e stabile applicazione piattaforme di hosting.
-   [Microservizi](https://www.visualstudio.com/learn/what-are-microservices/) architettura è tooisolate sfruttate casi di utilizzo di business in piccoli servizi riutilizzabili.  Questa architettura consente l'efficienza e scalabilità.

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni su sicurezza OMS e la soluzione di controllo, vedere hello seguenti articoli:

- [Operations Management Suite | Sicurezza e Conformità](https://www.microsoft.com/cloud-platform/security-and-compliance).
- [Monitoraggio e risposta tooSecurity gli avvisi in Operations Management Suite di protezione e controllo soluzione](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-responding-alerts).
- [Monitoraggio delle risorse nella soluzione Operations Management Suite per la sicurezza e il controllo](https://docs.microsoft.com/en-us/azure/operations-management-suite/oms-security-monitoring-resources).
