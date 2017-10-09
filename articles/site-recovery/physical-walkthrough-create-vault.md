---
title: aaaSet di un insieme di credenziali per il server fisico replica tooAzure usando Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello è necessario tooset backup tooAzure di server fisici tooreplicate un insieme di credenziali usando Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d99f2605-f417-4995-be77-5323136b814f
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 988928e3ece31116823f132cc39223fe44443468
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-set-up-a-vault-for-physical-server-replication-tooazure"></a>Passaggio 6: Configurare un insieme di credenziali per tooAzure replica server fisico


Questo articolo viene descritto come tooset di un insieme di credenziali. Creare l'insieme di credenziali hello e specificare gli elementi da tooreplicate dal tooAzure percorso locale, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.


Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).




## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

## <a name="select-a-protection-goal"></a>Scegliere un obiettivo di protezione

Selezionare gli elementi da tooreplicate, e in cui si desidera tooreplicate per.

1. Fare clic su **Insiemi di credenziali dei servizi di ripristino** e quindi sull'insieme di credenziali.
2. In hello risorsa Menu, fare clic su **Site Recovery** > **preparare l'infrastruttura** > **obiettivi della protezione dati**.
3. In **obiettivi della protezione dati**selezionare **tooAzure** > **non virtualizzato/altri**.


## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 7: configurare l'origine e di destinazione](physical-walkthrough-source-target.md)
