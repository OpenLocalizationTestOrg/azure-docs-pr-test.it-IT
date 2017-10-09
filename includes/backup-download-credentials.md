## <a name="using-vault-credentials-tooauthenticate-with-hello-azure-backup-service"></a>Con insieme di credenziali le credenziali tooauthenticate hello servizio Azure Backup
il server locale Hello (client di Windows o Windows Server o Data Protection Manager sul server) deve toobe autenticato con un insieme di credenziali di backup prima di è possibile eseguire il backup dei dati tooAzure. l'autenticazione di Hello viene ottenuta utilizzando "insieme di credenziali delle credenziali". il concetto di Hello di insieme di credenziali è il concetto di toohello simile di un file "impostazioni di pubblicazione" utilizzato in Azure PowerShell.

### <a name="what-is-hello-vault-credential-file"></a>Che cos'è file delle credenziali dell'insieme di credenziali hello?
file delle credenziali dell'insieme di credenziali Hello è un certificato generato dal portale hello per ogni insieme di credenziali di backup. portale Hello carica quindi hello toohello chiave pubblica del servizio di controllo di accesso (ACS). chiave privata di Hello del certificato di hello è attivata la modalità utente toohello disponibile come parte del flusso di lavoro hello fornito come input per il flusso di lavoro di hello macchina registrazione. Consente di autenticare hello macchina toosend dati di backup identificato tooan insieme di credenziali in hello servizio Azure Backup.

insieme di credenziali Hello viene utilizzato solo durante il flusso di lavoro di hello registrazione. È tooensure responsabilità dell'utente hello che l'insieme di credenziali non venga compromessa file hello. Se si trova in mani hello di qualsiasi utente non autorizzato, hello insieme di credenziali le credenziali file può essere utilizzato tooregister altre macchine hello stesso insieme di credenziali. Tuttavia, come dati di backup hello sono crittografati con una passphrase che appartiene toohello cliente, i dati di backup esistenti non possono essere compromesso. toomitigate questo problema, l'insieme di credenziali viene impostata tooexpire in 48hrs. È possibile scaricare l'insieme di credenziali di un insieme di credenziali backup hello qualsiasi numero di volte, ma è applicabile solo hello file più recente dell'insieme di credenziali delle credenziali durante il flusso di lavoro di hello registrazione.

### <a name="download-hello-vault-credential-file"></a>Scaricare file delle credenziali dell'insieme di credenziali hello
file delle credenziali dell'insieme di credenziali Hello viene scaricato tramite un canale protetto da hello portale di Azure. Hello servizio Azure Backup non è a conoscenza della chiave privata di hello del certificato hello e la chiave privata di hello non è persistenti nel portale di hello o servizio hello. Utilizzare hello seguendo i passaggi toodownload hello archivio credenziali file tooa computer locale.

1. Accedi toohello [portale di gestione](https://manage.windowsazure.com/)
2. Fare clic su **servizi di ripristino** nel riquadro di spostamento a sinistra hello e credenziali di backup selezionare hello che è stato creato. Fare clic sull'icona tooget toohello visualizzazione avvio rapido dell'insieme di credenziali di backup hello di hello cloud.
   
   ![Anteprima](./media/backup-download-credentials/quickview.png)
3. Nella pagina introduttiva hello, fare clic su **Scarica credenziali**. portale di Hello genera i file di credenziali dell'insieme di credenziali di hello, che viene reso disponibili per il download.
   
   ![Scaricare](./media/backup-download-credentials/downloadvc.png)
4. portale Hello genererà un insieme di credenziali utilizzando una combinazione di nome insieme di credenziali hello e hello data corrente. Fare clic su **salvare** toodownload hello archivio credenziali toohello account locale cartella di download o scegliere Salva con nome hello salvare menu toospecify un percorso per l'insieme di credenziali hello.

### <a name="note"></a>Nota
* Verificare che l'insieme di credenziali hello viene salvato in una posizione accessibile dal computer. Se è stata archiviata in un condivisione di file/SMB, la verifica delle autorizzazioni di accesso hello.
* file delle credenziali dell'insieme di credenziali Hello viene utilizzato solo durante il flusso di lavoro di hello registrazione.
* file delle credenziali dell'insieme di credenziali Hello scade dopo 48hrs e può essere scaricato dal portale hello.
* Fare riferimento toohello Azure Backup [domande frequenti su](../articles/backup/backup-azure-backup-faq.md) per eventuali domande sul flusso di lavoro hello.

