---
title: "aaaWhat i carichi di lavoro è possibile proteggere con Azure Site Recovery?"
description: Azure Site Recovery consente di proteggere i carichi di lavoro e le applicazioni coordinando replica hello, failover e ripristino di macchine virtuali in locale e server fisici tooAzure o tooa secondario nel sito locale
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: 4953948f-26c0-4699-8fe7-59d3bfc1d3da
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/08/2017
ms.author: raynew
ms.openlocfilehash: cab2e1ce3c2b7b2c5f899d957219f5c12eb5965c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-workloads-can-you-protect-with-azure-site-recovery"></a>Quali carichi di lavoro è possibile proteggere con Azure Site Recovery?
In questo articolo descrive i carichi di lavoro e applicazioni che è possibile replicare con hello servizio Azure Site Recovery.

Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="overview"></a>Panoramica
Le organizzazioni devono una continuità aziendale e carichi di lavoro tookeep strategia ripristino d'emergenza e dati sicuro ed è disponibile durante i tempi di inattività pianificati ed e ripristino le condizioni di lavoro tooregular appena possibile.

Il ripristino del sito è un servizio di Azure che contribuisce strategia BCDR tooyour. Tramite il ripristino del sito, è possibile distribuire cloud toohello replica compatibile con l'applicazione o sito secondario tooa. Se le app sono finestre o basati su Linux, in esecuzione nei server fisici, VMware o Hyper-V, è possibile utilizzare la replica tooorchestrate il ripristino del sito, eseguire i test del ripristino di emergenza ed eseguire i failover e failback.

Site Recovery si integra con numerose applicazioni Microsoft, tra cui SharePoint, Exchange, Dynamics, SQL Server e Active Directory. Microsoft collabora strettamente con fornitori leader, tra cui Oracle, SAP, IBM e Red Hat. È possibile personalizzare le soluzioni di replica in base alle app.

## <a name="why-use-site-recovery-for-application-replication"></a>Perché usare Site Recovery per la protezione della replica?
Il ripristino del sito contribuisce tooapplication a livello di protezione e ripristino come segue:

* Indipendente dall'app, fornendo la replica per carichi di lavoro in esecuzione in una macchina supportata.
* Replica quasi sincrono con RPO arrivare fino a 30 secondi toomeet hello esigenze più importanti applicazioni aziendali.
* Snapshot coerenti con l'app per le applicazioni a uno o più livelli.
* Integrazione con SQL Server AlwaysOn e interazione con altre tecnologie di replica a livello di applicazione, tra cui la replica di AD, SQL AlwaysOn, i gruppi di disponibilità dei database di Exchange e Oracle Data Guard.
* I piani di ripristino flessibile, che consentono di toorecover dello stack con un solo clic, un'intera applicazione e includere gli script esterni tooinclude e azioni manuali nel piano di hello.
* Avanzate di gestione di rete in Site Recovery e Azure toosimplify requisiti di rete di app, inclusi gli indirizzi IP di tooreserve possibilità hello, configurare il bilanciamento del carico e integrazione con Azure Traffic Manager, per switchovers di rete RTO basso.
* Una libreria di automazione avanzata che fornisce script pronti per la produzione e specifici per ogni applicazione, che possono essere scaricati e integrati nei piani di ripristino.

## <a name="workload-summary"></a>Riepilogo dei carichi di lavoro
Site Recovery può replicare qualsiasi app in esecuzione in una macchina supportata. Inoltre Collaboriamo con toocarry i team di prodotto out ulteriori test specifico dell'applicazione.

| **Carico di lavoro** | **Replica macchine virtuali Hyper-V tooa del sito secondario** | **Replicare macchine virtuali Hyper-V tooAzure** | **Replica le macchine virtuali VMware tooa del sito secondario** | **Replicare le macchine virtuali VMware tooAzure** |
| --- | --- | --- | --- | --- |
| Active Directory, DNS  |S |S |S |S |
| App Web (IIS, SQL) |S |S |S |S |
| System Center Operations Manager |S |S |S |S |
| SharePoint |S |S |S |S |
| SAP<br/><br/>Replicare tooAzure sito SAP per non cluster |Y (testato da Microsoft) |Y (testato da Microsoft) |Y (testato da Microsoft) |Y (testato da Microsoft) |
| Exchange (non DAG) |S |S |S |S |
| Desktop remoto/VDI |S |S |S |N/D |
| Linux (sistema operativo e app) |Y (testato da Microsoft) |Y (testato da Microsoft) |Y (testato da Microsoft) |Y (testato da Microsoft) |
| Dynamics AX |S |S |S |S |
| Dynamics CRM |S |Presto disponibile |S |Presto disponibile |
| Oracle |Y (testato da Microsoft) |Y (testato da Microsoft) |Y (testato da Microsoft) |Y (testato da Microsoft) |
| File Server Windows |S |S |S |S |
| Citrix XenApp e XenDesktop |N/D |S |N/D |S |

## <a name="replicate-active-directory-and-dns"></a>Replicare Active Directory e DNS
Un'infrastruttura Active Directory e DNS sono le app aziendali toomost essenziali. Durante il ripristino di emergenza, si sarà necessario tooprotect e ripristinare questi componenti dell'infrastruttura, prima di recuperare i carichi di lavoro e applicazioni.

È possibile utilizzare il ripristino del sito toocreate un piano di ripristino di emergenza automatizzati completo per Active Directory e DNS. Ad esempio, se si desidera toofail su SharePoint e SAP da un sito secondario tooa primario, è possibile configurare un piano di ripristino viene eseguito il failover Active Directory prima di tutto, e quindi un ripristino specifico dell'applicazione aggiuntivi pianificare toofail su hello altre App che si basano su attivo Directory.

[Altre informazioni](site-recovery-active-directory.md) sulla protezione di Active Directory e DNS.

## <a name="protect-sql-server"></a>Proteggere SQL Server
SQL Server fornisce un base per i servizi dati di molte app aziendali in un data center locale.  Il ripristino del sito è utilizzabile con tecnologie di SQL Server a disponibilità elevata/ripristino di emergenza, le applicazioni a più livelli enterprise tooprotect che utilizzano SQL Server. Site Recovery offre:

* Una soluzione di ripristino di emergenza semplice ed economica per SQL Server. Replicare più versioni ed edizioni del server di SQL Server autonomi e cluster, tooAzure o tooa sito secondario.  
* Integrazione con i gruppi di disponibilità AlwaysOn SQL, toomanage failover e failback con i piani di ripristino di Azure Site Recovery.
* Piani di ripristino end-to-end per hello tutti i livelli di un'applicazione, inclusi i database di SQL Server hello.
* Possibilità di ridimensionamento di SQL Server per i picchi di carico con Site Recovery, espandendoli in macchine virtuali IaaS di dimensioni maggiori in Azure.
* Esecuzione facilitata dei test di ripristino di emergenza di SQL Server. È possibile eseguire i test failover tooanalyze dati ed eseguire controlli di conformità, senza alcun impatto sull'ambiente di produzione.

[Altre informazioni](site-recovery-sql.md) sulla protezione di SQL server.

## <a name="protect-sharepoint"></a>Proteggere SharePoint
Azure Site Recovery consente di proteggere le distribuzioni di SharePoint come indicato di seguito:

* Elimina l'esigenza di hello e i costi di infrastruttura associato per una farm di standby per il ripristino di emergenza. Utilizzare il ripristino del sito tooreplicate un'intera farm (livelli di applicazione, Web e il database) tooAzure o tooa del sito secondario.
* Semplifica la distribuzione di applicazioni e la gestione. Aggiornamenti distribuiti toohello primario di sito vengono replicate automaticamente e sono pertanto disponibile dopo il failover e ripristino di una farm in un sito secondario. Inoltre riduce la complessità della gestione hello e i costi associati all'aggiornamento di una farm di standby.
* Semplifica lo sviluppo e i test dell'applicazione SharePoint creando una copia su richiesta simile a quella in produzione per il test e il debug nell'ambiente di replica.
* Tramite il ripristino del sito toomigrate SharePoint distribuzioni tooAzure per semplificare cloud toohello transizione.

[Altre informazioni](site-recovery-sharepoint.md) sulla protezione di SharePoint.

## <a name="protect-dynamics-ax"></a>Proteggere Dynamics AX
Azure Site Recovery consente di proteggere la soluzione ERP Dynamics AX. In particolare, è possibile:

* Orchestrazione di replica dell'intero ambiente Dynamics AX (livelli Web e AOS, SharePoint, livelli di database), tooAzure o tooa nel sito secondario.
* Allo scopo di semplificare la migrazione del cloud di toohello le distribuzioni di Dynamics AX (Azure).
* Semplificare lo sviluppo e il test dell'applicazione Dynamics AX creando una copia su richiesta simile a quella in produzione per il test e il debug.

[Altre informazioni](site-recovery-dynamicsax.md) sulla protezione di Dynamic AX.

## <a name="protect-rds"></a>Proteggere RDS
Servizi Desktop remoto (RDS) consente l'infrastruttura VDI (VDI), desktop basati su sessione e applicazioni, permettendo toowork gli utenti in qualsiasi punto. Con Azure Site Recovery è possibile:

* Replicare un sito secondario tooa di desktop virtuali in pool gestiti o non gestiti e le applicazioni e le sessioni tooa secondario del sito remoto o Azure.
* Ecco cosa è possibile replicare:

| **SERVIZI DESKTOP REMOTO** | **Replica macchine virtuali Hyper-V tooa del sito secondario** | **Replicare macchine virtuali Hyper-V tooAzure** | **Replica le macchine virtuali VMware tooa del sito secondario** | **Replicare le macchine virtuali VMware tooAzure** | **La replica del sito secondario di server fisici tooa** | **Replicare tooAzure server fisici** |
| --- | --- | --- | --- | --- | --- | --- |
| **Desktop virtuale in pool (non gestito)** |Sì |No |Sì |No |Sì |No |
| **Desktop virtuale in pool (gestito e senza UPD)** |Sì |No |Sì |No |Sì |No |
| **Applicazioni remote e le sessioni Desktop (senza UPD)** |Sì |Sì |Sì |Sì |Sì |Sì |

[Altre informazioni](https://gallery.technet.microsoft.com/Remote-Desktop-DR-Solution-bdf6ddcb) sulla protezione di RDS.

## <a name="protect-exchange"></a>Proteggere Exchange
Site Recovery consente di proteggere Exchange come segue:

* Per le distribuzioni di piccole dimensioni di Exchange, ad esempio un server singolo o autonomo, il ripristino del sito può replicare ed eseguire il failover tooAzure o tooa sito secondario.
* Per distribuzioni estese, Site Recovery si integra con i gruppi di disponibilità dei database di Exchange.
* DAG di Exchange sono hello consigliato soluzione per il ripristino di emergenza di Exchange in un'organizzazione.  I piani di ripristino di ripristino del sito possono includere DAG, tooorchestrate DAG failover tra siti.

[Altre informazioni](https://gallery.technet.microsoft.com/Exchange-DR-Solution-using-11a7dcb6) sulla protezione di Exchange.

## <a name="protect-sap"></a>Proteggere SAP
Utilizzare il ripristino del sito tooprotect la distribuzione di SAP, come segue:

* Abilitare la protezione di applicazioni SAP NetWeaver e non di produzione NetWeaver in esecuzione in locale, tramite la replica tooAzure componenti.
* Abilitare la protezione di applicazioni SAP NetWeaver e non di produzione NetWeaver in esecuzione di Azure, grazie alla replica tooanother componenti Data Center di Azure.
* Semplificare la migrazione di cloud, tramite il ripristino del sito toomigrate il tooAzure distribuzione SAP.
* Semplificare gli aggiornamenti, i test e la creazione di prototipi dei progetti SAP, creando un clone di produzione on demand per i test delle applicazioni SAP.

[Altre informazioni](site-recovery-sap.md) sulla protezione di SAP.

## <a name="protect-iis"></a>Proteggere IIS
Utilizzare il ripristino del sito tooprotect la distribuzione di IIS, come segue:

Azure Site Recovery consente il ripristino di emergenza mediante la replica componenti fondamentali di hello in ambiente tooa freddo sito remoto o un cloud pubblico, come Microsoft Azure. Macchina virtuale hello con server web hello e database hello vengono replicati toohello sito di ripristino, non è alcun file di configurazione toobackup requisito o certificati separatamente. Hello mapping applicazioni e le variabili di ambiente che vengono modificate post failover che dipendono dal binding può essere aggiornato tramite script integrato in piani di ripristino di emergenza hello. Macchine virtuali vengono attivate nel sito di ripristino hello solo nell'evento hello di un failover. Non solo a questo, Azure Site Recovery consente inoltre di orchestrare hello fine tooend failover fornendo che Hello seguenti funzionalità:

-   Sequenziazione hello chiusura e avvio delle macchine virtuali in hello vari livelli.
-   Aggiunta di aggiornamento tooallow script delle associazioni e le dipendenze dell'applicazione in macchine virtuali hello dopo l'avvio. gli script Hello possono inoltre essere utilizzati tooupdate hello DNS toopoint toohello ripristino sito del server di.
-   Allocare IP indirizzi toovirtual macchine pre-failover eseguendo il mapping delle reti di hello primario e di ripristino e quindi utilizzare gli script non è necessario failover post toobe aggiornato.
-   Possibilità per un failover di un solo clic per più applicazioni web nei server web hello, eliminando così ambito hello confusione nell'evento hello un'emergenza.
-   Capacità tootest hello i piani di ripristino in un ambiente isolato per drill di ripristino di emergenza.

[Altre informazioni](https://aka.ms/asr-iis) sulla protezione di una Web farm IIS.

## <a name="protect-citrix-xenapp-and-xendesktop"></a>Proteggere Citrix XenApp e XenDesktop
Utilizzare il ripristino del sito tooprotect le distribuzioni di Citrix XenApp e XenDesktop, come segue:

* L'abilitazione della protezione di hello Citrix XenApp e XenDesktop la distribuzione, mediante la replica di distribuzione diversi livelli inclusi (database di server DNS di Active Directory, SQL server, Citrix recapito Controller StoreFront server Master di informazioni (VDA), Server licenze di Citrix informazioni) tooAzure.
* Semplificare la migrazione di cloud, tramite il ripristino del sito toomigrate tooAzure la distribuzione Citrix XenApp e XenDesktop.
* Semplificare i test di Citrix XenApp/XenDesktop creando una copia su richiesta simile a quella di produzione per i test e il debug.
* Questa soluzione è applicabile solo per computer desktop virtuali con sistema operativo Windows Server e non per computer desktop virtuali client, poiché questi ultimi non sono ancora supportati per le licenze in Azure.
[Altre informazioni](https://azure.microsoft.com/pricing/licensing-faq/) sulle licenze per computer desktop client/server in Azure.

[Altre informazioni](site-recovery-citrix-xenapp-and-xendesktop.md) sulla protezione di distribuzioni Citrix XenApp e XenDesktop. In alternativa, è possibile fare riferimento di hello [white paper da Citrix](https://aka.ms/citrix-xenapp-xendesktop-with-asr) che riporta in dettaglio hello stesso.

## <a name="next-steps"></a>Passaggi successivi
[Verifica dei prerequisiti](site-recovery-prereq.md)
