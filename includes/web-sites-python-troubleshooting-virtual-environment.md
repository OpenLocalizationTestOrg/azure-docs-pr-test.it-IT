script di distribuzione Hello ignorerà la creazione dell'ambiente virtuale hello in Azure se rileva che esiste già un ambiente virtuale compatibile.  Questo comportamento può accelerare notevolmente la distribuzione.  I pacchetti già installati verranno ignorati da pip.

In alcune situazioni, è consigliabile eliminare tooforce tale ambiente virtuale.  È opportuno toodo questa se si decide di tooinclude un ambiente virtuale come parte del repository.  È inoltre possibile toodo questo se è necessario tooget rid di alcuni pacchetti o test toorequirements.txt le modifiche.

Esistono alcuni hello toomanage di opzioni esistente di un ambiente virtuale in Azure:

### <a name="option-1-use-ftp"></a>Opzione 1: Utilizzare il FTP
Con un client FTP, connettere toohello server e la cartella di env toodelete in grado di hello.  Si noti che alcuni client FTP (ad esempio i browser web) sia di sola lettura e non consentono di toodelete cartelle, quindi è opportuno toomake che toouse un client FTP con tale funzionalità.  nome host FTP Hello e utente vengono visualizzati nel pannello dell'app web in hello [portale Azure](https://portal.azure.com).

### <a name="option-2-toggle-runtime"></a>Opzione 2: Attiva/Disattiva runtime
Di seguito è un'alternativa che sfrutta il fatto di hello che lo script di distribuzione hello cartella verrà eliminata hello env quando non corrisponde a versione desiderata di hello di Python.  In modo efficace questa verrà eliminare l'ambiente esistente hello e crearne uno nuovo.

1. Versione diversa di tooa commutatore di Python (tramite runtime.txt o hello **le impostazioni dell'applicazione** pannello in hello portale di Azure)
2. Eseguire il push GIT di alcune modifiche (ignorare eventuali errori di installazione di pip)
3. Passa indietro tooinitial versione di Python
4. Eseguire di nuovo il push GIT di alcune modifiche

### <a name="option-3-customize-deployment-script"></a>Opzione 3: personalizzare lo script di distribuzione
Se si è personalizzato script di distribuzione hello, è possibile modificare hello codificarlo in Deploy tooforce cartella env di hello toodelete.

