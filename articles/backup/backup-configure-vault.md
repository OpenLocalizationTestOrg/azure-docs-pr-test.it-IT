---
title: aaaUse Azure Backup agent tooback backup di file e cartelle | Documenti Microsoft
description: Utilizzare hello Microsoft Azure Backup agent tooback backup tooAzure file e cartelle di Windows. Creare un insieme di credenziali di servizi di ripristino, installare l'agente di Backup hello, definire i criteri di backup hello ed eseguire backup iniziale hello in cartelle e file hello.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: insieme di credenziali di backup; backup di un server Windows; backup di Windows;
ms.assetid: 7f5b1943-b3c1-4ddb-8fb7-3560533c68d5
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: be203c24841971872b5c6e7cf260a2fa5c58ac47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-windows-server-or-client-tooazure-using-hello-resource-manager-deployment-model"></a>Eseguire il backup di un tooAzure di Windows Server o client utilizzando hello modello di distribuzione di gestione risorse
> [!div class="op_single_selector"]
> * [Portale di Azure](backup-configure-vault.md)
> * [Portale classico](backup-configure-vault-classic.md)
>
>

Questo articolo spiega come tooAzure tooback backup del Server di Windows (o un client di Windows) di file e cartelle con Azure Backup tramite hello il modello di distribuzione di gestione risorse.

[!INCLUDE [learn-about-deployment-models](../../includes/backup-deployment-models.md)]

![Passaggi del processo di backup](./media/backup-configure-vault/initial-backup-process.png)

## <a name="before-you-start"></a>Prima di iniziare
tooback backup di un server o client tooAzure, è necessario un account di Azure. Se non si ha un account, è possibile crearne uno [gratuito](https://azure.microsoft.com/free/) in pochi minuti.

## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino
Un insieme di credenziali di servizi di ripristino è un'entità contenente tutti i backup di hello e i punti di ripristino creati nel corso del tempo. insieme di credenziali di servizi di ripristino Hello contiene inoltre hello applicato criteri di backup protetti toohello file e cartelle. Quando si crea un insieme di credenziali di servizi di ripristino, è necessario inoltre selezionare opzione di ridondanza di archiviazione appropriato hello.

### <a name="toocreate-a-recovery-services-vault"></a>toocreate un insieme di credenziali di servizi di ripristino
1. Se non già stato fatto, accedere toohello [portale Azure](https://portal.azure.com/) tramite la sottoscrizione di Azure.
2. Nel menu Hub hello, fare clic su **più servizi** e nell'elenco di hello delle risorse, digitare **servizi di ripristino** e fare clic su **insiemi di credenziali di servizi di ripristino**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 1](./media/backup-try-azure-backup-in-10-mins/open-rs-vault-list.png) <br/>

    Se sono presenti archivi di servizi di ripristino nella sottoscrizione hello, vengono elencati gli insiemi di credenziali di hello.

3. In hello **insiemi di credenziali di servizi di ripristino** menu, fare clic su **Aggiungi**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 2](./media/backup-try-azure-backup-in-10-mins/rs-vault-menu.png)

    Servizi di ripristino Hello insieme di credenziali si apre Pannello chiesto tooprovide un **nome**, **sottoscrizione**, **gruppo di risorse**, e **percorso**.

    ![Creare un insieme di credenziali dei servizi di ripristino - Passaggio 3](./media/backup-try-azure-backup-in-10-mins/rs-vault-step-3.png)

4. Per **nome**, immettere un insieme di credenziali di nome descrittivo tooidentify hello. nome di Hello deve toobe univoco per la sottoscrizione di Azure hello. Digitare un nome che contenga tra i 2 e i 50 caratteri. Deve iniziare con una lettera e può contenere solo lettere, numeri e trattini.

5. In hello **sottoscrizione** sezione, utilizzare hello toochoose di menu a discesa hello sottoscrizione di Azure. Se si utilizza una sola sottoscrizione, che viene visualizzato di sottoscrizione ed è possibile ignorare toohello successivo passaggio. Se non sei sicuro che toouse di sottoscrizione, utilizzare predefinito hello (o suggerito) sottoscrizione. Sono disponibili più scelte solo se l'account dell'organizzazione è associato a più sottoscrizioni di Azure.

6. In hello **gruppo di risorse** sezione:

    * Selezionare **Crea nuovo** se si desidera toocreate un nuovo gruppo di risorse.
    Or
    * Selezionare **utilizzare esistente** e fare clic su hello dal menu a discesa toosee hello disponibili elenco di gruppi di risorse.

  Per informazioni complete su gruppi di risorse, vedere hello [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).

7. Fare clic su **percorso** tooselect hello località geografica per l'insieme di credenziali hello. Questa opzione determina l'area geografica di hello in cui viene inviati ai dati di backup.

8. Nella parte inferiore di hello del pannello dell'insieme di credenziali di servizi di ripristino hello, fare clic su **crea**.

  Può richiedere alcuni minuti per hello che toobe creato insieme di credenziali di servizi di ripristino. Monitorare le notifiche di stato hello in area destra superiore hello del portale hello. Una volta creato l'insieme di credenziali, viene visualizzato nell'elenco hello degli insiemi di credenziali di servizi di ripristino. Se l'insieme di credenziali non viene visualizzato dopo qualche minuto, fare clic su **Aggiorna**.

  ![Fare clic sul pulsante Aggiorna](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

  Dopo aver visualizzato l'insieme di credenziali nell'elenco di hello degli insiemi di credenziali di servizi di ripristino, si è pronti tooset ridondanza dell'archiviazione hello.


### <a name="set-storage-redundancy"></a>Impostare la ridondanza di archiviazione
Quando si crea per la prima volta un insieme di credenziali di Servizi di ripristino, si determina come replicare lo spazio di archiviazione.

1. Da hello **insiemi di credenziali di servizi di ripristino** pannello, fare clic su nuovo insieme di credenziali hello.

    ![Selezionare nuovo insieme di credenziali hello hello elenco dell'insieme di credenziali di servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/rs-vault-list.png)

    Quando si seleziona l'insieme di credenziali hello, hello **insieme di credenziali di servizi di ripristino** consente di restringere blade e pannello impostazioni hello (*che ha il nome di hello dell'insieme di credenziali hello nella parte superiore di hello*) e pannello Dettagli insieme di credenziali hello aperto.

    ![Configurazione dell'archiviazione hello vista per nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration-2.png)

2. Nel pannello impostazioni di hello nuovo insieme di credenziali, utilizzare hello tooscroll di scorrimento verticale verso il basso toohello sezione gestione e fare clic su **infrastruttura Backup**.

  verrà visualizzata la finestra di blade Backup infrastruttura Hello.

3. Nel Pannello di hello infrastruttura di Backup, fare clic su **la configurazione del Backup** tooopen hello **la configurazione del Backup** blade.

  ![Set di configurazione dell'archiviazione hello per nuovo insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/set-storage-configuration.png)

4. Scegliere l'opzione di replica di archiviazione appropriato hello per l'insieme di credenziali.

  ![opzioni di configurazione dell'archiviazione](./media/backup-try-azure-backup-in-10-mins/choose-storage-configuration.png)

  Per impostazione predefinita, l'insieme di credenziali prevede l'archiviazione con ridondanza geografica. Se si usa Azure come un endpoint di archiviazione di backup primario, continuare toouse **con ridondanza geografica**. Se non si utilizza Azure come un endpoint di archiviazione di backup primario, quindi scegliere **ridondanza locale**, che consente di ridurre i costi di archiviazione di Azure hello. Per altre informazioni sulle opzioni di archiviazione [con ridondanza geografica](../storage/common/storage-redundancy.md#geo-redundant-storage) e [con ridondanza locale](../storage/common/storage-redundancy.md#locally-redundant-storage), vedere [Panoramica della ridondanza di archiviazione](../storage/common/storage-redundancy.md).

Dopo aver creato un insieme di credenziali, preparare l'infrastruttura tooback backup di file e cartelle dal download e installazione agente servizi di ripristino di Microsoft Azure hello, scaricare l'insieme di credenziali e quindi utilizzare tali credenziali tooregister hello agente insieme di credenziali Hello.

## <a name="configure-hello-vault"></a>Configurare l'insieme di credenziali hello

1. In hello pannello dell'insieme di credenziali di servizi di ripristino (per hello insieme di credenziali appena creato), nella sezione Guida introduttiva hello, fare clic su **Backup**, quindi su hello **Introduzione a Backup** pannello seleziona  **Obiettivo di backup**.

  ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

  Hello **Backup obiettivo** apre blade. Se hello insieme di credenziali di servizi di ripristino è stata configurata in precedenza, hello **Backup obiettivo** pannelli viene visualizzata quando si fa clic su **Backup** in servizi di ripristino hello credenziali blade.

  ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. Da hello **in cui viene eseguito il carico di lavoro?** menu a discesa, seleziona **locale**.

  Si sceglie **Locale** perché il server di Windows o il computer Windows è un computer fisico che non si trova in Azure.

3. Da hello **cosa si desidera toobackup?** dal menu **file e cartelle**, fare clic su **OK**.

  ![Configurazione di file e cartelle](./media/backup-try-azure-backup-in-10-mins/set-file-folder.png)

  Fare clic su OK, un segno di spunta accanto troppo**obiettivo Backup**, hello e **Prepare infrastruttura** apre blade.

  ![Preparare l'infrastruttura dopo aver configurato l'obiettivo del backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-configed.png)

4. In hello **Prepare infrastruttura** pannello, fare clic su **Scarica agente per Windows Server o Client Windows**.

  ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/choose-agent-for-server-client.png)

  Se si utilizza Windows Server essenziali, quindi scegliere agente hello toodownload per Windows Server essenziali. Un menu a comparsa chiede toorun o salvare MARSAgentInstaller.exe.

  ![Finestra di dialogo di MARSAgentInstaller](./media/backup-try-azure-backup-in-10-mins/mars-installer-run-save.png)

5. Nel menu a comparsa download hello, fare clic su **salvare**.

  Per impostazione predefinita, hello **MARSagentinstaller.exe** tooyour cartella di download viene salvato. Al termine dell'installazione guidata di hello, verrà visualizzato un messaggio popup che chiede se si desidera che il programma di installazione di toorun hello o aprire la cartella hello.

  ![Preparare l'infrastruttura](./media/backup-try-azure-backup-in-10-mins/mars-installer-complete.png)

  È necessario ancora agente hello tooinstall. È possibile installare l'agente di hello dopo avere scaricato l'insieme di credenziali hello.

6. In hello **Prepare infrastruttura** pannello, fare clic su **scaricare**.

  ![Scaricare le credenziali dell'insieme di credenziali](./media/backup-try-azure-backup-in-10-mins/download-vault-credentials.png)

  insieme di credenziali Hello scaricare tooyour cartella di download. Dopo l'insieme di credenziali hello completare il download, vengono visualizzati una finestra popup che chiede se si desidera tooopen o salvare le credenziali di hello. Fare clic su **Salva**. Se si sceglie accidentalmente **aprire**, consentono di finestra di dialogo hello tenta tooopen hello insieme di credenziali, l'esito negativo. È possibile aprire l'insieme di credenziali hello. Passaggio successivo toohello di procedere. insieme di credenziali Hello sono nella cartella di download di hello.   

  ![Il download delle credenziali dell'insieme di credenziali è terminato](./media/backup-try-azure-backup-in-10-mins/vault-credentials-downloaded.png)

## <a name="install-and-register-hello-agent"></a>Installare e registrare agente hello

> [!NOTE]
> Non è ancora disponibile, l'abilitazione backup tramite il portale di Azure hello. Utilizzare hello tooback di agente servizi di ripristino di Microsoft Azure backup di file e cartelle.
>

1. Individuare e fare doppio clic su hello **MARSagentinstaller.exe** dalla cartella download di hello (o altro percorso di salvataggio).

  programma di installazione Hello fornisce una serie di messaggi durante l'estrazione, installa e registra l'agente di servizi di ripristino hello.

  ![Eseguire il programma di installazione dell'agente di Servizi di ripristino](./media/backup-try-azure-backup-in-10-mins/mars-installer-registration.png)

2. Completare l'installazione guidata di Microsoft Azure Recovery Services Agent hello. procedura guidata hello toocomplete, è necessario:

  * Scegliere il percorso della cartella di installazione e la cache di hello.
  * Fornire il proprio proxy informazioni sul server se si utilizza un toohello tooconnect di server proxy internet.
  * Se si usa un proxy autenticato, immettere il nome utente e la password.
  * Fornire le credenziali dell'insieme di credenziali scaricato hello
  * Salvare la passphrase di crittografia hello in un luogo sicuro.

  > [!NOTE]
  > Se si perde o dimentica passphrase hello, Microsoft non consente di ripristinare i dati di backup hello. Salvare il file hello in un luogo sicuro. È necessario toorestore una copia di backup.
  >
  >

agente Hello è ora installato e il computer è registrato toohello insieme di credenziali. È possibile tooconfigure e pianificare il backup.

## <a name="network-and-connectivity-requirements"></a>Requisiti di rete e connettività

Se il computer/proxy ha limitato l'accesso a internet, assicurarsi che le impostazioni del firewall nel computer di hello/proxy siano configurati tooallow hello URL seguenti: <br>
    1. www.msftncsi.com
    2. *.Microsoft.com
    3. windowsazure.com
    4. *.microsoftonline.com
    5. *. windows.ne


## <a name="create-hello-backup-policy"></a>Creare criteri di backup hello
criterio di backup Hello è pianificazione hello quando i punti di ripristino vengono eseguiti e hello periodo di tempo sono mantenuti i punti di ripristino hello. Usare hello Microsoft Azure Backup agent toocreate hello criterio di backup di file e cartelle.

### <a name="toocreate-a-backup-schedule"></a>toocreate una pianificazione di backup
1. Aprire l'agente di Backup di Microsoft Azure hello. È possibile trovarlo se si cerca **Backup di Microsoft Azure**nel computer.

    ![Avviare l'agente Azure Backup hello](./media/backup-configure-vault/snap-in-search.png)
2. Nell'agente hello Backup **azioni** riquadro, fare clic su **pianifica Backup** toolaunch hello pianificazione guidata Backup.

    ![Pianificare un backup di Windows Server](./media/backup-configure-vault/schedule-first-backup.png)

3. In hello **Introduzione** di hello pianificazione guidata Backup fare clic su **Avanti**.
4. In hello **selezionare elementi tooBackup** pagina, fare clic su **Aggiungi elementi**.

  verrà visualizzata la finestra di dialogo Seleziona elementi Hello.

5. Selezionare il file hello e le cartelle che desidera tooprotect e quindi fare clic su **OK**.
6. In hello **selezionare elementi tooBackup** pagina, fare clic su **Avanti**.
7. In hello **specificare pianificazione Backup** specificare pianificazione backup hello e fare clic su **Avanti**.

    È possibile pianificare backup giornalieri, da eseguire non più di tre volte al giorno, o settimanali.

    ![Elementi per il backup di Windows Server](./media/backup-configure-vault/specify-backup-schedule-close.png)

   > [!NOTE]
   > Per ulteriori informazioni su come toospecify hello pianificazione del backup, vedere l'articolo hello [tooreplace utilizzare Azure Backup infrastruttura nastro](backup-azure-backup-cloud-as-tape.md).
   >
   >

8. In hello **selezionare criteri di conservazione** pagina, scegliere hello di criteri di memorizzazione specifico hello hello copia di backup e fare clic su **Avanti**.

    criteri di conservazione Hello specificano durata hello viene archiviato il backup di hello. Anziché specificare solo un criterio"semplice" per tutti i punti di backup, è possibile specificare i criteri di conservazione diversi in base a quando viene eseguito il backup di hello. È possibile modificare toomeet criteri di conservazione giornaliero, settimanale, mensile e annuale hello le proprie esigenze.
9. Nella pagina tipo di Backup iniziale scegliere hello, scegliere il tipo di backup iniziale di hello. Lasciare l'opzione hello **automaticamente tramite rete hello** selezionata e quindi fare clic su **Avanti**.

    È possibile eseguire il backup automaticamente tramite rete hello oppure è possibile eseguire il backup non in linea. resto Hello di questo articolo descrive il processo di hello per il backup automaticamente. Se si preferisce toodo un backup offline, vedere l'articolo di hello [Offline backup flusso di lavoro in Backup di Azure](backup-azure-backup-import-export.md) per ulteriori informazioni.
10. Nella pagina di conferma hello, esaminare le informazioni di hello e quindi fare clic su **fine**.
11. Al termine la procedura guidata hello creazione pianificazione backup hello, fare clic su **Chiudi**.

### <a name="enable-network-throttling"></a>Abilitare la limitazione della larghezza di banda
agente di Backup di Microsoft Azure Hello fornisce la limitazione delle richieste di rete. La limitazione controlla l'uso della larghezza di banda della rete durante il trasferimento dati. Questo controllo può essere utile se è necessario tooback dei dati durante le ore lavorative, ma non si desidera hello toointerfere di processo di backup con il traffico Internet. La limitazione si applica tooback backup e ripristino.

> [!NOTE]
> La limitazione di rete non è disponibile su Windows Server 2008 R2 SP1, Windows Server 2008 SP2 o Windows 7 (con i pacchetti di servizio). rete di Backup di Azure Hello limitazione funzionalità coinvolge Quality of Service (QoS) nel sistema operativo locale hello. Se il Backup di Azure per poter proteggere questi sistemi operativi, versione di hello QoS disponibile in queste piattaforme non funziona con la limitazione della rete di Backup di Azure. La limitazione di rete può essere utilizzata in tutti gli altri [sistemi operativi supportati](backup-azure-backup-faq.md).
>
>

**la limitazione delle richieste di rete tooenable**

1. Nell'agente di Backup di Microsoft Azure hello, fare clic su **Modifica proprietà**.

    ![Modifica proprietà](./media/backup-configure-vault/change-properties.png)
2. In hello **limitazione** scheda, seleziona hello **abilitare la limitazione per le operazioni di backup all'utilizzo della larghezza di banda di internet** casella di controllo.

    ![Limitazione della larghezza di banda della rete](./media/backup-configure-vault/throttling-dialog.png)
3. Dopo avere abilitato la limitazione delle richieste, specificare hello consentito della larghezza di banda per trasferire i dati di backup durante **ore lavorative** e **ore Non lavorative**.

    i valori di larghezza di banda Hello iniziano 512 kilobit al secondo (Kbps) e possono aumentare fino a too1, 023 megabyte al secondo (MBps). È anche possibile designare inizio hello e di fine per **ore lavorative**, e i giorni della settimana hello sono considerate giorni. Gli orari al di fuori delle ore lavorative definite vengono considerati ore non lavorative.
4. Fare clic su **OK**.

### <a name="tooback-up-files-and-folders-for-hello-first-time"></a>tooback backup di file e cartelle per la prima volta hello
1. Nell'agente di backup hello, fare clic su **Effettua backup** hello toocomplete iniziale tramite rete hello il seeding.

    ![Eseguire ora il backup di Windows Server](./media/backup-configure-vault/backup-now.png)
2. Nella pagina di conferma hello, rivedere le impostazioni di hello che hello backup guidato immediato utilizzerà tooback macchina hello. Fare clic su **Backup**.
3. Fare clic su **Chiudi** guidata hello tooclose. Se si esegue questa operazione prima al termine del processo di backup hello, toorun guidata hello continua in background hello.

Al termine dell'operazione backup iniziale hello, hello **processo completato** stato viene visualizzato nella console Backup hello.

![Completamento infrarossi](./media/backup-configure-vault/ircomplete.png)

## <a name="questions"></a>Domande?
Se si hanno domande o se è presente una funzionalità che si desidera toosee incluso, [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sul backup di macchine virtuali o altri carichi di lavoro, vedere:

* Ora che si è eseguito il backup dei file e delle cartelle, è possibile [gestire l'insieme di credenziali e i server](backup-azure-manage-windows-server.md).
* Se è necessario toorestore una copia di backup, utilizzare anche in questo articolo[ripristinare i file tooa Windows macchina](backup-azure-restore-windows-server.md).
