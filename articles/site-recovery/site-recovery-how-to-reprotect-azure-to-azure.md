---
title: tooReprotect aaaHow dal failover tooprimary indietro di macchine virtuali di Azure regione di Azure | Documenti Microsoft
description: "Dopo il failover delle macchine virtuali da un tooanother area di Azure, è possibile utilizzare le macchine di Azure Site Recovery tooprotect hello in direzione inversa. Informazioni sui passaggi di hello come toodo un riprotezione prima del failover nuovamente."
services: site-recovery
documentationcenter: 
author: ruturaj
manager: gauravd
editor: 
ms.assetid: 44813a48-c680-4581-a92e-cecc57cc3b1e
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 08/11/2017
ms.author: ruturajd
ms.openlocfilehash: 991c7ee8f489e84c250230bf73f3e99015c5f051
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="reprotect-from-failed-over-azure-region-back-tooprimary-region"></a>Riprotezione dal failover Azure tooprimary indietro paese.



>[!NOTE]
>
> La replica di Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.


## <a name="overview"></a>Panoramica
Quando si [failover](site-recovery-failover.md) hello le macchine virtuali da un'area di Azure tooanother, hello le macchine virtuali sono in uno stato non protetto. Se si desidera toobring li area primaria toohello, è necessario toofirst proteggere di nuovo le macchine virtuali hello e quindi il failover. Non vi è differenza tra l'esecuzione del failover in una direzione o nell'altra. Analogamente, dopo l'abilitazione della protezione delle macchine virtuali hello, non vi è alcuna differenza tra hello riprotezione post failover o il failback post.
tooexplain hello i flussi di lavoro di riprotezione e tooavoid confusione, si utilizzerà hello sito primario dei computer protetti hello come area Asia orientale e sito di ripristino hello macchine hello come area Asia sudorientale. Durante il failover, sarà possibile area Asia sudorientale toohello di failover hello macchine virtuali. Prima di eseguire il failback, è necessario tooreprotect hello le macchine virtuali da tooEast indietro sud-est asiatico Asia. In questo articolo vengono descritti i passaggi di hello sul tooreprotect.

> [!WARNING]
> Se dispone di [completato la migrazione](site-recovery-migrate-to-azure.md#what-do-we-mean-by-migration)risorsa tooanother della macchina virtuale spostata hello gruppo o eliminato hello macchina virtuale di Azure, non è possibile eseguire il failback in seguito.

Dopo la riprotezione termina e la replica di macchine virtuali hello protetto, è possibile avviare un failover su hello macchine virtuali toobring area Asia tooEast nuovamente.

Registrare commenti o domande alla fine di hello di questo articolo o di hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="prerequisites"></a>Prerequisiti
1. macchine virtuali Hello dovrebbe essere stato eseguito il commit.
2. sito di destinazione Hello - in questo caso area Asia orientale Azure hello devono essere disponibile e devono essere in grado di creare tooaccess/nuove risorse in tale area.

## <a name="steps-tooreprotect"></a>Passaggi tooreprotect

Seguenti sono hello tooreprotect passaggi di una macchina virtuale utilizzando le impostazioni predefinite di hello.

1. In **insieme di credenziali** > **gli elementi replicati**, hello macchina virtuale in cui è stato eseguito il failover e quindi scegliere **riproteggere**. È anche possibile fare clic su hello computer e seleziona **riproteggere** dai pulsanti di comando hello.

![Fare clic con il pulsante destro tooreprotect](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotect.png)

2. Notare che direzione hello di protezione, nel pannello hello **Asia sudorientale tooEast asia**, è già selezionato.

![Riproteggere il pannello](./media/site-recovery-how-to-reprotect-azure-to-azure/reprotectblade.png)

3. Hello revisione **set archiviazione e la disponibilità del gruppo, rete, risorse** informazioni e fare clic su OK. Se sono presenti tutte le risorse contrassegnate (nuovo), verrà creati come parte di hello riproteggere.

Questo trigger un processo riproteggere processo eseguirà innanzitutto il seeding del sito di destinazione di hello (SEA in questo caso) con dati più recenti hello e una volta che viene completato, verranno replicate delta hello prima del failover è nuovamente tooSoutheast Asia.

### <a name="reprotect-customization"></a>Personalizzazione della riprotezione
Se si desidera toochoose hello estratto conto o hello rete di archiviazione durante ricrea la protezione, è possibile effettuare questa operazione utilizzando hello personalizzare opzione disponibile nel Pannello di riprotezione hello.

![Opzione di personalizzazione](./media/site-recovery-how-to-reprotect-azure-to-azure/customize.png)

È possibile personalizzare le proprietà della macchina virtuale di destinazione he seguenti durante la riprotezione hello.

![Personalizzare il pannello](./media/site-recovery-how-to-reprotect-azure-to-azure/customizeblade.png)

|Proprietà |Note  |
|---------|---------|
|Gruppo di risorse di destinazione     | È possibile scegliere toochange gruppo di risorse destinazione hello in cui verrà creato macchina virtuale th. Come parte di hello di riprotezione, verranno eliminata hello macchina virtuale di destinazione, pertanto è possibile scegliere un nuovo gruppo di risorse in cui è possibile creare hello failover post della macchina virtuale         |
|Rete virtuale di destinazione     | Rete non può essere modificata durante riprotezione hello. hello toochange di rete, ripetere il mapping di rete hello.         |
|Archiviazione di destinazione     | È possibile modificare l'account di archiviazione hello macchina virtuale di hello toowhich sarà failover post creato.         |
|Archiviazione cache     | È possibile specificare un account di archiviazione cache che verrà usato durante la replica. Se si passa con valori predefiniti di hello, un nuovo account di archiviazione della cache verrà creato, se non esiste già.         |
|Set di disponibilità     |Se hello di macchina virtuale in Asia orientale fa parte di un set di disponibilità, è possibile scegliere un set di disponibilità per la macchina virtuale di destinazione hello in Asia sudorientale. Valori predefiniti verranno trovare set di disponibilità SEA esistente hello e provare a toouse è. Durante la personalizzazione, è possibile specificare un set di disponibilità completamente nuovo.         |


### <a name="what-happens-during-reprotect"></a>Cosa accade durante la riprotezione?

Solo come dopo hello innanzitutto abilitare la protezione, di seguito sono artefatti hello che verranno creati se si utilizzano impostazioni predefinite di hello.
1. Nell'area Asia orientale hello, viene creato un account di archiviazione della cache.
2. Se l'account di archiviazione di destinazione hello (hello account di archiviazione originale della macchina virtuale in Asia sudorientale hello) non esiste, viene creato uno nuovo. nome Hello è l'account di archiviazione della macchina virtuale in Asia orientale di hello aggiunto il suffisso "asr".
3. Se il set di destinazioni AV hello non esiste, e le impostazioni predefinite hello rilevati talmente toocreate impostato un nuovo AV, quindi verrà creato come parte di hello riproteggere processo. Se è stata personalizzata hello ricrea la protezione, quindi impostare AV hello selezionata verrà utilizzata.
4.

di seguito Hello sono elenco hello dei passaggi che si verificano quando si attiva un processo di riprotezione. Si tratta di macchina virtuale esista sul lato di destinazione di hello hello case.

1. Hello necessario artefatti vengono creati come parte di riprotezione. Se esistono già, vengono riusati.
2. macchina virtuale di Hello destinazione lato (sud-est asiatico) prima di tutto è stata disattivata, se è in esecuzione.
3. disco Hello destinazione lato macchina virtuale viene copiato da Azure Site Recovery in un contenitore come blob di valore di inizializzazione.
4. macchina virtuale sul lato di destinazione Hello viene quindi eliminato.
5. blob di valore di inizializzazione Hello viene utilizzato da tooreplicate corrente della macchina virtuale lato (Asia orientale) di origine in hello. In questo modo vengono replicati solo i valori delta.
6. le modifiche principali di Hello tra il disco di origine hello e blob di valore di inizializzazione hello sono sincronizzate. Questa operazione può richiedere alcuni toocomplete ora.
7. Una volta hello riproteggere processo viene completato, replica differenziale hello inizia che crea un punto di ripristino in base ai criteri di hello.

> [!NOTE]
> Non è possibile eseguire la riprotezione a un livello di piano di ripristino. È solo possibile eseguire la riprotezione solo a un livello di macchina virtuale.

Dopo hello riproteggere esito positivo, verrà attivata la macchina virtuale hello uno stato protetto.

## <a name="next-steps"></a>Passaggi successivi

Dopo la macchina virtuale hello ha immesso uno stato protetto, è possibile avviare un failover. failover Hello spegnere la macchina virtuale hello nell'area Asia orientale Azure e quindi crea e avvia macchina virtuale di area Asia sudorientale hello. È pertanto un breve tempo di inattività per un'applicazione hello. In tal caso, scegliere il tempo di hello per il failover quando l'applicazione può tollerare un tempo di inattività. È consigliabile testare il failover hello macchina virtuale toomake che arrivano correttamente, prima di avviare un failover.

-   [Passaggi tooinitiate test failover della macchina virtuale hello](site-recovery-test-failover-to-azure.md)

-   [Passaggi tooinitiate failover della macchina virtuale hello](site-recovery-failover.md)
