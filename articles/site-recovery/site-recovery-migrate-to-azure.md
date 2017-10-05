---
title: Eseguire la migrazione ad Azure con Site Recovery | Documentazione Microsoft
description: Questo articolo offre una panoramica della migrazione di VM e server fisici ad Azure con Azure Site Recovery
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
ms.openlocfilehash: f4dfe430fba51bd009431ca72279a21be55e3a40
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-to-azure-with-site-recovery"></a>Eseguire la migrazione ad Azure con Site Recovery

Leggere questo articolo per una panoramica dell'uso del servizio Azure Site Recovery per la migrazione di macchine virtuali e server fisici.

Site Recovery è un servizio di Azure che contribuisce all'attuazione della strategia per la continuità aziendale e il ripristino di emergenza orchestrando la replica delle macchine virtuali e dei server fisici locali nel cloud di Azure o in un data center secondario. In caso di interruzioni nella località primaria, verrà eseguito il failover alla località secondaria per mantenere disponibili app e carichi di lavoro. Quando la località primaria sarà di nuovo operativa, si tornerà a tale località. Per altre informazioni, vedere [Che cos'è Site Recovery?](site-recovery-overview.md) È possibile inoltre usare Site Recovery per eseguire la migrazione di carichi di lavoro locali esistenti in Azure per accelerare il viaggio verso il cloud e accedere alla gamma di funzionalità offerte da Azure.

Per una rapida panoramica di come eseguire la migrazione, guardare questo video.
>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/ASRHowTo-Video2-Migrate-Virtual-Machines-to-Azure/player]

Questo articolo descrive la distribuzione nel [portale di Azure](https://portal.azure.com). Il [portale di Azure classico](https://manage.windowsazure.com/) può essere usato per gestire gli insiemi di credenziali di Site Recovery esistenti, ma non per crearne di nuovi.

È possibile inserire commenti nella parte inferiore di questo articolo. In caso di domande tecniche, visitare il [forum di Azure Site Recovery](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).


## <a name="what-do-we-mean-by-migration"></a>Informazioni sulla migrazione

È possibile distribuire Site Recovery per la replica di macchine virtuali e server fisici in locale, in Azure o in un sito secondario. L'utente esegue la replicare delle macchine, il failover dal sito primario quando si verificano interruzioni e il failback al sito primario quando si esegue il ripristino. Inoltre è possibile usare Site Recovery per eseguire la migrazione di VM e server fisici ad Azure e consentire così agli utenti di accedervi come VM di Azure. La migrazione comporta la replica, il failover dal sito primario ad Azure e il completamento della migrazione.

## <a name="what-can-site-recovery-migrate"></a>Elementi di cui è possibile eseguire la migrazione con Site Recovery

È possibile:

- Eseguire la migrazione di carichi di lavoro in esecuzione in server fisici e VM Hyper-V e VMware locali, perché vengano eseguiti in VM di Azure. In questo scenario è anche possibile eseguire la replica completa e il failback.
- Eseguire la migrazione di [VM IaaS di Azure](site-recovery-migrate-azure-to-azure.md) tra aree di Azure. Questo scenario supporta attualmente solo la migrazione, non il failback.
- Eseguire la migrazione di [istanze di Windows per Amazon Web Services](site-recovery-migrate-aws-to-azure.md) a VM IaaS di Azure. Questo scenario supporta attualmente solo la migrazione, non il failback.

## <a name="migrate-on-premises-vms-and-physical-servers"></a>Eseguire la migrazione di server fisici e VM locali

Per eseguire la migrazione di server fisici e VM VMware e Hyper-V locali, si segue approssimativamente la stessa procedura usata per la replica normale.

1. Configurare un insieme di credenziali dei Servizi di ripristino
2. Configurare i server di gestione necessari (VMware, VMM o Hyper-V a seconda degli elementi di cui si vuole eseguire la migrazione), aggiungerli all'insieme di credenziali e specificare le impostazioni di replica.
3. Abilitare la replica per le macchine virtuali di cui eseguire la migrazione
4. Dopo la migrazione iniziale, eseguire un rapido failover di test per verificare che tutto funzioni come previsto.
5. Dopo aver verificato il funzionamento dell'ambiente di replica, si usa un failover pianificato o non pianificato a seconda della [tipologia supportata](site-recovery-failover.md) per lo scenario. È consigliabile usare un failover pianificato, quando possibile.
6. Per la migrazione non è necessario eseguire il commit del failover oppure eliminarlo. Si seleziona invece l'opzione **Completa la migrazione** per ogni computer di cui si vuole eseguire la migrazione.
     - In **Elementi replicati** fare clic con il pulsante destro del mouse sulla macchina virtuale e scegliere **Completa la migrazione**. Fare clic su **OK** per completare la migrazione. È possibile tenere traccia dello stato del processo nelle proprietà della VM oppure monitorando il processo Completa la migrazione in **Processi di Site Recovery**.
     - L'azione **Completa la migrazione** porta a termine il processo di migrazione, rimuove la replica per il computer e interrompe la relativa fatturazione di Site Recovery.

![completemigration](./media/site-recovery-hyper-v-site-to-azure/migrate.png)

## <a name="migrate-between-azure-regions"></a>Eseguire la migrazione tra aree di Azure

È possibile eseguire la migrazione di VM di Azure tra aree usando Site Recovery. In questo scenario è supportata solo la migrazione. In altri termini, è possibile replicare VM di Azure ed effettuarne il failover in un'altra area, ma non eseguire il failback. In questo scenario si configura un insieme di credenziali di Servizi di ripristino, si distribuisce un server di configurazione locale per gestire la replica, si aggiunge tale server all'insieme di credenziali e si specificano le impostazioni di replica. Dopo aver abilitato la replica per i computer di cui si vuole eseguire la migrazione, si effettua un rapido failover di test. Si esegue quindi un failover non pianificato con l'opzione **Completa la migrazione**.

## <a name="migrate-aws-to-azure"></a>Eseguire la migrazione da AWS ad Azure

È possibile eseguire la migrazione di istanze AWS a VM di Azure. In questo scenario è supportata solo la migrazione. In altri termini, è possibile replicare le istanze AWS ed effettuarne il failover in Azure, ma non eseguire il failback. Ai fini della migrazione, le istanze AWS vengono gestite come i server fisici. Si configura un insieme di credenziali di Servizi di ripristino, si distribuisce un server di configurazione locale per gestire la replica, si aggiunge tale server all'insieme di credenziali e si specificano le impostazioni di replica. Dopo aver abilitato la replica per i computer di cui si vuole eseguire la migrazione, si effettua un rapido failover di test. Si esegue quindi un failover non pianificato con l'opzione **Completa la migrazione**.




## <a name="next-steps"></a>Passaggi successivi

- [Eseguire la migrazione di VM VMware ad Azure](site-recovery-vmware-to-azure.md)
- [Eseguire la migrazione di VM Hyper-V in cloud VMM ad Azure](site-recovery-vmm-to-azure.md)
- [Eseguire la migrazione di VM Hyper-V senza VMM ad Azure](site-recovery-hyper-v-site-to-azure.md)
- [Eseguire la migrazione di VM di Azure tra aree di Azure](site-recovery-migrate-azure-to-azure.md)
- [Eseguire la migrazione di istanze AWS ad Azure](site-recovery-migrate-aws-to-azure.md)
- [Preparare le macchine sottoposte a migrazione per abilitare la replica](site-recovery-azure-to-azure-after-migration.md) in un'altra area per il ripristino di emergenza.
- Iniziare a proteggere i carichi di lavoro [replicando le macchine virtuali di Azure](site-recovery-azure-to-azure.md).
