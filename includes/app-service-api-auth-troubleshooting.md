La maggior parte degli errori di autenticazione ora hello causati da impostazioni di configurazione non corretta o non coerenti. Di seguito sono riportati alcuni suggerimenti specifici per operazioni toocheck.

* Assicurarsi che non è stata Ometti hello **salvare** pulsante remoto via Internet. Questo è spesso semplice toodo e il risultato di hello è che parlerò valori corretti di hello in una pagina del portale, ma in realtà non sono state salvate in hello ambiente Azure o un'applicazione Azure AD.
* Per le impostazioni configurate in hello **le impostazioni dell'applicazione** blade di hello portale di Azure, assicurarsi che tale hello app per le API o un'app web è stato selezionato quando sono state immesse le impostazioni di hello corretto.  Assicurarsi inoltre che le impostazioni di hello siano stati immessi come **impostazioni App** e non **le stringhe di connessione**, come il formato delle sezioni hello due hello è simile.
* Per l'autenticazione tooa front-end JavaScript, download hello nuovo manifesto tooverify che `oauth2AllowImplicitFlow` è stato modificato troppo`true`.
* Verificare di avere usato HTTPS ogni volta che sono stati configurati gli URL:
  
  * Nel codice del progetto
  * In CORS
  * Nelle impostazioni dell'app dell'ambiente Azure per ogni app per le API e app Web
  * Nelle impostazioni dell'applicazione di Azure AD.
    
    Si noti che se si copia l'URL di un'API app dal portale di hello, spesso è `http://` e si dispone di modificarla troppo toomanually`https://`.
* Assicurarsi che tutte le modifiche del codice sono state correttamente distribuite. In una soluzione multiprogetto, ad esempio, è possibile toochange un progetto del codice e accidentalmente scegliere uno dei hello ad altri utenti quando si modifica hello toodeploy.
* Assicurarsi che si sta tooHTTPS URL nel browser, non l'URL HTTP. Per impostazione predefinita, Visual Studio crea profili con URL HTTP di pubblicazione ed è ciò che viene aperto nel browser di hello dopo aver distribuito un progetto.
* Per l'autenticazione tooa front-end JavaScript, assicurarsi che CORS sia configurato correttamente in app di API hello che hello chiamate di codice JavaScript. In caso di dubbi sul problema hello correlati a CORS, provare a "*" come hello consentito URL di origine. 
* Per un front-end JavaScript, aprire tooget di scheda Console degli strumenti per sviluppatori del browser ulteriori informazioni sull'errore ed esaminare le richieste HTTP su hello rete. Tuttavia, i messaggi di errore della console possono essere fuorvianti. Se viene visualizzato un messaggio che indica un errore CORS, problema reale hello sia l'autenticazione. È possibile verificare se ciò avviene hello eseguendo l'applicazione hello con autenticazione temporaneamente temporaneamente disabilitata.
* Per un'applicazione API .NET, assicurarsi che si desidera ottenere le informazioni nei messaggi di errore possibili impostando [tooOff modalità customErrors](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remoteview).
* Per un'applicazione API .NET, avviare un [sessione di debug remoto](../articles/app-service-web/web-sites-dotnet-troubleshoot-visual-studio.md#remotedebug)ed esaminare i valori hello delle variabili di hello passati toocode che usa ADAL tooacquire un token di connessione o il codice che verifica le attestazioni con l'ID dell'entità servizio hello previsto. Si noti che il codice può prelevare i valori di configurazione da molte origini diverse, pertanto è possibile toofind sorprese in questo modo. Ad esempio, se commette `ida:ClientId` come `ida:ClientID` quando si configurano le impostazioni di ambiente del servizio App di Azure, il codice hello potrebbe ottenere hello `ida:ClientId` valore che esegue la ricerca di file Web. config hello, ignorando l'impostazione di servizio App di Azure hello. 
* Se ciò non funziona in una normale finestra di Internet Explorer, gli accessi esistenti potrebbero interferire. Provare quindi la modalità InPrivate e Firefox o Chrome.

