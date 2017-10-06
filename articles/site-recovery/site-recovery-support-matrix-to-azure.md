---
title: Matrice di supporto aaaAzure Site Recovery per la replica tooAzure | Documenti Microsoft
description: Vengono riepilogati i sistemi operativi supportato hello e componenti per Azure Site Recovery
services: site-recovery
documentationcenter: 
author: Rajani-Janaki-Ram
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: rajanaki
ms.openlocfilehash: eae1db2ff1392d272f6b2eb0e3410da19d09da7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-on-premises-tooazure"></a>Matrice di supporto Azure Site Recovery per la replica dal tooAzure locale


Questo articolo riepiloga le configurazioni supportate e i componenti di Azure Site Recovery quando la replica e il recupero di tooAzure. Per ulteriori informazioni sui requisiti di Azure Site Recovery, vedere hello [prerequisiti](site-recovery-prereq.md).


## <a name="support-for-deployment-options"></a>Supporto per opzioni di distribuzione

**Distribuzione** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)** |
--- | --- | ---
**Portale di Azure** | Archiviazione tooAzure le macchine virtuali VMware, con reti o archiviazione classico e Gestione risorse di Azure in locale.<br/><br/> Failover tooResource classiche o gestione basato su macchine virtuali. | Macchine virtuali Hyper-V tooAzure archiviazione, con reti o archiviazione classico e Gestione risorse in locale.<br/><br/> Failover tooResource classiche o gestione basato su macchine virtuali.
**Portale classico** | Solo modalità manutenzione. Non è possibile creare nuovi insiemi di credenziali. | Solo modalità manutenzione.
**PowerShell** | Attualmente non è supportata. | Supportato


## <a name="support-for-datacenter-management-servers"></a>Supporto per server di gestione dei data center

### <a name="virtualization-management-entities"></a>Entità di gestione della virtualizzazione

**Distribuzione** | **Supporto**
--- | ---
**Server fisico/VM VMware** | vCenter 6.5, 6.0 o 5.5
**Hyper-V (con Virtual Machine Manager)** | System Center Virtual Machine Manager 2016 e System Center Virtual Machine Manager 2012 R2

  >[!Note]
  > Un cloud System Center Virtual Machine Manager 2016 con una combinazione di host Windows Server 2016 e 2012 R2 non è attualmente supportato.

### <a name="host-servers"></a>Server host

**Distribuzione** | **Supporto**
--- | ---
**Server fisico/VM VMware** | vSphere 6.5, 6.0 e 5.5
**Hyper-V (con/senza Virtual Machine Manager)** | Windows Server 2016, Windows Server 2012 R2 con gli aggiornamenti più recenti.<br></br>Se si usa SCVMM, gli host Windows Server 2016 dovranno essere gestiti da SCVMM 2016.


  >[!Note]
  >Un sito di Hyper-V con una combinazione di host che eseguono Windows Server 2016 e 2012 R2 non è attualmente supportato. Ripristino tooan percorso alternativo per le macchine virtuali in un host Windows Server 2016 non è attualmente supportato.

## <a name="support-for-replicated-machine-os-versions"></a>Supporto per le versioni dei sistemi operativi dei computer replicati

Macchine virtuali che sono protette deve soddisfare [requisiti Azure](#failed-over-azure-vm-requirements) durante la replica tooAzure.
Hello nella tabella seguente viene riepilogato il supporto del sistema operativo replicati in diversi scenari di distribuzione durante l'utilizzo di Azure Site Recovery. Questo supporto è applicabile per qualsiasi carico di lavoro in esecuzione su hello indicato del sistema operativo.

 **Server fisico/VMware** | **Hyper-V (con/senza VMM)** |
--- | --- |
Le VM Windows Server 2012 R2 a 64 bit, Windows Server 2012, Windows Server 2008 R2 con SP1 o successivo<br/>*Windows Server 2016*: non supportato attualmente in macchine virtuali VMware e server fisici. <br/><br/> Red Hat Enterprise Linux: too5.11 5.2, 6.1 too6.8, too7.3 7.0 <br/><br/>Sistema operativo cento: too5.11 5.2, 6.1 too6.8, too7.3 7.0 <br/><br/>Server Ubuntu 14.04 LTS[ (versioni del kernel supportate)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Server Ubuntu 16.04 LTS[ (versioni del kernel supportate)](#supported-ubuntu-kernel-versions-for-vmwarephysical-servers)<br/><br/>Oracle Enterprise Linux 6.4, 6.5 esegue kernel compatibile di hello Red Hat o non interrompibile Enterprise Kernel Release 3 (UEK3) <br/><br/> SUSE Linux Enterprise Server 11 SP3 <br/><br/> SUSE Linux Enterprise Server 11 SP4 <br/>(Aggiornamento di replicare macchine da SLES 11 SP3 tooSLES 11 SP4 non è supportato. Se un computer replicato è stato aggiornato da SLES 11SP3 tooSLES 11 SP4, si sarà necessario toodisable replica e proteggere computer hello nuovamente post-aggiornamento hello.) | Qualsiasi sistema operativo guest [supportato da Azure](https://technet.microsoft.com/library/cc794868.aspx)


>[!IMPORTANT]
>(Applicabile tooVMware/server fisici replica tooAzure)
>
> Nel server di 7 + CentOS e Red Hat Enterprise Linux Server 7 +, 3.10.0-514 versione kernel è supportata a partire dalla versione 9.8 di hello servizio di mobilità di ripristino del sito di Azure.<br/><br/>
> I clienti sul kernel 3.10.0-514 hello con una versione di hello servizio di mobilità inferiore alla versione 9.8 sono necessari toodisable replica, quindi fare clic su aggiornamento hello versione di hello mobilità servizio tooversion 9.8 e quindi abilitare nuovamente la replica.


### <a name="supported-ubuntu-kernel-versions-for-vmwarephysical-servers"></a>Versioni del kernel Ubuntu supportate per server VMware/fisici

**Versione** | **Versione del servizio Mobility** | **Versione del kernel** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-Generic too3.13.0 117-generica,<br/>3.16.0-25-Generic too3.16.0-77-generico,<br/>3.19.0-18-Generic too3.19.0 80-generica,<br/>4.2.0-18-Generic too4.2.0-42-generico,<br/>4.4.0-21-Generic generico 75 too4.4.0 |
14.04 LTS | 9.10 | 3.13.0-24-Generic too3.13.0 121-generica,<br/>3.16.0-25-Generic too3.16.0-77-generico,<br/>3.19.0-18-Generic too3.19.0 80-generica,<br/>4.2.0-18-Generic too4.2.0-42-generico,<br/>4.4.0-21-Generic generico 81 too4.4.0 |
16.04 LTS | 9.10 | 4.4.0-21-Generic too4.4.0 81-generica,<br/>4.8.0-34-Generic too4.8.0-56-generico,<br/>4.10.0-14-Generic too4.10.0-24-generico |


## <a name="supported-file-systems-and-guest-storage-configurations-on-linux-vmwarephysical-servers"></a>File system e configurazioni di archiviazione guest supportate in Linux (server VMware/fisici)

esempio Hello file di archiviazione e i sistemi software di configurazione è supportata nei server Linux in esecuzione nei server VMware o fisici:
* File system: ext3, ext4, ReiserFS (solo Suse Linux Enterprise Server), XFS
* Gestore volumi: LVM2
* Software con percorsi multipli: mapper dispositivi

I dispositivi di archiviazione paravirtualizzati, ovvero dispositivi esportati da driver paravirtualizzati, non sono supportati.<br/>
I dispositivi di I/O a blocchi a code multiple non sono supportati.<br/>
I server fisici con controller di archiviazione HP CCISS hello non sono supportati.<br/>

>[!Note]
> In hello server Linux seguenti directory (se impostato come le partizioni, file-sistemi separati) devono essere tutti in hello stesso disco (disco del sistema operativo hello) nel server di origine hello: / (radice), /boot, in /usr., percorso /usr/local, /var, /etc/hosts<br/><br/>
> Funzionalità XFSv5 su XFS file System, ad esempio checksum dei metadati sono supportate a partire dalla versione 9.10 di hello servizio di mobilità. Se si usano le funzionalità di XFSv5, verificare che sia in esecuzione il servizio Mobility 9.10 o versione successiva. È possibile utilizzare superblocco di hello xfs_info utilità toocheck hello XFS per partizione hello. Se ftype è impostato too1, quindi vengono utilizzate funzionalità XFSv5.
>


## <a name="support-for-network-configuration"></a>Supporto per la configurazione di rete
Hello le tabelle seguenti riepiloga il supporto di configurazione di rete in vari scenari di distribuzione che utilizzano tooAzure tooreplicate Azure Site Recovery.

### <a name="host-network-configuration"></a>Configurazione di rete per host

**Configurazione** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | ---
Gruppo NIC | Sì<br/><br/>Non supportato quando i computer fisici vengono replicati| Sì
VLAN | Sì | Sì
IPv4 | Sì | Sì
IPv6 | No | No

### <a name="guest-vm-network-configuration"></a>Configurazione di rete per VM guest

**Configurazione** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | ---
Gruppo NIC | No | No
IPv4 | Sì | Sì
IPv6 | No | No
IP statico (Windows) | Sì | Sì
IP statico (Linux) | Sì <br/><br/>Macchine virtuali è configurato toouse DHCP su failback  | No
Più NIC | Sì | Sì

### <a name="failed-over-azure-vm-network-configuration"></a>Configurazione di rete per VM di Azure sottoposte a failover

**Rete di Azure** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | ---
Express Route | Sì | Sì
ILB | Sì | Sì
ELB | Sì | Sì
Gestione traffico | Sì | Sì
Più NIC | Sì | Sì
IP riservato | Sì | Sì
IPv4 | Sì | Sì
Conservazione IP origine | Sì | Sì


## <a name="support-for-storage"></a>Supporto per archiviazione
Hello le tabelle seguenti riepiloga il supporto di configurazione di archiviazione in vari scenari di distribuzione che utilizzano tooAzure tooreplicate Azure Site Recovery.

### <a name="host-storage-configuration"></a>Configurazione di archiviazione per host

**Configurazione** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | --- | ---
NFS | Sì per VMware<br/><br/> No per server fisici | N/D
SMB 3.0 | N/D | Sì
SAN (iSCSI) | Sì | Sì
Percorsi multipli (MPIO)<br></br>Testata con: DSM Microsoft, EMC PowerPath 5.7 SP4, DSM EMC PowerPath per CLARiiON | Sì | Sì

### <a name="guest-or-physical-server-storage-configuration"></a>Configurazione di archiviazione per server fisici o guest

**Configurazione** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | ---
VMDK | Sì | N/D
VHD/VHDX | N/D | Sì
VM di seconda generazione | N/D | Sì
EFI/UEFI| No | Sì
Disco cluster condiviso | No | No
Disco crittografato | No | No
NFS | No | N/D
SMB 3.0 | No | No
RDM | Sì<br/><br/> N/D per server fisici | N/D
Disco superiore a 1 TB | Sì<br/><br/>Fino a 4095 GB | Sì<br/><br/>Fino a 4095 GB
Disco con dimensioni del settore di 4K | Sì | Sì, supportato per VM di generazione 1<br/><br/>Non supportato per VM di generazione 2
Volume con disco con striping superiore a 1 TB<br/><br/> Gestione volumi logici (LVM) | Sì | Sì
Spazi di archiviazione | No | Sì
Aggiunta/rimozione a caldo disco | No | No
Esclusione disco | Sì | Sì
Percorsi multipli (MPIO) | N/D | Sì

**Archiviazione di Azure** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | ---
Archiviazione con ridondanza locale | Sì | Sì
Archiviazione con ridondanza geografica | Sì | Sì
RA-GRS | Sì | Sì
Archiviazione ad accesso sporadico | No | No
Archiviazione ad accesso frequente| No | No
Crittografia dei dati inattivi (SSE)| Sì | Sì
Archiviazione Premium | Sì | Sì
Servizio di importazione/esportazione | No | No


## <a name="support-for-azure-compute-configuration"></a>Supporto per configurazione di calcolo di Azure

**Funzionalità di calcolo** | **Server fisico/VMware** | **Hyper-V (con/senza Virtual Machine Manager)**
--- | --- | --- 
Set di disponibilità | Sì | Sì
HUB | Sì | Sì  
Dischi gestiti | Sì | Sì<br/><br/>Il failback tooon locale dalla macchina virtuale di Azure con dischi gestiti non è attualmente supportato.

## <a name="failed-over-azure-vm-requirements"></a>Requisiti per VM di Azure sottoposte a failover

È possibile distribuire macchine virtuali di tooreplicate il ripristino del sito e server fisici che eseguono un sistema operativo supportato da Azure. vale a dire la maggior parte delle versioni di Windows e Linux. Macchine virtuali che si desidera tooreplicate deve essere conforme con i seguenti requisiti di Azure durante la replica tooAzure hello in locale.

**Entità** | **Requisiti** | **Dettagli**
--- | --- | ---
**Sistema operativo guest** | La replica Hyper-V tooAzure: il ripristino del sito supporta tutti i sistemi operativi [supportato da Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx). <br/><br/> Per la replica di server fisici e VMware: controllare hello Windows e Linux [prerequisiti](site-recovery-vmware-to-azure-classic.md) | Il controllo dei prerequisiti avrà esito negativo se non supportato.
**Architettura sistema operativo guest** | 64 bit | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Dimensioni disco del sistema operativo** | Backup too2048 GB se si replicano **le macchine virtuali VMware o i server fisici tooAzure**.<br/><br/>Fino a 2048 GB per le macchine virtuali **Hyper-V di prima generazione**.<br/><br/>Fino a 300 GB per le **macchine virtuali Hyper-V di seconda generazione**.  | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Numero di dischi del sistema operativo** | 1 | Il controllo dei prerequisiti avrà esito negativo se non supportato.
**Numero di dischi dati** | minore o uguale a 64 se si replicano **tooAzure le macchine virtuali VMware**; 16 o meno se si replicano **tooAzure macchine virtuali Hyper-V** | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Dimensioni dei dischi rigidi virtuali dei dischi dati** | Too4095 GB | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Schede di rete** | Sono supportate più schede |
**Disco rigido virtuale condiviso** | Non supportate | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Disco FC** | Non supportate | Il controllo dei prerequisiti avrà esito negativo se non supportato
**Formato disco rigido** | VHD  <br/><br/> VHDX | Sebbene VHDX non è attualmente supportato in Azure, il ripristino del sito converte automaticamente VHDX tooVHD quando si esegue il failover tooAzure. Quando il failback delle macchine virtuali di hello tooon locale continuano formato VHDX di toouse hello.
**BitLocker** | Non supportate | Prima di proteggere una macchina virtuale è necessario disabilitare BitLocker.
**Nome VM** | Tra 1 e 63 caratteri. Tooletters con restrizioni, numeri e trattini. nome della macchina virtuale Hello deve iniziare e terminare con una lettera o un numero. | Aggiornare il valore di hello nella proprietà della macchina virtuale hello in Site Recovery.
**Tipo di VM** | Prima generazione<br/><br/> Seconda generazione - Windows | Sono supportate le macchine virtuali di seconda generazione con disco del sistema operativo di base che include uno o più volumi di dati in formato VHDX e inferiori a 300 GB di spazio su disco.<br></br>Le macchine virtuali Linux di seconda generazione non sono supportate. [Altre informazioni](https://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/)|

## <a name="support-for-recovery-services-vault-actions"></a>Supporto per azioni su insiemi di credenziali di Servizi di ripristino

**Azione** | **Server fisico/VMware** | **Hyper-V (senza Virtual Machine Manager)** | **Hyper-V (con Virtual Machine Manager)**
--- | --- | --- | ---
Spostamento insieme di credenziali tra gruppi di risorse<br/><br/> All'interno e tra sottoscrizioni | No | No | No
Spostamento di risorse di archiviazione, rete e VM di Azure tra gruppi di risorse<br/><br/> All'interno e tra sottoscrizioni | No | No | No


## <a name="support-for-provider-and-agent"></a>Supporto per provider e agente

**Nome** | **Descrizione** | **Versione più recente** | **Dettagli**
--- | --- | --- | --- | ---
**Provider di Azure Site Recovery** | Coordina le comunicazioni tra server locali e Azure <br/><br/> Installato nei server Virtual Machine Manager locali o nei server Hyper-V se non è presente un server Virtual Machine Manager | 5.1.19 ([disponibile dal portale](http://aka.ms/downloaddra)) | [Funzionalità e correzioni più recenti](https://support.microsoft.com/kb/3155002)
**Installazione Azure Site Recovery unificata (tooAzure VMware)** | Coordina le comunicazioni tra server VMware locali e Azure  <br/><br/> Installato su server VMware locali | 9.3.4246.1 (disponibile dal portale) | [Funzionalità e correzioni più recenti](https://support.microsoft.com/kb/3155002)
**Servizio Mobility** | Coordina la replica fra server VMware locali/server fisici e sito Azure/secondario<br/><br/> Installato in server fisici o di VMware VM desiderato tooreplicate  | N/D (disponibile dal portale) | N/D
**Agente di Servizi di ripristino di Microsoft Azure (MARS)** | Coordina la replica tra le macchine virtuali Hyper-V e Azure<br/><br/> Installato nei server Hyper-V locali (con o senza un server Virtual Machine Manager) | Agente più recente ([disponibile dal portale](http://aka.ms/latestmarsagent)) |






## <a name="next-steps"></a>Passaggi successivi
[Verifica dei prerequisiti](site-recovery-prereq.md)
