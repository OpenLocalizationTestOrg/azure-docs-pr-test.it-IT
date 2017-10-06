---
title: Crittografia lato aaaClient con Python per archiviazione di Microsoft Azure | Documenti Microsoft
description: Hello Azure Storage Client Library per Python supporta la crittografia lato client per garantire la massima sicurezza per le applicazioni di servizio di archiviazione Azure.
services: storage
documentationcenter: python
author: lakasa
manager: jahogg
editor: tysonn
ms.assetid: f9bf7981-9948-4f83-8931-b15679a09b8a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 05/11/2017
ms.author: lakasa
ms.openlocfilehash: 3a52b64f93daf85a55308f8a4bee9c98b2315d4f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-with-python-for-microsoft-azure-storage"></a>Crittografia lato client con Python per Archiviazione di Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Panoramica
Hello [Azure Storage Client Library per Python](https://pypi.python.org/pypi/azure-storage) supporta la crittografia dei dati all'interno delle applicazioni client prima di caricare tooAzure Storage e la decrittografia dei dati durante il download toohello client.

> [!NOTE]
> libreria Python di archiviazione di Azure Hello è in anteprima.
> 
> 

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Crittografia e decrittografia tramite una tecnica di busta hello
i processi di Hello di crittografia e decrittografia seguono tecnica busta hello.

### <a name="encryption-via-hello-envelope-technique"></a>Crittografia tramite una tecnica di busta hello
La crittografia tramite una tecnica di busta hello funziona nel seguente modo hello:

1. libreria client di archiviazione di Azure Hello genera una chiave di crittografia del contenuto (CEK), che è una chiave simmetrica con un utilizzo.
2. I dati utente vengono crittografati con questa chiave CEK.
3. Hello CEK viene eseguito il wrapping (crittografata) con chiave di crittografia della chiave hello (CHIAVI). Hello KEK è identificato da un identificatore di chiave e può essere una coppia di chiavi asimmetriche o di una chiave simmetrica, viene gestita in locale.
   libreria client di archiviazione Hello stessa non ha mai tooKEK di accesso. libreria Hello richiama chiave hello wrapping algoritmo viene fornito da hello KEK. Gli utenti possono scegliere toouse provider personalizzati per ritorno a capo/wrapping di una chiave se necessario.
4. Hello dati crittografati viene quindi caricato toohello servizio di archiviazione di Azure. Hello chiave incapsulata con alcuni metadati di crittografia aggiuntiva archiviati come metadati (in un blob) o interpolati con dati crittografato hello (messaggi in coda e le entità di tabella).

### <a name="decryption-via-hello-envelope-technique"></a>Decrittografia tramite una tecnica di busta hello
La decrittografia tramite una tecnica di busta hello funziona nel seguente modo hello:

1. libreria client Hello si presuppone che l'utente hello gestisce localmente chiave di crittografia della chiave hello (CHIAVI). utente Hello tooknow hello specifica chiave utilizzati per la crittografia non è necessario. In alternativa, è possibile impostare e utilizzato un resolver di chiave, che consente di risolvere identificatori di chiave diversi tookeys.
2. libreria client Hello Scarica i dati di crittografato hello insieme a qualsiasi materiale di crittografia che viene archiviato nel servizio hello.
3. chiave di crittografia del contenuto sottoposto a wrapping Hello (CEK) è annullato il wrapping (decrittografati) mediante hello chiave di crittografia della chiave (KEK). Qui, libreria client hello non dispone di accesso tooKEK. Richiama semplicemente algoritmo di wrapping hello provider personalizzato.
4. Hello contenuto chiave di crittografia (CEK) viene quindi utilizzato i dati utente crittografato hello toodecrypt.

## <a name="encryption-mechanism"></a>Meccanismo di crittografia
libreria client di archiviazione Hello Usa [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) dei dati utente tooencrypt ordine. In particolare, si avvale della modalità [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) con AES. Ogni servizio funziona in modo diverso, pertanto qui verrà illustrato ciascuno di essi.

### <a name="blobs"></a>Blobs
libreria client Hello supporta attualmente la crittografia dell'intero BLOB solo. In particolare, la crittografia è supportata quando gli utenti utilizzano hello **creare*** metodi. Per i download, sono supportati sia i download completi che quelli di intervallo ed è disponibile il calcolo parallelo dei download e degli upload.

Durante la crittografia, la libreria client di hello genererà un vettore di inizializzazione casuale (IV) di 16 byte, con una chiave di crittografia casuale del contenuto (CEK) di 32 byte ed eseguono la crittografia envelope dei dati blob hello utilizzando le informazioni. Hello inclusi CEK e alcuni metadati di crittografia supplementari vengono quindi archiviati come metadati insieme ai blob di crittografato hello sul servizio hello del blob.

> [!WARNING]
> Se si modifica o il caricamento dei metadati personalizzata per il blob hello, è necessario che questi metadati viene mantenuto tooensure. Se si caricano nuovi metadati senza metadati, hello CEK sottoposta a wrapping, IV e altri metadati andranno persi e il contenuto di blob hello mai possano essere recuperato.
> 
> 

Download di blob crittografato comporta il recupero del contenuto di hello dell'intero blob hello utilizzando hello **ottenere*** metodi pratici. Hello CEK sottoposta a wrapping viene estratta e utilizzato insieme hello IV (archiviati come metadati del blob in questo caso) tooreturn hello decrittografata dati toohello utenti.

Download di un intervallo arbitrario (**ottenere*** metodi con parametri intervallo passato) nelle hello blob crittografato comporta la modifica intervallo hello fornito dagli utenti in ordine tooget una piccola quantità di dati aggiuntivi che possono essere utilizzati toosuccessfully decrypt hello l'intervallo richiesto.

I BLOB in blocchi e BLOB di pagine possono essere crittografati/decrittografati solamente con questo schema. Attualmente non è disponibile nessun supporto per la crittografia dei blob di accodamento.

### <a name="queues"></a>Code
Poiché i messaggi in coda possono essere di qualsiasi formato, la libreria client di hello definisce un formato personalizzato che include hello vettore di inizializzazione (IV) e la chiave di crittografia del contenuto crittografato hello (CEK) nel testo del messaggio hello.

Durante la crittografia libreria client hello genera un vettore di Inizializzazione casuale di 16 byte con una CEK casuale di 32 byte ed esegue la crittografia envelope hello coda del testo del messaggio utilizzando le informazioni. Hello inclusi CEK e alcuni metadati di crittografia supplementari vengono quindi aggiunti messaggio della coda crittografati toohello. Questo messaggio modificato (mostrato sotto) verrà archiviato nel servizio hello.

```
<MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>
```

Durante la decrittografia, la chiave incapsulata hello è estratto dal messaggio in coda hello ed estratta. IV Hello è inoltre estratto dal messaggio in coda hello e utilizzato insieme ai dati di messaggio della coda di hello estratta toodecrypt chiave hello. Si noti che i metadati crittografia hello sono piccolo (in byte) 500, in modo mentre tiene conto per il limite di 64KB hello per un messaggio nella coda, impatto hello debba essere gestito.

### <a name="tables"></a>Tabelle
Hello client libreria supporta la crittografia delle proprietà di entità per l'inserimento e sostituire operazioni.

> [!NOTE]
> L’unione non è attualmente supportata. Poiché un subset delle proprietà è stato crittografato in precedenza usando una chiave diversa, semplicemente l'unione di nuove proprietà hello e l'aggiornamento dei metadati hello comporterà la perdita di dati. L'unione di uno, è necessario rendere servizio aggiuntivo chiama entità preesistente di hello tooread dal servizio hello o utilizzando una nuova chiave per ogni proprietà, che non sono adatti per motivi di prestazioni.
> 
> 

La crittografia dei dati della tabella funziona nel modo seguente:

1. Gli utenti specificano toobe proprietà hello crittografati.
2. libreria client Hello genera un vettore di inizializzazione casuale (IV) di 16 byte con una chiave di crittografia casuale del contenuto (CEK) di 32 byte per ogni entità ed esegue la crittografia envelope toobe singole proprietà hello crittografati mediante la derivazione di un vettore di Inizializzazione per proprietà. proprietà crittografato Hello viene archiviato come dati binari.
3. Hello inclusi CEK e alcuni metadati di crittografia supplementari vengono quindi archiviati come due proprietà riservate aggiuntive. Hello prima proprietà riservata (\_ClientEncryptionMetadata1) è una proprietà stringa che contiene informazioni hello IV, versione e la chiave sottoposta a wrapping. proprietà riservata secondo Hello (\_ClientEncryptionMetadata2) è una proprietà binaria che contiene le informazioni sulle proprietà hello crittografati hello. informazioni contenute in questa seconda proprietà Hello (\_ClientEncryptionMetadata2) è crittografata.
4. Scadenza toothese riservato proprietà aggiuntive richieste per la crittografia, gli utenti possono hanno proprietà personalizzate solo 250 anziché 252. dimensioni totali di Hello dell'entità hello devono essere minore di 1MB.
   
   Si noti che solo le proprietà di stringa possono essere crittografate. Se altri tipi di proprietà toobe crittografati, devono essere toostrings convertito. crittografato Hello sono archiviate nel servizio hello come proprietà binarie e vengono convertiti toostrings indietro (stringhe non elaborate, non EntityProperties con tipo EdmType.STRING) dopo la decrittografia.
   
   Per le tabelle, inoltre i criteri di crittografia toohello, gli utenti devono specificare toobe proprietà hello crittografati. Questa operazione può essere eseguita archiviando entrambe queste proprietà in oggetti TableEntity con hello tipo set tooEdmType.STRING e crittografare set tootrue o impostazione hello encryption_resolver_function sull'oggetto tableservice hello. Un resolver di crittografia è una funzione che accetta una chiave di partizione, una chiave di riga e un nome di proprietà e restituisce un valore booleano che indica se tale proprietà deve essere crittografata. Durante la crittografia, la libreria client di hello utilizzerà questo toodecide informazioni se una proprietà deve essere crittografata durante la scrittura di transito toohello. delegato di Hello fornisce anche la possibilità di hello di logica per la modalità di crittografia delle proprietà. (Ad esempio, se X, quindi crittografa la proprietà A; in caso contrario crittografa le proprietà A e B). Si noti che è necessario non tooprovide queste informazioni durante la lettura o di una query sulle entità.

### <a name="batch-operations"></a>Operazioni batch
Un criterio di crittografia si applica tooall righe nel batch hello. libreria client Hello internamente genererà un nuovo vettore di Inizializzazione casuale e una CEK casuale per ogni riga nel batch hello. Utenti possono inoltre scegliere tooencrypt proprietà diverse per ogni operazione nel batch hello mediante la definizione di questo comportamento nel sistema di risoluzione crittografia hello.
Se un batch viene creato un Manager di contesto tramite metodo batch() tableservice di hello, criteri di crittografia del tableservice hello verranno automaticamente applicati toohello batch. Se viene creato un batch in modo esplicito chiamando il costruttore di hello, criteri di crittografia hello devono essere passato come parametro e non modificato per la durata di hello del batch hello sinistra.
Si noti che le entità vengono crittografate come essi vengono inseriti nel batch di hello tramite criteri di crittografia del batch hello (entità non vengono crittografate in fase di commit di batch di hello tramite criteri di crittografia del tableservice hello di hello).

### <a name="queries"></a>Query
operazioni di query tooperform, è necessario specificare un resolver di chiave che è in grado di tooresolve tutti hello chiavi nel set di risultati hello. Se un'entità inclusa nel risultato della query hello non può essere risolto tooa provider, la libreria client di hello genererà un errore. Per le query che esegue le proiezioni lato server, la libreria client di hello aggiungerà proprietà dei metadati di crittografia speciali hello (\_ClientEncryptionMetadata1 e \_ClientEncryptionMetadata2) per impostazione predefinita toohello colonne selezionate. .

> [!IMPORTANT]
> Quando si utilizza la crittografia lato client, tenere presente i seguenti aspetti importanti:
> 
> * Quando la scrittura o lettura dal tooan crittografati blob, usare i comandi di caricamento di tutto il blob e i comandi di download di intervallo/intero blob. Evitare di scrivere tooan blob crittografato tramite operazioni di protocollo, ad esempio inserire blocco, inserire elenco di blocchi, scrivere pagine o Cancella pagine. in caso contrario è possibile danneggiare blob crittografato hello e renderlo illeggibile.
> * Per le tabelle esiste un vincolo simile. Essere toonot attenzione aggiornamento crittografato proprietà senza aggiornare i metadati di crittografia hello.
> * Se si impostano i metadati sul blob crittografato hello, si potrebbero sovrascrivere hello relative a crittografia metadati richiesti per la decrittografia, poiché l'impostazione dei metadati non additivo. Ciò vale anche per gli snapshot; evitare di specificare i metadati durante la creazione di uno snapshot di un BLOB crittografato. Se è necessario impostare i metadati, hello toocall assicurarsi di essere **get_blob_metadata** tooget primo metodo hello i metadati di crittografia corrente ed evitare di scritture simultanee durante l'impostazione di metadati.
> * Abilitare hello **require_encryption** flag hello oggetto del servizio per gli utenti che dovrebbero funzionare solo con i dati crittografati. Per ulteriori informazioni, vedere di seguito.
> 
> 

libreria client di archiviazione Hello prevede hello fornito KEK e resolver chiave hello tooimplement interfaccia seguente. [insieme di credenziali delle chiavi di Azure](https://azure.microsoft.com/services/key-vault/) per la gestione delle chiavi KEK per Python è in sospeso e verrà integrato in questa libreria al termine del completamento.

## <a name="client-api--interface"></a>API client/interfaccia
Dopo aver creato un oggetto servizio di archiviazione (ad esempio blockblobservice), hello utente può assegnare valori toohello campi che costituiscono un criterio di crittografia: key_encryption_key, key_resolver_function e require_encryption. Gli utenti possono fornire solo una chiave KEK, solo un resolver o entrambi. key_encryption_key è hello chiave tipo di base che è identificato mediante un identificatore di chiave e che fornisce la logica di hello per ritorno a capo/annullamento del wrapping. key_resolver_function è tooresolve usato una chiave durante il processo di decrittografia hello. Restituisce una chiave KEK valida in base a un identificatore di chiave. In questo modo gli utenti hello possibilità toochoose tra più chiavi che vengono gestiti in più posizioni.

Hello KEK deve implementare seguente hello toosuccessfully metodi crittografare i dati:

* wrap_key(cek): esegue il wrapping hello specificato CEK (byte) utilizzando un algoritmo hello scelto dall'utente. Hello restituisce eseguito il wrapping di chiave.
* get_key_wrap_algorithm(): utilizzato l'algoritmo di hello restituisce toowrap chiavi.
* get_kid(): id chiave restituisce hello stringa per questa chiave di scambio delle CHIAVI.
  Hello KEK deve implementare hello metodi toosuccessfully decrittografare i dati seguenti:
* unwrap_key (cek, algoritmo): restituisce hello rimosso wrapping del modulo di hello specificato utilizzando l'algoritmo specificato dalla stringa hello CEK.
* get_kid(): restituisce un ID chiave stringa per questa chiave KEK.

resolver chiave Hello deve implementare almeno un metodo che, dato un id chiave, restituisce hello KEK implementazione hello interfaccia corrispondente precedente. Solo questo metodo è toobe assegnata toohello key_resolver_function proprietà nell'oggetto servizio hello.

* Per la crittografia, hello usata sempre e assenza hello di una chiave si verificherà un errore.
* Per la decrittografia:
  
  * resolver chiave Hello viene richiamato se chiave hello tooget specificato. Se il resolver hello viene specificato, ma non dispone di un mapping per l'identificatore di chiave hello, viene generato un errore.
  * Se il sistema di risoluzione non è specificato, ma viene specificata una chiave, chiave hello viene utilizzato se il relativo identificatore corrisponde identificatore di chiave hello necessario. Se l'identificatore hello non corrisponde, viene generato un errore.
    
    Negli esempi di crittografia azure.storage.samples Hello <fix URL>viene illustrato uno scenario end-to-end più dettagliato per BLOB, code e tabelle.
      Esempi di implementazione del resolver chiave e hello KEK sono fornite nei file di esempio hello come KeyWrapper e KeyResolver rispettivamente.

### <a name="requireencryption-mode"></a>Modalità RequireEncryption
Gli utenti possono facoltativamente abilitare una modalità operativa quando tutte le operazioni di caricamento e download devono essere crittografate. In questa modalità, avrà esito negativo tentativi tooupload dati senza una crittografia criteri o scaricare dati che non vengono crittografati nel servizio hello client hello. Hello **require_encryption** flag hello servizio oggetto controlla questo comportamento.

### <a name="blob-service-encryption"></a>Crittografia del servizio BLOB
Impostare i campi dei criteri di crittografia hello hello blockblobservice oggetto. Tutti gli altri verranno gestiti dalla libreria client hello internamente.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_block_blob_service.key_encryption_key = kek
my_block_blob_service.key_resolver_funcion = key_resolver.resolve_key

# Upload hello encrypted contents toohello blob.
my_block_blob_service.create_blob_from_stream(container_name, blob_name, stream)

# Download and decrypt hello encrypted contents from hello blob.
blob = my_block_blob_service.get_blob_to_bytes(container_name, blob_name)
```

### <a name="queue-service-encryption"></a>Crittografia del servizio di accodamento
Impostare i campi dei criteri di crittografia hello hello queueservice oggetto. Tutti gli altri verranno gestiti dalla libreria client hello internamente.

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Set hello KEK and key resolver on hello service object.
my_queue_service.key_encryption_key = kek
my_queue_service.key_resolver_funcion = key_resolver.resolve_key

# Add message
my_queue_service.put_message(queue_name, content)

# Retrieve message
retrieved_message_list = my_queue_service.get_messages(queue_name)
```

### <a name="table-service-encryption"></a>Crittografia del servizio tabelle
Inoltre toocreating un criterio di crittografia e l'impostazione in Opzioni di richiesta, è necessario specificare un **encryption_resolver_function** su hello **tableservice**, o set hello crittografare l'attributo in Hello EntityProperty.

### <a name="using-hello-resolver"></a>Mediante resolver hello

```python
# Create hello KEK used for encryption.
# KeyWrapper is hello provided sample implementation, but hello user may use their own object as long as it implements hello interface above.
kek = KeyWrapper('local:key1') # Key identifier

# Create hello key resolver used for decryption.
# KeyResolver is hello provided sample implementation, but hello user may use whatever implementation they choose so long as hello function set on hello service object behaves appropriately.
key_resolver = KeyResolver()
key_resolver.put_key(kek)

# Define hello encryption resolver_function.
def my_encryption_resolver(pk, rk, property_name):
        if property_name == 'foo':
                return True
        return False

# Set hello KEK and key resolver on hello service object.
my_table_service.key_encryption_key = kek
my_table_service.key_resolver_funcion = key_resolver.resolve_key
my_table_service.encryption_resolver_function = my_encryption_resolver

# Insert Entity
my_table_service.insert_entity(table_name, entity)

# Retrieve Entity
# Note: No need toospecify an encryption resolver for retrieve, but it is harmless tooleave hello property set.
my_table_service.get_entity(table_name, entity['PartitionKey'], entity['RowKey'])
```

### <a name="using-attributes"></a>Utilizzo di attributi
Come indicato in precedenza, una proprietà può essere contrassegnata per la crittografia archiviandoli in un oggetto EntityProperty e impostazione hello crittografare campo.

```python
encrypted_property_1 = EntityProperty(EdmType.STRING, value, encrypt=True)
```

## <a name="encryption-and-performance"></a>Crittografia e prestazioni
Si noti che la crittografia dei dati di archiviazione restituisce un overhead delle prestazioni aggiuntivo. Hello contenuto chiave e vettore di Inizializzazione deve essere generato, contenuto hello deve essere crittografato e i metadati aggiuntivi devono essere formattati e caricati. Questo overhead variano a seconda della quantità di hello dei dati da crittografare. È consigliabile che i clienti testano sempre le proprie applicazioni per le prestazioni durante lo sviluppo.

## <a name="next-steps"></a>Passaggi successivi
* Scaricare hello [Azure Storage Client Library per il pacchetto di PyPi Java](https://pypi.python.org/pypi/azure-storage)
* Scaricare hello [Azure Storage Client Library per il codice sorgente di Python da GitHub](https://github.com/Azure/azure-storage-python)
