---
title: aaaBack dei server VMware con Server di Backup di Azure | Documenti Microsoft
description: Utilizzare Server di Backup di Azure tooback backup un disco o VMware server vCenter/ESXi tooAzure. Questo articolo offre istruzioni dettagliate per il backup o la protezione dei carichi di lavoro VMware.
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
ms.assetid: 6b131caf-de85-4eba-b8e6-d8a04545cd9d
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 07/24/2017
ms.author: markgal;
ms.openlocfilehash: 3edb6880a526ed0b18605fee0fac27196a608e7a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-a-vmware-server-tooazure"></a>Eseguire il backup di un tooAzure server VMware

Questo articolo viene illustrato come proteggere i carichi di lavoro server VMware tooconfigure toohelp di Server di Backup di Azure. In questo articolo si presuppone che sia stato già installato il server di Backup di Azure. Se non è installato Azure Backup Server, vedere [preparare tooback dei carichi di lavoro tramite il Server di Backup di Azure](backup-azure-microsoft-azure-backup.md).

Il server di Backup di Azure può eseguire il backup o assicurare la protezione di server VMware vCenter versione 6.5, 6.0 e 5.5.


## <a name="create-a-secure-connection-toohello-vcenter-server"></a>Creare una connessione sicura toohello vCenter Server

Per impostazione predefinita, il server di Backup di Azure comunica con ognuno dei server vCenter tramite un canale HTTPS. tooturn sulla comunicazione sicura hello, è consigliabile installare hello VMware autorità di certificazione certificato nel Server di Backup di Azure. Se si non richieda una comunicazione protetta e si preferisce requisito di toodisable hello HTTPS, vedere [protocollo di comunicazione protetta Disable](backup-azure-backup-server-vmware.md#disable-secure-communication-protocol). toocreate una connessione sicura tra il Server di Backup di Azure e hello vCenter Server, importarlo hello attendibile nel Server di Backup di Azure.

In genere, si utilizza un browser hello Azure Backup Server macchina tooconnect toohello Server vCenter tramite vSphere hello Client Web. Hello prima volta che si utilizza hello Azure Backup Server browser tooconnect toohello vCenter Server, hello connessione non protetta. Hello seguente immagine Mostra connessione hello non protetta.

![Esempio di connessione non protetta tooVMware server](./media/backup-azure-backup-server-vmware/unsecure-url.png)

toofix questo problema, creare una connessione sicura e scaricare i certificati CA radice attendibile hello.

1. Nel browser hello nel Server di Backup di Azure, immettere hello URL toohello vSphere Client Web. verrà visualizzata la pagina di accesso di Hello vSphere Client Web.

    ![Client Web vSphere](./media/backup-azure-backup-server-vmware/vsphere-web-client.png)

    Nella parte inferiore di hello informazioni hello ad amministratori e sviluppatori, individuare hello **Download attendibili i certificati CA radice** collegamento.

    ![Certificati CA radice attendibile hello toodownload di collegamento](./media/backup-azure-backup-server-vmware/vmware-download-ca-cert-prompt.png)

  Se non viene visualizzato nella pagina account di accesso Client di Web vSphere hello, controllare le impostazioni proxy del browser.

2. Fare clic su **Scarica certificati CA radice attendibili**.

    Server vCenter Hello scarica un computer locale tooyour di file. Hello nome del file è denominato **scaricare**. A seconda del browser, viene visualizzato un messaggio che chiede se tooopen o salvare il file hello.

    ![messaggio di download quando vengono scaricati i certificati](./media/backup-azure-backup-server-vmware/download-certs.png)

3. Hello file tooa percorso di salvataggio nel Server di Backup di Azure. Quando si salva il file hello, aggiungere l'estensione di file con estensione zip hello.

    file Hello è un file con estensione zip che contiene informazioni di hello sui certificati hello. Con estensione zip hello, è possibile utilizzare gli strumenti di estrazione hello.

4. Fare doppio clic su **download.zip**, quindi selezionare **Estrai tutto** contenuto hello tooextract.

    file con estensione zip Hello estrae il relativo contenuto tooa cartella **certificati**. Due tipi di file vengono visualizzati nella cartella certificati hello. file del certificato radice Hello ha un'estensione che inizia con una sequenza numerata come,0 e. 1.
    
    file CRL Hello ha un'estensione che inizia con una sequenza come .r0 o .r1. file CRL Hello è associata a un certificato.

    ![File di download estratto localmente ](./media/backup-azure-backup-server-vmware/extracted-files-in-certs-folder.png)

5. In hello **certificati** cartella, fare clic sul file di certificato radice hello e quindi fare clic su **rinominare**.

    ![Ridenominazione del certificato radice ](./media/backup-azure-backup-server-vmware/rename-cert.png)

    Modifica estensione too.crt del certificato radice hello. Quando viene richiesto se si è certi che si desidera toochange hello estensione, fare clic su **Sì** o **OK**. In caso contrario, modificare la funzione prevista del file hello. icona di Hello per hello file modifiche tooan icona rappresenta un certificato radice.

6. Fare doppio clic su certificato radice hello e scegliere dal menu a comparsa hello **Installa certificato**.

    Hello **importazione guidata certificati** viene visualizzata la finestra di dialogo.

7. In hello **importazione guidata certificati** nella finestra di dialogo **computer locale** come destinazione di hello per hello certificato e quindi fare clic su **Avanti** toocontinue.

    ![Opzioni di destinazione di archiviazione del certificato ](./media/backup-azure-backup-server-vmware/certificate-import-wizard1.png)

    Se viene chiesto se si desidera di tooallow modifiche toohello computer, fare clic su **Sì** o **OK**, le modifiche di hello tooall.

8. In hello **archivio certificati** selezionare **colloca tutti i certificati nel seguente archivio hello**, quindi fare clic su **Sfoglia** archivio certificati di hello toochoose.

    ![Inserire i certificati in un punto di archiviazione specifico](./media/backup-azure-backup-server-vmware/cert-import-wizard-local-store.png)

    Hello **Selezione archivio certificati** viene visualizzata la finestra di dialogo.

    ![Gerarchia di cartelle di archiviazione di certificati](./media/backup-azure-backup-server-vmware/cert-store.png)

9. Selezionare **autorità di certificazione radice attendibili** come cartella di destinazione hello per certificati hello e quindi fare clic su **OK**.

    ![Cartella di destinazione dei certificati](./media/backup-azure-backup-server-vmware/certificate-store-selected.png)

    Hello **autorità di certificazione radice attendibili** cartella viene confermata come archivio di certificati hello. Fare clic su **Avanti**.

    ![Cartella archivio certificati](./media/backup-azure-backup-server-vmware/certificate-import-wizard2.png)

10. In hello **hello Completamento importazione guidata certificati** pagina, verificare che il certificato hello nella cartella desiderata hello e quindi fare clic su **fine**.

    ![Verificare i certificati si trova nella cartella corretta di hello](./media/backup-azure-backup-server-vmware/cert-wizard-final-screen.png)

    Viene visualizzata una finestra di dialogo, viene confermata l'importazione del certificato ha esito positivo hello.

11. Accedi toohello vCenter Server tooconfirm che la connessione è protetta.

  Importazione certificati hello non ha esito positivo, se non è possibile stabilire una connessione sicura, consultare la documentazione di vSphere VMware hello in [richiesta di certificati server](http://pubs.vmware.com/vsphere-60/index.jsp#com.vmware.wssdk.dsg.doc/sdk_sg_server_certificate_Appendixes.6.4.html).

  Se si hanno limiti protetti all'interno dell'organizzazione e non desidera tooturn su hello il protocollo HTTPS, è possibile utilizzare hello seguendo procedure toodisable hello proteggere le comunicazioni.

### <a name="disable-secure-communication-protocol"></a>Disabilitazione del protocollo di comunicazione sicura

Se l'organizzazione non richiede il protocollo HTTPS hello, utilizzare hello seguendo i passaggi toodisable HTTPS. toodisable hello comportamento predefinito, creare una chiave del Registro di sistema che ignora il comportamento predefinito di hello.

1. Copiare e incollare hello dopo il testo in un file con estensione txt.

  ```
  Windows Registry Editor Version 5.00
  [HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Data Protection Manager\VMWare]
  "IgnoreCertificateValidation"=dword:00000001
  ```

2. Salvare i computer del Server di Backup di Azure tooyour file hello. Utilizzare DisableSecureAuthentication.reg per nome file hello.

3. Fare doppio clic sulla voce del Registro di sistema hello tooactivate file hello.


## <a name="create-a-role-and-user-account-on-hello-vcenter-server"></a>Creare un account utente e ruoli Server vCenter hello

Hello vCenter Server, un ruolo è un set predefinito di privilegi. Un amministratore del Server vCenter Crea ruoli hello. autorizzazioni tooassign, amministratore hello coppie gli account utente con un ruolo. tooestablish hello utente necessari credenziali tooback dei computer del Server vCenter hello, creare un ruolo con privilegi specifici e quindi associare account utente di hello hello ruolo.

Server di Backup di Azure Usa tooauthenticate un nome utente e password con hello vCenter Server. Il server di Backup di Azure sfrutta tali credenziali come autenticazione per ogni operazione di backup.

tooadd un ruolo del Server vCenter e i relativi privilegi di amministratore di backup:

1. Eseguire l'accesso in toohello vCenter Server e quindi nel Server vCenter hello **Navigator** pannello, fare clic su **amministrazione**.

    ![Opzione Administration (Amministrazione) nel pannello Navigator (Strumento di navigazione) del server vCenter](./media/backup-azure-backup-server-vmware/vmware-navigator-panel.png)

2. In **amministrazione** selezionare **ruoli**e quindi in hello **ruoli** fare clic su Pannello hello aggiungere l'icona del ruolo (simbolo + hello).

    ![Aggiungi ruolo](./media/backup-azure-backup-server-vmware/vmware-define-new-role.png)

    Hello **Create Role** viene visualizzata la finestra di dialogo.

    ![Create role (Crea ruolo)](./media/backup-azure-backup-server-vmware/vmware-define-new-role-priv.png)

3. In hello **Create Role** della finestra di dialogo hello **nome ruolo** immettere *BackupAdminRole*. nome del ruolo Hello può essere scelto liberamente, ma deve essere riconoscibile per scopo del ruolo hello.

4. Selezionare hello privilegi per la versione appropriata di hello di vCenter e quindi fare clic su **OK**. Hello nella tabella seguente identifica i privilegi necessario hello per vCenter 6.0 e vCenter 5.5.

  Quando si selezionano privilegi hello, fare clic su hello icona Avanti toohello padre etichetta tooexpand hello padre vista hello figlio privilegi di amministratore. privilegi di VirtualMachine tooselect hello, è necessario toogo vari livelli in hello relazione gerarchica. Non è necessario tooselect tutti i privilegi figlio all'interno di un privilegio padre.

  ![Gerarchia di privilegi padre-figlio](./media/backup-azure-backup-server-vmware/cert-add-privilege-expand.png)

  Dopo aver fatto clic **OK**, hello nuovo ruolo viene visualizzato nell'elenco di hello sul pannello ruoli hello.

|Privilegi per vCenter 6.0| Privilegi per vCenter 5.5|
|--------------------------|---------------------------|
|Datastore.AllocateSpace   | Datastore.AllocateSpace|
|Global.ManageCustomFields | Global.ManageCustomerFields|
|Global.SetCustomFields    |   |
|Host.Local.CreateVM       | Network.Assign |
|Network.Assign            |  |
|Resource.AssignVMToPool   |  |
|VirtualMachine.Config.AddNewDisk  | VirtualMachine.Config.AddNewDisk   |
|VirtualMachine.Config.AdvanceConfig| VirtualMachine.Config.AdvancedConfig|
|VirtualMachine.Config.ChangeTracking| VirtualMachine.Config.ChangeTracking |
|VirtualMachine.Config.HostUSBDevice||
|VirtualMachine.Config.QueryUnownedFiles|    |
|VirtualMachine.Config.SwapPlacement| VirtualMachine.Config.SwapPlacement |
|VirtualMachine.Interact.PowerOff| VirtualMachine.Interact.PowerOff |
|VirtualMachine.Inventory.Create| VirtualMachine.Inventory.Create |
|VirtualMachine.Provisioning.DiskRandomAccess| |
|VirtualMachine.Provisioning.DiskRandomRead|VirtualMachine.Provisioning.DiskRandomRead |
|VirtualMachine.State.CreateSnapshot| VirtualMachine.State.CreateSnapshot|
|VirtualMachine.State.RemoveSnapshot|VirtualMachine.State.RemoveSnapshot |
</br>



## <a name="create-a-vcenter-server-user-account-and-permissions"></a>Creare un account utente del server vCenter e le relative autorizzazioni

Una volta hello ruolo con privilegi è configurato, creare un account utente. account utente di Hello ha un nome e una password, che fornisce le credenziali hello vengono utilizzate per l'autenticazione.

1. un account utente, nel Server vCenter hello toocreate **Navigator** pannello, fare clic su **utenti e gruppi**.

    ![Opzione Users and Groups (Utenti e gruppi)](./media/backup-azure-backup-server-vmware/vmware-userandgroup-panel.png)

    Hello **vCenter utenti e gruppi** pannello viene visualizzato.

    ![Pannello vCenter Users and Groups (Utenti e gruppi di vCenter)](./media/backup-azure-backup-server-vmware/usersandgroups.png)

2. In hello **vCenter utenti e gruppi** pannello, seleziona hello **utenti** scheda e quindi fare clic su hello aggiungere utenti icona (simbolo + hello).

    Hello **nuovo utente** viene visualizzata la finestra di dialogo.

3. In hello **nuovo utente** finestra di dialogo, aggiungere le informazioni dell'utente hello e quindi scegliere **OK**. In questa procedura, nome utente di hello è BackupAdmin.

    ![Finestra di dialogo New User (Nuovo utente)](./media/backup-azure-backup-server-vmware/vmware-new-user-account.png)

    nuovo account utente di Hello viene visualizzato nell'elenco di hello.

4. account utente di hello tooassociate con ruolo hello in hello **Navigator** pannello, fare clic su **autorizzazioni globali**. In hello **autorizzazioni globali** pannello, seleziona hello **Gestisci** scheda e quindi fare clic su hello aggiungere icona (simbolo + hello).

    ![Pannello Global Permissions (Autorizzazioni globali)](./media/backup-azure-backup-server-vmware/vmware-add-new-perms.png)

    Hello **globale autorizzazioni Root - Aggiungi autorizzazione** viene visualizzata la finestra di dialogo.

5. In hello **radice autorizzazione globale - Aggiungi autorizzazione** la finestra di dialogo, fare clic su **Aggiungi** toochoose hello utente o gruppo.

    ![Scegliere un utente o un gruppo](./media/backup-azure-backup-server-vmware/vmware-add-new-global-perm.png)

    Hello **selezionare utenti/gruppi** viene visualizzata la finestra di dialogo.

6. In hello **selezionare utenti/gruppi** finestra di dialogo scegliere **BackupAdmin** e quindi fare clic su **Aggiungi**.

    In **utenti**, hello *dominio omeutente* formato viene utilizzato per l'account utente di hello. Se si desidera toouse un dominio diverso, sceglierlo dall'hello **dominio** elenco.

    ![Aggiungere l'utente BackupAdmin](./media/backup-azure-backup-server-vmware/vmware-assign-account-to-role.png)

    Fare clic su **OK** tooadd hello selezionato utenti toohello **Aggiungi autorizzazione** la finestra di dialogo.

7. Dopo aver identificato utente hello, assegnazione del ruolo di toohello utente hello. In **ruolo assegnato**, dall'elenco a discesa hello, selezionare **BackupAdminRole**, quindi fare clic su **OK**.

    ![Assegnare l'utente toorole](./media/backup-azure-backup-server-vmware/vmware-choose-role.png)

  In hello **Gestisci** scheda hello **autorizzazioni globali** pannello, nuovo account utente di hello e ruolo hello associato vengono visualizzati nell'elenco di hello.


## <a name="establish-vcenter-server-credentials-on-azure-backup-server"></a>Definizione di credenziali del server vCenter sul server di Backup di Azure

Prima di aggiungere hello VMware server tooAzure Backup Server, installare [Update 1 per il Server di Backup di Azure](https://support.microsoft.com/help/3175529/update-1-for-microsoft-azure-backup-server).

1. tooopen Server di Backup di Azure, fare doppio clic hello sul desktop del Server di Backup di Azure hello.

    ![Icona del server di Backup di Azure](./media/backup-azure-backup-server-vmware/mabs-icon.png)

    Se non si trova sull'icona di hello sul desktop di hello, aprire il Server di Backup di Azure dall'elenco di hello delle App installate. nome dell'app Azure Backup Server Hello viene chiamato Backup di Microsoft Azure.

2. Nella console di Server di Backup di Azure hello, fare clic su **Management**, fare clic su **server di produzione**e quindi fare clic sulla barra multifunzione dello strumento di hello, **gestire VMware**.

    ![Console del server di Backup di Azure](./media/backup-azure-backup-server-vmware/add-vmware-credentials.png)

    Hello **Gestisci credenziali** viene visualizzata la finestra di dialogo.

    ![Finestra di dialogo Gestisci credenziali del server di Backup di Azure](./media/backup-azure-backup-server-vmware/mabs-manage-credentials-dialog.png)

3. In hello **Gestisci credenziali** la finestra di dialogo, fare clic su **Aggiungi** tooopen hello **Add Credential** la finestra di dialogo.

4. In hello **Add Credential** finestra di dialogo immettere un nome e una descrizione per le nuove credenziali di hello. Specificare quindi hello username e password. nome Hello, *credential Contoso Vcenter* utilizzato credenziali hello tooidentify hello procedura descritta di seguito. Utilizzare hello stesso nome utente e la password utilizzata per hello vCenter Server. Se il Server vCenter hello e Server di Backup di Azure non sono in hello nello stesso dominio, in **nome utente**, specificare il dominio hello.

    ![Finestra di dialogo Aggiungi credenziali del server di Backup di Azure](./media/backup-azure-backup-server-vmware/mabs-add-credential-dialog2.png)

    Fare clic su **Aggiungi** tooadd hello nuova credenziale tooAzure Backup Server. nuove credenziali Hello verrà visualizzato nell'elenco hello hello **Gestisci credenziali** la finestra di dialogo.
    
    ![Finestra di dialogo Gestisci credenziali del server di Backup di Azure](./media/backup-azure-backup-server-vmware/new-list-of-mabs-creds.png)

5. hello tooclose **Gestisci credenziali** finestra di dialogo fare clic su hello **X** nell'angolo superiore destro di hello.


## <a name="add-hello-vcenter-server-tooazure-backup-server"></a>Aggiungere hello vCenter Server tooAzure Backup Server

Creazione guidata Aggiunta Server di produzione è usato tooadd hello vCenter Server tooAzure Backup Server.

tooopen guidata di aggiunta Server di produzione, hello completo seguente procedura:

1. Nella console di Server di Backup di Azure hello, fare clic su **Management**, fare clic su **server di produzione**, quindi fare clic su **Aggiungi**.

    ![Aprire l'Aggiunta guidata server di produzione](./media/backup-azure-backup-server-vmware/add-vcenter-to-mabs.png)

    Hello **guidata Aggiunta Server di produzione** viene visualizzata la finestra di dialogo.

    ![Aggiunta guidata server di produzione](./media/backup-azure-backup-server-vmware/production-server-add-wizard.png)

2. In hello **tipo selezionare Server di produzione** selezionare **server VMware**e quindi fare clic su **Avanti**.

3. In **nome Server o indirizzo IP**, specificare il nome di dominio completo hello (FQDN) o indirizzo IP del server VMware hello. Se tutti i server ESXi hello gestiti da hello vCenter stesso, è possibile utilizzare il nome di vCenter hello.

    ![Specificare l'FQDN o l'indirizzo IP del server VMware](./media/backup-azure-backup-server-vmware/add-vmware-server-provide-server-name.png)

4. In **porta SSL**, immettere una porta di hello toocommunicate utilizzato con server VMware hello. Utilizzare la porta 443, che è la porta predefinita hello, a meno che non si sa che una porta diversa è obbligatoria.

5. In **specificare le credenziali**, selezionare hello credenziali creato in precedenza.

    ![Specifica credenziale](./media/backup-azure-backup-server-vmware/identify-creds.png)

6. Fare clic su **Aggiungi** tooadd hello VMware server toohello elenco **aggiunto i server VMware**, quindi fare clic su **Avanti** toomove toohello pagina successiva procedura guidata hello.

    ![Aggiungere il server VMware e le credenziali](./media/backup-azure-backup-server-vmware/add-vmware-server-credentials.png)

7. In hello **riepilogo** pagina, fare clic su **Aggiungi** tooadd hello specificato tooAzure server VMware Server Backup.

    ![Aggiungi VMware server tooAzure Backup Server](./media/backup-azure-backup-server-vmware/tasks-screen.png)

  Hello VMware server backup è un backup senza agente e hello nuovo server viene aggiunto immediatamente. Hello **fine** pagina vengono visualizzati hello risultati.

  ![Pagina Fine](./media/backup-azure-backup-server-vmware/summary-screen.png)

  tooadd più istanze di tooAzure Server vCenter Server Backup, ripetere l'operazione hello precedente i passaggi in questa sezione.

Dopo aver aggiunto hello vCenter Server tooAzure Backup Server, hello è toocreate un gruppo protezione dati. gruppo protezione dati Hello specifica hello vari dettagli per la conservazione a breve o lungo termine in modo in cui si definisce e applicare i criteri di backup hello. criterio di backup Hello è pianificazione hello per quando si verificano i backup, e ciò che viene eseguito il backup.


## <a name="configure-a-protection-group"></a>Configurazione di un gruppo protezione dati

Se si utilizza System Center Data Protection Manager o Server di Backup di Azure prima di, vedere [pianificare i backup su disco](https://technet.microsoft.com/library/hh758026.aspx) tooprepare l'ambiente hardware. Dopo che si verifica di avere un'adeguata archiviazione, utilizzare hello Crea nuovo gruppo protezione dati guidata tooadd le macchine virtuali VMware.

1. Nella console di Server di Backup di Azure hello, fare clic su **protezione**, nella barra multifunzione dello strumento di hello, fare clic su **New** procedura guidata Crea nuovo gruppo protezione dati di tooopen hello.

    ![Procedura guidata Crea nuovo gruppo protezione dati hello aperto](./media/backup-azure-backup-server-vmware/open-protection-wizard.png)

    Hello **Crea nuovo gruppo protezione dati** viene visualizzata la finestra di dialogo Creazione guidata.

    ![Finestra di dialogo della procedura guidata Crea nuovo gruppo protezione dati](./media/backup-azure-backup-server-vmware/protection-wizard.png)

    Fare clic su **Avanti** tooadvance toohello **Seleziona tipo di gruppo protezione dati** pagina.

2. In hello **il tipo di gruppo protezione dati selezionare** selezionare **server** e quindi fare clic su **Avanti**. Hello **Seleziona membri del gruppo** verrà visualizzata la pagina.

3. In hello **Seleziona membri del gruppo** pagina, i membri disponibili hello e membri hello selezionato vengono visualizzati. Selezionare i membri di hello che desidera tooprotect e quindi fare clic su **Avanti**.

    ![Seleziona membri del gruppo](./media/backup-azure-backup-server-vmware/server-add-selected-members.png)

    Quando si seleziona un membro, se si seleziona una cartella che contiene altre cartelle o macchine virtuali, vengono selezionate anche le cartelle e le macchine virtuali contenute. inclusione di Hello di cartelle di hello e macchine virtuali nella cartella padre hello viene chiamata la protezione a livello di cartella. tooremove una cartella o nella macchina virtuale, la casella di controllo crittografato hello.

    Se una macchina virtuale o in una cartella che contiene una macchina virtuale, è già protetto tooAzure, è possibile selezionare nuovamente tale macchina virtuale. Vale a dire, dopo aver protetto tooAzure una macchina virtuale, non può essere protetto anche punti di ripristino duplicati che impedisce la creazione di una macchina virtuale. Se si desidera toosee quale istanza del Server di Backup di Azure protegge già un membro, il punto toohello toosee hello Nome membro hello protezione del server.

4. In hello **Selezione metodo protezione dati** pagina, immettere un nome per il gruppo di protezione dati hello. Protezione a breve termine (toodisk) e online sono selezionati. Se si desidera la protezione online toouse (tooAzure), è necessario utilizzare toodisk protezione a breve termine. Fare clic su **Avanti** intervallo di protezione tooproceed toohello a breve termine.

    ![Seleziona metodo protezione dati](./media/backup-azure-backup-server-vmware/name-protection-group.png)

5. In hello **Specifica obiettivi a breve termine** pagina per **mantenimento**, specificare hello numero di giorni per cui si desidera che i punti di ripristino di tooretain *archiviati toodisk*. Se si desidera ora hello toochange e giorni quando vengono eseguiti i punti di ripristino, fare clic su **modifica**. punti di ripristino a breve termine Hello sono backup completi. e non backup incrementali. Quando si è soddisfatti gli obiettivi a breve termine hello, fare clic su **Avanti**.

    ![Specifica obiettivi a breve termine](./media/backup-azure-backup-server-vmware/short-term-goals.png)

6. In hello **Verifica allocazione dischi** pagina, esaminare e se necessario, modificare lo spazio su disco hello per le macchine virtuali hello. Hello consigliati allocazioni dei dischi sono in base hello periodo di mantenimento specificato in hello **Specifica obiettivi a breve termine** pagina hello tipo di carico di lavoro e dimensioni di hello di hello i dati protetti (identificati nel passaggio 3).  

  - **Dimensioni dei dati:** dimensioni dei dati di hello nel gruppo protezione dati hello.
  - **Spazio su disco:** hello quantità di spazio su disco per il gruppo di protezione dati hello consigliata. Se si desidera toomodify questa impostazione, è consigliabile allocare uno spazio totale leggermente superiore rispetto a quanto hello che si prevede di che aumento delle dimensioni di ogni origine dati.
  - **Condividi percorso dati:** se si attiva la condivisione del percorso, più origini dati nella protezione hello possono mappare tooa singola replica e volume del punto di ripristino. La condivisione del percorso non è supportata per tutti i carichi di lavoro.
  - **Aumento automatico delle dimensioni:** se si abilita questa impostazione, se i dati nel gruppo protetto hello superano l'allocazione iniziale di hello, System Center Data Protection Manager tenta di dimensioni del disco tooincrease hello del 25%.
  - **Dettagli pool di archiviazione:** Mostra stato hello hello del pool di archiviazione, inclusi totale e residua dimensioni del disco.

    ![Rivedere l'allocazione dei dischi](./media/backup-azure-backup-server-vmware/review-disk-allocation.png)

    Quando si è soddisfatti di allocazione dello spazio di hello, fare clic su **Avanti**.

7. In hello **Scegli metodo di creazione della Replica** pagina, specificare come copia iniziale di toogenerate hello o replica, dei dati di hello protetto nel Server di Backup di Azure.

    valore predefinito di Hello è **automaticamente tramite rete hello** e **ora**. Se si utilizza l'impostazione di hello, si consiglia di specificare un orario. Scegliere **In seguito** e specificare un giorno e un'ora.

    Per grandi quantità di dati o condizioni della rete-ottimale, prendere in considerazione la replica dei dati hello offline usando supporti rimovibili.

    Dopo avere effettuato le scelte, fare clic su **Avanti**.

    ![Scelta del metodo per la creazione della replica](./media/backup-azure-backup-server-vmware/replica-creation.png)

8. In hello **opzioni di verifica coerenza** pagina, selezionare come e quando le verifiche della coerenza hello tooautomate. È possibile eseguire verifiche della coerenza quando i dati di replica diventano incoerenti o in base a una pianificazione impostata.

    Se non si desidera tooconfigure le verifiche di coerenza automatica, è possibile eseguire una verifica manuale. Nell'area di protezione hello hello Azure Backup della console di Server, gruppo di protezione dati hello e quindi scegliere **Esegui verifica coerenza**.

    Fare clic su **Avanti** toomove toohello prossima pagina.

9. In hello **specificare dati da proteggere Online** pagina, selezionare uno o più origini dati che si desidera tooprotect. È possibile selezionare i membri di hello singolarmente o fare clic su **Seleziona tutto** toochoose tutti i membri. Dopo aver scelto i membri di hello, fare clic su **Avanti**.

    ![Specifica i dati da proteggere online](./media/backup-azure-backup-server-vmware/select-data-to-protect.png)

10. In hello **pianificazione dei Backup Online specificare** specificare toogenerate i punti di ripristino da backup su disco hello hello pianificazione. Dopo la generazione di un punto di ripristino hello, è l'insieme di credenziali di servizi di ripristino toohello trasferiti in Azure. Quando si è soddisfatti di pianificazione dei backup online hello, fare clic su **Avanti**.

    ![Specificare la pianificazione dei backup online](./media/backup-azure-backup-server-vmware/online-backup-schedule.png)

11. In hello **specificare criteri di conservazione Online** pagina, specificare quanto tempo si desidera tooretain dati di backup hello in Azure. Dopo aver definito i criteri di hello, fare clic su **Avanti**.

    ![Specificare i criteri di mantenimento online](./media/backup-azure-backup-server-vmware/retention-policy.png)

    Non esiste un limite di tempo per la conservazione dei dati in Azure. Quando si archiviano i dati relativi al punto di ripristino in Azure, hello solo limite è che non è possibile avere più di 9999 punti di ripristino per ogni istanza protetta. In questo esempio, istanza protetta hello è server VMware hello.

12. In hello **riepilogo** pagina, esaminare i dettagli di hello per le impostazioni e i membri del gruppo protezione dati e quindi fare clic su **Crea gruppo**.

    ![Riepilogo delle impostazioni e dei membri del gruppo protezione dati](./media/backup-azure-backup-server-vmware/protection-group-summary.png)

## <a name="next-steps"></a>Passaggi successivi
Se si utilizzano i carichi di lavoro di Azure Backup Server tooprotect VMware, potrebbe essere interessati all'uso di Server di Backup di Azure toohelp proteggere un [Microsoft Exchange server](./backup-azure-exchange-mabs.md), [farm Microsoft SharePoint](./backup-azure-backup-sharepoint-mabs.md), o un [Database di SQL Server](./backup-azure-sql-mabs.md).

Per informazioni sui problemi con la registrazione dell'agente di hello, configurare il gruppo di protezione dati hello o il backup dei processi, vedere [risoluzione dei problemi dei Server di Backup Azure](./backup-azure-mabs-troubleshoot.md).
