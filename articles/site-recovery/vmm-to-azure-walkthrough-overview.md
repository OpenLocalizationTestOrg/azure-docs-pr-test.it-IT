---
title: cloud di macchine virtuali Hyper-V in VMM aaaReplicate tooAzure con Azure Site Recovery | Documenti Microsoft
description: Viene fornita una panoramica per la replica delle macchine virtuali Hyper-V in VMM cloud tooAzure utilizzando il servizio di Azure Site Recovery hello
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8e7d868e-00f3-4e8b-9a9e-f23365abf6ac
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: raynew
ms.openlocfilehash: d6f729a49cc86ea07bebc4d7266fd7b58b3998f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-in-vmm-clouds-tooazure-using-site-recovery-in-hello-azure-portal"></a>Replicare le macchine virtuali Hyper-V in VMM cloud tooAzure usando Site Recovery nel portale di Azure hello
> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-vmm-to-azure.md)
> * [Azure classico](site-recovery-vmm-to-azure-classic.md)
> * [PowerShell - Resource Manager](site-recovery-vmm-to-azure-powershell-resource-manager.md)
> * [PowerShell - Classica](site-recovery-deploy-with-powershell.md)


In questo articolo fornisce una panoramica di hello passaggi necessari tooreplicate locale macchine virtuali di Hyper-V (VM) gestite in tooAzure cloud di System Center Virtual Machine Manager (VMM), utilizzando hello [Azure Site Recovery](site-recovery-overview.md) servizio Hello portale di Azure.

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-hello-scenario-architecture"></a>Passaggio 1: Esaminare l'architettura dello scenario hello

Prima di avviare la distribuzione, esaminare l'architettura dello scenario hello e assicurarsi di aver compreso tutti i componenti di hello è necessario toodeploy.

Andare troppo[passaggio 1: esaminare l'architettura di hello](vmm-to-azure-walkthrough-architecture.md)

## <a name="step-2-review-prerequisites-and-limitations"></a>Passaggio 2: Esaminare i prerequisiti e le limitazioni

Assicurarsi di comprendere le limitazioni e prerequisiti di distribuzione hello.

**Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.
**Server VMM locali e host Hyper-V**: assicurarsi che i server VMM e gli host Hyper-V siano conformi e preparati per la distribuzione di Site Recovery.
**Macchine virtuali replicate**: verificare che le macchine virtuali desiderate tooreplicate conformi ai requisiti di Azure.

Andare troppo[passaggio 2: verificare i prerequisiti e limitazioni](vmm-to-azure-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Passaggio 3: Pianificare la capacità

Se si sta eseguendo una distribuzione completa, è necessario toofigure risorse quali la replica è necessario. Esistono un paio di strumenti disponibili toohelp si esegue questa operazione. Se si sta eseguendo una rapida Configura tootest hello ambiente, è possibile ignorare questo passaggio.

Andare troppo[passaggio 3: pianificare la capacità](vmm-to-azure-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Passaggio 4: Pianificare la rete

È necessario toodo alcuni pianificazione tooensure che è possibile configurare il mapping di rete quando si distribuisce uno scenario di hello, della rete che macchine virtuali di Azure saranno le reti virtuali connesse tooAzure dopo che si verifica il failover e indirizzi che che sono state assegnate IP appropriato.

Andare troppo[passaggio 4: pianificare la rete](vmm-to-azure-walkthrough-network.md)


## <a name="step-5-prepare-azure-resources"></a>Passaggio 5: Preparare le risorse di Azure

Configurare un account Azure, reti e archiviazione. È possibile eseguire queste operazioni durante la distribuzione, ma si consiglia di farlo prima di iniziare.

Andare troppo[passaggio 5: preparare Azure](vmm-to-azure-walkthrough-prepare-azure.md)

## <a name="step-6-prepare-vmm-and-hyper-v"></a>Passaggio 6: Preparare VMM e Hyper-V

Preparare i server VMM locale di hello e host Hyper-V per la distribuzione di Site Recovery.

Andare troppo[passaggio 6: preparare i server locali](vmm-to-azure-walkthrough-vmm-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Passaggio 7: Configurare un insieme di credenziali

Configurare un insieme di credenziali dei Servizi di ripristino. insieme di credenziali Hello contiene impostazioni di configurazione e Orchestra la replica.

[Passaggio 7: Configurare un insieme di credenziali](vmm-to-azure-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Passaggio 8: Configurare le impostazioni di origine e di destinazione

Impostare il percorso di replica di origine e destinazione hello. Aggiungi insieme di credenziali toohello server VMM hello e scaricare i file di installazione hello per i componenti di Site Recovery. Eseguire l'installazione di Provider di Azure Site Recovery nel server VMM hello. Il programma di installazione installa hello Provider nel server VMM hello e registra il server hello nell'insieme di credenziali hello. Installare l'agente di servizi di ripristino di Microsoft hello in ogni host Hyper-V.

Andare troppo[passaggio 8: configurare le impostazioni di origine e di destinazione](vmm-to-azure-walkthrough-source-target.md)

## <a name="step-9-configure-network-mapping"></a>Passaggio 9: Configurare il mapping di rete

Mappa reti virtuali tooAzure di reti VM di VMM in locale. Dopo il failover, macchine virtuali di Azure vengono create in hello rete di Azure che esegue il mapping di rete VM toohello locale in cui hello Hyper-V di origine si trova.

Andare troppo[passaggio 9: configurare il mapping di rete](vmm-to-azure-walkthrough-network-mapping.md)


## <a name="step-10-set-up-a-replication-policy"></a>Passaggio 10: Configurare un criterio di replica

Specificare la modalità di macchine virtuali in locale verranno replicate tooAzure.

Andare troppo[passaggio 10: configurare un criterio di replica](vmm-to-azure-walkthrough-replication.md)


## <a name="step-11-enable-replication-for-vms"></a>Passaggio 11: Abilitare la replica per le macchine virtuali

Selezionare le macchine virtuali hello desiderato tooreplicate. Abilitazione di una macchina virtuale per tooAzure la replica iniziale hello trigger di replica, seguito dalla replica differenziale in corso.

Andare troppo[passaggio 11: abilitare la replica](vmm-to-azure-walkthrough-enable-replication.md)


## <a name="step-12-run-a-test-failover"></a>Passaggio 12: Eseguire un failover di test

Eseguire un toomake di failover di test che tutto funzioni come previsto.

Andare troppo[passaggio 12: eseguire un failover di test](vmm-to-azure-walkthrough-test-failover.md)


