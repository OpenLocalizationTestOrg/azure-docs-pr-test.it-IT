---
title: "aaaWhat è Azure Site Recovery? | Microsoft Docs"
description: Viene fornita una panoramica del servizio Azure Site Recovery hello e vengono riepilogati gli scenari di distribuzione.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: cfreeman
editor: 
ms.assetid: e9b97b00-0c92-4970-ae92-5166a4d43b68
ms.service: site-recovery
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/25/2017
ms.author: raynew
ms.openlocfilehash: da6755654b8036a03314ec836f014b64428d5518
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-site-recovery"></a>Che cos'è Site Recovery?

Benvenuti toohello servizio di Azure Site Recovery. Questo articolo fornisce una rapida panoramica del servizio hello.

## <a name="business-continuity-and-disaster-recovery-bcdr-with-azure-recovery-services"></a>Continuità aziendale e ripristino di emergenza (BCDR) con Servizi di ripristino di Azure

Come un'organizzazione è necessario toofigure out come eseguirai tookeep dati sicuro e App/i carichi di lavoro in esecuzione quando pianificato e interruzioni non pianificate vengono eseguite.

Servizi di ripristino di Azure contribuisce strategia BCDR tooyour:

- **Servizio Site Recovery**: Site Recovery consente di garantire la continuità aziendale, mantenendo le app in esecuzione nelle macchine virtuali e nei server fisici disponibili in caso di arresto di un sito. Il ripristino del sito vengono replicati i carichi di lavoro in esecuzione su macchine virtuali e server fisici in modo che rimangano disponibili in una posizione secondaria se sito primario di hello non è disponibile. Vengono ripristinati i carichi di lavoro toohello primario di sito quando è attivo ed eseguendo nuovamente.
- **Servizio di backup**: hello inoltre [Azure Backup](https://docs.microsoft.com/azure/backup/) servizio i dati rimangono al sicuro e recuperabili tramite backup tooAzure.

Site Recovery può gestire la replica per:

- Replica di VM di Azure tra aree di Azure.
- Locale macchine virtuali e server fisici, replica tooAzure o tooa di sito secondario.


## <a name="what-does-site-recovery-provide"></a>Che cosa offre Site Recovery?

**Funzionalità** | **Dettagli**
--- | ---
**Distribuire una soluzione BCDR semplice** | Tramite il ripristino del sito, è possibile configurare e gestire la replica, il failover e failback da un'unica posizione in hello portale di Azure.
**Replicare le VM di Azure** | È possibile configurare la strategia di BCDR in modo che le VM di Azure vengano replicate tra le aree di Azure.
**Replicare le VM locali in una posizione esterna** | È possibile replicare le macchine virtuali in locale e server fisici tooAzure o percorso locale secondario tooa. Consente di eliminare la replica tooAzure hello costi e complessità di gestione di un Data Center secondario.
**Replica di qualsiasi carico di lavoro** | Replicare qualsiasi carico di lavoro in esecuzione in VM di Azure, VM Hyper-V locali, VM VMware supportate e nei server fisici di Windows o Linux.
**Mantenere i dati resilienti e sicuri** | Site Recovery gestisce la replica senza intercettare i dati delle applicazioni. Dati replicati vengono archiviati in archiviazione di Azure con resilienza hello che fornisce. Quando si verifica il failover, macchine virtuali di Azure vengono create in base ai dati replicato hello.
**Soddisfare RTO e RPO** | Mantenere gli obiettivi del punto di ripristino (RPO, Recovery Point Objective) e gli obiettivi del tempo di ripristino (RTO, Recovery Time Objective) entro i limiti dell'organizzazione. Site Recovery offre la replica continua per le VM di Azure e le VM WMware e una frequenza di replica di soli 30 secondi per Hyper-V. È possibile ridurre ulteriormente gli obiettivi del tempo di ripristino (RTO) grazie all'integrazione con [Gestione traffico di Azure](https://azure.microsoft.com/blog/reduce-rto-by-using-azure-traffic-manager-with-azure-site-recovery/).
**Mantenere la coerenza delle app nel failover** | È possibile configurare punti di ripristino con snapshot coerenti con l'applicazione. Gli snapshot coerenti con l'applicazione acquisiscono i dati dei dischi, tutti i dati in memoria e tutte le transazioni in corso.
**Test senza interruzioni** | Sia possibile eseguire facilmente i test failover toosupport esercitazioni di ripristino di emergenza, senza influire sulla replica in corso.
**Eseguire failover flessibili** | È possibile eseguire failover pianificati senza perdita di dati per interruzioni previste o il failover non pianificato con perdita di dati minima, in base alla frequenza di replica, per emergenze impreviste. È possibile eseguire il sito primario tooyour indietro facilmente quando è nuovamente disponibile.
**Creare piani di ripristino** | Con i piani di ripristino è possibile personalizzare e definire la sequenza di failover e ripristino di applicazioni multilivello distribuite in più macchine virtuali. L'utente raggruppa le macchine all'interno dei piani e aggiunge script e azioni manuali. I piani di ripristino possono essere integrati con i runbook di Automazione di Azure.
**Eseguire l'integrazione con tecnologie BCDR esistenti** | Site Recovery si integra con altre tecnologie BCDR. Ad esempio, è possibile utilizzare il ripristino del sito tooprotect hello Server SQL back-end dei carichi di lavoro aziendali, incluso il supporto nativo per SQL Server AlwaysOn, toomanage hello failover dei gruppi di disponibilità.
**Integrazione con la libreria di automazione hello** | Un'avanzata libreria di automazione di Azure offre script pronti per la produzione e specifici dell'applicazione che possono essere scaricati e integrati con Site Recovery.
**Gestire le impostazioni di rete** | Site Recovery si integra con Azure per una gestione semplice della rete delle applicazioni, tra cui l'impostazione di indirizzi IP riservati, la configurazione di servizi di bilanciamento del carico e l'integrazione di Gestione traffico di Azure per cambi di rete efficienti.


## <a name="what-can-i-replicate"></a>Ciò che è possibile replicare?

**Supportato** | **Dettagli**
--- | ---
**Cosa è possibile replicare?** | VM di Azure tra aree di Azure (in anteprima)<br/><br/>  Le macchine virtuali VMware, le macchine virtuali Hyper-V, i server fisici (Windows e Linux) tooAzure locale < br /<br/> Le macchine virtuali VMware, le macchine virtuali Hyper-V, del sito secondario di server fisici tooa in locale. Per le macchine virtuali Hyper-V, del sito secondario di replica tooa è supportato solo se l'host Hyper-V gestiti da System Center VMM.
**Quali aree sono supportate per Site Recovery?** | [Aree supportate](https://azure.microsoft.com/regions/services/) |
**Quali sistemi operativi sono richiesti per le macchine replicate?** | [Requisiti per le VM di Azure](site-recovery-support-matrix-azure-to-azure.md#support-for-replicated-machine-os-versions)<br></br>[Requisiti per le VM VMware](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)<br/><br/> Per le macchine virtuali Hyper-V, è supportato qualsiasi [sistema operativo guest](https://technet.microsoft.com/windows-server-docs/compute/hyper-v/supported-windows-guest-operating-systems-for-hyper-v-on-windows) supportato da Azure e Hyper-V.<br/><br/> [Requisiti per i server fisici](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)
**Quali server/host VMware sono necessari?** | Le VM VMware possono trovarsi in [host vSphere/server vCenter supportati](site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers)
**Quali carichi di lavoro è possibile replicare?** | È possibile replicare qualsiasi carico di lavoro in esecuzione in un computer di replica supportato. Inoltre, team Site Recovery hello siano eseguite specifico dell'applicazione di test per un [numero di app](site-recovery-workload.md#workload-summary).


## <a name="azure-portal-considerations"></a>Considerazioni sul portale di Azure

* Il ripristino del sito può essere distribuito in hello [portale di Azure](https://portal.azure.com).
* Nel portale di Azure classico hello, è possibile gestire il ripristino del sito con modello di gestione di servizi classico hello.
- portale classico Hello deve essere solo le distribuzioni di ripristino del sito esistenti toomaintain utilizzato. È possibile creare nuovi insiemi di credenziali nel portale classico hello.

## <a name="next-steps"></a>Passaggi successivi
* Altre informazioni sul [supporto dei carichi di lavoro](site-recovery-workload.md)
* Introduzione a [replica macchina virtuale di Azure tra aree](site-recovery-azure-to-azure.md), [tooAzure replica VMware](vmware-walkthrough-overview.md), o [tooAzure di replica Hyper-V](hyper-v-site-walkthrough-overview.md).
