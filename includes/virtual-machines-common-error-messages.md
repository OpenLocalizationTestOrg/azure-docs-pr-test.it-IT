>[!NOTE]
> È possibile lasciare commenti in questa pagina oppure nel forum di [commenti e suggerimenti](https://feedback.azure.com/forums/216843-virtual-machines) su Azure tramite #azerrormessage.

## <a name="error-response-format"></a>Formato di risposta di errore 
Macchine virtuali di Azure usare hello seguendo il formato JSON di risposta di errore:

```json
{
  "status": "status code",
  "error": {
    "code":"Top level error code",
    "message":"Top level error message",
    "details":[
     {
      "code":"Inner evel error code",
      "message":"Inner level error message"
     }
    ]
   }
}
```

Una risposta di errore include sempre un codice di stato e un oggetto error. Ogni oggetto error contiene sempre un codice di errore e una sezione message. Se hello macchina virtuale viene creata con un modello, oggetto error hello contiene inoltre una sezione dei dettagli che contiene un livello interno di codici di errore e il messaggio. In genere, hello livello interno la maggior parte del messaggio di errore sono errore radice hello.


## <a name="common-virtual-machine-management-errors"></a>Messaggi di errore comuni nella gestione di macchine virtuali

In questa sezione elenca hello messaggi di errore comuni che possono verificarsi durante la gestione delle macchine virtuali:

|  Codice di errore  |  Messaggio di errore  |  
|  :------| :-------------|  
|  AcquireDiskLeaseFailed  |  Impossibile tooacquire lease durante la creazione del disco '{0}' con blob \\{1 \\} URI. Il BLOB è già in uso.  |  
|  AllocationFailed  |  Allocazione non riuscita. Provare a ridurre le dimensioni VM hello o numero di macchine virtuali, riprovare più tardi o provare a distribuire tooa Set di disponibilità o percorso di Azure diverso.  |  
|  AllocationFailed  |  Errore interno tooan Hello allocazione della macchina virtuale non riuscita. . Riprovare più tardi o provare a distribuire tooa altro percorso.  |
|  ArtifactNotFound  |  Impossibile trovare nel percorso '{2}' Hello estensione della macchina virtuale con editore '{0}' e il tipo '\\{1 \\}'.  |
|  ArtifactNotFound  |  Tipo di estensione con editore '{0}', '\\{1 \\}' e versione del gestore tipo '{2}' non è stata trovata nel repository di estensione hello.  |
|  ArtifactVersionNotFound  |  Nessuna versione trovata nel repository di artefatti hello che soddisfa hello richiesto version '{0}'.  |
|  ArtifactVersionNotFound  |  Nessuna versione trovata nel repository di artefatti hello che soddisfa hello richiesto versione '{0}' per l'estensione della macchina virtuale con editore '\\{1 \\}' e il tipo '{2}'.  |
|  AttachDiskWhileBeingDetached  |  Non è possibile collegare dati disco '{0}' tooVM '\\{1 \\}' perché il disco di hello è attualmente in corso di disconnessione. Attendere fino al disco hello sia completamente scollegato e quindi riprovare.  |
|  RichiestaNonValida  |  Il set di disponibilità di tipo 'Allineato' non sono ancora supportati in questa area.  |
|  RichiestaNonValida  |  Aggiunta di una macchina virtuale con dischi gestiti gestiti toonon Set di disponibilità o l'aggiunta di una macchina virtuale con toomanaged dischi blob basato su Set di disponibilità non è supportata. Creare un Set di disponibilità con set di proprietà "gestito" in ordine tooadd una macchina virtuale con dischi gestiti tooit.  |
|  RichiestaNonValida  |  Il servizio Managed Disks non è supportato in questa area.  |
|  RichiestaNonValida  |  Per il tipo di sistema operativo '{0}' non sono supportate più estensioni della macchina virtuale per ciascun gestore. L'estensione della macchina virtuale '{1}' con gestore '{2}' è già stata aggiunta o specificata nell'input.  |
|  RichiestaNonValida  |  L'operazione '{0}' non è supportata nella risorsa '{1}' con dischi gestiti.  |
|  CertificateImproperlyFormatted  |  rappresentazione JSON di un segreto recuperato da {0} Hello ha un campo di dati che non è un file PFX formattato correttamente o password hello fornita non decodifica correttamente file PFX hello.  |
|  CertificateImproperlyFormatted  |  dati Hello recuperati da {0} non sono deserializzabili in JSON.  |
|  Conflitto  |  Ridimensionamento del disco è consentito solo quando la creazione di una macchina virtuale o hello VM viene deallocato.  |
|  ConflictingUserInput  |  Impossibile collegare il disco '{0}' come disco di hello è già di proprietà dalla macchina virtuale '\\{1 \\}'.  |
|  ConflictingUserInput  |  Gruppi di risorse di origine e destinazione sono hello stesso.  |
|  ConflictingUserInput  |  Gli account di archiviazione di origine e di destinazione per il disco {0} sono diversi.  |
|  ContainerAlreadyOnLease  |  È già presente un lease nel contenitore di archiviazione hello tenendo blob hello con URI {0}.  |
|  CrossSubscriptionMoveWithKeyVaultResources  |  richiesta di spostamento delle risorse Hello contiene risorse KeyVault che fanno riferimento uno o più {0} s nella richiesta di hello. Questo scenario non è attualmente supportato nello spostamento tra sottoscrizioni. Verificare i dettagli dell'errore hello per hello ID risorsa KeyVault.  |
|  DiagnosticsOperationInternalError  |  Si è verificato un errore interno durante l'elaborazione di un profilo di diagnostica della macchina virtuale {0}.  |
|  DiskBlobAlreadyInUseByAnotherDisk  |  BLOB {0} è già in uso da un altro disco appartenente tooVM '\\{1 \\}'. È possibile esaminare i metadati del blob hello hello disco informazioni di riferimento.  |
|  DiskBlobNotFound  |  Non è possibile toofind VHD blob con URI {0} per il disco '\\{1 \\}'.  |
|  DiskBlobNotFound  |  Non è possibile toofind VHD blob con URI {0}.  |
|  DiskEncryptionKeySecretMissingTags  |  segreto {0} privo di tag di hello \\{1 \\}. Aggiornare una versione del segreto hello, aggiungere tag hello necessarie e riprovare.  |
|  DiskEncryptionKeySecretUnwrapFailed  |  L'annullamento del wrapping del valore {0} del segreto tramite la chiave {1} non è riuscito.  |
|  DiskImageNotReady  |  L'immagine del disco {0} si trova nello stato {1}. Riprovare quando l'immagine è pronta.  |
|  DiskPreparationError  |  Si sono verificati uno o più errori durante la preparazione dei dischi della macchina virtuale. Per informazioni, vedere la visualizzazione dell'istanza del disco.  |
|  DiskProcessingError  |  L'elaborazione del disco è stato interrotto hello VM contiene altri dischi in dischi danneggiati.  |
|  ImageBlobNotFound  |  Non è possibile toofind VHD blob con URI {0} per il disco '\\{1 \\}'.  |
|  ImageBlobNotFound  |  Non è possibile toofind VHD blob con URI {0}.  |
|  IncorrectDiskBlobType  |  I BLOB del disco possono essere solo di tipo BLOB di pagine. Il BLOB {0} per il disco '{1}' è di tipo BLOB in blocchi.  |
|  IncorrectDiskBlobType  |  I BLOB del disco possono essere solo di tipo BLOB di pagine. Il BLOB {0} è del tipo '{1}'.  |
|  IncorrectImageBlobType  |  I BLOB del disco possono essere solo di tipo BLOB di pagine. Il BLOB {0} per il disco '{1}' è di tipo BLOB in blocchi.  |
|  IncorrectImageBlobType  |  I BLOB del disco possono essere solo di tipo BLOB di pagine. Il BLOB {0} è del tipo '{1}'.  |
|  InternalOperationError  |  Non è stato possibile risolvere l'account di archiviazione {0}. Verificare che è stato creato tramite hello Provider di risorse di archiviazione in hello stesso percorso hello della risorsa di calcolo.  |
|  InternalOperationError  |  Le attività di ricerca obiettivo {0} non sono riuscite.  |
|  InternalOperationError  |  Errore nella convalida hello del profilo di rete della macchina virtuale '{0}'.  |
|  InvalidAccountType  |  Hello AccountType {0} non è valido.  |
|  InvalidParameter  |  Hello valore del parametro {0} non è valido.  |
|  InvalidParameter  |  password amministratore Hello specificata non è consentita.  |
|  InvalidParameter  |  "la password di hello fornito deve essere compresa tra {0}, \ {1 \} caratteri e deve soddisfare almeno {2} di requisiti di complessità delle password seguenti hello: <ol><li> Contiene un carattere maiuscolo</li><li>Contiene un carattere minuscolo</li><li>Contiene una cifra numerica</li><li>Contiene un carattere speciale.</li></ol>  |
|  InvalidParameter  |  Hello nome utente amministratore specificato non è consentita.  |
|  InvalidParameter  |  Impossibile collegare un disco del sistema operativo esistente se hello macchina virtuale viene creato da un'immagine della piattaforma o utente.  |
|  InvalidParameter  |  Il nome del contenitore {0} non è valido. I nomi dei contenitori devono avere una lunghezza compresa tra 3 e 63 caratteri e possono contenere solo caratteri alfanumerici minuscoli e trattini. Il trattino deve essere preceduto e seguito da un carattere alfanumerico.  |
|  InvalidParameter  |  Il nome del contenitore {0} nell'URL {1} non è valido. I nomi dei contenitori devono avere una lunghezza compresa tra 3 e 63 caratteri e possono contenere solo caratteri alfanumerici minuscoli e trattini. Il trattino deve essere preceduto e seguito da un carattere alfanumerico.  |
|  InvalidParameter  |  nome del blob Hello nell'URL {0} contiene una barra rovesciata. Questo carattere non è attualmente supportato per i dischi.  |
|  InvalidParameter  |  Hello URI {0} non ha l'aspetto toobe URI blob corretto.  |
|  InvalidParameter  |  Un disco denominato '{0}' già utilizzato hello stesso LUN: \\{1 \\}.  |
|  InvalidParameter  |  Un disco denominato '{0}' esiste già.  |
|  InvalidParameter  |  Non è possibile specificare l'immagine utente esegue l'override di un disco già definito in hello specificata dell'immagine di riferimento.  |
|  InvalidParameter  |  Un disco denominato '{0}' già utilizzato hello stesso \\{1 \\} URL VHD.  |
|  InvalidParameter  |  Hello {0} conteggio dominio di errore specificato deve essere compreso nell'intervallo di hello {1} too\ {2 \}.  |
|  InvalidParameter  |  tipo di licenza Hello {0} non è valido. I tipi di licenza validi sono: Windows_Client o Windows_Server, con distinzione tra maiuscole e minuscole.  |
|  InvalidParameter  |  Nome host Linux non può superare {0} caratteri o contenere i caratteri hello: \\{1 \\}.  |
|  InvalidParameter  |  Percorso di destinazione per le chiavi pubbliche Ssh è il valore predefinito di tooits attualmente limitata {0} tooa scadenza noto problema nell'agente di provisioning di Linux.  |
|  InvalidParameter  |  Esiste già un disco in corrispondenza del numero di unità logica (LUN) {0}.  |
|  InvalidParameter  |  Sottoscrizione {0} della richiesta di hello devono corrispondere \\{1 \\} sottoscrizione hello contenuta nell'id disco gestito hello.  |
|  InvalidParameter  |  I dati personalizzati in OSProfile devono essere con codifica Base 64 e con una lunghezza massima di {0} caratteri.  |
|  InvalidParameter  |  Il nome BLOB nell'URL {0} deve terminare con l'estensione '{1}'.  |
|  InvalidParameter  |  {0}' non è un prefisso del nome BLOB VHD acquisito valido. Un prefisso valido corrisponde a regex '{1}'.  |
|  InvalidParameter  |  Non è possibile aggiungere i certificati tooyour VM se l'agente VM hello non è disponibile.  |
|  InvalidParameter  |  Esiste già un disco in corrispondenza del numero di unità logica (LUN) {0}.  |
|  InvalidParameter  |  Impossibile toocreate hello VM perché hello richiesto {0} dimensioni non è disponibile nel cluster hello in cui il set di disponibilità hello è attualmente allocato. sono di dimensioni disponibili Hello: \\{1 \\}. Per altre informazioni sulla strategia di ridimensionamento delle macchine virtuali, vedere https://aka.ms/azure-resizevm.  |
|  InvalidParameter  |  Hello richiesto {0} dimensioni macchina virtuale non è disponibile nell'area corrente hello. dimensioni Hello disponibili nell'area corrente hello sono: \\{1 \\}. Ulteriori informazioni su dimensioni delle macchine Virtuali disponibili hello in ogni area in https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Hello richiesto {0} dimensioni macchina virtuale non è disponibile nell'area corrente hello. Ulteriori informazioni su dimensioni delle macchine Virtuali disponibili hello in ogni area in https://aka.ms/azure-regions.  |
|  InvalidParameter  |  Nome utente amministratore di Windows non può essere più di {0} caratteri long, terminano con un punto o contengono i caratteri hello: \\{1 \\}.  |
|  InvalidParameter  |  Nome del computer Windows non può essere più di {0} caratteri long, essere interamente numerico o contengono i caratteri hello: \\{1 \\}.  |
|  MissingMoveDependentResources  |  richiesta di spostamento delle risorse Hello non contiene tutte le risorse dipendenti hello. Controllare i dettagli dell'errore per individuare gli ID delle risorse mancanti.  |
|  MoveResourcesHaveInvalidState  |  richiesta di spostare risorse Hello contiene macchine virtuali che sono associate agli account di archiviazione non valido. Verificare i dettagli per questi ID di risorsa e per i nomi degli account di archiviazione di riferimento.  |
|  MoveResourcesHavePendingOperations  |  richiesta di spostamento delle risorse Hello contiene risorse per cui è in sospeso un'operazione. Controllare i dettagli per individuare gli ID di queste risorse. Ripetere l'operazione dopo il completamento di hello operazioni in sospeso.  |
|  MoveResourcesNotFound  |  Hello spostare le risorse richiesta contiene le risorse che non è state trovate. Controllare i dettagli per individuare gli ID di queste risorse.  |
|  NetworkingInternalOperationError  |  Errore di allocazione di rete sconosciuto.  |
|  NetworkingInternalOperationError  |  Errore di allocazione di rete sconosciuto.  |
|  NetworkingInternalOperationError  |  Si è verificato un errore interno durante l'elaborazione di profilo di rete della macchina virtuale hello.  |
|  NotFound  |  Impossibile trovare Hello {0} di Set di disponibilità.  |
|  NotFound  |  Macchina virtuale di origine '{0}' specificato nella richiesta di hello non esiste in questa posizione di Azure.  |
|  NotFound  |  Il tenant con ID {0} non è stato trovato.  |
|  NotFound  |  Impossibile trovare l'immagine di Hello {0}.  |
|  NotSupported  |  tipo di licenza Hello è {0}, ma hello \\{1 \\} blob di immagini non è locale.  |
|  OperationNotAllowed  |  Il set di disponibilità {0} non può essere eliminato. Prima di eliminare un set di disponibilità, verificare che non contenga macchine virtuali.  |
|  OperationNotAllowed  |  Modifica la disponibilità di set di SKU dal too'Classic 'Aligned' ' non è consentito.  |
|  OperationNotAllowed  |  Impossibile modificare le estensioni nella macchina virtuale hello quando hello VM non è in esecuzione.  |
|  OperationNotAllowed  |  azione di acquisizione Hello è supportato solo in una macchina virtuale con dischi basati su blob. Utilizzare toocreate le API di risorsa 'Immagine' hello un'immagine da una macchina virtuale gestito.  |
|  OperationNotAllowed  |  Impossibile creare risorse Hello {0} da \\{1 \\} immagine fino a quando l'immagine sia stata creata.  |
|  OperationNotAllowed  |  TooencryptionSettings gli aggiornamenti non è consentita quando macchina virtuale viene allocata riprovare dopo la deallocazione della macchina virtuale  |
|  OperationNotAllowed  |  Aggiunta di un tooa disco gestito macchina virtuale con dischi di base di blob non è supportata.  |
|  OperationNotAllowed  |  numero massimo di Hello di dischi di dati consentito tooa toobe collegato VM di questa dimensione è {0}.  |
|  OperationNotAllowed  |  Aggiunta di un tooVM disco blob di base con dischi gestiti non è supportata.  |
|  OperationNotAllowed  |  Operazione '{0}' non è consentita nell'immagine '\\{1 \\}' poiché hello che immagine è contrassegnata per l'eliminazione. È possibile ripetere l'operazione di eliminazione hello (o attendere un uno toocomplete in corso).  |
|  OperationNotAllowed  |  Operazione '{0}' non è consentita nella macchina virtuale '\\{1 \\}' poiché hello che macchina virtuale è generalizzata.  |
|  OperationNotAllowed  |  L'operazione '{0}' non è consentita perché la raccolta di punti di ripristino '{1}' è contrassegnata per l'eliminazione.  |
|  OperationNotAllowed  |  L'operazione '{0}' non è consentita nell'estensione della macchina virtuale '{1}' perché è contrassegnata per l'eliminazione. È possibile ripetere l'operazione di eliminazione hello (o attendere un uno toocomplete in corso).  |
|  OperationNotAllowed  |  L'operazione '{0}' non è consentita perché le macchine virtuali hello '\\{1 \\}' sono in corso il provisioning usando {2}' hello immagine'.  |
|  OperationNotAllowed  |  L'operazione '{0}' non è consentita perché hello ScaleSet macchina virtuale '\\{1 \\}' è attualmente in uso hello '{2}' immagine.  |
|  OperationNotAllowed  |  Operazione '{0}' non è consentita nella macchina virtuale '\\{1 \\}' poiché hello che macchina virtuale è contrassegnato per l'eliminazione. È possibile ripetere l'operazione di eliminazione hello (o attendere un uno toocomplete in corso).  |
|  OperationNotAllowed  |  Operazione '{0}' non è consentita nella macchina virtuale '\\{1 \\}' poiché hello macchina virtuale è deallocata o contrassegnata toobe deallocato.  |
|  OperationNotAllowed  |  Operazione '{0}' non è consentita nella macchina virtuale '\\{1 \\}' poiché hello che macchina virtuale è in esecuzione. . Spegnimento in modo esplicito nel caso in cui si arresta hello VM dal sistema operativo guest di hello.  |
|  OperationNotAllowed  |  Operazione '{0}' non è consentita nella macchina virtuale '\\{1 \\}' poiché hello che VM non viene deallocata.  |
|  OperationNotAllowed  |  L'operazione '{0}' non è consentita nella macchina virtuale '{1}' perché l'estensione '{2}' della macchina virtuale presenta uno stato di errore.  |
|  OperationNotAllowed  |  L'operazione '{0}' non è consentita nella macchina virtuale '{1}' perché è in esecuzione un'altra operazione.  |
|  OperationNotAllowed  |  operazione di Hello '{0}' richiede hello macchina virtuale '\\{1 \\}' toobe generalizzato.  |
|  OperationNotAllowed  |  operazione Hello richiede hello toobe di macchina virtuale in esecuzione (o set toorun).  |
|  OperationNotAllowed  |  Disco con dimensioni di {0} GB, che è di dimensioni inferiori a quelle di hello {1}GB del disco corrispondente nell'immagine, non è consentita.  |
|  OperationNotAllowed  |  È possibile aggiungere le estensioni di Set di scalabilità della macchina virtuale del gestore '{0}' solo in fase di hello della creazione di Set di scalabilità della macchina virtuale.  |
|  OperationNotAllowed  |  Le estensioni di Set di scalabilità della macchina virtuale del gestore '{0}' possono essere eliminate solo in fase di hello di eliminazione di Set di scalabilità della macchina virtuale.  |
|  OperationNotAllowed  |  La macchina virtuale '{0}' usa già dischi gestiti.  |
|  OperationNotAllowed  |  Macchina virtuale '{0}' appartiene too'Classic' "\\{1 \\}" set di disponibilità. Aggiornamento hello disponibilità impostare toouse 'Aligned' SKU, quindi ripetere hello conversione.  |
|  OperationNotAllowed  |  La macchina virtuale creata dall'immagine non può contenere dischi basati su BLOB. Tutti i dischi sono dischi toobe gestiti.  |
|  OperationNotAllowed  |  Acquisire non è possibile completare l'operazione perché hello VM non è generalizzata.  |
|  OperationNotAllowed  |  Poiché i dischi di macchina virtuale vengono convertiti toomanaged dischi, non sono consentite operazioni di gestione nella macchina virtuale '{0}'.  |
|  OperationNotAllowed  |  Un'operazione in corso è la modifica di stato di alimentazione della macchina virtuale {0} too\ {1 \}. Eseguire l'operazione {2} più tardi.  |
|  OperationNotAllowed  |  Non è possibile tooadd o aggiornamento hello macchina virtuale. Hello richiesto {0} dimensioni macchina virtuale potrebbe non essere disponibile nell'unità di allocazione esistenti hello. Per altre informazioni sulla strategia di ridimensionamento delle macchine virtuali, vedere https://aka.ms/azure-resizevm.  |
|  OperationNotAllowed  |  Impossibile tooresize hello VM perché hello richiesto {0} dimensioni non è disponibile nel cluster hello in cui il set di disponibilità hello è attualmente allocato. sono di dimensioni disponibili Hello: \\{1 \\}. Per altre informazioni sulla strategia di ridimensionamento delle macchine virtuali, vedere https://aka.ms/azure-resizevm.  |
|  OperationNotAllowed  |  Non è possibile tooresize hello VM perché hello richiesto {0} dimensioni non è disponibile in cluster hello in hello macchina virtuale è attualmente allocato. tooresize il too\ VM {1 \}. deallocare (questo è l'operazione di arresto nel portale di Azure hello) e riprovare hello ridimensionamento. Per altre informazioni sulla strategia di ridimensionamento delle macchine virtuali, vedere https://aka.ms/azure-resizevm.  |
|  OSProvisioningClientError  |  Provisioning del sistema operativo non riuscita per la macchina virtuale '{0}' perché il sistema operativo guest hello è attualmente in corso il provisioning.  |
|  OSProvisioningClientError  |  Il provisioning del sistema operativo per la macchina virtuale '{0}' non è riuscito. Dettagli errore: \\{1 \\} Crea immagine hello che sia stata preparata correttamente (generalizzata). <ul><li>Istruzioni per Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/  </li></ul> |
|  OSProvisioningClientError  |  La generazione della chiave host SSH non è riuscita. Dettagli sull'errore: {0}. tooresolve il problema, verificare se l'agente Linux è configurato correttamente. <ul><li>È possibile controllare istruzioni hello: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-agent-user-guide/ </li></ul> |
|  OSProvisioningClientError  |  Specificare il nome utente per hello che VM non è valido per la distribuzione di Linux. Dettagli sull'errore: {0}.  |
|  OSProvisioningInternalError  |  Provisioning del sistema operativo non riuscita per la macchina virtuale '{0}' a causa di errore interno tooan.  |
|  OSProvisioningTimedOut  |  Provisioning del sistema operativo per la macchina virtuale '{0}' non è terminata in hello tempo assegnato. Hello VM può comunque completare il provisioning. Controllare lo stato del provisioning più tardi.  |
|  OSProvisioningTimedOut  |  Provisioning del sistema operativo per la macchina virtuale '{0}' non è terminata in hello tempo assegnato. Hello VM può comunque completare il provisioning. Controllare lo stato del provisioning più tardi. Inoltre, assicurarsi che l'immagine di hello è stata preparata correttamente (generalizzata).   <ul><li>Istruzioni per Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Istruzioni per Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OSProvisioningTimedOut  |  Provisioning del sistema operativo per la macchina virtuale '{0}' non è terminata in hello tempo assegnato. Tuttavia, l'agente guest VM hello è stato in esecuzione. Ciò suggerisce guest hello OS non è stato correttamente preparato toobe utilizzata come immagine di macchina virtuale (con CreateOption = FromImage). tooresolve questo problema, entrambi hello Usa disco rigido virtuale, come nel caso con CreateOption = Attach o preparare correttamente per l'utilizzo come immagine:   <ul><li>Istruzioni per Windows: https://azure.microsoft.com/documentation/articles/virtual-machines-windows-upload-image/ </li><li> Istruzioni per Linux: https://azure.microsoft.com/documentation/articles/virtual-machines-linux-capture-image/</li></ul>  |
|  OverConstrainedAllocationRequest  |  Hello necessario dimensioni della macchina virtuale non sono attualmente disponibile nel percorso hello selezionato.  |
|  ResourceUpdateBlockedOnPlatformUpdate  |  Risorsa non è possibile aggiornare in questo momento a causa di aggiornamento della piattaforma tooongoing. Riprovare più tardi.  |
|  StorageAccountLimitation  |  Account di archiviazione '{0}' non supporta i BLOB di pagine che sono necessari toocreate dischi.  |
|  StorageAccountLimitation  |  L'account di archiviazione '{0}' ha superato la quota allocata.  |
|  StorageAccountLocationMismatch  |  Non è stato possibile risolvere l'account di archiviazione {0}. Verificare che è stato creato tramite hello Provider di risorse di archiviazione in hello stesso percorso hello della risorsa di calcolo.  |
|  StorageAccountNotFound  |  L'account di archiviazione {0} non è stato trovato. Verificare l'account di archiviazione non viene eliminato e appartiene toohello stesso percorso hello VM Azure.  |
|  StorageAccountNotRecognized  |  Usare un account di archiviazione gestito dal provider delle risorse di archiviazione. L'uso di {0} non è supportato.  |
|  StorageAccountOperationInternalError  |  Si è verificato un errore interno durante l'accesso all'account di archiviazione {0}.  |
|  StorageAccountSubscriptionMismatch  |  Account di archiviazione {0} non appartiene \\{1 \\} toosubscription.  |
|  StorageAccountTooBusy  |  L'account di archiviazione '{0}' è attualmente occupato. Valutare l'uso di un altro account.  |
|  StorageAccountTypeNotSupported  |  Il disco {0} usa {1} che è un account di archiviazione BLOB. Riprovare con un account di archiviazione per utilizzo generico.  |
|  StorageAccountTypeNotSupported  |  L'account di archiviazione {0} è di tipo {1}. La diagnostica di avvio supporta account di archiviazione di tipo {2}.  |
|  SubscriptionNotAuthorizedForImage  |  sottoscrizione di Hello non è autorizzato.  |
|  TargetDiskBlobAlreadyExists  |  Il BLOB {0} esiste già. Fornire un toocreate URI blob diverso una nuova data vuoto disco '\\{1 \\}'.  |
|  TargetDiskBlobAlreadyExists  |  Acquisire non è possibile continuare l'operazione perché {0} blob immagine di destinazione esiste già e BLOB VHD toooverwrite di hello flag non è impostata. Eliminare il blob hello o impostare il flag di hello BLOB VHD toooverwrite e riprovare.  |
|  TargetDiskBlobAlreadyExists  |  L'operazione di acquisizione non può continuare perché il BLOB dell'immagine di destinazione {0} contiene un lease attivo.   |
|  TargetDiskBlobAlreadyExists  |  Il BLOB {0} esiste già. Specificare un URI BLOB diverso come destinazione per il disco '{1}'.  |
|  TooManyVMRedeploymentRequests  |  Numero eccessivo di richieste di ridistribuzione sono stati ricevuti per la macchina virtuale '{0}' o le macchine virtuali hello in hello stesso set di disponibilità di questa macchina virtuale. Riprovare più tardi.  |
|  VHDSizeInvalid  |  Hello è specificato il valore di dimensioni del disco di {0} per il disco '\\{1 \\}' con blob {2} non è valido. La dimensione del disco deve essere compresa tra {3} e {4}.  |
|  VMAgentStatusCommunicationError  |  La macchina virtuale '{0}' non ha segnalato lo stato per le estensioni o l'agente di macchine virtuali. Verificare hello VM è un agente di macchine Virtuali in esecuzione e può stabilire archiviazione tooAzure le connessioni in uscita.  |
|  VMArtifactRepositoryInternalError  |  Si è verificato un errore durante la comunicazione con hello repository tooretrieve VM artefatto i dettagli sull'elemento.  |
|  VMArtifactRepositoryInternalError  |  Si è verificato un errore interno durante il recupero di dati dell'elemento hello VM dal repository di artefatti hello.  |
|  VMExtensionHandlerNonTransientError  |  Il gestore '{0}' ha segnalato un errore per l'estensione '{1}' della macchina virtuale con codice di errore terminale '{2}' e messaggio di errore '{3}'  |
|  VMExtensionManagementInternalError  |  Si è verificato un errore interno durante l'elaborazione dell'estensione della macchina virtuale '{0}'.  |
|  VMExtensionManagementInternalError  |  Si sono verificati più errori durante la preparazione delle estensioni VM hello. Per informazioni, vedere la visualizzazione dell'istanza dell'estensione della macchina virtuale.  |
|  VMExtensionProvisioningError  |  La macchina virtuale ha segnalato un errore durante l'elaborazione dell'estensione '{0}'. Messaggio di errore: "{1}".  |
|  VMExtensionProvisioningError  |  Più estensioni di macchina virtuale non è stato possibile toobe effettuato il provisioning in hello macchina virtuale. Visualizzazione dell'istanza estensione VM hello per informazioni dettagliate vedere.  |
|  VMExtensionProvisioningTimeout  |  Timeout del provisioning dell'estensione della macchina virtuale '{0}'. L'installazione dell'estensione ha richiesto troppo tempo oppure non è stato possibile ottenere lo stato dell'estensione.  |
|  VMMarketplaceInvalidInput  |  Creazione di una macchina virtuale da un'immagine non Marketplace non necessario le informazioni del piano, rimuovere hello informazioni sul piano nella richiesta di hello. Il nome del disco del sistema operativo è {0}.  |
|  VMMarketplaceInvalidInput  |  informazioni sull'acquisto di Hello non corrisponde. Non è possibile toodeploy dall'immagine del Marketplace hello. Il nome del disco del sistema operativo è {0}.  |
|  VMMarketplaceInvalidInput  |  La creazione di una macchina virtuale dall'immagine del Marketplace richiede informazioni sul piano nella richiesta di hello. Il nome del disco del sistema operativo è {0}.  |
|  VMNotFound  |  Hello macchina virtuale '{0}' non è possibile trovare.  |
|  VMRedeploymentFailed  |  Ridistribuzione di macchina virtuale '{0}' non è riuscita a causa di errore interno tooan. Riprovare più tardi.  |
|  VMRedeploymentTimedOut  |  Ridistribuzione della macchina virtuale '{0}' non è stata completata in hello tempo assegnato. È possibile che venga comunque completata in futuro. In caso contrario, è possibile ritentare la richiesta hello.  |
|  VMStartTimedOut  |  Macchina virtuale '{0}' non è stato avviato in hello tempo assegnato. Hello VM può comunque essere avviata. Verificare lo stato di alimentazione hello in un secondo momento.  |


## <a name="next-steps"></a>Passaggi successivi
Se è necessario ulteriore assistenza, è possibile contattare hello Azure esperti in [hello forum MSDN di Azure e di Overflow dello Stack](https://azure.microsoft.com/support/forums/). In alternativa, è possibile archiviare un evento imprevisto di supporto tecnico di Azure. Passare toohello [sito del supporto tecnico di Azure](https://azure.microsoft.com/support/options/) e selezionare **ottenere supporto**.
