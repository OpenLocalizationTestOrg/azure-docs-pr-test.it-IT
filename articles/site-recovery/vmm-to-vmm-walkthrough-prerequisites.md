---
title: prerequisiti di hello aaaReview per Hyper-V replica tooa sito VMM secondario con Azure Site Recovery | Documenti Microsoft
description: Vengono descritti i prerequisiti hello per la replica delle macchine virtuali Hyper-V tooa VMM del sito secondario con Azure Site Recovery.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 21ff0545-8be5-4495-9804-78ab6e24add6
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/30/2017
ms.author: raynew
ms.openlocfilehash: 1bd945fdda36c3cce5d159209abbd3c98a7e3682
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-and-limitations-for-hyper-v-vm-replication-tooa-secondary-vmm-site"></a>Passaggio 2: Esaminare hello prerequisiti e limitazioni per la macchina virtuale Hyper-V replica tooa VMM del sito secondario


Dopo aver esaminato hello [architettura dello scenario](vmm-to-vmm-walkthrough-architecture.md), leggere questo articolo di toomake è importante comprendere i prerequisiti di distribuzione hello, quando la replica delle macchine virtuali di Hyper-V locale (VM) gestiti in System Center Virtual Cloud Machine Manager (VMM), tooa secondario del sito utilizzando [Azure Site Recovery](site-recovery-overview.md) in hello portale di Azure.

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prerequisites-and-limitations"></a>Prerequisiti e limitazioni

**Requisito** | **Dettagli**
--- | ---
**Azzurro** | Una sottoscrizione di [Microsoft Azure](http://azure.microsoft.com/).<br/><br/> È possibile iniziare con una [versione di valutazione gratuita](https://azure.microsoft.com/pricing/free-trial/).<br/><br/> [Altre informazioni](https://azure.microsoft.com/pricing/details/site-recovery/) sui prezzi di Site Recovery.<br/><br/> Verificare le aree di hello è supportato per il ripristino del sito, in aree geografiche disponibili in [dettagli prezzi di Azure Site Recovery](https://azure.microsoft.com/pricing/details/site-recovery/).
**Server VMM** | È consigliabile che disporre di due server VMM, uno nel sito primario di hello e uno in hello secondario.<br/><br/> È possibile eseguire la replica tra cloud in un unico server VMM.<br/><br/> Server VMM devono essere in esecuzione almeno System Center 2012 SP1 con gli aggiornamenti più recenti di hello.<br/><br/> I server VMM richiedono l'accesso a Internet.
**Cloud VMM** | Ogni server VMM deve essere in uno o più cloud e in tutte le aree è necessario impostare il profilo di capacità Hyper-V hello. <br/><br/>I cloud devono contenere uno o più gruppi host VMM.<br/><br/> Se si dispone solo di un server VMM, è necessario almeno due cloud, tooact come primario e secondario.
**Hyper-V** | Server Hyper-V deve essere in esecuzione almeno Windows Server 2012 con il ruolo Hyper-V hello, e hanno hello installati aggiornamenti più recenti.<br/><br/> Il server Hyper-V deve contenere una o più macchine virtuali.<br/><br/>  Server host Hyper-V devono essere distribuiti nei gruppi host nei cloud VMM primario e secondario di hello.<br/><br/> Se si esegue Hyper-V in un cluster in Windows Server 2012 R2 installare l'[aggiornamento 2961977](https://support.microsoft.com/kb/2961977)<br/><br/> Se si esegue Hyper-V in un cluster basato su indirizzi IP statici in Windows Server 2012, il broker del cluster non viene creato automaticamente. Configurare un gestore cluster hello manualmente. [Altre informazioni](http://social.technet.microsoft.com/wiki/contents/articles/18792.configure-replica-broker-role-cluster-to-cluster-replication.aspx).<br/><br/> I server Hyper-V richiedono l'accesso a Internet.




## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 3: pianificare la rete](vmm-to-vmm-walkthrough-network.md).
