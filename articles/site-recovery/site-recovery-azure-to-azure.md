---
title: 'Replicare macchine virtuali di Azure tra le aree di Azure per il ripristino di emergenza deve: tooAzure Azure | Documenti Microsoft'
description: "Vengono riepilogati i passaggi di hello è necessario tooreplicate macchine virtuali di Azure tra le aree di Azure (Azure in Azure) con il servizio di Azure Site Recovery hello per esigenze di ripristino di emergenza."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a>Eseguire la replica delle VM di Azure tra le aree con Azure Site Recovery

>[!NOTE]
>
> La replica di Azure Site Recovery per le macchine virtuali di Azure è attualmente in anteprima.

In questo articolo viene descritto come tooreplicate macchine virtuali di Azure tra le aree di Azure tramite hello [Site Recovery](site-recovery-overview.md) di hello portale di Azure.

Inviare commenti e domande nella parte inferiore di hello di questo articolo o di hello [forum di servizi di ripristino di Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).

## <a name="disaster-recovery-in-azure"></a>Ripristino di emergenza in Azure

Caratteristiche e funzionalità predefinite dell'infrastruttura di Azure contribuiscono tooa strategia di disponibilità solida e flessibile per carichi di lavoro eseguiti su macchine virtuali di Azure. Tuttavia, esistono molti motivi per cui è necessario tooplan per il ripristino di emergenza tra aree di Azure manualmente:

- È necessario toomeet linee guida di conformità per App specifiche e i carichi di lavoro che richiedono un continuità aziendale e una strategia di ripristino di emergenza.
- Si desidera tooprotect possibilità hello e il ripristino macchine virtuali di Azure in base a quanto deciso business e non solo in base alle funzionalità di Azure incorporata.
- È necessario tootest failover e il ripristino in base alle esigenze aziendali e di conformità, senza alcun impatto sulla produzione.
- È necessario toofail rispetto all'area di ripristino toohello nell'evento hello un'emergenza ed esito negativo toohello indietro area di origine originale senza problemi.

Utilizzare il ripristino del sito per la macchina virtuale di Azure in Azure replica toohelp tutte queste operazioni.


## <a name="why-use-site-recovery"></a>Perché usare Site Recovery?      

Il ripristino del sito fornisce un modo semplice di tooreplicate macchine virtuali di Azure tra aree:

- **Distribuzione automatica**. A differenza di un modello di replica attivo-attivo, non è necessario per un'infrastruttura dispendiosa e complessa nell'area secondaria hello. Quando si abilita la replica, il ripristino del sito vengono automaticamente create hello necessarie risorse nell'area di destinazione hello, in base alle impostazioni di area di origine.
- **Aree di controllo**. Con il ripristino del sito, è possibile replicare da un'area di tooany area all'interno di un continente. È possibile confrontare questo approccio con l'archiviazione con ridondanza geografica e accesso in lettura, che esegue la replica asincrona solo tra [aree abbinate](https://docs.microsoft.com/azure/best-practices-availability-paired-regions). Archiviazione con ridondanza geografica e accesso in lettura fornisce accesso in sola lettura toohello dati area di destinazione hello.
- **Replica automatica**. Site Recovery fornisce la replica continua automatica. È possibile attivare il failover e il failback con un singolo clic.
- **RTO e RPO**. Il ripristino del sito si avvale dell'infrastruttura di rete di Azure hello che si connette aree tookeep obiettivi RTO e RPO molto bassa.
- **Test**. È possibile eseguire esercitazioni per il ripristino di emergenza con failover di test su richiesta, quando necessario, senza influire sui carichi di lavoro di produzione o sulla replica continua.
- **Piani di ripristino** È possibile utilizzare i failover tooorchestrate piani di ripristino e il failback di hello tutta l'applicazione in esecuzione su più macchine virtuali. funzionalità del piano di ripristino Hello dispone di integrazione di prima classe completa con i runbook di automazione di Azure.


## <a name="deployment-summary"></a>Riepilogo della distribuzione

Di seguito è riportato un riepilogo di ciò che è necessario tooset toodo la replica delle macchine virtuali tra aree di Azure:

1. Creare un insieme di credenziali dei servizi di ripristino. insieme di credenziali Hello contiene le impostazioni di configurazione e Orchestra la replica.
2. Abilitare la replica per hello macchine virtuali di Azure.
3. Eseguire un toomake di failover di test assicurarsi che tutto funzioni come previsto.

>[!IMPORTANT]
>
> È possibile controllare hello [matrice del supporto per la replica di macchina virtuale di Azure](./site-recovery-support-matrix-azure-to-azure.md).

>[!IMPORTANT]
>
> Per informazioni su come tooconfigure hello necessaria la connettività di rete in uscita per le macchine virtuali di Azure per la replica di Site Recovery, vedere hello [rete fornite nel documento](./site-recovery-azure-to-azure-networking-guidance.md).

### <a name="before-you-start"></a>Prima di iniziare

* L'account utente di Azure deve toohave determinati [autorizzazioni](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replica della macchina virtuale di Azure.
* La sottoscrizione di Azure deve essere abilitato toocreate macchine virtuali nel percorso di destinazione hello che si desidera toouse come area di ripristino di emergenza hello. Contattare il supporto tecnico tooenable hello quota obbligatorio.

## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> Si consiglia di creare credenziali di servizi di ripristino hello in hello percorso in cui tooreplicate le macchine virtuali. Ad esempio, se il percorso di destinazione è hello central US, creare un archivio di hello in **centrale Usa**.

## <a name="enable-replication"></a>Abilitare la replica

In **insiemi di credenziali di servizi di ripristino**, fare clic sul nome dell'insieme di credenziali hello. Nell'insieme di credenziali hello, fare clic su hello **+ replicare** pulsante.

### <a name="step-1-configure-hello-source"></a>Passaggio 1. Configurare l'origine hello
1. In **Origine** selezionare **Azure - ANTEPRIMA**.
2. In **percorso di origine**selezionare origine hello regione di Azure in cui le macchine virtuali attualmente in esecuzione.
3. Modello di distribuzione selezionare hello delle macchine virtuali: **Gestione risorse** o **classico**.
4. Seleziona hello **il gruppo di risorse di origine** per le macchine virtuali di gestione risorse o **servizio cloud** per le macchine virtuali classiche.

    ![Configurare l'origine hello](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a>Passaggio 2. Selezionare le macchine virtuali

* Selezionare le macchine virtuali hello desidera tooreplicate e quindi fare clic su **OK**.

    ![Selezionare le VM](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a>Passaggio 3. Configurare le impostazioni

1. valore predefinito di hello toooverride le impostazioni di destinazione e specificare le impostazioni di hello di propria scelta, fare clic su **Personalizza**. Per altre informazioni, vedere [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources) (Personalizzare le risorse di destinazione).

    ![Configurare le impostazioni](./media/site-recovery-azure-to-azure/settings.png)


2. Per impostazione predefinita, Site Recovery crea un criterio di replica che crea snapshot coerenti con l'app ogni 4 ore e conserva i punti di ripristino per 24 ore. toocreate criteri con impostazioni diverse, fare clic su **Personalizza** Avanti troppo**criteri di replica**.

    ![Personalizzare i criteri](./media/site-recovery-azure-to-azure/customize-policy.png)

3. Fare clic su risorse di destinazione hello provisioning toostart, **creare risorse di destinazione**. Il provisioning richiede circa un minuto. Non chiudere il pannello hello durante il provisioning o è necessario toostart su.

4. replica tootrigger di hello selezionata VM, fare clic su **abilitare la replica**.

5. È possibile monitorare lo stato di avanzamento di hello **abilitare la protezione** processo **impostazioni** > **processi** > **processi di ripristino del sito**.

6. In **impostazioni** > **elementi replicati**, è possibile visualizzare lo stato di hello di macchine virtuali e hello stato della replica iniziale. Fare clic su hello VM toodrill verso il basso nelle relative impostazioni.

## <a name="run-a-test-failover"></a>Eseguire un failover di test

Dopo aver configurato tutti gli elementi, eseguire una toomake di failover di test che tutto funzioni come previsto:

1. toofail su un singolo computer, in **impostazioni** > **elementi replicati**, fare clic su hello VM **+ Test Failover** icona.

2. toofail sul ripristino di un piano, in **impostazioni** > **piani di ripristino**, piano hello rapida **Failover di Test**. un piano di ripristino, toocreate [seguire queste istruzioni](site-recovery-create-recovery-plans.md). 

3. In **Failover di Test**selezionare toowhich di rete virtuale di Azure di destinazione hello macchine virtuali di Azure sono connesse dopo il failover hello.

4. toostart hello failover, fare clic su **OK**. tootrack sullo stato di avanzamento, fare clic su hello VM tooopen le relative proprietà. Oppure è possibile fare clic su hello **Failover di Test** processo nel nome dell'insieme di credenziali hello > **impostazioni** > **processi** > **iprocessidiripristinodelsito**.

5. Hello failover termine, replica hello macchina di Azure viene visualizzato nel portale di Azure hello > **macchine virtuali**. Assicurarsi che tale hello VM sia di dimensioni appropriate hello, che si è connesso toohello di rete appropriata e che sia in esecuzione.

6. Fare clic su toodelete hello macchine virtuali che sono stati creati durante il failover di test hello, **il failover di test di pulizia** su hello replicati hello o elemento piano di ripristino. In **note**, registrare e salvare eventuali commenti associati hello test failover. 

[Altre informazioni](site-recovery-test-failover-to-azure.md) sui failover di test.


## <a name="next-steps"></a>Passaggi successivi

Dopo aver test distribuzione hello:

- [Altre informazioni](site-recovery-failover.md) sui diversi tipi di failover e modalità toorun li.
- Altre informazioni, vedere [utilizzando i piani di ripristino](site-recovery-create-recovery-plans.md) tooreduce RTO.
