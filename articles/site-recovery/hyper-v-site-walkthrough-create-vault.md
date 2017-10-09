---
title: aaaSet di un insieme di credenziali per Hyper-V replica (senza System Center VMM) tooAzure usando Azure Site Recovery | Documenti Microsoft
description: Vengono riepilogati i passaggi di hello tooset di un insieme di credenziali necessarie per Hyper-V replica tooAzure usando Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a936b3e2-0dbe-47ac-a98e-5285d96dc786
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/22/2017
ms.author: raynew
ms.openlocfilehash: e3ef8758faab36d19d0968d98a23105bed7830f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-7-set-up-a-vault-for-hyper-v-replication"></a>Passaggio 7: Configurare un insieme di credenziali per la replica Hyper-V

In questo articolo viene descritto come configurare un insieme di credenziali, tooset e specificare le tooreplicate dal percorso locale, utilizzando hello tooAzure [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.


Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]



## <a name="select-a-protection-goal"></a>Scegliere un obiettivo di protezione

Selezionare gli elementi da tooreplicate, e in cui si desidera tooreplicate per.

1. Fare clic su **Insiemi di credenziali dei servizi di ripristino** e quindi sull'insieme di credenziali.
2. In hello risorsa Menu, fare clic su **Site Recovery** > **preparare l'infrastruttura** > **obiettivi della protezione dati**.
3. In **obiettivi della protezione dati**selezionare **tooAzure** > **Sì, con Hyper-V**. Selezionare **n** tooconfirm VMM non è in uso. 

    ![Scegliere gli obiettivi](./media/hyper-v-site-walkthrough-create-vault/choose-goals2.png)



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 8: Imposta origine e destinazione](hyper-v-site-walkthrough-source-target.md)
