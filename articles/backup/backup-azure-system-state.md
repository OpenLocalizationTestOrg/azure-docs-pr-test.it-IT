---
title: aaaBack backup tooAzure lo stato del sistema di Windows | Documenti Microsoft
description: Informazioni su tooback backup dello stato del sistema di Windows Server e/o tooAzure computer Windows hello.
services: backup
documentationcenter: 
author: saurabhsensharma
manager: carmonm
editor: 
keywords: "modalità toobackup; modalità tooback; backup di file e cartelle"
ms.assetid: 5b15ebf1-2214-4722-b937-96e2be8872bb
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: saurse;markgal
ms.openlocfilehash: be5d4be81af981c10de82add9fe962a730753cf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-windows-system-state-in-resource-manager-deployment"></a>Eseguire il backup dello stato del sistema Windows in una distribuzione Resource Manager
Questo articolo illustra la modalità di stato tooAzure tooback il sistema di Windows Server. Si tratta di un'esercitazione toowalk previsto di nozioni di base hello.

Se si desidera tooknow ulteriori informazioni su Backup di Azure, leggere questo [Panoramica](backup-introduction-to-azure-backup.md).

Se non è disponibile una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/) che consente di accedere a qualsiasi servizio di Azure.

## <a name="create-a-recovery-services-vault"></a>Creare un insieme di credenziali di Servizi di ripristino
tooback backup di file e cartelle, è necessario un insieme di credenziali di servizi di ripristino nell'area di hello in cui si desidera dati hello toostore toocreate. È inoltre necessario toodetermine la modalità di archiviazione replicata.

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

    * Selezionare **Crea nuovo** se si desidera toocreate un gruppo di risorse.
    Or
    * Selezionare **utilizzare esistente** e fare clic su hello dal menu a discesa toosee hello disponibili elenco di gruppi di risorse.

  Per informazioni complete su gruppi di risorse, vedere hello [Panoramica di gestione risorse di Azure](../azure-resource-manager/resource-group-overview.md).

7. Fare clic su **percorso** tooselect hello località geografica per l'insieme di credenziali hello. Questa opzione determina l'area geografica di hello in cui viene inviati ai dati di backup.

8. Nella parte inferiore di hello del pannello dell'insieme di credenziali di servizi di ripristino hello, fare clic su **crea**.

    Può richiedere alcuni minuti per hello che toobe creato insieme di credenziali di servizi di ripristino. Monitorare le notifiche di stato hello in area destra superiore hello del portale hello. Una volta creato l'insieme di credenziali, viene visualizzato nell'elenco hello degli insiemi di credenziali di servizi di ripristino. Se l'insieme di credenziali non viene visualizzato dopo qualche minuto, fare clic su **Aggiorna**.

    ![Fare clic sul pulsante Aggiorna](./media/backup-try-azure-backup-in-10-mins/refresh-button.png)</br>

    Dopo aver visualizzato l'insieme di credenziali nell'elenco di hello degli insiemi di credenziali di servizi di ripristino, si è pronti tooset ridondanza dell'archiviazione hello.

### <a name="set-storage-redundancy-for-hello-vault"></a>Impostare la ridondanza di archiviazione per l'insieme di credenziali hello
Quando si crea un insieme di credenziali di servizi di ripristino, verificare che la ridondanza dell'archiviazione è configurata hello desiderato.

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

Dopo aver creato un insieme di credenziali, configurarlo per il backup dello stato del sistema Windows.

## <a name="configure-hello-vault"></a>Configurare l'insieme di credenziali hello
1. In hello pannello dell'insieme di credenziali di servizi di ripristino (per hello insieme di credenziali appena creato), nella sezione Guida introduttiva hello, fare clic su **Backup**, quindi su hello **Introduzione a Backup** pannello seleziona  **Obiettivo di backup**.

    ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/open-backup-settings.png)

    Hello **Backup obiettivo** apre blade.

    ![Aprire il Pannello Obiettivo di backup](./media/backup-try-azure-backup-in-10-mins/backup-goal-blade.png)

2. Da hello **in cui viene eseguito il carico di lavoro?** menu a discesa, seleziona **locale**.

    Si sceglie **Locale** perché il server di Windows o il computer Windows è un computer fisico che non si trova in Azure.

3. Da hello **cosa si desidera toobackup?** dal menu **dello stato del sistema**, fare clic su **OK**.

    ![Configurazione di file e cartelle](./media/backup-azure-system-state/backup-goal-system-state.png)

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
> Non è ancora disponibile, l'abilitazione backup tramite il portale di Azure hello. Utilizzare hello tooback di agente servizi di ripristino di Microsoft Azure backup dello stato di sistema di Windows Server.
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

## <a name="back-up-windows-server-system-state-preview"></a>Eseguire il backup dello stato del sistema Windows Server (anteprima)
backup iniziale Hello include tre attività:

* Abilitare i Backup dello stato del sistema tramite hello Azure Backup agent
* Pianifica backup hello
* Eseguire il backup di file e cartelle per hello prima volta

toocomplete hello primo backup, agente di servizi di ripristino di Microsoft Azure Usa hello.

### <a name="tooenable-system-state-backup-using-hello-azure-backup-agent"></a>backup dello stato del sistema tooenable utilizzando hello Azure Backup agent

1. In una sessione di PowerShell, eseguire hello seguente motore di comando toostop hello Azure Backup.

  ```
  PS C:\> Net stop obengine
  ```

2. Aprire hello del Registro di sistema di Windows.

  ```
  PS C:\> regedit.exe
  ```

3. Aggiungere la seguente chiave del Registro di sistema con hello hello specificato valore DWord.

  | Percorso del Registro | Chiave del Registro di sistema | Valore DWORD |
  |---------------|--------------|-------------|
  | HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | TurnOffSSBFeature | 2 |

4. Riavviare il motore di Backup hello eseguendo hello seguente comando in un prompt dei comandi con privilegi elevati.

  ```
  PS C:\> Net start obengine
  ```

### <a name="tooschedule-hello-backup-job"></a>processo di backup hello tooschedule

1. Aprire l'agente di servizi di ripristino di Microsoft Azure hello. È possibile trovarlo se si cerca **Backup di Microsoft Azure**nel computer.

    ![Avviare l'agente di servizi di ripristino di Azure hello](./media/backup-try-azure-backup-in-10-mins/snap-in-search.png)

2. Nell'agente di servizi di ripristino hello, fare clic su **pianifica Backup**.

    ![Pianificare un backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/schedule-first-backup.png)

3. Pagina di pianificazione guidata Backup hello introduzione su hello, fare clic su **Avanti**.

4. Nella pagina di tooBackup selezionare elementi hello, fare clic su **Aggiungi elementi**.

5. Selezionare **Stato del sistema** e quindi fare clic su **OK**.

6. Fare clic su **Avanti**.

7. Hello pianificazione di Backup dello stato del sistema e alla conservazione dei verrà automaticamente impostata tooback backup ogni domenica ora locale 9:00 PM, e il periodo di conservazione hello è too60 giorni.

   > [!NOTE]
   > I criteri di backup e di conservazione dello stato del sistema vengono configurati automaticamente. Se si esegue il backup di file e cartelle inoltre toohello dello stato del sistema Windows Server, specificare solo hello Backup e criteri di memorizzazione per i backup di file dalla procedura guidata hello. 
   >

8. Nella pagina di conferma hello, esaminare le informazioni di hello e quindi fare clic su **fine**.

9. Al termine la procedura guidata hello creazione pianificazione backup hello, fare clic su **Chiudi**.

### <a name="tooback-up-windows-server-system-state-for-hello-first-time"></a>tooback backup dello stato di sistema di Windows Server per la prima volta hello

1. Verificare che non siano presenti aggiornamenti in sospeso di Windows Server che richiedono un riavvio.

2. Nell'agente di servizi di ripristino hello, fare clic su **Effettua backup** hello toocomplete iniziale tramite rete hello il seeding.

    ![Eseguire ora il backup di Windows Server](./media/backup-try-azure-backup-in-10-mins/backup-now.png)

3. Nella pagina di conferma hello, rivedere le impostazioni di hello che hello backup guidato immediato utilizzerà tooback macchina hello. Fare clic su **Backup**.

4. Fare clic su **Chiudi** guidata hello tooclose. Se si chiude la procedura guidata hello prima al termine del processo di backup hello, toorun guidata hello continua in background hello.

5. Se si esegue il backup di file e cartelle sul server, inoltre toohello dello stato del sistema Server Windows, hello Esegui Backup verrà solo eseguito il backup dei file. uno stato di sistema ad hoc tooperform eseguire il backup, usare hello comando PowerShell seguente:

    ```
    PS C:\> Start-OBSystemStateBackup
    ```

  Al termine dell'operazione backup iniziale hello, hello **processo completato** stato viene visualizzato nella console Backup hello.

  ![Completamento infrarossi](./media/backup-try-azure-backup-in-10-mins/ircomplete.png)

## <a name="frequently-asked-questions"></a>Domande frequenti

Hello domande e risposte seguenti forniscono informazioni supplementari.

### <a name="what-is-hello-staging-volume"></a>Che cos'è il Volume di gestione temporanea hello?

Volume di gestione temporanea Hello rappresenta posizione intermedia di hello in hello disponibile in modo nativo, Windows Server Backup fasi hello Backup dello stato del sistema. Agente di Backup di Azure quindi comprime e crittografa il backup intermedio e invia che tramite toohello il protocollo HTTPS protetta configurato l'insieme di credenziali di servizi di ripristino. **È consigliabile che stabilire hello Volume di gestione temporanea in un volume di sistema operativo Windows. Se si osservano problemi con i backup dello stato di sistema, la verifica percorso hello del Volume di gestione temporanea è hello primo passaggio di risoluzione dei problemi.** 

### <a name="how-can-i-change-hello-staging-volume-path-specified-in-hello-azure-backup-agent"></a>Come è possibile modificare hello percorso del Volume di gestione temporanea specificata nell'agente di Backup di Azure hello?

Per impostazione predefinita, Hello Volume di gestione temporanea si trova nella cartella della cache di hello. 

1. toochange questo percorso, utilizzare hello comando (in un prompt dei comandi con privilegi elevati) seguente:
  ```
  PS C:\> Net stop obengine
  ```

2. Aggiornare quindi hello seguenti voci del registro con hello percorso toohello nuova Volume di gestione temporanea.

  |Percorso del Registro|Chiave del Registro di sistema|Valore|
  |-------------|------------|-----|
  |HKEY_LOCAL_MACHINE\Software\Microsoft\Windows Azure Backup\Config\CloudBackupProvider | SSBStagingPath | Nuovo percorso del volume di staging |

Hello percorso gestione temporanea viene fatta distinzione tra maiuscole e minuscole e deve essere hello esatta stesso maiuscole e minuscole come ciò che esiste nel server di hello. 

3. Dopo aver modificato percorso del volume di gestione temporanea hello, riavviare il motore di Backup hello:
  ```
  PS C:\> Net start obengine
  ```
4. toopick percorso hello modificato, agente di servizi di ripristino di Microsoft Azure aprire hello e trigger di un backup dello stato del sistema ad hoc.

### <a name="why-is-hello-system-state-default-retention-set-too60-days"></a>Motivo per cui è stato del sistema hello periodo di memorizzazione predefinito impostato too60 giorni?

ciclo di vita utile Hello di un backup dello stato del sistema è hello stesso come impostazione di hello "tombstone lifetime" per il ruolo di Windows Server Active Directory hello. il valore predefinito Hello per la voce di durata oggetto contrassegnato per rimozione hello è 60 giorni. Questo valore può essere impostato sull'oggetto di configurazione del servizio Directory (NTDS) hello.

### <a name="how-do-i-change-hello-default-backup-and-retention-policy-for-system-state"></a>Come modificare predefinito hello Backup e criteri di conservazione per lo stato del sistema?

valore predefinito di hello toochange Backup e criteri di conservazione per lo stato del sistema:
1. Arrestare il motore di Backup hello. Eseguire hello comando seguente da un prompt dei comandi con privilegi elevati.

  ```
  PS C:\> Net stop obengine
  ```

2. Aggiungere o aggiornare hello seguenti voci chiave del Registro di sistema HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows Backup\Config\CloudBackupProvider di Azure.

  |Nome nel Registro di sistema|Descrizione|Valore|
  |-------------|-----------|-----|
  |SSBScheduleTime|Tooconfigure usato hello ora del backup hello. L'impostazione predefinita sono le 21 ora locale.|DWORD: formato HHMM (numero decimale), ad esempio 2130 per le 21:30 ora locale|
  |SSBScheduleDays|Giorni di hello tooconfigure utilizzato quando i Backup dello stato del sistema deve essere eseguito a hello specificati ora. Singole cifre specificano i giorni della settimana hello. 0 rappresenta domenica, 1 lunedì e così via. Il giorno predefinito per il backup è domenica.|DWord: giorni di backup di toorun settimana hello (decimale), ad esempio 1230 pianifica backup su lunedì, martedì, mercoledì e domenica.|
  |SSBRetentionDays|Backup di tooretain giorni hello tooconfigure utilizzato. Il valore predefinito è 60. Il massimo consentito è 180.|DWord: Backup di tooretain giorni (decimale).|

3. Modulo di backup hello toorestart comando che segue hello di utilizzo.
    ```
    PS C:\> Net start obengine
    ```

4. Aprire l'agente di servizi di ripristino di Microsoft hello.

5. Fare clic su **pianifica Backup** e quindi fare clic su **Avanti** fino a visualizzare modifiche hello.

6. Fare clic su **fine** modifiche hello tooapply.


## <a name="questions"></a>Domande?
Se si hanno domande o se è presente una funzionalità che si desidera toosee incluso, [inviare commenti e suggerimenti](http://aka.ms/azurebackup_feedback).

## <a name="next-steps"></a>Passaggi successivi
* Sono disponibili altre informazioni sul [backup di computer Windows](backup-configure-vault.md).
* Ora che si è eseguito il backup dei file e delle cartelle, è possibile [gestire l'insieme di credenziali e i server](backup-azure-manage-windows-server.md).
* Se è necessario toorestore una copia di backup, utilizzare anche in questo articolo[ripristinare i file tooa Windows macchina](backup-azure-restore-windows-server.md).
