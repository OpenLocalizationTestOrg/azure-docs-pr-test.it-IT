---
title: aaaReplicate macchine virtuali Hyper-V tooa VMM del sito secondario con Azure Site Recovery | Documenti Microsoft
description: Fornisce una panoramica per la replica delle macchine virtuali Hyper-V tooa sito VMM secondario tramite hello portale di Azure.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: 476ca82a-8f5c-4498-9dcf-e1011d60ed59
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/27/2017
ms.author: raynew
ms.openlocfilehash: 90e44bfc2237dfa7646fb2b7b1e533a7f6d83c50
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooa-secondary-vmm-site"></a>Replicare le macchine virtuali Hyper-V in VMM cloud tooa VMM del sito secondario

> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-vmm-to-vmm.md)
> * [Portale classico](site-recovery-vmm-to-vmm-classic.md)
> * [PowerShell - Gestione risorse](site-recovery-vmm-to-vmm-powershell-resource-manager.md)
>
>

In questo articolo viene fornita una panoramica dei passaggi necessari tooreplicate locale macchine virtuali di Hyper-V (VM) gestite nei cloud di System Center Virtual Machine Manager (VMM), tooa percorso secondario di VMM, hello utilizzando [Azure Site Recovery](site-recovery-overview.md)in hello portale di Azure.

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Passaggio 1: Esaminare l'architettura dello scenario hello

Prima di avviare la distribuzione, esaminare l'architettura dello scenario hello e assicurarsi di aver compreso tutti i componenti di hello è necessario toodeploy.

Andare troppo[passaggio 1: esaminare l'architettura di hello](vmm-to-vmm-walkthrough-architecture.md).

## <a name="step-2-review-prerequisites-and-limitations"></a>Passaggio 2: Esaminare i prerequisiti e le limitazioni

Assicurarsi di comprendere le limitazioni e prerequisiti di distribuzione hello.

**Prerequisiti di Azure**: È necessaria una sottoscrizione di Microsoft Azure e servizi di ripristino di Azure dell'insieme di credenziali, tooorchestrate e gestire la replica.
**Server VMM locali e host Hyper-V**: assicurarsi che i server VMM e gli host Hyper-V siano conformi e preparati per la distribuzione di Site Recovery.

Andare troppo[passaggio 2: verificare i prerequisiti e limitazioni](vmm-to-vmm-walkthrough-prerequisites.md).

## <a name="step-3-plan-networking"></a>Passaggio 3: Pianificare la rete

È necessario toodo alcuni pianificazione che è possibile configurare i mapping di rete tra le reti VM di VMM quando si distribuisce uno scenario di hello tooensure della rete.

Andare troppo[passaggio 3: pianificare la rete](vmm-to-vmm-walkthrough-network.md).


## <a name="step-4-prepare-vmm-and-hyper-v"></a>Passaggio 4: Preparare VMM e Hyper-V

Preparare i server VMM hello e host Hyper-V per la distribuzione di Site Recovery.

Andare troppo[passaggio 4: preparare i server locali](vmm-to-vmm-walkthrough-vmm-hyper-v.md).

## <a name="step-5-set-up-a-vault"></a>Passaggio 5: Configurare un insieme di credenziali

Configurare un insieme di credenziali dei Servizi di ripristino. insieme di credenziali Hello contiene impostazioni di configurazione e Orchestra la replica.

[Passaggio 5: Configurare un insieme di credenziali](vmm-to-vmm-walkthrough-create-vault.md).

## <a name="step-6-set-up-source-and-target-settings"></a>Passaggio 6: Configurare le impostazioni di origine e destinazione

Impostare hello ubicazioni VMM replica origine e di destinazione. Aggiungi insieme di credenziali toohello server VMM hello e scaricare i file di installazione hello per i componenti di Site Recovery. Eseguire l'installazione di Provider di Azure Site Recovery nel server VMM hello. Il programma di installazione installa hello Provider nel server VMM hello e registra il server hello nell'insieme di credenziali hello. Installare l'agente di servizi di ripristino di Microsoft hello in ogni host Hyper-V.

Andare troppo[passaggio 6: configurare le impostazioni di origine e destinazione hello](vmm-to-vmm-walkthrough-source-target.md).

## <a name="step-7-configure-network-mapping"></a>Passaggio 7: Configurare il mapping di rete

Mapping delle reti VM di VMM nei percorsi di origine e destinazione hello. Dopo il failover, le macchine virtuali vengono create nella rete di destinazione hello tale rete VM di mappe toohello origine in cui hello si trova la macchina virtuale Hyper-V di origine.

Andare troppo[passaggio 7: configurare il mapping di rete](vmm-to-vmm-walkthrough-network-mapping.md).


## <a name="step-8-set-up-a-replication-policy"></a>Passaggio 8: Configurare un criterio di replica

Specificare in che modo le macchine virtuali verranno replicate tra posizioni di VMM.

Andare troppo[passaggio 8: impostare un criterio di replica](vmm-to-vmm-walkthrough-replication.md).


## <a name="step-9-enable-replication-for-vms"></a>Passaggio 9: Abilitare la replica per le VM

Selezionare le macchine virtuali hello desiderato tooreplicate. Abilitazione di una macchina virtuale per il sito secondario di replica i trigger hello la replica iniziale toohello, seguito dalla replica differenziale in corso.

Andare troppo[passaggio 9: abilitare la replica](vmm-to-vmm-walkthrough-enable-replication.md).


## <a name="step-10-run-a-test-failover"></a>Passaggio 10: Eseguire un failover di test

Eseguire un toomake di failover di test che tutto funzioni come previsto.

Andare troppo[passaggio 10: eseguire un failover di test](vmm-to-vmm-walkthrough-test-failover.md).
