---
title: architettura di hello aaaReview per VMware replica tooAzure | Documenti Microsoft
description: In questo articolo viene fornita una panoramica dei componenti e architettura utilizzata per la replica locale le macchine virtuali VMware tooAzure con hello servizio Azure Site Recovery
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
ms.topic: article
ms.date: 06/27.017
ms.author: raynew
ms.openlocfilehash: 7acb1d8e83a846dca79e175fd1af9324f2c31e65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-vmware-replication-tooazure"></a>Passaggio 1: Esaminare l'architettura di hello per tooAzure replica VMware

In questo articolo vengono descritti i componenti di hello e processi utilizzati quando la replica locale tooAzure di macchine virtuali VMware tramite hello [Azure Site Recovery](site-recovery-overview.md) servizio.

Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="architectural-components"></a>Componenti dell'architettura

tabella Hello vengono riepilogati i componenti di hello che è necessario.

**Componente** | **Requisito** | **Dettagli**
--- | --- | ---
**Azzurro** | Sono necessari una sottoscrizione di Azure, un account di archiviazione di Azure e una rete di Azure. | Dati replicati vengono archiviati nell'account di archiviazione hello. Macchine virtuali di Azure vengono create con i dati replicato hello quando si verifica il failover da sito locale. Hello macchine virtuali di Azure connettersi toohello rete virtuale di Azure quando vengono creati.
**Server di configurazione** | Un singolo server di gestione (VMware VM) che esegue i componenti di Site Recovery per la distribuzione di hello tutte hello in locale in locale. Sono inclusi un server di configurazione, un server di elaborazione e un server di destinazione master. | componente server di configurazione Hello coordina le comunicazioni tra sedi locali e Azure e gestisce la replica dei dati.
 **Server di elaborazione**  | Installato per impostazione predefinita nel server di configurazione hello. | Agisce come un gateway di replica. Riceve dati di replica, consente di ottimizzare con la memorizzazione nella cache, la compressione e crittografia e lo invia tooAzure archiviazione.<br/><br/> server di elaborazione Hello inoltre gestisce l'installazione push del computer tooprotected del servizio di mobilità hello ed esegue l'individuazione automatica delle macchine virtuali VMware.<br/><br/> Man mano che aumenta la distribuzione è possibile aggiungere ulteriori processo dedicato separato server toohandle aumentare i volumi di traffico di replica.
 **Server master di destinazione** | Installato per impostazione predefinita nel server di configurazione di on-premise hello. | Gestisce i dati di replica durante il failback da Azure.<br/><br/> Se i volumi del traffico di failback sono elevati, è possibile distribuire un server di destinazione master separato per il failback.
**Server VMware** | Le macchine virtuali VMware ospitate su server di vSphere ESXi, si consiglia un vCenter host hello toomanage di server. | Aggiungere un insieme di credenziali VMware server tooyour servizi di ripristino.
**Computer replicati** | servizio di mobilità Hello verrà installato in ogni VM VMware si esegue la replica. Può essere installato manualmente su ogni computer o con un'installazione push dal server di elaborazione hello.

**Figura 1: VMware tooAzure componenti**

![Componenti](./media/vmware-walkthrough-architecture/arch-enhanced.png)

## <a name="replication-process"></a>Processo di replica

1. Impostare la distribuzione di hello, inclusi i componenti di Azure e locali. Nell'insieme di credenziali con servizi di ripristino di hello specificare origine della replica hello e destinazione, configurare il server di configurazione di hello, creare un criterio di replica, distribuire il servizio di mobilità hello, abilitare la replica ed eseguire un failover di test.
2. Replicare macchine in base ai criteri di replica hello e una copia iniziale dei dati hello è archiviazione tooAzure replicati.
3. Al termine della replica iniziale, avvia la replica di tooAzure le modifiche delta. Le modifiche rilevate vengono salvate in un file HRL.
    - La replica macchine comunicano con server di configurazione hello sulla porta HTTPS 443 in entrata per la gestione della replica.
    - La replica macchine inviano server di elaborazione toohello dati di replica sulla porta HTTPS 9443 in ingresso (può essere modificato).
    - il server di configurazione di Hello Orchestra la gestione di replica in Azure tramite la porta HTTPS 443 in uscita.
    - server di elaborazione Hello riceve dati dal computer di origine, Ottimizza e crittografa e invia tooAzure archiviazione tramite la porta 443 in uscita.
    - Se si abilita la coerenza tra più macchine, quindi nel gruppo di replica hello macchine comunicano tra loro attraverso la porta 20004. La coerenza tra più VM viene usata se si raggruppano più computer in gruppi di replica che condividono punti di ripristino coerenti con l'arresto anomalo del sistema e coerenti con l'app quando si esegue il failover. Ciò è utile se sono in esecuzione macchine hello stesso carico di lavoro ed è necessario toobe coerente.
4. Il traffico è superiore all'endpoint pubblici di archiviazione replicata tooAzure, hello internet. In alternativa, è possibile usare il [peering pubblico](../expressroute/expressroute-circuit-peerings.md#public-peering) di Azure ExpressRoute. Non è supportata la replica del traffico tramite una VPN da sito a sito da un tooAzure sito locale.


**Figura 2: VMware tooAzure replica**

![Avanzato](./media/vmware-walkthrough-architecture/v2a-architecture-henry.png)

## <a name="failover-and-failback-process"></a>Processo di failover e failback

1. Dopo aver verificato che il failover di test funzioni come previsto, è possibile eseguire failover pianificati tooAzure come richiesto. Il failover pianificato non è supportato.
2. È possibile eseguire il failover a un singolo computer o creare [i piani di ripristino](site-recovery-create-recovery-plans.md), toofail in più macchine virtuali.
3. Quando si esegue un failover, vengono create VM di replica in Azure. Si esegue il commit di un failover toostart accesso hello carico di lavoro dalla replica hello macchina virtuale di Azure.
4. Quando il sito locale primario è di nuovo disponibile, è possibile effettuare il failback. Configurare un'infrastruttura di failback, avviare la replica macchina hello da hello del sito secondario toohello primario ed eseguire un failover non pianificato dal sito secondario hello. Dopo il commit, il failover dati sarà nascosto in locale e occorre tooenable replica tooAzure nuovamente. [Altre informazioni](site-recovery-failback-azure-to-vmware.md)

Esistono alcuni requisiti per il failback:


- **Server di elaborazione temporaneo in Azure**: se si desidera toofail da Azure dopo il failover sarà necessario tooset di una macchina virtuale di Azure configurato come un server di elaborazione, la replica toohandle da Azure. Questa VM può essere eliminata al termine del failback.
- **Connessione VPN**: per il failback, occorre una connessione VPN (o Azure ExpressRoute) imposta da hello Azure rete toohello nel sito locale.
- **Server di destinazione master locale separato**: server di destinazione master locale hello gestisce il failback. server di destinazione master Hello è installato per impostazione predefinita nel server di gestione di hello, ma se si sta riesce nuovamente più grandi volumi di traffico deve configurare un server di destinazione master locale separato per questo scopo.
- **Criteri di failback**: tooyour indietro tooreplicate sito locale, è necessario un criterio di failback. che viene creato automaticamente quando si crea il criterio di replica.
- **Infrastruttura VMware**: È necessario eseguire il failback tooan locale VM VMware. Il che richiede un'infrastruttura VMware in locale, anche se si esegue la replica tooAzure server fisici locali.

**Figura 3: Failback VMware/fisico**

![Failback](./media/vmware-walkthrough-architecture/enhanced-failback.png)


## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 2: verificare i prerequisiti e limitazioni](vmware-walkthrough-prerequisites.md)
