---
title: aaaSet di VMM e Hyper-V per il sito secondario di replica tooa con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come tooset dei server di System Center VMM e host Hyper-V per il sito di replica tooa secondario VMM.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d0389e3b-3737-496c-bda6-77152264dd98
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 677bf6d38328ccc425e3b0f056d03159a52da428
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-4-set-up-vmm-and-hyper-v-for-hyper-v-vm-replication-tooa-secondary-site"></a>Passaggio 4: Configurazione di VMM e Hyper-V per il sito secondario di macchina virtuale Hyper-V replica tooa 

Dopo che è stata preparata per la rete, configurare il server di System Center Virtual Machine Manager (VMM) e gli host Hyper-V per Hyper-V macchina virtuale (VM) replica tooa sito secondario, utilizzando [Azure Site Recovery](site-recovery-overview.md) in hello portale di Azure. 

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).



## <a name="prepare-vmm-servers"></a>Preparare i server VMM 

tooprepare per la distribuzione:


1. Verificare che il server VMM è conforme con hello [supportare requisiti](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), e [prerequisiti di distribuzione](vmm-to-vmm-walkthrough-prerequisites.md).
2. Verificare che il server VMM siano connesso toohello internet e dispone di accesso toothese URL.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.
    - Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).
    - Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).
3. Assicurarsi che sia il server VMM hello [preparati per il mapping di rete](vmm-to-vmm-walkthrough-network.md#prepare-for-network-mapping)


## <a name="prepare-hyper-v-hostsclusters"></a>Preparare gli host/cluster Hyper-V

1. Assicurarsi che gli host o cluster Hyper-V conformarsi hello [supportare requisiti](site-recovery-support-matrix-to-sec-site.md#on-premises-servers), e [prerequisiti di distribuzione](vmm-to-vmm-walkthrough-prerequisites.md).
2. Verificare i requisiti di hello per [macchine virtuali Hyper-V](site-recovery-support-matrix-to-sec-site.md#support-for-replicated-machine-os-versions)
3. Verificare i requisiti di [rete](site-recovery-support-matrix-to-sec-site.md#network-configuration) e [archiviazione](site-recovery-support-matrix-to-sec-site.md#storage).
4. Verificare che gli host Hyper-V siano connesso toohello internet e dispone di accesso toothese URL.
    
    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
    - Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.
    - Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).
    - Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).

## <a name="prepare-for-single-server-deployment"></a>Prepararsi per una distribuzione a server singolo


Se si dispone solo di un singolo server VMM, è possibile replicare le macchine virtuali in host Hyper-V nel cloud VMM hello troppo[Azure](hyper-v-site-walkthrough-overview.md) o tooa secondario cloud VMM, come descritto in questo documento. È consigliabile prima opzione hello perché la replica tra cloud non è trasparente.

Se si desidera tooreplicate tra cloud, è possibile replicare un server VMM singolo autonomo o con un singolo server VMM distribuito in un cluster di Windows con estensione

### <a name="replicate-with-a-standalone-vmm-server"></a>Eseguire la replica con un server VMM autonomo

In questo scenario, la distribuzione di server VMM singolo hello come una macchina virtuale nel sito primario di hello e replicare il sito secondario tooa VM utilizzando il ripristino del sito e Replica Hyper-V.

1. **Configurare VMM in una VM Hyper-V**. Si consiglia di condivisione percorso di istanza di SQL Server hello utilizzato da VMM in hello stessa macchina virtuale. Ciò consente di risparmiare tempo come solo una macchina virtuale ha toobe creato. Se si desidera toouse istanza remota di SQL Server e si verifica un'interruzione, è necessario toorecover quell'istanza prima di poter ripristinare VMM.
2. **Verificare che il server VMM hello disponga di almeno due cloud configurato**. Un cloud contiene macchine virtuali desiderate tooreplicate e hello altri cloud verranno utilizzata come posizione secondaria hello hello. Hello cloud che si desidera tooprotect devono essere conformi alle macchine virtuali di hello contiene [prerequisiti](#prerequisites).
3. Configurare Site Recovery come descritto in questo articolo. Creare e registrare il server VMM hello in un insieme di credenziali, impostare un criterio di replica e abilitare la replica. nomi di VMM di origine e destinazione Hello verrà essere hello stesso. Specificare che la replica iniziale viene effettuata tramite rete hello.
4. Quando si configura il mapping di rete eseguire il mapping di rete VM hello per rete VM di toohello hello cloud primario per il cloud secondario hello.
5. Nella console di gestione di Hyper-V hello, abilitare la Replica Hyper-V nell'host Hyper-V hello contenente hello VM di VMM e abilitare la replica in hello macchina virtuale. Assicurarsi che non si aggiungono tooclouds di macchina virtuale VMM hello che sono protetti mediante il ripristino del sito, tooensure che le impostazioni di Replica Hyper-V non sono sottoposto a override da Site Recovery.
6. Se si crea piani di ripristino per il failover che è utilizzare hello stesso server VMM di origine e di destinazione.
7. In caso di interruzione totale, eseguire il failover e il ripristino come riportato di seguito:

   1. Eseguire un failover non pianificato nella console di gestione di Hyper-V hello nel sito secondario di hello, toofail su hello VM di VMM toohello secondario del sito primario.
   2. Verificare che hello che VM di VMM sia attivo e in esecuzione e nell'insieme di credenziali hello eseguire toofail un failover non pianificato in macchine virtuali hello da cloud primario toosecondary. Eseguire il commit hello failover e selezionare un punto di ripristino alternativa, se necessario.
   3. Al termine hello failover non pianificato, tutte le risorse sono accessibili dal sito primario di hello nuovamente.
   4. Quando il sito primario di hello è disponibile anche nella console di gestione di Hyper-V hello nel sito secondario di hello, abilitare la replica inversa per hello VM di VMM. Verrà avviata la replica per hello VM da tooprimary secondario.
   5. Eseguire un failover pianificato nella console di gestione di Hyper-V hello nel sito secondario di hello, toofail su hello sito primario di toohello VM di VMM. Eseguire il commit hello failover. Abilitare la replica inversa, in modo che hello VM di VMM è nuovamente la replica da primario toosecondary.
   6. Nell'insieme di credenziali di hello servizi di ripristino, abilitare la replica inversa per carico di lavoro hello le macchine virtuali, toostart replicarle da tooprimary secondario.
   7. Nell'archivio di servizi di ripristino hello, eseguire un failover pianificato toofail hello indietro del carico di lavoro macchine virtuali toohello sito primario. Eseguire il commit toocomplete failover hello è. Quindi, abilitare la replica inversa toostart replica hello carico di lavoro macchine virtuali da toosecondary primario.

### <a name="replicate-with-a-stretched-vmm-cluster"></a>Eseguire la replica con un cluster VMM con estensione

Anziché distribuire un server VMM autonomo come una macchina virtuale che esegue la replica del sito secondario tooa, effettuabili VMM a disponibilità elevata mediante la distribuzione di una macchina virtuale in un cluster di failover di Windows. assicurando così flessibilità al carico di lavoro e protezione da errori hardware. toodeploy con hello Site Recovery VM di VMM devono essere distribuiti in un cluster di estensione in siti geograficamente separati. toodo questo:

1. Installazione di VMM in una macchina virtuale in un cluster di failover di Windows e selezionare hello opzione toorun hello server come a disponibilità elevata durante l'installazione.
2. istanza di SQL Server Hello che viene utilizzato da VMM deve essere replicato con gruppi di disponibilità AlwaysOn di SQL Server, in modo che vi sia una replica di database hello nel sito secondario hello.
3. Seguire le istruzioni hello questo toocreate articolo un insieme di credenziali, registrare il server di hello e impostare la protezione. È necessario tooregister ogni server VMM in hello cluster nel hello insieme di credenziali di servizi di ripristino. toodo, si installa hello Provider in un nodo attivo e registrare il server VMM hello. È quindi possibile installare Provider hello in altri nodi.
4. Quando si verifica un'interruzione, il server VMM hello e il database di SQL Server corrispondente sono il failover e accessibili dal sito secondario hello.



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 5: configurare un insieme di credenziali](vmm-to-vmm-walkthrough-create-vault.md).
