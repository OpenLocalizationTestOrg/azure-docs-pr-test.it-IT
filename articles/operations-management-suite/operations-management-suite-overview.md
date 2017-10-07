---
title: Panoramica di Management Suite (OMS) aaaOperations | Documenti Microsoft
description: "Microsoft Operations Management Suite (OMS) è la soluzione Microsoft per la gestione IT basata sul cloud che consente di gestire e proteggere l'infrastruttura locale e cloud.  In questo articolo viene descritto il valore di hello di OMS, identifica hello diversi servizi e offerte incluse in OMS e vengono forniti i collegamenti tootheir dettagliate contenuto."
services: operations-management-suite
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 9dc437b9-e83c-45da-917c-cb4f4d8d6333
ms.service: operations-management-suite
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/16/2017
ms.author: bwren
ms.openlocfilehash: ec3fe6d82aec46d1f715a4338f126e79e04a9147
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-operations-management-suite-oms"></a>Informazioni su Operations Management Suite (OMS)
Questo articolo fornisce un tooOperations introduzione Management Suite (OMS), tra cui una breve panoramica di offerte hello tale pacchetto insieme a diversi servizi, soluzioni di servizi e la gestione di hello include e fornisce il valore di business hello e soluzioni.  Sono inclusi i collegamenti toohello dettagliate documentazione sulla distribuzione e l'utilizzo di ogni servizio e la soluzione.

## <a name="from-on-premises-toohello-cloud"></a>Dal cloud toohello locale
Microsoft offre da tempo prodotti per la gestione degli ambienti aziendali.  Più prodotti sono stati consolidati in famiglia di prodotti di gestione di System Center hello in 2007.  Sono stati Configuration Manager che fornisce funzionalità quali la distribuzione del software e inventario, Operations Manager, che fornisce il monitoraggio proattivo dei sistemi e applicazioni, Orchestrator che include i processi manuali tooautomate di runbook e Data Protection Manager per il backup e ripristino di dati critici.

Con più risorse di calcolo cloud toohello di spostamento, i prodotti System Center acquisita altre funzionalità di cloud, ad esempio Operations Manager e la gestione delle risorse in Azure di Orchestrator.  Erano però ancora sostanzialmente progettati come soluzioni locali e richiedevano un considerevole investimento dal punto di vista della distribuzione e della manutenzione dell'ambiente di gestione locale.  toocompletely sfruttare cloud hello e supportano future applicazioni, è necessaria una nuova toomanagement approccio.

## <a name="introducing-operations-management-suite"></a>Introduzione a Operations Management Suite
Operations Management Suite (noto anche come OMS) è una raccolta di servizi di gestione che sono stati progettati in cloud hello dall'inizio hello.  Invece di distribuire e gestire risorse locali, i componenti di OMS sono completamente ospitati in Azure.  La configurazione è minima ed è possibile essere operativi in davvero pochi minuti.  

- **Costi minimi e complessità della distribuzione.**  Poiché tutti i componenti di hello e i dati per OMS vengono archiviati in Azure, è e in esecuzione in un breve periodo di tempo senza la complessità di hello e investimenti in locale i componenti.
- **Toocloud livelli di scala.**  Non si dispone di tooworry sul pagamento per le risorse di calcolo che non è necessario o sull'esaurimento dello spazio di archiviazione dall'hello cloud consente toopay solo per ciò che è effettivamente utilizzare e consente di scalare facilmente carico tooany desiderate.  È possibile avviare alcuni tooget risorse avviata la gestione e quindi applicare la scalabilità verticale tooyour tutto l'ambiente.
- **È possibile sfruttare funzionalità più recenti di hello.**  Nei servizi OMS vengono continuamente aggiunte e aggiornate diverse funzionalità.  Continuamente, è necessario accedere alle funzionalità più recenti di toohello senza aggiornamenti toodeploy requisito.
- **Servizi integrati.**  Anche se ognuno dei servizi OMS hello fornisce un valore significativo in modo autonomo, possano funzionare insieme toosolve scenari di gestione complesse.  Ad esempio, un runbook in automazione di Azure potrebbe essere l'unità di un processo di failover con Azure Site Recovery e quindi accedere a informazioni tooLog Analitica toogenerate un avviso.
- **Conoscenza globale.**  Le soluzioni di gestione in OMS hanno continuamente informazioni più recenti toohello di accesso.  Hello soluzione Security and Audit, ad esempio, è possibile eseguire un'analisi di minaccia utilizzando minacce più recenti di hello viene rilevate in tutto il mondo hello.
- **Accesso ovunque.**  Per accedere all'ambiente di gestione è sufficiente un browser.  Installare app OMS hello sul tuo smartphone per dati di monitoraggio tooyour accesso immediato.

### <a name="is-it-just-for-hello-cloud"></a>È solo per cloud hello?
Il fatto che i servizi OMS vengono eseguiti nel cloud hello non significa che non è possibile gestire efficacemente l'ambiente locale.  Inserire un agente su tutte le finestre o computer Linux nel proprio data center e invierà tooLog dati Analitica in cui possono essere analizzato insieme a tutti gli altri dati raccolti dai servizi cloud o locale.  Utilizzare Backup di Azure e Azure Site Recovery cloud hello tooleverage per backup e disponibilità elevata per le risorse locali.  
I runbook nel cloud hello in genere non è possibile accedere alle risorse di on-premise, ma è possibile installare un agente in uno o più computer troppo che ospiterà i runbook nel data center.  Quando si avvia un runbook, è sufficiente specificare se si desidera che toorun nel cloud hello o in un thread di lavoro locale.

## <a name="hybrid-management-with-system-center"></a>Gestione ibrida con System Center
Se si dispone di un'installazione esistente di System Center, è possibile integrare questi componenti con servizi OMS tooprovide una soluzione ibrida per entrambi locale e cloud ambienti sfruttando specializzazioni di relativo hello di ogni prodotto.  Connettere gli esistenti agenti Operations Manager Gestione gruppo tooLog Analitica tooanalyze gestiti nel cloud hello.  Utilizzare il processo di backup esistente con Data Protection Manager toobackup toohello i dati nel cloud.  


## <a name="oms-services"></a>Servizi OMS
funzionalità di base Hello di OMS viene fornita da un set di servizi in esecuzione in Azure.  Ogni servizio fornisce una funzione di gestione specifico, ed è possibile combinare gli scenari di gestione diverso di servizi tooachieve.

|| Service | Descrizione |
|:--|:--|:--|
| ![Log Analytics](media/operations-management-suite-overview/icon-log-analytics.png) | Log Analytics | Monitorare e analizzare hello disponibilità e prestazioni di diverse risorse incluse fisici e macchine virtuali. |
| ![Automazione di Azure](media/operations-management-suite-overview/icon-automation.png) | Automazione | Automatizza i processi manuali ed applica le configurazioni per i computer fisici e le macchine virtuali. |
| ![Backup di Azure](media/operations-management-suite-overview/icon-backup.png) | Backup | Esegue il backup e ripristino dei dati critici. |
| ![Azure Site Recovery](media/operations-management-suite-overview/icon-site-recovery.png) | Site Recovery | Offre disponibilità elevata per le applicazioni critiche. |

### <a name="log-analytics"></a>Log Analytics
[Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics) fornisce servizi di monitoraggio per OMS raccogliendo i dati delle risorse gestite in un repository centrale.  Questi dati possono includere gli eventi, dati sulle prestazioni o dati personalizzati forniti tramite hello API. Una volta raccolti, hello sono disponibili dati per gli avvisi, l'analisi e l'esportazione.  Questo metodo consente tooconsolidate dati da diverse origini in modo è possibile combinare dati da servizi di Azure con l'ambiente locale esistente.  Inoltre chiaramente separa raccolta hello di dati hello dall'azione di hello eseguita su tali dati in modo che tutte le azioni sono tooall disponibili tipi di dati.  

![Panoramica di Log Analytics](media/operations-management-suite-overview/overview-log-analytics.png)

#### <a name="collecting-data"></a>Raccolta dei dati
Esistono diversi modi in cui è possibile ottenere i dati nel repository di hello per tooanalyze Analitica di Log.

- **Computer e macchine virtuali Windows o Linux.**  Installare Microsoft Monitoring Agent hello in [Windows](../log-analytics/log-analytics-windows-agents.md) e [Linux](../log-analytics/log-analytics-linux-agents.md) computer o macchine virtuali che si desidera che i dati toocollect da.  agente Hello viene scaricato automaticamente dalla configurazione di Log Analitica che definisce gli eventi e toocollect dati sulle prestazioni.  È possibile installarlo agente hello in macchine virtuali in esecuzione in Azure utilizzando hello portale di Azure.  Se si dispone di un ambiente di Operations Manager esistente, è possibile connettersi hello gestione gruppo tooLog Analitica e avviare automaticamente la raccolta dei dati da tutti gli agenti esistenti.
- **Servizi di Azure.**  Log Analitica raccoglie dati di telemetria da [diagnostica di Azure e Azure Monitoring](../log-analytics/log-analytics-azure-storage.md) repository hello in modo che è possibile monitorare le risorse di Azure.
- **API di raccolta dati.**  Log Analytics ha un'[API REST per popolare i dati da qualsiasi client](../log-analytics/log-analytics-data-collector-api.md).  Questo consente toocollect dati da applicazioni di terze parti o implementare scenari di gestione personalizzata.  Un metodo comune è toouse un runbook in dati toocollect di automazione di Azure e quindi utilizzare toowrite API dell'agente di raccolta dati hello è toohello repository.

#### <a name="reporting-and-analyzing-data"></a>Creazione di report e analisi dei dati
Log Analitica include un potente query language tooextract di dati archiviati nel repository di hello.  Poiché i dati di tutte le origini vengono archiviati come record, è possibile analizzare i dati di più origini in una singola query.
  
Inoltre analisi ad hoc tooad, Analitica Log fornisce più modi tooreport e analizzare i dati da una query.

- **Viste e dashboard.**  [Viste](../log-analytics/log-analytics-view-designer.md) e [dashboard](../log-analytics/log-analytics-dashboards.md) visualizzare risultati hello di una query nel portale di hello.  Soluzioni di gestione in genere contiene viste che consentono di analizzare dati hello dalla soluzione hello.  È anche possibile creare visualizzazioni personalizzate tooanalyze dati e renderla immediatamente disponibile nel portale personalizzato.
- **Esportazione.**  Si dispone di risultati di hello opzione tooexport hello delle query in modo che consente di analizzare i Log Analitica di fuori di.  È anche possibile pianificare un'esportazione regolare troppo[Power BI](../log-analytics/log-analytics-powerbi.md) che fornisce potenti funzionalità di visualizzazione e analisi.
- **API di ricerca log.**  Log Analytics ha un'[API REST per raccogliere i dati da qualsiasi client](../log-analytics/log-analytics-log-search-api.md).  Questo consente tooprogrammatically lavoro con i dati raccolti nel repository di hello o accedervi da un altro strumento di monitoraggio.

#### <a name="alerting"></a>Creazione di avvisi
Log Analytics può [avvisare in modo proattivo](../log-analytics/log-analytics-alerts.md) o eseguire un'azione correttiva quando rileva un problema.  Come tutte le altre operazioni di analisi in Log Analytics, anche questa viene eseguita con una ricerca log.  Questa ricerca viene eseguita a intervalli regolari e viene creato un avviso se i risultati di hello corrispondono a determinati criteri.

![Avvisi Log Analytics](media/operations-management-suite-overview/overview-alerts.png)

Inoltre toocreating un record di avviso nel repository di hello Analitica di Log, degli avvisi possono richiedere hello seguenti azioni.

- **Posta elettronica.**  Inviare un messaggio di posta elettronica tooproactively notifica di un problema rilevato.
- **Runbook.**  Un avviso in Log Analytics può avviare un runbook in Automazione di Azure.  Ciò avviene in genere problema di tooattempt toocorrect hello rilevato.  Hello runbook può essere avviato nel cloud hello in hello case di un problema in Azure o un altro cloud o è stato possibile avviare un agente locale per un problema per una macchina virtuale o fisica.
- **Webhook.**  Un avviso può avviare un webhook e passare dati dai risultati della ricerca log hello di hello.  Ciò consente l'integrazione con servizi esterni, ad esempio un altro sistema di avvisi, o può tentare l'azione correttiva tootake per un sito web esterno.

### <a name="azure-automation"></a>Automazione di Azure
[Automazione di Azure](http://azure.microsoft.com/documentation/services/automation) fornisce tooOMS Gestione automazione e la configurazione di processo.  Consente di automatizzare i processi manuali e aiuta a tooenforce configurazioni per i computer fisici e virtuali.  

#### <a name="process-automation"></a>Automazione dei processi
Automazione di Azure automatizza i processi manuali usando i [runbook](../automation/automation-runbook-types.md) che si basano su uno script di PowerShell o su un flusso di lavoro di PowerShell.  Include inoltre un asset che supporta i runbook, ad esempio variabili che possono essere condivisi tra più runbook e le credenziali e le connessioni che consentono di toostore crittografati informazioni che potrebbero essere necessarie per un runbook per l'autenticazione.
I runbook offrono l'automazione dei processi per hello altri servizi nella suite di hello.  Poiché ogni di hello è possibile accedere ad altri servizi con PowerShell o tramite un'API REST, è possibile creare runbook tooperform tali funzioni come raccolta di dati di gestione nel Log Analitica o l'avvio di un backup con Backup di Azure.

##### <a name="accessing-resources"></a>Accesso alle risorse
Poiché i runbook si basano su PowerShell, possono gestire qualsiasi risorsa accessibile con i cmdlet di PowerShell.  Quando si [caricare un modulo](../automation/automation-integration-modules.md) nell'account di automazione, diventa disponibile tooall runbook in tale account. 
 
Quando runbook eseguiti nel cloud hello, possono accedere tutte le risorse accessibili dal cloud hello.  Può trattarsi di risorse nella sottoscrizione di Azure, in un altro cloud, ad esempio Amazon Web Services (AWS), o in un servizio accessibile tramite un'API REST.  I runbook nel cloud hello non vengono eseguiti con le credenziali, ma in grado di sfruttare gli asset di automazione, ad esempio le credenziali, connessioni e i certificati tooauthenticate tooresources che accedono.

Non è possibile accedere alle risorse nel data center probabilmente da un runbook in esecuzione nel cloud hello.  È possibile installare uno o più [Runbook worker ibridi](../automation/automation-hybrid-runbook-worker.md) nei dati center tuttavia toorun runbook che richiedono l'accesso alle risorse di toolocal.  Quando si avvia un runbook, specificare se deve essere eseguito nel cloud hello o in un processo di lavoro specifico.

![Runbook di Automazione di Azure](media/operations-management-suite-overview/overview-runbooks.png)

##### <a name="starting-a-runbook"></a>Avvio di un runbook
Poiché i runbook possono essere [avviati con diversi metodi](../automation/automation-starting-a-runbook.md), è possibile includerli in svariati scenari di gestione.  

- **Portale di Azure.**  Analogamente ad altri servizi Azure, è possibile gestire automazione di Azure dal portale di Azure hello.  Inoltre toostarting runbook, è possibile importarli o creare propri.
- **Pianificazione.**  È possibile pianificare i runbook toostart a intervalli regolari.  In questo modo è tooautomatically ripetere un processo di gestione regolare o raccogliere dati tooLog Analitica.
- **PowerShell e API.**  È possibile avviare i runbook e passare le necessarie informazioni sui parametri da un cmdlet di PowerShell o hello API REST di automazione di Azure.  
- **Webhook.**  È possibile creare un webhook per qualsiasi runbook che ne consenta toobe avviato da applicazioni esterne o siti web.
- **Avviso di Log Analytics.**  Un avviso nel Log Analitica può essere avviato automaticamente un problema di hello runbook tooattempt toocorrect identificato dall'avviso hello.

#### <a name="configuration-management"></a>Gestione della configurazione
[PowerShell DSC Desired State Configuration ()](../automation/automation-dsc-overview.md) è una piattaforma di gestione di Windows PowerShell che consente di toodeploy e applicare la configurazione di hello del fisico e macchine virtuali.  Automazione di Azure gestisce le configurazioni DSC e fornisce un server di pull in cloud hello che gli agenti possano accedere configurazioni tooretrieve richiesto.

![Automation DSC per Azure](media/operations-management-suite-overview/overview-dsc.png)

### <a name="azure-backup-and-azure-site-recovery"></a>Backup di Azure e Azure Site Recovery
Backup di Azure e Azure Site Recovery contribuiscono toobusiness continuità e ripristino di emergenza.  Ognuna di esse presenta caratteristiche che consentono di tooensure che le applicazioni rimangano disponibili quando interruzioni e restituiscono toonormal operazioni quando i sistemi ritornano online.  Entrambi i servizi contribuiscono toohello obiettivi del punto di ripristino (RPO) e gli obiettivi del tempo di ripristino (RTO) definiti per l'organizzazione. L'obiettivo RPO definisce limite accettabile di hello in cui dati non sono disponibili durante un'interruzione, i hello RTO quantità accettabile di hello di tempo in cui un servizio o un'app non è disponibile durante un'interruzione.

#### <a name="azure-backup"></a>Backup di Azure
[Backup di Azure](http://azure.microsoft.com/documentation/services/backup) fornisce servizi di backup e ripristino dei dati per OMS.  Protegge i dati delle applicazioni e li conserva per anni, senza investimenti di capitali e con costi operativi minimi.  Può eseguire il backup dei dati dal server Windows fisici e virtuali nei carichi di lavoro tooapplication aggiunta, ad esempio SQL Server e SharePoint.  Può essere utilizzato anche da tooAzure dati tooreplicate protetto di System Center Data Protection Manager (DPM) per la ridondanza e archiviazione a lungo termine.

I dati protetti in Backup di Azure vengono archiviati in un insieme di credenziali di backup che si trova in una determinata area geografica. Hello dati vengono replicati all'interno hello stessa area geografica e, in base al tipo di hello dell'insieme di credenziali, possono essere replicati tooanother area per un'ulteriore resilienza.

Backup di Azure prevede tre scenari fondamentali.

- **Computer Windows con l'agente di Backup di Azure.** Backup di file e cartelle da qualsiasi client o server Windows direttamente tooyour insieme di credenziali di backup Azure.<br><br>![Computer Windows con l'agente di Backup di Azure](media/operations-management-suite-overview/overview-backup-01.png)
- **System Center Data Protection Manager (DPM) o server di Backup di Microsoft Azure.** Sfruttare DPM o il Server di Backup di Microsoft Azure toobackup i file e cartelle nei carichi di lavoro tooapplication aggiunta, ad esempio archiviazione toolocal SQL e SharePoint e quindi replicare tooyour insieme di credenziali di backup Azure. Supporta macchine virtuali Windows e Linux in Hyper-V o VMware.<br><br>![System Center Data Protection Manager (DPM) o server di Backup di Microsoft Azure](media/operations-management-suite-overview/overview-backup-02.png)
- **Estensioni delle macchine virtuali di Azure.** Backup di Windows o Linux virtuale macchine tooyour Azure insieme di credenziali di backup Azure.<br><br>![Estensioni delle macchine virtuali di Azure](media/operations-management-suite-overview/overview-backup-03.png)



#### <a name="azure-site-recovery"></a>Azure Site Recovery
[Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery) fornisce la continuità aziendale gestendo la replica locale virtuale e tooAzure macchine fisiche o tooa di sito secondario. Se il sito primario non è disponibile, è possibile failover posizione secondaria toohello in modo che gli utenti possono continuare a lavorare e failback quando i sistemi restituiscono tooworking ordine. 

Azure Site Recovery fornisce disponibilità elevata per i server e le applicazioni.  Contribuisce tooyour continuità aziendale e una strategia di ripristino di emergenza gestendo la replica, il failover e ripristino di macchine virtuali di Hyper-V locali, macchine virtuali VMware e server fisici Windows/Linux. È possibile replicare macchine tooa data center secondario o estendere il data center replicandole tooAzure. Site Recovery fornisce inoltre funzionalità per semplificare il failover e il ripristino dei carichi di lavoro. Si integra con i meccanismi di ripristino di emergenza come SQL Server AlwaysOn e prevede piani di ripristino per il failover semplificato dei carichi di lavoro organizzati su più livelli in diversi computer.

Azure Site Recovery prevede tre scenari di replica fondamentali.

- **Replica di macchine virtuali Hyper-V.**  Se le macchine virtuali Hyper-V vengono gestite nei cloud VMM, è possibile replicare l'archiviazione di dati secondari tooa center o tooAzure. Replica tooAzure è su una connessione internet sicura. Data Center secondario tooa di replica viene eseguita tramite hello LAN.  Se le macchine virtuali Hyper-V non sono gestite da VMM, è possibile replicare tooAzure esclusivamente all'archiviazione. Replica tooAzure è su una connessione internet sicura.<br><br>![Replica di macchine virtuali Hyper-V](media/operations-management-suite-overview/overview-siterecovery-hyperv.png)
- **Replica di macchine virtuali VMware.**  È possibile replicare VMware le macchine virtuali tooa Data Center secondario che esegue VMware o tooAzure di archiviazione. Replica tooAzure può essere eseguita tramite una VPN site-to-site o ExpressRoute di Azure o una connessione Internet sicura. Data Center secondario tooa di replica viene eseguita tramite il canale dati di InMage Scout hello.<br><br>![Replica di macchine virtuali VMware](media/operations-management-suite-overview/overview-siterecovery-vmware.png)
- **Replica di server fisici Windows e Linux.**  È possibile replicare i server fisici tooa Data Center o tooAzure archiviazione secondaria. Replica tooAzure può essere eseguita tramite una VPN site-to-site o ExpressRoute di Azure o una connessione Internet sicura. Data Center secondario tooa di replica viene eseguita tramite il canale dati di InMage Scout hello. Azure Site Recovery dispone di una soluzione OMS che visualizza alcune statistiche, ma è necessario utilizzare hello portale di Azure per qualsiasi operazione.<br><br>![Replica di server fisici Windows e Linux](media/operations-management-suite-overview/overview-siterecovery-physical.png)


Site Recovery archivia i metadati in insiemi di credenziali che si trovano in una determinata area geografica di Azure. Nessun dato replicato viene archiviato dal servizio Site Recovery hello.

## <a name="management-solutions"></a>Soluzioni di gestione
Le [soluzioni di gestione](operations-management-suite-solutions.md) sono set predefiniti di logica che implementano un particolare scenario di gestione sfruttando uno o più servizi OMS.  Diverse soluzioni sono disponibili da Microsoft e dai partner che è possibile aggiungere facilmente tooyour valore hello tooincrease di sottoscrizione di Azure dell'investimento in OMS.  Come partner è possibile creare la propria toosupport soluzioni le applicazioni e servizi e fornire loro toousers tramite hello Azure Marketplace o modelli di avvio rapido.

Un buon esempio di una soluzione che sfrutti più funzionalità aggiuntive di servizi tooprovide è hello [soluzione di gestione degli aggiornamenti](oms-solution-update-management.md).  Questa soluzione Usa l'agente di Log Analitica hello per Windows e Linux toocollect informazioni sugli aggiornamenti necessari in ogni agente.  Scrive questo repository Analitica Log toohello di dati in cui è possibile analizzare con un dashboard incluso.  Quando si crea una distribuzione, i runbook in automazione di Azure sono utilizzati tooinstall necessari aggiornamenti.  Gestire l'intero processo nel portale di hello e non è necessario tooworry dettagli hello sottostante.

![Soluzione](media/operations-management-suite-overview/overview-solution.png)

La maggior parte delle soluzioni possono eseguire una o più delle seguenti funzioni hello.

- Raccogliere Informazioni aggiuntive.  Log Analytics raccoglie svariati dati da client e servizi, inclusi eventi e dati sulle prestazioni.  Una soluzione di gestione può raccogliere informazioni aggiuntive non disponibili in altre origini dati, spesso usando i runbook di Automazione di Azure.
- Fornire un'analisi aggiuntiva delle informazioni raccolte.  Le soluzioni di gestione includono dashboard e viste che consentono l'analisi e la visualizzazione dei dati.  Queste ricerche nei log toopredefined indietro collegamenti che consentono di organizzare toodrill in hello in dettaglio i dati.  Sono inoltre possibile eseguire analisi sui dati che sono già stato raccolto nel repository di hello, ad esempio ricerca gli eventi di sicurezza per i modelli che indicano una minaccia.
- Aggiungere funzionalità.  Alcune soluzioni fornite da Microsoft possono basarsi sulle funzionalità di hello di funzionalità aggiuntive di hello core services tooprovide.  Mappa del servizio, ad esempio, fornisce il proprio toodiscover console ed esegue il mapping di server e dipendenze dei processi in tempo reale.
Le soluzioni vengono regolarmente aggiunti tooOMS da Microsoft e partner consentono toocontinuously aumentare il valore di hello dell'investimento.  È possibile individuare e installare soluzioni Microsoft attraverso hello soluzioni catalogo nel portale OMS hello o Sfoglia e installare le soluzioni di Microsoft e partner tramite hello Azure Marketplace in hello portale di Azure.  

![Raccolta soluzioni](media/operations-management-suite-overview/solution-gallery.png)


## <a name="next-steps"></a>Passaggi successivi
* Informazioni su [Log Analytics](http://azure.microsoft.com/documentation/services/log-analytics)
* Informazioni su [Automazione di Azure](../automation/automation-intro.md)
* Informazioni su [Backup di Azure](http://azure.microsoft.com/documentation/services/backup)
* Informazioni su [Azure Site Recovery](http://azure.microsoft.com/documentation/services/site-recovery)
* Individuare hello [soluzioni disponibili](../log-analytics/log-analytics-add-solutions.md) nelle diverse offerte di OMS hello. 

