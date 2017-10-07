---
title: aaaHow funziona il ripristino del sito? | Microsoft Docs
description: Questo articolo offre una panoramica dell'architettura di Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 06/14/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-azure-to-azure-architecture
ms.openlocfilehash: ff1580d0fe294148dc0c621728491e6119c3048a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-site-recovery-work-for-on-premises-infrastructure"></a>Funzionamento di Azure Site Recovery per l'infrastruttura locale

> [!div class="op_single_selector"]
> * [Replicare le macchine virtuali di Azure](site-recovery-azure-to-azure-architecture.md)
> * [Replicare le macchine virtuali locali](site-recovery-components.md)

Questo articolo vengono descritti l'architettura sottostante di hello [Azure Site Recovery](site-recovery-overview.md) servizio e i componenti di hello che funzionano per replicare i carichi di lavoro da tooAzure locale.

Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="replicate-tooazure"></a>Replicare tooAzure

È possibile replicare e proteggere seguente hello nella tooAzure infrastruttura locale:

- **VMware**: macchine virtuali VMware locali in esecuzione in un [host supportato](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). È possibile replicare macchine virtuali VMware che eseguono i [sistemi operativi supportati](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions).
- **Hyper-V**: macchine virtuali Hyper-V locali in esecuzione negli [host supportati](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- **Macchine fisiche**: server fisici locali che eseguono Windows o Linux nei [sistemi operativi supportati](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions). È possibile replicare macchine virtuali Hyper-V che eseguono qualsiasi sistema operativo guest [supportato da Hyper-V e Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).

## <a name="vmware-tooazure"></a>VMware tooAzure

Ecco cosa occorre per la replica tooAzure le macchine virtuali VMware.

Area | Componente | Dettagli
--- | --- | ---
**Server di configurazione** | Un singolo server di gestione (VM VMWare) esegue tutti i componenti locali: server di configurazione, server di elaborazione, server master di destinazione. | il server di configurazione di Hello coordina le comunicazioni tra sedi locali e Azure e gestisce la replica dei dati.
 **Server di elaborazione**  | Installato per impostazione predefinita nel server di configurazione hello. | Agisce come un gateway di replica. Riceve dati di replica, consente di ottimizzare con la memorizzazione nella cache, la compressione e crittografia e lo invia tooAzure archiviazione.<br/><br/> server di elaborazione Hello inoltre gestisce l'installazione push del computer tooprotected del servizio di mobilità hello ed esegue l'individuazione automatica delle macchine virtuali VMware.<br/><br/> Man mano che aumenta la distribuzione è possibile aggiungere ulteriori processo dedicato separato server toohandle aumentare i volumi di traffico di replica.
 **Server master di destinazione** | Installato per impostazione predefinita nel server di configurazione di on-premise hello. | Gestisce i dati di replica durante il failback da Azure.<br/><br/> Se i volumi del traffico di failback sono elevati, è possibile distribuire un server di destinazione master separato per il failback.
**Server VMware** | Le macchine virtuali VMware ospitate su server di vSphere ESXi, si consiglia un vCenter host hello toomanage di server. | Aggiungere un insieme di credenziali VMware server tooyour servizi di ripristino.<br/><br/>
**Computer replicati** | servizio di mobilità Hello verrà installato in ogni macchina virtuale che si desidera tooreplicate VMware. Può essere installato manualmente su ogni computer o con un'installazione push dal server di elaborazione hello.| -

**Figura 1: VMware tooAzure componenti**

![Componenti](./media/site-recovery-components/arch-enhanced.png)

### <a name="replication-process"></a>Processo di replica

1. Impostare la distribuzione di hello, inclusi i componenti di Azure e un insieme di credenziali di servizi di ripristino. Nell'insieme di credenziali hello specificare origine della replica hello e destinazione, configurare il server di configurazione di hello, aggiungere server VMware, creare un criterio di replica, distribuire il servizio di mobilità hello, abilitare la replica ed eseguire un failover di test.
2.  Macchine avviare la replica in base ai criteri di replica hello e una copia iniziale dei dati hello è archiviazione tooAzure replicati.
4. Replica di tooAzure le modifiche delta inizia dopo il completamento della replica iniziale hello. Le modifiche rilevate vengono salvate in un file HRL.
    - La replica macchine comunicano con server di configurazione hello sulla porta HTTPS 443 in entrata per la gestione della replica.
    - La replica macchine inviano server di elaborazione toohello dati di replica sulla porta HTTPS 9443 in ingresso (può essere configurato).
    - il server di configurazione di Hello Orchestra la gestione di replica in Azure tramite la porta HTTPS 443 in uscita.
    - server di elaborazione Hello riceve dati dal computer di origine, Ottimizza e crittografa e invia tooAzure archiviazione tramite la porta 443 in uscita.
    - Se si abilita la coerenza tra più macchine, quindi nel gruppo di replica hello macchine comunicano tra loro attraverso la porta 20004. La coerenza tra più VM viene usata se si raggruppano più computer in gruppi di replica che condividono punti di ripristino coerenti con l'arresto anomalo del sistema e coerenti con l'app quando si esegue il failover. Ciò è utile se sono in esecuzione macchine hello stesso carico di lavoro ed è necessario toobe coerente.
5. Il traffico è superiore all'endpoint pubblici di archiviazione replicata tooAzure, hello internet. In alternativa, è possibile usare il [peering pubblico](https://docs.microsoft.com/en-us/azure/expressroute/expressroute-circuit-peerings#public-peering) di Azure ExpressRoute. Non è supportata la replica del traffico tramite una VPN da sito a sito da un tooAzure sito locale.

**Figura 2: VMware tooAzure replica**

![Avanzato](./media/site-recovery-components/v2a-architecture-henry.png)

### <a name="failover-and-failback"></a>Failover e failback

1. Dopo aver verificato che il failover di test funzioni come previsto, è possibile eseguire failover pianificati tooAzure come richiesto. Il failover pianificato non è supportato.
2. È possibile eseguire il failover a un singolo computer o creare [i piani di ripristino](site-recovery-create-recovery-plans.md), toofail in più macchine virtuali.
3. Quando si esegue un failover, vengono create VM di replica in Azure. Si esegue il commit di un failover toostart accesso hello carico di lavoro dalla replica hello macchina virtuale di Azure.
4. Quando il sito locale primario è di nuovo disponibile, è possibile effettuare il failback. Configurare un'infrastruttura di failback, avviare la replica macchina hello da hello del sito secondario toohello primario ed eseguire un failover non pianificato dal sito secondario hello. Dopo il commit, il failover dati sarà nascosto in locale e occorre tooenable replica tooAzure nuovamente. [Altre informazioni](site-recovery-failback-azure-to-vmware.md)

**Figura 3: Failback VMware/fisico**

![Failback](./media/site-recovery-components/enhanced-failback.png)

## <a name="physical-tooazure"></a>TooAzure fisico

Quando si esegue la replica tooAzure server fisico locale, utilizzato nella replica hello anche componenti e i processi [tooAzure VMware](#vmware-replication-to-azure), ma Tieni presente queste differenze:

- È possibile utilizzare un server fisico per i server di configurazione hello, anziché una VM VMware
- Sarà necessaria un'infrastruttura VMware locale per il failback. È possibile eseguire il computer fisico tooa indietro.

## <a name="hyper-v-tooazure"></a>TooAzure Hyper-V

### <a name="replication-process"></a>Processo di replica

1. Impostare hello componenti di Azure. È consigliabile configurare gli account di archiviazione e di rete prima di iniziare la distribuzione di Site Recovery.
2. Si crea un insieme di credenziali dei servizi di replica per Site Recovery e si configurano le impostazioni dell'insieme di credenziali, tra cui:
    - Impostazioni di origine e di destinazione. Se non si gestiscono gli host Hyper-V in un cloud VMM, per la destinazione di hello creare un contenitore di Hyper-V del sito e aggiungere tooit gli host Hyper-V. Se l'host Hyper-V vengono gestite in VMM, origine hello è cloud VMM hello. destinazione Hello è Azure.
    - Installazione del Provider di Azure Site Recovery hello e dell'agente di servizi di ripristino di Microsoft Azure hello. Se si dispone di hello VMM verrà installato su di esso, Provider e hello agente in ogni host Hyper-V. Se non si dispone di VMM, hello Provider sia agente vengono installati in ogni host.
    - Creare un criterio di replica per il sito di Hyper-V hello o il cloud VMM. criteri di Hello sono macchine virtuali tooall applicato presenti negli host nel sito di hello o cloud.
    - Si abilita la replica per le VM Hyper-V. Viene eseguita la replica iniziale in base alle impostazioni di criteri di replica hello.
4. Vengono rilevate le modifiche ai dati e la replica di tooAzure le modifiche delta inizia dopo il completamento della replica iniziale hello. Le modifiche rilevate per un elemento vengono salvate in un file HRL.
5. Eseguire un toomake di failover di test che funzionino.

### <a name="failover-and-failback-process"></a>Processo di failover e failback

1. È possibile eseguire un pianificato o non pianificato [failover](site-recovery-failover.md) da tooAzure macchine virtuali Hyper-V locale. Se si esegue un failover pianificato, quindi le macchine virtuali di origine vengono arrestate tooensure senza perdita di dati.
2. È possibile eseguire il failover a un singolo computer o creare [i piani di ripristino](site-recovery-create-recovery-plans.md) tooorchestrate failover di più macchine.
4. Dopo aver eseguito il failover hello, si dovrebbe essere hello toosee in grado di creare macchine virtuali di replica in Azure. Se necessario, è possibile assegnare un toohello di indirizzo IP pubblico macchina virtuale.
5. È quindi eseguire il commit hello failover toostart l'accesso a carico di lavoro hello dalla replica hello macchina virtuale di Azure.
6. Quando il sito locale primario è di nuovo disponibile, è possibile [effettuare il failback](site-recovery-failback-from-azure-to-hyper-v.md). Avviare un failover pianificato da Azure toohello primario di sito. Per un failover pianificato, che è possibile selezionare toofailback toohello stessa macchina virtuale o tooan percorso alternativo e sincronizzare le modifiche tra Azure e locali, tooensure senza perdita di dati. Creazione di macchine virtuali in locale, si esegue il commit hello failover.

**Figura 4: Replica di tooAzure siti Hyper-V**

![Componenti](./media/site-recovery-components/arch-onprem-azure-hypervsite.png)

**Figura 5: Replica tooAzure di cloud di Hyper-V in VMM**

![Componenti](./media/site-recovery-components/arch-onprem-onprem-azure-vmm.png)


## <a name="replicate-tooa-secondary-site"></a>La replica del sito secondario tooa

È possibile replicare hello sito secondario tooyour seguente:

- **VMware**: macchine virtuali VMware locali in esecuzione in un [host supportato](site-recovery-support-matrix-to-sec-site.md#on-premises-servers). È possibile replicare macchine virtuali VMware che eseguono i [sistemi operativi supportati](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions).
- **Macchine fisiche**: server fisici locali che eseguono Windows o Linux nei [sistemi operativi supportati](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions).
- **Hyper-V**: macchine virtuali Hyper-V locali in esecuzione negli [host Hyper-V supportati](site-recovery-support-matrix-to-sec-site.md#on-premises-servers) gestiti in cloud VMM. [host supportati](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers). È possibile replicare macchine virtuali Hyper-V che eseguono qualsiasi sistema operativo guest [supportato da Hyper-V e Azure](https://technet.microsoft.com/en-us/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows).


## <a name="vmwarephysical-tooa-secondary-site"></a>Sito secondario di VMware/fisici tooa

Replicare le macchine virtuali VMware o il sito secondario di server fisici tooa utilizzando InMage Scout.

### <a name="components"></a>Componenti

**Area** | **Componente** | **Dettagli**
--- | --- | ---
**Server di elaborazione** | Situato nel sito primario | Distribuire la memorizzazione nella cache di hello processo server toohandle, compressione e l'ottimizzazione di dati.<br/><br/> Gestisce inoltre l'installazione push dell'agente unificata toomachines desiderato tooprotect hello.
**Server di configurazione** | Situato nel sito secondario | gestisce il server di configurazione di Hello, configurare e monitorare la distribuzione, ovvero tramite il sito Web management hello o console vContinuum hello.
**Server vContinuum** | Facoltativo. Installato in hello stesso percorso del server di configurazione hello. | Fornisce una console per la gestione e il monitoraggio dell'ambiente protetto.
**Server master di destinazione** | Si trova nel sito secondario hello | server di destinazione master Hello contiene i dati replicati. Riceve dati dal server di elaborazione hello, crea una macchina di replica nel sito secondario hello e contiene i punti di conservazione dati hello.<br/><br/> numero di Hello del server di destinazione master che è necessario dipende dal numero di hello che si proteggono macchine.<br/><br/> Se si desidera toofail toohello indietro primario di sito, è necessario un server di destinazione master sono troppo. Hello unificata agente è installato in questo server.
**Server VMware ESX/ESXi e vCenter** |  Le macchine virtuali sono ospitate in host ESX/ESXi. Gli host vengono gestiti con un server vCenter. | È necessario un tooreplicate infrastruttura VMware le macchine virtuali VMware.
**VM/server fisici** |  Unificata agente installato in macchine virtuali VMware e server fisici che si desidera tooreplicate. | agente Hello funge da un provider di comunicazione tra tutti i componenti di hello.


### <a name="replication-process"></a>Processo di replica

1. Si impostare i server del componente hello in ogni sito (processo di configurazione, la destinazione master) e installa hello agente unificato in un computer che si desidera tooreplicate.
2. Dopo la replica iniziale, hello agente in ogni computer invia i server di elaborazione toohello delta della replica delle modifiche.
3. server di elaborazione Hello Ottimizza dati hello e trasferisce i server di destinazione master toohello nel sito secondario hello. il server di configurazione di Hello gestisce il processo di replica hello.

**Figura 6: VMware tooVMware replica**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)



## <a name="hyper-v-tooa-secondary-site"></a>Sito secondario tooa Hyper-V

Ecco cosa occorre per la replica del sito secondario tooa di macchine virtuali Hyper-V.


**Area** | **Componente** | **Dettagli**
--- | --- | ---
**Server VMM** | Si consiglia di un server VMM nel sito primario di hello e uno nel sito secondario hello | Ogni server VMM deve essere connesso toohello internet.<br/><br/> Ogni server deve disporre di almeno un cloud privato VMM, con set di profili di capacità hello Hyper-V.<br/><br/> Installare hello Provider di Azure Site Recovery nel server VMM hello. coordinate Hello Provider e Orchestra la replica con hello servizio Site Recovery su hello internet. Le comunicazioni tra Provider hello e Azure sono protetto e crittografato.
**Server Hyper-V** |  Uno o più server Hyper-V host nei cloud VMM primario e secondario di hello.<br/><br/> I server devono essere connesso toohello internet.<br/><br/> Dati vengono replicati tra hello server primario e secondario Hyper-V host su hello LAN o VPN, utilizzando l'autenticazione Kerberos o certificati.  
**VM Hyper-V** | Si trova nel server host Hyper-V di origine hello. | server host di origine Hello deve avere almeno una macchina virtuale che si desidera tooreplicate.

### <a name="replication-process"></a>Processo di replica

1. Impostare hello account Azure.
2. Si crea un insieme di credenziali dei servizi di replica per Site Recovery e si configurano le impostazioni dell'insieme di credenziali, tra cui:

    - origine della replica Hello e destinazione (siti primari e secondari).
    - Installazione del Provider di Azure Site Recovery hello e dell'agente di servizi di ripristino di Microsoft Azure hello. Hello Provider è installato nel server VMM e hello agente in ogni host Hyper-V.
    - Si crea un criterio di replica per il cloud VMM di origine. criteri di Hello sono applicato tooall macchine virtuali presenti negli host nel cloud hello.
    - Si abilita la replica per le VM Hyper-V. Viene eseguita la replica iniziale in base alle impostazioni di criteri di replica hello.
4. Vengono rilevate le modifiche ai dati e la replica del delta cambia toobegins dopo il completamento della replica iniziale hello. Le modifiche rilevate per un elemento vengono salvate in un file HRL.
5. Eseguire un toomake di failover di test che funzionino.

**Figura 7: La replica tooVMM VMM**

![Tooon tra più sedi locali](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback"></a>Failover e failback

1. È possibile eseguire un [failover](site-recovery-failover.md) pianificato o non pianificato tra siti locali. Se si esegue un failover pianificato, quindi le macchine virtuali di origine vengono arrestate tooensure senza perdita di dati.
2. È possibile eseguire il failover a un singolo computer o creare [i piani di ripristino](site-recovery-create-recovery-plans.md) tooorchestrate failover di più macchine.
4. Se si esegue un failover non pianificato tooa sito secondario, dopo il failover delle macchine hello nella posizione secondaria hello non sono abilitati per la replica o di protezione. Se si esegue un failover pianificato, dopo il failover hello, le macchine in posizione secondaria hello sono protetti.
5. Quindi, si esegue il commit hello failover toostart accesso hello del carico di lavoro dalla replica hello macchina virtuale.
6. Quando il sito primario è nuovamente disponibile, si avvia tooreplicate replica inversa da hello del sito secondario toohello primario. La replica inversa porta hello le macchine virtuali in uno stato protetto, ma Data Center secondario hello è ancora percorso attivo hello.
7. sito primario di hello toomake nel percorso active hello, si avvia nuovamente un failover pianificato da tooprimary secondario, seguita da un'altra replica inversa.


## <a name="next-steps"></a>Passaggi successivi

- [Altre informazioni](site-recovery-hyper-v-azure-architecture.md) sul flusso di lavoro replica hello Hyper-V.
- [Controllare i prerequisiti](site-recovery-prereq.md)
