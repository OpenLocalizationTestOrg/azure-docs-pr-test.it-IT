---
title: gli insiemi di credenziali e i server di servizi aaaManage Azure recovery | Documenti Microsoft
description: Utilizzare questa esercitazione toolearn come insiemi di credenziali di servizi di ripristino di Azure toomanage e server.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: 4eea984b-7ed6-4600-ac60-99d2e9cb6d8a
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: markgal
ms.openlocfilehash: b4c35c86faa0828b3c63a13b85c095c0cbaba50e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-manage-azure-recovery-services-vaults-and-servers-for-windows-machines"></a>Monitorare e gestire i server e gli insiemi di credenziali dei servizi di ripristino di Azure per i computer Windows
> [!div class="op_single_selector"]
> * [Gestione risorse](backup-azure-manage-windows-server.md)
> * [Classico](backup-azure-manage-windows-server-classic.md)
>
>

In questo articolo vengono fornite una panoramica di hello gestione e Monitoraggio attività di backup disponibili tramite hello Azure portal e hello Microsoft Azure Backup agent. Questo articolo presuppone che sia già disponibile una sottoscrizione di Azure e che sia stato creato almeno un insieme di credenziali di Servizi di ripristino.

[!INCLUDE [learn-about-deployment-models](../../includes/learn-about-deployment-models-rm-include.md)]


## <a name="open-a-recovery-services-vault"></a>Aprire un insieme di credenziali di Servizi di ripristino

dashboard dell'insieme di credenziali di servizi di ripristino Hello è possibile visualizzare i dettagli di hello o attributi di un insieme di credenziali di servizi di ripristino.

1. Accedi toohello [portale Azure](https://portal.azure.com/) tramite la sottoscrizione di Azure.
2. Nel menu Hub hello, fare clic su **più servizi**.

    ![Aprire l'elenco degli insiemi di credenziali di Servizi di ripristino](./media/backup-azure-manage-windows-server/open-rs-vault-list.png) <br/>

3. Si desidera tooopen un insieme di credenziali di servizi di ripristino. Nella finestra di dialogo hello inizia a digitare **servizi di ripristino**. Si inizia a digitare, elenco hello verrà filtrato in base all'input. Fare clic su **insiemi di credenziali di servizi di ripristino** elenco hello toodisplay di servizi di ripristino di insiemi di credenziali nella sottoscrizione.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-manage-windows-server/browse-to-rs-vaults-2.png) <br/>

    verrà visualizzato l'elenco di Hello degli insiemi di credenziali di servizi di ripristino.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-azure-manage-windows-server/list-of-rs-vaults.png) <br/>

4. Dall'elenco di hello degli insiemi di credenziali, selezionare il nome di hello dell'archivio di servizi di ripristino si desidera tooopen hello. verrà visualizzata la finestra di blade dashboard dell'insieme di credenziali di Hello servizi di ripristino.

    ![Dashboard dell'insieme di credenziali dei servizi di ripristino](./media/backup-azure-manage-windows-server/rs-vault-blade.png) <br/>

    Ora che è stata aperta l'insieme di credenziali di servizi di ripristino hello, provare a eseguire una delle attività di monitoraggio o la gestione di hello.

## <a name="monitor-backup-jobs-and-alerts"></a>Monitorare i processi di backup e gli avvisi

Monitorare i processi e avvisi da hello servizi di ripristino dell'insieme di credenziali dashboard, in cui vedere:

* Dettagli degli avvisi di backup
* I file e cartelle, nonché macchine virtuali di Azure protette nel cloud hello
* Spazio di archiviazione totale utilizzato in Azure
* Stato dei processi di backup

![Eseguire un backup delle attività del dashboard](./media/backup-azure-manage-windows-server/dashboard-tiles.png)

Fare clic su informazioni hello in ognuno di questi riquadri aprirà blade di hello associata sarà possibile gestire le attività correlate.

Dall'alto hello di hello Dashboard:

* Impostazioni: fornisce l'accesso alle attività di backup disponibili.
* Insieme di credenziali di backup - consente il backup di nuovi file e cartelle (o macchine virtuali di Azure) toohello servizi di ripristino.
* Delete - se l'insieme di credenziali dei servizi di un ripristino non è più utilizzato, è possibile eliminarla toofree spazio di archiviazione. Eliminazione è abilitata solo dopo aver eliminati tutti i server protetti dall'insieme di credenziali hello.

![Eseguire un backup delle attività del dashboard](./media/backup-azure-manage-windows-server/dashboard-tasks.png)

## <a name="alerts-for-backups-using-azure-backup-agent"></a>Avvisi per i backup con l'agente di Backup di Azure:
| Livello avviso | Avvisi inviati |
| --- | --- |
| Critico |Errore di backup, errore di ripristino |
| Avviso |Backup completato con avvisi (quando meno di 100 file non sottoposti a backup a causa di problemi di toocorruption e più di un milione correttamente backup) |
| Informazioni |None |

## <a name="manage-backup-alerts"></a>Gestire gli avvisi di backup
Fare clic su hello **gli avvisi di Backup** riquadro tooopen hello **gli avvisi di Backup** blade e gestire gli avvisi.

![Avvisi di backup](./media/backup-azure-manage-windows-server/manage-backup-alerts.png)

gli avvisi di Backup Hello Mostra riquadro hello numero di:

* avvisi critici non risolti nelle ultime 24 ore
* avvertenze non risolte nelle ultime 24 ore

Facendo clic su ognuno di questi collegamenti accetta toohello **gli avvisi di Backup** pannello con una visualizzazione filtrata di questi avvisi (critici o avvisi).

Dal pannello hello gli avvisi di Backup è:

* Scegliere hello informazioni appropriate tooinclude con gli avvisi.

    ![Scegliere le colonne](./media/backup-azure-manage-windows-server/choose-alerts-colunms.png)
* Filtrare gli avvisi per gravità, stato e ora di inizio/fine.

    ![Filtrare gli avvisi](./media/backup-azure-manage-windows-server/filter-alerts.png)
* Configurare le notifiche in relazione a gravità, frequenza e destinatari, oltre ad attivare o disattivare gli avvisi.

    ![Filtrare gli avvisi](./media/backup-azure-manage-windows-server/configure-notifications.png)

Se **per ogni avviso** sia selezionato come hello **notifica** frequenza viene eseguita alcuna raggruppamento o la riduzione di messaggi di posta elettronica. Ogni avviso restituisce 1 notifica. Questo è l'impostazione predefinita hello e posta elettronica risoluzione hello viene inoltre inviato immediatamente.

Se **Digest oraria** sia selezionato come hello **notifica** frequenza un messaggio di posta elettronica viene inviato utente toohello informa che non vi siano risolti nuovi avvisi generati in hello ultima ora. Viene inviato un messaggio di posta elettronica risoluzione alla fine hello ora hello.

Gli avvisi possono essere inviati per hello seguenti livelli di gravità:

* Critico
* Avviso
* Informazioni

Disattivare l'avviso di hello con hello **disattiva** pulsante nel Pannello di dettagli processo hello. Quando si fa clic su Disattiva, è possibile inserire note sulla risoluzione.

Si scelgono le colonne di hello desiderato tooappear nell'ambito dell'avviso hello con hello **scegliere le colonne** pulsante.

> [!NOTE]
> Da hello **impostazioni** pannello, gestire gli avvisi di backup selezionando **monitoraggio e report > avvisi ed eventi > avvisi di Backup** e quindi fare clic su **filtro** o ** Configurare le notifiche**.
>
>

## <a name="manage-backup-items"></a>Gestire gli elementi di backup
È ora disponibile nel portale di gestione di hello la gestione dei backup in locale. Nella sezione Backup hello del dashboard hello hello **gli elementi di Backup** riquadro mostra il numero di hello degli elementi di backup protetto toohello insieme di credenziali.

Fare clic su **File-cartelle** in hello riquadro gli elementi di Backup.

![Riquadro Elementi di backup](./media/backup-azure-manage-windows-server/backup-items-tile.png)

gli elementi di Backup Hello blade viene aperto con hello filtrare set tooFile-cartella in cui si verifica ogni backup specifico elemento elencati.

![Elementi di backup](./media/backup-azure-manage-windows-server/backup-item-list.png)

Se si seleziona un elemento di backup specifico dall'elenco di hello, vedrai informazioni essenziali di hello per quell'elemento.

> [!NOTE]
> Da hello **impostazioni** pannello gestire file e cartelle selezionando **elementi protetti > Backup elementi** e quindi selezionando **File-cartelle** da hello menu a discesa.
>
>

![Elementi di backup da Impostazioni](./media/backup-azure-manage-windows-server/backup-files-and-folders.png)

## <a name="manage-backup-jobs"></a>Gestire i processi di backup
I processi di backup per i backup di Azure e locale (quando è il server locale hello backup tooAzure) sono visibili nel dashboard di hello.

Nella sezione di Backup del dashboard hello hello, riquadro di processo di Backup hello Mostra il numero di hello di processi:

* in corso
* non è riuscita in hello ultime 24 ore.

toomanage processi di backup, fare clic su hello **i processi di Backup** riquadro, che apre il pannello di hello i processi di Backup.

![Elementi di backup da Impostazioni](./media/backup-azure-manage-windows-server/backup-jobs.png)

Modificare le informazioni di hello disponibili nel Pannello di processi di Backup hello con hello **scegliere le colonne** pulsante nella parte superiore di hello della pagina hello.

Hello utilizzare **filtro** tooselect pulsante tra file e cartelle e i backup di macchina virtuale di Azure.

Se non viene visualizzato stato eseguito il backup dei file e cartelle, fare clic su **filtro** pulsante nella parte superiore di hello della pagina hello e selezionare **file e cartelle** dal menu di tipo di elemento hello.

> [!NOTE]
> Da hello **impostazioni** pannello, gestire i processi di backup selezionando **monitoraggio e report > processi > processi di Backup** e quindi selezionando **File-cartelle** elenco hello menu.
>
>

## <a name="monitor-backup-usage"></a>Monitorare l'utilizzo del backup
Nella sezione di Backup del dashboard hello hello, riquadro di utilizzo di Backup hello Mostra archiviazione hello utilizzato in Azure. L'utilizzo dello spazio di archiviazione viene fornito per:

* Utilizzo dell'archiviazione con ridondanza locale associato all'insieme di credenziali hello del cloud
* Utilizzo di memoria di archiviazione con ridondanza geografica cloud associato all'insieme di credenziali hello

## <a name="manage-your-production-servers"></a>Gestire i server di produzione
Fare clic su server di produzione, toomanage **impostazioni**.

In Gestisci fare clic su **Infrastruttura di backup > Server di produzione**.

elenchi di blade Hello Server di produzione di tutti i server di produzione disponibili. Fare clic su un server di dettagli del server hello tooopen elenco hello.

![Elementi protetti](./media/backup-azure-manage-windows-server/production-server-list.png)


## <a name="open-hello-azure-backup-agent"></a>Agente di Backup di Azure aprire hello
Aprire hello **Microsoft Azure Backup agent** (disponibili tramite la ricerca di computer per *Backup di Microsoft Azure*).

![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)

Da hello **azioni** disponibile all'indirizzo hello destra della console di agente di backup hello è eseguire hello seguenti attività di gestione:

* Registra server
* Pianificazione di un backup
* Esegui backup
* Modifica proprietà

![Azioni della console dell'agente Backup di Microsoft Azure](./media/backup-azure-manage-windows-server/console-actions.png)

> [!NOTE]
> troppo**Ripristina dati**, vedere [ripristinare i file tooa Windows server o computer client Windows](backup-azure-restore-windows-server.md).
>
>

## <a name="modify-hello-backup-schedule"></a>Modifica pianificazione backup hello
1. Nell'agente di Backup di Microsoft Azure hello fare clic su **pianifica Backup**.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
2. In hello **pianificazione guidata Backup** lasciare hello **apportare modifiche toobackup elementi o tempistica** opzione selezionata e fare clic su **Avanti**.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
3. Se si desidera tooadd o modificare gli elementi, di hello **selezionare elementi tooBackup** fare clic su schermo **Aggiungi elementi**.

    È inoltre possibile impostare **impostazioni di esclusione** da questa pagina nella creazione guidata hello. Se si desidera che il file tooexclude o procedura hello per l'aggiunta di leggere i tipi di file [impostazioni di esclusione](#manage-exclusion-settings).
4. Selezionare il file hello e le cartelle desidera ripristinare tooback e fare clic su **OK**.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/add-items-modify.png)
5. Specificare hello **pianificazione del backup** e fare clic su **Avanti**.

    È possibile pianificare backup giornalieri (non più di 3 al giorno) o settimanali.

    ![Elementi per il backup di Windows Server](./media/backup-azure-manage-windows-server/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Specifica la pianificazione del backup hello è illustrata in dettaglio in questo [articolo](backup-azure-backup-cloud-as-tape.md).
   >

6. Seleziona hello **criteri di conservazione** copia di backup hello e fare clic su **Avanti**.

    ![Elementi per il backup di Windows Server](./media/backup-azure-manage-windows-server/select-retention-policy-modify.png)
7. In hello **conferma** schermata hello rivedere le informazioni e fare clic su **fine**.
8. Al termine della creazione di hello guidata hello **pianificazione del backup**, fare clic su **Chiudi**.

    Dopo la modifica della protezione, è possibile verificare che i backup attivano correttamente da passare toohello **processi** scheda e conferma che le modifiche vengono riflesse nel hello i processi di backup.

## <a name="enable-network-throttling"></a>Abilitare la limitazione della larghezza di banda della rete

l'agente Azure Backup Hello fornisce una scheda di limitazione delle richieste che consente di toocontrol modalità di utilizzo della larghezza di banda di rete durante il trasferimento dei dati. Questo controllo può essere utile se è necessario tooback dei dati durante le ore lavorative, ma non si desidera hello toointerfere di processo di backup con il traffico internet. La limitazione delle richieste di dati trasferimento applica tooback backup e ripristino.  

tooenable limitazione:

1. In hello **agente di Backup**, fare clic su **Modifica proprietà**.
2. In hello * * limitazione scheda, selezionare **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet**.

    ![Limitazione della larghezza di banda della rete](./media/backup-azure-manage-windows-server/throttling-dialog.png)

    Dopo aver abilitato la limitazione delle richieste, specificare hello consentito della larghezza di banda per trasferire i dati di backup durante **ore lavorative** e **ore Non lavorative**.

    i valori di larghezza di banda Hello iniziano da 512 kilobyte per secondo (Kbps) e possono aumentare fino a too1023 megabyte al secondo (Mbps). È anche possibile designare inizio hello e di fine per **ore lavorative**, e i giorni della settimana hello vengono considerati lavoro giorni. tempo di Hello di fuori di hello designato per le ore lavorative è ore non lavorative toobe considerate.
3. Fare clic su **OK**.

## <a name="manage-exclusion-settings"></a>Gestire le impostazioni di esclusione
1. Aprire hello **Microsoft Azure Backup agent** (sarà possibile trovarlo cercando il computer per *Backup di Microsoft Azure*).

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/snap-in-search.png)
2. Nell'agente di Backup di Microsoft Azure hello fare clic su **pianifica Backup**.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/schedule-backup.png)
3. In Pianificazione guidata Backup hello lasciare hello **apportare modifiche toobackup elementi o tempistica** opzione selezionata e fare clic su **Avanti**.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/modify-or-stop-a-scheduled-backup.png)
4. Fare clic su **Impostazioni di esclusione**.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclusion-settings.png)
5. Fare clic su **Aggiungi esclusione**.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/add-exclusion.png)
6. Selezionare il percorso di hello e quindi fare clic su **OK**.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclusion-location.png)
7. Aggiungere l'estensione del file hello in hello **tipo di File** campo.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclude-file-type.png)

    Aggiunta di un'estensione mp3

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclude-mp3.png)

    tooadd un'altra estensione, fare clic su **Aggiunta esclusione** e immettere un'altra estensione del tipo di file (aggiunta di un'estensione JPEG).

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/exclude-jpg.png)
8. Dopo aver aggiunto tutte le estensioni di hello, fare clic su **OK**.
9. Continuare il processo hello pianificazione guidata Backup fare clic su **Avanti** finché hello **pagina di conferma**, quindi fare clic su **fine**.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server/finish-exclusions.png)

## <a name="frequently-asked-questions"></a>Domande frequenti
**Q1. stato del processo di backup Hello indicato come completato nel hello agente Azure backup, perché non vengono riflesse immediatamente nel portale?**

R1. Si è in ritardo massimo di 15 minuti tra lo stato del processo di backup hello applicata hello agente Azure backup e hello portale di Azure.

**Q.2 quando un processo di backup non riesce, quanto tempo occorre tooraise un avviso?**

All'interno di 20 minuti di hello Azure backup non riusciti, viene generato un avviso. 2.

**D3. Esiste un caso in cui non viene inviato un messaggio di posta elettronica se le notifiche sono configurate?**

R3. Di seguito sono casi hello quando non verrà inviate notifiche hello nella frequenza degli avvisi hello tooreduce ordine:

* Se le notifiche sono configurate ogni ora e un avviso viene generato e risolto entro ora hello
* Il processo viene annullato.
* Secondo processo di backup non riuscito perché è in corso il processo di backup originale.

## <a name="troubleshooting-monitoring-issues"></a>Risoluzione dei problemi di monitoraggio
**Problema:** processi e/o gli avvisi generati da agente Azure Backup hello non vengono visualizzati nel portale di hello.

**Risoluzione dei problemi:** hello processo ```OBRecoveryServicesManagementAgent```, invia hello processo e avviso dati toohello servizio Azure Backup. A volte questo processo può risultare danneggiato o arrestato.

1. il processo di hello tooverify non è in esecuzione, aprire **Task Manager** e verificare se hello ```OBRecoveryServicesManagementAgent``` processo è in esecuzione.
2. Supponendo che il processo di hello non è in esecuzione, aprire **Pannello di controllo** e visualizzare hello elenco dei servizi. Avviare o riavviare **Agente di gestione di Servizi di ripristino di Microsoft Azure**.

    Per ulteriori informazioni, visitare registri hello:<br/>
   `<AzureBackup_agent_install_folder>\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider*` Ad esempio:<br/>
   `C:\Program Files\Microsoft Azure Recovery Services Agent\Temp\GatewayProvider0.errlog`

## <a name="next-steps"></a>Passaggi successivi
* [Ripristino di Windows Server o Windows Client da Azure](backup-azure-restore-windows-server.md)
* toolearn ulteriori informazioni sui Backup di Azure, vedere [Cenni preliminari su Backup di Azure](backup-introduction-to-azure-backup.md)
* Visitare hello [Forum di Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933)
