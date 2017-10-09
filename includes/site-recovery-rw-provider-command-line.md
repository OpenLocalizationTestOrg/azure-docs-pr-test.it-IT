UnifiedSetup.exe [/ ServerMode < CS/PS >] [/ Unitàinstallazione <DriveLetter>] [/ MySQLCredsFilePath <MySQL credentials file path>] [/ VaultCredsFilePath <Vault credentials file path>] [/ EnvType < VMWare/NonVMWare >] [/ PSIP < toobe indirizzo IP utilizzato per il trasferimento di dati] [/CSIP <IP address of CS toobe registered with>] [/ PassphraseFilePath <Passphrase file path>]

Parametri

* /ServerMode: obbligatorio. Specifica se deve essere installato sia hello configurazione processo server o solo i server di elaborazione hello. Valori di input: CS, PS.
* InstallLocation: obbligatorio. cartella Hello in cui hello vengono installati i componenti.
* /MySQLCredsFilePath: Obbligatorio. percorso del file Hello in cui hello MySQL sono archiviate le credenziali di server. file Hello deve essere nel formato seguente:
* [MySQLCredentials]
* MySQLRootPassword = "<Password>"
* MySQLUserPassword = "<Password>"
* /VaultCredsFilePath: Obbligatorio. percorso di Hello del file delle credenziali dell'insieme di credenziali hello
* /EnvType: Obbligatorio. tipo di Hello di installazione. Valori: VMware, NonVMware.
* /PSIP e /CSIP. Obbligatorio. indirizzo IP di Hello del server di elaborazione hello e server di configurazione.
* /PassphraseFilePath. Obbligatorio. posizione di Hello del file della passphrase hello.
* /BypassProxy: Facoltativo. Specifica che nel server configurazione hello si connette tooAzure senza un proxy.
* /ProxySettingsFilePath: Facoltativo. Impostazioni proxy (proxy predefinito hello richiede l'autenticazione o un proxy personalizzato). file Hello deve essere nel formato seguente:
* [ProxySettings]
* ProxyAuthentication = "Sì/No"
* Proxy IP = "Indirizzo IP>"
* ProxyPort = "<Port>"
* ProxyUserName="<User Name>"
* ProxyPassword="<Password>"
* DataTransferSecurePort: Facoltativo. numero di porta Hello per dati di replica.
* SkipSpaceCheck: facoltativo. Ignora la verifica dello spazio per la cache.
* AcceptThirdpartyEULA: Obbligatorio. Accetta il contratto di terze parti hello.
* ShowThirdpartyEULA: obbligatorio. Visualizza le condizioni di licenza di terze parti. Se specificato come input, tutti gli altri parametri vengono ignorati.
