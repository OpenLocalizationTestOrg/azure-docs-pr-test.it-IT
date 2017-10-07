---
title: aaaPrerequisites per la replica tooAzure tramite Azure Site Recovery | Documenti Microsoft
description: Informazioni sui prerequisiti di hello per la replica delle macchine virtuali e i computer fisici tooAzure tramite il servizio di Azure Site Recovery hello.
services: site-recovery
documentationcenter: 
author: rajani-janaki-ram
manager: jwhit
editor: tysonn
ms.assetid: e24eea6c-50a7-4cd5-aab4-2c5c4d72ee2d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/23/2017
ms.author: rajanaki
ms.openlocfilehash: 0e32ab7cd7c65a3f67ffa2f2c15af189c15b6f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
#  <a name="prerequisites-for-replication-from-on-premises-tooazure-by-using-site-recovery"></a>Prerequisiti per la replica dal tooAzure locale utilizzando il ripristino del sito

> [!div class="op_single_selector"]
> * [La replica da Azure tooAzure](site-recovery-azure-to-azure-prereq.md)
> * [La replica da locale tooAzure](site-recovery-prereq.md)

Azure Site Recovery consentono di supportare strategia ripristino di emergenza e la continuità di business gestendo la replica di un'area di Azure di tooanother macchina virtuale di Azure (VM). Il ripristino del sito vengono replicati anche i server fisici locali e macchine virtuali toohello cloud (Azure) o Data Center secondario tooa. Se si verifica un'interruzione nella posizione primaria, è possibile eseguire il failover tooa posizione secondaria tookeep App e carichi di lavoro disponibili. È possibile eseguire il percorso primario tooyour indietro quando la posizione primaria hello restituisce toonormal operazioni. Per altre informazioni su Site Recovery, vedere [Che cos'è Site Recovery?](site-recovery-overview.md).

In questo articolo si riepilogano i prerequisiti hello per iniziare la replica di ripristino del sito da un tooAzure macchina locale.

È possibile inviare eventuali commenti nella parte inferiore di hello dell'articolo hello. È anche possibile porre domande tecniche in hello [forum di servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="azure-requirements"></a>Requisiti di Azure

**Requisito** | **Dettagli**
--- | ---
**Account di Azure** | [Account Microsoft Azure](http://azure.microsoft.com/). È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).
**Servizio Site Recovery** | Per ulteriori informazioni sui prezzi hello servizio Azure Site Recovery, vedere [dei prezzi di Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
**Archiviazione di Azure** | È necessario un toostore replicati dati dell'account di archiviazione di Azure. account di archiviazione Hello deve trovarsi in hello stessa area hello insieme di credenziali di servizi di ripristino di Azure. In caso di failover, vengono create macchine virtuali di Azure.<br/><br/> A seconda del modello di risorsa hello desiderate toouse per failover della macchina virtuale di Azure, è possibile impostare un account tramite hello [il modello di distribuzione Azure Resource Manager](../storage/common/storage-create-storage-account.md) o hello [modello di distribuzione classica](../storage/common/storage-create-storage-account.md).<br/><br/>È possibile usare l'[archiviazione con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) o locale. È consigliabile usare l'archiviazione con ridondanza geografica, Con l'archiviazione con ridondanza geografica, data è resiliente se si verifica un'interruzione dell'alimentazione locale o se non è possibile recuperare l'area primaria hello.<br/><br/> È possibile usare un account standard di Archiviazione di Azure oppure l'archiviazione Premium di Azure. L'[archiviazione Premium](https://docs.microsoft.com/azure/storage/storage-premium-storage) viene in genere usata per le macchine virtuali che richiedono un livello di prestazioni di I/O costantemente elevato e bassa latenza. Con l'archiviazione Premium una macchina virtuale può ospitare carichi di lavoro con uso intensivo di I/O. Se si usa l'archiviazione Premium per i dati replicati, è necessario anche un account di archiviazione standard. Un account di archiviazione standard archivia i log di replica che acquisiscono dati locali tooon le modifiche in corso.<br/><br/>
**Limiti di archiviazione** | Impossibile spostare gli account di archiviazione in uso nel gruppo di risorse diverso tooa il ripristino del sito, o spostare tooor utilizzare con un'altra sottoscrizione.<br/><br/> Attualmente, gli account di archiviazione toopremium India centrale e meridionale di replica non è disponibile.
**Rete di Azure** | È necessaria una rete di Azure, macchine virtuali di Azure toowhich connettersi dopo il failover. Hello rete di Azure deve essere hello stessa area hello insieme di credenziali di servizi di ripristino.<br/><br/> In hello portale di Azure, è possibile creare una rete di Azure tramite hello [il modello di distribuzione di gestione risorse](../virtual-network/virtual-networks-create-vnet-arm-pportal.md) o hello [modello di distribuzione classica](../virtual-network/virtual-networks-create-vnet-classic-pportal.md).<br/><br/> Se si replica da tooAzure di System Center Virtual Machine Manager (VMM), è necessario impostare mapping di rete tra le reti VM di VMM e le reti di Azure. In questo modo si garantisce che le macchine virtuali di Azure connettersi tooappropriate reti dopo il failover.
**Limitazioni di rete** | Impossibile spostare gli account di rete in uso nel gruppo di risorse diverso tooa il ripristino del sito, o spostare tooor utilizzare con un'altra sottoscrizione.
**Mapping di rete** | Se si esegue la replica di macchine virtuali di Microsoft Hyper-V nei cloud VMM, è necessario configurare il mapping di rete. In questo modo si garantisce che le macchine virtuali di Azure connettersi reti tooappropriate quando vengono creati dopo il failover.

> [!NOTE]
> Hello nelle sezioni seguenti descrivono i prerequisiti hello per vari componenti dell'ambiente del cliente hello. Per ulteriori informazioni sul supporto per configurazioni specifiche, vedere hello [matrice del supporto](site-recovery-support-matrix.md).
>

## <a name="disaster-recovery-of-vmware-vms-or-physical-windows-or-linux-servers-tooazure"></a>Ripristino di emergenza di macchine virtuali VMware o fisici tooAzure di server Windows o Linux
Hello seguenti componenti è necessario per il ripristino di emergenza di macchine virtuali VMware o i server fisici Windows o Linux. Sono inoltre toohello quelli descritti nella [requisiti Azure](#azure-requirements).


### <a name="configuration-server-or-additional-process-server"></a>Server di configurazione o server di elaborazione aggiuntivo

Configurare un computer locale come hello configurazione server tooorchestrate la comunicazione tra hello nel sito locale e Azure. computer locale Hello gestisce anche la replica dei dati. <br/></br>

*   **Prerequisiti dell'host VMware vCenter o vSphere**

    | **Componente** | **Requisiti** |
    | --- | --- |
    | **vSphere** | Sono necessari uno o più hypervisor VMware vSphere.<br/><br/>Hypervisor devono essere in esecuzione la versione di vSphere 5.1, 6.0 o 5.5 con hello aggiornamenti più recenti.<br/><br/>È consigliabile che gli host vSphere e il server vCenter che sia incluso hello stessa rete come server di elaborazione hello. A meno che non aver configurato un server di elaborazione dedicato, è hello rete in cui si trova il server di configurazione di hello. |
    | **vCenter** | È consigliabile distribuire un toomanage di VMware vCenter server host vSphere. Deve essere eseguito vCenter versione 6.0 o 5.5, con gli aggiornamenti più recenti di hello.<br/><br/>**Limitazione**: Site Recovery non supporta la replica tra istanze di vCenter vMotion. Neanche l'archiviazione DRS e l'archiviazione vMotion sono supportate nella macchina virtuale di destinazione master in seguito a un'operazione di riprotezione.||

* **Prerequisiti dei computer replicati**

    | **Componente** | **Requisiti** |
    | --- | --- |
    | **Macchine virtuali locali** (macchine virtuali di VMware) | Nelle macchine virtuali replicate devono essere installati e in esecuzione gli strumenti VMware.<br/><br/> Le macchine virtuali devono soddisfare i [prerequisiti di Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) per la creazione di una macchina virtuale di Azure.<br/><br/>La capacità del disco in ogni macchina protetta non può essere più di 1.023 GB. <br/><br/>Un almeno 2 GB di spazio disponibile sull'unità di installazione hello è necessaria per l'installazione del componente.<br/><br/>Se si desidera la coerenza tra più macchine tooenable, porta 20004 deve essere aperta nel firewall locale della macchina virtuale hello.<br/><br/>I nomi delle macchine devono avere una lunghezza da 1 a 63 caratteri e si possono usare lettere, numeri e trattini. nome Hello deve iniziare con una lettera o un numero e terminare con una lettera o un numero. <br/><br/>Dopo aver abilitato la replica per un computer, è possibile modificare hello nomi di Azure.<br/><br/> |
    | **Computer Windows (fisico o VMware)** | Hello macchina deve essere in esecuzione uno dei seguenti hello supportati i sistemi operativi a 64 bit: <br/>- Windows Server 2012 R2<br/>- Windows Server 2012<br/>- Windows Server 2008 R2 con SP1 o versione successiva<br/><br/> Hello sistema operativo installato nel disco del sistema operativo hello unità C. deve essere un disco di base di Windows e non dinamici. disco dati Hello può essere dinamica.<br/><br/>|
    | **Computer Linux** (fisico o VMware) | Hello macchina deve essere in esecuzione uno dei seguenti hello supportati i sistemi operativi a 64 bit: <br/>- Red Hat Enterprise Linux 7.2, 7.1, 6.8 o 6.7<br/>- Centos 7.2, 7.1, 7.0, 6.8, 6.7, 6.6 o 6.5<br/>- Server Ubuntu 14.04 LTS (per un elenco delle versioni supportate del kernel per Ubuntu, vedere i [sistemi operativi supportati](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions))<br/>-Kernel compatibile con Enterprise Linux versione 6.5 o 6.4, in esecuzione uno hello Red Hat oracle o non interrompibile Enterprise Kernel versione 3 (UEK3)<br/>- SUSE Linux Enterprise Server 11 SP4 o SUSE Linux Enterprise Server 11 SP3<br/><br/>I file /etc/hosts nel computer protetto devono avere le voci che eseguono il mapping degli indirizzi tooIP nome host locale hello associati a tutte le schede di rete.<br/><br/>Dopo il failover, se si desidera tooconnect tooan macchina virtuale di Azure che esegue Linux tramite un client Secure Shell (SSH), assicurarsi che il servizio SSH hello nel computer protetto hello è toostart automaticamente all'avvio del sistema. Verificare inoltre che le regole del firewall consentano un computer protetto toohello di connessione SSH.<br/><br/>nome host Hello, punti di montaggio, i nomi dei dispositivi e i percorsi di sistema di Linux e i nomi di file (ad esempio, /etc/ e in /usr.) devono essere solo in inglese.<br/><br/>Hello seguenti directory (se impostato come partizioni distinte o file System) deve essere in hello stesso disco (disco del sistema operativo hello) nel server di origine hello:<br/>- / (root)<br/>- /boot<br/>- /usr<br/>- /usr/local<br/>- /var<br/>- /etc<br/><br/>Attualmente, le funzionalità di XFS v5, come il checksum dei metadati, non sono supportate da Site Recovery nei file system XFS. Assicurarsi che i file system XFS non usino alcuna funzionalità v5. È possibile utilizzare superblocco di hello xfs_info utilità toocheck hello XFS per partizione hello. Se **ftype** è troppo**1**, vengono utilizzate le funzionalità XFS v5.<br/><br/>In server Red Hat Enterprise Linux 7 e CentOS 7, l'utilità lsof hello deve essere installato e disponibile.<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-tooazure-no-vmm"></a>Ripristino di emergenza di macchine virtuali Hyper-V tooAzure (senza VMM)

Hello seguenti componenti è necessario per il ripristino di emergenza delle macchine virtuali Hyper-V nei cloud VMM. Sono inoltre toohello quelli descritti nella [requisiti Azure](#azure-requirements).

| **Prerequisito** | **Dettagli** |
| --- | --- |
| **Host Hyper-V** |Uno o più server locale deve essere in esecuzione Windows Server 2012 R2 con aggiornamenti più recenti hello e ruolo Hyper-V hello abilitato o Microsoft Hyper-V Server 2012 R2.<br/><br/>I server Hyper-V devono contenere una o più macchine virtuali.<br/><br/>Server Hyper-V deve essere connesso toohello Internet, direttamente o tramite un proxy.<br/><br/>Server Hyper-V deve avere correzioni hello descritte nell'articolo della Knowledge Base hello [2961977](https://support.microsoft.com/kb/2961977) installato.
|**Provider e agente**| Durante la distribuzione di Site Recovery, si installa il provider di Azure Site Recovery hello. installazione del provider Hello viene installato anche l'agente di servizi di ripristino di Azure hello in ogni server Hyper-V che esegue macchine virtuali che si desidera tooprotect. <br/><br/>Tutti i server Hyper-V in un ripristino del sito deve disporre dell'insieme di credenziali hello le stesse versioni del provider di hello e agente hello.<br/><br/>provider di Hello deve tooconnect tooSite ripristino su hello Internet. Il traffico può essere inviato direttamente oppure tramite un proxy. Si noti che il proxy basato su HTTPS non è supportato. Hello proxy server deve consentire l'accesso toohello URL seguenti:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/>Se si dispone di regole firewall basate sull'indirizzo IP nel server di hello, assicurarsi che le regole di hello consentono la comunicazione tooAzure.<br/><br/> Consenti hello [intervalli IP Data Center di Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e HTTPS (porta 443).<br/><br/> Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per hello occidentale Stati Uniti (utilizzato per la gestione di identità e controllo di accesso).


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooazure"></a>Ripristino di emergenza delle macchine virtuali Hyper-V in VMM cloud tooAzure

Hello seguenti componenti è necessario per il ripristino di emergenza delle macchine virtuali Hyper-V nei cloud VMM. Sono inoltre toohello quelli descritti nella [requisiti Azure](#azure-requirements).

| **Prerequisito** | **Dettagli** |
| --- | --- |
| **Virtual Machine Manager** |Devono essere disponibili uno o più server VMM in esecuzione su System Center 2012 R2 o versione successiva. Ogni server VMM deve essere configurato con uno o più cloud. <br/><br/>Un cloud deve includere:<br/>- Uno o più gruppi host VMM.<br/>- Uno o più cluster o server host Hyper-V in ogni gruppo host.<br/><br/>Per ulteriori informazioni sull'impostazione di cloud VMM, vedere [come toocreate un cloud Virtual Machine Manager 2012](http://social.technet.microsoft.com/wiki/contents/articles/2729.how-to-create-a-cloud-in-vmm-2012.aspx). |
| **Hyper-V** |I server host Hyper-V devono essere in esecuzione almeno Windows Server 2012 R2 con ruolo hello Hyper-V abilitato o Microsoft Hyper-V Server 2012 R2. è necessario installare gli aggiornamenti più recenti di Hello.<br/><br/> Un server Hyper-V deve contenere una o più macchine virtuali.<br/><br/> Un server host Hyper-V o un cluster che include macchine virtuali che si desidera tooreplicate deve essere gestito in un cloud VMM.<br/><br/>Server Hyper-V deve essere connesso toohello Internet, direttamente o tramite un proxy.<br/><br/>Server Hyper-V deve avere correzioni hello descritte nell'articolo della Knowledge Base hello [2961977](https://support.microsoft.com/kb/2961977) installato.<br/><br/>I server host Hyper-V è necessario l'accesso a Internet per tooAzure di replica di dati. |
| **Provider e agente** |Durante la distribuzione di Azure Site Recovery, installare il Provider di Azure Site Recovery nel server VMM hello. Installare l'agente di Servizi di ripristino negli host Hyper-V. l'agente e il provider di hello necessario tooconnect tooAzure direttamente tramite Internet hello o un proxy. Un proxy basato su HTTPS non è supportato. il server proxy Hello nel server VMM hello e host Hyper-V deve consentire l'accesso a: <br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>Se si dispone di regole firewall basate sull'indirizzo IP nel server VMM hello, assicurarsi che le regole di hello consentono la comunicazione tooAzure.<br/><br/> Consenti hello [intervalli IP Data Center di Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653) e HTTPS (porta 443).<br/><br/>Consenti gli intervalli di indirizzi IP per hello regione di Azure per la sottoscrizione e per gli Stati Uniti occidentali di hello (utilizzato per la gestione di identità e controllo di accesso).<br/><br/> |

### <a name="replicated-machine-prerequisites"></a>Prerequisiti dei computer replicati

| **Componente** | **Dettagli** |
| --- | --- |
| **Macchine virtuali protette** | Site Recovery supporta tutti i sistemi operativi supportati da [Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).<br/><br/>Macchine virtuali devono soddisfare hello [Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) per la creazione di una macchina virtuale di Azure. I nomi delle macchine devono avere una lunghezza da 1 a 63 caratteri e si possono usare lettere, numeri e trattini. nome Hello deve iniziare con una lettera o un numero e terminare con una lettera o un numero. <br/><br/>Dopo aver abilitato la replica per hello VM, è possibile modificare il nome di macchina virtuale hello. <br/><br/> La capacità del disco per ogni macchina protetta non può essere più di 1.023 GB. Una macchina virtuale può essere composto too16 dischi (in alto too16 TB).<br/><br/>


## <a name="disaster-recovery-of-hyper-v-vms-in-vmm-clouds-tooa-customer-owned-site"></a>Ripristino di emergenza delle macchine virtuali Hyper-V nel sito di proprietà dell'azienda cliente tooa cloud VMM

Hello seguenti componenti è necessario per il ripristino di emergenza delle macchine virtuali Hyper-V nel sito di proprietà dell'azienda cliente tooa cloud VMM. Sono inoltre toohello quelli descritti nella [requisiti Azure](#azure-requirements).

| **Componente** | **Dettagli** |
| --- | --- |
| **Virtual Machine Manager** |  È consigliabile distribuire un server VMM nel sito primario di hello sia del sito secondario di hello.<br/><br/> È possibile [eseguire la replica tra cloud in un unico server VMM](site-recovery-vmm-to-vmm.md#prepare-for-single-server-deployment). tooreplicate tra cloud in un singolo server VMM, è necessario almeno due cloud configurati nei server VMM hello.<br/><br/> Server VMM devono essere in esecuzione almeno System Center 2012 SP1, con gli aggiornamenti più recenti di hello.<br/><br/> Ogni server VMM deve avere uno o più cloud. Tutti i cloud devono disporre di hello che set di profili di capacità Hyper-V. <br/><br/>I cloud devono contenere uno o più gruppi host VMM. Per altre informazioni sulla configurazione di cloud VMM, vedere [Preparare la distribuzione di Azure Site Recovery](https://msdn.microsoft.com/library/azure/dn469075.aspx#BKMK_Fabric). |
| **Hyper-V** | Server Hyper-V deve essere in esecuzione almeno Windows Server 2012 con ruolo hello Hyper-V abilitato e avere hello installati aggiornamenti più recenti.<br/><br/> Un server Hyper-V deve contenere una o più macchine virtuali.<br/><br/>  Server host Hyper-V devono essere posizionati nei gruppi host nei cloud VMM primario e secondario di hello.<br/><br/> Se si esegue Hyper-V in un cluster in Windows Server 2012 R2, è consigliabile installare l'aggiornamento di hello descritto nell'articolo della Knowledge Base [2961977](https://support.microsoft.com/kb/2961977).<br/><br/> Se si esegue Hyper-V in un cluster basato su indirizzi IP statici in Windows Server 2012, non viene creato automaticamente un gestore cluster. È necessario configurare manualmente un gestore cluster hello. Per ulteriori informazioni su gestore cluster hello, vedere [Configura ruolo gestore di replica di hello per la replica da cluster](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx). |
| **Provider** | Durante la distribuzione di Site Recovery, installare il provider di Azure Site Recovery hello nei server VMM. provider di Hello comunica con il ripristino del sito tramite replica tooorchestrate HTTPS (porta 443). La replica dei dati si verifica tra hello server primario e secondario Hyper-V in hello LAN o tramite una connessione VPN.<br/><br/> provider di Hello in cui è in esecuzione nel server VMM hello deve accedere toohello URL seguenti:<br/><br/>[!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)] <br/><br/>provider di Site Recovery Hello deve consentire la comunicazione di firewall da hello VMM server toohello [intervalli IP Data Center di Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e consentire il protocollo HTTPS (porta 443) di hello. |


## <a name="url-access"></a>Accesso a URL
Gli URL seguenti dovranno essere disponibili dai server host Hyper-V, VMware e VMM:

|**URL** | **VMM tooVMM** | **VMM tooAzure** | **TooAzure Hyper-V** | **VMware tooAzure** |
|--- | --- | --- | --- | --- |
|``*.accesscontrol.windows.net`` | CONSENTI | Consenti | Consenti | Consenti |
|``*.backup.windowsazure.com`` | Facoltativo | Consenti | Consenti | Consenti |
|``*.hypervrecoverymanager.windowsazure.com`` | Consenti | Consenti | Consenti | Consenti |
|``*.store.core.windows.net`` | Consenti | Consenti | Consenti | Consenti |
|``*.blob.core.windows.net`` | Facoltativo | Consenti | Consenti | Consenti |
|``https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi`` | Facoltativo | Facoltativo | Facoltativo | Consentire download SQL |
|``time.windows.com`` | Consenti | Consenti | Consenti | Consenti|
|``time.nist.gov`` | Consenti | Consenti | Consenti | CONSENTI |
