|Nome parametro| Tipo | Descrizione| Valori possibili|
|-|-|-|-|
| /Modalità server|Mandatory|Specifica se deve essere installato sia hello configurazione processo server o solo i server di elaborazione hello|CS<br>PS|
|/InstallLocation|Mandatory|cartella Hello in cui hello vengono installati i componenti| Qualsiasi cartella nel computer di hello|
|/MySQLCredsFilePath|Mandatory|percorso del file Hello in cui hello MySQL sono archiviate le credenziali di server|file Hello deve essere in formato hello specificato di seguito|
|/VaultCredsFilePath|Mandatory|percorso di Hello del file delle credenziali dell'insieme di credenziali hello|Percorso del file valido|
|/EnvType|Mandatory|Tipo di ambiente che si desidera tooprotect |VMware<br>NonVMware|
|/PSIP|Mandatory|Indirizzo IP di hello NIC toobe utilizzata per il trasferimento di dati di replica| Qualsiasi indirizzo IP valido|
|/CSIP|Mandatory|indirizzo IP Hello della NIC hello in cui hello è in ascolto il server di configurazione| Qualsiasi indirizzo IP valido|
|/PassphraseFilePath|Mandatory|Hello toolocation percorso completo del file della passphrase hello|Percorso del file valido|
|/BypassProxy|Facoltativo|Specifica che il server di configurazione di hello si connette tooAzure senza un proxy|toodo ottenere tale valore dalla Venu|
|/ProxySettingsFilePath|Facoltativo|Impostazioni proxy (proxy predefinito hello richiede l'autenticazione o un proxy personalizzato)|file Hello deve essere nel formato hello specificato di seguito|
|DataTransferSecurePort|Facoltativo|Numero di porta hello PSIP toobe utilizzato per i dati di replica| Numero di porta valido (il valore predefinito è 9433)|
|/SkipSpaceCheck|Facoltativo|Ignora la verifica dello spazio per il disco della cache| |
|/AcceptThirdpartyEULA|Mandatory|Il flag implica l'accettazione dell'EULA di terze parti| |
|/ShowThirdpartyEULA|Facoltativo|Visualizza le condizioni di licenza di terze parti. Se specificato come input, tutti gli altri parametri vengono ignorati| |
