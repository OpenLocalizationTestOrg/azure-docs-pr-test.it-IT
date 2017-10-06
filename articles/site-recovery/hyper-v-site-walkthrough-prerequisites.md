---
title: prerequisiti di hello aaaReview per Hyper-V tooAzure della replica (senza System Center VMM) usando Azure Site Recovery | Documenti Microsoft
description: Vengono descritti i prerequisiti hello per la configurazione di replica, il failover e il ripristino di tooAzure di macchine virtuali Hyper-V locale con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 7ef3fb46-52f5-4c8a-b1a1-658c2305762a
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: 3eefc3b7e3982ec6c413c1db7f7784863f9c701d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-2-review-hello-prerequisites-for-hyper-v-without-vmm-tooazure-replication"></a>Passaggio 2: Esaminare i prerequisiti di hello per la replica Hyper-V (senza VMM) tooAzure

prerequisiti di Hello sono riepilogati nella tabella di hello.


**Prerequisito** | **Dettagli** 
--- | --- 
**Azure** | Vedere i [requisiti di Azure](site-recovery-prereq.md#azure-requirements).
**Server locali** | [Altre informazioni](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm) sui requisiti per gli host Hyper-V locale di hello.
**VM Hyper-V locali** | Macchine virtuali che si desidera tooreplicate deve essere in esecuzione un [sistema operativo supportato](site-recovery-support-matrix-to-azure.md#support-for-replicated-machine-os-versions)e devono essere conformi con [Azure prerequisiti](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).
**URL di Azure** | Host Hyper-V è necessario accedere toothese URL:<br/><br/> [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]<br/><br/> Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.<br/></br> Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).<br/></br> Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).



## <a name="next-steps"></a>Passaggi successivi

- Se si sta eseguendo una distribuzione completa, andare troppo[passaggio 3: pianificare la capacità](hyper-v-site-walkthrough-capacity.md)
- Se si sta eseguendo una distribuzione di test semplice, andare troppo[passaggio 4: pianificare la rete](hyper-v-site-walkthrough-network.md).
