---
title: aaaHow funziona locale macchina replica tooa locale secondario del sito in Azure Site Recovery? | Microsoft Docs
description: In questo articolo viene fornita una panoramica dei componenti e architettura utilizzata quando la replica locale macchine virtuali e il sito secondario di server fisici tooa con hello servizio Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 05/29/2017
ms.author: raynew
ms.openlocfilehash: 097a3f43446fec69ed7f9e0b7f11e8d11f41cc6a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-on-premises-machine-replication-tooa-secondary-site-work-in-site-recovery"></a>Modalità locale computer lavoro del sito secondario tooa di replica in Site Recovery?

Questo articolo vengono descritti i componenti di hello e processi per la replica locale macchine virtuali e server fisici tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) servizio.

È possibile replicare hello tooa locale secondario sito seguente:
- Macchine virtuali Hyper-V locali, macchine virtuali Hyper-V in cluster Hyper-V e host autonomi gestiti nei cloud System Center Virtual Machine Manager (VMM).
- Macchine virtuali VMware locali e server fisici Windows/Linux. In questo scenario la replica è gestita da Scout.

Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="replicate-hyper-v-vms-tooa-secondary-on-premises-site"></a>Replicare macchine virtuali Hyper-V tooa secondario nel sito locale


### <a name="architectural-components"></a>Componenti dell'architettura

Ecco cosa occorre per la replica del sito secondario tooa di macchine virtuali Hyper-V.

**Componente** | **Posizione** | **Dettagli**
--- | --- | ---
**Azzurro** | È necessario un account Microsoft. |
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

**Figura 1: La replica tooVMM VMM**

![Tooon tra più sedi locali](./media/site-recovery-components/arch-onprem-onprem.png)

### <a name="failover-and-failback-process"></a>Processo di failover e failback

1. È possibile eseguire un [failover](site-recovery-failover.md) pianificato o non pianificato tra siti locali. Se si esegue un failover pianificato, quindi le macchine virtuali di origine vengono arrestate tooensure senza perdita di dati.
2. È possibile eseguire il failover a un singolo computer o creare [i piani di ripristino](site-recovery-create-recovery-plans.md) tooorchestrate failover di più macchine.
4. Se si esegue un failover non pianificato tooa sito secondario, dopo il failover delle macchine hello nella posizione secondaria hello non sono abilitati per la replica o di protezione. Se si esegue un failover pianificato, dopo il failover hello, le macchine in posizione secondaria hello sono protetti.
5. Quindi, si esegue il commit hello failover toostart accesso hello del carico di lavoro dalla replica hello macchina virtuale.
6. Quando il sito primario è nuovamente disponibile, si avvia tooreplicate replica inversa da hello del sito secondario toohello primario. La replica inversa porta hello le macchine virtuali in uno stato protetto, ma Data Center secondario hello è ancora percorso attivo hello.
7. sito primario di hello toomake nel percorso active hello, si avvia nuovamente un failover pianificato da tooprimary secondario, seguita da un'altra replica inversa.




## <a name="replicate-vmware-vmsphysical-servers-tooa-secondary-site"></a>Replicare le macchine virtuali VMware/fisici server tooa sito secondario

Replicare le macchine virtuali VMware o il sito secondario di server fisici tooa utilizzando InMage Scout, utilizzo di questi componenti dell'architettura:


### <a name="architectural-components"></a>Componenti dell'architettura

**Componente** | **Posizione** | **Dettagli**
--- | --- | ---
**Azzurro** | InMage Scout | tooobtain InMage Scout è necessaria una sottoscrizione di Azure.<br/><br/> Dopo aver creato un insieme di credenziali di servizi di ripristino, scaricare InMage Scout e installare tooset gli aggiornamenti più recenti di hello distribuzione hello.
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

**Figura 2: VMware tooVMware replica**

![VMware tooVMware](./media/site-recovery-components/vmware-to-vmware.png)


## <a name="next-steps"></a>Passaggi successivi

Hello revisione [matrice del supporto](site-recovery-support-matrix-to-sec-site.md)
