---
title: le macchine virtuali VMware aaaReplicate e server fisici tooAzure nel portale classico di hello | Documenti Microsoft
description: In questo articolo viene descritto come toodeploy Azure Site Recovery tooorchestrate replica, il failover e ripristino di locale macchine virtuali VMware e tooAzure server fisici Windows/Linux.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: a9022c1f-43c1-4d38-841f-52540025fb46
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: raynew
ROBOTS: NOINDEX, NOFOLLOW
redirect_url: site-recovery-vmware-to-azure
ms.openlocfilehash: f85e4139ad45552ce963072e14d71d279bb7dac9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-virtual-machines-and-physical-servers-tooazure-with-azure-site-recovery"></a>Replica delle macchine virtuali VMware e server fisici tooAzure con Azure Site Recovery
> [!div class="op_single_selector"]
> * [Hello portale di Azure](site-recovery-vmware-to-azure.md)
> * [portale classico Hello](site-recovery-vmware-to-azure-classic.md)
> * [portale classico Hello (legacy)](site-recovery-vmware-to-azure-classic-legacy.md)
>
>

servizio Azure Site Recovery Hello contribuisce tooyour continuità aziendale e strategia di ripristino di emergenza gestendo la replica, il failover e il ripristino delle macchine virtuali e server fisici. Computer possono essere replicati tooAzure o data center di tooa secondario in locale. Per una panoramica rapida, vedere [Che cos'è Azure Site Recovery?](site-recovery-overview.md)

## <a name="overview"></a>Panoramica
Questo articolo illustra come:

* **Replicare tooAzure macchine virtuali VMware**: distribuire Site Recovery toocoordinate replica, il failover e recupero di spazio di archiviazione tooAzure macchine virtuali VMware in locale.
* **La replica di server fisici tooAzure**: distribuire Azure Site Recovery toocoordinate replica, il failover e ripristino di tooAzure server Windows e Linux fisica locale.

> [!NOTE]
> Questo articolo viene descritto come tooreplicate tooAzure. Se si desidera tooreplicate Windows/Linux o macchine virtuali VMware server fisici tooa Data Center secondario, vedere [tooVMware VMware di ripristino del sito](site-recovery-vmware-to-vmware.md).
>
>

Inviare eventuali commenti o domande nella parte inferiore di hello di questo articolo o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="enhanced-deployment"></a>Distribuzione avanzata
In questo articolo sono incluse istruzioni per una distribuzione avanzata nel portale di Azure classico hello. È consigliabile usare questa versione per tutte le nuove distribuzioni. Se già stato distribuito da utilizzando hello versioni legacy, è consigliabile eseguire la migrazione toohello nuova versione. Per ulteriori informazioni sulla migrazione, vedere [VMware di ripristino del sito tooAzure classica legacy](site-recovery-vmware-to-azure-classic-legacy.md#migrate-to-the-enhanced-deployment).

distribuzione avanzata di Hello è un aggiornamento importante. Di seguito è riportato un riepilogo che sono stati apportati miglioramenti di hello:

* **Macchine virtuali in Azure senza infrastruttura**: i dati vengono replicati direttamente tooan account di archiviazione Azure. Inoltre, non è tooset alcuna necessità di un'infrastruttura di macchine virtuali (come server di configurazione o il server di destinazione master) per la replica e failover in base alle esigenze stato distribuzione legacy hello.  
* **Installazione unificata**: un'unica installazione garantisce la scalabilità per i componenti locali e ne semplifica la configurazione.
* **Distribuzione sicura**: tutto il traffico viene crittografato e le comunicazioni relative alla gestione della replica vengono inviate tramite HTTPS 443.
* **Punti di ripristino**: supporto per punti di ripristino per l'arresto anomalo del sistema e coerenti con l'applicazione per ambienti Windows e Linux. Sono supportate configurazioni coerenti con VM singole e multiple.
* **Failover di test**: supporto per tooAzure di failover di test non comportano interruzioni del servizio senza influire sulla produzione o la sospensione di replica.
* **Failover non pianificato**: supporto per il failover non pianificato tooAzure con un'opzione avanzata di tooautomatically arresta le macchine virtuali prima del failover.
* **Il failback**: failback integrato che consente di replicare solo le modifiche delta di eseguire il backup toohello sito locale.
* **vSphere 6.0**: supporto limitato per le distribuzioni di VMware vSphere 6.0.

## <a name="how-does-site-recovery-help-protect-virtual-machines-and-physical-servers"></a>Azure Site Recovery contribuisce alla protezione di macchine virtuali e server fisici
* Gli amministratori di VMware possono configurare le misure di sicurezza di una posizione esterna tooprotect Azure da carichi di lavoro di business e applicazioni in esecuzione su macchine virtuali VMware. Server Manager consente di replicare tooAzure di server di Windows e Linux fisica locale.
* console di Azure Site Recovery Hello fornisce un'unica posizione per semplificare l'installazione e la gestione della replica, il failover e processi di ripristino.
* Se si esegue la replica di macchine virtuali VMware gestite da un server vCenter, Site Recovery può rilevare automaticamente le macchine virtuali. Se i computer fanno parte di un host ESXi, il ripristino del sito individua le macchine virtuali nell'host di hello.
* Se si eseguono i failover facili dal tooAzure infrastruttura locale, è possibile eseguire il backup (ripristino) dai server di VM Azure tooVMware hello nel sito locale.
* È possibile configurare piani di ripristino che raggruppano i carichi di lavoro delle applicazioni a più livelli su più macchine. Se si esegue il failover tali piani, il ripristino del sito fornisce la coerenza tra più macchine in modo che i computer che eseguono hello carichi di lavoro possono essere ripristinati contemporaneamente tooa dati coerenti a punto.

## <a name="supported-operating-systems"></a>Sistemi operativi supportati
### <a name="windows-64-bit-only"></a>Windows (solo 64 bit)
* Windows Server 2008 R2 SP1+
* Windows Server 2012
* Windows Server 2012 R2

### <a name="linux-64-bit-only"></a>Linux (solo versione a 64 bit)
* Red Hat Enterprise Linux 6.7, 7.1 e 7.2
* CentOS 6.5, 6.6, 6.7, 7.0, 7.1 e 7.2
* Kernel compatibile di Oracle Enterprise Linux versione 6.4 e in esecuzione uno hello Red Hat 6.5 o non interrompibile Enterprise Kernel versione 3 (UEK3)
* SUSE Linux Enterprise Server 11 SP3

## <a name="scenario-architecture"></a>Architettura dello scenario
Componenti dello scenario:

* **Un server di gestione locale**: il server di gestione di hello esegue i componenti di Site Recovery:
  * **Server di configurazione**: coordina le comunicazioni e gestisce i processi di ripristino e replica dei dati.
  * **Server di elaborazione**: agisce come un gateway di replica. Riceve dati dal computer di origine protetta; ottimizzata con la memorizzazione nella cache, la compressione e crittografia; e invia la replica dei dati tooAzure archiviazione. Inoltre gestisce l'installazione push del computer tooprotected del servizio di mobilità e la esegue l'individuazione automatica delle macchine virtuali VMware.
  * **Server di destinazione master**: gestisce i dati di replica durante il failback da Azure.
    È inoltre possibile distribuire un server di gestione che funge da solo un tooscale di processo server della distribuzione.
* **servizio di mobilità Hello**: questo componente viene distribuito in ogni computer che si desidera tooreplicate tooAzure (VMware VM o server fisico). Scrive dati nel computer di hello acquisisce e li inoltra toohello server di elaborazione.
* **Azure**: non è necessario toocreate qualsiasi replica toohandle macchine virtuali di Azure e il failover. Hello servizio Site Recovery gestisce la gestione dei dati e i dati vengono replicati direttamente tooAzure archiviazione. Macchine virtuali di Azure replicate sono riattivate automaticamente solo quando si verifica il failover tooAzure. Tuttavia, se si desidera toofail dal sito locale toohello Azure, è necessario tooset backup tooact una macchina virtuale di Azure come un server di elaborazione.

Hello seguente immagine (creato dal Henry Robalino) viene illustrato come questi componenti interagiscono:

![Architettura dei componenti](./media/site-recovery-vmware-to-azure/v2a-architecture-henry.png)

## <a name="capacity-planning"></a>Pianificazione della capacità
Quando la pianificazione della capacità, ecco cosa occorre toothink su:

* **ambiente di origine Hello**: pianificazione o hello VMware infrastructure e origine macchina i requisiti di capacità.
* **il server di gestione di Hello**: per hello Gestione server locali che eseguono i componenti di Site Recovery la pianificazione.
* **Larghezza di banda di rete da origine tootarget**: pianificazione della larghezza di banda di rete necessario per la replica tra origine hello e Azure.

### <a name="source-environment-considerations"></a>Considerazioni relative all'ambiente di origine
* **Frequenza di modifica giornaliera massima**: una macchina protetta può usare un solo server di elaborazione. Un server singolo processo può gestire backup too2 modificare TB di dati al giorno. 2 TB è pertanto dati giornaliera massima hello modificare frequenza con cui è supportato per un computer protetto.
* **Velocità effettiva massima**: un computer replicato può appartenere tooone account di archiviazione in Azure. Un account di archiviazione standard può gestire un massimo di 20.000 richieste al secondo, si consiglia di mantenere numero hello di operazioni IOPS tra un too20 macchina di origine, 000. Ad esempio, se si dispone di una macchina di origine con 5 dischi e ogni disco genera 120 IOPS (dimensioni di 8 KB) nell'origine hello, sarà all'interno di hello Azure limite di IOPS disco pari a 500. numero di account di archiviazione richiesto Hello = origine totale IOPs/20, 000.

### <a name="management-server-considerations"></a>Considerazioni relative al server di elaborazione
il server di gestione di Hello esegue i componenti di Site Recovery che gestiscono l'ottimizzazione di dati, replica e la gestione. Deve essere capacità di frequenza giornaliera modifica di toohandle in grado di hello in tutti i carichi di lavoro in esecuzione nel computer protetto, e ha la replica di archiviazione dei dati tooAzure toocontinuously della larghezza di banda sufficiente. In particolare:

* il server di elaborazione di Hello riceve i dati di replica da macchine virtuali protette e ottimizzata con la memorizzazione nella cache, la compressione e crittografia prima di inviarlo tooAzure. server di gestione di Hello deve disporre di sufficienti risorse tooperform queste attività.
* server di elaborazione Hello Usa cache basata su disco. Si consiglia di un disco separato della cache di 600 GB o più modifiche di dati toohandle archiviate nell'evento hello del collo di bottiglia di rete o di interruzione. Durante la distribuzione, è possibile configurare cache di hello in qualsiasi unità con almeno 5 GB di spazio di archiviazione disponibile, ma 600 GB è raccomandazione minimo hello.
* Come procedura consigliata, si consiglia di tale server di gestione di hello si trova in hello stessa rete e segmento LAN come hello macchine da tooprotect. Sono reperibili in una rete diversa, ma si desidera tooprotect devono avere L3 rete visibilità tooit macchine.

Nella hello nella tabella seguente sono riepilogati i suggerimenti di dimensioni per il server di gestione di hello:

| **CPU del server di gestione** | **Memoria** | **Dimensione disco cache** | **Frequenza di modifica dei dati** | **Computer protetti** |
| --- | --- | --- | --- | --- |
| 8 vCPU (2 socket * 4 core a 2,5 GHz) |16 GB |300 GB |500 GB o inferiore |Distribuire un server di gestione con queste impostazioni di tooreplicate meno di 100 macchine. |
| 12 vCPU (2 socket * 6 core a 2,5 GHz) |18 GB |600 GB |500 GB too1 TB |Distribuire un server di gestione con le macchine di 100-150 tooreplicate queste impostazioni. |
| 16 vCPU (2 socket * 8 core a 2,5 GHz) |32 GB |1 TB |1 TB too2 TB |Distribuire un server di gestione con le macchine 150 e 200 tooreplicate queste impostazioni. |
| Distribuire un altro server di elaborazione | | |Superiore a 2 TB |Distribuire i server di elaborazione aggiuntive se si esegue la replica di più di 200 macchine, o se i dati giornalieri hello modifica frequenza supera i 2 TB. |

Dove:

* Ogni computer di origine è configurato con 3 dischi da 100 GB.
* La risorsa di archiviazione di benchmarking usata per le misurazioni del disco della cache è di 8 unità SAS a 10.000 RPM con RAID 10.

### <a name="network-bandwidth-from-source-tootarget"></a>Larghezza di banda di rete da origine tootarget
Verificare che il calcolo della larghezza di banda hello che sarebbe richiesto per la replica differenziale e la replica iniziale usando hello [dello strumento di pianificazione delle capacità](site-recovery-capacity-planner.md).

#### <a name="throttling-bandwidth-used-for-replication"></a>Limitazione della larghezza di banda usata per la replica
VMware traffico replicato tooAzure passa attraverso un server di processo specifico. È possibile limitare hello larghezza di banda disponibile per la replica di ripristino del sito su tale server come indicato di seguito:

1. Aprire hello snap-in MMC di Microsoft Azure Backup nel server di gestione principale hello o in un server di gestione in esecuzione aggiuntive provisioning server di elaborazione. Per impostazione predefinita, viene creato un collegamento per il Backup di Microsoft Azure sul desktop hello. In alternativa passare a C:\Program Files\Microsoft Azure Recovery Services Agent\bin\wabadmin.
2. Hello nello snap-in, fare clic su **Modifica proprietà**.

    ![Modificare le proprietà della limitazione della larghezza di banda](./media/site-recovery-vmware-to-azure-classic/throttle1.png)
3. In hello **limitazione** , specificare la larghezza di banda hello che può essere utilizzato per la replica di Site Recovery e hello pianificazione applicabile.

    ![Limitare la larghezza di banda per la replica](./media/site-recovery-vmware-to-azure-classic/throttle2.png)

È possibile impostare la limitazione usando PowerShell. Ad esempio:

    Set-OBMachineSetting -WorkDay $mon, $tue -StartWorkHour "9:00:00" -EndWorkHour "18:00:00" -WorkHourBandwidth (512*1024) -NonWorkHourBandwidth (2048*1024)

#### <a name="maximizing-bandwidth-usage"></a>Ottimizzazione dell'utilizzo della larghezza di banda
tooincrease hello della larghezza di banda utilizzata per la replica da Azure Site Recovery, è necessario toochange una chiave del Registro di sistema.

Hello seguenti controlli chiavi hello numero di thread per la replica su disco utilizzato per la replica:

    HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Replication\UploadThreadsPerVM

 In una rete di provisioning eccessivo, questa chiave del Registro di sistema deve toobe modificato da valori predefiniti. Il numero massimo supportato è 32.  

Per altre informazioni sulla pianificazione dettagliata della capacità, vedere [Site Recovery Capacity Planner](site-recovery-capacity-planner.md).

### <a name="additional-process-servers"></a>Server di elaborazione aggiuntivi
Se è necessario tooprotect più di 200 macchine o tasso di modifica giornaliero è maggiore di 2 TB, è possibile aggiungere ulteriori server toohandle hello carico. tooscale out, è possibile:

* Aumentare il numero di hello del server di gestione. Ad esempio, è possibile proteggere le macchine too400 con due server di gestione.
* Aggiungere i server di elaborazione aggiuntive e utilizzare questi server di gestione toohandle hello traffico anziché (o in aggiunta a).

Questa tabella descrive uno scenario in cui:

* Impostare hello originale toouse server di gestione come server di configurazione.
* Viene configurato un server di elaborazione aggiuntivo.
* Per configurare le macchine virtuali protette toouse hello processo aggiuntivo server.
* Ogni computer di origine protetto è configurato con tre dischi da 100 GB.

| **Server di gestione originale**<br/><br/>(server di configurazione) | **Server di elaborazione aggiuntivo** | **Dimensione disco cache** | **Frequenza di modifica dei dati** | **Computer protetti** |
| --- | --- | --- | --- | --- |
| 8 vCPU (2 socket * 4 core a 2,5 GHz), 16 GB di RAM |4 vCPU (2 socket * 2 core a 2,5 GHz), 8 GB di RAM |300 GB |250 GB o inferiore |È possibile eseguire la replica di un massimo di 85 macchine. |
| 8 vCPU (2 socket * 4 core a 2,5 GHz), 16 GB di RAM |8 vCPU (2 socket * 4 core a 2,5 GHz), 12 GB di RAM |600 GB |250 GB too1 TB |È possibile eseguire la replica di 85-150 macchine. |
| 12 vCPU (2 socket * 6 core a 2,5 GHz), 18 GB di RAM |12 vCPU (2 socket * 6 core a 2,5 GHz), 24 GB di RAM |1 TB |1 TB too2 TB |È possibile eseguire la replica di 150-225 macchine. |

Il modo in cui i server vengono ridimensionati dipende dalle preferenze per il modello di aumento delle prestazioni o di aumento del numero di istanze. È possibile aumentare le prestazioni distribuendo alcuni server di gestione e di elaborazione avanzati. È possibile aumentare il numero di istanze distribuendo più server con minori risorse. Ad esempio: se è necessario tooprotect 220 macchine, è possibile eseguire una delle seguenti hello:

* Configurare il server di gestione originale hello con 12 Vcpu e 18 GB di RAM. Configurare un server di elaborazione aggiuntivo con 12 vCPU e 24 GB di RAM. Configurare server di elaborazione aggiuntive di macchine virtuali protette toouse solo hello.
* Configurare due server di gestione (Vcpu 2 x 8, 16 GB di RAM) e due i server di elaborazione aggiuntive (Vcpu 1x8 e 4vCPUs x 1 macchine (220) di toohandle 135 + 85). Configurare i computer protetti toouse solo hello processo aggiuntivo server.

Seguire le istruzioni hello [distribuire i server di elaborazione aggiuntive](#deploy-additional-process-servers) tooset di un server di elaborazione aggiuntive.

## <a name="before-you-start-deployment"></a>Prima di iniziare la distribuzione
Hello nelle tabelle seguenti riepilogano prerequisiti hello per questo scenario di distribuzione.

### <a name="azure-prerequisites"></a>Prerequisiti di Azure
| **Prerequisito** | **Dettagli** |
| --- | --- |
| **Account di Azure** |È necessario un account [Microsoft Azure](https://azure.microsoft.com/) . È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/). Per altre informazioni sui prezzi di Site Recovery, vedere [Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/). |
| **Archiviazione di Azure** |È necessario un toostore replicati dati dell'account di archiviazione di Azure. I dati replicati vengono memorizzati nell'archiviazione di Azure e le macchine virtuali di Azure vengono attivate quando si verifica il failover. <br/><br/>È necessario un [account di archiviazione con ridondanza geografica Standard](../storage/storage-redundancy.md#geo-redundant-storage). hello stessa area hello servizio Site Recovery ed essere associato a hello, l'account di Hello deve trovarsi nella stessa sottoscrizione. Account di archiviazione toopremium di replica non è attualmente supportato e non devono essere usate.<br/><br/>Non è supportato lo spostamento di account di archiviazione creati utilizzando hello [portale di Azure](../storage/storage-create-storage-account.md) tra gruppi di risorse. Per ulteriori informazioni, vedere [tooMicrosoft introduzione di archiviazione di Azure](../storage/storage-introduction.md).<br/><br/> |
| **Rete di Azure** |È necessario una rete virtuale di Azure che si connetteranno macchine virtuali di Azure viene eseguito il failover toowhen. Hello rete virtuale di Azure deve essere in hello stessa area dell'insieme di credenziali di Site Recovery hello.<br/><br/>toofail dopo tooAzure di failover, è necessario un VPN connessione (o Azure ExpressRoute) imposta da sito locale toohello di hello rete di Azure. |

### <a name="on-premises-prerequisites"></a>Prerequisiti locali
| **Prerequisito** | **Dettagli** |
| --- | --- |
| **Server di gestione** |È necessario un server Windows 2012 R2 locale in esecuzione in una macchina virtuale o un server fisico. Tutti i componenti di hello in locale il ripristino del sito vengono installati sul server di gestione.<br/><br/> È consigliabile che distribuire server hello come una VM VMware a disponibilità elevata. Il failback toohello nel sito locale da Azure è sempre tooVMware macchine virtuali indipendentemente dal fatto se è stato eseguito il failover le macchine virtuali o i server fisici. Se non si configura il server di gestione di hello come una VM VMware, è necessario tooset di un server di destinazione master separato come un traffico di failback tooreceive VM VMware.<br/><br/>server Hello non deve essere un controller di dominio.<br/><br/>Hello server deve disporre di un indirizzo IP statico.<br/><br/>nome di host Hello del server di hello deve essere di 15 caratteri o meno.<br/><br/>impostazioni locali del sistema operativo Hello devono essere solo in lingua inglese.<br/><br/>il server di gestione di Hello richiede l'accesso a Internet.<br/><br/>È necessario l'accesso in uscita dal server hello come segue: l'accesso temporaneo su 80 HTTP durante l'installazione dei componenti di Site Recovery hello (toodownload MySQL); accesso in uscita in corso su HTTPS 443 per la gestione di replica; in corso accesso in uscita su 9443 HTTPS per il traffico di replica (questa porta può essere modificata).<br/><br/> Verificare che questi URL sono accessibili dal server di gestione di hello: <br/>- \*.hypervrecoverymanager.windowsazure.com<br/>- \*.accesscontrol.windows.net<br/>- \*.backup.windowsazure.com<br/>- \*.blob.core.windows.net<br/>- \*.store.core.windows.net<br/>- https://www.msftncsi.com/ncsi.txt<br/>- [https://dev.MySQL.com/Get/Archives/MySQL-5.5/MySQL-5.5.37-Win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi")<br/><br/>Se si dispone di regole firewall basate sull'indirizzo IP nel server di hello, verificare che le regole di hello consentono la comunicazione tooAzure. È necessario hello tooallow [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/details.aspx?id=41653) e hello porta HTTPS (443). È necessario anche toowhitelist intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali. URL di Hello [https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi] (https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi " https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi") per il download di MySQL. |
| **VMware vCenter e host ESXi** |È necessario uno o più VMware vSphere ESX/ESXi hypervisor la gestione delle macchine virtuali VMware, che esegue ESX/ESXi versione 5.1, 6.0 o 5.5 con gli aggiornamenti più recenti di hello.<br/><br/> È consigliabile distribuire un toomanage di VMware vCenter server host ESXi. Dovrebbe essere in esecuzione vCenter versione 6.0 o 5.5 con gli aggiornamenti più recenti di hello.<br/><br/>Si noti che Site Recovery non supporta le nuove funzionalità di vCenter e vSphere 6.0 come cross-vCenter vMotion, Virtual Volumes e Storage DRS. Supporto per il ripristino del sito è limitato toofeatures che sono anche disponibili nella versione 5.5. |
| **Computer protetti** |**Azzurro**<br/><br/>Computer che si desidera tooprotect devono essere conformi ai [Azure prerequisiti](site-recovery-prereq.md) per la creazione di macchine virtuali di Azure.<br><br/>Se si desidera tooconnect toohello macchine virtuali di Azure dopo il failover, è necessario tooenable le connessioni di Desktop remoto nel firewall locale hello.<br/><br/>La capacità dei singoli dischi nei computer protetti non deve superare 1023 GB. Una macchina virtuale può essere composto too64 dischi (in questo modo i too64 TB). Se si hanno dischi di dimensioni superiori a 1 TB è consigliabile usare la replica di database, ad esempio SQL Server Always On oppure Oracle Data Guard.<br/><br/>Minimo 2 GB di spazio disponibile sull'unità di installazione di hello per l'installazione del componente.<br/><br/>I cluster guest in dischi condivisi non sono supportati. Se si ha una distribuzione in cluster è consigliabile usare la replica di database, ad esempio SQL Server Always On oppure Oracle Data Guard.<br/><br/>L'avvio UEFI (Unified Extensible Firmware Interface)/EFI (Extensible Firmware Interface) non è supportato.<br/><br/>I nomi delle macchine devono contenere da 1 a 63 caratteri, ovvero lettere, numeri e trattini. nome Hello deve iniziare con una lettera o un numero e terminare con una lettera o un numero. Dopo che un computer è protetto, è possibile modificare hello nomi di Azure.<br/><br/>**VM VMware**<br/><br>È necessario tooinstall VMware vSphere PowerCLI 6.0. nel server di gestione hello (server di configurazione).<br/><br/>Macchine virtuali VMware desiderato tooprotect deve essere installato e in esecuzione gli strumenti VMware.<br/><br/>Se l'origine hello VM con gruppo NIC, viene convertito tooa singola scheda di rete dopo il failover tooAzure.<br/><br/>Se un disco iSCSI dispongono di macchine virtuali protette, hello converte il ripristino del sito protetto disco iSCSI della macchina virtuale in un file di disco rigido virtuale in caso di failover tooAzure hello VM. Se la destinazione iSCSI sia raggiungibile da hello macchina virtuale di Azure, verrà connettersi tooiSCSI destinazione e vedere essenzialmente due dischi: disco VHD hello hello macchina virtuale di Azure e hello iSCSI disco di origine. In questo caso, è necessario toodisconnect destinazione iSCSI hello che viene visualizzato in hello sottoposte a failover macchina virtuale di Azure.<br/><br/>Per ulteriori informazioni sulle autorizzazioni utente di VMware hello richiede che il ripristino del sito, vedere [VMware autorizzazioni per l'accesso in vCenter](#vmware-permissions-for-vcenter-access).<br/><br/> **Macchine Windows Server (su VM VMware o server fisico)**<br/><br/>server Hello deve essere in esecuzione un sistema operativo a 64 bit supportato: Windows Server 2012 R2, Windows Server 2012 o Windows Server 2008 R2 con in almeno SP1.<br/><br/>sistema operativo Hello deve essere installato nell'unità C e disco del sistema operativo hello deve essere un disco di base di Windows. (hello del sistema operativo non installato su un disco dinamico di Windows.)<br/><br/>Per i computer Windows Server 2008 R2, è necessario .NET Framework 3.5.1 installato toohave.<br/><br/>È necessario un account amministratore tooprovide (deve essere un amministratore locale nel computer di Windows hello) per hello installazione hello push del servizio di mobilità nei server Windows. Se hello account è un account non di dominio, è necessario il controllo di accesso remoto nel computer locale hello toodisable. Per ulteriori informazioni, vedere [installare il servizio di mobilità hello con l'installazione push](#install-the-mobility-service-with-push-installation).<br/><br/>Site Recovery supporta VM con un disco RDM. Durante il failback, Site Recovery riutilizzerà il disco RDM hello se sono disponibili macchina virtuale di origine originale hello e il disco RDM. Se non sono disponibili, durante il failback Site Recovery crea un nuovo file VMDK per ogni disco.<br/><br/>**Computer Linux**<br/><br/>È necessario un sistema operativo a 64 bit supportato: Red Hat Enterprise Linux 6.7; Centos versione 6.5, 6.6 o 6.7; Oracle Enterprise Linux versione 6.4 o 6.5 esegue kernel compatibile di hello Red Hat o non interrompibile Enterprise Kernel Release 3 (UEK3); SUSE Linux Enterprise Server 11 SP3.<br/><br/>il file /etc/hosts nel computer protetto devono contenere voci che mappa gli indirizzi tooIP nome host locale hello associati a tutte le schede di rete. <br/><br/>Se si desidera tooconnect tooan macchina virtuale di Azure che eseguono Linux dopo il failover utilizzando Secure Shell client (ssh), assicurarsi che il servizio Secure Shell hello nel computer protetto hello è impostato toostart automaticamente all'avvio del sistema del sistema, e che le regole del firewall consentano un ssh connessione tooit.<br/><br/>Protezione può essere abilitata solo per i computer Linux con hello archiviazione seguenti: File system (EXT3 ETX4, ReiserFS, XFS); Mapper (multipath); dispositivo di software Multipath Gestione di volume (LVM2). I server fisici con archiviazione del controller HP CCISS non sono supportati. Hello ReiserFS file system è supportato solo in SUSE Linux Enterprise Server 11 SP3.<br/><br/>Site Recovery supporta VM con un disco RDM. Durante il failback per Linux, il ripristino del sito non riutilizzare il disco RDM hello. ma crea un nuovo file VMDK per ogni disco RDM corrispondente. |

Solo per una VM Linux: assicurarsi di impostare impostazione disk.enableUUID=true hello in hello parametri di configurazione di macchina virtuale in VMware hello. Se questa riga non esiste, aggiungerla Si tratta di tooprovide richiesto un toohello UUID coerenza VMDK, in modo che monta correttamente. Senza questa impostazione, eseguire il failback causerà un download completo anche se hello macchina virtuale è disponibile in locale. L'aggiunta di questa impostazione assicura che solo le modifiche differenziali vengano trasferite durante il failback.

## <a name="step-1-create-a-vault"></a>Passaggio 1: Creare un insieme di credenziali
1. Accedi toohello [portale di Azure](https://manage.windowsazure.com/).
2. Espandere **Servizi dati** > **Servizi di ripristino** e fare clic su **Insieme di credenziali di Site Recovery**.
3. Fare clic su **Creare nuovo** > **Creazione rapida**.
4. In **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello.
5. In **area**, selezionare hello area geografica per l'insieme di credenziali hello. aree toocheck supportati, vedere [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
6. Fare clic su **Create vault**.
    ![Crea insieme di credenziali](./media/site-recovery-vmware-to-azure-classic/quick-start-create-vault.png)

Controllare tooconfirm barra di stato hello che hello insieme di credenziali è stato creato correttamente. insieme di credenziali Hello verrà elencato come **Active** su hello principale **servizi di ripristino** pagina.

## <a name="step-2-set-up-an-azure-network"></a>Passaggio 2: Configurare una rete di Azure
Configurare una rete di Azure in modo che le macchine virtuali di Azure saranno connesse tooa rete dopo il failover in modo che il failback toohello locale sito possa funzionare come previsto.

1. Nel portale di Azure hello, selezionare **crea rete virtuale** e specificare il nome di rete hello, intervallo di indirizzi IP e nome della subnet.
2. Se è necessario eseguire il failback toodo, aggiungere la rete toohello VPN/ExpressRoute. È possibile aggiungere VPN/ExpressRoute toohello rete anche dopo il failover.

Per altre informazioni sulle reti di Azure, vedere la [panoramica sulle reti virtuali](../virtual-network/virtual-networks-overview.md).

> [!NOTE]
> [Migrazione delle reti](../azure-resource-manager/resource-group-move-resources.md) tra risorse gruppi all'interno hello stessa sottoscrizione o per le sottoscrizioni non è supportata per le reti utilizzate per la distribuzione di Site Recovery.
>
>

## <a name="step-3-install-hello-vmware-components"></a>Passaggio 3: Installare i componenti VMware hello
Se si desidera tooreplicate le macchine virtuali VMware, seguire questi passaggi nel server di gestione di hello:

1. [Scaricare](https://my.vmware.com/web/vmware/details?productId=491&downloadGroup=PCLI600R1) e installare VMware vSphere PowerCLI 6.0.
2. Riavviare il server di hello.

## <a name="step-4-download-a-vault-registration-key"></a>Passaggio 4: Scaricare una chiave di registrazione dell'insieme di credenziali
1. Dal server di gestione di hello, aprire la console di Site Recovery hello in Azure. In hello **servizi di ripristino** pagina, fare clic su hello tooopen insieme di credenziali di hello **avvio rapido** pagina. È inoltre possibile aprire hello **avvio rapido** pagina in qualsiasi momento facendo clic sull'icona di hello.

    ![Icona Avvio rapido](./media/site-recovery-vmware-to-azure-classic/quick-start-icon.png)
2. In hello **avvio rapido** pagina, fare clic su **preparare le risorse di destinazione** > **scaricare una chiave di registrazione**. file di registrazione Hello viene generato automaticamente. È valido cinque giorni dopo essere stato generato.

## <a name="step-5-install-hello-management-server"></a>Passaggio 5: Installare il server di gestione di hello
> [!TIP]
> Verificare che questi URL sono accessibili dal server di gestione di hello:
>
> * *.hypervrecoverymanager.windowsazure.com
> * *.accesscontrol.windows.net
> * *.backup.windowsazure.com
> * *.blob.core.windows.net
> * *.store.core.windows.net
> * https://dev.mysql.com/get/archives/mysql-5.5/mysql-5.5.37-win32.msi
> * https://www.msftncsi.com/ncsi.txt
>
>



>[!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Setup-Registration/player]



1. In hello **avvio rapido** pagina, scaricare file toohello server di installazione unificata hello.
2. Eseguire il programma di installazione di hello installazione file toostart in hello **installazione unificata di Site Recovery** procedura guidata.
3. In **prima di iniziare**selezionare **installare server di configurazione hello e server di elaborazione**.

   ![Prima di iniziare](./media/site-recovery-vmware-to-azure-classic/combined-wiz1.png)
4. In **licenza Software di terze parti**, fare clic su **accetto** toodownload e installare MySQL.

    ![Software di terze parti](./media/site-recovery-vmware-to-azure-classic/combined-wiz105.PNG)
5. In **registrazione**individuare e selezionare una chiave di registrazione hello scaricato dall'insieme di credenziali hello.

    ![Registrazione](./media/site-recovery-vmware-to-azure-classic/combined-wiz3.png)
6. In **impostazioni Internet**, specificare la modalità provider hello in esecuzione nel server di configurazione hello si connetteranno tooAzure Site Recovery tramite Internet hello.

   * Se si desidera tooconnect proxy hello che è attualmente configurato nel computer di hello, selezionare **Connetti con impostazioni proxy esistenti**.
   * Se si desidera hello provider tooconnect direttamente, selezionare **Connetti direttamente senza un proxy**.
   * Selezionare se hello esistente proxy richiede l'autenticazione, o se si desidera toouse un proxy personalizzato per la connessione al provider di hello, **Connetti con impostazioni proxy personalizzate**.
     * Se si utilizza un proxy personalizzato, è necessario credenziali, porta e indirizzo hello toospecify.
     * Se si utilizza un proxy, deve aver già consentito hello URL seguenti:
       * *.hypervrecoverymanager.windowsazure.com    
       * *.accesscontrol.windows.net
       * *.backup.windowsazure.com
       * *.blob.core.windows.net
       * *. store.core.windows.net

    ![Firewall](./media/site-recovery-vmware-to-azure-classic/combined-wiz4.png)

1. In **controllo dei prerequisiti**, il programma di installazione viene eseguito un toomake controllo assicura che vengano eseguite l'installazione di hello.

    ![Prerequisiti](./media/site-recovery-vmware-to-azure-classic/combined-wiz5.png)

     Se viene visualizzato un avviso su hello **controllo sincronizzazione globale**, verificare che ora hello clock di sistema hello (**data e ora** impostazioni) hello stesso fuso orario hello.

     ![Problema di sincronizzazione dell'ora](./media/site-recovery-vmware-to-azure-classic/time-sync-issue.png)

1. In **configurazione MySQL**, creare le credenziali per la firma nell'istanza di server MySQL toohello che verrà installato.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz6.png)
2. In **dettagli sull'ambiente**selezionare se si ha intenzione di macchine virtuali VMware tooreplicate. In caso affermativo, il programma di installazione verifica se è installato PowerCLI 6.0.

    ![MySQL](./media/site-recovery-vmware-to-azure-classic/combined-wiz7.png)
3. In **Install Location**, selezionare dove si desidera che i file binari hello tooinstall e archiviazione la cache di hello. È possibile selezionare un'unità con almeno 5 GB di spazio su disco disponibile, ma è consigliabile usare un'unità cache con almeno 600 GB di spazio disponibile.

   ![Percorso di installazione](./media/site-recovery-vmware-to-azure-classic/combined-wiz8.png)
4. In **Selezione rete**, specificare hello listener (scheda di rete e porta SSL) su cui hello del server di configurazione verrà inviare e ricevere dati di replica. È possibile modificare l'impostazione predefinita di hello porta (9443). Nella porta toothis aggiunta, la porta 443 verrà utilizzata da un server web che gestisce le operazioni di replica. Non usare la porta 443 per ricevere il traffico di replica.

    ![Selezione rete](./media/site-recovery-vmware-to-azure-classic/combined-wiz9.png)



1. In **riepilogo**, esaminare le informazioni di hello e fare clic su **installare**. Al termine dell'installazione verrà generata una passphrase. Sarà necessaria quando si abilita la replica, quindi copiarla e conservarla in un luogo sicuro.

   ![Riepilogo](./media/site-recovery-vmware-to-azure-classic/combined-wiz10.png)


> [!WARNING]
> Hello proxy agente servizi di ripristino di Microsoft Azure deve essere configurato.
> Al termine dell'installazione hello, avviare Shell di Microsoft Azure Recovery Services hello dal menu Start di Windows hello. Nella finestra di comando hello visualizzata, eseguire hello seguente set di comandi tooset le impostazioni del server proxy hello.
>
>
    $pwd = ConvertTo-SecureString -String ProxyUserPassword
    Set-OBMachineSetting -ProxyServer http://myproxyserver.domain.com -ProxyPort PortNumb – ProxyUserName domain\username -ProxyPassword $pwd
    net stop obengine
    net start obengine
>


### <a name="run-setup-from-hello-command-line"></a>Eseguire il programma di installazione dalla riga di comando hello
È anche possibile eseguire guidata unificata hello dalla riga di comando hello, come indicato di seguito:

    UnifiedSetup.exe [/ServerMode <CS/PS>] [/InstallDrive <DriveLetter>] [/MySQLCredsFilePath <MySQL credentials file path>] [/VaultCredsFilePath <Vault credentials file path>] [/EnvType <VMWare/NonVMWare>] [/PSIP <IP address toobe used for data transfer] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>]

Dove:

* /ServerMode: obbligatorio. Specifica se l'installazione hello deve installare il server di configurazione e processo hello o hello processo solo server (server di processo aggiuntivo tooinstall utilizzato). Valori di input: CS, PS.
* InstallDrive. Obbligatorio. Specifica cartella hello in cui sono installati i componenti di hello.
* /MySQLCredFilePath. Obbligatorio. Specifica hello percorso tooa file in cui sono archiviate le credenziali del server MySQL hello. Ottenere file hello toocreate di hello del modello.
* /VaultCredFilePath. Obbligatorio. Percorso del file di credenziali di hello insieme di credenziali.
* /EnvType: Obbligatorio. Tipo di installazione. Valori: VMware, NonVMware.
* /PSIP e /CSIP. Obbligatorio. Indirizzo IP del server di elaborazione hello e server di configurazione.
* /PassphraseFilePath. Obbligatorio. Percorso del file passphrase hello.
* /ByPassProxy. Facoltativo. Specifica i server di gestione hello che si connette tooAzure senza un proxy.
* /ProxySettingsFilePath: Facoltativo. Specifica le impostazioni per un proxy personalizzato (proxy predefinito nel server di hello che richiede l'autenticazione) o proxy personalizzato.

## <a name="step-6-set-up-credentials-for-hello-vcenter-server"></a>Passaggio 6: Configurare le credenziali per hello vCenter server
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Discovery/player]
>
>

server di elaborazione Hello può individuare automaticamente le macchine virtuali VMware gestite da un server vCenter. Per l'individuazione automatica, il ripristino del sito è necessario un account e le credenziali che possono accedere hello vCenter server. Questa istruzione non si applica se si esegue solo la replica di server fisici.

account di hello tooset e le credenziali:

1. Nel server vCenter hello, creare un ruolo (**Azure_Site_Recovery**) a livello di vCenter hello con hello [delle autorizzazioni necessarie](#vmware-permissions-for-vcenter-access).
2. Assegnare hello **Azure_Site_Recovery** utente vCenter tooa di ruolo.

   > [!NOTE]
   > Un account utente vCenter con ruolo di sola lettura hello è possibile eseguire il failover senza arrestare il computer di origine protetta. Se si desidera tooshut tali macchine, è necessario hello Azure_Site_Recovery ruolo. Se si esegue solo la migrazione di macchine virtuali da VMware tooAzure e non è necessario toofail nuovamente, il ruolo di sola lettura hello è sufficiente.
   >
   >
3. account di hello tooadd, aprire **cspsconfigtool**. È disponibile come collegamento sul desktop hello e si trova nella cartella \home\svsystems\bin hello [percorso di installazione].
4. In hello **Gestisci account** scheda, fare clic su **Aggiungi Account**.

    ![Aggiungi account](./media/site-recovery-vmware-to-azure-classic/credentials1.png)
5. In **dettagli Account**, aggiungere le credenziali che possono essere utilizzati tooaccess hello vCenter server. Può richiedere più di 15 minuti per hello account nome tooappear nel portale di hello. tooupdate immediatamente, fare clic su **aggiornamento** su hello **server di configurazione** scheda.

    ![Dettagli](./media/site-recovery-vmware-to-azure-classic/credentials2.png)

## <a name="step-7-add-vcenter-servers-and-esxi-hosts"></a>Passaggio 7: Aggiungere server vCenter e host ESXi
Se si esegue la replica di macchine virtuali VMware, è necessario un server vCenter tooadd (o host ESXi).

1. In hello **server** > **server di configurazione** , selezionare **Aggiungi vCenter server**.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter1.png)
2. Aggiungere server vCenter hello o dettagli host ESXi, nome hello di hello che l'account specificato tooaccess hello vCenter server nel passaggio precedente hello e server di elaborazione hello che verrà utilizzato toodiscover le macchine virtuali VMware gestite dal server vCenter hello. server vCenter Hello o host ESXi deve trovarsi nella stessa rete server hello in cui hello è installato il server di processo hello.

   > [!NOTE]
   > Se si sta aggiungendo server vCenter hello o host ESXi con un account che non dispone dei privilegi di amministratore nel server vCenter o l'host di hello, assicurarsi che vCenter hello o ESXi account dispone di questi privilegi abilitati: Data Center, l'archivio dati, cartella, Jost, rete, Risorsa macchina virtuale e vSphere Switch distribuiti. server vCenter Hello deve hello archiviazione viste privilegio abilitato.
   >
   >

    ![Aggiungere il server vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter2.png)
3. Al termine dell'individuazione, server vCenter hello verrà elencata nella hello **server di configurazione** scheda.

    ![vCenter](./media/site-recovery-vmware-to-azure-classic/add-vcenter3.png)

## <a name="step-8-create-a-protection-group"></a>Passaggio 8: Creare un gruppo di protezione
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Protection/player]
>
>

I gruppi di protezione sono raggruppamenti logici di macchine virtuali o i server fisici che si desidera tooprotect utilizzando hello stesse impostazioni di protezione. Si applica a gruppo protezione dati tooa le impostazioni di protezione e tali impostazioni vengono applicate tooall macchine (virtuali o fisiche) che si aggiunge il gruppo di toohello.

1. Andare troppo**elementi protetti** > **gruppo protezione dati** e fare clic sull'icona di hello tooadd un gruppo protezione dati.

    ![Crea gruppo di protezione](./media/site-recovery-vmware-to-azure-classic/protection-groups1.png)
2. In hello **specifica le impostazioni del gruppo di protezione** , specificare un nome per il gruppo di hello. In hello **da** elenco a discesa, il server di configurazione selezionare hello in cui si desidera che il gruppo di hello toocreate. **Destinazione** è Microsoft Azure.

    ![Impostazioni del gruppo di protezione](./media/site-recovery-vmware-to-azure-classic/protection-groups2.png)
3. In hello **specificare le impostazioni di replica** pagina, configurare le impostazioni di replica hello che verranno utilizzate per tutte le macchine hello gruppo hello.

    ![Replica del gruppo di protezione](./media/site-recovery-vmware-to-azure-classic/protection-groups3.png)

   * **La coerenza Multi VM**: se si attiva questa, crea punti di ripristino coerenti con l'applicazione condivisa tra più computer hello in gruppo protezione dati hello. Questa impostazione è molto utile quando sono in esecuzione tutti i computer nel gruppo protezione dati hello hello stesso carico di lavoro. Tutti i computer sarà ripristinato toohello stesso punto dati. Questa opzione è disponibile sia per la replica di macchine virtuali VMware che per la replica di server fisici Windows o Linux.
   * **Soglia RPO**: set hello RPO. Quando replica per la protezione dati continui hello supera valore di soglia RPO hello configurata, vengono generati avvisi.
   * **Conservazione del punto di ripristino**: Specifica il periodo di memorizzazione hello. Macchine virtuali protette possono essere ripristinati tooany punto all'interno di questa finestra.
   * **Frequenza snapshot coerenti con l'applicazione**: specifica con quale frequenza verranno creati i punti di ripristino contenenti snapshot coerenti con l'applicazione.

Quando si seleziona hello segno di spunta, viene creato un gruppo protezione dati con nome hello specificato. Inoltre, in cui viene creato un secondo gruppo di protezione dati con nome hello *nome del gruppo protezione dati*- Failback. Questo gruppo protezione dati viene utilizzato se non si toohello indietro nel sito locale dopo il failover tooAzure. È possibile monitorare i gruppi protezione dati hello che vengono creati in hello **elementi protetti** pagina.

## <a name="step-9-install-hello-mobility-service"></a>Passaggio 9: Installare il servizio di mobilità hello
Hello primo passaggio per abilitare la protezione per le macchine virtuali e server fisici è servizio di mobilità tooinstall hello. Questa operazione può essere eseguita in due modi:

* Push e installare il servizio hello in ogni computer dal server di elaborazione hello automaticamente. Quando si aggiunta gruppo protezione dati tooa di computer e è già in esecuzione una versione appropriata di hello servizio di mobilità, non si verifica l'installazione push. È possibile installare anche automaticamente servizio hello usando il metodo push di enterprise, ad esempio Windows Server Update Services o System Center Configuration Manager. Assicurarsi di che aver configurato il server di gestione di hello prima di procedere.
* Installare manualmente il servizio hello in ogni computer che si desidera tooprotect. Assicurarsi di che aver configurato il server di gestione di hello prima di procedere.

### <a name="install-hello-mobility-service-with-push-installation"></a>Installare il servizio di mobilità hello con l'installazione push
Quando si aggiunge a gruppo di protezione dati tooa macchine, hello servizio di mobilità viene automaticamente inserito e installata in ogni computer da server di elaborazione hello.

#### <a name="prepare-for-automatic-push-on-windows-machines"></a>Preparare il push automatico nei computer Windows
computer che eseguono Windows tooprepare in modo che il servizio di mobilità di hello può essere installato automaticamente dal server di elaborazione hello:

1. Creare un account di che tale server di elaborazione hello è possibile utilizzare macchina hello tooaccess. account di Hello deve disporre dei privilegi di amministratore (locale o dominio). Queste credenziali vengono utilizzate solo per l'installazione push del servizio di mobilità hello.

   > [!NOTE]
   > Se non si utilizza un account di dominio, è necessario il controllo di accesso remoto nel computer locale hello toodisable. toodo, nel Registro di sistema hello HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System, aggiungere la voce DWORD hello LocalAccountTokenFilterPolicy con un valore pari a 1 in. voce del Registro di sistema di hello tooadd da CLI comando Apri o usando PowerShell, immettere  **`REG ADD HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System /v LocalAccountTokenFilterPolicy /t REG_DWORD /d 1`** .
   >
   >
2. Per Windows Firewall nel computer di hello che si desidera tooprotect, selezionare **Consenti app o funzionalità attraverso Firewall**e abilitare **condivisione File e stampanti** e **gestione Windows Strumentazione**. Per i computer appartenenti al dominio tooa, è possibile configurare i criteri firewall hello con un oggetto Criteri di gruppo.

   ![Impostazioni del firewall](./media/site-recovery-vmware-to-azure-classic/mobility1.png)
3. Aggiungere account hello creato:

   * Aprire **cspsconfigtool**. È disponibile come collegamento sul desktop hello e si trova nella cartella \home\svsystems\bin hello [percorso di installazione].
   * In hello **Gestisci account** scheda, fare clic su **Aggiungi Account**.
   * Aggiungere account hello creato. Dopo aver aggiunto l'account di hello, è necessario credenziali hello tooprovide quando si aggiunge un gruppo di protezione dati tooa macchina.

#### <a name="prepare-for-automatic-push-on-linux-servers"></a>Preparare il push automatico nei server Linux
1. Verificare che tale computer Linux hello desiderato tooprotect sia supportato come descritto in [prerequisiti locale](#on-premises-prerequisites). Verificare che sia presente la connettività di rete tra computer hello desiderato tooprotect e hello server di gestione che esegue il server di elaborazione hello.
2. Creare un account di che tale server di elaborazione hello è possibile utilizzare macchina hello tooaccess. account di Hello deve essere un utente root nel server di hello origine Linux. Queste credenziali vengono utilizzate solo per l'installazione push del servizio di mobilità hello.

   * Aprire **cspsconfigtool**. È disponibile come collegamento sul desktop hello e si trova nella cartella \home\svsystems\bin hello [percorso di installazione].
   * In hello **Gestisci account** scheda, fare clic su **Aggiungi Account**.
   * Aggiungere account hello creato. Dopo aver aggiunto l'account di hello, è necessario credenziali hello tooprovide quando si aggiunge un gruppo di protezione dati tooa macchina.
3. Controllare il file /etc/hosts hello sull'origine hello Linux server contiene voci che eseguono il mapping di indirizzi di tooIP hello nome host locale associati a tutte le schede di rete.
4. Installare i pacchetti di openssh e openssh server openssl più recenti hello computer hello che si desidera tooprotect.
5. Assicurarsi che SSH sia abilitato e in esecuzione sulla porta 22.
6. Abilitare l'autenticazione SFTP di sottosistema e password nel file sshd_config hello come segue:

   * Accedere come utente ROOT.
   * Nel file /etc/ssh/sshd_config hello trovare riga hello che inizia con PasswordAuthentication.
   * Rimuovere il commento riga hello e modificare il valore di hello da **non** troppo**Sì**.
   * Riga hello di ricerca che inizia con **sottosistema** e rimuovere il commento riga hello.

     ![override default of no subsystems in Linux](./media/site-recovery-vmware-to-azure-classic/mobility2.png)

### <a name="install-hello-mobility-service-manually"></a>Installare manualmente il servizio di mobilità hello
programmi di installazione Hello sono disponibili in C:\Program Files (x86) \Microsoft Azure Site Recovery\home\svsystems\pushinstallsvc\repository.

| Sistema operativo di origine | File di installazione del servizio Mobility |
| --- | --- |
| Windows Server (solo 64 bit) |Microsoft-ASR_UA_9.*.0.0_Windows_* release.exe |
| CentOS 6.4, 6.5, 6.6 (solo 64 bit) |Microsoft-ASR_UA_9.*.0.0_RHEL6-64_*release.tar.gz |
| SUSE Linux Enterprise Server 11 SP3 (solo 64 bit) |Microsoft-ASR_UA_9.*.0.0_SLES11-SP3-64_*release.tar.gz |
| Oracle Enterprise Linux 6.4, 6.5 (solo 64 bit) |Microsoft-ASR_UA_9.*.0.0_OL6-64_*release.tar.gz |

#### <a name="install-hello-mobility-service-manually-on-a-windows-server"></a>Installare manualmente il servizio di mobilità hello in un server Windows
1. Scaricare ed eseguire l'installazione rilevanti hello.
2. In **Prima di iniziare** selezionare **Servizio Mobility**.

    ![Installazione del servizio Mobility](./media/site-recovery-vmware-to-azure-classic/mobility3.png)
3. In **i dettagli di configurazione Server**, specificare l'indirizzo IP hello hello del server di gestione e la passphrase generata durante l'installazione di componenti server di gestione hello hello. È possibile recuperare la passphrase hello eseguendo  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** nel server di gestione di hello.

    ![Servizio Mobility](./media/site-recovery-vmware-to-azure-classic/mobility6.png)
4. In **Install Location**mantenere percorso predefinito di hello e fare clic su **Avanti** toobegin installazione.
5. In **l'avanzamento dell'installazione**, verificare l'installazione e, se richiesto, riavviare il computer di hello.

È inoltre possibile installare immettendo hello seguente riga di comando di testo hello:

    UnifiedAgent.exe [/Role <Agent/MasterTarget>] [/InstallLocation <Installation Directory>] [/CSIP <IP address of CS toobe registered with>] [/PassphraseFilePath <Passphrase file path>] [/LogFilePath <Log File Path>]

In hello precedente comando:

* /Role. Obbligatorio. Specifica se deve essere installato il servizio di mobilità hello.
* /InstallLocation. Obbligatorio. Specifica dove tooinstall hello del servizio.
* /PassphraseFilePath. Obbligatorio. Specifica la passphrase di hello configurazione server.
* /LogFilePath. Obbligatorio. Specifica percorso file di programma di installazione di hello registro.

#### <a name="uninstall-hello-mobility-service-manually"></a>Disinstallare manualmente il servizio di mobilità hello
È possibile disinstallare il servizio di mobilità hello utilizzando **Disinstalla o modifica programma** nel Pannello di controllo o dalla riga di comando hello.

Hello comando toouninstall servizio di mobilità dalla riga di comando hello è:

    MsiExec.exe /qn /x {275197FC-14FD-4560-A5EB-38217F80CBD1}

#### <a name="change-hello-ip-address-of-hello-management-server"></a>Modificare l'indirizzo IP hello hello del server di gestione
Dopo aver eseguito la procedura guidata hello, è possibile modificare come indicato di seguito l'indirizzo IP hello hello del server di gestione:

1. Aprire hostconfig.exe file hello (che si trova sul desktop hello).
2. In hello **globale** scheda, modificare l'indirizzo IP hello hello del server di gestione.

   > [!NOTE]
   > Modificare solo indirizzo IP hello hello del server di gestione. il numero di porta Hello per le comunicazioni di server di gestione deve essere la porta 443, e **utilizzare HTTPS** deve essere abilitato a sinistra. Non modificare la passphrase hello.
   >
   >

    ![Indirizzo IP del server di gestione](./media/site-recovery-vmware-to-azure-classic/host-config.png)

#### <a name="install-hello-mobility-service-manually-on-a-linux-server"></a>Installare manualmente il servizio di mobilità hello in un server Linux
1. Copiare i computer Linux hello tar appropriato archivio toohello che si desidera tooprotect. Vedere la tabella hello in [installare manualmente il servizio di mobilità hello](#install-the-mobility-service-manually) toodetermine archiviare la cui tar deve utilizzare.
2. Aprire un programma shell ed estrarre percorso locale tooa archivio con estensione tar compresso hello eseguendo:`tar -xvzf Microsoft-ASR_UA_8.5.0.0*`
3. Creare un file denominato passphrase.txt in hello toowhich di directory locale è stato estratto il contenuto di hello dell'archivio tar hello. toodo, copia hello passphrase da C:\ProgramData\Microsoft Azure sito Recovery\private\connection.passphrase nel server di gestione di hello e salvarlo in passphrase.txt eseguendo  *`echo <passphrase> >passphrase.txt`*  nella shell di hello.
4. Installare il servizio di mobilità hello immettendo hello comando seguente:*`sudo ./install -t both -a host -R Agent -d /usr/local/ASR -i <IP address> -p <port> -s y -c https -P passphrase.txt`*
5. Specificare l'indirizzo IP interno hello hello del server di gestione e assicurarsi che sia selezionata la porta 443.

#### <a name="install-hello-mobility-service-from-hello-command-line"></a>Installare il servizio di mobilità hello dalla riga di comando hello

Copiare la passphrase hello C:\Program Files (x86) \InMage Systems\private\connection nel server di gestione di hello e salvarlo come "passphrase.txt" nel server di gestione di hello. Eseguire quindi hello i comandi seguenti. In questo esempio, indirizzo IP del server Gestione hello è 104.40.75.37 e hello porta HTTPS 443:

tooinstall in un server di produzione:

    ./install -t both -a host -R Agent -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt

tooinstall nel server di destinazione master hello:

    ./install -t both -a host -R MasterTarget -d /usr/local/ASR -i 104.40.75.37 -p 443 -s y -c https -P passphrase.txt


## <a name="step-10-enable-protection-for-a-machine"></a>Passaggio 10: Abilitare la protezione per un computer
protezione tooenable, aggiungere macchine virtuali e gruppo di server fisici tooa protezione dati. Prima di iniziare, tenere presente i seguenti hello se si proteggono macchine virtuali VMware:

* Le macchine virtuali VMware vengono individuate ogni 15 minuti e potrebbe richiedere più di 15 minuti per tali tooappear nel portale di Site Recovery hello dopo l'individuazione.
* Le modifiche dell'ambiente nella macchina virtuale hello (ad esempio, l'installazione degli strumenti di VMware) potrebbero richiedere anche più di 15 minuti toobe aggiornato in Site Recovery.
* È possibile controllare hello individuati ultima ora per le macchine virtuali VMware in hello **ultimo contatto in** campo per hello vCenter/ESXi di server host hello **server di configurazione** scheda.
* Se si aggiunge un Server vCenter o l'host ESXi dopo la creazione di un gruppo protezione dati, potrebbe richiedere più di 15 minuti per toorefresh portale di Azure Site Recovery hello e per macchine virtuali toobe elencati in hello **gruppo protezione dati di Aggiungi macchine tooa**la finestra di dialogo.
* Se si desidera tooproceed immediatamente e Aggiungi gruppo di protezione di macchine tooa senza attendere l'individuazione pianificata hello, evidenziare il server di configurazione di hello (selezionarla) e fare clic su **aggiornamento**.

Eseguire anche queste operazioni:

* È consigliabile progettare i gruppi di protezione in modo che rispecchino i carichi di lavoro. Ad esempio, aggiungere i computer che eseguono un'applicazione specifica di toohello nello stesso gruppo.
* Quando si aggiunge a gruppo di protezione dati tooa macchine, inserisce automaticamente il server di elaborazione hello e installa il servizio di mobilità hello se non è già installato. È necessario meccanismo di push hello toohave preparata come descritto nel passaggio precedente hello.

### <a name="add-machines-tooa-protection-group"></a>Aggiungere il gruppo di protezione di macchine tooa

1. Andare troppo**elementi protetti** > **gruppo protezione dati** > **macchine** > **aggiungere macchine** .
2. Se si proteggono macchine virtuali VMware, in **Seleziona macchine virtuali**, selezionare un server vCenter che gestisce le macchine virtuali host EXSi hello in cui vengono eseguiti (o) e quindi selezionare le macchine hello.

    ![Abilitare la protezione per le macchine virtuali](./media/site-recovery-vmware-to-azure-classic/enable-protection2.png)
3. Se si intende proteggere i server fisici, in **Seleziona macchine virtuali**aprire hello **aggiungere le macchine fisiche** procedura guidata e specificare l'indirizzo IP hello e il nome descrittivo. Selezionare quindi la famiglia di sistemi operativi hello.

   ![Abilitare la protezione dei server fisici](./media/site-recovery-vmware-to-azure-classic/enable-protection1.png)
4. In **risorse di destinazione specificare**, selezionare l'account di archiviazione hello che si sta utilizzando per la replica e consente di indicare se le impostazioni di hello devono essere utilizzate per tutti i carichi di lavoro. Gli account di archiviazione Premium non sono attualmente supportati.

   > [!NOTE]
   > Non è supportato lo spostamento di account di archiviazione creati utilizzando hello [portale di Azure](../storage/storage-create-storage-account.md) tra gruppi di risorse.                           
   > [Migrazione di account di archiviazione](../azure-resource-manager/resource-group-move-resources.md) tra risorse gruppi all'interno hello stessa sottoscrizione o per le sottoscrizioni non è supportata per gli account di archiviazione utilizzati per la distribuzione di Site Recovery.
   >
   >

    ![Configurare le impostazioni di destinazione](./media/site-recovery-vmware-to-azure-classic/enable-protection3.png)
5. In **specificare account**, selezionare account hello [impostare](#install-the-mobility-service-with-push-installation) toouse per l'installazione automatica di hello servizio di mobilità.

    ![Specificare gli account](./media/site-recovery-vmware-to-azure-classic/enable-protection4.png)
6. Fare clic su hello segno di spunta toofinish aggiunta macchine toohello protezione toostart e gruppo di replica iniziale per ogni computer.

   > [!NOTE]
   > Se l'installazione push è stata preparata, hello servizio di mobilità viene installato automaticamente nei computer che non hanno come vengono aggiunte toohello gruppo di protezione dati. Dopo aver installato il servizio di hello, un processo di protezione viene avviata e non riesce. Dopo l'errore hello, è necessario riavviare toomanually hello di ogni computer in cui è stato installato servizio di mobilità. Dopo il riavvio di hello, ricomincia il processo di protezione hello e viene eseguita la replica iniziale.
   >
   >

È possibile monitorare lo stato su hello **processi** pagina.

![Monitorare lo stato nella pagina processi hello](./media/site-recovery-vmware-to-azure-classic/enable-protection5.png)

È possibile monitorare lo stato di protezione anche in **Elementi protetti** > *nome gruppo di protezione* > **Macchine virtuali**. Al termine della replica iniziale e sincronizzazione dei dati, computer lo stato viene modificato troppo**Protected**.

![Monitorare lo stato in Elementi protetti](./media/site-recovery-vmware-to-azure-classic/enable-protection6.png)

## <a name="step-11-set-protected-machine-properties"></a>Passaggio 11: Impostare le proprietà dei computer protetti
1. Quando lo stato della macchina è **Protetto**, è possibile configurarne le proprietà di failover. In dettagli hello del gruppo protezione dati, selezionare hello hello computer e aprire **configura** scheda.
2. Il ripristino del sito vengono suggerite alcune proprietà per la macchina virtuale di Azure hello e automaticamente rileva hello locale le impostazioni di rete.

    ![Impostare le proprietà di una macchina virtuale](./media/site-recovery-vmware-to-azure-classic/vm-properties1.png)
3. È possibile modificare queste impostazioni:

   * **Nome della macchina virtuale Azure**: hello nome che verrà assegnato al computer toohello in Azure dopo il failover. nome Hello deve essere conformi ai requisiti di Azure.
   * **Dimensioni VM di Azure**: hello numero di schede di rete dipende dalle dimensioni hello specificato per una macchina virtuale di destinazione hello. Per ulteriori informazioni sulle dimensioni e le schede, vedere hello [dimensioni tabelle](../virtual-machines/linux/sizes.md). Si noti che:

     * Quando si modifica la dimensione hello di una macchina virtuale e salvare le impostazioni di hello, verrà modificato il numero di hello di schede di rete quando si apre hello **configura** hello scheda successivo. numero minimo di Hello di schede di rete nelle macchine virtuali di destinazione è uguale toohello numero minimo di schede di rete in una macchina virtuale di origine. numero massimo di Hello di schede di rete è determinato dalle dimensioni hello della macchina virtuale hello.
       * Se il numero di hello di schede di rete nel computer di origine hello è minore o uguale a toohello numero di schede di consentito per dimensioni macchina di destinazione hello, destinazione hello avrà hello origine hello stesso numero di schede.
       * Se il numero di hello di schede per la macchina virtuale di origine hello supera il numero di hello consentito per le dimensioni di destinazione hello, dimensione massima dei hello destinazione verrà utilizzato.
        Ad esempio, se un computer di origine dispone di due schede di rete e le dimensioni del computer di destinazione hello supporta quattro, nel computer di destinazione hello avrà due schede. Se il computer di origine di hello ha due schede di dimensioni di destinazione supportato hello supportano solo una, nel computer di destinazione hello avrà una sola scheda di.
     * Se macchina virtuale hello dispone di più schede di rete, tutte le schede devono essere connesso toohello stessa rete di Azure.
   * **Rete di Azure**: È necessario specificare una rete di Azure che macchine virtuali di Azure saranno connesse tooafter failover. Se non si specifica uno, hello macchine virtuali di Azure non sarà connesse tooany rete. Inoltre, è necessario toospecify una rete di Azure se si desidera toofailback da sito locale toohello Azure. Il failback richiede una connessione VPN tra una rete di Azure e una rete locale.
   * **Azure/subnet di indirizzi IP**: per ogni scheda di rete, selezionare hello di toowhich hello subnet VM di Azure devono connettersi. Si noti che se la scheda di rete hello del computer di origine hello toouse configurato un indirizzo IP statico, è possibile specificare un indirizzo IP statico per hello macchina virtuale di Azure. Se non si specifica un indirizzo IP statico verrà allocato un indirizzo IP disponibile. Se viene specificato l'indirizzo IP di destinazione hello ma è già in uso da un'altra macchina virtuale in Azure, il failover avrà esito negativo. Se la scheda di rete hello hello computer di origine è configurata toouse DHCP, è necessario DHCP come impostazione di hello per Azure.      

## <a name="step-12-create-a-recovery-plan-and-run-a-failover"></a>Passaggio 12: Creare un piano di ripristino ed eseguire un failover
> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Enhanced-VMware-to-Azure-Failover/player]
>
>

È possibile eseguire un failover per un singolo computer, oppure è possibile eseguire failover più macchine virtuali che eseguono hello stesse attività o eseguire hello stesso carico di lavoro. toofail su più computer in hello stesso tempo, è necessario aggiungerli tooa piano di ripristino.

toocreate un piano di ripristino:

1. In hello **piani di ripristino** pagina, fare clic su **Aggiungi piano di ripristino** e aggiungere un piano di ripristino. Specificare i dettagli per il piano di hello e selezionare **Azure** come destinazione di hello.

 ![Configurare un piano di ripristino](./media/site-recovery-vmware-to-azure-classic/recovery-plan1.png)
2. In **seleziona macchina virtuale**, selezionare un gruppo protezione dati e quindi selezionare le macchine nel piano di ripristino toohello tooadd gruppo hello.

 ![Aggiungi macchine virtuali.](./media/site-recovery-vmware-to-azure-classic/recovery-plan2.png)

È possibile personalizzare i gruppi del piano di toocreate hello e ordine di hello sequenza in cui le macchine nel piano di ripristino hello vengono eseguite il failover. È anche possibile aggiungere script e istruzioni per azioni manuali. Gli script possono essere creati manualmente o usando i [runbook di Automazione di Azure](site-recovery-runbook-automation.md). Per altre informazioni sulla personalizzazione dei piani di ripristino, vedere [Creare piani di ripristino](site-recovery-create-recovery-plans.md).

## <a name="run-a-failover"></a>Eseguire un failover
Prima di eseguire un failover:

* Verificare che il server di gestione di hello è in esecuzione e disponibili. In caso contrario, il failover avrà esito negativo.
* Se si esegue un failover non pianificato:

  * È consigliabile arrestare le macchine primarie prima di eseguire un failover non pianificato. In questo modo si garantisce che non si dispone di entrambe le macchine di origine e di replica hello hello in esecuzione contemporaneamente. Se si esegue la replica le macchine virtuali VMware quando si esegue un failover non pianificato, è possibile specificare che il ripristino del sito deve avvenire tooshut macchine di origine hello. A seconda dello stato hello del sito primario di hello, ciò può o potrebbe non funzionare. Per la replica di server fisici questa opzione non è disponibile.
  * Un failover non pianificato arresta la replica dei dati dalle macchine primarie per evitare il trasferimento di dati differenziali a failover iniziato.
  * Se si desidera una macchina virtuale di replica toohello tooconnect in Azure dopo il failover, abilitare connessione Desktop remoto nel computer di origine hello prima di eseguire il failover hello. Consente quindi la connessione RDP attraverso il firewall hello. Dopo il failover, è necessario anche tooallow RDP su endpoint pubblici di hello di hello macchina virtuale di Azure. Seguire [consigliate](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) tooensure utilizzabile RDP dopo un failover.

> [!NOTE]
> tooget hello migliori prestazioni quando si esegue l'operazione tooAzure un failover, assicurarsi di aver installato nel computer protetto hello hello agente di Azure. Ciò consente di avvio della macchina hello più veloce e consente di diagnosticare i problemi. Hello agente di Azure è disponibile per [Linux](https://github.com/Azure/WALinuxAgent) e [Windows](http://go.microsoft.com/fwlink/?LinkID=394789).
>
>

### <a name="run-a-test-failover"></a>Eseguire un failover di test
Eseguire un toosimulate di failover di test del failover e continuano normalmente i processi di ripristino in una rete isolata che non influisce sull'ambiente di produzione e consente la replica normale. Failover di test è initiatd sull'origine hello ed è possibile eseguirlo in due modi:

* **Non specificare una rete di Azure**: se si esegue un failover di test senza una rete, test hello verificherà che le macchine virtuali, avviare e vengono visualizzati correttamente in Azure. Macchine virtuali non saranno connesse tooan rete di Azure dopo il failover.
* **Specificare una rete di Azure**: questo tipo di failover controlla che hello intero ambiente di replica viene visualizzato come previsto e che macchine virtuali di Azure vengono connessa toohello di rete specificata.

toorun un failover di test:

1. In hello **piani di ripristino** pagina, selezionare il piano di hello e fare clic su **Failover di Test**.

 ![Selezionare il piano di hello](./media/site-recovery-vmware-to-azure-classic/test-failover1.png)
2. In **conferma Failover di Test**selezionare **Nessuno** tooindicate che non si desidera toouse una rete di Azure per hello failover di test o test di hello toowhich rete hello selezionare le macchine virtuali verranno connesse dopo il failover. Fare clic su hello segno di spunta toostart hello failover.

 ![Effettuare una selezione](./media/site-recovery-vmware-to-azure-classic/test-failover2.png)
3. Monitorare lo stato di failover su hello **processi** scheda.

 ![Monitorare lo stato](./media/site-recovery-vmware-to-azure-classic/test-failover3.png)
4. Al termine del failover hello, inoltre deve essere in grado di replica di hello toosee macchina di Azure visualizzata **macchine virtuali** in hello portale di Azure. Se si desidera tooinitiate un toohello connessione RDP macchina virtuale di Azure, è necessario tooopen porta 3389 sull'endpoint di macchina virtuale hello.
5. Dopo aver terminato, quando il failover raggiunge hello **completa** test fase, fare clic su **completamento del Test** toofinish. In **note**, registrare e salvare eventuali commenti associati hello test failover.
6. Fare clic su **hello failover di test è stato completato** tooautomatically pulire l'ambiente di test hello. Al termine, il failover di test hello visualizzerà un **completa** stato. Vengono eliminate gli elementi o macchine virtuali create automaticamente durante il failover di test hello. Se un failover di test continua a più di due settimane, viene forzato toofinish.

### <a name="run-an-unplanned-failover"></a>Eseguire un failover non pianificato
Failover non pianificato viene avviato da Azure e può essere eseguito anche se sito primario di hello non è disponibile.

1. In hello **piani di ripristino** pagina, selezionare il piano di hello e fare clic su **Failover** > **Failover non pianificato**.

 ![Selezionare il piano di hello](./media/site-recovery-vmware-to-azure-classic/unplanned-failover1.png)
2. Se si esegue la replica di macchine virtuali VMware, è possibile provare tooshut verso il basso le macchine virtuali locali. Si tratta di un'azione sforzo e failover continua se sforzo hello ha esito positivo o non. Se non viene completato, i dettagli dell'errore verranno visualizzato in hello **processi** scheda **i processi di Failover non pianificato**.

 ![Opzione per l'arresto delle macchine virtuali in locale](./media/site-recovery-vmware-to-azure-classic/unplanned-failover2.png)

 > [!NOTE]
 > Questa opzione non è disponibile se si esegue la replica di server fisici. È necessario tootry tooshut quelli verso il basso manualmente se possibile.
 >
 >

3. In **conferma Failover**verificare direzione del failover hello (tooAzure) e selezionare il punto di ripristino hello che si desidera toouse per il failover hello. Se è abilitato multi-VM durante la configurazione delle proprietà di replica, è possibile recuperare il punto di ripristino più recente coerente con l'arresto anomalo del sistema o applicazione toohello. È inoltre possibile selezionare **punto di ripristino personalizzato** toorecover tooan precedente punto nel tempo. Fare clic su hello segno di spunta toostart hello failover.

 ![Confermare la direzione del failover](./media/site-recovery-vmware-to-azure-classic/unplanned-failover3.png)
4. Attendere hello toofinish processo di failover non pianificato. È possibile monitorare lo stato di avanzamento di failover su hello **processi** scheda. Anche se si verificano errori durante il failover non pianificato, il piano di ripristino hello viene eseguito fino al completamento. È anche possibile toosee hello replica macchina di Azure visualizzata nel **macchine virtuali** in hello portale di Azure.

### <a name="connect-tooreplicated-azure-virtual-machines-after-failover"></a>Connettersi tooreplicated Azure dopo il failover le macchine virtuali
tooconnect tooreplicated macchine virtuali in Azure dopo il failover, è necessario:

- Una connessione Desktop remoto è abilitata nella macchina primaria hello.
- Windows Firewall nel computer primario hello impostare tooallow RDP.
- RDP aggiunto toohello endpoint pubblico per la macchina virtuale di Azure hello.

Per altre informazioni su questa impostazione, vedere [Troubleshooting remote desktop connection after failover using ASR](http://social.technet.microsoft.com/wiki/contents/articles/31666.troubleshooting-remote-desktop-connection-after-failover-using-asr.aspx) (Risoluzione dei problemi di Connessione Desktop remoto dopo il failover tramite ASR).

## <a name="deploy-additional-process-servers"></a>Distribuire server di elaborazione aggiuntivi
Se è necessario scalare orizzontalmente la distribuzione oltre 200 macchine di origine oppure se la frequenza di varianza totale giornaliero supera i 2 TB, è necessario volume di traffico hello toohandle server processo aggiuntivo. tooset di un server di processo aggiuntivo, controllare i requisiti di hello in [i server di elaborazione aggiuntive](#additional-process-servers), e quindi impostare il server di elaborazione hello in base toohello seguendo le istruzioni. Dopo aver configurato il server di hello, è possibile configurare toouse macchine di origine è.

### <a name="set-up-an-additional-process-server"></a>Configurare un server di elaborazione aggiuntivo
Per configurare un server di elaborazione aggiuntivo, procedere come segue:

* Eseguire hello unificata guidata tooconfigure un server di gestione come un solo server di elaborazione.
* Se si desidera la replica dei dati toomanage utilizzando solo hello nuovo server di elaborazione, è necessario toomigrate i computer protetti.

### <a name="install-hello-process-server"></a>Installare il server di elaborazione hello
1. In hello **avvio rapido** pagina, scaricare il file di installazione unificata hello per hello Installazione componenti di Site Recovery. Eseguire l'installazione.
2. In **prima di iniziare**selezionare **aggiungere processo aggiuntivo server tooscale distribuzione**.

 ![Aggiungere il server di elaborazione](./media/site-recovery-vmware-to-azure-classic/add-ps1.png)
3. Completare la procedura guidata hello come è stato fatto quando si [impostare](#step-5-install-the-management-server) il primo server di gestione hello.
4. In **i dettagli di configurazione Server**, immettere l'indirizzo IP hello hello originale del server di gestione in cui è installato il server di configurazione di hello e quindi immettere la passphrase hello. Se non si dispone di hello passphrase, eseguire  **<SiteRecoveryInstallationFolder>\home\sysystems\bin\genpassphrase.exe – n** su hello originale tooretrieve server di gestione è.

 ![Dettagli del server di configurazione](./media/site-recovery-vmware-to-azure-classic/add-ps2.png)

### <a name="migrate-machines-toouse-hello-new-process-server"></a>Eseguire la migrazione di macchine toouse hello nuovo server di elaborazione
1. Aprire **server di configurazione** > **Server** > *nome del server di gestione originale di hello*  >   **I dettagli del server**.

 ![Dettagli del server](./media/site-recovery-vmware-to-azure-classic/update-process-server1.png)
2. In hello **i server di elaborazione** elenco, selezionare **Cambia Server di elaborazione** server toohello successivo che si desidera toochange.

 ![Aggiornare il server di elaborazione hello](./media/site-recovery-vmware-to-azure-classic/update-process-server2.png)
3. Selezionare **Cambia Server di elaborazione**selezionare **il Server di elaborazione di destinazione**, e quindi selezionare hello nuovo server di gestione. Quindi gestire le macchine virtuali selezionare hello hello nuovo server di elaborazione. Fare clic su hello icona tooget informazioni sui server hello. Hello Media dello spazio è sufficiente tooreplicate ogni macchina virtuale selezionata toohello nuovo server di elaborazione è visualizzato toohelp si apportano le decisioni di carico. Fare clic su hello segno di spunta toostart replica toohello nuovo server di elaborazione.

 ![Cambia server di elaborazione hello](./media/site-recovery-vmware-to-azure-classic/update-process-server3.png)

## <a name="vmware-permissions-for-vcenter-access"></a>Autorizzazioni di VMware per l'accesso a vCenter
server di elaborazione Hello può individuare automaticamente le macchine virtuali in un server vCenter. tooperform l'individuazione automatica, è necessario un ruolo (Azure_Site_Recovery) toodefine al server vCenter hello vCenter tooallow livello Site Recovery tooaccess hello. Se solo necessario toomigrate VMware macchine tooAzure non toofailback da Azure, è possibile definire un ruolo di sola lettura che è sufficiente. Impostare le autorizzazioni di hello, come descritto in [passaggio 6: configurare le credenziali per il server vCenter hello](#step-6-set-up-credentials-for-the-vcenter-server). le autorizzazioni del ruolo Hello sono riepilogate nella hello nella tabella seguente:

| **Ruolo** | **Dettagli** | **Autorizzazioni** |
| --- | --- | --- |
| Ruolo Azure_Site_Recovery |Individuazione di macchine virtuali VMware |Assegnare i privilegi per hello v Center server:<br/><br/>Datastore (Archivio dati): Allocate space (Alloca spazio), Browse datastore (Sfoglia archivio dati), Low level file operations (Operazioni file di livello basso), Remove file (Rimuovi file), Update virtual machine files (Aggiorna file macchina virtuale)<br/><br/>Network (Rete): Network assign (Assegnazione rete)<br/><br/>Risorse: Assegnare pool tooresource macchina virtuale, migrazione spegnimento macchina virtuale, eseguire la migrazione acceso macchina virtuale<br/><br/>Tasks (Attività): Create task (Crea attività), Update task (Aggiorna attività)<br/><br/>Virtual machine (Macchina virtuale) > Configuration (Configurazione)<br/><br/>Virtual machine (Macchina virtuale) > Interact (Interagisci) > Answer question (Rispondi alla domanda), Device connection (Connessione dispositivo), Configure CD media (Configura supporto CD), Configure floppy media (Configura supporto floppy), Power off (Spegni), Power on (Accendi), VMware tools install (Installazione strumenti VMware)<br/><br/>Virtual machine (Macchina virtuale) > Inventory (Inventario) > Create (Crea), Register (Registra), Unregister (Annulla registrazione)<br/><br/>Virtual machine (Macchina virtuale) > Provisioning > Allow virtual machine download (Consenti download macchina virtuale), Allow virtual machine files upload (Consenti upload file macchina virtuale)<br/><br/>Virtual machine (Macchina virtuale) > Snapshots > Remove snapshots (Rimuovi snapshot) |
| Ruolo vCenter User |Individuazione della macchina virtuale VMware/Failover senza arresto della macchina virtuale di origine |Assegnare i privilegi per hello v Center server:<br/><br/>Oggetto di Data Center > Propaga tooChild oggetto Demand, role = sola lettura <br/><br/>utente Hello è assegnato al livello di Data Center hello e pertanto accesso tooall hello oggetti nel Data Center hello. Se si desidera accedere hello toorestrict, assegnare hello **Nessun accesso** ruolo con hello **propagare toochild** gli oggetti figlio toohello (gli host ESX, archivi dati, le macchine virtuali e reti) dell'oggetto. |
| Ruolo vCenter User |Failover e failback |Assegnare i privilegi per hello v Center server:<br/><br/>Data Center oggetto: oggetto toochild di propagazione, ruolo = Azure_Site_Recovery<br/><br/>utente Hello è assegnato a livello di Data Center e pertanto gli oggetti di access tooall hello nel Data Center hello.  Se si desidera accedere hello toorestrict, assegnare hello * * Nessun accesso * * ruolo con hello **propaga toochild oggetto** oggetto figlio di toohello (gli host ESX, archivi dati, le macchine virtuali e reti). |

## <a name="third-party-software-notices-and-information"></a>Informazioni e comunicazioni sul software di terze parti
<!--Do Not Translate or Localize-->

software Hello e in esecuzione nel firmware hello prodotto Microsoft o servizio è basato su o integra materiale proveniente dai hello progetti elencati sotto (collettivamente, "terze parti Code").  Microsoft è hello autore originale non di hello codice di terze parti.  copyright originale Hello e la licenza, in cui Microsoft ha ricevuto tale codice di terze parti, sono set specificato di seguito.

informazioni di Hello nella sezione si riferisce il codice di terze parti componenti dei progetti hello elencati di seguito. Such licenses and information are provided for informational purposes only.  Questo codice di terze parti è in corso tooyou relicensed da Microsoft in termini di hello prodotto o servizio Microsoft di licenza software Microsoft.  

informazioni di Hello nella sezione B sono per quanto riguarda i componenti del codice di terze parti che vengono eseguiti tooyou disponibili da Microsoft in condizioni di licenza originale hello.

è possibile trovare completo del file Hello in hello [Microsoft Download Center](http://go.microsoft.com/fwlink/?LinkId=529428). Microsoft reserves all rights not expressly granted herein, whether by implication, estoppel or otherwise.

## <a name="next-steps"></a>Passaggi successivi
[Altre informazioni su failback](site-recovery-failback-azure-to-vmware-classic.md) toobring le macchine di failover in esecuzione in Azure backup tooyour nell'ambiente locale.
