---
title: aaaReplicate tooAzure di macchine virtuali Hyper-V con Azure Site Recovery | Documenti Microsoft
description: Viene descritto come replica tooorchestrate, failover e il ripristino di locale Hyper-V VM tooAzure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: efddd986-bc13-4a1d-932d-5484cdc7ad8d
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: ab9cd14149ef32a416428d0f4327aa18b042e9c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-hyper-v-virtual-machines-without-vmm-tooazure"></a>La replica Hyper-V le macchine virtuali (senza VMM) tooAzure 

> [!div class="op_single_selector"]
> * [Portale di Azure](site-recovery-hyper-v-site-to-azure.md)
> * [Azure classico](site-recovery-hyper-v-site-to-azure-classic.md)
> * [PowerShell - Gestione risorse](site-recovery-deploy-with-powershell-resource-manager.md)
>
>

In questo articolo viene fornita una panoramica di hello passaggi necessari tooreplicate locale Hyper-V le macchine virtuali tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) in hello portale di Azure. In questa distribuzione le macchine virtuali Hyper-V non vengono gestite tramite la soluzione Virtual Machine Manager (VMM) di System Center.


Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="step-1-review-architecture-and-prerequisites"></a>Passaggio 1: Esaminare l'architettura e i prerequisiti

Prima di iniziare la distribuzione, esaminare l'architettura dello scenario hello e assicurarsi di che aver compreso tutti i componenti di hello necessari toodeploy

Andare troppo[passaggio 1: esaminare l'architettura di hello](hyper-v-site-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Passaggio 2: Esaminare i prerequisiti

Assicurarsi di avere i prerequisiti di hello sul posto per ogni componente di distribuzione:

- **Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.
- **Prerequisiti di Hyper-V in locale**: assicurarsi che gli host Hyper-V siano pronti per la distribuzione di Site Recovery.
- **Macchine virtuali replicate**: macchine virtuali che si desidera tooreplicate necessario toocomply ai requisiti di Azure.

Andare troppo[passaggio 2: verificare i prerequisiti e limitazioni](hyper-v-site-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Passaggio 3: Pianificare la capacità

Se si sta eseguendo una distribuzione completa, è necessario toofigure risorse quali la replica è necessario. Esistono un paio di strumenti disponibili toohelp si esegue questa operazione. Passare tooStep 2. Se si sta eseguendo una rapida Configura tootest hello ambiente è possibile ignorare questo passaggio.

Andare troppo[passaggio 3: pianificare la capacità](hyper-v-site-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Passaggio 4: Pianificare la rete

È necessario toodo alcuni pianificazione tooensure che macchine virtuali di Azure siano connessi toonetworks dopo che si verifica il failover e che dispongano di hello destra indirizzi IP della rete.

Andare troppo[passaggio 4: pianificare la rete](hyper-v-site-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Passaggio 5: Preparare le risorse di Azure

Configurare le reti e le risorse di archiviazione di Azure prima di iniziare. È possibile eseguire queste operazioni durante la distribuzione, ma si consiglia di farlo prima di iniziare.

Andare troppo[passaggio 5: preparare Azure](hyper-v-site-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-hyper-v"></a>Passaggio 6: Preparare Hyper-V

Assicurarsi che i server Hyper-V soddisfino i requisiti di distribuzione di Site Recovery.

Andare troppo[passaggio 6: preparazione Hyper-V](hyper-v-site-walkthrough-prepare-hyper-v.md)

## <a name="step-7-set-up-a-vault"></a>Passaggio 7: Configurare un insieme di credenziali

È necessario tooset backup un tooorchestrate insieme di credenziali di servizi di ripristino e gestire la replica. Quando si imposta l'insieme di credenziali hello, specificare gli elementi da tooreplicate, e in cui si desidera tooreplicate a.

Andare troppo[passaggio 7: creare un insieme di credenziali](hyper-v-site-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Passaggio 8: Configurare le impostazioni di origine e di destinazione

Consente di impostare hello origine e di destinazione che viene utilizzato per la replica. Configurare le impostazioni dell'origine include l'aggiunta di host Hyper-V tooa sito di Hyper-V, l'installazione di hello Provider di Site Recovery e l'agente di servizi di ripristino in ogni host Hyper-V e la registrazione del sito hello in hello che insieme di credenziali di servizi di ripristino.

Andare troppo[passaggio 8: impostare hello origine e di destinazione](hyper-v-site-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Passaggio 9: Configurare i criteri di replica

Impostare le impostazioni di replica toospecify un criterio per le macchine virtuali Hyper-V nell'insieme di credenziali hello.

Andare troppo[passaggio 9: configurare un criterio di replica](hyper-v-site-walkthrough-replication.md)


## <a name="step-10-enable-replication"></a>Passaggio 10: Abilitare la replica

Dopo aver creato un criterio di replica sul posto, dopo aver abilitato, viene eseguita la replica iniziale di VM hello.

Andare troppo[passaggio 10: abilitare la replica](hyper-v-site-walkthrough-enable-replication.md)

## <a name="step-11-run-a-test-failover"></a>Passaggio 11: Eseguire un failover di test

Dopo il completamento della replica iniziale e la replica differenziale è in esecuzione, è possibile eseguire un toomake di failover di test che tutto funziona come previsto.

Andare troppo[passaggio 11: eseguire un failover di test](hyper-v-site-walkthrough-test-failover.md)
