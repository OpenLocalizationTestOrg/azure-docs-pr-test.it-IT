---
title: architettura di hello aaaReview per la replica delle macchine virtuali di Azure tra le aree di Azure | Documenti Microsoft
description: In questo articolo viene fornita una panoramica dei componenti e architettura utilizzata durante la replica delle macchine virtuali di Azure tra le aree di Azure tramite il servizio di Azure Site Recovery hello.
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/12/2017
ms.author: raynew
ms.openlocfilehash: 4caab4e7a764040f317201d1345c40c73f836d81
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-1-review-hello-architecture-for-azure-vm-replication-between-azure-regions"></a>Passaggio 1: Esaminare l'architettura di hello per la replica di macchina virtuale di Azure tra le aree di Azure


Dopo aver esaminato hello [passaggi Panoramica](azure-to-azure-walkthrough-overview.md) per questa distribuzione, leggere questo componenti hello toounderstand di articolo e processi utilizzati quando si esegue la replica e il ripristino delle macchine virtuali di Azure (VM) da un'area di Azure tooanother, utilizzando [Azure Site Recovery](site-recovery-overview.md).

- Dopo aver articolo hello, è necessario comprendere a fondo il funzionamento area tooanother replica di macchina virtuale di Azure.
- Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

>[!NOTE]
>Replica di macchina virtuale di Azure con hello servizio Site Recovery è attualmente in anteprima.



## <a name="architectural-components"></a>Componenti dell'architettura

Hello seguente diagramma mostra una panoramica generale di un ambiente di macchina virtuale di Azure in un'area specifica (in questo esempio, il percorso di Stati Uniti orientali hello). In un ambiente di VM di Azure:
- Le app possono essere in esecuzione in macchine virtuali con dischi distribuiti tra gli account di archiviazione.
- Hello macchine virtuali può essere inclusi in uno o più subnet all'interno di una rete virtuale.

![customer-environment](./media/azure-to-azure-walkthrough-architecture/source-environment.png)

## <a name="replication-process"></a>Processo di replica

### <a name="step-1"></a>Passaggio 1

Quando si abilita la replica di macchina virtuale di Azure nel portale di Azure hello, hello risorse visualizzate in hello seguente diagramma e la tabella vengono creati automaticamente nell'area di destinazione hello. Per impostazione predefinita, le risorse vengono create in base alle impostazioni dell'area di origine. È possibile personalizzare le impostazioni di destinazione hello come richiesto. [Altre informazioni](site-recovery-replicate-azure-to-azure.md)

![Abilitare il processo di replica - Passaggio 1](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-1.png)

**Risorsa** | **Dettagli**
--- | ---
**Gruppo di risorse di destinazione** | Hello toowhich gruppo di risorse appartengono le macchine virtuali replicate dopo il failover.
**Rete virtuale di destinazione** | rete virtuale Hello in cui si trovano le macchine virtuali replicate dopo il failover. Un mapping di rete viene creato tra le reti virtuali di origine e di destinazione e viceversa.
**Account di archiviazione della cache** | Prima che le modifiche nell'origine che sono macchine virtuali replicate toohello account di archiviazione di destinazione, vengono rilevati e inviati toohello account di archiviazione della cache nel percorso di destinazione hello. In questo modo un impatto minimo sulle app di produzione in esecuzione su hello macchina virtuale.
**Account di archiviazione di destinazione**  | Gli account di archiviazione di dati di hello destinazione percorso toowhich hello viene replicata.
**Set di disponibilità di destinazione**  | Set di disponibilità in cui hello replicata le macchine virtuali si trovano dopo il failover.

### <a name="step-2"></a>Passaggio 2

Come la replica è abilitata, viene automaticamente installata hello estensione per il ripristino del sito servizio di mobilità hello macchina virtuale. si verifica in seguito Hello:

1. Hello VM è registrato con il ripristino del sito.

2. La replica continua è configurata per hello macchina virtuale. Dati scrive sul hello macchina virtuale i dischi vengono sempre trasferiti toohello account di archiviazione della cache nel percorso di origine hello.

   ![Abilitare il processo di replica - Passaggio 2](./media/azure-to-azure-walkthrough-architecture/enable-replication-step-2.png)

  
  Si noti che il ripristino del sito non deve mai in ingresso connettività toohello macchina virtuale. Solo in uscita indirizzi URL/IP di servizio di integrazione applicativa tooSite ripristino, l'autenticazione di Office 365 URL/e gli indirizzi IP, indirizzi IP account di archiviazione della cache è necessaria. 

## <a name="continuous-replication-process"></a>Processo di replica continua

Dopo che utilizza la replica continua, disco operazioni di scrittura sono immediatamente trasferito toohello account di archiviazione della cache. Il ripristino del sito elabora i dati di hello e lo invia toohello account di archiviazione di destinazione. Dopo l'elaborazione dati hello, punti di ripristino vengono generati nell'account di archiviazione di destinazione hello ogni pochi minuti.

## <a name="failover-process"></a>Processo di failover

Quando si avvia un failover, le macchine virtuali vengono create nella rete virtuale di destinazione, gruppo di risorse di destinazione hello alla subnet di destinazione hello e hello di destinazione set di disponibilità. Durante un failover è possibile usare qualsiasi punto di ripristino.

![Processo di failover](./media/azure-to-azure-walkthrough-architecture/failover.png)

## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 2: verificare i prerequisiti e limitazioni](azure-to-azure-walkthrough-prerequisites.md)
