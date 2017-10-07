---
title: tooAzure aaaMigrate con il ripristino del sito | Documenti Microsoft
description: In questo articolo viene fornita una panoramica della migrazione di macchine virtuali e server fisici tooAzure con Azure Site Recovery
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: jwhit
editor: 
ms.assetid: c413efcd-d750-4b22-b34b-15bcaa03934a
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/05/2017
ms.author: raynew
ms.openlocfilehash: 6e65deee337c5371d441812ddb820dc8bc233684
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-tooazure-with-site-recovery"></a>Eseguire la migrazione tooAzure con il ripristino del sito

Leggere questo articolo per una panoramica dell'utilizzo del servizio Azure Site Recovery hello per la migrazione di macchine virtuali e server fisici.

Il ripristino del sito è un servizio di Azure che contribuisce strategia di BCDR tooyour dall'orchestrazione replica dei server fisici locali e macchine virtuali toohello cloud (Azure) o Data Center secondario tooa. Quando si verificano interruzioni nella propria posizione primaria, è possibile failover toohello posizione secondaria tookeep App e carichi di lavoro disponibili. Non si posizione primaria tooyour indietro quando vengono restituite le operazioni di toonormal. Per altre informazioni, vedere [Che cos'è Site Recovery?](site-recovery-overview.md) È possibile utilizzare anche il ripristino del sito toomigrate esistente locale tooexpedite tooAzure i carichi di lavoro del viaggio cloud e DISP hello gamma di funzionalità che offre Azure.

Per una rapida panoramica di come tooperform migrazione, consultare toothis video.
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

In questo articolo viene descritta la distribuzione in hello [portale di Azure](https://portal.azure.com). Hello [portale di Azure classico](https://manage.windowsazure.com/) possono essere utilizzati toomaintain esistenti insiemi di credenziali per il ripristino del sito, ma non è possibile creare nuovi insiemi.

Inviare eventuali commenti nella parte inferiore di hello di questo articolo. Porre domande tecniche su hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="what-do-we-mean-by-migration"></a>Informazioni sulla migrazione

È possibile distribuire Site Recovery per la replica di macchine virtuali in locale e server fisici, tooAzure o tooa sito secondario. Replicare le macchine, eseguire il failover da sito primario di hello quando si verificano interruzioni e non riuscire li sito primario toohello indietro quando vengono ripristinati. In aggiunta toothis, è possibile utilizzare le macchine virtuali toomigrate il ripristino del sito e server fisici tooAzure, in modo che gli utenti possono accedere come macchine virtuali di Azure. La migrazione comporta la replica e il failover da hello tooAzure di sito primario e un movimento di completare la migrazione.

## <a name="what-can-site-recovery-migrate"></a>Elementi di cui è possibile eseguire la migrazione con Site Recovery

È possibile:

- Eseguire la migrazione dei carichi di lavoro in esecuzione in locale di macchine virtuali Hyper-V, le macchine virtuali VMware e server fisici, toorun nelle macchine virtuali di Azure. In questo scenario è anche possibile eseguire la replica completa e il failback.
- Eseguire la migrazione di [VM IaaS di Azure](site-recovery-migrate-azure-to-azure.md) tra aree di Azure. Questo scenario supporta attualmente solo la migrazione, non il failback.
- Eseguire la migrazione [istanze Windows AWS](site-recovery-migrate-aws-to-azure.md) tooAzure le macchine virtuali IaaS. Questo scenario supporta attualmente solo la migrazione, non il failback.

## <a name="migrate-on-premises-vms-and-physical-servers"></a>Eseguire la migrazione di server fisici e VM locali

toomigrate locale macchine virtuali Hyper-V, le macchine virtuali VMware e server fisici, seguire quasi hello stessi passaggi utilizzati per la replica normale.

1. Configurare un insieme di credenziali dei Servizi di ripristino
2. Configurare il server di gestione di hello richiesto (VMware, VMM, Hyper-V, a seconda di ciò che desidera toomigrate), aggiungerli toohello insieme di credenziali e specificare le impostazioni di replica.
3. Abilitare la replica per hello macchine si desidera toomigrate
4. Dopo la migrazione iniziale hello, eseguire una tooensure di failover di test rapido che funzionino come previsto.
5. Dopo aver verificato il funzionamento dell'ambiente di replica, si usa un failover pianificato o non pianificato a seconda della [tipologia supportata](site-recovery-failover.md) per lo scenario. È consigliabile usare un failover pianificato, quando possibile.
6. Per la migrazione, non necessario toocommit un failover o eliminarlo. Selezionare, invece, hello **completare la migrazione** opzione per ogni computer si desidera toomigrate.
     - In **elementi replicati**, fare doppio clic su hello macchina virtuale e fare clic su **completare la migrazione**. Fare clic su **OK** toocomplete. È possibile monitorare i progressi nelle proprietà della macchina virtuale, hello in mediante il monitoraggio di processo di migrazione completa hello in **i processi di ripristino del sito**.
     - Hello **completare la migrazione** azione termina il processo di migrazione hello, rimuove la replica per macchina hello e viene arrestata la fatturazione di Site Recovery per la macchina hello.

![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a>Eseguire la migrazione tra aree di Azure

È possibile eseguire la migrazione di VM di Azure tra aree usando Site Recovery. In questo scenario è supportata solo la migrazione. In altre parole, è possibile replicare macchine virtuali di Azure hello e il failover tooanother area, ma è Impossibile eseguire il failback. In questo scenario che è impostare un insieme di credenziali di servizi di ripristino, la distribuzione di una replica di toomanage server di configurazione locale, aggiungerlo toohello insieme di credenziali e specificare le impostazioni di replica. Abilitare la replica per le macchine hello desiderata toomigrate per eseguire un rapido test failover. Quindi si esegue un failover non pianificato con hello **completare la migrazione** opzione.

## <a name="migrate-aws-tooazure"></a>Eseguire la migrazione di AWS tooAzure

È possibile eseguire la migrazione di istanze AWS tooAzure macchine virtuali. In questo scenario è supportata solo la migrazione. In altre parole, è possibile replicare le istanze di AWS hello e il failover tooAzure, ma è Impossibile eseguire il failback. Le istanze AWS vengono gestite in hello stesso come server fisici per la migrazione. Configurare un insieme di credenziali di servizi di ripristino, la distribuzione di una replica di toomanage server di configurazione locale, aggiungerlo toohello insieme di credenziali e specificare le impostazioni di replica. Abilitare la replica per le macchine hello desiderata toomigrate per eseguire un rapido test failover. Quindi si esegue un failover non pianificato con hello **completare la migrazione** opzione.




## <a name="next-steps"></a>Passaggi successivi

- [Eseguire la migrazione di macchine virtuali VMware tooAzure](site-recovery-vmware-to-azure.md)
- [Eseguire la migrazione di macchine virtuali Hyper-V in VMM cloud tooAzure](site-recovery-vmm-to-azure.md)
- [Eseguire la migrazione di macchine virtuali Hyper-V senza tooAzure VMM](site-recovery-hyper-v-site-to-azure.md)
- [Eseguire la migrazione di VM di Azure tra aree di Azure](site-recovery-migrate-azure-to-azure.md)
- [Eseguire la migrazione di AWS istanze tooAzure](site-recovery-migrate-aws-to-azure.md)
- [Preparare la migrazione di macchine tooenable replica](site-recovery-azure-to-azure-after-migration.md) tooanother area per esigenze di ripristino di emergenza.
- Iniziare a proteggere i carichi di lavoro [replicando le macchine virtuali di Azure](site-recovery-azure-to-azure.md).
