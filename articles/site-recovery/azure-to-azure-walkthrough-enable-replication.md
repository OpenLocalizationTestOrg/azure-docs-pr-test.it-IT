---
title: la replica aaaEnable per macchine virtuali di Azure tooanother area di Azure con Azure Site Recovery | Documenti Microsoft
description: "Vengono riepilogati i passaggi di hello tooenable replica tooanother area di Azure è necessario per le macchine virtuali di Azure, tramite il servizio di Azure Site Recovery hello"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a>Passaggio 5: Abilitare la replica per le macchine virtuali di Azure


Dopo aver impostato un [insieme di credenziali di servizi di ripristino](azure-to-azure-walkthrough-vault.md), utilizzare la replica tooenable articolo macchine virtuali (VM), tooanother area di Azure con [Azure Site Recovery](site-recovery-overview.md). replica tooenable, è possibile impostare le impostazioni di origine e di destinazione, verificare i criteri di replica hello e selezionare le macchine virtuali desiderate tooreplicate.

- Una volta terminato l'articolo hello, le macchine virtuali di Azure deve essere la replica toohello area secondaria di Azure.
- Inviare eventuali commenti nella parte inferiore di hello di questo articolo, o porre domande in hello [forum sui servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)

>[!NOTE]
>
> La replica di macchine virtuali di Azure è attualmente in anteprima.


## <a name="select-hello-source"></a>Selezionare l'origine hello 

1. In insiemi di credenziali di servizi di ripristino, fare clic sul nome dell'insieme di credenziali di hello > **+ replicare**.
2. In **Origine** selezionare **Azure - ANTEPRIMA**.
2. In **percorso di origine**selezionare origine hello regione di Azure in cui le macchine virtuali attualmente in esecuzione.
3. Seleziona hello **il modello di distribuzione di macchina virtuale di Azure** per le macchine virtuali: **Gestione risorse** o **classico**.
4. Seleziona hello **il gruppo di risorse di origine** per Gestione risorse di macchine virtuali o **servizio cloud** per le macchine virtuali classiche.
5. Fare clic su **OK** impostazioni hello toosave.

    ![Configurare l'origine hello](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a>Selezionare le macchine virtuali hello

Il ripristino del sito recupera un elenco di macchine virtuali associate alla sottoscrizione hello e risorse gruppo/servizio cloud hello.

1. In **macchine virtuali**, selezionare le macchine virtuali hello desiderato tooreplicate.
2. Fare clic su **OK**.

    ![Selezionare le VM](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a>Configurare le impostazioni

Le impostazioni predefinite per l'area di destinazione hello (in base alle impostazioni area di origine hello), esegue il provisioning di Site Recovery e il criterio di replica hello:

   - **Percorso di destinazione**: area di destinazione hello desiderate toouse per il ripristino di emergenza. È consigliabile che il percorso di destinazione hello corrisponda percorso hello dell'insieme di credenziali di Site Recovery hello.
   - **Il gruppo di risorse di destinazione**: gruppo di risorse toowhich macchine virtuali di Azure nell'area di destinazione hello apparterrà dopo il failover. Per impostazione predefinita, il ripristino del sito viene creato un nuovo gruppo di risorse nell'area di destinazione hello con un suffisso "asr". 
   - **Rete virtuale di destinazione**: rete hello in cui le macchine virtuali di Azure in hello area di destinazione sarà posizionato dopo il failover. Per impostazione predefinita, il ripristino del sito crea una nuova rete virtuale (e le subnet) nell'area di destinazione hello con un suffisso "asr". Questa rete è mappata tooyour rete di origine. Si noti che è possibile assegnare un indirizzo IP specifico dopo il failover di una macchina virtuale, se è necessario tooretain hello stesso indirizzo IP in posizioni di origine e destinazione hello. 
   - **Memorizzare nella cache gli account di archiviazione**: il ripristino del sito Usa un account di archiviazione nell'area di origine hello. Le modifiche apportate nelle macchine virtuali di origine vengono inviate toothis account, prima di percorso di destinazione di replica toohello. 
   - **Gli account di archiviazione di destinazione**: per impostazione predefinita, il ripristino del sito viene creato un nuovo account di archiviazione nell'area di destinazione hello, origine hello toomirror account di archiviazione macchina virtuale.
   -  **Set di disponibilità di destinazione**: per impostazione predefinita, il ripristino del sito viene creato un nuovo set di disponibilità in area di destinazione hello, con il suffisso "asr" hello. 
   - **Nome del criterio di replica**: nome del criterio.
   - **Conservazione del punto di ripristino**: per impostazione predefinita, Site Recovery conserva i punti di ripristino per 24 ore. È possibile configurare un valore compreso tra 1 e 72 ore.
   - **Frequenza snapshot coerenti con l'app**: per impostazione predefinita, Site Recovery accetta uno snapshot coerente con l'app ogni 4 ore. È possibile configurare un valore compreso tra 1 e 12 ore. I dati vengono replicati in modo continuo:
    - I punti di ripristino coerenti con l'arresto anomalo conservano un ordine di scrittura dati coerente, se creati. Questo tipo di punto di ripristino è in genere sufficiente se l'applicazione viene progettata toorecover dopo un arresto anomalo senza incoerenze dei dati
    - I punti di ripristino coerenti con l'arresto anomalo vengono generati ogni pochi minuti. Tramite questi toofail punti di ripristino su e ripristinare le macchine virtuali fornisce un obiettivo del punto di ripristino (RPO) in ordine di hello di minuti.
    - Punti di ripristino coerenti con l'App (in coerenza toowrite ordine di aggiunta) verificare che le applicazioni in esecuzione completare tutte le operazioni e scaricare i buffer toodisk (disattivazione dell'applicazione). È consigliabile usare questi punti di ripristino per le app di database come Exchange, Oracle e SQL Server.
        
    ![Configurare le impostazioni](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a>Modificare le impostazioni

Se si desiderano impostazioni di criteri di replica e di destinazione toomodify, hello seguenti:

1. tooview o modificare le impostazioni di destinazione, fare clic su **impostazioni**.
2. Fare clic su impostazioni di destinazione predefinito hello toooverride, **Personalizza**. È possibile specificare un gruppo di risorse di destinazione, una rete virtuale, un set di disponibilità e account di archiviazione di destinazione. Se le macchine virtuali fanno parte di un set nell'area di origine hello, è possibile aggiungere solo i set di disponibilità.

    ![Configurare le impostazioni](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. Fare clic su impostazioni di replica toooverride per i punti di ripristino e gli snapshot coerenti con l'app, **Personalizza** Avanti troppo**criteri di replica**.
 
    ![Configurare le impostazioni](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. Fare clic su risorse di destinazione hello provisioning toostart, **creare risorse di destinazione**. Il provisioning richiede circa un minuto. Non chiudere il pannello hello durante il provisioning o avrai toostart su.




## <a name="enable-replication"></a>Abilitare la replica

1. In **Impostazioni** fare clic su **Abilita replica**. In questo modo la replica iniziale di hello macchine virtuali è stata selezionata. Lo stato della replica iniziale potrebbe richiedere alcuni toorefresh ora. Fare clic su **aggiornamento** tooget stato più recente di hello.

2. È possibile monitorare lo stato di avanzamento di hello **abilitare la protezione** processo **impostazioni** > **processi** > **processi di ripristino del sito**.

3. In **impostazioni** > **elementi replicati**, è possibile visualizzare lo stato di hello di macchine virtuali e hello stato della replica iniziale. Fare clic su hello VM toodrill verso il basso nelle relative impostazioni.



## <a name="next-steps"></a>Passaggi successivi

Andare troppo[passaggio 6: eseguire un failover di test](azure-to-azure-walkthrough-test-failover.md)
