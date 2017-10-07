---
title: applicazioni aaaReplicate (Azure tooAzure) | Documenti Microsoft
description: In questo articolo viene descritto come tooset la replica di virtuale dei computer in esecuzione in un'area di Azure troppo un'altra area in Azure.
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 5/22/2017
ms.author: asgang
ms.openlocfilehash: fb190dac14419f892a1c6b45a3d991d8005e4bd0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-virtual-machines-tooanother-azure-region"></a>Replicare macchine virtuali di Azure tooanother area di Azure



>[!NOTE]
>
> La replica di Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.

In questo articolo viene descritto come tooset la replica di virtuale dei computer in esecuzione in una regione di Azure tooanother area di Azure.

## <a name="prerequisites"></a>Prerequisiti

* Hello si presume che già si conoscono le Site Recovery e l'insieme di credenziali di servizi di ripristino. È necessario toohave una versione preliminare 'Insieme di credenziali Recovery services' creata.

    >[!NOTE]
    >
    > È consigliabile creare hello 'Insieme di credenziali Recovery services' nel percorso di hello in cui si desidera tooreplicate le macchine virtuali. Ad esempio, se la posizione di destinazione è "Stati Uniti centrali", creare l'insieme di credenziali in "Stati Uniti centrali".

* Se si utilizzano le regole di sicurezza gruppi (rete) o la connettività internet di firewall proxy toocontrol accesso toooutbound hello macchine virtuali di Azure, verificare che hello di whitelist è richiesta la URL o gli indirizzi IP. Fare riferimento troppo[rete fornite nel documento](./site-recovery-azure-to-azure-networking-guidance.md) per altri dettagli.

* Se si dispone di ExpressRoute o una connessione VPN tra sedi locali e hello in Azure percorso di origine, seguire [considerazioni sul ripristino del sito per locale tooon Azure ExpressRoute o configurazione VPN](site-recovery-azure-to-azure-networking-guidance.md#guidelines-for-existing-azure-to-on-premises-expressroutevpn-configuration) documento.

* L'account utente di Azure deve toohave determinati [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica della macchina virtuale di Azure.

* La sottoscrizione di Azure deve essere abilitato toocreate VM nel percorso di destinazione hello desiderato toouse come area di ripristino di emergenza. Contattare il supporto tooenable hello obbligatorio quota.

## <a name="enable-replication-from-azure-site-recovery-vault"></a>Abilitare la replica dall'insieme di credenziali di Azure Site Recovery
Per questa illustrazione, si eseguirà la replica di macchine virtuali in esecuzione in toohello di località di Azure "Asia orientale" hello ' sud-est asiatico ' percorso. come indicato di seguito sono riportati i passaggi di Hello:

 Fare clic su **+ replicare** nella replica di tooenable hello insieme di credenziali per le macchine virtuali hello.

1. **Origine:** fa toohello punto di origine delle macchine di hello, che in questo caso è **Azure**.

2. **Percorso di origine:** è hello area in cui si desidera tooprotect le macchine virtuali di Azure. Per questa figura, il percorso di origine hello sarà "Asia orientale"

3. **Modello di distribuzione:** fa riferimento al modello di distribuzione di Azure toohello dei computer di origine hello. È possibile selezionare entrambi classica o Gestione risorse di computer appartenenti a modello specifico toohello viene elencato per la protezione nel passaggio successivo hello.

      >[!NOTE]
      >
      > È possibile eseguire la replica di una macchina virtuale classica e ripristinarla solo come macchina virtuale classica. Non è possibile ripristinarla come macchina virtuale di Resource Manager.

4. **Gruppo di risorse:** del toowhich gruppo di risorse hello appartengono le macchine virtuali di origine. Verrà elencati per la protezione nel passaggio successivo hello hello tutte le macchine virtuali nel gruppo di risorse selezionato hello.

    ![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/enabledrwizard1.png)

In **macchine virtuali > macchine virtuali selezionare**, fare clic su e selezionare ciascuna macchina da tooreplicate. È possibile selezionare solo i computer per cui è possibile abilitare la replica. Fare quindi clic su OK.
    ![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/virtualmachine_selection.png)


Nella sezione Impostazioni è possibile configurare le proprietà del sito di destinazione.

1. **Percorso di destinazione:** hello posizione in cui verranno replicati i dati di macchina virtuale di origine. In base al percorso di macchine virtuali selezionate, il ripristino del sito verrà fornito che Hello elenco delle aree di destinazione appropriato.

    > [!TIP]
    > È consigliabile il percorso di destinazione tookeep stesso al momento del ripristino dell'insieme di credenziali dei servizi.

2. **Il gruppo di risorse di destinazione:** è hello toowhich di gruppo di risorse al quale apparterrà tutte le macchine virtuali replicate. Per impostazione predefinita ASR creerà un nuovo gruppo di risorse nell'area di destinazione hello con nome con il suffisso "asr". Nel caso in cui il gruppo di risorse creato da ASR già esiste, verrà riutilizzata. È anche possibile scegliere toocustomize, come illustrato nella sezione hello riportata di seguito.    
3. **Rete virtuale di destinazione:** per impostazione predefinita, ripristino automatico di sistema creerà una nuova rete virtuale nell'area di destinazione hello con nome con il suffisso "asr". Questa sarà la rete di origine mappata tooyour e verrà utilizzata per alcuna protezione future.

    > [!NOTE]
    > [Controllare i dettagli rete](site-recovery-network-mapping-azure-to-azure.md) tooknow ulteriori informazioni sul mapping di rete.

4. **Gli account di archiviazione di destinazione:** per impostazione predefinita, creerà hello nuova destinazione account di archiviazione che rispecchia la configurazione di archiviazione macchina virtuale di origine ripristino automatico di sistema. Nel caso in cui l'account di archiviazione creato da Azure Site Recovery esista già, verrà riutilizzato.

5. **Memorizzare nella cache gli account di archiviazione:** ASR richiede account di archiviazione aggiuntiva denominata archiviazione cache nell'area di origine hello. Tutti hello modifiche che si verifichi hello macchine virtuali di origine vengono monitorate e inviate toocache account di archiviazione prima di replicare questi percorso di destinazione toohello.

6. **Set di disponibilità:** per impostazione predefinita, creerà un nuovo set di disponibilità nell'area di destinazione hello con nome con il suffisso "asr" Ripristino automatico di sistema. Nel caso in cui il set di disponibilità creato da Azure Site Recovery esista già, verrà riutilizzato.

7.  **Criteri di replica:** definisce le impostazioni per ripristino punto di memorizzazione della cronologia e app snapshot coerente con la frequenza di hello. Per impostazione predefinita, Azure Site Recovery creerà un nuovo criterio di replica con impostazioni predefiniti di "24 ore" per la conservazione del punto di ripristino e di "60 minuti" per la frequenza snapshot coerenti con l'app.

    ![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/enabledrwizard3.PNG)

## <a name="customize-target-resources"></a>Personalizzare le risorse di destinazione

Nel caso in cui si desidera impostazioni predefinite di hello toochange utilizzate da Ripristino automatico di sistema, è possibile modificare le impostazioni di hello in base alle proprie esigenze.

1. **Personalizzare:** selezionarlo toochange hello predefinite utilizzate da Ripristino automatico di sistema.

2. **Il gruppo di risorse di destinazione:** è possibile selezionare il gruppo di risorse hello elenco hello di tutti i gruppi di risorse hello esistente nella posizione di destinazione hello sottoscrizione hello.

3. **Rete virtuale di destinazione:** è possibile trovare l'elenco di hello della rete virtuale di hello tutte nel percorso di destinazione hello.

4. **Set di disponibilità:** è possibile aggiungere solo disponibilità set di impostazioni toohello macchine virtuali che fanno parte di disponibilità nell'area di origine.

5. **Target Storage accounts (Account di archiviazione di destinazione):**

![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/customize.PNG) Fare clic su **Create target resources** (Crea risorse di destinazione) e quindi su Abilita replica.


Una volta macchine virtuali sono protetti, è possibile controllare lo stato di hello di integrità di macchine virtuali in **gli elementi replicati**

>[!NOTE]
>Durante hello momento della replica iniziale esiste Impossibile la possibilità che lo stato accetta ora toorefresh e non viene visualizzato lo stato di avanzamento per un certo tempo. È possibile scegliere il pulsante Aggiorna hello in primo piano hello di stato più recente di hello pannello tooget hello.
>

![Abilitare la replica](./media/site-recovery-replicate-azure-to-azure/replicateditems.PNG)


## <a name="next-steps"></a>Passaggi successivi
- [Altre informazioni](site-recovery-test-failover-to-azure.md) sull'esecuzione di un failover di test.
- [Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e come toorun li.
- Altre informazioni, vedere [utilizzando i piani di ripristino](site-recovery-create-recovery-plans.md) tooreduce RTO.
- Altre informazioni sulla [riprotezione delle VM di Azure](site-recovery-how-to-reprotect.md) dopo il failover.
