---
title: aaaManage e monitorare i backup di macchina virtuale di Azure | Documenti Microsoft
description: Informazioni su come toomanage e monitoraggio virtuale di Azure per una macchina backup
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a>Gestire i processi di Backup di Azure comuni e attivare gli avvisi nel portale classico hello
> [!div class="op_single_selector"]
> * [Gestire i backup delle macchine virtuali di Azure](backup-azure-manage-vms.md)
> * [Gestire i backup delle macchine virtuali classiche](backup-azure-manage-vms-classic.md)
>
>

In questo articolo vengono fornite informazioni sulle comuni attività di gestione e monitoraggio per le macchine virtuali modello classico protette in Azure.  

> [!NOTE]
> Azure offre due modelli di distribuzione per creare e usare le risorse: [Resource Manager e distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). Vedere [preparare tooback l'ambiente di macchine virtuali di Azure](backup-azure-vms-prepare.md) per informazioni dettagliate sull'utilizzo di distribuzione classica le macchine virtuali del modello.
>
> [!IMPORTANT]
>A partire da marzo 2017, è possibile utilizzare non è più insiemi di credenziali Backup hello toocreate portale classico.
>
> È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup. **Entro il 1° novembre 2017**:
>- Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.

## <a name="manage-protected-virtual-machines"></a>Gestire le macchine virtuali protette
toomanage macchine virtuali protette:

1. tooview e gestire le impostazioni di backup per una macchina virtuale fare clic su hello **elementi protetti** scheda.
2. Fare clic sul nome hello di hello di toosee un elemento protetto **dettagli Backup** scheda, in cui vengono visualizzate informazioni sull'ultimo backup hello.

    ![Backup di una macchina virtuale](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. tooview e gestire le impostazioni di criteri di backup per una macchina virtuale fare clic su hello **criteri** scheda.

    ![Criteri per una macchina virtuale](./media/backup-azure-manage-vms/manage-policy-settings.png)

    Hello **criteri di Backup** scheda Mostra hello criterio esistente. È possibile modificare i criteri in base alle esigenze. Se è necessario un nuovo criterio toocreate fare clic su **crea** su hello **criteri** pagina. Si noti che se si desidera tooremove un criterio non deve contenere tutte le macchine virtuali è associate.

    ![Criteri per una macchina virtuale](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. È possibile ottenere ulteriori informazioni sulle azioni o lo stato per una macchina virtuale in hello **processi** pagina. Fare clic su un processo in hello elenco tooget ulteriori dettagli, o filtrare i processi per una macchina virtuale specifica.

    ![Processi](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a>Backup su richiesta di una macchina virtuale
È possibile eseguire il backup su richiesta di una macchina virtuale dopo averla configurata per la protezione. Se il backup iniziale hello è in sospeso per la macchina virtuale hello, backup su richiesta verrà creata una copia completa della macchina virtuale hello nell'insieme di credenziali di backup Azure. Se il primo backup viene completato, verrà di backup su richiesta solo le modifiche di trasmissione da un precedente backup tooAzure backup insieme di credenziali ad esempio, è sempre incrementale.

> [!NOTE]
> Periodo di mantenimento di un backup su richiesta è impostato un valore tooretention specificato per la conservazione giornaliera nel criterio di backup corrispondente toohello macchina virtuale.  
>
>

backup tootake una richiesta di una macchina virtuale:

1. Passare toohello **elementi protetti** pagina e selezionare **macchina virtuale di Azure** come **tipo** (se non è già selezionata) e fare clic su **selezionare**pulsante.

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/vm-type.png)
2. Selezionare hello e della macchina virtuale in cui desidera che una richiesta tootake backup fare clic su **Esegui Backup ora** pulsante nella parte inferiore di hello della pagina hello.

    ![Esegui backup](./media/backup-azure-manage-vms/backup-now.png)

    Verrà creato un processo di backup sulla macchina virtuale hello selezionato. Mantenimento del punto di ripristino creato tramite il processo sarà corrisponde a quello specificato nel criterio hello associata a una macchina virtuale hello.

    ![Creazione del processo di backup](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > criteri di hello tooview associato a una macchina virtuale, drill down in macchina virtuale in hello **elementi protetti** pagina e la scheda Criteri toobackup passare.
   >
   >
3. Una volta creato il processo di hello, è possibile fare clic su **Visualizza processo** pulsante di tipo avviso popup hello barra toosee processo corrispondente di hello nella pagina dei processi hello.

    ![Processo di backup creato](./media/backup-azure-manage-vms/created-job.png)
4. Dopo il completamento del processo di hello, verrà creato un punto di ripristino che è possibile utilizzare macchina virtuale di toorestore hello. Questo valore colonna punto di ripristino hello anche incrementa di 1 in **elementi protetti** pagina.

## <a name="stop-protecting-virtual-machines"></a>Arrestare la protezione delle macchine virtuali
È possibile scegliere toostop nei backup futuri hello di una macchina virtuale con hello le opzioni seguenti:

* Mantenere i dati di backup associati alla macchina virtuale nell'insieme di credenziali di Backup di Azure.
* Eliminare i dati di backup associati alla macchina virtuale.

Se sono stati selezionati i dati di backup tooretain associati alla macchina virtuale, è possibile utilizzare la macchina virtuale hello dati di backup toorestore hello. Per i dettagli relativi ai prezzi per queste macchine virtuali, fare clic [qui](https://azure.microsoft.com/pricing/details/backup/).

protezione tooStop per una macchina virtuale:

1. Passare troppo**elementi protetti** pagina e selezionare **macchina virtuale di Azure** come tipo di filtro hello (se non è già selezionata) e fare clic su **selezionare** pulsante.

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/vm-type.png)
2. Selezionare la macchina virtuale di hello e fare clic su **Arresta protezione dati** nella parte inferiore di hello della pagina hello.

    ![Arresta protezione](./media/backup-azure-manage-vms/stop-protection.png)
3. Per impostazione predefinita, Azure Backup non elimina i dati di backup hello associati alla macchina virtuale hello.

    ![Conferma arresto protezione](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    Se si desiderano toodelete dati di backup, selezionare la casella di controllo hello.

    ![Casella di controllo](./media/backup-azure-manage-vms/checkbox.png)

    Selezionare un motivo per l'interruzione del backup hello. Mentre questo è facoltativo, fornire un motivo verrà Guida toowork di Backup di Azure ai suggerimenti hello e assegnare priorità agli scenari cliente hello.
4. Fare clic su **Invia** hello toosubmit pulsante **arrestare la protezione dati** processo. Fare clic su **Visualizza processo** toosee hello processo hello corrispondente in **processi** pagina.

    ![Arresta protezione](./media/backup-azure-manage-vms/stop-protect-success.png)

    Se non è stato selezionato **Elimina dati di backup associati** opzione durante **Arresta protezione dati** procedura guidata, quindi registra il completamento del processo, la protezione stato diventa troppo**protezione interrotta**. dati Hello rimangono con Backup di Azure finché viene eliminato in modo esplicito. È sempre possibile eliminare dati hello selezionando una macchina virtuale hello in hello **elementi protetti** pagina e fare clic su **eliminare**.

    ![Protezione arrestata](./media/backup-azure-manage-vms/protection-stopped-status.png)

    Se si è scelto di hello **Elimina dati di backup associati** opzione, hello macchina virtuale non far parte di hello **elementi protetti** pagina.

## <a name="re-protect-virtual-machine"></a>Riattivare la protezione della macchina virtuale
Se non è stato selezionato hello **Elimina dati di backup associati** opzione **Arresta protezione dati**, è possibile proteggere nuovamente macchina virtuale hello seguendo toobacking simile passaggi di hello backup registrato virtuale macchine. Una volta protetto, la macchina virtuale sarà protetto in modo i dati di backup conservati toostop precedente e punti di ripristino creato dopo riproteggere.

Dopo aver riproteggere, lo stato di protezione della macchina virtuale hello verrà modificato troppo**Protected** se non esistono punti di ripristino precedenti troppo**Arresta protezione dati**.

  ![Protezione VM riattivata](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> Quando si proteggono nuovamente macchina virtuale hello, è possibile scegliere un criterio diverso rispetto a criterio hello con cui è stato inizialmente protetto macchina virtuale.
>
>

## <a name="unregister-virtual-machines"></a>Annullare la registrazione di macchine virtuali
Se si desidera una macchina virtuale di hello tooremove dall'insieme di credenziali backup hello:

1. Fare clic su hello **UNREGISTER** pulsante nella parte inferiore di hello della pagina hello.

    ![Disabilita protezione](./media/backup-azure-manage-vms/unregister-button.png)

    Viene visualizzata una notifica di tipo avviso popup nella parte inferiore di hello della schermata Ciao richiesta di conferma. Fare clic su **Sì** toocontinue.

    ![Disabilita protezione](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a>Eliminare i dati di backup
È possibile eliminare i dati di backup hello associati a una macchina virtuale, ovvero:

* Durante il processo Arresta protezione
* Dopo il completamento del processo Arresta protezione in una macchina virtuale

toodelete i dati di backup in una macchina virtuale, ovvero in hello *protezione interrotta* stato post corretto completamento di un **Interrompi Backup** processo:

1. Passare toohello **elementi protetti** pagina e selezionare **macchina virtuale di Azure** come *tipo* e fare clic su hello **selezionare** pulsante.

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/vm-type.png)
2. Selezionare una macchina virtuale hello. macchina virtuale di Hello sarà **protezione interrotta** stato.

    ![Protezione arrestata](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. Fare clic su hello **eliminare** pulsante nella parte inferiore di hello della pagina hello.

    ![Elimina backup](./media/backup-azure-manage-vms/delete-backup.png)
4. In hello **Elimina dati di backup** procedura guidata, selezionare un motivo per l'eliminazione di dati di backup (scelta consigliati) e fare clic su **Invia**.

    ![Elimina dati di backup](./media/backup-azure-manage-vms/delete-backup-data.png)
5. Verrà creato un processo toodelete backup di dati della macchina virtuale selezionata. Fare clic su **Visualizza processo** toosee processo corrispondente nella pagina processi.

    ![Eliminazione dei dati completata](./media/backup-azure-manage-vms/delete-data-success.png)

    Una volta completato il processo di hello, hello voce verrà rimosso dalla macchina virtuale corrispondente con toohello **gli elementi protetti** pagina.

## <a name="dashboard"></a>Dashboard
In hello **Dashboard** pagina è possibile esaminare le informazioni sulle macchine virtuali di Azure, i relativi archiviazione e i processi associati ad essi nel hello ultime 24 ore. È possibile visualizzare lo stato del backup ed eventuali errori di backup associati.

![Dashboard](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> I valori nel dashboard di hello vengono aggiornati una volta ogni 24 ore.
>
>

## <a name="auditing-operations"></a>Operazioni di controllo
Backup di Azure offre la revisione di hello "operazione i log" di operazioni di backup attivati dal cliente hello rende facile toosee esattamente quali operazioni di gestione sono state eseguite sul insieme di credenziali backup hello. Registri operazioni abilitare grande finale e il supporto per operazioni di backup hello di controllo.

Hello dopo le operazioni viene registrata nei log operazioni:

* Registra
* Unregister 
* Configura protezione
* Backup (sia backup pianificato che su richiesta tramite BackupNow)
* Ripristino
* Arresta protezione
* Elimina dati di backup
* Aggiungi criteri
* Elimina criteri
* Aggiorna criteri
* Annulla processo

operazione tooview registra l'insieme di credenziali backup tooa corrispondente:

1. Passare troppo**servizi di gestione** nel portale di Azure, quindi fare clic su hello **registri operazioni** scheda.

    ![Log delle operazioni](./media/backup-azure-manage-vms/ops-logs.png)
2. Nei filtri di hello selezionare **Backup** come *tipo* e specificare il nome dell'insieme di credenziali backup hello in *nome servizio* e fare clic su **Invia**.

    ![Filtro dei log operazioni](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. Nei registri operazioni hello, selezionare qualsiasi operazione e fare clic su **dettagli** toosee dettagli operazione tooan corrispondente.

    ![Log operazioni: recupero dei dettagli](./media/backup-azure-manage-vms/ops-logs-details.png)

    Hello **guidata dettagli** contiene informazioni sull'operazione hello attivato, il processo, Id di risorsa in cui viene attivata, questa operazione e ora di inizio dell'operazione di hello.

    ![Dettagli operazione](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a>Notifiche di avviso
È possibile ottenere le notifiche di avviso personalizzate per i processi di hello nel portale. Questo risultato si ottiene definendo le regole di avviso basate su PowerShell negli eventi dei log operativi. Si raccomanda di utilizzare *PowerShell 1.3.0 o versioni successive*.

toodefine tooalert una notifica personalizzata per gli errori di backup, un comando di esempio sarà simile:

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

**ResourceId**: è possibile ottenere queste informazioni dalla finestra popup Log operazioni come descritto nella sezione precedente. Nella finestra popup di dettagli di un'operazione ResourceUri è hello ResourceId toobe fornito per questo cmdlet.

**OperationName**: trattarsi del formato hello "Microsoft.Backup/backupvault/<EventName>" dove EventName è uno di registrare, annullare la registrazione, ConfigureProtection, Backup, ripristino, StopProtection, DeleteBackupData, UpdateProtectionPolicy CreateProtectionPolicy, DeleteProtectionPolicy,

**Status**: i valori supportati sono Started, Succeeded e Failed.

**Gruppo di risorse**: gruppo di risorse della risorsa hello in cui viene attivata l'operazione. È possibile ottenere queste informazioni dal valore di ResourceId. Valore compreso tra i campi */ResourceGroups /* e */providers/* in ResourceId corrisponde al valore hello per gruppo di risorse.

**Nome**: nome della regola di avviso hello.

**CustomEmail**: specificare toowhich indirizzo di posta elettronica personalizzati hello toosend notifica di avviso

**SendToServiceOwners**: questa opzione Invia gli amministratori tooall notifica di avviso e i coamministratori della sottoscrizione hello. Può essere usata nel cmdlet **New AzureRmAlertRuleEmail** .

### <a name="limitations-on-alerts"></a>Limitazioni per gli avvisi
Avvisi basati su eventi sono sottoposti toohello limitazioni seguenti:

1. Gli avvisi vengono attivati in tutte le macchine virtuali nell'insieme di credenziali backup hello. Non è possibile personalizzare il tooget gli avvisi per un set specifico di macchine virtuali in un insieme di credenziali di backup.
2. Questa funzionalità è in anteprima. [Altre informazioni](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. Si riceveranno avvisi da "alerts-noreply@mail.windowsazure.com". Attualmente non è possibile modificare il mittente di posta elettronica hello.

## <a name="next-steps"></a>Passaggi successivi
* [Ripristinare una macchina virtuale](backup-azure-restore-vms.md)
