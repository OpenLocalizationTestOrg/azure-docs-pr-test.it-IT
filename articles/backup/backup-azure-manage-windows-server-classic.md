---
title: aaaManage insiemi di credenziali di Backup di Azure e i server Azure utilizzando il modello di distribuzione classica hello | Documenti Microsoft
description: Utilizzare questa esercitazione toolearn come insiemi di credenziali di Backup di Azure toomanage e server.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: tysonn
ms.assetid: f175eb12-0905-437f-91fd-eaee03ab6e81
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2017
ms.author: markgal;
ms.openlocfilehash: 6c38b04f4a76604bfd639a9b2d58237ce44e2386
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-backup-vaults-and-servers-using-hello-classic-deployment-model"></a>Gestire gli insiemi di credenziali di Backup di Azure e i server utilizzando il modello di distribuzione classica hello
> [!div class="op_single_selector"]
> * [Gestione risorse](backup-azure-manage-windows-server.md)
> * [Classico](backup-azure-manage-windows-server-classic.md)
>
>

In questo articolo sono disponibili una panoramica delle attività di gestione dei backup hello disponibili tramite hello portale di Azure classico e l'agente di Microsoft Azure Backup hello.

> [!IMPORTANT]
> Azure offre due diversi modelli di distribuzione per creare e usare le risorse: [Gestione risorse e la distribuzione classica](../azure-resource-manager/resource-manager-deployment-model.md). In questo articolo viene illustrato l'utilizzo del modello di distribuzione classica hello. Si consiglia di utilizzano il modello di gestione risorse hello più nuove distribuzioni.

> [!IMPORTANT]
> È ora possibile aggiornare i servizi archivi di Backup gli insiemi di credenziali tooRecovery. Per informazioni dettagliate, vedere l'articolo hello [aggiornare un tooa insieme di credenziali di Backup dell'insieme di credenziali di servizi di ripristino](backup-azure-upgrade-backup-to-recovery-services.md). Microsoft incoraggia gli utenti tooupgrade insiemi di credenziali di servizi tooRecovery insiemi di credenziali di Backup.<br/> Dopo 15 ottobre 2017, è possibile utilizzare gli insiemi di credenziali di PowerShell toocreate Backup. **Entro il 1° novembre 2017**:
>- Tutti gli archivi di Backup rimanenti verrà automaticamente aggiornato tooRecovery servizi insiemi di credenziali.
>- Si sarà in grado di tooaccess ai dati di backup nel portale classico hello. Utilizzare invece hello Azure tooaccess portale i dati di backup in insiemi di servizi di ripristino.
>

## <a name="management-portal-tasks"></a>Attività del portale di gestione
1. Accedi toohello [portale di gestione](https://manage.windowsazure.com).
2. Fare clic su **servizi di ripristino**, quindi fare clic su nome hello della pagina di avvio rapido dell'insieme di credenziali backup tooview hello.

    ![Servizi di ripristino](./media/backup-azure-manage-windows-server-classic/rs-left-nav.png)

Selezionando le opzioni di hello nella parte superiore di hello della pagina di avvio rapido di hello, è possibile visualizzare l'attività di gestione disponibili hello.

![Gestire le schede](./media/backup-azure-manage-windows-server-classic/qs-page.png)

### <a name="dashboard"></a>Dashboard
Selezionare **Dashboard** panoramica sull'utilizzo di hello toosee per server hello. Hello **panoramica sull'utilizzo** include:

* numero di Hello di Windows Server registrate toocloud
* numero di Hello macchine virtuali di Azure protette nel cloud
* Hello spazio di archiviazione totale utilizzato in Azure
* stato Hello di processi recenti

Nella parte inferiore di hello di hello Dashboard è possibile eseguire hello seguenti attività:

* **Gestisci certificato** : se un certificato server hello tooregister usato, quindi usare questo certificato hello tooupdate. Se si usano le credenziali di insieme, non usare la funzionalità **Gestisci certificato**.
* **Eliminare** -eliminazioni hello corrente backup dell'insieme di credenziali. Se non viene utilizzato un archivio di backup, è possibile eliminare toofree spazio di archiviazione. **Eliminare** è abilitata solo dopo aver eliminati tutti i server registrati dall'insieme di credenziali hello.

![Eseguire un backup delle attività del dashboard](./media/backup-azure-manage-windows-server-classic/dashboard-tasks.png)

## <a name="registered-items"></a>Elementi registrati
Selezionare **elementi registrati** tooview i nomi di hello del server hello che sono registrati toothis insieme di credenziali.

![Elementi registrati](./media/backup-azure-manage-windows-server-classic/registered-items.png)

Hello **tipo** filtro predefinito tooAzure macchina virtuale. Selezionare i nomi di hello tooview dei server hello di insieme di credenziali registrati toothis **Windows server** da hello menu a discesa.

Da qui è possibile eseguire hello seguenti attività:

* **Ripetere la registrazione** : quando questa opzione è selezionata per un server è possibile utilizzare hello **registrazione guidata** hello in Microsoft Azure Backup agent tooregister hello server locale insieme di credenziali di backup hello una seconda volta . Potrebbe essere necessario toore la registrazione a causa di errore tooan nel certificato hello oppure se un server di stato toobe ricompilato.
* **Eliminare** -Elimina un server dall'insieme di credenziali backup hello. Tutti i dati archiviato hello associati hello server vengono eliminati immediatamente.

    ![Attività di Elementi registrati](./media/backup-azure-manage-windows-server-classic/registered-items-tasks.png)

## <a name="protected-items"></a>Elementi protetti
Selezionare **elementi protetti** elementi hello tooview che sono stato eseguito il backup dai server hello.

![Elementi protetti](./media/backup-azure-manage-windows-server-classic/protected-items.png)

## <a name="configure"></a>Configurare
Da hello **configura** scheda è possibile selezionare l'opzione di ridondanza di archiviazione appropriato hello. Hello ora tooselect hello archiviazione ridondanza migliore è subito dopo la creazione di un insieme di credenziali e prima che tutti i computer siano registrati tooit.

> [!WARNING]
> Una volta un elemento dell'insieme di credenziali registrati toohello, opzione di ridondanza di archiviazione hello è bloccato e non può essere modificato.
>
>

![Configurare](./media/backup-azure-manage-windows-server-classic/configure.png)

Per altre informazioni sulla [ridondanza di archiviazione](../storage/common/storage-redundancy.md), vedere questo articolo.

## <a name="microsoft-azure-backup-agent-tasks"></a>Attività dell'agente Backup di Microsoft Azure
### <a name="console"></a>Console
Aprire hello **Microsoft Azure Backup agent** (sarà possibile trovarlo cercando il computer per *Backup di Microsoft Azure*).

![Agente di Backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)

Da hello **azioni** disponibile all'indirizzo hello destra della console di agente di backup hello è possibile eseguire hello seguenti attività di gestione:

* Registra server
* Pianificazione di un backup
* Esegui backup
* Modifica proprietà

![Azioni della console dell'agente](./media/backup-azure-manage-windows-server-classic/console-actions.png)

> [!NOTE]
> troppo**Ripristina dati**, vedere [ripristinare i file tooa Windows server o computer client Windows](backup-azure-restore-windows-server.md).
>
>

### <a name="modify-an-existing-backup"></a>Modificare un backup esistente
1. Nell'agente di Backup di Microsoft Azure hello fare clic su **pianifica Backup**.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
2. In hello **pianificazione guidata Backup** lasciare hello **apportare modifiche toobackup elementi o tempistica** opzione selezionata e fare clic su **Avanti**.

    ![Modificare un backup pianificato](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
3. Se si desidera tooadd o modificare gli elementi, di hello **selezionare elementi tooBackup** fare clic su schermo **Aggiungi elementi**.

    È inoltre possibile impostare **impostazioni di esclusione** da questa pagina nella creazione guidata hello. Se si desidera che il file tooexclude o procedura hello per l'aggiunta di leggere i tipi di file [impostazioni di esclusione](#exclusion-settings).
4. Selezionare il file hello e le cartelle desidera ripristinare tooback e fare clic su **OK**.

    ![Aggiungi elementi](./media/backup-azure-manage-windows-server-classic/add-items-modify.png)
5. Specificare hello **pianificazione del backup** e fare clic su **Avanti**.

    È possibile pianificare backup giornalieri (non più di 3 al giorno) o settimanali.

    ![Specificare la pianificazione dei backup](./media/backup-azure-manage-windows-server-classic/specify-backup-schedule-modify-close.png)

   > [!NOTE]
   > Specifica la pianificazione del backup hello è illustrata in dettaglio in questo [articolo](backup-azure-backup-cloud-as-tape.md).
   >
   >
6. Seleziona hello **criteri di conservazione** copia di backup hello e fare clic su **Avanti**.

    ![Selezionare i criteri di conservazione](./media/backup-azure-manage-windows-server-classic/select-retention-policy-modify.png)
7. In hello **conferma** schermata hello rivedere le informazioni e fare clic su **fine**.
8. Al termine della creazione di hello guidata hello **pianificazione del backup**, fare clic su **Chiudi**.

    Dopo la modifica della protezione, è possibile verificare che i backup attivano correttamente da passare toohello **processi** scheda e conferma che le modifiche vengono riflesse nel hello i processi di backup.

### <a name="enable-network-throttling"></a>Abilitare la limitazione della larghezza di banda della rete
l'agente Azure Backup Hello fornisce una scheda di limitazione delle richieste che consente di toocontrol modalità di utilizzo della larghezza di banda di rete durante il trasferimento dei dati. Questo controllo può essere utile se è necessario tooback dei dati durante le ore lavorative, ma non si desidera hello toointerfere di processo di backup con il traffico internet. La limitazione delle richieste di dati trasferimento applica tooback backup e ripristino.  

tooenable limitazione:

1. In hello **agente di Backup**, fare clic su **Modifica proprietà**.
2. Seleziona hello **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet** casella di controllo.

    ![Limitazione della larghezza di banda della rete](./media/backup-azure-manage-windows-server-classic/throttling-dialog.png)
3. Dopo aver abilitato la limitazione delle richieste, specificare hello consentito della larghezza di banda per trasferire i dati di backup durante **ore lavorative** e **ore Non lavorative**.

    i valori di larghezza di banda Hello iniziano da 512 kilobyte per secondo (Kbps) e possono aumentare fino a too1023 megabyte al secondo (Mbps). È anche possibile designare inizio hello e di fine per **ore lavorative**, e i giorni della settimana hello vengono considerati lavoro giorni. tempo di Hello di fuori di hello designato per le ore lavorative è ore non lavorative toobe considerate.
4. Fare clic su **OK**.

## <a name="exclusion-settings"></a>Impostazioni di esclusione
1. Aprire hello **Microsoft Azure Backup agent** (sarà possibile trovarlo cercando il computer per *Backup di Microsoft Azure*).

    ![Aprire l'agente di backup](./media/backup-azure-manage-windows-server-classic/snap-in-search.png)
2. Nell'agente di Backup di Microsoft Azure hello fare clic su **pianifica Backup**.

    ![Pianificare un backup di Windows Server](./media/backup-azure-manage-windows-server-classic/schedule-backup.png)
3. In Pianificazione guidata Backup hello lasciare hello **apportare modifiche toobackup elementi o tempistica** opzione selezionata e fare clic su **Avanti**.

    ![Modificare una pianificazione](./media/backup-azure-manage-windows-server-classic/modify-or-stop-a-scheduled-backup.png)
4. Fare clic su **Impostazioni di esclusione**.

    ![Selezionare gli elementi tooexclude](./media/backup-azure-manage-windows-server-classic/exclusion-settings.png)
5. Fare clic su **Aggiungi esclusione**.

    ![Aggiungere esclusioni](./media/backup-azure-manage-windows-server-classic/add-exclusion.png)
6. Selezionare il percorso di hello e quindi fare clic su **OK**.

    ![Selezionare una posizione per l'esclusione](./media/backup-azure-manage-windows-server-classic/exclusion-location.png)
7. Aggiungere l'estensione del file hello in hello **tipo di File** campo.

    ![Escludere per tipo di file](./media/backup-azure-manage-windows-server-classic/exclude-file-type.png)

    Aggiunta di un'estensione mp3

    ![Esempio di tipo di file](./media/backup-azure-manage-windows-server-classic/exclude-mp3.png)

    tooadd un'altra estensione, fare clic su **Aggiunta esclusione** e immettere un'altra estensione del tipo di file (aggiunta di un'estensione JPEG).

    ![Altro esempio di tipo di file](./media/backup-azure-manage-windows-server-classic/exclude-jpg.png)
8. Dopo aver aggiunto tutte le estensioni di hello, fare clic su **OK**.
9. Continuare il processo hello pianificazione guidata Backup fare clic su **Avanti** finché hello **pagina di conferma**, quindi fare clic su **fine**.

    ![Conferma dell'esclusione](./media/backup-azure-manage-windows-server-classic/finish-exclusions.png)

## <a name="next-steps"></a>Passaggi successivi
* [Ripristino di Windows Server o Windows Client da Azure](backup-azure-restore-windows-server.md)
* toolearn ulteriori informazioni sui Backup di Azure, vedere [Cenni preliminari su Backup di Azure](backup-introduction-to-azure-backup.md)
* Visitare hello [Forum di Azure Backup](http://go.microsoft.com/fwlink/p/?LinkId=290933)
