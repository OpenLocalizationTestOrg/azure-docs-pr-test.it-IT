---
title: 'Primo approccio: Proteggere le VM di Azure con un insieme di credenziali dei servizi di ripristino | Microsoft Docs'
description: Proteggere le VM di Azure con un insieme di credenziali dei servizi di ripristino. Utilizzare i backup di macchine virtuali distribuite di gestione risorse, macchine virtuali distribuite classica e Premium archiviazione macchine virtuali, le macchine virtuali crittografati, le macchine virtuali su dischi gestiti tooprotect i dati. Creare e registrare un insieme di credenziali dei servizi di ripristino. Registrare macchine virtuali, creare criteri e proteggere macchine virtuali in Azure.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keyword: backups; vm backup
ms.assetid: 45e773d6-c91f-4501-8876-ae57db517cd1
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 08/15/2017
ms.author: markgal;jimpark
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 70e4700abb76e16e32e1ead06ce1dbe277e1f0e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-toorecovery-services-vaults"></a>Eseguire il backup degli archivi di servizi tooRecovery macchine virtuali di Azure
> [!div class="op_single_selector"]
> * [Proteggere le VM con un insieme di credenziali dei servizi di ripristino](backup-azure-vms-first-look-arm.md)
> * [Proteggere le VM con un insieme di credenziali per il backup](backup-azure-vms-first-look.md)
>
>

In questa esercitazione illustra i passaggi di hello per la creazione di un insieme di credenziali di servizi di ripristino e backup di una macchina virtuale di Azure (VM). Gli insiemi di credenziali dei servizi di ripristino proteggono:

* VM distribuite in Azure Resource Manager
* Macchine virtuali classiche
* Macchine virtuali di Archiviazione Standard
* Macchine virtuali di Archiviazione Premium
* Macchine virtuali in esecuzione su Managed Disks
* VM crittografate usando Crittografia dischi di Azure, con BEK e KEK
* Backup coerente con le applicazioni di macchine virtuali Windows tramite VSS e di macchine virtuali Linux tramite script pre-snapshot e post-snapshot personalizzati

Per ulteriori informazioni sulla protezione di archiviazione Premium macchine virtuali, vedere l'articolo hello [backup e ripristino di macchine virtuali di archiviazione Premium](backup-introduction-to-azure-backup.md#using-premium-storage-vms-with-azure-backup). Per altre informazioni sul supporto per macchine virtuali con Managed Disks, vedere [Backup e ripristino di macchine virtuali in Managed Disks](backup-introduction-to-azure-backup.md#using-managed-disk-vms-with-azure-backup). Per altre informazioni sul framework di script pre-snapshot e post-snapshot per il backup di macchine virtuali Linux, vedere [Backup coerente con le applicazioni di VM Linux di Azure] (https://docs.microsoft.com/azure/backup/backup-azure-linux-app-consistent).

Fare riferimento toofind più cosa può di backup e non è possibile, [qui](backup-azure-vms-prepare.md#limitations-when-backing-up-and-restoring-a-vm)

> [!NOTE]
> In questa esercitazione si presuppone che si dispone già di una macchina virtuale nella sottoscrizione di Azure e di aver eseguito le misure tooallow hello servizio di backup tooaccess hello macchina virtuale.
>
>

[!INCLUDE [learn-about-Azure-Backup-deployment-models](../../includes/backup-deployment-models.md)]

In base al numero di hello di macchine virtuali desiderate tooprotect, è possibile iniziare da diversi punti di partenza. Se si desidera tooback backup di più macchine virtuali in un'unica operazione, Vai a insieme di credenziali di servizi di ripristino toohello e [processo di backup hello iniziare dal dashboard dell'insieme di credenziali hello](backup-azure-vms-first-look-arm.md#configure-the-backup-job-from-the-recovery-services-vault). Se si desidera tooback una singola macchina virtuale, è possibile avviare processo di backup hello dal Pannello di gestione di macchina virtuale.

## <a name="configure-hello-backup-job-from-hello-vm-management-blade"></a>Configurare un processo di backup hello dal Pannello di gestione di hello macchina virtuale

Utilizzare hello successivo processo di backup di passaggi tooconfigure hello dal Pannello di gestione di macchine virtuali di hello in hello portale di Azure. Questi passaggi si applicano toohello di macchine virtuali nel portale classico hello.

1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Nel menu Hub hello, fare clic su **più servizi** e nella finestra di dialogo Filtro hello, digitare **macchine virtuali**. Durante la digitazione, hello elenco di filtri di risorse. Dopo averla individuata, selezionare la voce Macchine virtuali.

  ![Nel menu Hub fare clic sulla finestra di dialogo di più servizi tooopen testo e digitare le macchine virtuali](./media/backup-azure-vms-first-look-arm/open-vm-from-hub.png)

  viene visualizzato l'elenco di Hello delle macchine virtuali (VM) nella sottoscrizione hello.

  ![viene visualizzato l'elenco di Hello di macchine virtuali nella sottoscrizione hello.](./media/backup-azure-vms-first-look-arm/list-of-vms.png)

3. Dall'elenco di hello, selezionare una macchina virtuale tooback backup.

  ![viene visualizzato l'elenco di Hello di macchine virtuali nella sottoscrizione hello.](./media/backup-azure-vms-first-look-arm/list-of-vms-selected.png)

  Quando si seleziona hello VM, elenco hello di macchine virtuali vengono spostati toohello sinistra e pannello Gestione di macchine virtuali hello e dashboard di hello macchina virtuale, aprire. </br>
 ![Pannello di gestione della VM](./media/backup-azure-vms-first-look-arm/vm-management-blade.png)

4. Nel Pannello di gestione VM hello, in hello **impostazioni** fare clic su **Backup**. </br>

  ![Opzione di backup nel pannello di gestione della macchina virtuale](./media/backup-azure-vms-first-look-arm/backup-option-vm-management-blade.png)

  verrà visualizzata la finestra di backup blade di Hello attiva.

  ![Opzione di backup nel pannello di gestione della macchina virtuale](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

5. Per l'insieme di credenziali di servizi di ripristino hello, fare clic su **selezionare esistente** e scegliere l'insieme di credenziali hello dall'elenco a discesa hello.

  ![Procedura guidata Abilita backup](./media/backup-azure-vms-first-look-arm/vm-blade-enable-backup.png)

  Se sono non presenti gli insiemi di credenziali servizi di ripristino o si desidera toouse un nuovo insieme di credenziali, fare clic su **Crea nuovo** e specificare il nome di hello per nuovo insieme di credenziali hello. Viene creato un nuovo insieme di credenziali in hello stesso gruppo di risorse e la stessa posizione come macchina virtuale hello. Se si desidera toocreate un insieme di credenziali di servizi di ripristino con valori diversi, vedere hello sezione sul troppo[creare un insieme di credenziali di servizi di ripristino](backup-azure-vms-first-look-arm.md#create-a-recovery-services-vault-for-a-vm).

6. Fare clic su Dettagli hello tooview di criteri di Backup, hello **criteri di Backup**.

  Hello **criteri di Backup** pannello viene aperto e fornisce dettagli hello del criterio di hello selezionato. Se esistono altri criteri, utilizzare hello dal menu a discesa toochoose diversi criteri di backup. Se si desidera toocreate un criterio, selezionare **Crea nuovo** dal menu a discesa hello. Per istruzioni sulla definizione di un criterio di backup, vedere [Definizione di un criterio di backup](backup-azure-vms-first-look-arm.md#defining-a-backup-policy). dei criteri di backup toosave hello modifiche toohello e toohello restituito Abilita backup pannello, fare clic su **OK**.

  ![Selezionare il criterio di backup](./media/backup-azure-vms-first-look-arm/setting-rs-backup-policy-new-2.png)

7. Nel Pannello di backup attiva hello, fare clic su **Abilita Backup** criteri hello toodeploy. Distribuzione di criteri di hello associa insieme di credenziali hello e macchine virtuali hello.

  ![Pulsante Abilita backup](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-button.png)

8. È possibile monitorare lo stato di avanzamento di hello configurazione tramite le notifiche di hello vengono visualizzate nel portale di hello. Hello di esempio seguente viene illustrato che la distribuzione è stato avviato.

  ![Notifica di Abilita backup](./media/backup-azure-vms-first-look-arm/vm-management-blade-enable-backup-notification.png)

9. Una volta lo stato di avanzamento di hello configurazione completata, nel Pannello di gestione di hello macchina virtuale, fare clic su **Backup** blade di elemento di Backup tooopen hello e visualizzare i dettagli di hello.

  ![Visualizzazione dell'elemento di backup della macchina virtuale](./media/backup-azure-vms-first-look-arm/backup-item-view.png)

  Al completamento di backup iniziale hello, **stato ultimo backup** viene illustrato come **avviso (backup iniziale in sospeso)**. si verifica toosee momento hello successivo processo di backup, in **criteri di Backup** fare clic sul nome del criterio hello hello. viene visualizzata la pannello dei criteri di Backup Hello ora hello del backup pianificato hello.

10. toorun un Backup del processo e creare il punto di ripristino iniziale hello, su hello Backup dell'insieme di credenziali fare clic su pannello **Backup ora**.

  ![Fare clic su backup iniziale hello toorun ora Backup](./media/backup-azure-vms-first-look-arm/backup-now.png)

  verrà visualizzata la finestra di Backup ora pannello Hello.

  ![Mostra pannello hello Esegui Backup](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

11. Nel pannello Esegui Backup hello fare clic sull'icona calendario hello, utilizzare hello tooselect di controllo calendario hello ultimo giorno di tale punto di ripristino è stato mantenuto e fare clic su **Backup**.

  ![impostare hello ultimo giorno hello Esegui Backup viene mantenuto un punto di ripristino](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Le notifiche di distribuzione consentono di sapere che è possibile monitorare lo stato di avanzamento hello del processo di hello nella pagina processi di Backup hello e processo di backup hello è stato attivato.

## <a name="configure-hello-backup-job-from-hello-recovery-services-vault"></a>Configurare un processo di backup hello da hello che insieme di credenziali di servizi di ripristino
processo di backup di hello tooconfigure termine hello alla procedura seguente.  

1. Creare un insieme di credenziali di Servizi di ripristino per una macchina virtuale.
2. Utilizzare Ciao tooselect portale Azure uno Scenario di impostare un criterio di Backup e identificare tooprotect elementi.
3. Eseguire il backup iniziale hello.

## <a name="create-a-recovery-services-vault-for-a-vm"></a>Creare l'insieme di credenziali dei servizi di ripristino per una macchina virtuale
Un insieme di credenziali di servizi di ripristino è un'entità contenente tutti i backup di hello e i punti di ripristino che sono stati creati nel corso del tempo. Hello insieme di credenziali di servizi di ripristino contiene anche i criteri di backup hello applicati toohello protetto le macchine virtuali.

> [!NOTE]
> Il backup delle VM è un processo locale. È possibile eseguire il backup di macchine virtuali dall'insieme di credenziali di un'unica posizione tooa servizi di ripristino in un'altra posizione. In tal caso, per ogni località di Azure con backup toobe di macchine virtuali, almeno un insieme di credenziali di servizi di ripristino deve esistere in tale percorso.
>
>

toocreate un insieme di credenziali di servizi di ripristino:

1. Se non già stato fatto, accedere toohello [portale di Azure](https://portal.azure.com/) tramite la sottoscrizione di Azure.
2. Nel menu Hub hello, fare clic su **più servizi** e nel tipo di finestra di dialogo Filtro hello **servizi di ripristino**. Durante la digitazione, hello elenco di filtri di risorse. Quando vengono visualizzati gli insiemi di credenziali di servizi di ripristino nell'elenco di hello, selezionarla.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Se nella sottoscrizione hello sono insiemi di credenziali di servizi di ripristino, vengono elencati gli insiemi di credenziali di hello.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-azure-vms-first-look-arm/list-of-rs-vault.png)
3. In hello **insiemi di credenziali di servizi di ripristino** menu, fare clic su **Aggiungi**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Servizi di ripristino Hello insieme di credenziali si apre Pannello chiesto tooprovide un **nome**, **sottoscrizione**, **gruppo di risorse**, e **percorso**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. Per **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello. nome di Hello deve toobe univoco per la sottoscrizione di Azure hello. Digitare un nome che contenga tra i 2 e i 50 caratteri. Deve iniziare con una lettera e può contenere solo lettere, numeri e trattini.

5. In hello **sottoscrizione** sezione, utilizzare hello toochoose di menu a discesa hello sottoscrizione di Azure. Se si utilizza una sola sottoscrizione, che viene visualizzato di sottoscrizione ed è possibile ignorare toohello successivo passaggio. Se non sei sicuro che toouse di sottoscrizione, utilizzare predefinito hello (o suggerito) sottoscrizione. Sono disponibili più scelte solo se l'account dell'organizzazione è associato a più sottoscrizioni di Azure.

6. In hello **gruppo di risorse** sezione:

    * Selezionare **Crea nuovo** se si desidera toocreate un gruppo di risorse.
    Or
    * Selezionare **utilizzare esistente** e fare clic su hello dal menu a discesa toosee hello disponibili elenco di gruppi di risorse.

  Per informazioni complete su gruppi di risorse, vedere hello [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).

7. Fare clic su **percorso** tooselect hello località geografica per l'insieme di credenziali hello. Questa opzione determina l'area geografica di hello in cui viene inviati ai dati di backup.

  > [!IMPORTANT]
  > Se si è certi della posizione di hello in cui esiste la macchina virtuale, chiudere la finestra di dialogo Creazione dell'insieme di credenziali hello e passare toohello elenco di macchine virtuali nel portale di hello. Se si hanno macchine virtuali in più aree, creare un insieme di credenziali di Servizi di ripristino in ogni area. Creare hello nella prima posizione hello prima di passare alla posizione successiva toohello. È presente che alcun account di archiviazione necessario toospecify hello non utilizzato toostore hello dati di backup - insieme di credenziali di servizi di ripristino hello e hello servizio Backup di Azure gestisce automaticamente la archiviazione hello.
  >

8. Nella parte inferiore di hello del pannello dell'insieme di credenziali di servizi di ripristino hello, fare clic su **crea**.

    Può richiedere alcuni minuti per hello che toobe creato insieme di credenziali di servizi di ripristino. Monitorare le notifiche di stato hello in area destra superiore hello del portale hello. Una volta creato l'insieme di credenziali, viene visualizzato nell'elenco hello degli insiemi di credenziali di servizi di ripristino. Se l'insieme di credenziali non viene visualizzato dopo qualche minuto, fare clic su **Aggiorna**.

    ![Fare clic sul pulsante Aggiorna](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Dopo aver visualizzato l'insieme di credenziali nell'elenco di hello degli insiemi di credenziali di servizi di ripristino, si è pronti tooset ridondanza dell'archiviazione hello.

Dopo aver creato l'insieme di credenziali, informazioni su come tooset hello replica di archiviazione.

### <a name="set-storage-replication"></a>Impostare la replica di archiviazione
opzione di replica di archiviazione Hello consente toochoose tra l'archiviazione con ridondanza geografica e l'archiviazione con ridondanza locale. Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica. Se hello insieme di credenziali di servizi di ripristino del backup primario, lasciare hello archiviazione replica opzione set toogeo l'archiviazione con ridondanza. Se si vuole un'opzione più economica ma non altrettanto permanente, scegliere l'archiviazione con ridondanza locale. Altre informazioni sui [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage) opzioni di archiviazione in hello [Cenni preliminari sulla replica di archiviazione di Azure](../storage/common/storage-redundancy.md).

impostazione di replica tooedit hello archiviazione:

1. Da hello **insiemi di credenziali di servizi di ripristino** blade, nuovo insieme di credenziali selezionare hello.

  ![Selezionare nuovo insieme di credenziali hello hello elenco dell'insieme di credenziali di servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

  Quando si seleziona l'insieme di credenziali hello, hello pannello impostazioni (*che ha il nome dell'insieme di credenziali di hello nella parte superiore di hello*) e pannello Dettagli insieme di credenziali hello aperto.

  ![Configurazione dell'archiviazione hello vista per nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. Nel pannello impostazioni di hello nuovo insieme di credenziali, utilizzare hello tooscroll di scorrimento verticale verso il basso toohello sezione gestione e fare clic su **infrastruttura Backup**.
    verrà visualizzata la finestra di blade Backup infrastruttura Hello.
3. Nel Pannello di hello infrastruttura di Backup, fare clic su **la configurazione del Backup** tooopen hello **la configurazione del Backup** blade.

    ![Set di configurazione dell'archiviazione hello per nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)
4. Scegliere l'opzione di replica di archiviazione appropriato hello per l'insieme di credenziali.

    ![opzioni di configurazione dell'archiviazione](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

    Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica. Se si usa Azure come un endpoint di archiviazione di backup primario, continuare toouse **con ridondanza geografica**. Se non si utilizza Azure come un endpoint di archiviazione di backup primario, quindi scegliere **ridondanza locale**, che consente di ridurre i costi di archiviazione di Azure hello. Per altre informazioni sulle opzioni di archiviazione [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [con ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage), vedere [Panoramica della ridondanza di archiviazione](../storage/common/storage-redundancy.md).


## <a name="select-a-backup-goal-set-policy-and-define-items-tooprotect"></a>Selezionare un obiettivo di backup, impostare criteri e definire gli elementi tooprotect
Prima di registrare una macchina virtuale con un insieme di credenziali, eseguire hello tooensure di processo di individuazione che eventuali nuove macchine virtuali che sono stati aggiunti toohello sottoscrizione vengono identificate. le query di processo di Hello Azure per elenco hello delle macchine virtuali nella sottoscrizione di hello, insieme a informazioni aggiuntive come nome del servizio cloud hello e area hello. Nel portale di Azure hello, scenario si riferisce toowhat sarà tooput nell'insieme di credenziali di hello recovery services. Criteri sono pianificazione hello per la frequenza e quando vengono eseguiti i punti di ripristino. Criteri includono anche periodo di mantenimento dei punti di ripristino hello hello.

1. Se si dispone già di un insieme di credenziali aprire Servizi di ripristino, procedere toostep 2. In caso contrario, nel menu Hub hello, fare clic su **più servizi** e nell'elenco di hello delle risorse, digitare **servizi di ripristino** e fare clic su **insiemi di credenziali di servizi di ripristino**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    viene visualizzato l'elenco di Hello degli archivi di servizi di ripristino.

    ![Visualizzazione di hello servizi di ripristino di insiemi di credenziali di elenco](./media/backup-azure-arm-vms-prepare/rs-list-of-vaults.png)

    Hello degli archivi di servizi di ripristino selezionare nell'elenco tooopen un insieme di credenziali per il dashboard.

     ![Pannello dell'insieme di credenziali aperto](./media/backup-azure-arm-vms-prepare/new-vault-settings-blade.png)

2. Nel menu del dashboard hello insieme di credenziali, fare clic su **Backup** blade di Backup tooopen hello.

    ![Pannello Backup aperto](./media/backup-azure-arm-vms-prepare/backup-button.png)

    Aprire i pannelli di Backup e Backup obiettivo Hello.

    ![Pannello Scenario aperto](./media/backup-azure-arm-vms-prepare/select-backup-goal-1.png)
3. Nel Pannello di obiettivo di Backup hello, da hello **in cui viene eseguito il carico di lavoro** menu a discesa, scegliere Azure. Da hello **cosa si desidera toobackup** elenco a discesa, scegliere una macchina virtuale, quindi fare clic su **OK**.

    Queste azioni registrare l'estensione della macchina virtuale hello insieme di credenziali hello. Obiettivo di Backup pannello chiude Hello e hello **criteri di Backup** apre blade.

    ![Pannello Scenario aperto](./media/backup-azure-arm-vms-prepare/select-backup-goal-2.png)

4. Nel Pannello di criteri di Backup hello, selezionare i criteri di backup hello da tooapply toohello insieme di credenziali.

    ![Selezionare il criterio di backup](./media/backup-azure-arm-vms-prepare/setting-rs-backup-policy-new.png)

    Dettagli Hello del criterio predefinito hello sono elencati nel menu di scelta rapida hello. Se si desidera toocreate un criterio, selezionare **Crea nuovo** dal menu a discesa hello. Per istruzioni sulla definizione di un criterio di backup, vedere [Definizione di un criterio di backup](backup-azure-vms-first-look-arm.md#defining-a-backup-policy).
    Fare clic su **OK** tooassociate dei criteri di backup hello con insieme di credenziali hello.

    Hello chiude pannello dei criteri di Backup e hello **selezionare le macchine virtuali** apre blade.
5. In hello **selezionare le macchine virtuali** pannello, scegliere hello tooassociate di macchine virtuali con hello specificato criteri e fare clic su **OK**.

    ![Selezionare il carico di lavoro](./media/backup-azure-arm-vms-prepare/select-vms-to-backup.png)

    macchina virtuale Hello selezionato viene convalidato. Se non è possibile visualizzare hello virtuale macchine che si prevede di toosee, verificare che esistano in hello nello stesso percorso di Azure come archivio di servizi di ripristino hello. percorso Hello di hello che insieme di credenziali di servizi di ripristino viene visualizzato nel dashboard dell'insieme di credenziali hello.

6. Dopo aver definito tutte le impostazioni per l'insieme di credenziali hello, nel Pannello di hello Backup, fare clic su **abilitare il Backup** toodeploy hello insieme di credenziali toohello criteri e hello macchine virtuali. Distribuzione di criteri di backup hello non crea punto di ripristino iniziale hello per la macchina virtuale hello.

    ![Abilita backup](./media/backup-azure-arm-vms-prepare/vm-validated-click-enable.png)

Dopo avere abilitato correttamente il backup di hello, i criteri di backup verranno eseguito su pianificazione. Tuttavia, procedere tooinitiate hello primo processo di backup.

## <a name="initial-backup"></a>Backup iniziale
Una volta distribuito un criterio di backup nella macchina virtuale hello, che non ne implica dati hello sono stato eseguito il backup. Per impostazione predefinita, hello prima pianificati backup (come definito nel criterio di backup hello) corrisponde hello iniziale. Fino a quando non si verifica il backup iniziale hello, hello ultimo stato di Backup su hello **i processi di Backup** pannello viene visualizzato come **avviso (backup iniziale in sospeso)**.

![Backup in sospeso](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

A meno che il backup iniziale è scadenza toobegin imminente, è consigliabile eseguire **Esegui backup**.

toorun hello iniziale processo di backup:

1. Nel dashboard dell'insieme di credenziali hello, fare clic sul numero hello in **elementi Backup**, oppure fare clic su hello **elementi Backup** riquadro. <br/>
  ![Icona Impostazioni](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)

  Hello **elementi Backup** apre blade.

  ![Elementi di backup](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. In hello **elementi Backup** blade, elemento selezionare hello.

  ![Icona Impostazioni](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  Hello **elementi Backup** viene aperto l'elenco. <br/>

  ![Processo di backup attivato](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. In hello **elementi Backup** fare clic sui puntini di sospensione hello **...**  menu di scelta rapida tooopen hello.

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu.png)

  viene visualizzato il menu di scelta rapida Hello.

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. Nel menu di scelta rapida hello, fare clic su **Backup ora**.

  ![Menu di scelta rapida](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  verrà visualizzata la finestra di Backup ora pannello Hello.

  ![Mostra pannello hello Esegui Backup](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. Nel pannello Esegui Backup hello fare clic sull'icona calendario hello, utilizzare hello tooselect di controllo calendario hello ultimo giorno di tale punto di ripristino è stato mantenuto e fare clic su **Backup**.

  ![impostare hello ultimo giorno hello Esegui Backup viene mantenuto un punto di ripristino](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  Le notifiche di distribuzione consentono di sapere che è possibile monitorare lo stato di avanzamento hello del processo di hello nella pagina processi di Backup hello e processo di backup hello è stato attivato. A seconda delle dimensioni di hello della macchina virtuale, la creazione di backup iniziale hello potrebbe richiedere qualche minuto.

6. lo stato di hello tooview o di una traccia di backup iniziale hello, nel dashboard dell'insieme di credenziali hello in hello **i processi di Backup** fare clic su riquadro **In corso**.

  ![Riquadro dei processi di backup](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  Apre il pannello di processi di Backup Hello.

  ![Riquadro dei processi di backup](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  In hello **i processi di Backup** pannello, è possibile visualizzare lo stato di hello di tutti i processi. Controllare se il processo di backup hello per la macchina virtuale è ancora in corso o ha terminato. Al termine di un processo di backup, lo stato di hello è *completato*.

  > [!NOTE]
  > Come parte dell'operazione di backup hello, hello servizio Backup di Azure esegue un'estensione di backup toohello comando in ogni macchina virtuale di tooflush tutti scrive e creare uno snapshot coerenza.
  >
  >


[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a>Installare hello agente della macchina virtuale nella macchina virtuale hello
Queste informazioni vengono fornite nel caso in cui siano necessarie. Hello agente VM di Azure deve essere installato nella macchina virtuale di Azure per hello Backup estensione toowork hello. Tuttavia, se la macchina virtuale è stata creata da hello raccolta di Azure, quindi hello agente VM è già presente nella macchina virtuale hello. Macchine virtuali che vengono migrate dal Data Center locale hello agente della macchina virtuale non verrà installato. In tal caso, hello agente VM deve toobe installato. Se si verificano problemi di backup hello macchina virtuale di Azure, verificare che hello agente VM di Azure sia installato correttamente nella macchina virtuale hello (vedere hello nella tabella seguente). Se si crea una macchina virtuale personalizzata, [verificare hello **hello installa agente VM** casella di controllo è selezionata](../virtual-machines/windows/classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) prima di provisioning della macchina virtuale hello.

Informazioni su hello [agente VM](https://go.microsoft.com/fwLink/?LinkID=390493&clcid=0x409) e [come tooinstall è](../virtual-machines/windows/classic/manage-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).

Hello nella tabella seguente fornisce informazioni aggiuntive su hello agente VM per Windows e le macchine virtuali Linux.

| **Operazione** | **Windows** | **Linux** |
| --- | --- | --- |
| L'installazione dell'agente VM hello |<li>Scaricare e installare hello [agente MSI](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). È necessario installazione hello toocomplete privilegi di amministratore. <li>[Aggiorna proprietà macchina virtuale hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate che hello agente è installato. |<li> Installare più recente hello [agente Linux](https://github.com/Azure/WALinuxAgent) da GitHub. È necessario installazione hello toocomplete privilegi di amministratore. <li> [Aggiorna proprietà macchina virtuale hello](http://blogs.msdn.com/b/mast/archive/2014/04/08/install-the-vm-agent-on-an-existing-azure-vm.aspx) tooindicate che hello agente è installato. |
| Aggiornamento agente VM hello |Aggiornamento hello agente della macchina virtuale è semplice come reinstallare hello [binari agente VM](http://go.microsoft.com/fwlink/?LinkID=394789&clcid=0x409). <br>Verificare che non venga eseguita alcuna operazione di backup durante l'aggiornamento dell'agente VM hello. |Seguire le istruzioni di hello [aggiornamento hello agente VM Linux](../virtual-machines/linux/update-agent.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json). <br>Verificare che nessuna operazione di backup è in esecuzione durante hello che agente VM viene aggiornata. |
| Convalida di installazione dell'agente VM hello |<li>Passare toohello *C:\WindowsAzure\Packages* cartella hello macchina virtuale di Azure. <li>È necessario trovare un file WaAppAgent.exe hello presentano.<li> Fare clic sul file hello, andare troppo**proprietà**, quindi selezionare hello **dettagli** campo versione prodotto di hello scheda deve essere 2.6.1198.718 o versione successiva. |N/D |

### <a name="backup-extension"></a>Estensione di backup
Una volta hello che agente VM viene installato nella macchina virtuale hello hello servizio Azure Backup installa hello estensione backup toohello agente della macchina virtuale. Hello servizio Azure Backup facilmente vengono aggiornati e le patch di estensione del backup hello senza l'intervento dell'utente.

il servizio di Backup Hello Installa estensione backup hello, anche se hello VM non è in esecuzione. Una macchina virtuale in esecuzione fornisce hello maggiore probabilità di riuscire a ottenere un punto di ripristino coerenti con l'applicazione. Tuttavia, hello servizio Backup di Azure continua tooback backup hello VM anche se è stato disattivato e non è stato installato l'estensione hello. Questo tipo di backup è noto come VM non in linea e punto di ripristino hello è *anomalo*.

## <a name="troubleshooting-information"></a>Informazioni sulla risoluzione dei problemi
Se si verificano problemi il completamento di alcune delle attività hello in questo articolo, consultare il [le indicazioni di Troubleshooting](backup-azure-vms-troubleshoot.md).

## <a name="pricing"></a>Prezzi
costo di Hello di backup di macchine virtuali di Azure è basato sul numero di hello di istanze protette. Per una definizione di istanza protetta, vedere [Che cos'è un'istanza protetta?](backup-introduction-to-azure-backup.md#what-is-a-protected-instance). Per un esempio del calcolo del costo di hello di backup di una macchina virtuale, vedere [come vengono calcolate istanze protette](backup-azure-vms-introduction.md#calculating-the-cost-of-protected-instances). Vedere hello dei prezzi di Azure Backup pagina per informazioni su [dei prezzi di Backup](https://azure.microsoft.com/pricing/details/backup/).

## <a name="questions"></a>Domande?
Se si hanno domande o se è presente una funzionalità che si desidera toosee incluso, [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).
