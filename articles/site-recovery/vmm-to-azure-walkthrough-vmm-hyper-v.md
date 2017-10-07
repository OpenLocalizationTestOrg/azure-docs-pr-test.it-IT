---
title: aaaPrepare System Center VMM per Hyper-V replica tooAzure | Documenti Microsoft
description: Viene descritto come server di System Center VMM tooprepare per tooAzure di replica Hyper-V, usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: afcd81ae-d192-4013-a0af-3dac45b3c7e9
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/23/2017
ms.author: raynew
ms.openlocfilehash: 773b06afaf7d3eea1fe64f050bf3970943cf466a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-prepare-vmm-servers-and-hyper-v-hosts-for-hyper-v-replication-tooazure"></a>Passaggio 6: Preparare i server VMM e host Hyper-V per Hyper-V replica tooAzure

Dopo l'impostazione [componenti di Azure](vmm-to-azure-walkthrough-prepare-azure.md) per la distribuzione di hello, utilizzare le istruzioni di hello in questo server VMM locali tooprepare di articolo e toointeract gli host Hyper-V con Azure Site Recovery.

Dopo aver letto questo articolo, inviare eventuali commenti nella parte inferiore di hello o porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="prepare-vmm-servers"></a>Preparare i server VMM

- È necessario almeno un server VMM che soddisfano i requisiti di hello supporto per la replica di Site Recovery (site-recovery-support-matrix-to-azure.md#support-for-datacenter-management-servers).
- Assicurarsi che preparato il server VMM hello per [mapping di rete](vmm-to-azure-walkthrough-network.md#network-mapping-for-replication-to-azure).
- Verificare che il server VMM hello possibile accedere a questi URL

    [!INCLUDE [site-recovery-URLS](../../includes/site-recovery-URLS.md)]
    
- Se si dispone di regole del firewall basato su indirizzi IP, assicurarsi che consentano la comunicazione tooAzure.
- Consenti hello [intervalli IP dei Data Center Azure](https://www.microsoft.com/download/confirmation.aspx?id=41653)e hello porta HTTPS (443).
- Consenti gli intervalli di indirizzi IP per hello area della sottoscrizione di Azure e per Stati Uniti occidentali (utilizzato per il controllo di accesso e gestione delle identità).

Durante la distribuzione di Site Recovery, si scarica hello Provider di Site Recovery e installarlo in ogni server VMM. server VMM Hello è registrato nell'insieme di credenziali di servizi di ripristino hello.




## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 7: creare un insieme di credenziali](vmm-to-azure-walkthrough-create-vault.md)

