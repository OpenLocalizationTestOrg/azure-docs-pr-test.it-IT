---
title: i backup di distribuzione di gestione risorse di macchina virtuale aaaManage | Documenti Microsoft
description: Informazioni su come toomanage e monitorare i backup distribuito Gestione risorse di macchina virtuale
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: f3050283-d60f-472d-b464-cb844e70d67e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/28/2016
ms.author: trinadhk;markgal
ms.openlocfilehash: 241fc4b2a29c5cd8b8b0ee8efbf8ba4e96c6a7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-machine-backups"></a>Gestire i backup delle macchine virtuali di Azure
> [!div class="op_single_selector"]
> * [Gestire i backup delle macchine virtuali di Azure](backup-azure-manage-vms.md)
> * [Gestire i backup delle macchine virtuali classiche](backup-azure-manage-vms-classic.md)
>
>

In questo articolo vengono fornite indicazioni sulla gestione dei backup di macchine Virtuali e vengono illustrate le informazioni di avvisi di backup hello disponibili nel dashboard del portale hello. linee guida di Hello in questo articolo si applicano le macchine virtuali toousing con gli insiemi di credenziali di servizi di ripristino. In questo articolo non viene illustrata la creazione di hello di macchine virtuali, né spiegano come tooprotect le macchine virtuali. Per una panoramica sulla protezione di macchine virtuali distribuite di gestione risorse di Azure in Azure con un insieme di credenziali di servizi di ripristino, vedere [innanzitutto: eseguire il backup di macchine virtuali tooa insieme di credenziali di servizi di ripristino](backup-azure-vms-first-look-arm.md).

## <a name="manage-vaults-and-protected-virtual-machines"></a>Gestire gli insiemi di credenziali e le macchine virtuali protette
Nel portale di Azure hello, dashboard dell'insieme di credenziali di servizi di ripristino hello fornisce accesso tooinformation sull'inclusione di hello insieme di credenziali:

* Hello backup più recente dello snapshot, che è anche il punto di ripristino più recente di hello < br\>
* criteri di backup Hello < br\>
* Dimensioni totali di tutti gli snapshot di backup <br\>
* numero di macchine virtuali che sono protetti con insieme di credenziali hello < br\>

Molte attività di gestione con un backup della macchina virtuale iniziano con l'apertura di insieme di credenziali hello in dashboard hello. Tuttavia, poiché gli insiemi di credenziali possono essere utilizzati tooprotect tooview i dettagli relativi a una determinata macchina virtuale, aprire più elementi (o più macchine virtuali), dashboard di elemento di insieme di credenziali hello. Hello procedura riportata di seguito illustra come hello tooopen *dashboard dell'insieme di credenziali* e quindi continuare toohello *dashboard elemento dell'insieme di credenziali*. In entrambe le procedure che segnalano come tooadd hello insieme di credenziali e credenziali toohello elemento dashboard di Azure tramite hello Pin toodashboard comando sono disponibili "suggerimenti per la". PIN toodashboard è una modalità di creazione di un insieme di credenziali di scelta rapida toohello o un elemento. È inoltre possibile eseguire comandi comuni da collegamento hello.

> [!TIP]
> Se si dispone di più dashboard e aprire pannelli, utilizzare il dispositivo di scorrimento di hello-blu scuro nella parte inferiore di hello di hello di tooslide finestra hello Azure dashboard e viceversa.
>
>

![Visualizzazione completa con il dispositivo di scorrimento](./media/backup-azure-manage-vms/bottom-slider.png)

### <a name="open-a-recovery-services-vault-in-hello-dashboard"></a>Aprire un insieme di credenziali di servizi di ripristino nel dashboard di hello:
1. Accedi toohello [portale di Azure](https://portal.azure.com/).
2. Nel menu Hub hello, fare clic su **Sfoglia** e nell'elenco di hello delle risorse, digitare **servizi di ripristino**. Si inizia a digitare, hello filtri di elenco in base all'input. Fare clic su **Insiemi di credenziali dei servizi di ripristino**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-manage-vms/browse-to-rs-vaults.png) <br/>

    viene visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino.

    ![Elenco di insiemi di credenziali dei Servizi di ripristino ](./media/backup-azure-manage-vms/list-o-vaults.png) <br/>

   > [!TIP]
   > Se si aggiunge un toohello insieme di credenziali per il Dashboard di Azure, che insieme di credenziali è immediatamente accessibili quando si apre hello portale di Azure. un dashboard toohello insieme di credenziali, nell'elenco dell'insieme di credenziali hello toopin insieme di credenziali hello e scegliere **toodashboard Pin**.
   >
   >
3. Hello elenco degli insiemi di credenziali, selezionare hello insieme di credenziali tooopen relativo dashboard. Quando si seleziona insieme di credenziali hello, dashboard dell'insieme di credenziali hello e hello **impostazioni** pannello aperto. Nella seguente immagine di hello, hello **Contoso insieme di credenziali** dashboard è quello evidenziato.

    ![Aprire il dashboard dell'insieme di credenziali e il pannello Impostazioni](./media/backup-azure-manage-vms/full-view-rs-vault.png)

### <a name="open-a-vault-item-dashboard"></a>Aprire il dashboard di un elemento dell'insieme di credenziali
Nella procedura precedente hello è aperto il dashboard di insieme di credenziali hello. dashboard di elemento dell'insieme di credenziali hello tooopen:

1. Dashboard dell'insieme di credenziali hello in hello **elementi Backup** riquadro, fare clic su **macchine virtuali di Azure**.

    ![Aprire il riquadro Elementi di backup](./media/backup-azure-manage-vms/contoso-vault-1606.png)

    Hello **gli elementi di Backup** blade sono elencati l'ultimo processo backup di hello per ogni elemento. In questo esempio è presente una sola macchina virtuale, demovm-markgal, protetta da questo insieme di credenziali.  

    ![Riquadro Elementi di backup](./media/backup-azure-manage-vms/backup-items-blade.png)

   > [!TIP]
   > Per facilitare l'accesso, è possibile aggiungere un toohello di elemento di insieme di credenziali del Dashboard di Azure. un elemento dell'insieme di credenziali, nell'elenco di elementi dell'insieme di credenziali di hello, elemento hello pulsante destro del mouse e scegliere toopin **toodashboard Pin**.
   >
   >
2. In hello **elementi Backup** pannello, fare clic su elemento dashboard di hello elemento tooopen hello insieme di credenziali.

    ![Riquadro Elementi di backup](./media/backup-azure-manage-vms/backup-items-blade-select-item.png)

    dashboard di elemento di insieme di credenziali Hello e il relativo **impostazioni** pannello aperto.

    ![Dashboard degli elementi di backup con il pannello Impostazioni](./media/backup-azure-manage-vms/item-dashboard-settings.png)

    Dal dashboard di elemento di insieme di credenziali hello, è possibile eseguire molte attività di gestione delle chiavi, ad esempio:

   * Modificare i criteri o creare nuovi criteri di backup<br\>
   * Visualizzare i punti di ripristino e vedere il relativo stato di coerenza <br\>
   * Eseguire il backup su richiesta di una macchina virtuale <br\>
   * Arrestare la protezione delle macchine virtuali <br\>
   * Riprendere la protezione delle macchine virtuali <br\>
   * Eliminare i dati di un backup o un punto di ripristino <br\>
   * [ripristinare i dischi di backup](backup-azure-arm-restore-vms.md#restore-backed-up-disks)  <br\>

Per hello seguire le procedure seguenti, hello punto di partenza è dashboard elemento dell'insieme di credenziali di hello.

## <a name="manage-backup-policies"></a>Gestire i criteri di backup
1. In hello [dashboard elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard), fare clic su **tutte le impostazioni** tooopen hello **impostazioni** blade.

    ![Pannello Criteri di backup](./media/backup-azure-manage-vms/all-settings-button.png)
2. In hello **impostazioni** pannello, fare clic su **criteri di Backup** tooopen tale pannello.

    Nel Pannello di hello, vengono visualizzati dettagli intervallo frequenza e conservazione dei backup hello.

    ![Pannello Criteri di backup](./media/backup-azure-manage-vms/backup-policy-blade.png)
3. Da hello **scegliere Criteri di backup** menu:

   * toochange criteri, selezionare un criterio diverso e fare clic su **salvare**. nuovo criterio di Hello viene applicata immediatamente toohello insieme di credenziali. <br\>
   * Selezionare un criterio, toocreate **Crea nuovo**.

     ![Backup di una macchina virtuale](./media/backup-azure-manage-vms/backup-policy-create-new.png)

     Per istruzioni sulla creazione di criteri di backup, vedere [Definizione di un criterio di backup](backup-azure-manage-vms.md#defining-a-backup-policy).

[!INCLUDE [backup-create-backup-policy-for-vm](../../includes/backup-create-backup-policy-for-vm.md)]

> [!NOTE]
> Durante la gestione dei criteri di backup, verificare che hello toofollow [consigliate](backup-azure-vms-introduction.md#best-practices) per ottimizzare le prestazioni di backup
>
>

## <a name="on-demand-backup-of-a-virtual-machine"></a>Backup su richiesta di una macchina virtuale
È possibile eseguire il backup su richiesta di una macchina virtuale dopo averla configurata per la protezione. Se il backup iniziale hello è in sospeso, il backup su richiesta crea una copia completa della macchina virtuale hello in hello che insieme di credenziali di servizi di ripristino. Se il backup iniziale di hello è completato, un backup su richiesta invierà le modifiche apportate dallo snapshot precedente hello, insieme di credenziali di servizi di ripristino toohello. I backup successivi sono sempre incrementali.

> [!NOTE]
> periodo di mantenimento Hello per un backup su richiesta è il valore di conservazione hello specificato per il punto di backup giornaliero hello nei criteri di hello. Se non è selezionato alcun punto di backup giornaliero, viene utilizzato il punto di backup settimanale di hello.
>
>

backup tootrigger una richiesta di una macchina virtuale:

* In hello [dashboard elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard), fare clic su **Backup ora**.

    ![Pulsante Esegui backup ora](./media/backup-azure-manage-vms/backup-now-button.png)

    portale Hello assicura che si desidera toostart un processo di backup su richiesta. Fare clic su **Sì** toostart processo di backup hello.

    ![Pulsante Esegui backup ora](./media/backup-azure-manage-vms/backup-now-check.png)

    processo di backup Hello crea un punto di ripristino. periodo di mantenimento Hello hello del punto di ripristino è hello uguale al periodo di conservazione specificato nei criteri di hello associato a una macchina virtuale hello. stato di avanzamento hello tootrack per il processo di hello, nel dashboard dell'insieme di credenziali hello, fare clic su hello **i processi di Backup** riquadro.  

## <a name="stop-protecting-virtual-machines"></a>Arrestare la protezione delle macchine virtuali
Se si sceglie toostop protezione di una macchina virtuale, viene chiesto se si desidera che i punti di ripristino hello tooretain. Esistono due modi toostop proteggono le macchine virtuali:

* interrompere tutti i processi di backup futuri ed eliminare tutti i punti di ripristino oppure
* arrestare tutti i processi di backup futuri, ma lasciare hello punti di ripristino <br/>

È un costo associato lasciando hello punti di ripristino nel servizio di archiviazione. Il vantaggio di hello di lasciare hello punti di ripristino è tuttavia che è possibile ripristinare una macchina virtuale hello in un secondo momento, se lo si desidera. Per informazioni sul costo di hello di lasciare hello punti di ripristino, vedere hello [prezzi](https://azure.microsoft.com/pricing/details/backup/). Se si sceglie toodelete tutti i punti di ripristino, è possibile ripristinare una macchina virtuale hello.

protezione toostop per una macchina virtuale:

1. In hello [dashboard elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard), fare clic su **Interrompi backup**.

    ![Pulsante Arresta backup](./media/backup-azure-manage-vms/stop-backup-button.png)

    verrà visualizzata la finestra di blade Interrompi Backup Hello.

    ![Pannello Arresta backup](./media/backup-azure-manage-vms/stop-backup-blade.png)
2. In hello **Interrompi Backup** pannello, scegliere se tooretain o delete hello dati di backup. casella di Hello informazioni dettagliate sul prescelto.

    ![Arresta protezione](./media/backup-azure-manage-vms/retain-or-delete-option.png)
3. Se si sceglie di dati di backup hello tooretain, ignorare toostep 4. Se si sceglie toodelete dati di backup, verificare i processi di backup hello toostop desiderato e quindi eliminare i punti di ripristino hello - Nome hello del tipo di elemento di hello.

    ![Arresta verifica](./media/backup-azure-manage-vms/item-verification-box.png)

    Se non si è certi del nome dell'elemento hello, passare il mouse sul nome di hello punto esclamativo tooview hello. Inoltre, in nome hello dell'elemento di hello **Interrompi Backup** nella parte superiore di hello del pannello hello.
4. L'aggiunta di un **motivo** o **commento** è facoltativa.
5. processo di backup hello toostop per l'elemento corrente hello, fare clic su ![backup pulsante di arresto](./media/backup-azure-manage-vms/stop-backup-button-blue.png)

    Un messaggio di notifica consentono di conoscere i processi di backup hello siano stati arrestati.

    ![Conferma arresto protezione](./media/backup-azure-manage-vms/stop-message.png)

## <a name="resume-protection-of-a-virtual-machine"></a>Riprendere la protezione di una macchina virtuale
Se hello **Mantieni dati di Backup** opzione scelto durante la protezione per la macchina virtuale hello è stata arrestata, è possibile tooresume protezione. Se hello **Elimina dati di Backup** è stata scelta l'opzione, quindi non è possibile riprendere la protezione per la macchina virtuale hello.

protezione per la macchina virtuale hello tooresume

1. In hello [dashboard elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard), fare clic su **Riprendi backup**.

    ![Riprendere la protezione](./media/backup-azure-manage-vms/resume-backup-button.png)

    Apre il pannello di criteri di Backup Hello.

   > [!NOTE]
   > Quando si proteggono nuovamente macchina virtuale hello, è possibile scegliere un criterio diverso rispetto a criterio hello con cui è stato inizialmente protetto macchina virtuale.
   >
   >
2. Seguire i passaggi di hello in [gestire criteri di backup](backup-azure-manage-vms.md#manage-backup-policies) criteri hello tooassign per la macchina virtuale hello.

    Una volta macchina virtuale toohello applicati criteri di backup hello, vedrai segue messaggio hello.

    ![Macchina virtuale protetta correttamente](./media/backup-azure-manage-vms/success-message.png)

## <a name="delete-backup-data"></a>Eliminare i dati di backup
È possibile eliminare i dati di backup hello associati a una macchina virtuale durante hello **Interrompi backup** processo, o in qualsiasi momento dopo hello processo di backup è stata completata. Potrebbe essere utile toowait giorni o settimane prima di eliminare i punti di ripristino hello. A differenza di ripristino dei punti di ripristino, durante l'eliminazione di dati di backup, è possibile scegliere toodelete punti di ripristino specifico. Se si scelgono toodelete ai dati di backup, eliminare tutti i punti di ripristino associati a elementi hello.

Hello procedura riportata di seguito si presuppone che il processo di Backup hello per la macchina virtuale hello è stato arrestato o disabilitato. Dopo aver disabilitato il processo di Backup di hello, hello **Riprendi backup** e **Elimina backup** opzioni sono disponibili nel dashboard di elemento di insieme di credenziali hello.

![Pulsanti Riprendi ed Elimina](./media/backup-azure-manage-vms/resume-delete-buttons.png)

dati di backup in una macchina virtuale con hello toodelete *Backup disabilitato*:

1. In hello [dashboard elemento dell'insieme di credenziali](backup-azure-manage-vms.md#open-a-vault-item-dashboard), fare clic su **Elimina backup**.

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/delete-backup-buttom.png)

    Hello **Elimina dati di Backup** apre blade.

    ![Tipo macchina virtuale](./media/backup-azure-manage-vms/delete-backup-blade.png)
2. Nome del tipo hello di hello elemento tooconfirm desiderato punti di ripristino toodelete hello.

    ![Arresta verifica](./media/backup-azure-manage-vms/item-verification-box.png)

    Se non si è certi del nome dell'elemento hello, passare il mouse sul nome di hello punto esclamativo tooview hello. Inoltre, in nome hello dell'elemento di hello **Elimina dati di Backup** nella parte superiore di hello del pannello hello.
3. L'aggiunta di un **motivo** o **commento** è facoltativa.
4. Fare clic su dati di backup hello toodelete per l'elemento corrente hello, ![backup pulsante di arresto](./media/backup-azure-manage-vms/delete-button.png)

    Un messaggio di notifica consente di verificare i dati di backup hello sono stati eliminati.

## <a name="next-steps"></a>Passaggi successivi
Per informazioni su come ricreare una macchina virtuale da un punto di ripristino, vedere [Ripristinare macchine virtuali in Azure](backup-azure-restore-vms.md). Per ulteriori informazioni sulla protezione di macchine virtuali, vedere [innanzitutto: eseguire il backup di macchine virtuali tooa insieme di credenziali di servizi di ripristino](backup-azure-vms-first-look-arm.md). Per informazioni sul monitoraggio degli eventi, vedere [Monitor alerts for Azure virtual machine backups](backup-azure-monitor-vms.md)(Monitorare gli avvisi per i backup delle macchine virtuali di Azure).
