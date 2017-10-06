---
title: procedure consigliate per il ripristino del sito aaaAzure | Documenti Microsoft
description: Questo articolo illustra le procedure consigliate per la distribuzione di Azure Site Recovery
services: site-recovery
documentationCenter: 
author: rayne-wiselman"
manager: cfreeman
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-support-matrix-to-azure
ms.openlocfilehash: 288df858a0e1c1f5ad96dbe8b9dd0dc69d8f56ae
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-ready-toodeploy-azure-site-recovery"></a>Ottenere toodeploy pronto Azure Site Recovery

Questo articolo viene descritto come tooprepare per la distribuzione di Azure Site Recovery.

## <a name="protecting-hyper-v-virtual-machines"></a>Protezione di macchine virtuali Hyper-V

Per proteggere le macchine virtuali Hyper-V, sono disponibili due scelte a livello di distribuzione. È possibile replicare locale macchine virtuali Hyper tooAzure o Data Center secondario tooa. Esistono requisiti diversi per ogni distribuzione.

**Requisito** | **Replicare tooAzure (con VMM)** | **Replicare macchine virtuali Hyper-V tooAzure (senza VMM)** | **Replicare macchine virtuali Hyper-V toosecondary sito (con VMM)** | **Dettagli**
---|---|---|---|---
**VMM** | VMM in esecuzione su System Center 2012 R2. <br/><br/>Almeno un cloud VMM contenente uno o più gruppi host VMM. | ND | Server VMM in siti primari e secondari hello in esecuzione almeno su System Center 2012 SP1 con gli aggiornamenti più recenti. <br/><br/> Almeno un cloud in ogni server VMM. Cloud devono avere profilo capacità di Hyper-V hello set.<br/><br/> cloud di origine Hello deve avere almeno un gruppo host VMM. | Facoltativo. Non è necessario System Center VMM è distribuito in ordine tooreplicate Hyper-V le macchine virtuali tooAzure toohave ma se è necessario toomake che il server VMM hello sia impostato correttamente. Che include assicurandosi che si esegue versione di VMM corretta hello e che siano impostati cloud.
**Hyper-V** | Almeno un server host di Hyper-V nel sito locale hello in esecuzione Windows Server 2012 R2 o versioni successive | Almeno un server Hyper-V in siti di origine e destinazione di hello in esecuzione almeno Windows Server 2012 con gli aggiornamenti più recenti di hello installato e connesso toohello internet.<br/><br/> server Hyper-V Hello deve essere in un gruppo host in un cloud VMM. | Almeno un server Hyper-V in siti di origine e destinazione di hello in esecuzione almeno Windows Server 2012 con gli aggiornamenti più recenti di hello installato e connesso toohello internet.<br/><br/> server Hyper-V Hello deve trovarsi in un gruppo host in un cloud VMM. |
**Macchine virtuali** | Almeno una macchina virtuale nel server host Hyper-V di origine di hello | Almeno una macchina virtuale nel server host Hyper-V hello in origine hello cloud VMM | Almeno una macchina virtuale nel server host Hyper-V hello in origine hello cloud VMM. |  Macchine virtuali di replica tooAzure devono essere conforme con i prerequisiti di macchina virtuale di Azure
**Account di Azure** | È necessario un account Azure e un toohello sottoscrizione servizio Site Recovery. | È necessario un account Azure e un toohello sottoscrizione servizio Site Recovery. | ND | Nel caso in cui non sia disponibile un account, iniziare con una versione di valutazione gratuita.
**Archiviazione di Azure** | È necessaria una sottoscrizione per un account di archiviazione di Azure con la replica geografica abilitata. | È necessaria una sottoscrizione per un account di archiviazione di Azure con la replica geografica abilitata. | ND | account di Hello deve essere nella stessa area dell'insieme di credenziali di Azure Site Recovery hello hello e associato hello stessa sottoscrizione.
**Rete** | Configurare la rete mapping tooensure che tutti i computer che il failover su hello stessa rete di Azure può connettersi tooeach altri, indipendentemente dal piano di ripristino si trovano in. Inoltre se un gateway di rete è configurata nella destinazione hello rete di Azure, le macchine virtuali possono connettersi le macchine virtuali locali tooother. Se non si imposta rete mapping solo le macchine che il failover in hello stesso piano di ripristino può connettersi. | ND |  <br/><br/>Consente di impostare tooensure mapping di rete che le macchine virtuali sono connesse tooappropriate reti dopo il failover e che le macchine virtuali di replica vengono posizionate in server host Hyper-V. Se non si configura rete mapping macchine replicate sarà rete VM tooany connesse dopo il failover. |  tooset mapping di rete con VMM, occorre toomake verificare che VMM logiche e reti VM siano configurate correttamente.
**Provider e agenti** | Durante la distribuzione verrà installato hello Provider di Azure Site Recovery nei server VMM. Installare l'agente di servizi di ripristino di Azure hello nei server Hyper-V nei cloud VMM. | Durante la distribuzione verrà installato sia hello Provider di Azure Site Recovery e l'agente di servizi di ripristino di Azure hello in hello Hyper-V server o cluster host| Durante la distribuzione verrà installato hello Provider di Azure Site Recovery nei server VMM. Installare l'agente di servizi di ripristino di Azure hello nei server Hyper-V nei cloud VMM. | Provider e gli agenti si connettono tooSite ripristino su hello internet mediante una connessione HTTPS crittografata. Non necessario tooadd le eccezioni del firewall o creare un proxy specifico per la connessione al Provider di hello.
**Connettività Internet** | Solo i server VMM di hello è necessaria una connessione internet | Solo server di host Hyper-V hello è necessaria una connessione internet | La connessione Internet è necessaria solo per i server VMM. | Macchine virtuali non più necessario qualsiasi componente installato su di essi e non connettere direttamente toohello internet.



## <a name="protect-vmware-virtual-machines-or-physical-servers"></a>Proteggere macchine virtuali VMware o server fisici

Per proteggere le macchine virtuali VMware o i server fisici Windows/Linux, sono disponibili due scelte a livello di distribuzione. È possibile replicare le tooAzure o Data Center secondario tooa. Esistono requisiti diversi per ogni distribuzione.

**Requisito** | **TooAzure server VMware replicare le macchine virtuali o fisici)** | * **Replicare le macchine virtuali VMware/fisici server toosecondary sito**  
---|---|---
**Sito primario** | **Server di elaborazione**: server Windows dedicato, fisico o virtuale. | **Server di elaborazione**: server Windows dedicato, fisico o VM VMware.<br/><br/>  
**Sito locale secondario** | ND | **Server di configurazione**: server Windows dedicato, fisico o virtuale. <br/><br/> **Server di destinazione master**: server dedicato, fisico o virtuale. Configurare con i computer Windows tooprotect Windows o Linux tooprotect Linux.
**Azzurro** | **Sottoscrizione**: È necessario un abbonamento per hello servizio Site Recovery. <br/><br/> **Account di archiviazione**: è necessario un account di archiviazione con la replica geografica abilitata. account di Hello deve essere nella stessa area dell'insieme di credenziali di Site Recovery hello hello e associato hello stessa sottoscrizione. <br/><br/> **Server di configurazione**: È necessario tooset di server di configurazione hello come una macchina virtuale di Azure <br/><br/> **Server di destinazione master**: È necessario tooset di server di destinazione master hello come una macchina virtuale di Azure <br/><br/> Configurare con i computer Windows tooprotect Windows o Linux tooprotect Linux.<br/><br/> **Rete virtuale di Azure**: È necessario che una rete virtuale di Azure in cui hello verrà distribuiti il server di configurazione e il server di destinazione master. Dovrebbe essere hello stessa sottoscrizione e area geografica dell'insieme di credenziali di Azure Site Recovery hello | ND  
**Macchine virtuali/server fisici** | Almeno una macchina virtuale VMware o un server fisico Windows/Linux.<br/><br/>Durante la distribuzione verrà installato in ogni computer hello servizio di mobilità| Almeno una VM VMware o un server fisico Windows/Linux.<br/><br/> Durante la distribuzione dell'agente unificato hello è installato in ogni computer.




## <a name="azure-virtual-machine-requirements"></a>Requisiti delle macchine virtuali di Azure

È possibile distribuire macchine virtuali di tooreplicate il ripristino del sito e server fisici che eseguono un sistema operativo supportato da Azure. vale a dire la maggior parte delle versioni di Windows e Linux. Sarà necessario toomake assicurarsi che le macchine virtuali che si desidera tooprotect conforme ai requisiti di Azure in locale.


## <a name="optimizing-your-deployment"></a>Ottimizzazione della distribuzione

Utilizzare hello seguente toohelp suggerimenti è ottimizzare e ridimensionare la distribuzione.

- **Dimensioni volume del sistema operativo**: quando si esegue la replica hello di tooAzure una macchina virtuale volume del sistema operativo deve essere minore di 1 TB. Se si dispone di più volumi rispetto ai ciò è possibile spostarli manualmente in tooa altro disco prima di iniziare la distribuzione.
- **Dimensioni del disco dati**: se si esegue la replica tooAzure possono esistere fino a too32 dischi di dati in una macchina virtuale, ognuna con un massimo di 1 TB. È possibile replicare in modo efficiente una macchina virtuale di ~32 TB ed eseguirne il failover.
- **I limiti di piano di ripristino**: il ripristino del sito possono essere ridimensionati toothousands delle macchine virtuali. I piani di ripristino sono progettati come un modello per le applicazioni che devono si verifica il failover in modo, è necessario limitare il numero di hello macchine in un too50 piano di ripristino.
- **Limiti dei servizi di Azure**: ogni sottoscrizione di Azure include un set di limiti predefiniti su core, servizi cloud e così via. È consigliabile eseguire una test di failover toovalidate hello la disponibilità delle risorse nella sottoscrizione. È possibile modificare questi limiti tramite il supporto di Azure.
- **Pianificazione della capacità**: pianificare la scalabilità e le prestazioni.
- **Larghezza di banda della replica**: in caso di larghezza di banda insufficiente, è opportuno notare quanto indicato di seguito.
    - **ExpressRoute**: Site Recovery funziona con Azure ExpressRoute e con gli ottimizzatori WAN, ad esempio Riverbed.
    - **Il traffico di replica**: utilizza il ripristino del sito esegue una replica iniziale smart utilizzando solo i blocchi di dati e non hello intero disco rigido virtuale. Solo le modifiche vengono replicate durante la replica in corso.
    - **Il traffico di rete**: È possibile controllare il traffico di rete utilizzato per la replica mediante la configurazione di QoS di Windows con un criterio basato su porta e indirizzo IP di destinazione hello.  Inoltre, se si esegue la replica tooAzure Site Recovery tramite hello Azure Backup agent. è possibile configurare la limitazione per tale agente.
- **RTO**: se si desidera toomeasure hello obiettivo tempo di ripristino (RTO) è possibile prevedere con il ripristino del sito è consigliabile eseguire un failover di test e visualizzazione tooanalyze i processi di Site Recovery hello il tempo accetta toocomplete operazioni hello. Se esegue il failover tooAzure, per hello piani RTO migliori è consigliabile automatizzare tutte le azioni manuali grazie all'integrazione con l'automazione di Azure e di ripristino.
- **RPO**: il ripristino del sito supporta un obiettivo del punto di ripristino quasi sincrono (RPO) quando si esegue la replica tooAzure. Ciò presuppone sufficiente larghezza di banda tra il datacenter e Azure.
