## <a name="download-install-and-register-hello-azure-backup-agent"></a>Scaricare, installare e registrare l'agente Azure Backup hello
Dopo aver creato l'insieme di credenziali di Backup di Azure hello, deve essere installato un agente in ogni computer Windows (Windows Server, client di Windows, server System Center Data Protection Manager o il computer Server di Backup di Azure) che consente di eseguire il backup dei dati e delle applicazioni tooAzure.

1. Accedi toohello [portale di gestione](https://manage.windowsazure.com/)
2. Fare clic su **servizi di ripristino**, quindi selezionare hello insieme di credenziali backup che si desidera tooregister con un server. verrà visualizzata la pagina avvio rapido Hello per tale insieme di credenziali di backup.
   
    ![Avvio rapido](./media/backup-install-agent/quickstart.png)
3. Nella pagina introduttiva hello, fare clic su hello **client per Windows Server o System Center Data Protection Manager o Windows** opzione **Scarica agente**. Fare clic su **salvare** toocopy il computer locale toohello.
   
    ![Salva agente](./media/backup-install-agent/agent.png)
4. Dopo aver installato l'agente di hello, fare doppio clic su installazione di hello toolaunch MARSAgentInstaller.exe dell'agente di Backup di Azure hello. Scegliere la cartella di installazione hello e la cartella dei file temporanei necessari per l'agente di hello. percorso della cache di Hello specificato deve disporre di spazio disponibile ovvero almeno il 5% dei dati di backup hello.
5. Se si utilizza un toohello tooconnect di server proxy internet, hello **configurazione Proxy** schermata, immettere i dettagli del server proxy hello. Se si utilizza un proxy autenticato, immettere i dettagli di nome e una password utente hello in questa schermata.
6. l'agente di Backup di Azure Hello installazione di .NET Framework 4.5 e Windows PowerShell (se non è già disponibile) toocomplete hello.
7. Dopo aver installato l'agente di hello, fare clic su hello **procedere tooRegistration** pulsante toocontinue con flusso di lavoro hello.
   
   ![Registra](./media/backup-install-agent/register.png)
8. Nella schermata di credenziali dell'insieme di credenziali di hello, Sfoglia tooand hello selezionare insieme di credenziali le credenziali che è stato scaricato in precedenza.
   
    ![Credenziali di insieme](./media/backup-install-agent/vc.png)
   
    file delle credenziali dell'insieme di credenziali Hello è valido solo per 48 ore (dopo che è stato scaricato dal portale hello). Se si verifica un errore in questa schermata (ad esempio "insieme di credenziali file specificato è scaduto"), account di accesso toohello portale di Azure e scarica hello credenziali file nuovamente.
   
    Verificare che il file di credenziali dell'insieme di credenziali hello è disponibile in una posizione in cui è possibile accedere da un'applicazione hello il programma di installazione. Se si verificano errori correlati di accedere, hello copia l'insieme di credenziali file tooa percorso temporaneo in questo computer e riprova l'operazione di hello.
   
    Se si verifica un errore di credenziali dell'insieme di credenziali non valido (ad esempio "credenziali non valido fornite"), file hello è danneggiato o sono credenziali più recenti hello associate con il servizio di ripristino hello. Ripetere l'operazione di hello dopo il download di un nuovo file delle credenziali dell'insieme di credenziali dal portale hello. Questo errore si verifica in genere se hello utente fa clic su hello **Download insieme di credenziali** opzione nel portale di Azure in rapida successione hello. In questo caso, solo hello secondo insieme di credenziali file delle credenziali è valido.
9. In hello **impostazione di crittografia** schermata, è possibile generare una passphrase o fornire una passphrase (minimo 16 caratteri). Tenere presente che toosave hello passphrase in un luogo sicuro.
   
    ![Crittografia](./media/backup-install-agent/encryption.png)
   
   > [!WARNING]
   > Se hello passphrase viene persa o dimenticata; Consente di recuperare i dati di backup hello non consente di Microsoft. Microsoft non abbiano visibilità sul passphrase hello utilizzata dall'utente finale di hello utente finale di Hello proprietario hello passphrase di crittografia. Salvare il file hello in un luogo sicuro in quanto è necessario durante un'operazione di ripristino.
   > 
   > 
10. Dopo aver scelto hello **fine** pulsante, hello macchina è stata registrata toohello insieme di credenziali e si sono ora pronti toostart backup tooMicrosoft Azure.
11. Quando si usa Microsoft Azure Backup autonomo è possibile modificare le impostazioni di hello specificate durante il flusso di lavoro di hello registrazione facendo clic su hello **Modifica proprietà** opzione hello Azure Backup snap-in mmc.
    
    ![Modifica proprietà](./media/backup-install-agent/change.png)
    
    In alternativa, quando si usa Data Protection Manager, è possibile modificare le impostazioni di hello specificate durante il flusso di lavoro di hello registrazione facendo hello **configura** opzione selezionando **Online** in hello **Gestione** scheda.
    
    ![Configurare il Backup di Azure](./media/backup-install-agent/configure.png)

