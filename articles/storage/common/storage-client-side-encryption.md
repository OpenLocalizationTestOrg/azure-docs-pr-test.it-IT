---
title: la crittografia lato aaaClient con .NET per l'archiviazione di Microsoft Azure | Documenti Microsoft
description: Hello Azure Storage Client Library per .NET supporta la crittografia lato client e l'integrazione con l'insieme di credenziali chiave di Azure per garantire la massima sicurezza per le applicazioni di servizio di archiviazione Azure.
services: storage
documentationcenter: .net
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: becfccca-510a-479e-a798-2044becd9a64
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: robinsh
ms.openlocfilehash: c09246f43801e17aff96ea453182d11ffbf5e420
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="client-side-encryption-and-azure-key-vault-for-microsoft-azure-storage"></a>Crittografia lato client e Insieme di credenziali chiave Azure per Archiviazione di Microsoft Azure
[!INCLUDE [storage-selector-client-side-encryption-include](../../../includes/storage-selector-client-side-encryption-include.md)]

## <a name="overview"></a>Panoramica
Hello [Azure Storage Client Library per il pacchetto Nuget .NET](https://www.nuget.org/packages/WindowsAzure.Storage) supporta la crittografia dei dati all'interno delle applicazioni client prima di caricare tooAzure Storage e la decrittografia dei dati durante il download toohello client. libreria Hello supporta anche l'integrazione con [insieme credenziali chiavi Azure](https://azure.microsoft.com/services/key-vault/) per la gestione di chiave account di archiviazione.

Per un'esercitazione dettagliata che ti assista hello processo di crittografia di oggetti BLOB usando la crittografia lato client e l'insieme di credenziali chiave di Azure, vedere [crittografa e decrittografa i BLOB in archiviazione di Microsoft Azure con insieme credenziali chiavi Azure](../blobs/storage-encrypt-decrypt-blobs-key-vault.md).

Per la crittografia sul lato client con Java, vedere [Crittografia sul lato client con Java per l'Archiviazione di Microsoft Azure](storage-client-side-encryption-java.md).

## <a name="encryption-and-decryption-via-hello-envelope-technique"></a>Crittografia e decrittografia tramite una tecnica di busta hello
i processi di Hello di crittografia e decrittografia seguono tecnica busta hello.

### <a name="encryption-via-hello-envelope-technique"></a>Crittografia tramite una tecnica di busta hello
La crittografia tramite una tecnica di busta hello funziona nel seguente modo hello:

1. libreria client di archiviazione di Azure Hello genera una chiave di crittografia del contenuto (CEK), che è una chiave simmetrica con un utilizzo.
2. I dati utente vengono crittografati con questa chiave CEK.
3. Hello CEK viene eseguito il wrapping (crittografata) con chiave di crittografia della chiave hello (CHIAVI). Hello KEK è identificato da un identificatore di chiave e può essere una coppia di chiavi asimmetriche o di una chiave simmetrica e possono essere gestito in locale o memorizzato in insiemi di credenziali chiave di Azure.
   
    libreria client di archiviazione Hello stessa non ha mai tooKEK di accesso. libreria Hello richiama l'algoritmo di wrapping delle chiavi hello fornito dall'insieme di credenziali chiave. Gli utenti possono scegliere toouse provider personalizzati per ritorno a capo/wrapping di una chiave se necessario.

4. Hello dati crittografati viene quindi caricato toohello servizio di archiviazione di Azure. Hello chiave incapsulata con alcuni metadati di crittografia aggiuntiva archiviati come metadati (in un blob) o interpolati con dati crittografato hello (messaggi in coda e le entità di tabella).

### <a name="decryption-via-hello-envelope-technique"></a>Decrittografia tramite una tecnica di busta hello
La decrittografia tramite una tecnica di busta hello funziona nel seguente modo hello:

1. libreria client Hello si presuppone che l'utente hello gestisce chiave di crittografia della chiave hello (KEK) in locale o in insiemi di credenziali chiave di Azure. utente Hello tooknow hello specifica chiave utilizzati per la crittografia non è necessario. In alternativa, è possibile impostare e utilizzato un resolver di chiave che si risolve tookeys identificatori di chiave diversi.
2. libreria client Hello Scarica i dati di crittografato hello insieme a qualsiasi materiale di crittografia che viene archiviato nel servizio hello.
3. chiave di crittografia del contenuto sottoposto a wrapping Hello (CEK) è annullato il wrapping (decrittografati) mediante hello chiave di crittografia della chiave (KEK). Qui, libreria client hello non dispone di accesso tooKEK. Richiama semplicemente hello personalizzata o l'algoritmo di wrapping del provider dell'insieme di credenziali chiave.
4. Hello contenuto chiave di crittografia (CEK) viene quindi utilizzato i dati utente crittografato hello toodecrypt.

## <a name="encryption-mechanism"></a>Meccanismo di crittografia
libreria client di archiviazione Hello Usa [AES](http://en.wikipedia.org/wiki/Advanced_Encryption_Standard) dei dati utente tooencrypt ordine. In particolare, si avvale della modalità [Cipher Block Chaining (CBC)](http://en.wikipedia.org/wiki/Block_cipher_mode_of_operation#Cipher-block_chaining_.28CBC.29) con AES. Ogni servizio funziona in modo diverso, pertanto qui verrà illustrato ciascuno di essi.

### <a name="blobs"></a>Blobs
libreria client Hello supporta attualmente la crittografia dell'intero BLOB solo. In particolare, la crittografia è supportata quando gli utenti utilizzano hello **UploadFrom*** metodi o hello **OpenWrite** metodo. Per i download, sono supportati sia i download completi che di intervallo.

Durante la crittografia, la libreria client di hello genererà un vettore di inizializzazione casuale (IV) di 16 byte, con una chiave di crittografia casuale del contenuto (CEK) di 32 byte ed eseguono la crittografia envelope dei dati blob hello utilizzando le informazioni. Hello inclusi CEK e alcuni metadati di crittografia supplementari vengono quindi archiviati come metadati insieme ai blob di crittografato hello sul servizio hello del blob.

> [!WARNING]
> Se si modifica o il caricamento dei metadati personalizzata per il blob hello, è necessario che questi metadati viene mantenuto tooensure. Se si caricano nuovi metadati senza metadati, hello CEK sottoposta a wrapping, IV e altri metadati andranno persi e il contenuto di blob hello mai possano essere recuperato.
> 
> 

Download di blob crittografato comporta il recupero del contenuto di hello dell'intero blob hello utilizzando hello **DownloadTo***/**BlobReadStream** praticità metodi. Hello CEK sottoposta a wrapping viene estratta e utilizzato insieme hello IV (archiviati come metadati del blob in questo caso) tooreturn hello decrittografata dati toohello utenti.

Download di un intervallo arbitrario (**DownloadRange*** metodi) nelle hello blob crittografato comporta la modifica intervallo hello fornite dagli utenti in ordine tooget una piccola quantità di dati aggiuntivi che possono essere utilizzati toosuccessfully decrittografare hello intervallo richiesto.

Tutti i tipi di BLOB (BLOB in blocchi, BLOB di pagine e BLOB di accodamento) possono essere crittografati/decrittografati con questo schema.

### <a name="queues"></a>Code
Poiché i messaggi in coda possono essere di qualsiasi formato, la libreria client di hello definisce un formato personalizzato che include hello vettore di inizializzazione (IV) e la chiave di crittografia del contenuto crittografato hello (CEK) nel testo del messaggio hello.

Durante la crittografia libreria client hello genera un vettore di Inizializzazione casuale di 16 byte con una CEK casuale di 32 byte ed esegue la crittografia envelope hello coda del testo del messaggio utilizzando le informazioni. Hello inclusi CEK e alcuni metadati di crittografia supplementari vengono quindi aggiunti messaggio della coda crittografati toohello. Questo messaggio modificato (mostrato sotto) verrà archiviato nel servizio hello.

    <MessageText>{"EncryptedMessageContents":"6kOu8Rq1C3+M1QO4alKLmWthWXSmHV3mEfxBAgP9QGTU++MKn2uPq3t2UjF1DO6w","EncryptionData":{…}}</MessageText>

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
3. Hello inclusi CEK e alcuni metadati di crittografia supplementari vengono quindi archiviati come due proprietà riservate aggiuntive. proprietà riservata prima Hello (_ClientEncryptionMetadata1) è una proprietà stringa che contiene informazioni hello IV, versione e la chiave sottoposta a wrapping. proprietà riservata secondo Hello (_ClientEncryptionMetadata2) è una proprietà binaria che contiene le informazioni sulle proprietà hello crittografati hello. informazioni di Hello in questa seconda proprietà (_ClientEncryptionMetadata2) sono crittografata.
4. Scadenza toothese riservato proprietà aggiuntive richieste per la crittografia, gli utenti possono hanno proprietà personalizzate solo 250 anziché 252. dimensioni totali di Hello dell'entità hello devono essere minore di 1 MB.

Si noti che solo le proprietà di stringa possono essere crittografate. Se altri tipi di proprietà toobe crittografati, devono essere toostrings convertito. crittografato Hello sono archiviate nel servizio hello come proprietà binarie e vengono convertiti toostrings indietro dopo la decrittografia.

Per le tabelle, inoltre i criteri di crittografia toohello, gli utenti devono specificare toobe proprietà hello crittografati. Questa operazione può essere eseguita specificando un attributo [EncryptProperty] \(per le entità POCO che derivano da TableEntity) o un resolver di crittografia nelle opzioni di richiesta. Un resolver di crittografia è un delegato che accetta una chiave di partizione, una chiave di riga e un nome di proprietà e restituisce un valore booleano che indica se tale proprietà deve essere crittografata. Durante la crittografia, la libreria client di hello utilizzerà questo toodecide informazioni se una proprietà deve essere crittografata durante la scrittura di transito toohello. delegato di Hello fornisce anche la possibilità di hello di logica per la modalità di crittografia delle proprietà. (Ad esempio, se X, quindi crittografa la proprietà A; in caso contrario crittografa le proprietà A e B). Si noti che è necessario non tooprovide queste informazioni durante la lettura o di una query sulle entità.

### <a name="batch-operations"></a>Operazioni batch
Nelle operazioni batch, hello KEK stesso verrà usata in tutte le righe di hello in quell'operazione batch perché la libreria client di hello consente solo di un oggetto di opzioni (e pertanto un criterio/KEK) per ogni operazione batch. Tuttavia, la libreria client di hello internamente genererà un nuovo vettore di Inizializzazione casuale e una CEK casuale per ogni riga nel batch hello. Utenti possono inoltre scegliere tooencrypt proprietà diverse per ogni operazione nel batch hello mediante la definizione di questo comportamento nel sistema di risoluzione crittografia hello.

### <a name="queries"></a>Query
operazioni di query tooperform, è necessario specificare un resolver di chiave che è in grado di tooresolve tutti hello chiavi nel set di risultati hello. Se un'entità inclusa nel risultato della query hello non può essere risolto tooa provider, la libreria client di hello genererà un errore. Per le query eseguite sul lato server proiezioni, libreria client hello aggiungerà proprietà di metadati di crittografia speciali di hello (_ClientEncryptionMetadata1 e _ClientEncryptionMetadata2) dalle colonne toohello selezionato predefinito.

## <a name="azure-key-vault"></a>Insieme di credenziali chiave Azure
L'insieme di credenziali chiave di Azure consente di proteggere le chiavi e i segreti di crittografia usati da servizi e applicazioni cloud. Con l'insieme di credenziali chiave di Azure gli utenti possono crittografare chiavi e segreti (ad esempio, chiavi di autenticazione, chiavi dell'account di archiviazione, chiavi di crittografia dati, file PFX e password) usando chiavi protette da moduli di protezione hardware (HSM). Per altre informazioni, vedere [Informazioni sull’insieme di credenziali chiave di Azure](../../key-vault/key-vault-whatis.md)

libreria client di archiviazione Hello utilizza una libreria di base di insieme di credenziali chiave di hello in ordine tooprovide un framework comune in Azure per la gestione delle chiavi. Gli utenti inoltre ottenere ulteriore vantaggio di hello dell'utilizzo della libreria di estensioni di hello insieme di credenziali chiave. libreria di estensioni Hello fornisce funzionalità utili semplice e trasparente Symmetric/RSA locale e i principali fornitori di servizi cloud e con l'aggregazione e la memorizzazione nella cache.

### <a name="interface-and-dependencies"></a>Interfaccia e dipendenze
Esistono tre pacchetti insieme di credenziali chiave:

* Microsoft.Azure.KeyVault.Core contiene hello IKey e IKeyResolver. È un pacchetto di piccole dimensioni senza dipendenze. libreria client di archiviazione Hello per .NET definisce come una dipendenza.
* Microsoft.Azure.KeyVault contiene client REST dell'insieme di credenziali chiave hello.
* Microsoft.Azure.KeyVault.Extensions contiene codice di estensione che include le implementazioni di algoritmi di crittografia e un RSAKey e un SymmetricKey. Si varia a seconda degli spazi dei nomi di base e KeyVault hello e fornisce funzionalità toodefine un resolver di aggregazione (quando gli utenti desiderano toouse più provider di chiavi) e un sistema di risoluzione chiave memorizzazione nella cache. Sebbene libreria client di archiviazione hello dipende direttamente questo pacchetto, se gli utenti desiderano toouse insieme credenziali chiavi Azure toostore le chiavi o hello tooconsume estensioni di toouse hello insieme di credenziali chiave locale e cloud di provider di crittografia, sarà necessario questo pacchetto.

L’insieme di credenziali chiave è progettato per chiavi master di valore elevato e la soglia di limitazione per ogni insieme di credenziali chiave è progettata considerando questo fattore. Quando si esegue la crittografia lato client con l'insieme di credenziali chiave, modello preferito hello è toouse master le chiavi simmetriche archiviate come segreti nell'insieme di credenziali chiave e memorizzata nella cache in locale. Gli utenti devono eseguire la seguente hello:

1. Creare una chiave privata non in linea e caricarlo tooKey insieme di credenziali.
2. Utilizzare l'identificatore di base di un segreto hello come tooresolve un parametro hello versione corrente del segreto hello per la crittografia e memorizzare nella cache localmente queste informazioni. Utilizzare CachingKeyResolver per la memorizzazione nella cache; gli utenti sono previsti non tooimplement la relativa logica specifica la memorizzazione nella cache.
3. Durante la creazione di criteri di crittografia hello, utilizzare il resolver di memorizzazione nella cache di hello come input.

Ulteriori informazioni sull'utilizzo della chiave dell'insieme di credenziali sono reperibile in hello [esempi di codice di crittografia](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples).

## <a name="best-practices"></a>Procedure consigliate
Supporto della crittografia è disponibile solo nella libreria client di archiviazione hello per .NET. Windows Phone e Windows Runtime attualmente non supportano la crittografia.

> [!IMPORTANT]
> Quando si utilizza la crittografia lato client, tenere presente i seguenti aspetti importanti:
> 
> * Quando la scrittura o lettura dal tooan crittografati blob, usare i comandi di caricamento di tutto il blob e i comandi di download di intervallo/intero blob. Evitare di scrivere tooan blob crittografato tramite operazioni di protocollo, ad esempio inserire blocco, inserire elenco Blocca, scrivere pagine, pagine deselezionare o Append Block in caso contrario è possibile danneggiare blob crittografato hello e renderlo illeggibile.
> * Per le tabelle esiste un vincolo simile. Essere toonot attenzione aggiornamento crittografato proprietà senza aggiornare i metadati di crittografia hello.
> * Se si impostano i metadati sul blob crittografato hello, si potrebbero sovrascrivere hello relative a crittografia metadati richiesti per la decrittografia, poiché l'impostazione dei metadati non additivo. Ciò vale anche per gli snapshot; evitare di specificare i metadati durante la creazione di uno snapshot di un BLOB crittografato. Se è necessario impostare i metadati, hello toocall assicurarsi di essere **FetchAttributes** tooget primo metodo hello i metadati di crittografia corrente ed evitare di scritture simultanee durante l'impostazione di metadati.
> * Abilitare hello **RequireEncryption** proprietà nelle opzioni di richiesta hello predefinito per gli utenti che dovrebbero funzionare solo con i dati crittografati. Per ulteriori informazioni, vedere di seguito.
> 
> 

## <a name="client-api--interface"></a>API client/interfaccia
Durante la creazione di un oggetto EncryptionPolicy, gli utenti possono specificare solo una chiave (implementazione IKey), solo un resolver (implementazione IKeyResolver) o entrambi. IKey è hello chiave tipo di base che è identificato mediante un identificatore di chiave e che fornisce la logica di hello per ritorno a capo/annullamento del wrapping. IKeyResolver è tooresolve usato una chiave durante il processo di decrittografia hello. Definisce un metodo ResolveKey che restituisce un IKey dato un identificatore di chiave. In questo modo gli utenti hello possibilità toochoose tra più chiavi che vengono gestiti in più posizioni.

* Per la crittografia, hello usata sempre e assenza hello di una chiave si verificherà un errore.
* Per la decrittografia:
  * resolver chiave Hello viene richiamato se chiave hello tooget specificato. Se il resolver hello viene specificato, ma non dispone di un mapping per l'identificatore di chiave hello, viene generato un errore.
  * Se il sistema di risoluzione non è specificato, ma viene specificata una chiave, chiave hello viene utilizzato se il relativo identificatore corrisponde identificatore di chiave hello necessario. Se l'identificatore hello non corrisponde, viene generato un errore.

Hello [esempi crittografia](https://github.com/Azure/azure-storage-net/tree/master/Samples/GettingStarted/EncryptionSamples) viene illustrato uno scenario end-to-end più dettagliato per BLOB, code e tabelle, insieme con l'integrazione dell'insieme di credenziali chiave.

### <a name="requireencryption-mode"></a>Modalità RequireEncryption
Gli utenti possono facoltativamente abilitare una modalità operativa quando tutte le operazioni di caricamento e download devono essere crittografate. In questa modalità, avrà esito negativo tentativi tooupload dati senza una crittografia criteri o scaricare dati che non vengono crittografati nel servizio hello client hello. Hello **RequireEncryption** proprietà dell'oggetto di opzioni di richiesta hello controlla questo comportamento. Se l'applicazione consente di crittografare tutti gli oggetti archiviati in archiviazione di Azure, è possibile impostare hello **RequireEncryption** proprietà opzioni di richiesta di hello predefinite per oggetto hello client del servizio. Ad esempio, impostare **CloudBlobClient.DefaultRequestOptions.RequireEncryption** troppo**true** toorequire crittografia per tutte le operazioni blob eseguite tramite l'oggetto client.

### <a name="blob-service-encryption"></a>Crittografia del servizio BLOB
Creare un **BlobEncryptionPolicy** e impostarlo in Opzioni di richiesta hello (per l'API o a un livello di client tramite **DefaultRequestOptions**). Tutti gli altri verranno gestiti dalla libreria client hello internamente.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 BlobEncryptionPolicy policy = new BlobEncryptionPolicy(key, null);

 // Set hello encryption policy on hello request options.
 BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

 // Upload hello encrypted contents toohello blob.
 blob.UploadFromStream(stream, size, null, options, null);

 // Download and decrypt hello encrypted contents from hello blob.
 MemoryStream outputStream = new MemoryStream();
 blob.DownloadToStream(outputStream, null, options, null);
```

### <a name="queue-service-encryption"></a>Crittografia del servizio di accodamento
Creare un **QueueEncryptionPolicy** e impostarlo in Opzioni di richiesta hello (per l'API o a un livello di client tramite **DefaultRequestOptions**). Tutti gli altri verranno gestiti dalla libreria client hello internamente.

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 QueueEncryptionPolicy policy = new QueueEncryptionPolicy(key, null);

 // Add message
 QueueRequestOptions options = new QueueRequestOptions() { EncryptionPolicy = policy };
 queue.AddMessage(message, null, null, options, null);

 // Retrieve message
 CloudQueueMessage retrMessage = queue.GetMessage(null, options, null);
```

### <a name="table-service-encryption"></a>Crittografia del servizio tabelle
Inoltre toocreating un criterio di crittografia e l'impostazione in Opzioni di richiesta, è necessario specificare un **EncryptionResolver** in **TableRequestOptions**, o impostare l'attributo [EncryptProperty] hello in entità Hello.

#### <a name="using-hello-resolver"></a>Mediante resolver hello

```csharp
// Create hello IKey used for encryption.
 RsaKey key = new RsaKey("private:key1" /* key identifier */);

 // Create hello encryption policy toobe used for upload and download.
 TableEncryptionPolicy policy = new TableEncryptionPolicy(key, null);

 TableRequestOptions options = new TableRequestOptions()
 {
    EncryptionResolver = (pk, rk, propName) =>
     {
        if (propName == "foo")
         {
            return true;
         }
         return false;
     },
     EncryptionPolicy = policy
 };

 // Insert Entity
 currentTable.Execute(TableOperation.Insert(ent), options, null);

 // Retrieve Entity
 // No need toospecify an encryption resolver for retrieve
 TableRequestOptions retrieveOptions = new TableRequestOptions()
 {
    EncryptionPolicy = policy
 };

 TableOperation operation = TableOperation.Retrieve(ent.PartitionKey, ent.RowKey);
 TableResult result = currentTable.Execute(operation, retrieveOptions, null);
```

#### <a name="using-attributes"></a>Utilizzo di attributi
Come indicato in precedenza, se l'entità hello implementa TableEntity, proprietà hello può essere decorata con l'attributo [EncryptProperty] hello anziché specificare hello **EncryptionResolver**.

```csharp
[EncryptProperty]
 public string EncryptedProperty1 { get; set; }
```

## <a name="encryption-and-performance"></a>Crittografia e prestazioni
Si noti che la crittografia dei dati di archiviazione restituisce un overhead delle prestazioni aggiuntivo. Hello contenuto chiave e vettore di Inizializzazione deve essere generato, contenuto hello deve essere crittografato e metadati aggiuntivi devono essere formattato e caricati. Questo overhead variano a seconda della quantità di hello dei dati da crittografare. È consigliabile che i clienti testano sempre le proprie applicazioni per le prestazioni durante lo sviluppo.

## <a name="next-steps"></a>Passaggi successivi
* [Esercitazione: Crittografare e decrittografare i BLOB in Archiviazione di Microsoft Azure tramite l'insieme di credenziali delle chiavi di Azure](../blobs/storage-encrypt-decrypt-blobs-key-vault.md)
* Scaricare hello [Azure Storage Client Library per il pacchetto NuGet .NET](https://www.nuget.org/packages/WindowsAzure.Storage)
* Scaricare hello NuGet insieme di credenziali chiave di Azure [Core](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Core/), [Client](http://www.nuget.org/packages/Microsoft.Azure.KeyVault/), e [estensioni](http://www.nuget.org/packages/Microsoft.Azure.KeyVault.Extensions/) pacchetti  
* Visitare hello [documentazione dell'insieme di credenziali chiave di Azure](../../key-vault/key-vault-whatis.md)
