---
title: aaaSet di un insieme di credenziali per VMware replica tooAzure usando Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello tooset di un insieme di credenziali è necessario per VMware replica tooAzure usando Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 8bce940e-f19f-4418-8360-aee7b073519a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 8a7755a6c9a3f55f241c615e425285bc4b782493
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-vmware-replication-tooazure"></a>Passaggio 7: Configurare un insieme di credenziali per tooAzure replica VMware


In questo articolo viene descritto come configurare un insieme di credenziali, tooset e specificare le tooreplicate dal percorso locale, utilizzando hello tooAzure [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.


Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Scegliere un obiettivo di protezione

Selezionare gli elementi da tooreplicate, e in cui si desidera tooreplicate per.

1. Fare clic su **Insiemi di credenziali dei servizi di ripristino** e quindi sull'insieme di credenziali.
2. In hello risorsa Menu, fare clic su **Site Recovery** > **preparare l'infrastruttura** > **obiettivi della protezione dati**.
3. In **obiettivi della protezione dati**selezionare **tooAzure** > **Sì, con VMware vSphere Hypervisor**.



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 8: Imposta origine e destinazione](vmware-walkthrough-source-target.md)
