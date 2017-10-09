---
title: aaaPrepare Hyper-V ospita (senza System Center VMM) per la replica tooAzure | Documenti Microsoft
description: Viene descritto come tooprepare Hyper-V ospita per replica tooAzure usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 0f204e24-8d78-4076-95c5-8137d1be9c01
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: 714b229d5efbd66a9844bd09e36ac3f69919a6bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-hyper-v-hosts-for-replication-tooazure"></a>Passaggio 6: Preparare l'host Hyper-V per la replica tooAzure

Hello seguire le istruzioni riportate in questo articolo di tooprepare locale toointeract gli host Hyper-V con Azure Site Recovery.

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-hosts"></a>Preparare gli host

- Verificare che gli host Hyper-V hello soddisfino hello [prerequisiti](site-recovery-prereq.md#disaster-recovery-of-hyper-v-vms-to-azure-no-vmm).
- Assicurarsi che gli host hello possono accedere agli URL di hello necessarie:

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.
- Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).
- Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).

Durante la distribuzione di Site Recovery, aggiungere gli host Hyper-V che contengono macchine virtuali che si desidera che il sito di Hyper-V tooa tooreplicate. Provider di Site Recovery Hello e dell'agente di servizi di ripristino vengono installati in ogni host. sito Hello Hyper-V è registrato nell'insieme di credenziali di servizi di ripristino hello.

## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 7: creare un insieme di credenziali](hyper-v-site-walkthrough-create-vault.md)

