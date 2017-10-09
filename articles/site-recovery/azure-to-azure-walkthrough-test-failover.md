---
title: un failover di test per la replica di macchina virtuale di Azure con Azure Site Recovery aaaRun | Documenti Microsoft
description: Vengono riepilogati i passaggi di hello che necessario per l'esecuzione di un failover di test per le macchine virtuali di Azure la replica con area di Azure tooanother hello Azure Site Recovery di servizio.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: e15c1b0c-5d75-4fdf-acb0-e61def9e9339
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/01/2017
ms.author: raynew
ms.openlocfilehash: c1f765aa94c59dd70b33317ebbcd04beb7977969
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-6-run-a-test-failover-for-azure-vm-replication"></a>Passaggio 6: Eseguire un failover di test per la replica della macchina virtuale di Azure

Dopo avere abilitato la replica per la macchina virtuale di Azure (VM), seguire i passaggi di hello in questo articolo, il failover di test toorun da tooanother un'area di Azure, utilizzando hello [Azure Site Recovery](site-recovery-overview.md) di hello portale di Azure.

- Dopo aver articolo hello, deve aver verificato con un failover di test, che almeno una macchina virtuale di Azure può eseguire il failover tooyour area secondaria di Azure. 
- Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> La replica di macchine virtuali di Azure è attualmente in anteprima.


## <a name="before-you-start"></a>Prima di iniziare

- Prima di eseguire un failover di test, è consigliabile verificare le proprietà della VM hello e apportare le modifiche è necessario. è possibile accedere a proprietà della macchina virtuale hello in **gli elementi replicati**. Hello **Essentials** pannello mostra le informazioni sulle impostazioni computer e lo stato.
- Si consiglia di usare una rete VM di Azure separata per il failover di test hello e non in rete di hello (predefinito o personalizzato) che è stato configurato per il failover di produzione.
- Hello test failover failover delle macchine virtuali di Azure (e relativo spazio di archiviazione) toohello area secondaria di Azure. Non vengono replicate eventuali app o risorse dipendenti. Se l'App in esecuzione su non riuscito su macchine virtuali sono dipendenti da altre risorse, ad esempio Active Directory o DNS, è necessario tooreplicate questi troppo, se non sono già disponibili nell'area secondaria. [Altre informazioni](site-recovery-test-failover-to-azure.md#prepare-active-directory-and-dns)
- Se si desidera tooaccess replicate le macchine virtuali dopo il failover da un sito locale, è necessario troppo[preparare tooconnect](site-recovery-test-failover-to-azure.md#prepare-to-connect-to-azure-vms-after-failover) toothese macchine virtuali.

## <a name="run-a-test-failover"></a>Eseguire un failover di test

1. In **impostazioni** > **elementi replicati**, fare clic su hello VM **+ Test Failover** icona. 

2. In **Failover di Test**, selezionare un toouse del punto di ripristino per il failover hello:

    - **Ultima elaborazione**: ha esito negativo hello VM sul punto di ripristino più recente toohello che è stato elaborato dal servizio Site Recovery hello. viene visualizzato l'indicatore data e ora Hello. Con questa opzione, non viene impiegato alcun tempo di elaborazione dati, pertanto viene fornito un RTO (Recovery Time Objective) basso.
    - **Versione più recente coerente con app**: questa opzione non funziona su tutte le macchine virtuali toohello più recente coerente con l'app punto di ripristino. viene visualizzato l'indicatore data e ora Hello. 
    - **Personalizzazione**: selezionare qualsiasi punto di ripristino.
 
3. Verranno connesse toowhich di rete virtuale di Azure di destinazione selezionare hello macchine virtuali di Azure nell'area secondaria hello, dopo il failover hello.
4. toostart hello failover, fare clic su **OK**. tootrack sullo stato di avanzamento, fare clic su hello VM tooopen le relative proprietà. In alternativa, è possibile fare clic su hello **Failover di Test** processo nel nome dell'insieme di credenziali hello > **impostazioni** > **processi** > **iprocessidiripristinodelsito**.
5. Hello failover termine, replica hello macchina virtuale di Azure viene visualizzato nel portale di Azure hello > **macchine virtuali**. Assicurarsi che tale hello VM sia di dimensioni appropriate hello, che si è connesso toohello di rete appropriata e che sia in esecuzione.
6. Fare clic su toodelete hello macchine virtuali che sono stati creati durante il failover di test hello, **il failover di test di pulizia** su hello replicati hello o elemento piano di ripristino. In **note**, registrare e salvare eventuali commenti associati hello test failover. 

[Altre informazioni](site-recovery-test-failover-to-azure.md) sui failover di test.

## <a name="next-steps"></a>Passaggi successivi

Dopo aver testato il failover, questa procedura dettagliata viene completata. A questo punto, informazioni sull'esecuzione di failover nell'ambiente di produzione:

- [Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e come toorun li.
- Altre informazioni sul failover su più macchine virtuali [tramite un piano di ripristino](site-recovery-create-recovery-plans.md).
- Altre informazioni sull'[uso dei piani di ripristino](site-recovery-create-recovery-plans.md).
- Altre informazioni sulla [riprotezione delle VM di Azure](site-recovery-how-to-reprotect.md) dopo il failover.

