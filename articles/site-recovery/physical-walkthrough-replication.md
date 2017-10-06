---
title: aaaSet un criterio di replica per tooAzure replica server fisico con Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello è necessario tooset un criterio di replica quando la replica locale server fisici tooAzure di archiviazione utilizzando il servizio di Azure Site Recovery hello"
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
ms.openlocfilehash: d6bdeeffc24ffc8eaba24311f7c76452edb65648
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-8-set-up-a-replication-policy-for-physical-server-replication-tooazure"></a>Passaggio 8: Impostare un criterio di replica per tooAzure replica server fisico


Questo articolo viene descritto come tooset un criterio di replica quando si esegue la replica tooAzure server fisici Windows/Linux utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.


Inviare commenti e domande nella parte inferiore di hello di questo articolo, o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="configure-a-policy"></a>Configurare i criteri

1. Fare clic su **Infrastruttura di Site Recovery** > **Criteri di replica** > **+Criteri di replica**.
2. In **Creare i criteri di replica** specificare un nome per i criteri.
3. In **soglia RPO**, specificare il limite RPO hello. Questo valore indica la frequenza con cui vengono creati punti di ripristino dei dati. Se la replica continua supera questo limite, viene generato un avviso.
4. In **conservazione del punto di ripristino**, specificare per quanto tempo (in ore) è un intervallo di conservazione hello per ogni punto di ripristino. Macchine virtuali replicate possono essere ripristinati tooany punto in una finestra. Backup too24 conservazione ore è supportata per i computer replicati archiviazione toopremium e 72 ore per l'archiviazione standard.
5. In **Frequenza snapshot coerenti con l'app**specificare la frequenza, in minuti, per la creazione di punti di ripristino contenenti snapshot coerenti con l'applicazione. Fare clic su **OK** criteri hello toocreate.

    ![Criteri di replica](./media/physical-walkthrough-replication/gs-replication2.png)
8. Quando si crea un nuovo criterio associata automaticamente con il server di configurazione di hello. Per impostazione predefinita vengono creati automaticamente criteri corrispondenti per il failback. Ad esempio, se hello criterio di replica è **rep criteri** verrà utilizzato come criterio di failback hello **rep-criteri-failback**. Questi criteri non vengono usati fino a quando non si avvia un failback da Azure.

## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 9: installare il servizio Mobility hello](physical-walkthrough-install-mobility.md)
