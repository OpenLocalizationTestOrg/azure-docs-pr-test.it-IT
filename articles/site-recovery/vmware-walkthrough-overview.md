---
title: aaaReplicate tooAzure di macchine virtuali VMware con Azure Site Recovery | Documenti Microsoft
description: Viene fornita una panoramica dei passaggi di hello per la replica dei carichi di lavoro in esecuzione in macchine virtuali VMware tooAzure
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 7104f67a3635b916048dcb61bca770c89f0c77fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-vmware-vms-tooazure-with-site-recovery"></a>Replicare le macchine virtuali VMware tooAzure con il ripristino del sito

In questo articolo viene fornita una panoramica di hello passaggi necessari tooreplicate locale VMware le macchine virtuali tooAzure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.


![Processo di distribuzione](./media/vmware-walkthrough-overview/vmware-to-azure-process.png)

**Figura 1: Riepilogo del processo di distribuzione**

## <a name="step-1-review-architecture-and-prerequisites"></a>Passaggio 1: Esaminare l'architettura e i prerequisiti

Prima di iniziare la distribuzione, esaminare l'architettura dello scenario hello e assicurarsi di che aver compreso tutti i componenti di hello necessari toodeploy

Andare troppo[passaggio 1: esaminare l'architettura di hello](vmware-walkthrough-architecture.md)


## <a name="step-2-review-prerequisites"></a>Passaggio 2: Esaminare i prerequisiti

Assicurarsi di avere i prerequisiti di hello sul posto per ogni componente di distribuzione:

- **Prerequisiti di Azure**: sono necessari un account Microsoft Azure, reti di Azure e account di archiviazione.
- **Componenti locali di Site Recovery**: è necessario un computer che esegue i componenti locali di Site Recovery.
- **Prerequisiti di VMware locale**: È necessario tooset gli account in modo che il ripristino del sito possono accedere al server VMware e le macchine virtuali.
- **Macchine virtuali replicate**: le macchine virtuali desiderate tooreplicate necessità toocomply ai requisiti di Azure e hanno installato il componente del servizio Mobility hello.

Andare troppo[passaggio 2: esaminare i prerequisiti e limitazioni](vmware-walkthrough-prerequisites.md)

## <a name="step-3-plan-capacity"></a>Passaggio 3: Pianificare la capacità

Se si sta eseguendo una distribuzione completa, è necessario toofigure risorse quali la replica è necessario. Esistono un paio di strumenti disponibili toohelp si esegue questa operazione. Passare tooStep 2. Se si sta eseguendo una rapida Configura tootest hello ambiente è possibile ignorare questo passaggio.

Andare troppo[passaggio 3: pianificare la capacità](vmware-walkthrough-capacity.md)

## <a name="step-4-plan-networking"></a>Passaggio 4: Pianificare la rete

È necessario toodo alcuni pianificazione tooensure che macchine virtuali di Azure siano connessi toonetworks dopo che si verifica il failover e che dispongano di hello destra indirizzi IP della rete.

Andare troppo[passaggio 4: pianificare la rete](vmware-walkthrough-network.md)

##  <a name="step-5-prepare-azure-resources"></a>Passaggio 5: Preparare le risorse di Azure

Configurare le reti e le risorse di archiviazione di Azure prima di iniziare. È possibile eseguire queste operazioni durante la distribuzione, ma si consiglia di farlo prima di iniziare.

Andare troppo[passaggio 5: preparare Azure](vmware-walkthrough-prepare-azure.md)


## <a name="step-6-prepare-vmware"></a>Passaggio 6: Preparare VMware

È necessario tooset gli account utilizzati per il ripristino del sito:

- Accesso VMware virtualizzazione server tooautomatically rilevare le macchine virtuali.
- Accedere a servizio di mobilità hello tooinstall macchine virtuali. Ogni macchina virtuale si desidera tooreplicate deve avere l'agente di servizio di mobilità hello installato prima possibile abilitare la replica.

Andare troppo[passaggio 6: preparazione VMware](vmware-walkthrough-prepare-vmware.md)

## <a name="step-7-set-up-a-vault"></a>Passaggio 7: Configurare un insieme di credenziali

È necessario tooset backup un tooorchestrate insieme di credenziali di servizi di ripristino e gestire la replica. Quando si imposta l'insieme di credenziali hello, specificare gli elementi da tooreplicate, e in cui si desidera tooreplicate a.

Andare troppo[passaggio 7: configurare un insieme di credenziali](vmware-walkthrough-create-vault.md)

## <a name="step-8-configure-source-and-target-settings"></a>Passaggio 8: Configurare le impostazioni di origine e di destinazione

Consente di impostare hello origine e di destinazione che viene utilizzato per la replica. Configurare le impostazioni dell'origine include l'esecuzione del programma di installazione unificata tooinstall componenti Site Recovery di hello locali.

Andare troppo[passaggio 8: impostare hello origine e di destinazione](vmware-walkthrough-source-target.md)

## <a name="step-9-set-up-a-replication-policy"></a>Passaggio 9: Configurare i criteri di replica

Impostare le impostazioni di replica toospecify un criterio per le macchine virtuali VMware nell'insieme di credenziali hello.

Andare troppo[passaggio 9: configurare un criterio di replica](vmware-walkthrough-replication.md)

## <a name="step-10-install-hello-mobility-service"></a>Passaggio 10: Installare il servizio di mobilità hello

servizio di mobilità Hello deve essere installato in ogni macchina virtuale si desidera tooreplicate. Esistono alcuni modi tooset servizio hello con installazione push o pull.

Andare troppo[passaggio 10: installare il servizio Mobility hello](vmware-walkthrough-install-mobility.md)

## <a name="step-11-enable-replication"></a>Passaggio 11: Abilitare la replica

Dopo che il servizio di mobilità hello è in esecuzione in una macchina virtuale è possibile abilitare la replica. Dopo aver abilitato, viene eseguita la replica iniziale di VM hello.

Andare troppo[passaggio 11: abilitare la replica](vmware-walkthrough-enable-replication.md)

## <a name="step-12-run-a-test-failover"></a>Passaggio 12: Eseguire un failover di test

Dopo il completamento della replica iniziale e la replica differenziale è in esecuzione, è possibile eseguire un toomake di failover di test che tutto funziona come previsto.

Andare troppo[passaggio 12: eseguire un failover di test](vmware-walkthrough-test-failover.md)
