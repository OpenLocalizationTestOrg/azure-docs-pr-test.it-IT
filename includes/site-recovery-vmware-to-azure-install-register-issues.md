
### <a name="installation-failures"></a>Errori di installazione
| **Messaggio di errore di esempio** | **Azione consigliata** |
|--------------------------|------------------------|
|Account tooload non riuscito di errore. Errore: IOException: Impossibile tooread dati hello trasporto della connessione durante l'installazione e la registrazione di hello server CS.| Verificare che TLS 1.0 sia abilitato nel computer di hello. |

### <a name="registration-failures"></a>Errori di registrazione
Il debug degli errori di registrazione possono essere eseguiti esaminando i registri hello in hello **%ProgramData%\ASRLogs** cartella.

| **Messaggio di errore di esempio** | **Azione consigliata** |
|--------------------------|------------------------|
|**09:20:06**:InnerException.Type: SrsRestApiClientLib.AcsException,InnerException.<br>Message: ACS50008: SAML token is invalid.<br>Trace ID: 1921ea5b-4723-4be7-8087-a75d3f9e1072<br>Correlation ID: 62fea7e6-2197-4be4-a2c0-71ceb7aa2d97><br>Timestamp: **2016-12-12 14:50:08Z<br>** | Verificare che ora hello l'orologio di sistema non sia più di 15 minuti di inattività ora locale hello. Eseguire di nuovo la registrazione di hello installer toocomplete hello.|
|**35:09:27** : DRRegistrationException durante il tentativo di tooget tutti emergenza ripristino insieme di credenziali per il certificato selezionato hello:: Exception.Type:Microsoft.DisasterRecovery.Registration.DRRegistrationException ha generato, Exception. Message: ACS50008: Token SAML non è valido.<br>Trace ID: e5ad1af1-2d39-4970-8eef-096e325c9950<br>Correlation ID: abe9deb8-3e64-464d-8375-36db9816427a<br>Timestamp: **2016-05-19 01:35:39Z**<br> | Verificare che ora hello l'orologio di sistema non sia più di 15 minuti di inattività ora locale hello. Eseguire di nuovo la registrazione di hello installer toocomplete hello.|
|06:28:45: certificato toocreate non riuscita<br>06:28:45:Setup cannot proceed. È necessario tooSite tooauthenticate che ripristino non è possibile creare un certificato. Rerun Setup | Verificare di eseguire il programma di installazione come amministratore locale. |
