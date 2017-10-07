---
title: aaaSet un criterio di replica per tooAzure replica VMware VM con Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello è necessario tooset un criterio di replica per la replica di archiviazione di macchine virtuali VMware tooAzure"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: d7874bd8-6626-4668-9ec9-dbd2d26f8f81
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 12870f3f98a4dd412221b817581403cd4bf7a76d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-9-set-up-a-replication-policy-for-vmware-vm-replication-tooazure"></a>Passaggio 9: Configurare un criterio di replica per VMware VM replica tooAzure


Questo articolo viene descritto come tooset un criterio di replica quando si esegue la replica di macchine virtuali VMware tooAzure utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.


Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Configurare i criteri

Ottenere una rapida panoramica video prima di iniziare:
> [!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video2-vCenter-Server-Discovery-and-Replication-Policy/player]

1. toocreate nuovi criteri di replica, fare clic su **dell'infrastruttura di Site Recovery** > **criteri di replica** > **+ criterio di replica**.
2. In **Creare i criteri di replica** specificare un nome per i criteri.
3. In **soglia RPO**, specificare il limite RPO hello. Questo valore specifica la frequenza con cui vengono creati punti di ripristino dei dati. Se la replica continua supera questo limite, viene generato un avviso.
4. In **conservazione del punto di ripristino**, specificare per quanto tempo (in ore) è un intervallo di conservazione hello per ogni punto di ripristino. Macchine virtuali replicate possono essere ripristinati tooany punto in una finestra. Backup too24 conservazione ore è supportata per i computer replicati archiviazione toopremium e 72 ore per l'archiviazione standard.
5. In **Frequenza snapshot coerenti con l'app**specificare la frequenza, in minuti, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione. Fare clic su **OK** criteri hello toocreate.

    ![Criteri di replica](./media/vmware-walkthrough-replication/gs-replication2.png)
8. Quando si crea un nuovo criterio associata automaticamente con il server di configurazione di hello. Per impostazione predefinita vengono creati automaticamente criteri corrispondenti per il failback. Ad esempio, se hello criterio di replica è **rep criteri** verrà utilizzato come criterio di failback hello **rep-criteri-failback**. Questi criteri non vengono usati fino a quando non si avvia un failback da Azure.

## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 10: installare il servizio Mobility hello](vmware-walkthrough-install-mobility.md)
