---
title: aaaAzure di registrazione e controllo | Documenti Microsoft
description: Informazioni sull'utilizzo di approfondite di registrazione dati toogain sull'applicazione.
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
ms.openlocfilehash: d0e817b071962ad9bef6250267092b5f9282bc7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-logging-and-auditing"></a>Registrazione e controllo di Azure
## <a name="introduction"></a>Introduzione
### <a name="overview"></a>Panoramica
tooassist e potenziali Azure i clienti comprendere e usare hello disponibile in varie funzionalità correlate alla sicurezza e che circonda hello piattaforma Azure, Microsoft ha sviluppato una serie di white paper, una panoramica di sicurezza, le procedure consigliate, e gli elenchi di controllo. intervallo di argomenti in termini di dimensioni e della complessità Hello e vengono aggiornate periodicamente. Questo documento fa parte della serie, come riepilogato nella seguente sezione astratta hello.
### <a name="azure-platform"></a>Piattaforma Azure
Azure è una piattaforma cloud aperta e flessibile del servizio che supporta hello selezione più ampia di sistemi operativi, linguaggi di programmazione, Framework, strumenti, i database e i dispositivi.

Ad esempio, è possibile:
-   Eseguire i contenitori Linux con l'integrazione Docker.

-   Compilare le app con JavaScript, Python, .NET, PHP, Java e Node.js.

-   Compilare i back-end per dispositivi iOS, Android e Windows.

Servizi cloud pubblico di Azure supportano hello stesse tecnologie milioni di sviluppatori e professionisti IT si basano su già e attendibile.

Quando si compila, o eseguire la migrazione di risorse IT a, un provider di cloud, ci si basa sul tooprotect capacità dell'organizzazione che le applicazioni e dati con controlli hello e servizi di hello assicurano toomanage hello delle risorse basati su cloud.

Infrastruttura di Azure è progettato da hello tooapplications di funzionalità per l'hosting contemporaneamente milioni di clienti e fornisce una base attendibile in cui le aziende grado di soddisfare le esigenze di sicurezza. Inoltre, Azure offre un'ampia gamma di toocontrol possibilità hello e opzioni di protezione configurabili loro in modo che sia possibile personalizzare sicurezza toomeet hello requisiti delle distribuzioni. Grazie a questo documento è possibile soddisfare tali requisiti.

### <a name="abstract"></a>Sunto
Il controllo e la registrazione di eventi relativi alla sicurezza e di avvisi correlati, sono componenti importanti di una strategia di protezione dei dati efficace. Registri di protezione e i report offrono un record di attività sospette e la Guida è rilevare modelli che possono indicare l'esito positivo o tentativi penetrazione esterno della rete di hello, nonché gli attacchi interni elettronico. È possibile utilizzare l'attività degli utenti toomonitor controllo, conformità alle normative di documento, eseguire analisi forensi e altro ancora. Tramite gli avvisi si ottiene la notifica immediata quando si verificano eventi che riguardano la sicurezza.

Prodotti e servizi di Microsoft Azure offrono il controllo della sicurezza configurabile e registrazione toohelp opzioni identificare i gap nei criteri di sicurezza e meccanismi e risolvere tali toohelp gap impedire violazioni della sicurezza. I servizi Microsoft offrono alcune (e in alcuni casi, tutte) di hello le opzioni seguenti: centralizzato di monitoraggio, registrazione e analisi sistemi tooprovide continua visibilità; avvisi tempestivi; e toohelp i report gestiti hello numerose informazioni generate da dispositivi e servizi.

Dati del log di Microsoft Azure possono essere esportato tooSecurity sistemi di gestione di eventi (SIEM) ed eventi imprevisti per l'analisi e si integrano con soluzioni di controllo di terze parti.

Questo white paper offre un'introduzione alle operazioni di creazione, raccolta e analisi dei log di sicurezza dai servizi ospitati in Azure, oltre ad aiutare i clienti a ottenere informazioni più approfondite sulla sicurezza nelle proprie distribuzioni di Azure. ambito Hello di questo white paper è limitato tooapplications e servizi compilato e distribuito in Azure.

> [!Note]
> Alcune indicazioni contenute in questo documento possono comportare un maggior consumo delle risorse di calcolo, di rete o dei dati, con un aumento dei costi di licenza o sottoscrizione.

## <a name="types-of-logs-in-azure"></a>Tipi di log in Azure
Le applicazioni cloud sono complesse e hanno molte parti mobili. I file registro tooensure dati che l'applicazione resta alto e in esecuzione in uno stato integro. Consente inoltre toostave è impostata su off problemi potenziali o risolvere i problemi oltre quelle. Inoltre, è possibile utilizzare approfondite di registrazione dati toogain sull'applicazione. Tali informazioni possono consentono di prestazioni dell'applicazione tooimprove o manutenibilità o automatizzare le operazioni che altrimenti richiederebbero un intervento manuale.

Azure produce registrazioni complete per ogni servizio di Azure. I log sono classificati nei seguenti tipi principali:
-   **I registri di controllo/gestione** ottenere visibilità in hello operazioni di gestione risorse di Azure CREATE, UPDATE e DELETE. [I log attività di Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs) sono un esempio di questo tipo di log.

-   **Dati piano registri** ottenere visibilità in eventi hello generato nell'ambito di utilizzo di hello di una risorsa di Azure. Esempi di questo tipo di log sono eventi di Windows del sistema, sicurezza, hello e log applicazioni in una macchina virtuale e hello [log di diagnostica](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs) configurato tramite Monitor di Azure


-   **Eventi elaborati**, che offrono informazioni sugli eventi o avvisi analizzati dopo essere stati elaborati per conto dell'utente. Esempi di questo tipo sono i brevi [avvisi emessi dal Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-managing-and-responding-alerts) dopo aver eseguito l'[elaborazione e l'analisi della sottoscrizione](https://docs.microsoft.com/azure/security-center/security-center-intro).

la tabella seguente Hello più importante tipo di elenco di registri disponibili in Azure.

| Categoria di log | Tipo di log | Usi | Integrazione |
| ------------ | -------- | ------ | ----------- |
|[Log attività](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|Gli eventi del piano di controllo sulle risorse di Azure Resource Manager| Forniscono informazioni sulle operazioni hello eseguite sulle risorse nella sottoscrizione.|   API REST e [Monitoraggio di Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)|
|[Log di diagnostica di Azure](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|frequenti dei dati sull'operazione di hello delle risorse di gestione risorse di Azure nella sottoscrizione| Offrono informazioni approfondite sulle operazioni eseguite dalla risorsa stessa| Monitoraggio di Azure, [Stream](https://docs.microsoft.com/en-us/azure/monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs)|
|[Creazione di report in AAD](https://docs.microsoft.com/en-us/azure/active-directory/active-directory-reporting-azure-portal)|Log e report|Attività di accesso dell'utente e informazioni sulle attività di sistema riguardo alla gestione di utenti e gruppi|[API Graph](https://docs.microsoft.com/en-us/azure/active-directory/develop/active-directory-graph-api-quickstart)|
|[Macchine virtuali e servizi cloud](https://docs.microsoft.com/en-us/azure/cloud-services/cloud-services-dotnet-diagnostics-storage)|Log eventi di Windows e Syslog Linux|  Acquisisce i dati di sistema e i dati di registrazione nelle macchine virtuali hello e trasferisce i dati in un account di archiviazione di propria scelta.| Windows tramite [WAD](https://docs.microsoft.com/en-us/azure/azure-diagnostics) (archiviazione di diagnostica di Windows Azure) e Linux in Monitoraggio di Azure|
|[Analisi dell'archiviazione](https://docs.microsoft.com/en-us/rest/api/storageservices/fileservices/storage-analytics)|Esegue la registrazione di archiviazione e offre i dati delle metriche per un account di archiviazione.|Offre informazioni approfondite per tenere traccia delle richieste, analizzare le tendenze d'uso e diagnosticare i problemi relativi al proprio account di archiviazione.|  API REST o hello [libreria client](https://msdn.microsoft.com/en-us/library/azure/mt347887.aspx)|
|[Log dei flussi del gruppo di sicurezza di rete (NSG)](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-nsg-flow-logging-overview)|Formato JSON e mostra i flussi in ingresso e in uscita in base a ciascuna regola|Visualizzare le informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete|[Network Watcher](https://docs.microsoft.com/en-us/azure/network-watcher/network-watcher-monitoring-overview)|
|[Application Insights](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-overview)|Log, eccezioni e diagnostica personalizzata|  Servizio APM di gestione delle prestazioni delle applicazioni per sviluppatori Web su più piattaforme.| API REST, [Power BI](https://powerbi.microsoft.com/en-us/documentation/powerbi-azure-and-power-bi/)|
|Dati di elaborazione/avvisi di sicurezza| Avviso del Centro sicurezza di Azure, avviso OMS| Informazioni e avvisi sulla sicurezza.|   API REST, JSON|

### <a name="activity-log"></a>Log attività
Hello [Log attività Azure](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs), fornisce informazioni approfondite operazioni hello eseguite sulle risorse nella sottoscrizione. Hello Log attività è stata precedentemente noto come "Registri di controllo" o "I registri operativi", poiché fornisce [Pannello di controllo eventi](https://driftboatdave.com/2016/10/13/azure-auditing-options-for-your-custom-reporting-needs/) per le sottoscrizioni. Hello registro attività, consentono di determinare hello "cosa, chi e quando" per le operazioni (PUT, POST, DELETE) eseguite su risorse hello nella sottoscrizione di scrittura. È anche possibile comprendere lo stato di hello dell'operazione di hello e altre proprietà pertinenti. Log attività Hello non include le operazioni di lettura (GET).

Qui PUT, POST, DELETE si riferisce a operazioni di scrittura hello tooall log attività contiene risorse hello. Ad esempio, è possibile utilizzare hello attività registri toofind un errore durante la risoluzione dei problemi o toomonitor come un utente nell'organizzazione di modifica una risorsa.

![Log attività](./media/azure-log-audit/azure-log-audit-fig1.png)


È possibile recuperare gli eventi dal Log attività tramite il portale di Azure, hello [CLI](https://docs.microsoft.com/azure/storage/storage-azure-cli), i cmdlet di PowerShell e [API REST di Azure monitoraggio](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-rest-api-walkthrough). Il periodo di conservazione dei dati per i log attività è di 19 giorni.

Scenari di integrazione
-   [Creare un avviso di posta elettronica o webhook che attiva un evento del log attività.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/insights-auditlog-to-webhook-email)

-   [Flusso di Hub eventi tooan](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-activity-logs-event-hubs) per l'inserimento di un servizio di terze parti o di una soluzione analitica personalizzato, ad esempio Power BI.

-   Analizzare in Power BI usando hello [pacchetto di contenuto Power BI.](https://powerbi.microsoft.com/documentation/powerbi-content-pack-azure-audit-logs/)

-   [Salvare il file tooa Account di archiviazione per l'ispezione dell'archivio o manuale.](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-activity-log) È possibile specificare hello memorizzazione ora (in giorni) usando i profili di Log.

-   Eseguire una query e visualizzarlo nel portale di Azure hello.

-   Eseguire query tramite l'API REST, i cmdlet di PowerShell o l'interfaccia della riga di comando.

-   Esportare hello Log attività con i profili di Log troppo[log Analitica](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview).

È possibile utilizzare un account di archiviazione o [spazio dei nomi di hub eventi](https://docs.microsoft.com/azure/event-hubs/event-hubs-resource-manager-namespace-event-hub-enable-archive) che non si trova in hello stessa sottoscrizione come hello un log di creazione. utente di Hello che configura l'impostazione di hello deve avere hello appropriato [RBAC](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) tooboth sottoscrizioni
### <a name="azure-diagnostic-logs"></a>Log di diagnostica di Azure
I log di diagnostica Azure vengono creati da una risorsa che forniscono dati completo e frequenti sull'operazione di hello di tale risorsa. contenuto Hello di questi log varia in base al tipo di risorsa (ad esempio, [log eventi del sistema Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events)sono una categoria di Log di diagnostica per le macchine virtuali e [blob, tabella e coda registri](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) sono le categorie di log di diagnostica per gli account di archiviazione) e diversi da hello registro attività, che fornisce informazioni approfondite operazioni hello eseguite sulle risorse nella sottoscrizione.

![Log di diagnostica di Azure](./media/azure-log-audit/azure-log-audit-fig2.png)

I log di diagnostica di Azure offrono più opzioni di configurazione, vale a dire che il portale di Azure può usare l'API REST, PowerShell e l'interfaccia della riga di comando (CLI).

**Scenari di integrazione**
-   Salvarli tooa [Account di archiviazione](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-archive-diagnostic-logs) per un controllo di controllo o manuale. È possibile specificare hello memorizzazione ora (in giorni) utilizzando le impostazioni di diagnostica hello.

-   [Flusso di hub tooEvent](https://docs.microsoft.com/azure/monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs) per l'inserimento di un servizio di terze parti o di una soluzione analitica personalizzato, ad esempio [Power BI.](https://powerbi.microsoft.com/documentation/powerbi-azure-and-power-bi/)

-   Analizzarli con [OMS Log Analytics](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)

**Servizi supportati, schema per i log di diagnostica e categorie di log supportati per ogni tipo di risorsa**


| Servizio | Schema e documenti | Tipo di risorsa | Categoria |
| ------- | ------------- | ------------- | -------- |
|Bilanciamento del carico| [Analisi dei log per il servizio di bilanciamento del carico di Azure (anteprima)](https://docs.microsoft.com/en-us/azure/load-balancer/load-balancer-monitor-log)|Microsoft.Network/loadBalancers|  LoadBalancerAlertEvent|
|||Microsoft.Network/loadBalancers| LoadBalancerProbeHealthStatus
|Gruppi di sicurezza di rete|[Analisi dei log per i gruppi di sicurezza di rete](https://docs.microsoft.com/en-us/azure/virtual-network/virtual-network-nsg-manage-log)|Microsoft.Network/networksecuritygroups|NetworkSecurityGroupEvent|
|||Microsoft.Network/networksecuritygroups|NetworkSecurityGroupRuleCounter|
|Gateway applicazione|[Registrazione diagnostica per il gateway applicazione](https://docs.microsoft.com/en-us/azure/application-gateway/application-gateway-diagnostics)|Microsoft.Network/applicationGateways|ApplicationGatewayAccessLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayPerformanceLog|
|||Microsoft.Network/applicationGateways|ApplicationGatewayFirewallLog|
|Insieme di credenziali di chiave|[Registrazione dell'insieme di credenziali delle chiavi di Azure](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-logging)|Microsoft.KeyVault/vaults|AuditEvent|
|Ricerca di Azure|[Abilitazione e uso di Analisi del traffico di ricerca](https://docs.microsoft.com/en-us/azure/search/search-traffic-analytics)|Microsoft.Search/searchServices|OperationLogs|
|Archivio Data Lake|[Accesso ai log di diagnostica per Archivio Data Lake di Azure](https://docs.microsoft.com/en-us/azure/data-lake-store/data-lake-store-diagnostic-logs)|Microsoft.DataLakeStore/accounts|Audit|
|Analisi Data Lake|[Accesso ai log di diagnostica per Azure Data Lake Analytics](https://docs.microsoft.com/en-us/azure/data-lake-analytics/data-lake-analytics-diagnostic-logs)|Microsoft.DataLakeAnalytics/accounts|Audit|
|||Microsoft.DataLakeAnalytics/accounts|Richieste|
|||Microsoft.DataLakeStore/accounts|Richieste|
|App per la logica|[Schema di rilevamento personalizzato per le app per la logica B2B](https://docs.microsoft.com/en-us/azure/logic-apps/logic-apps-track-integration-account-custom-tracking-schema)|Microsoft.Logic/workflows|WorkflowRuntime|
|||Microsoft.Logic/integrationAccounts|IntegrationAccountTrackingEvents|
|Azure Batch|[Registrazione diagnostica di Azure Batch](https://docs.microsoft.com/en-us/azure/batch/batch-diagnostics)|Microsoft.Batch/batchAccounts|ServiceLog|
|Automazione di Azure|[Analisi dei log per Automazione di Azure](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|Microsoft.Automation/automationAccounts|JobLogs|
|||Microsoft.Automation/automationAccounts|JobStreams|
|Hub eventi|[Log di diagnostica di Hub eventi in Azure](https://docs.microsoft.com/en-us/azure/event-hubs/event-hubs-diagnostic-logs)|Microsoft.EventHub/namespaces|ArchiveLogs|
|||Microsoft.EventHub/namespaces|OperationalLogs|
|Analisi di flusso|[Log di diagnostica dei processi](https://docs.microsoft.com/en-us/azure/stream-analytics/stream-analytics-job-diagnostic-logs)|Microsoft.StreamAnalytics/streamingjobs|Esecuzione|
|||Microsoft.StreamAnalytics/streamingjobs|Creazione|
|Bus di servizio|[Log di diagnostica del bus di servizio di Azure](https://docs.microsoft.com/en-us/azure/service-bus-messaging/service-bus-diagnostic-logs)|Microsoft.ServiceBus/namespaces|OperationalLogs|

### <a name="azure-active-directory-reporting"></a>Creazione di report in Azure Active Directory
Azure Active Directory (Azure AD) include la sicurezza, l’attività e i report di controllo per la directory. Hello [Report di controllo di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-guide) consentono ai clienti con privilegiata tooidentify azioni che si sono verificati in Azure Active Directory. Le azioni con privilegi includono modifiche elevazione (ad esempio, creazione del ruolo o la reimpostazione della password), modificare le configurazioni di criteri (ad esempio criteri password) o configurazione toodirectory modifiche (ad esempio, le modifiche toodomain impostazioni di federazione).

report di Hello forniscono record di controllo hello per nome dell'evento hello, attore hello che ha eseguito l'azione di hello, risorse di destinazione hello interessata dalla modifica hello e hello data e ora (UTC). I clienti sono elenco hello tooretrieve in grado di eventi di controllo per Azure Active Directory tramite hello [portale di Azure](https://portal.azure.com/), come descritto in [consente di visualizzare il log di controllo](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-azure-portal). Di seguito è riportato un elenco di report hello inclusi:

| Report sulla sicurezza | Report sull’attività | Report di controllo |
| :--------------- | :--------------- | :------------ |
|Accessi da origini sconosciute| Utilizzo dell'applicazione: riepilogo| Report di controllo della Directory|
|Accessi dopo più errori|  Utilizzo dell'applicazione: dettagliato||
|Accessi da più aree geografiche|    Dashboard dell'applicazione||
|Accessi da indirizzi IP con attività sospette|   Errori di provisioning dell'account||
|Attività di accesso irregolare|    Dispositivi dell’utente singolo||
|Accessi da dispositivi potenzialmente infetti|   Attività dell’utente singolo||
|Utenti con anomalie dell'attività di accesso| Report attività dei gruppi||
||Report attività di registrazione per la reimpostazione password||
||Attività di reimpostazione password|||

dati di Hello di questi report possono essere applicazioni tooyour utile, ad esempio i sistemi SIEM, controllo e strumenti di business intelligence. Hello Azure AD reporting che API forniscono dati toohello accesso a livello di codice tramite un set di API basata su REST. È possibile chiamare queste [API](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-api-getting-started) da numerosi strumenti e linguaggi di programmazione.

Gli eventi in hello report di controllo di Azure AD vengono mantenuti per 180 giorni.

> [!Note]
> Per altre informazioni sulla conservazione dei report, vedere la pagina [Criteri di conservazione dei report di Azure Active Directory](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-retention).

Per i clienti che desiderano archiviare gli eventi di controllo per lunghi periodi di conservazione, hello Reporting API può essere utilizzato pull tooregularly [eventi di controllo](https://docs.microsoft.com/azure/active-directory/active-directory-reporting-audit-events) in un archivio dati separato.

### <a name="virtual-machine-logs-using-azure-diagnostics"></a>i log delle macchine virtuali con Diagnostica di Azure
[Diagnostica di Azure](https://docs.microsoft.com/azure/azure-diagnostics) hello funzionalità all'interno di Azure che consente la raccolta hello dei dati di diagnostica in un'applicazione distribuita. È possibile utilizzare l'estensione diagnostica hello da diverse origini. Sono attualmente supportati i [ruoli di lavoro e Web del servizio cloud di Azure](https://docs.microsoft.com/azure/cloud-services/cloud-services-choose-me) e

![i log delle macchine virtuali con Diagnostica di Azure](./media/azure-log-audit/azure-log-audit-fig3.png)

[Macchine virtuali di Azure](https://azure.microsoft.com/documentation/learning-paths/virtual-machines/) che eseguono Microsoft Windows e [Service Fabric](https://docs.microsoft.com/azure/service-fabric/service-fabric-overview).

È possibile abilitare la funzionalità Diagnostica di Azure in una macchina virtuale nei modi seguenti:

-   Utilizzo di Visual Studio, vedere [tootrace usare Visual Studio macchine virtuali di Azure](https://docs.microsoft.com/azure/vs-azure-tools-debug-cloud-services-virtual-machines)

-   [Configurare Diagnostica di Azure in una macchina virtuale Azure da remoto](https://docs.microsoft.com/azure/virtual-machines-dotnet-diagnostics)

-   [Utilizzare PowerShell tooset di diagnostica nelle macchine virtuali di Azure](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-ps-extensions-diagnostics?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

-   [Creare una macchina virtuale Windows con monitoraggio e diagnostica con un modello di Azure Resource Manager](https://docs.microsoft.com/azure/virtual-machines/virtual-machines-windows-extensions-diagnostics-template?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)

### <a name="storage-analytics"></a>di Analisi archiviazione
L'[Analisi archiviazione di Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics) esegue la registrazione e restituisce i dati delle metriche per un account di archiviazione. È possibile usare questo richieste tootrace dati, analizzare le tendenze di utilizzo e diagnosticare i problemi con l'account di archiviazione. La registrazione Analitica di archiviazione è disponibile per hello [servizi Blob, coda e tabella.](https://docs.microsoft.com/azure/storage/storage-introduction) Archiviazione Analitica registra informazioni dettagliate sul servizio di archiviazione tooa richieste riuscite e non riuscite.

Queste informazioni possono essere utilizzati toomonitor singole richieste e toodiagnose problemi con un servizio di archiviazione. Le richieste vengono registrate in base al massimo sforzo. Le voci di log vengono create solo se esistono richieste effettuate per l'endpoint del servizio hello. Ad esempio, se un account di archiviazione dispone di attività nel relativo endpoint Blob ma non nel relativo endpoint accodamento o tabelle, solo registra riguardano toohello servizio Blob viene creato.

toouse Analitica di archiviazione, è necessario abilitarla singolarmente per ogni servizio desiderato toomonitor. È possibile abilitarla in hello [portale di Azure](https://portal.azure.com/); per informazioni dettagliate, vedere [monitorare un account di archiviazione nel portale di Azure hello.](https://docs.microsoft.com/azure/storage/storage-monitor-storage-account) È anche possibile abilitare Analitica di archiviazione a livello di programmazione tramite hello API REST o libreria client hello. Utilizzare hello Set Service Properties operazione tooenable archiviazione Analitica singolarmente per ogni servizio.

dati aggregati Hello viene archiviati in un noto blob (per la registrazione) e in tabelle note (per la metrica), che sono accessibili tramite il servizio Blob di hello e API del servizio tabelle.

Archiviazione Analitica pone un limite di 20 TB sulla quantità hello di dati archiviati che sia indipendenti dal limite totale di hello dell'account di archiviazione. Tutti i log vengono archiviati in [BLOB in blocchi](https://docs.microsoft.com/azure/storage/storage-analytics) all'interno di un contenitore denominato $logs, che viene creato automaticamente quando viene abilitata l'Analisi archiviazione per un account di archiviazione.

> [!Note]
> Per altre informazioni sulla fatturazione e sui criteri di conservazione dei dati, vedere [Analisi archiviazione e fatturazione](https://docs.microsoft.com/rest/api/storageservices/fileservices/storage-analytics-and-billing).
>
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

### <a name="azure-networking-logs"></a>Log di rete di Azure
Il monitoraggio e la registrazione di rete in Azure comprende due categorie generali:

-   [Controllo di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-watcher) -monitoraggio di rete basata su Scenario viene fornito con funzionalità di hello Watcher di rete. Il servizio include l'acquisizione pacchetti, l'hop successivo, la verifica del flusso IP, la visualizzazione dei gruppi di sicurezza e i registri dei flussi dei gruppi di sicurezza di rete. Monitoraggio a livello di scenario è inclusa una visualizzazione di tooend finale delle risorse di rete in Monitoraggio risorse di rete di contrasto tooindividual.

-   [Monitoraggio delle risorse](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-resource-level-monitoring): il monitoraggio a livello di risorsa include funzionalità di log di diagnostica, metriche, risoluzione dei problemi e integrità delle risorse. Tutte queste funzionalità vengono compilate a livello di risorse di rete hello.

![Log di rete di Azure](./media/azure-log-audit/azure-log-audit-fig4.png)

Watcher di rete è un servizio internazionale che consente di toomonitor e diagnosticare le condizioni di livello rete scenario, a e da Azure. Diagnostica di rete e gli strumenti di visualizzazione disponibili con Watcher di rete consentono di comprendere, diagnosticare e ottenere rete tooyour insights in Azure.

**Flusso di NSG registrazione** -flusso di log per i gruppi di sicurezza di rete consentono di toocapture registri tootraffic correlati che vengono concesse o negate le regole di sicurezza hello gruppo hello. Questi registri di flusso sono scritti in formato JSON e mostrano in uscita e i flussi in ingresso per ogni regola, hello flusso hello NIC applicato, 5 tuple informazioni sul flusso hello (origine/destinazione IP, porta di origine/destinazione, Protocol) e se hello traffico è stato consentito o negato.

### <a name="network-security-group-flow-logging"></a>Registrazione dei flussi del gruppo di sicurezza di rete

[I registri del flusso di gruppo di sicurezza di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-nsg-flow-logging-overview) sono una funzionalità del controllo di rete che consente di tooview informazioni sul traffico IP in entrata e in uscita tramite un gruppo di sicurezza di rete. Questi registri di flusso sono scritti in formato JSON e mostrano in uscita e i flussi in ingresso per ogni regola, hello flusso hello NIC applicato, 5 tuple informazioni sul flusso hello (origine/destinazione IP, porta di origine/destinazione, Protocol) e se hello traffico è stato consentito o negato.

Mentre il flusso di log di gruppi di sicurezza di rete di destinazione, non vengono visualizzati hello stesso come hello altri log. I log dei flussi vengono archiviati solo all'interno di un account di archiviazione.

Hello stesso log tooflow di applicare i criteri di conservazione in altri log. Registri di disporre di criteri di conservazione che possono essere impostato da giorni too365 1 giorno. Se non è impostato un criterio di conservazione, hello registri vengono mantenuti sempre.

**Log di diagnostica**

Eventi periodici e spontanei vengono creati dalle risorse di rete e registrati negli account di archiviazione, inviate tooan Hub eventi o Analitica di Log. Questi log forniscono informazioni dettagliate sui integrità hello di una risorsa. e possono essere visualizzati con strumenti quali Power BI e Log Analytics. come i log di diagnostica tooview, visitare toolearn [Analitica di Log.](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-networking-analytics)

![Log di diagnostica](./media/azure-log-audit/azure-log-audit-fig5.png)

Sono disponibili log di diagnostica per il [servizio di bilanciamento del carico](https://docs.microsoft.com/azure/load-balancer/load-balancer-monitor-log), i [gruppi di sicurezza di rete](https://docs.microsoft.com/azure/virtual-network/virtual-network-nsg-manage-log), le route e il [gateway applicazione](https://docs.microsoft.com/azure/application-gateway/application-gateway-diagnostics).

Network Watcher offre una visualizzazione dei log di diagnostica contenente tutte le risorse di rete che supportano la registrazione diagnostica. Da questa visualizzazione è possibile abilitare e disabilitare le risorse di rete in modo facile e veloce.


Le funzionalità di registrazione toopreceding addizione, Watcher di rete presenta attualmente hello seguenti funzionalità:
- [Topologia](https://docs.microsoft.com/azure/network-watcher/network-watcher-topology-overview) -fornisce un hello con visualizzazione a livello di rete diversi interconnessioni e le associazioni tra le risorse di rete in un gruppo di risorse.

- [Acquisizione pacchetti variabile](https://docs.microsoft.com/azure/network-watcher/network-watcher-packet-capture-overview): acquisisce i dati dei pacchetti all'interno e all'esterno di una macchina virtuale. Gestione avanzata delle opzioni di filtro e ottimizzare i controlli, ad esempio si trova in grado di tooset limitazioni di dimensione e tempo forniscono versatility.hello pacchetto possono essere archiviati in un archivio blob o su disco locale di hello in formato CAP.

-   [Verifica flusso IP](https://docs.microsoft.com/azure/network-watcher/network-watcher-ip-flow-verify-overview): verifica se un pacchetto viene accettato o rifiutato in base ai relativi parametri sul flusso di informazioni, costituiti da informazioni a 5 tuple, ovvero l'indirizzo IP di destinazione, l'indirizzo IP di origine, la porta di destinazione, la porta di origine e il protocollo. Se i pacchetti hello viene negato da un gruppo di sicurezza, hello regola e gruppo di pacchetti hello negato.

-   [Hop successivo](https://docs.microsoft.com/azure/network-watcher/network-watcher-next-hop-overview) -determina hello hop successivo per i pacchetti hello infrastruttura di rete di Azure, consentendo di route definite dall'utente non è configurato correttamente qualsiasi toodiagnose indirizzato.

-   [Visualizzazione del gruppo di sicurezza](https://docs.microsoft.com/azure/network-watcher/network-watcher-security-group-view-overview) -Ottiene le regole di sicurezza efficace e applicato hello che vengono applicate in una macchina virtuale.

-   [Gateway di rete virtuale e la risoluzione dei problemi di connessione](https://docs.microsoft.com/azure/network-watcher/network-watcher-troubleshoot-manage-rest) -fornisce hello possibilità tootroubleshoot gateway di rete virtuale e le connessioni.

-   [Limiti della sottoscrizione di rete](https://docs.microsoft.com/azure/network-watcher/network-watcher-monitoring-overview#network-subscription-limits) -consente l'utilizzo delle risorse di rete tooview rispetto ai limiti.

### <a name="application-insight"></a>Application Insights

[Application Insights](https://docs.microsoft.com/azure/application-insights/app-insights-overview) è un servizio estendibile di gestione delle prestazioni delle applicazioni per sviluppatori Web su più piattaforme, Utilizzarlo toomonitor l'applicazione web in tempo reale. Il servizio rileva automaticamente le anomalie nelle prestazioni Include toohelp di analitica potenti strumenti per la diagnosi di problemi e toounderstand gli utenti che effettivamente svolgono con l'app.

 È progettato toohelp è migliorare continuamente le prestazioni e usabilità.

 Funziona per le app su una vasta gamma di piattaforme, tra cui .NET, Node.js e J2EE, ospitato in locale o nel cloud hello. Si integra con il processo di devOps e con gli strumenti di sviluppo toovarious punti di connessione.

![Application Insights](./media/azure-log-audit/azure-log-audit-fig6.png)

Application Insights è destinato a team di sviluppo hello, toohelp è comprendere le prestazioni dell'app e modalità di utilizzo. Esegue il monitoraggio di:

-   **Frequenza delle richieste, tempi di risposta e percentuali di errore**: trovare le pagine più visitate, gli orari di visita e la posizione degli utenti.  Vedere quali pagine abbiano prestazioni migliori. Se i tempi di risposta e le percentuali di errore aumentano di pari passo con le richieste, è probabile che ci sia un problema di assegnazione delle risorse.

-   **Tassi di dipendenza, tempi di risposta e percentuali di errore**: trovare quali servizi esterni causino un rallentamento.

-   **Eccezioni** : analizzare le statistiche aggregata hello, o selezionare istanze specifiche e approfondire l'analisi dello stack hello e le richieste correlate. Vengono segnalate eccezioni di server e browser.

-   **Visualizzazioni pagina e prestazioni di carico**, segnalate dai browser degli utenti.

-   **Chiamate AJAX** dalle pagine Web: tassi, tempi di risposta e percentuali di errore.

-   **Numeri di utenti e sessioni**.

-   **Contatori delle prestazioni** dai computer server Windows o Linux, ad esempio l'uso di CPU, memoria e rete.

-   **Diagnostica dell'host** da Docker o Azure.

-   **Log di traccia di diagnostica** dall'app, in modo da poter correlare gli eventi di traccia con le richieste.

-   **Eventi personalizzati e le metriche** scrivere manualmente nei hello client o server codice tootrack eventi aziendali, ad esempio gli articoli venduti o giochi acquisite.

**Elenco degli scenari di integrazione e relative descrizioni:**

| Scenari di integrazione | Descrizione |
| --------------------- | :---------- |
|[Mappa delle applicazioni](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-app-map)|componenti di Hello dell'app, con le metriche principali e avvisi.||
|[Ricerca diagnostica dei dati dell'istanza](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-diagnostic-search)| Cercare e filtrare eventi come richieste, eccezioni, chiamate a dipendenze, tracce di log e visualizzazioni di pagina.||
|[Esplora metriche per i dati aggregati](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-metrics-explorer)|Esaminare, filtrare e segmentare dati aggregati come frequenza delle richieste, errori, eccezioni, tempi di risposta e tempi di caricamento delle pagine.||
|[Dashboard](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-dashboards#dashboards)|Combinare dati di più risorse e condividerli con altri utenti. Ideale per applicazioni con più componenti e continui vengono visualizzati nella chat team hello.||
|[Flusso di metriche live](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-live-stream)|Quando si distribuisce una nuova compilazione, è possibile controllare queste toomake indicatori di prestazioni in tempo quasi reale che tutto funziona come previsto.||
|[Analisi](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics)|Questo avanzato linguaggio di query consente di trovare risposta a domande approfondite sull'utilizzo e sulle prestazioni dell'app.||
|[Avvisi automatici e manuali](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-alerts)|Avvisi automatici adattano i modelli di normale dell'app tooyour di telemetria e trigger quando ci sono di fuori di modello comune di hello. È anche possibile impostare avvisi su livelli particolari delle metriche standard o personalizzate.||
|[Visual Studio](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-visual-studio)|Vedere i dati sulle prestazioni nel codice hello. Vai toocode dalle tracce dello stack.||
|[Power BI](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-power-bi)|Integrare le metriche di uso con altra business intelligence.||
|[API REST](https://dev.applicationinsights.io/)|Scrivere codice toorun query su dati non elaborati e le metriche.||
|[Esportazione continua](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-export-telemetry)|Esportazione bulk di dati non elaborati toostorage quando arriva.||

### <a name="azure-security-center-alerts"></a>Avvisi del Centro sicurezza di Azure
[Centro sicurezza di Azure](https://docs.microsoft.com/azure/security-center/security-center-intro) automaticamente raccoglie analizza e consente di integrare dati di log da risorse di Azure, rete hello e soluzioni partner connesso, ad esempio soluzioni di protezione firewall ed endpoint, minacce reali toodetect e ridurre falsi positivi. Viene visualizzato un elenco di avvisi di sicurezza in ordine di priorità del Centro sicurezza PC insieme hello informazioni necessarie tooquickly analizzare problema hello e indicazioni sul tooremediate un attacco.

Rilevamento minacce del Centro sicurezza PC funziona automaticamente la raccolta di informazioni di sicurezza da risorse di Azure, rete hello e soluzioni partner connesso. Viene avviata l'analisi di queste informazioni, correlazione spesso informazioni provenienti da più origini, tooidentify minacce. Avvisi di sicurezza sono classificati in Centro sicurezza PC insieme ai consigli su come tooremediate hello minaccia.

![Centro sicurezza di Azure](./media/azure-log-audit/azure-log-audit-fig7.png)

Il Centro sicurezza si avvale di analisi della sicurezza avanzate, che vanno ben oltre gli approcci basati sulle firme. Successi in dati di grandi dimensioni e [machine learning](https://azure.microsoft.com/blog/machine-learning-in-azure-security-center/) tecnologie sono applicati tooevaluate eventi attraverso l'infrastruttura di cloud intera hello: rilevamento minacce che sarebbero Impossibile tooidentify approcci manuali e utilizzato per stimare hello evoluzione di attacchi. Queste analisi della sicurezza includono:

-   **Integrato sulle minacce:** ha un aspetto per noti cattivi attori applicando globale sulle minacce prodotti e servizi, Microsoft hello Microsoft Digital Crimes Unit (DCU), hello Microsoft Security Response Center (MSRC) ed esterne i feed.

-   **Comportamento analitica:** applica il comportamento di schemi noti toodiscover dannoso.

-   **Rilevamento di anomalie:** Usa statistiche di profiling toobuild una linea di base cronologico. Avvisa sulle deviazioni dalle linee di base stabilite conformi tooa potenziali attacchi.


Molte operazioni di sicurezza e i team di risposta agli eventi imprevisti si basano su una soluzione di informazioni di sicurezza e gestione di eventi (SIEM) come punto di partenza per la valutazione e analisi degli avvisi di sicurezza hello. Con l'integrazione dei log di Azure, i clienti possono sincronizzare gli avvisi del Centro sicurezza e gli eventi di sicurezza delle macchine virtuali, raccolti da Diagnostica di Azure e dai log di controllo di Azure, con la propria soluzione SIEM o di analisi dei log quasi in tempo reale.


## <a name="log-analytics"></a>Log Analytics

Log Analytics è un servizio di [Operations Management Suite (OMS)](https://docs.microsoft.com/azure/operations-management-suite/operations-management-suite-overview) che consente di raccogliere e analizzare i dati generati dalle risorse nel cloud e negli ambienti locali. Fornisce informazioni in tempo reale tramite la ricerca integrata e dashboard personalizzati tooreadily analizzare milioni di record in tutti i carichi di lavoro e i server indipendentemente dalla loro posizione fisica.

![Log Analytics](./media/azure-log-audit/azure-log-audit-fig8.png)

Centro di Log Analitica hello è repository OMS hello, che è ospitato in hello cloud di Azure. Raccolta dei dati nel repository di hello dai origini connesse, la configurazione delle origini dati e Aggiunta sottoscrizione tooyour di soluzioni. Origini dati e soluzioni ogni creare tipi di record diversi possono ancora essere analizzati insieme nel repository di query toohello ma il proprio set di proprietà. In questo modo hello toouse stesso toowork strumenti e i metodi con diversi tipi di dati raccolti da diverse origini.

Origini collegate sono computer hello e altre risorse che generano dati raccolti da Log Analitica. Sono inclusi gli agenti installati nei computer [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-windows-agents) e [Linux](https://docs.microsoft.com/azure/log-analytics/log-analytics-linux-agents) che si connettono direttamente o gli agenti in un [gruppo di gestione di System Center Operations Manager connesso](https://docs.microsoft.com/azure/log-analytics/log-analytics-om-agents). Log Analytics può anche raccogliere dati da [Archiviazione di Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage).

[Origini dati](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources) sono hello diversi tipi di dati raccolti da ogni origine connessa. Questo include gli eventi e [dati sulle prestazioni](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-performance-counters) da [Windows](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-windows-events) e gli agenti Linux in toosources aggiunta, ad esempio [registri IIS](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-iis-logs), e [registri di testo personalizzato.](https://docs.microsoft.com/azure/log-analytics/log-analytics-data-sources-custom-logs) Configurare ogni origine dati che si desidera toocollect e configurazione di hello è origine connessa tooeach recapitato automaticamente.

Esistono quattro diversi modi per [raccogliere log e metriche per i servizi di Azure](https://docs.microsoft.com/azure/log-analytics/log-analytics-azure-storage):
1.  Diagnostica di Azure diretto tooLog Analitica (diagnostica di hello nella tabella seguente)

2.  Diagnostica di Azure tooAzure archiviazione tooLog Analitica (archiviazione in hello nella tabella seguente)

3.  Connettori per servizi di Azure (connettori hello nella tabella seguente)

4.  Script di toocollect e, successivamente, i dati post in Log Analitica (vuote nella tabella seguente hello e per i servizi che non sono elencati)

| Service | Tipo di risorsa | Log | Metrica | Soluzione |
| :------ | :------------ | :--- | :------ | :------- |
|Gateway di applicazione|  Microsoft.Network/<br>applicationGateways|  Diagnostica|Diagnostica|    [Analisi dei ](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)gateway applicazione[ di Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-application-gateway-analytics-solution-in-log-analytics)|
|Application Insights||     Connettore|  Connettore|  [Application Insights](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)[Connector (Anteprima)](https://blogs.technet.microsoft.com/msoms/2016/09/26/application-insights-connector-in-oms/)|
|Account di Automazione|   Microsoft.Automation/<br>AutomationAccounts|    Diagnostica||       [Altre informazioni](https://docs.microsoft.com/en-us/azure/automation/automation-manage-send-joblogs-log-analytics)|
|Account Batch|    Microsoft.Batch/<br>batchAccounts|  Diagnostica|    Diagnostica||
|Servizi cloud classici||       Archiviazione||       [Altre informazioni](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-storage-iis-table)|
|Servizi cognitivi|    Microsoft.CognitiveServices/<br>account|       Diagnostica|||
|Data Lake Analytics|   Microsoft.DataLakeAnalytics/<br>account|   Diagnostica|||
|Data Lake Store|   Microsoft.DataLakeStore/<br>account|   Diagnostica|||
|Spazio dei nomi dell'hub eventi|   Microsoft.EventHub/<br>spazi dei nomi|  Diagnostica|    Diagnostica||
|Hub IoT|  Microsoft.Devices/<br>Hub IoT||     Diagnostica||
|Insieme di credenziali di chiave| Microsoft.KeyVault/<br>insiemi di credenziali|  Diagnostica  || [KeyVault Analytics](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-key-vault)|
|Servizi di bilanciamento del carico|    Microsoft.Network/<br>loadBalancers|    Diagnostica|||
|App per la logica|    Microsoft.Logic/<br>flussi di lavoro|  Diagnostica|    Diagnostica||
||Microsoft.Logic/<br>integrationAccounts||||
|Gruppi di sicurezza di rete|   Microsoft.Network/<br>networksecuritygroups|Diagnostica||   [Analisi del gruppo di sicurezza di rete di Azure](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-azure-networking-analytics#azure-network-security-group-analytics-solution-in-log-analytics)|
|Insiemi di credenziali di ripristino|   Microsoft.RecoveryServices/<br>insiemi di credenziali|||[Azure Recovery Services Analytics (Anteprima)](https://github.com/krnese/AzureDeploy/blob/master/OMS/MSOMS/Solutions/recoveryservices/)|
|Servizi di ricerca|   Microsoft.Search/<br>searchServices|    Diagnostica|    Diagnostica||
|Spazio dei nomi del bus di servizio| Microsoft.ServiceBus/<br>spazi dei nomi|    Diagnostica|Diagnostica|    [Service Bus Analytics (Anteprima)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-servicebus-solution)|
|Service Fabric||       Archiviazione||    [Service Fabric Analytics (anteprima)](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-service-fabric)|
|SQL (versione 12)| Microsoft.Sql/<br>servers/<br>database||       Diagnostica||
||Microsoft.Sql/<br>servers/<br>elasticPools||||
|Archiviazione|||         Script| [Azure Storage Analytics (Anteprima)](https://github.com/Azure/azure-quickstart-templates/tree/master/oms-azure-storage-analytics-solution)|
|Macchine virtuali|  Microsoft.Compute/<br>virtualMachines|  Estensione|  Estensione||
||||Diagnostica||
|Set di scalabilità di macchine virtuali|   Microsoft.Compute/<br>virtualMachines    ||Diagnostica||
||Microsoft.Compute/<br>virtualMachineScaleSets/<br>virtualMachines||||
|Server farm Web|Microsoft.Web/<br>serverfarms||   Diagnostica
|Microsoft Azure| Microsoft.Web/<br>siti ||      Diagnostica|    [Altre informazioni](https://github.com/Azure/azure-quickstart-templates/tree/master/101-webappazure-oms-monitoring)|
||Microsoft.Web/<br>sites/<br>slot|||||


## <a name="log-integration-with-on-premises-siem-systems"></a>Integrazione dei log con i sistemi SIEM locali
[Integrazione di log di Azure](https://www.microsoft.com/download/details.aspx?id=53324) consente toointegrate registri raw dalle risorse di Azure in tooyour locale **sistemi di informazione di sicurezza e gestione di eventi (SIEM)**.

![Integrazione dei log](./media/azure-log-audit/azure-log-audit-fig9.png)

L'integrazione dei log di Azure raccoglie i dati di Diagnostica di Azure dalle macchine virtuali Windows (WAD), i log attività di Azure, gli avvisi del Centro sicurezza di Azure e i log dei provider di risorse di Azure. Questa integrazione rappresenta un dashboard unificato di tutte le risorse, locale o cloud hello, in modo che è possibile aggregare, correlare, analizzare e avviso per gli eventi di sicurezza.



L'integrazione dei log di Azure supporta attualmente l'integrazione dei log di attività di Azure, del log eventi della macchina virtuale Windows inclusa nella sottoscrizione di Azure, degli avvisi del Centro sicurezza di Azure, dei log di Diagnostica di Azure e dei log di controllo di Azure Active Directory.

| Tipo di log | Log Analytics con supporto JSON (Splunk, ArcSight, Qradar) |
| :------- | :-------------------------------------------------------- |
|Log di controllo AAD|    sì|
|Log attività| Sì|
|Avvisi del Centro sicurezza di Azure |Sì|
|Log di diagnostica (log di risorse)|  Sì|
|Log VM|   Sì, tramite Eventi inoltrati e non attraverso JSON|


Hello nella tabella seguente illustra la categoria di Log hello e i dettagli di integrazione con SIEM.

[Introduzione all'integrazione dei log di Azure](https://docs.microsoft.com/azure/security/security-azure-log-integration-get-started) - L'esercitazione illustra come installare l'integrazione dei log di Azure e integrare i log dall'archiviazione di Azure WAD, i log attività di Azure, gli avvisi del Centro sicurezza di Azure e i log di controllo di Azure Active Directory.

Scenari di integrazione

-   [Passaggi di configurazione di partner](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/) – questo post di blog viene illustrato come tooconfigure Azure log toowork integrazione con soluzioni di partner Splunk e ArcSight HP, IBM QRadar.

-   [Domande frequenti sull'integrazione dei log di Azure](https://docs.microsoft.com/azure/security/security-azure-log-integration-faq) - Queste domande frequenti riguardano l'integrazione dei log di Azure.

-   [L'integrazione di Centro sicurezza PC avvisi con Azure log integrazione](https://docs.microsoft.com/azure/security-center/security-center-integrating-alerts-with-log-integration) : questo documento viene illustrato come centro di sicurezza toosync avvisi, insieme agli eventi di sicurezza di macchina virtuale raccolti da diagnostica di Azure e i log di controllo di Azure con analitica il log o Soluzione SIEM.

## <a name="next-steps"></a>Passaggi successivi

- [Controllo e registrazione](https://www.microsoft.com/trustcenter/security/auditingandlogging)

Proteggere i dati dalla gestione della visibilità e rispondere rapidamente tootimely degli avvisi di sicurezza

- [Raccolta dei log di controllo e di registrazione di sicurezza all'interno di Azure](https://azure.microsoft.com/resources/videos/security-logging-and-audit-log-collection/)

Quali impostazioni è necessario che la raccolta di istanze di Azure con tooenforce toomake hello sicurezza corrette e i log di controllo.

- [Configurare le impostazioni di controllo per una raccolta di siti](https://support.office.com/article/Configure-audit-settings-for-a-site-collection-A9920C97-38C0-44F2-8BCB-4CF1E2AE22D2?ui=&rs=&ad=US)

Come un amministratore della raccolta siti, uno può recuperare la cronologia della hello delle azioni eseguite da un utente specifico e può inoltre recuperare la cronologia hello delle azioni eseguite durante un intervallo di date specifico. 

- [Log di controllo di ricerca hello in Office 365 sicurezza hello & centro conformità](https://support.office.com/article/Search-the-audit-log-in-the-Office-365-Security-Compliance-Center-0d4d0f35-390b-4518-800e-0c7ec95e946c?ui=&rs=&ad=US)

Una possibile utilizzare hello centro di conformità e sicurezza di Office 365 toosearch hello unificata audit log tooview utente e attività dell'amministratore dell'organizzazione a Office 365.


