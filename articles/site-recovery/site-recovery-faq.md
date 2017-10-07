---
title: 'Azure Site Recovery: domande frequenti | Microsoft Docs'
description: Questo articolo illustra le domande frequenti su Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 5cdc4bcd-b4fe-48c7-8be1-1db39bd9c078
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 05/22/2017
ms.author: raynew
ms.openlocfilehash: 6d0bd2475466e5745e1f084bd2267d954d624ebd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-frequently-asked-questions-faq"></a>Azure Site Recovery: domande frequenti
In questo articolo sono riportate le domande frequenti su Azure Site Recovery. Se hai domande dopo aver letto questo articolo, pubblicare un post nel hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=hypervrecovmgr).

## <a name="general"></a>Generale
### <a name="what-does-site-recovery-do"></a>Quali sono le funzioni di Site Recovery?
Il ripristino del sito contribuisce tooyour continuità aziendale e strategia di ripristino di emergenza, da gestire e automatizzare la replica delle macchine virtuali di Azure tra le aree, macchine virtuali in locale e server fisici tooAzure e tooa macchine locali Data Center secondario. [Altre informazioni](site-recovery-overview.md)

### <a name="what-can-site-recovery-protect"></a>Quali elementi può proteggere Site Recovery?
* **Macchine virtuali di Azure**: Site Recovery può replicare qualsiasi carico di lavoro in esecuzione in una macchina virtuale di Azure supportata
* **Macchine virtuali Hyper-V**: Site Recovery può proteggere qualsiasi carico di lavoro in esecuzione in una macchina virtuale Hyper-V.
* **Server fisici**: Site Recovery può proteggere server fisici che eseguono Windows o Linux.
* **Macchine virtuali VMware**: Site Recovery può proteggere qualsiasi carico di lavoro in esecuzione in una macchina virtuale VMware.

### <a name="does-site-recovery-support-hello-azure-resource-manager-model"></a>Il ripristino del sito supporta il modello di gestione risorse di Azure hello?
Il ripristino del sito è disponibile nel portale di Azure con il supporto per Gestione risorse di hello. Il ripristino del sito supporta distribuzioni precedenti in hello portale di Azure classico. Non è possibile creare nuovi insiemi di credenziali nel portale classico hello e nuove funzionalità non sono supportate.

### <a name="can-i-replicate-azure-vms"></a>È possibile replicare le macchine virtuali di Azure?
Sì, è possibile replicare le macchine virtuali di Azure supportate tra le aree di Azure. [Altre informazioni](site-recovery-azure-to-azure.md)

### <a name="what-do-i-need-in-hyper-v-tooorchestrate-replication-with-site-recovery"></a>Cosa è necessario in replica tooorchestrate Hyper-V con il ripristino del sito?
Per i server host Hyper-V di hello è necessario dipende dallo scenario di distribuzione hello. Estrarre hello prerequisiti di Hyper-V in:

* [La replica delle macchine virtuali Hyper-V (senza VMM) tooAzure](site-recovery-hyper-v-site-to-azure.md)
* [La replica delle macchine virtuali Hyper-V (con VMM) tooAzure](site-recovery-vmm-to-azure.md)
* [Replica le macchine virtuali Hyper-V tooa Data Center secondario](site-recovery-vmm-to-vmm.md)
* Se si esegue la replica secondaria tooa datacenter a conoscenza [sistemi operativi guest supportati per le macchine virtuali Hyper-V](https://technet.microsoft.com/library/mt126277.aspx).
* Se si esegue la replica tooAzure, il ripristino del sito supporta tutti i sistemi operativi guest hello che sono [supportato da Azure](https://technet.microsoft.com/library/cc794868%28v=ws.10%29.aspx).

### <a name="can-i-protect-vms-when-hyper-v-is-running-on-a-client-operating-system"></a>È possibile proteggere le macchine virtuali quando Hyper-V è in esecuzione in un sistema operativo client?
No, le VM devono trovarsi in un server host Hyper-V in esecuzione in un computer server Windows supportato. Se è necessario tooprotect un computer client è stato possibile replicare come un computer fisico troppo[Azure](site-recovery-vmware-to-azure.md) o [Data Center secondario](site-recovery-vmware-to-vmware.md).

### <a name="what-workloads-can-i-protect-with-site-recovery"></a>Quali carichi di lavoro è possibile proteggere con Site Recovery?
È possibile utilizzare il ripristino del sito tooprotect la maggior parte dei carichi di lavoro in esecuzione in una macchina virtuale supportate o di un server fisico. Il ripristino del sito fornisce il supporto per la replica compatibile con l'applicazione, in modo che le app possono essere ripristinati tooan intelligente stato. Si integra con le applicazioni Microsoft, ad esempio SharePoint, Exchange, Dynamics, SQL Server e Active Directory, e opera a stretto contatto con importanti fornitori, tra cui Oracle, SAP, IBM e Red Hat. [Altre informazioni](site-recovery-workload.md) sulla protezione del carico di lavoro.

### <a name="do-hyper-v-hosts-need-toobe-in-vmm-clouds"></a>Host Hyper-V richiedono toobe nei cloud VMM?
Se si desidera tooreplicate tooa Data Center secondario, quindi le macchine virtuali Hyper-V deve trovarsi in Hyper-V ospita i server che si trovano in un cloud VMM. Se si desidera tooreplicate tooAzure, è possibile replicare le macchine virtuali nel server host Hyper-V con o senza i cloud VMM. [Altre informazioni](site-recovery-hyper-v-site-to-azure.md).

### <a name="can-i-deploy-site-recovery-with-vmm-if-i-only-have-one-vmm-server"></a>È possibile distribuire Site Recovery con VMM se si dispone di un solo server VMM?

Sì. È possibile replicare le macchine virtuali sia nel server Hyper-V in hello VMM cloud tooAzure o è possibile eseguire la replica tra cloud VMM in hello stesso server. Per la replica tooon tra più sedi locali, si consiglia di disporre di un server VMM nei due siti primari e secondari di hello.  

### <a name="what-physical-servers-can-i-protect"></a>Quali server fisici è possibile proteggere?
È possibile replicare i server fisici che eseguono Windows e Linux tooAzure o tooa sito secondario. [Informazioni](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) sui requisiti del sistema operativo.  Hello stessi requisiti si applicano se si esegue la replica in server fisici tooAzure o tooa di sito secondario.


Si noti che se il server locale si arresta, i server fisici vengono eseguiti come le macchine virtuali in Azure. Il failback tooan locale server fisico non è attualmente supportato. Per un computer protetto come fisico, è possibile solo eseguire il failback tooa VMware macchina virtuale.

### <a name="what-vmware-vms-can-i-protect"></a>Quali macchine virtuali VMware è possibile proteggere?

tooprotect le macchine virtuali VMware è necessario un hypervisor di vSphere e macchine virtuali in esecuzione gli strumenti VMware. Si consiglia inoltre di disporre di un hypervisor hello toomanage di VMware vCenter server. [Altre informazioni](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements) sui requisiti specifici per la replica dei server VMware e le macchine virtuali tooAzure o tooa di sito secondario.


### <a name="can-i-manage-disaster-recovery-for-my-branch-offices-with-site-recovery"></a>È possibile gestire il ripristino di emergenza per le succursali con Site Recovery?
Sì. Quando si usa il ripristino del sito tooorchestrate replica e failover nelle succursali, si otterrà un'orchestrazione unificata e visualizzazione di tutti i branch office carichi di lavoro in una posizione centrale. Eseguire i failover e amministrare il ripristino di emergenza di tutti i rami dalla sede centrale, senza visitare rami hello agevolmente.

## <a name="pricing"></a>Prezzi

### <a name="what-charges-do-i-incur-while-using-azure-site-recovery"></a>Quali tariffe vengono applicate quando si usa Azure Site Recovery?
Quando si usa il ripristino del sito, si devono sostenere i costi di licenza di Site Recovery hello, archiviazione di Azure, le transazioni di archiviazione e il trasferimento dei dati in uscita. [Altre informazioni](https://azure.microsoft.com/pricing/details/site-recovery)

licenza di Site Recovery Hello è per ogni istanza protetta, in cui un'istanza è una macchina virtuale o un server fisico.

- Se un disco di macchina virtuale viene replicato l'account di archiviazione standard tooa, hello costi di archiviazione di Azure è per l'utilizzo di archiviazione hello. Ad esempio, se sono di dimensioni del disco di origine hello viene utilizzato 1 TB e 400 GB, il ripristino del sito viene creato un disco rigido virtuale a 1 TB in Azure, ma archiviazione hello addebitato è 400 GB (più hello quantità spazio di archiviazione usato per i log di replica).
- Se un disco di macchina virtuale viene replicato l'account di archiviazione premium tooa, hello costi di archiviazione di Azure è per le dimensioni di archiviazione hello il provisioning, arrotondata per hello più vicino opzione disco di archiviazione premium. Se, ad esempio, dimensioni del disco di origine hello sono di 50 GB, il ripristino del sito viene creato un disco da 50 GB in Azure e Azure esegue il mapping di questo toohello più vicino al disco di archiviazione premium (P10).  Costi vengono calcolati in P10 e non su una dimensione del disco da 50 GB hello.  [Altre informazioni](https://aka.ms/premium-storage-pricing)  Se si utilizza l'archiviazione premium, è necessario anche un account di archiviazione standard per la registrazione di replica e quantità hello di spazio di archiviazione standard utilizzato per tali log anche viene fatturato.
- Non viene creato alcun disco fino a un failover del test o un failover. Nello stato di replica hello, archiviazione gli addebiti nella categoria hello del "blob di pagine e disco" in base alle hello [calcolatore dei costi di archiviazione](https://azure.microsoft.com/en-in/pricing/calculator/) addebitate. Questi si basano sul tipo di archiviazione hello premium/standard e hello della ridondanza dei dati digitare - archiviazione con ridondanza locale, archiviazione con ridondanza geografica, e così via RA-GRS.
- Se hello opzione toouse dischi gestiti in un failover è selezionato, [gli addebiti per i dischi gestiti](https://azure.microsoft.com/en-in/pricing/details/managed-disks/) si applicano dopo un failover o test failover. Gli addebiti dei dischi gestiti non si applicano durante la replica.
- Se i dischi di hello opzione toouse gestito in un failover non è selezionata, in base alle hello archiviazione gli addebiti nella categoria hello del "blob di pagine e disco" [calcolatore dei costi di archiviazione](https://azure.microsoft.com/en-in/pricing/calculator/) addebitate dopo il failover. Questi si basano sul tipo di archiviazione hello premium/standard e hello della ridondanza dei dati digitare - archiviazione con ridondanza locale, archiviazione con ridondanza geografica, e così via RA-GRS.
- Le transazioni di archiviazione vengono addebitate durante la replica nello stato stazionario e per le normali operazioni della macchina virtuale dopo il failover o il failover del test. Questi costi non sono trascurabili.

Durante il failover di test, in cui verranno applicati i costi di hello VM, archiviazione, uscita e archiviazione delle transazioni vengono inoltre sostenere i costi.



## <a name="security"></a>Sicurezza
### <a name="is-replication-data-sent-toohello-site-recovery-service"></a>Dati di replica inviati servizio Site Recovery toohello
No, Site Recovery non intercetta i dati replicati né raccoglie informazioni su ciò che è in esecuzione sulle macchine virtuali o sui server fisici.
I dati di replica vengono scambiati tra host Hyper-V, hypervisor VMware o server fisici e Archiviazione di Azure o il sito secondario. Il ripristino del sito non ha toointercept possibilità che i dati. Solo i metadati di hello necessari tooorchestrate replica e failover verrà inviato toohello del servizio Site Recovery.  

Il ripristino del sito è ISO 27001: 2013, 27018, HIPAA DPA certificate ed è in corso di hello delle valutazioni SOC2 e FedRAMP JAB.

### <a name="for-compliance-reasons-even-our-on-premises-metadata-must-remain-within-hello-same-geographic-region-can-site-recovery-help-us"></a>Per motivi di conformità, anche i metadati locale devono rimanere all'interno di hello stessa area geografica. Site Recovery può offrire vantaggi?
Sì. Quando si crea un insieme di credenziali di Site Recovery in un'area, è assicurarsi che tutti i metadati che è necessario tooenable e orchestrare replica e failover rimane all'interno di tale area della geografica limite.

### <a name="does-site-recovery-encrypt-replication"></a>Site Recovery consente di crittografare la replica?
Per la replica di macchine virtuali e server fisici tra siti locali, è supportata la crittografia in transito. Per le macchine virtuali e server fisici, replica tooAzure, sia la crittografia in transito e [--crittografia (in Azure)](https://docs.microsoft.com/en-us/azure/storage/storage-service-encryption) sono supportati.

## <a name="replication"></a>Replica

### <a name="can-i-replicate-over-a-site-to-site-vpn-tooazure"></a>È possibile replicare su un tooAzure VPN da sito a sito?
Azure Site Recovery consente di replicare i dati tooan account di archiviazione Azure, su un endpoint pubblico. La replica non avviene tramite una rete VPN da sito a sito. È possibile creare una rete VPN da sito a sito con una rete virtuale di Azure. Ciò non interferisce con la replica di Site Recovery.

### <a name="can-i-use-expressroute-tooreplicate-virtual-machines-tooazure"></a>È possibile utilizzare ExpressRoute tooreplicate macchine virtuali tooAzure?
Sì, ExpressRoute può essere utilizzato tooreplicate tooAzure di macchine virtuali. Azure Site Recovery consente di replicare dati tooan, Account di archiviazione Azure tramite un endpoint pubblico. È necessario tooset backup [peering pubblico](../expressroute/expressroute-circuit-peerings.md#public-peering) toouse ExpressRoute per la replica di Site Recovery. Dopo che le macchine virtuali hello impossibili su tooan rete virtuale di Azure è possibile accedervi utilizzando hello [peering privato](../expressroute/expressroute-circuit-peerings.md#private-peering) programma di installazione con hello rete virtuale di Azure.

### <a name="are-there-any-prerequisites-for-replicating-virtual-machines-tooazure"></a>Sono presenti tutti i prerequisiti per la replica delle macchine virtuali tooAzure?
Macchine virtuali da tooreplicate tooAzure devono essere conformi a [requisiti Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).

L'account utente di Azure deve toohave determinati [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica di un nuovo tooAzure macchina virtuale.

### <a name="can-i-replicate-hyper-v-generation-2-virtual-machines-tooazure"></a>È possibile replicare tooAzure 2 macchine virtuali di Hyper-V generazione?
Sì. Il ripristino del sito converte di generazione 2 toogeneration 1 durante il failover. Il failback macchina hello è convertito toogeneration back-2. [Altre informazioni](http://azure.microsoft.com/blog/2015/04/28/disaster-recovery-to-azure-enhanced-and-were-listening/).

### <a name="if-i-replicate-tooazure-how-do-i-pay-for-azure-vms"></a>Se si replicano tooAzure come posso pagare per le macchine virtuali di Azure?
Durante la replica normale, dati sono replicato archiviazione di Azure con ridondanza toogeo e non è necessario toopay eventuali addebiti di macchina virtuale IaaS di Azure, fornire un vantaggio significativo. Quando si esegue automaticamente tooAzure un failover, il ripristino del sito consente di creare macchine virtuali IaaS di Azure e dopo che verrà addebitato per le risorse di calcolo hello che puoi utilizzare in Azure.

### <a name="can-i-automate-site-recovery-scenarios-with-an-sdk"></a>È possibile automatizzare gli scenari di Site Recovery con un SDK?
Sì. È possibile automatizzare i flussi di lavoro di Site Recovery usando hello API Rest, PowerShell o hello Azure SDK. Scenari attualmente supportati per la distribuzione di Site Recovery tramite PowerShell:

* [Replicare macchine virtuali Hyper-V in VMM cloud tooAzure Gestione risorse di PowerShell](site-recovery-vmm-to-azure-powershell-resource-manager.md)
* [Replicare macchine virtuali Hyper-V senza tooAzure VMM Gestione risorse di PowerShell](site-recovery-deploy-with-powershell-resource-manager.md)

### <a name="if-i-replicate-tooazure-what-kind-of-storage-account-do-i-need"></a>Se si replicano tooAzure il tipo di account di archiviazione è necessario?
* **Portale di Azure classico**: se si distribuisce il ripristino del sito nel portale di Azure classico hello, è necessario un [account di archiviazione con ridondanza geografica standard](../storage/common/storage-redundancy.md#geo-redundant-storage). Archiviazione Premium non è attualmente supportata. Hello account deve trovarsi in hello stessa area dell'insieme di credenziali di Site Recovery hello.
* **Portale di Azure**: se si distribuisce il ripristino del sito nel portale di Azure hello, è necessario un account di archiviazione con ridondanza locale o di archiviazione con ridondanza geografica. Si consiglia di archiviazione con ridondanza geografica, in modo che i dati sono resilienti se si verifica un'interruzione dell'alimentazione locale o se non è possibile recuperare l'area primaria hello. Hello account deve trovarsi in hello stessa area hello insieme di credenziali di servizi di ripristino. Archiviazione Premium è ora supportata per VMware VM, macchina virtuale Hyper-V e la replica di server fisici, quando si distribuisce il ripristino del sito nel portale di Azure hello.

### <a name="how-often-can-i-replicate-data"></a>Con quale frequenza è possibile eseguire la replica dei dati?
* **Hyper-V:** le macchine virtuali Hyper-V possono essere replicate ogni 30 secondi (eccetto per Archiviazione Premium), 5 minuti o 15 minuti. Se è stata configurata la replica SAN, questa sarà sincrona.
* **VMware e server fisici:** in questo caso la frequenza di replica non è rilevante. La replica è continua.

### <a name="can-i-extend-replication-from-existing-recovery-site-tooanother-tertiary-site"></a>È possibile estendere la replica dal ripristino del sito tooanother terziaria sito esistente?
No, la replica concatenata o estesa non è supportata. Richiedere questa funzionalità nel [forum dei commenti](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6097959-support-for-exisiting-extended-replication).

### <a name="can-i-do-an-offline-replication-hello-first-time-i-replicate-tooazure"></a>È possibile eseguire un hello replica offline prima volta, che si replicano tooAzure?
Questa funzionalità non è supportata. Questa funzionalità in hello richiesta [forum sul feedback su](http://feedback.azure.com/forums/256299-site-recovery/suggestions/6227386-support-for-offline-replication-data-transfer-from).

### <a name="can-i-exclude-specific-disks-from-replication"></a>È possibile escludere dischi specifici dalla replica?
Questa funzionalità è supportata quando si è [replicare le macchine virtuali VMware e le macchine virtuali Hyper-V](site-recovery-exclude-disk.md) tooAzure, utilizzando hello portale di Azure.

### <a name="can-i-replicate-virtual-machines-with-dynamic-disks"></a>È possibile eseguire la replica delle macchine virtuali con i dischi dinamici?
I dischi dinamici sono supportati durante la replica delle macchine virtuali Hyper-V, Sono supportate anche per la replica delle macchine virtuali VMware e tooAzure macchine fisiche. disco del sistema operativo Hello deve essere un disco di base.

### <a name="can-i-add-a-new-machine-tooan-existing-replication-group"></a>È possibile aggiungere un nuovo computer tooan gruppo di replica esistente?
Aggiunta di nuovi gruppi di replica tooexisting macchine è supportata. toodo in tal caso, selezionare il gruppo di replica hello (dal pannello 'Elementi replicato') e menu di scelta rapida/Seleziona fare clic sul gruppo di replica hello e selezionare l'opzione appropriata hello.

![Aggiungere il gruppo tooreplication](./media/site-recovery-faq/add-server-replication-group.png)

### <a name="can-i-throttle-bandwidth-allotted-for-hyper-v-replication-traffic"></a>È possibile applicare limitazioni della larghezza di banda allocata per il traffico di replica Hyper-V?
Sì. Altre informazioni sulla limitazione della larghezza di banda in articoli sulla distribuzione di hello:

* [Pianificazione della capacità per la replica da VM VMware e server fisici](site-recovery-plan-capacity-vmware.md)
* [Pianificazione della capacità per la replica da VM Hyper-V nei cloud VMM](site-recovery-vmm-to-azure.md#capacity-planning)
* [Pianificazione della capacità per la replica da VM Hyper-V senza VMM](site-recovery-hyper-v-site-to-azure.md)

## <a name="failover"></a>Failover
### <a name="if-im-failing-over-tooazure-how-do-i-access-hello-azure-virtual-machines-after-failover"></a>Se sono failover tooAzure, come è possibile accedere hello Azure le macchine virtuali dopo il failover?
È possibile accedere hello macchine virtuali di Azure tramite una connessione Internet sicura, tramite una VPN site-to-site o expressroute di Azure. È necessario un numero di elementi in ordine tooconnect tooprepare. [Altre informazioni](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover)


### <a name="if-i-fail-over-tooazure-how-does-azure-make-sure-my-data-is-resilient"></a>Se esegue il failover come Azure assicurarsi tooAzure sono flessibili dei dati?
Azure è progettato nell'ottica della resilienza. Il ripristino del sito è già progettato per failover tooa secondario Data Center di Azure, in base alle hello nasce SLA di Azure, se necessario hello. Se in questo caso, ci si assicura che i metadati e gli insiemi di credenziali rimangono all'interno di hello stessa area geografica scelta per l'insieme di credenziali.  

### <a name="if-im-replicating-between-two-datacenters-what-happens-if-my-primary-datacenter-experiences-an-unexpected-outage"></a>Se si esegue la replica tra due data center, che cosa accade se nel data center principale si verifica un'interruzione imprevista?
È possibile attivare un failover non pianificato da sito secondario hello. Il ripristino del sito non è necessaria la connettività da sito primario di hello tooperform hello failover.

### <a name="is-failover-automatic"></a>Il failover è automatico?
Il failover non è automatico. Si avvia failover con singolo clic nel portale di hello o è possibile utilizzare [PowerShell di ripristino del sito](/powershell/module/azurerm.siterecovery) tootrigger un failover. Failback è un'operazione semplice nel portale di Site Recovery hello.

è possibile utilizzare tooautomate locale toodetect Orchestrator o Operations Manager un errore della macchina virtuale, e quindi trigger hello failover utilizzando hello SDK.

* [Ulteriori informazioni](site-recovery-create-recovery-plans.md) sui piani di ripristino.
* [Altre informazioni](site-recovery-failover.md) sul failover.
* [Altre informazioni](site-recovery-failback-azure-to-vmware.md) sul failback di VM VMware e server fisici

### <a name="if-my-on-premises-host-is-not-responding-or-crashed-can-i-failover-back-tooa-different-host"></a>Se l'host locale non risponde o bloccato, è possibile failover tooa indietro diversi host?
Sì, è possibile utilizzare hello posizione alternativa ripristino toofailback tooa host diverso da Azure. Altre informazioni sulle opzioni di hello hello collegamenti riportati di seguito per le macchine virtuali VMware e Hyper-v.

* [Per macchine virtuali VMware](site-recovery-how-to-failback-azure-to-vmware.md#fail-back-to-the-original-or-alternate-location)
* [Per macchine virtuali Hyper-V](site-recovery-failback-from-azure-to-hyper-v.md#failback-to-an-alternate-location)

## <a name="service-providers"></a>Provider di servizi
### <a name="im-a-service-provider-does-site-recovery-work-for-dedicated-and-shared-infrastructure-models"></a>Per i provider di servizi, Site Recovery funziona per modelli di infrastruttura dedicati e condivisi?
Sì, Site Recovery supporta i modelli di infrastruttura dedicati e condivisi.

### <a name="for-a-service-provider-is-hello-identity-of-my-tenant-shared-with-hello-site-recovery-service"></a>Per un provider di servizi è l'identità di hello del mio tenant condivisi con il servizio Site Recovery hello?
No. L'identità del tenant rimane anonima. I tenant non è necessario il portale di Site Recovery toohello di accesso. Solo amministratore di provider del servizio hello interagisce con il portale di hello.

### <a name="will-tenant-application-data-ever-go-tooazure"></a>Dati dell'applicazione tenant andrà mai tooAzure?
Durante la replica tra siti di provider di proprietà del servizio, i dati dell'applicazione passa mai tooAzure. Dati vengono crittografati in transito e replicate direttamente tra siti di provider del servizio di hello.

Se si esegue la replica tooAzure, i dati dell'applicazione viene inviati tooAzure archiviazione ma non toohello servizio Site Recovery. I dati vengono crittografati in transito e rimangono crittografati in Azure.

### <a name="will-my-tenants-receive-a-bill-for-any-azure-services"></a>I tenant riceveranno una fattura per ogni servizio Azure?
No. Relazione di fatturazione di Azure è direttamente con il provider di servizi di hello. I provider di servizi sono responsabili della generazione di fatture specifiche per i tenant.

### <a name="if-im-replicating-tooazure-do-we-need-toorun-virtual-machines-in-azure-at-all-times"></a>Se sono replica tooAzure, dobbiamo toorun di macchine virtuali in Azure in qualsiasi momento?
No, i dati sono replicati tooan account di archiviazione di Azure nella sottoscrizione. Quando si esegue un failover di test (un'analisi del ripristino di emergenza) o un failover effettivo, Site Recovery crea automaticamente macchine virtuali nella sottoscrizione.

### <a name="do-you-ensure-tenant-level-isolation-when-i-replicate-tooazure"></a>È possibile garantire isolamento a livello di tenant durante la replica tooAzure?
Sì.

### <a name="what-platforms-do-you-currently-support"></a>Quali piattaforme sono attualmente supportate?
Sono supportate distribuzioni basate su Azure Pack, Cloud Platform System e System Center (2012 e versioni successive). [Alter informazioni](https://technet.microsoft.com/library/dn850370.aspx) sull'integrazione di Azure Pack e Site Recovery.

### <a name="do-you-support-single-azure-pack-and-single-vmm-server-deployments"></a>Sono supportate singole distribuzioni di Azure Pack e del server VMM?
Sì, è possibile replicare tooAzure di macchine virtuali Hyper-V, o tra siti di provider del servizio.  Si noti che se si esegue la replica tra i siti del provider di servizi, l'integrazione del runbook di Azure non è disponibile.

## <a name="next-steps"></a>Passaggi successivi
* Hello lettura [Cenni preliminari sul ripristino del sito](site-recovery-overview.md)
* Informazioni sull' [architettura di Site Recovery](site-recovery-components.md)  
