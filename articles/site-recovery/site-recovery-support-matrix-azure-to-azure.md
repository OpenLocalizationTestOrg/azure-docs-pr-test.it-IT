---
title: Matrice di supporto di aaaAzure Site Recovery per la replica da Azure tooAzure | Documenti Microsoft
description: Vengono riepilogati i sistemi operativi supportato hello e configurazioni per la replica di Azure Site Recovery macchine virtuali di Azure (VM) da un'area tooanother per esigenze di ripristino di emergenza di emergenza.
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: 75b2451b4c2069ca4b11deb0efe1329d43879eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-azure-tooazure"></a>Matrice di supporto Azure Site Recovery per la replica dal tooAzure Azure


>[!NOTE]
>
> La replica di Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.

Questo articolo riepiloga le configurazioni supportate e i componenti per quando si esegue la replica e il ripristino di macchine virtuali di Azure da una regione tooanother regione di Azure Site Recovery.

## <a name="user-interface-options"></a>Opzioni dell'interfaccia utente

**Interfaccia utente** |  **Supportato / Non supportato**
--- | ---
**Portale di Azure** | Supportato
**Portale classico** | Non supportate
**PowerShell** | Attualmente non supportato
**API REST** | Attualmente non supportato
**CLI** | Attualmente non supportato


## <a name="resource-move-support"></a>Supporto spostamento risorse

**Tipo spostamento risorse** | **Supportato / Non supportato** | **Osservazioni**  
--- | --- | ---
**Spostamento insieme di credenziali tra gruppi di risorse** | Non supportate |È possibile spostare insieme di credenziali di hello Recovery services nei gruppi di risorse.
**Spostamento servizi di calcolo, archiviazione e rete tra gruppi di risorse** | Non supportate |Se si sposta una macchina virtuale (o i componenti associati, come archiviazione e rete) dopo l'abilitazione della replica, è necessario toodisable replica e abilitare la replica per la macchina virtuale hello.


## <a name="support-for-deployment-models"></a>Supporto per modelli di distribuzione

**Modello di distribuzione** | **Supportato / Non supportato** | **Osservazioni**  
--- | --- | ---
**Classico** | Supportato | È possibile eseguire la replica di una macchina virtuale classica e ripristinarla solo come macchina virtuale classica. Non è possibile ripristinarla come macchina virtuale di Resource Manager. Se si distribuisce una macchina virtuale classica senza una rete virtuale e direttamente tooan area di Azure, non è supportata.
**Gestione risorse** | Supportato |

## <a name="support-for-replicated-machine-os-versions"></a>Supporto per le versioni dei sistemi operativi dei computer replicati

Hello di sotto di supporto è applicabile per qualsiasi carico di lavoro in esecuzione su hello indicato del sistema operativo.

#### <a name="windows"></a>Windows

- Windows Server 2016 (Server Core e Server con esperienza desktop)*
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 con almeno SP1

>[!NOTE]
>
> \*Windows Server 2016 Nano Server non è supportato.

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 6.7, 6.8, 7.0, 7.1, 7.2, 7.3
- CentOS 6.5, 6.6, 6.7, 6.8, 7.0, 7.1, 7.2, 7.3
- Server Ubuntu 14.04 LTS[ (versioni del kernel supportate)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Server Ubuntu 16.04 LTS[ (versioni del kernel supportate)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Oracle Enterprise Linux 6.4, 6.5 esegue kernel compatibile di hello Red Hat o non interrompibile Enterprise Kernel Release 3 (UEK3)
- SUSE Linux Enterprise Server 11 SP3

>[!NOTE]
>
> Il server Ubuntu mediante password basato l'autenticazione e account di accesso e utilizzano macchine virtuali di hello cloud init pacchetto tooconfigure cloud, potrebbe avere basato su password account di accesso disabilitato in caso di failover (a seconda della configurazione di cloudinit hello.) Account di accesso basato su password può essere riabilitata nella macchina virtuale hello reimpostando la password di hello dal menu di impostazioni hello (in hello supporto + sezione Risoluzione dei problemi) di failover macchina virtuale nel portale di Azure hello hello.

### <a name="supported-ubuntu-kernel-versions-for-azure-virtual-machines"></a>Versioni del kernel Ubuntu supportate per macchine virtuali di Azure

**Versione** | **Versione del servizio Mobility** | **Versione del kernel** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0 117-generica,<br/>3.16.0-25-Generic too3.16.0-77-generico,<br/>3.19.0-18-Generic too3.19.0 80-generica,<br/>4.2.0-18-Generic too4.2.0-42-generico,<br/>4.4.0-21-Generic generico 75 too4.4.0 |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0 121-generica,<br/>3.16.0-25-Generic too3.16.0-77-generico,<br/>3.19.0-18-Generic too3.19.0 80-generica,<br/>4.2.0-18-Generic too4.2.0-42-generico,<br/>4.4.0-21-Generic generico 81 too4.4.0 |
16.04 LTS | 9.10 | 4.4.0-21-Generic too4.4.0 81-generica,<br/>4.8.0-34-Generic too4.8.0-56-generico,<br/>4.10.0-14-Generic too4.10.0-24-generico |

## <a name="supported-file-systems-and-guest-storage-configurations-on-azure-virtual-machines-running-linux-os"></a>File system e configurazioni di archiviazione guest supportati nelle macchine virtuali di Azure che eseguono il sistema operativo Linux

* File system: ext3, ext4, ReiserFS (solo Suse Linux Enterprise Server), XFS
* Gestore volumi: LVM2
* Software con percorsi multipli: mapper dispositivi

## <a name="region-support"></a>Supporto di area

È possibile eseguire la replica e il ripristino delle macchine virtuali tra le due aree all'interno di hello dello stesso cluster geografici.

**Cluster geografico** | **Aree di Azure**
-- | --
America | Canada orientale, Canada centrale, Stati Uniti centro-meridionali, Stati Uniti centro-occidentali, Stati Uniti orientali, Stati Uniti orientali 2, Stati Uniti occidentali, Stati Uniti occidentali 2, Stati Uniti centrali, Stati Uniti centro-settentrionali
Europa | Regno Unito occidentale, Regno Unito meridionale, Europa settentrionale, Europa occidentale
Asia | India meridionale, India centrale, Asia sud-orientale, Asia orientale, Giappone orientale, Giappone occidentale, Corea centrale, Corea meridionale
Australia   | Australia orientale, Australia sudorientale

>[!NOTE]
>
> Per un'area Brasile meridionale, è possibile replicare solo ed eseguire il failover tooone del centro-meridionali, centrale Stati Uniti occidentali, Stati Uniti orientali, Stati Uniti orientali 2, Stati Uniti occidentali, Stati Uniti occidentali 2 e North Central US aree e hanno esito negativo.


## <a name="support-for-compute-configuration"></a>Supporto per la configurazione del servizio di calcolo

**Configurazione** | **Supportato/Non supportato** | **Osservazioni**
--- | --- | ---
Dimensione | Macchine virtuali di Azure di qualsiasi dimensione con almeno 2 core CPU e 1 GB di RAM | Fare riferimento troppo[le dimensioni di macchina virtuale di Azure](../virtual-machines/windows/sizes.md)
Set di disponibilità | Supportato | Se si utilizza l'opzione predefinita di hello durante il passaggio 'Abilitare la replica' nel portale, il set di disponibilità hello viene automaticamente creata in base alla configurazione di area di origine. È possibile modificare hello destinazione set di disponibilità in ' articolo replicato > Impostazioni > calcolo e rete > set di disponibilità ' qualsiasi momento.
Macchine virtuali con vantaggio Hybrid Use (HUB, Hybrid Use Benefit) | Supportato | Se macchina virtuale di origine hello dispone di licenza HUB abilitato, il failover di Test di hello o Failover VM utilizzata licenza HUB hello.
set di scalabilità di macchine virtuali | Non supportate |
Immagini della raccolta di Azure - Pubblicate da Microsoft | Supportato | È supportato come hello macchina virtuale viene eseguita in un sistema operativo supportato per il ripristino del sito
Immagini della raccolta di Azure - Pubblicate da terze parti | Supportato | Supportato, purché hello macchina virtuale viene eseguita in un sistema operativo supportato per il ripristino del sito.
Immagini personalizzate - Pubblicate da terze parti | Supportato | Supportato, purché hello macchina virtuale viene eseguita in un sistema operativo supportato per il ripristino del sito.
Macchine virtuali migrate tramite Site Recovery | Supportato | Se è eseguita la migrazione di una macchina di VMware/fisici tooAzure utilizzando il ripristino del sito, è necessario toouninstall versione precedente di hello del servizio di mobilità e riavviare la macchina hello prima la replica tooanother area di Azure.

## <a name="support-for-storage-configuration"></a>Supporto per la configurazione dell'archiviazione

**Configurazione** | **Supportato/Non supportato** | **Osservazioni**
--- | --- | ---
Dimensioni massime del disco del sistema operativo | 1023 GB | Fare riferimento troppo[dischi utilizzati dalle macchine virtuali.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Dimensioni massime del disco dati | 1023 GB | Fare riferimento troppo[dischi utilizzati dalle macchine virtuali.](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
Numero di dischi dati | Fino a 64 come supportato da una dimensione specifica di una macchina virtuale di Azure | Fare riferimento troppo[le dimensioni di macchina virtuale di Azure](../virtual-machines/windows/sizes.md)
Disco temporaneo | Sempre escluso dalla replica | Il disco temporaneo è sempre escluso dalla replica. Non è opportuno inserire dati persistenti su un disco temporaneo in base alle indicazioni di Azure. Fare riferimento troppo[disco temporaneo in macchine virtuali di Azure](../virtual-machines/windows/about-disks-and-vhds.md#temporary-disk) per altri dettagli.
Frequenza su disco hello di modifica dei dati | Massimo 6 MB/s per disco | Se tasso di modifica dei dati Media di hello in disco hello va oltre 6 MBps continuamente, replica non verrà aggiornarsi. Tuttavia, se si tratta di un burst di dati occasionale e frequenza di modifica dati hello è maggiore di 6 MBps per un certo tempo e viene fornita verso il basso, la replica verrà aggiornarsi. In questo caso, potrebbero verificarsi punti di ripristino leggermente ritardati.
Dischi su account di archiviazione standard | Supportato |
Dischi su account di archiviazione premium | Supportato | Se una macchina virtuale con dischi distribuiti tra account di archiviazione standard e premium, è possibile selezionare un account di archiviazione destinazione diversa per ogni tooensure disco è hello stessa configurazione di archiviazione nell'area di destinazione
Dischi gestiti standard | Non supportate |  
Dischi gestiti premium | Non supportate |
Spazi di archiviazione | Supportato |         
Crittografia per dati inattivi (SSE) | Supportato | Per gli account di archiviazione della cache e di destinazione, è possibile selezionare un account di archiviazione SSE abilitato.     
Crittografia dischi di Azure (ADE) | Non supportate |
Aggiunta/rimozione a caldo disco | Non supportate | Se si aggiungono o rimozione il disco dati in hello VM, è necessario toodisable replica e abilitare la replica per hello macchina virtuale.
Esclusione disco | Non supportate|   Il disco temporaneo è escluso per impostazione predefinita.
Archiviazione con ridondanza locale | Supportato |
Archiviazione con ridondanza geografica | Supportato |
RA-GRS | Supportato |
ZRS | Non supportate |  
Archiviazione ad accesso frequente e sporadico | Non supportate | I dischi delle macchine virtuali non sono supportati per l'archiviazione ad accesso frequente e sporadico

>[!IMPORTANT]
> Assicurarsi di seguire hello [informazioni aggiuntive sull'archiviazione](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) per l'origine virtuali di Azure macchine tooavoid eventuali problemi di prestazioni. Se si seguono le impostazioni predefinite di hello, il ripristino del sito creerà gli account di archiviazione hello necessarie in base alla configurazione di origine hello. Se si personalizza e selezionare le proprie impostazioni, attenersi alle istruzioni hello (... / storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks) come macchine virtuali di origine.

## <a name="support-for-network-configuration"></a>Supporto per la configurazione di rete
**Configurazione** | **Supportato/Non supportato** | **Osservazioni**
--- | --- | ---
Interfaccia di rete (NIC) | Fino al numero massimo di schede di rete supportato da dimensioni specifiche delle macchine virtuali di Azure | Schede di rete vengono creati quando hello macchina virtuale viene creata come parte del failover di Test o l'operazione di Failover. numero di schede NIC hello failover che macchina virtuale dipende dal numero di hello dell'origine di hello schede di rete che nella macchina virtuale è in fase di abilitazione della replica di hello di Hello. Se si Aggiungi/Rimuovi scheda di rete dopo l'abilitazione della replica, non influire conteggio NIC hello failover della macchina virtuale.
Servizio di bilanciamento del carico Internet | Supportato | È necessario tooassociate hello preconfigurato bilanciamento del carico usando uno script di automazione di azure in un piano di ripristino.
Servizio di bilanciamento del carico interno | Supportato | È necessario tooassociate hello preconfigurato bilanciamento del carico usando uno script di automazione di azure in un piano di ripristino.
IP pubblico| Supportato | È necessario un toohello IP pubblico esistente NIC tooassociate o crearne uno e associare toohello NIC usando uno script di automazione di azure in un piano di ripristino.
Gruppo di sicurezza di rete (NSG) sulla scheda di rete (Resource Manager)| Supportato | È necessario tooassociate hello NSG toohello NIC usando uno script di automazione di azure in un piano di ripristino.  
Gruppo di sicurezza di rete (NSG) sulla subnet (Resource Manager e classica)| Supportato | È necessario tooassociate hello NSG toohello NIC usando uno script di automazione di azure in un piano di ripristino.
Gruppo di sicurezza di rete (NSG) sulla macchina virtuale (classica)| Supportato | È necessario tooassociate hello NSG toohello NIC usando uno script di automazione di azure in un piano di ripristino.
IP riservato (IP statico) / Mantieni IP di origine | Supportato | Se hello NIC nella macchina virtuale di origine hello dispone di configurazione con IP statico e subnet di destinazione hello è hello stesso IP disponibile, viene assegnato toohello failover della macchina virtuale. Se non dispone di subnet di destinazione hello hello stesso IP disponibile, uno di hello disponibili indirizzi IP in subnet hello è riservato per questa macchina virtuale. È possibile specificare un IP fisso a scelta in 'Elemento replicato > Impostazioni > Calcolo e rete > Interfacce di rete'. È possibile selezionare hello NIC e specificare una subnet hello e IP desiderato.
IP dinamico| Supportato | Se hello NIC nella macchina virtuale di origine hello è la configurazione IP dinamica, hello NIC hello failover macchina virtuale è anche dinamica per impostazione predefinita. È possibile specificare un IP fisso a scelta in 'Elemento replicato > Impostazioni > Calcolo e rete > Interfacce di rete'. È possibile selezionare hello NIC e specificare una subnet hello e IP desiderato.
Integrazione di Gestione traffico | Supportato | È possibile preconfigurare il profilo di gestione in modo che il traffico di hello è indirizzato toohello endpoint nell'area di origine in un endpoint di base e toohello regolari nell'area di destinazione in caso di failover.
DNS gestito di Azure | Supportato |
DNS personalizzato  | Supportato |    
Proxy non autenticato | Supportato | Fare riferimento troppo[rete fornite nel documento.](site-recovery-azure-to-azure-networking-guidance.md)    
Proxy autenticato | Non supportate | Se hello VM utilizza un proxy autenticato per la connettività in uscita, non possono essere replicata usando Azure Site Recovery.  
Sito tooSite VPN locale (con o senza ExpressRoute)| Supportato | Verificare che UDRs hello e NSGs siano configurati in modo che il traffico di ripristino del sito hello non è indirizzati tooon locale. Fare riferimento troppo[rete fornite nel documento.](site-recovery-azure-to-azure-networking-guidance.md)  
Connessione di rete virtuale tooVNET | Supportato | Fare riferimento troppo[rete fornite nel documento.](site-recovery-azure-to-azure-networking-guidance.md)  


## <a name="next-steps"></a>Passaggi successivi
- Altre informazioni sulle [indicazioni per la connettività di rete per la replica delle macchine virtuali di Azure](site-recovery-azure-to-azure-networking-guidance.md)
- Iniziare a proteggere i carichi di lavoro [replicando le macchine virtuali di Azure](site-recovery-azure-to-azure.md)
