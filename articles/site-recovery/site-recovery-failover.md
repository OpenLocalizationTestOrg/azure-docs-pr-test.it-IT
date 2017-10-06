---
title: aaaFailover in Site Recovery | Documenti Microsoft
description: Azure Site Recovery coordina la replica di hello, failover e il ripristino delle macchine virtuali e server fisici. Informazioni su failover tooAzure o un Data Center secondario.
services: site-recovery
documentationcenter: 
author: prateek9us
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/04/2017
ms.author: pratshar
ms.openlocfilehash: 7cacea829d78bb7de2b2d67402291b472b10f023
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="failover-in-site-recovery"></a>Failover in Site Recovery
In questo articolo viene descritto come toofailover le macchine virtuali e server fisici protetta da Site Recovery.

## <a name="prerequisites"></a>Prerequisiti
1. Prima di eseguire un failover, eseguire una [failover di test](site-recovery-test-failover-to-azure.md) tooensure che funzionino come previsto.
1. [Preparare la rete hello](site-recovery-network-design.md) nel percorso di destinazione prima di eseguire un failover.  


## <a name="run-a-failover"></a>Eseguire un failover
Questa procedura viene descritto come toorun un failover per un [piano di ripristino](site-recovery-create-recovery-plans.md). In alternativa è possibile eseguire il failover hello per una singola macchina virtuale o un server fisico da hello **gli elementi replicati** pagina


![Failover](./media/site-recovery-failover/Failover.png)

1. Selezionare **Piani di ripristino** > *nome_pianodiripristino*. Fare clic su **Failover**.
2. In hello **Failover** selezionare un **punto di ripristino** toofailover per. È possibile utilizzare una delle seguenti opzioni hello:
    1.  **Più recente** (impostazione predefinita): questa opzione Elabora prima tutti i dati che sono stato inviato tooSite ripristino servizio toocreate un punto di ripristino per ogni macchina virtuale prima del failover li tooit hello. Questa opzione offre hello più basso RPO (Recovery Point Objective) come macchina virtuale hello creato dopo il failover ha tutti i dati di hello che è stata replicata tooSite servizio di ripristino quando hello failover è stato attivato.
    1.  **Ultima elaborazione**: questa opzione viene eseguito il failover tutte le macchine virtuali hello piano toohello ultimo ripristino del punto di ripristino che è già stato elaborato dal servizio Site Recovery. Quando si esegue il failover di test di una macchina virtuale, viene visualizzato anche i timestamp dell'ultimo punto di ripristino elaborato hello. Se si esegue il failover di un piano di ripristino, è possibile passare una macchina virtuale tooindividual e osservare **punti di ripristino più recente** riquadro tooget queste informazioni. Come non viene impiegato per l'ora tooprocess hello dati non elaborati, questa opzione offre un'opzione failover RTO (tempo Recovery Time Objective).
    1.  **Versione più recente coerente con app**: questa opzione non funziona su tutte le macchine virtuali di hello piano toohello più recente dell'applicazione ripristino coerenti con punto di ripristino che è già stato elaborato dal servizio Site Recovery. Quando si esegue il failover di test di una macchina virtuale, viene visualizzato anche i timestamp dell'ultimo punto di ripristino coerenti con l'applicazione hello. Se si esegue il failover di un piano di ripristino, è possibile passare una macchina virtuale tooindividual e osservare **punti di ripristino più recente** riquadro tooget queste informazioni.
    1.  **Latest multi-VM processed** (Più recente coerente tra più VM elaborato): questa opzione è disponibile solo per i piani di ripristino con almeno una macchina virtuale in cui è abilitata la coerenza tra più macchine virtuali. Macchine virtuali che fanno parte di un gruppo failover toohello più recente comuni tra più macchine coerente ripristino della replica del punto. Altre macchine virtuali failover tootheir ultimo elaborati punto di ripristino.  
    1.  **Latest multi-VM app-consistent** (Più recente coerente con l'applicazione tra più VM): questa opzione è disponibile solo per i piani di ripristino con almeno una macchina virtuale in cui è abilitata la coerenza tra più macchine virtuali. Macchine virtuali che fanno parte di una replica di tipo gruppo failover toohello ultimo comuni tra più macchine coerenti con l'applicazione punto di ripristino. Altre macchine virtuali failover tootheir più recente coerente con l'applicazione del punto di ripristino.
    1.  **Custom**: se si sta eseguendo il failover di test di una macchina virtuale, quindi è possibile utilizzare questo punto di recupero specifico tooa toofailover opzione.

    > [!NOTE]
    > opzione di Hello toochoose un punto di ripristino è disponibile solo quando viene eseguito il failover tooAzure.
    >
    >


1. Se alcune delle macchine virtuali hello nel piano di ripristino hello failover durante un'esecuzione precedente e l'ora hello le macchine virtuali sono attive nel percorso di origine e di destinazione, è possibile utilizzare **modificare la direzione** opzione direzione hello toodecide in che eseguono il failover hello dovrebbe essere eseguita.
1. Se esegue il failover tooAzure e la crittografia dei dati è abilitata per il cloud di hello (si applica solo quando si protegge le macchine virtuali Hyper-v da un Server VMM), in **chiave di crittografia** certificato selezionare hello emesso quando si abilitare la crittografia dei dati durante l'installazione nel server VMM hello.
1. Selezionare **spegnere la macchina prima di iniziare il failover** se si desidera che il ripristino del sito tooattempt toodo un arresto delle macchine virtuali di origine prima che venga attivato hello failover. Il failover continua anche se l'arresto ha esito negativo.  

    > [!NOTE]
    > In caso di macchine virtuali Hyper-v, questa opzione tenta anche toosynchronize hello locale i dati non sono ancora stati inviati toohello servizio prima che venga attivato hello failover.
    >
    >

1. È possibile controllare lo stato di avanzamento di hello failover nella hello **processi** pagina. Anche se si verificano errori durante un failover non pianificato, il piano di ripristino hello viene eseguito fino al completamento.
1. Dopo il failover hello, convalidare macchina virtuale hello accedendo tooit. Se si desidera toogo un altro punto di ripristino per la macchina virtuale hello, quindi è possibile utilizzare **Modifica punto di ripristino** opzione.
1. Dopo avere effettuato hello failover macchina virtuale, è possibile **Commit** hello failover. Ciò consente di eliminare tutti i punti di ripristino hello disponibili con il servizio hello e **Modifica punto di ripristino** opzione non sarà disponibile.

## <a name="planned-failover"></a>Failover pianificato
Oltre al failover, le macchine virtuali Hyper-V protette con Site Recovery supportano anche il **failover pianificato**. Si tratta di un'opzione di failover senza alcuna perdita di dati. Quando viene attivato un failover pianificato, innanzitutto hello macchine virtuali vengono arrestate, dati hello ancora toobe sincronizzato è sincronizzato e quindi viene attivato un failover di origine.

> [!NOTE]
> Quando si macchine virtuali di failover Hyper-v da un locale tooanother sito locale sito, toocome toohello indietro locale primario è toofirst **replica inversa** sito tooprimary indietro di virtual machine hello e quindi avviato un failover. Se macchina virtuale primaria hello non è disponibile, quindi prima di avviare troppo**replica inversa** macchina virtuale di hello toorestore da un backup.   
>
>

## <a name="failover-job"></a>Processo di failover

![Failover](./media/site-recovery-failover/FailoverJob.png)

L'attivazione di un failover comporta l'esecuzione dei passaggi riportati di seguito.

1. Verifica preliminare: questo passaggio garantisce che siano soddisfatte tutte le condizioni necessarie per il failover.
1. Failover: Questo passaggio elabora i dati di hello e rende pronti in modo che sia possibile creare esplicitamente una macchina virtuale di Azure. Se si è scelto **più recente** punto di ripristino, questo passaggio Crea un punto di ripristino dai dati di hello inviati toohello servizio.
1. Start: Questo passaggio viene creata una macchina virtuale di Azure utilizzando dati hello elaborati nel passaggio precedente hello.

> [!WARNING]
> **Non annullare un corso failover**: prima di avviare il failover, è la replica per la macchina virtuale hello è interrotta. Se si **Annulla** un processo lo stato di avanzamento, macchina virtuale hello, ma si arresta il failover non verrà avviato tooreplicate. Non è possibile riavviare nuovamente la replica.
>
>

## <a name="time-taken-for-failover-tooazure"></a>Tempo impiegato per il failover tooAzure

In alcuni casi, il failover delle macchine virtuali prevede un passaggio intermedio aggiuntiva che in genere richiede circa 8 too10 minuti toocomplete. Questi casi sono i seguenti:

* Macchine virtuali VMware che usano una versione del servizio di mobilità precedente alla 9.8
* Server fisici 
* Macchine virtuali VMware Linux
* Macchine virtuali Hyper-V protette come server fisici
* Macchine virtuali VMware in cui i driver seguenti non sono presenti come driver di avvio 
    * storvsc 
    * vmbus 
    * storflt 
    * intelide 
    * atapi
* Macchine virtuali VMware che non dispongono del servizio DHCP abilitato indipendentemente che usino indirizzi IP statici o DHCP.

In hello tutti gli altri casi questo passaggio intermedio non è necessario e tempo per il failover hello hello è notevolmente inferiore. 





## <a name="using-scripts-in-failover"></a>Uso di script per il failover
È possibile tooautomate determinate azioni durante un failover. È possibile utilizzare script o [i runbook di automazione di Azure](site-recovery-runbook-automation.md) in [i piani di ripristino](site-recovery-create-recovery-plans.md) toodo che.

## <a name="other-considerations"></a>Altre considerazioni
* **Lettera di unità** -lettera di unità tooretain hello in macchine virtuali dopo il failover è possibile impostare hello **criteri SAN** per hello virtual machine troppo**OnlineAll**. [Altre informazioni](https://support.microsoft.com/en-us/help/3031135/how-to-preserve-the-drive-letter-for-protected-virtual-machines-that-are-failed-over-or-migrated-to-azure).



## <a name="next-steps"></a>Passaggi successivi
Dopo aver eseguito il failover le macchine virtuali e data center di hello in locale è disponibile, è necessario [ **riproteggere** ](site-recovery-how-to-reprotect.md) macchine virtuali VMware di eseguire il data center di toohello in locale.

Utilizzare [ **failover pianificato** ](site-recovery-failback-from-azure-to-hyper-v.md) opzione troppo**Failback** il backup di macchine virtuali Hyper-v locale tooon da Azure.

Se hanno esito negativo su un dati di on-premise tooanother macchina virtuale Hyper-v gestito da un centro dati principale VMM server e hello center è disponibile, quindi utilizzare **la replica inversa** opzione toostart hello replica indietro toohello data center principale.
