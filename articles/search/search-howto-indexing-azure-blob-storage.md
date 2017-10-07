---
title: aaaIndexing archiviazione Blob di Azure con ricerca di Azure
description: Informazioni su come testo tooindex Blob di Azure archiviazione ed estrazione da un documento con ricerca di Azure
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 2a5968f4-6768-4e16-84d0-8b995592f36a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 07/22/2017
ms.author: eugenesh
ms.openlocfilehash: 1bdd34e66a4a9192ed88cacbc7b8456d0dcdfeb6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="indexing-documents-in-azure-blob-storage-with-azure-search"></a>Indicizzazione di documenti in Archiviazione BLOB di Azure con Ricerca di Azure
Questo articolo viene illustrato come documenti di tooindex toouse ricerca di Azure (ad esempio PDF, documenti di Microsoft Office e diversi altri formati comuni) archiviati in archiviazione Blob di Azure. In primo luogo, vengono descritte le nozioni di base di hello di installazione e configurazione di un indicizzatore di blob. Quindi, offre un'esplorazione più approfondita dei comportamenti e scenari si è probabilmente tooencounter.

## <a name="supported-document-formats"></a>Formati di documento supportati
indicizzatore di blob Hello può estrarre il testo dalla hello seguenti formati di documento:

* PDF
* Formati di Microsoft Office: DOCX/DOC, XLSX/XLS, PPTX/PPT, MSG (messaggi di posta elettronica di Outlook)  
* HTML
* XML
* ZIP
* EML
* RTF
* File di testo normale (vedere anche [Indicizzazione di testo normale](#IndexingPlainText))
* JSON (vedere [Indicizzazione di BLOB JSON](search-howto-index-json-blobs.md))
* CSV (vedere la funzionalità in anteprima [Indicizzazione di BLOB CSV](search-howto-index-csv-blobs.md))

> [!IMPORTANT]
> Il supporto per gli array in formato CSV e JSON è attualmente in anteprima. Questi formati sono disponibili solo con versione **2016-09-01-Preview** di hello 2. x-preview API REST o la versione di hello .NET SDK. Si ricordi che le API di anteprima servono per il test e la valutazione e non devono essere usate negli ambienti di produzione.
>
>

## <a name="setting-up-blob-indexing"></a>Configurazione dell'indicizzazione BLOB
È possibile impostare un indicizzatore dell'Archiviazione BLOB di Azure usando:

* [Portale di Azure](https://ms.portal.azure.com)
* [API REST](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations) Ricerca di Azure
* [.NET SDK](https://aka.ms/search-sdk) Ricerca di Azure

> [!NOTE]
> Alcune delle funzionalità (ad esempio, i mapping campi) non sono ancora disponibili nel portale di hello che toobe utilizzato a livello di codice.
>
>

In questo caso, viene descritto come flusso hello utilizzando hello API REST.

### <a name="step-1-create-a-data-source"></a>Passaggio 1: Creare un'origine dati
Un'origine dati specifica quali dati tooindex, i dati di hello tooaccess le credenziali necessarie e criteri tooefficiently identificare le modifiche nei dati hello (nuovo, modificate o eliminate righe). Un'origine dati può essere utilizzata da più indicizzatori in hello stesso servizio di ricerca.

Per l'indicizzazione blob, origine dati hello deve avere hello seguenti proprietà obbligatorie:

* **nome** è hello nome univoco dell'origine dati hello all'interno del servizio di ricerca.
* **type** deve essere `azureblob`.
* **credenziali** fornisce una stringa di connessione account di archiviazione di hello come hello `credentials.connectionString` parametro. Vedere [come credenziali toospecify](#Credentials) sotto per informazioni dettagliate.
* **container** specifica un contenitore nell'account di archiviazione. Per impostazione predefinita, tutti i BLOB all'interno del contenitore hello sono recuperabili. Se si vuole solo BLOB tooindex in una directory virtuale specifica, è possibile specificare tale directory utilizzando hello facoltativo **query** parametro.

toocreate un'origine dati:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-container", "query" : "<optional-virtual-directory-name>" }
    }   

Per ulteriori informazioni su hello Datasource creare API, vedere [Datasource creare](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="how-toospecify-credentials"></a>Come credenziali toospecify ####

È possibile fornire credenziali di hello per il contenitore blob hello in uno dei modi seguenti:

- **Stringa di connessione dell'account di archiviazione per accesso completo**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>`. È possibile ottenere la stringa di connessione hello dal portale di Azure hello passando a pannello di account di archiviazione toohello > Impostazioni > chiavi (per gli account di archiviazione classica) o impostazioni > chiavi (per gli account di archiviazione di Azure Resource Manager) di accesso.
- **Firma di accesso condiviso di account di archiviazione** stringa di connessione (SAS): `BlobEndpoint=https://<your account>.blob.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=b&sp=rl` hello SAS necessario hello elenco e autorizzazioni di lettura per i contenitori e oggetti (BLOB in questo caso).
-  **Firma di accesso condiviso del contenitore**: `ContainerSharedAccessUri=https://<your storage account>.blob.core.windows.net/<container name>?sv=2016-05-31&sr=c&sig=<hello signature>&se=<hello validity end time>&sp=rl` hello SAS necessario hello elenco e autorizzazioni di lettura per il contenitore di hello.

Per altre informazioni sulle firme di accesso condiviso per l'archiviazione, vedere [Uso delle firme di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Se si utilizzano credenziali di firma di accesso condiviso, è necessario credenziali dell'origine dati hello tooupdate periodicamente con le firme rinnovato tooprevent scadenza. Se le credenziali di firma di accesso condiviso hanno una scadenza, un indicizzatore hello avrà esito negativo con un messaggio di errore simile troppo`Credentials provided in hello connection string are invalid or have expired.`.  

### <a name="step-2-create-an-index"></a>Passaggio 2: Creare un indice
indice Hello specifica campi hello in un documento, gli attributi, e altri costrutti di un'esperienza di ricerca hello tale forma.

Ecco come toocreate un indice con una ricerca `content` campo di testo hello toostore estratto dal BLOB:   

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "id", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false }
          ]
    }

Per altre informazioni sulla creazione di indici, vedere [Creare un indice](https://docs.microsoft.com/rest/api/searchservice/create-index)

### <a name="step-3-create-an-indexer"></a>Passaggio 3: Creare un indicizzatore
Un indicizzatore si connette a un'origine dati con un indice di ricerca di destinazione e fornisce un aggiornamento di dati di pianificazione tooautomate hello.

Dopo avere creato hello indice e l'origine dati, si è pronti toocreate indicizzatore di hello:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "blob-indexer",
      "dataSourceName" : "blob-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

Questo indicizzatore verrà eseguito ogni due ore (intervallo di pianificazione è impostata troppo "PT2H"). un indicizzatore toorun ogni 30 minuti, impostare l'intervallo di hello troppo "PT30M". intervallo supportato di Hello minimo è 5 minuti. Hello pianificazione è facoltativa: Se omesso, viene eseguito un indicizzatore solo una volta al momento della creazione. Tuttavia, è possibile eseguire un indicizzatore su richiesta in qualsiasi momento.   

Per ulteriori informazioni su hello creare API di indicizzatore, estrarre [indicizzatore creare](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="how-azure-search-indexes-blobs"></a>Indicizzazione dei BLOB con Ricerca di Azure

A seconda di hello [configurazione indicizzatore](#PartsOfBlobToIndex), indicizzatore blob hello consente di indicizzare solo i metadati di archiviazione (utile quando l'attenzione solo sui metadati hello e non è necessario tooindex hello contenuto di BLOB), archiviazione e il contenuto dei metadati, o entrambi i metadati e contenuto testuale. Per impostazione predefinita, indicizzatore hello estrae i metadati e il contenuto.

> [!NOTE]
> Per impostazione predefinita, i BLOB con contenuto strutturato, come quelli in formato JSON o CSV, vengono indicizzati come un unico blocco di testo. Se si desidera tooindex JSON e CSV BLOB in una struttura, vedere [JSON l'indicizzazione BLOB](search-howto-index-json-blobs.md) e [CSV l'indicizzazione BLOB](search-howto-index-csv-blobs.md) funzionalità di anteprima.
>
> Anche un documento composito o incorporato (ad esempio, un archivio ZIP o un documento di Word con una e-mail di Outlook incorporata con allegati) viene indicizzato come documento singolo.

* contenuto testuale di Hello del documento hello viene estratto in un campo stringa denominato `content`.

> [!NOTE]
> Ricerca di Azure limita la quantità di testo viene estratto in base al livello di prezzo hello: 32.000 caratteri gratuitamente livello, 64.000 per Basic e 4 milioni per i livelli Standard, Standard S2 e S3 Standard. Un avviso è incluso nella risposta di hello indicizzatore sullo stato per i documenti troncati.  

* Proprietà di metadati specificato dall'utente presenti nel blob hello, se presenti, vengono estratti testuale.
* Proprietà dei metadati del blob standard vengono estratti in hello seguenti campi:

  * **metadati\_archiviazione\_nome** (EDM) - nome del blob hello file hello. Ad esempio, se si dispone di un blob di /my-container/my-folder/subfolder/resume.pdf, hello valore di questo campo è `resume.pdf`.
  * **metadati\_archiviazione\_percorso** (EDM) - hello completo URI del blob hello, tra cui account di archiviazione hello. Ad esempio, `https://myaccount.blob.core.windows.net/my-container/my-folder/subfolder/resume.pdf`
  * **metadati\_archiviazione\_contenuto\_tipo** (EDM) - tipo di contenuto, come specificato dal codice hello è utilizzato blob hello tooupload. ad esempio `application/octet-stream`.
  * **metadati\_archiviazione\_ultimo\_modificato** (DateTimeOffset) - ultima modifica del timestamp per blob hello. Ricerca di Azure Usa questo BLOB tooidentify modificato timestamp, tooavoid la reindicizzazione di tutti gli elementi al termine dell'indicizzazione iniziale hello.
  * **metadata\_storage\_size** (Edm.Int64): dimensioni del BLOB in byte.
  * **metadati\_archiviazione\_contenuto\_md5** (EDM) - hash MD5 del contenuto di blob hello, se disponibile.
* Formato del documento metadati proprietà tooeach specifico vengono estratti in campi hello elencati [qui](#ContentSpecificMetadata).

Non è necessario toodefine campi per tutti i hello sopra le proprietà nell'indice di ricerca: acquisire solo le proprietà di hello che è necessario per l'applicazione.

> [!NOTE]
> Spesso, i nomi dei campi hello in un indice esistente è diverse da nomi di campo hello generati durante l'estrazione del documento. È possibile utilizzare **campo mapping** toomap i nomi di proprietà hello forniti da nomi di campo di ricerca di Azure toohello nell'indice di ricerca. Di seguito verrà visualizzato un esempio di mapping dei campi.
>
>

<a name="DocumentKeys"></a>
### <a name="defining-document-keys-and-field-mappings"></a>Definizione di chiavi di documento e dei mapping dei campi
In ricerca di Azure, hello documento chiave identifica in modo univoco un documento. Ogni indice di ricerca deve avere esclusivamente un campo chiave di tipo Edm.String. campo chiave Hello è obbligatorio per ogni documento che viene aggiunto indice toohello (è effettivamente hello unico campo obbligatorio).  

È necessario valutare attentamente il campo estratto deve eseguire il mapping toohello campo chiave per l'indice. candidati Hello sono:

* **metadati\_archiviazione\_nome** : ciò potrebbe essere un candidato ideale, ma si noti che i nomi di hello 1) potrebbero non essere univoci, come è possibile BLOB con stesso nome in cartelle diverse hello e 2) hello nome può contenere caratteri che non sono validi nelle chiavi di documento, ad esempio trattini. È possibile gestire con caratteri non validi usando hello `base64Encode` [funzione di mapping di campo](search-indexer-field-mappings.md#base64EncodeFunction) : in tal caso, considerare le chiavi dei documenti tooencode passarli nell'API chiama ad esempio di ricerca. (Ad esempio, in .NET è possibile utilizzare hello [UrlTokenEncode metodo](https://msdn.microsoft.com/library/system.web.httpserverutility.urltokenencode.aspx) a tale scopo).
* **metadati\_archiviazione\_percorso** : con percorso completo di hello garantisce l'univocità, ma contiene sicuramente percorso hello `/` caratteri [non valido in una chiave di documento](https://docs.microsoft.com/rest/api/searchservice/naming-rules).  Come illustrato in precedenza, è possibile hello codifica chiavi hello utilizzando hello `base64Encode` [funzione](search-indexer-field-mappings.md#base64EncodeFunction).
* Se nessuna delle opzioni di hello precedente risolvere il problema, è possibile aggiungere un BLOB toohello proprietà di metadati personalizzati. Questa opzione, tuttavia, richiedono il tooadd processo di caricamento blob tale BLOB tooall di proprietà dei metadati. Poiché la chiave hello è una proprietà obbligatoria, tutti i blob che non dispongono di tale proprietà non riuscirà toobe indicizzato.

> [!IMPORTANT]
> Se è presente alcun mapping esplicito per campo chiave hello indice hello, ricerca di Azure usa automaticamente `metadata_storage_path` come valori di chiave (hello seconda opzione precedente) di codifica hello chiave e base 64.
>
>

Per questo esempio, si seleziona hello `metadata_storage_name` campo come chiave di documento hello. Si supponga inoltre l'indice è un campo chiave denominato `key` e un campo `fileSize` per l'archiviazione di dimensioni del documento hello. le operazioni toowire nel modo desiderato e specificare hello dopo il mapping dei campi durante la creazione o l'aggiornamento dell'indicizzatore:

    "fieldMappings" : [
      { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
      { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
    ]

toobring questo tutti insieme, ecco come è possibile aggiungere i mapping dei campi e Abilita codifica base 64 di chiavi per un indicizzatore esistente:

    PUT https://[service name].search.windows.net/indexers/blob-indexer?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "dataSourceName" : " blob-datasource ",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" },
      "fieldMappings" : [
        { "sourceFieldName" : "metadata_storage_name", "targetFieldName" : "key", "mappingFunction" : { "name" : "base64Encode" } },
        { "sourceFieldName" : "metadata_storage_size", "targetFieldName" : "fileSize" }
      ]
    }

> [!NOTE]
> toolearn ulteriori informazioni sui mapping dei campi, vedere [questo articolo](search-indexer-field-mappings.md).
>
>

<a name="WhichBlobsAreIndexed"></a>
## <a name="controlling-which-blobs-are-indexed"></a>Controllo dei BLOB da indicizzare
È possibile controllare quali BLOB vengono indicizzati e quali vengono ignorati.

### <a name="index-only-hello-blobs-with-specific-file-extensions"></a>Solo i BLOB hello con determinate estensioni di file di indice
È possibile indicizzare solo BLOB hello con hello estensioni specificate utilizzando hello `indexedFileNameExtensions` parametro di configurazione dell'indicizzatore. il valore di Hello è una stringa contenente un elenco delimitato da virgole delle estensioni di file (con un punto iniziale). Ad esempio, tooindex solo hello. PDF e. BLOB DOCX, eseguire questa operazione:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "indexedFileNameExtensions" : ".pdf,.docx" } }
    }

### <a name="exclude-blobs-with-specific-file-extensions"></a>Escludere BLOB con estensioni di file specifiche
È possibile escludere i BLOB con estensioni di file specifico dall'indicizzazione mediante hello `excludedFileNameExtensions` parametro di configurazione. il valore di Hello è una stringa contenente un elenco delimitato da virgole delle estensioni di file (con un punto iniziale). Ad esempio, tooindex tutti i BLOB ad eccezione di quelli con hello. PNG e. Estensioni JPEG, eseguire questa operazione:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "excludedFileNameExtensions" : ".png,.jpeg" } }
    }

Se sono presenti entrambi i parametri `indexedFileNameExtensions` e `excludedFileNameExtensions`, Ricerca di Azure esamina in primo luogo `indexedFileNameExtensions`, quindi `excludedFileNameExtensions`. Ciò significa che se hello stessa estensione di file è presente in entrambi gli elenchi, esso verrà escluso dall'indicizzazione.

### <a name="dealing-with-unsupported-content-types"></a>Gestire tipi di contenuto non supportati

Per impostazione predefinita, l'indicizzatore blob hello arresta non appena viene rilevato un blob con un tipo di contenuto non supportato (ad esempio, un'immagine). Naturalmente è possibile utilizzare hello `excludedFileNameExtensions` tooskip parametro determinati tipi di contenuto. Tuttavia, potrebbe essere necessario tooindex BLOB senza conoscere in anticipo tutti hello possibili tipi di contenuto. toocontinue indicizzazione quando viene rilevato un tipo di contenuto non supportato, impostare hello `failOnUnsupportedContentType` parametro di configurazione troppo`false`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "failOnUnsupportedContentType" : false } }
    }

### <a name="ignoring-parsing-errors"></a>Ignorare gli errori di analisi

Logica di estrazione documento ricerca Azure non è perfetta e talvolta avrà esito negativo, ad esempio documenti tooparse di un tipo di contenuto supportato. DOCX o. PDF. Se si desidera hello toointerrupt l'indicizzazione in tali casi, impostare hello `maxFailedItems` e `maxFailedItemsPerBatch` valori ragionevole toosome parametri di configurazione. ad esempio:

    {
      ... other parts of indexer definition
      "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 10 }
    }

<a name="PartsOfBlobToIndex"></a>
## <a name="controlling-which-parts-of-hello-blob-are-indexed"></a>Controllare le parti del blob hello vengono indicizzate

È possibile controllare quali parti del BLOB hello vengono indicizzate utilizzando hello `dataToExtract` parametro di configurazione. Può accettare hello seguenti valori:

* `storageMetadata`-Specifica che solo hello [specificato dall'utente metadati e proprietà blob standard](../storage/blobs/storage-properties-metadata.md) vengono indicizzati.
* `allMetadata`-Specifica che i metadati di archiviazione e hello [metadati specifici del tipo di contenuto](#ContentSpecificMetadata) estratti dal blob hello contenuto vengono indicizzati.
* `contentAndMetadata`-Specifica che tutti i metadati e contenuto testuale estratto dal blob hello siano indicizzate. Questo è il valore di predefinito hello.

Ad esempio, tooindex solo hello archiviazione i metadati, usare:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "dataToExtract" : "storageMetadata" } }
    }

### <a name="using-blob-metadata-toocontrol-how-blobs-are-indexed"></a>Utilizzando toocontrol metadati blob come vengono indicizzati i BLOB

BLOB tooall si applicano i parametri di configurazione di Hello descritti in precedenza. In alcuni casi, è opportuno toocontrol come *singoli BLOB* vengono indicizzati. È possibile farlo aggiungendo hello segue blob proprietà dei metadati e i valori:

| Nome proprietà | Valore proprietà | Spiegazione |
| --- | --- | --- |
| AzureSearch_Skip |"true" |Indica il blob hello skip toocompletely di hello blob dell'indicizzatore. Non verrà tentata l'estrazione dei metadati né del contenuto. Ciò è utile quando un blob ha ripetutamente esito negativo e interrompe processo di indicizzazione hello. |
| AzureSearch_SkipContent |"true" |Questo è equivalente a `"dataToExtract" : "allMetadata"` descritta [sopra](#PartsOfBlobToIndex) tooa con ambito specifico blob. |

## <a name="incremental-indexing-and-deletion-detection"></a>Indicizzazione incrementale e rilevamento delle eliminazioni
Quando si configura un toorun indicizzatore blob in una pianificazione, viene nuovamente eseguita l'indicizzazione solo hello modificato BLOB, come determinato da blob di hello `LastModified` timestamp.

> [!NOTE]
> Non si dispone di un criterio di rilevamento modifiche toospecify: indicizzazione incrementale è abilitata automaticamente per l'utente.

toosupport l'eliminazione di documenti, usare un approccio di "eliminazione temporanea". Se si elimina il BLOB di hello definitiva, i documenti corrispondenti non verranno rimossa dall'indice di ricerca hello. Usare invece hello alla procedura seguente:  

1. Aggiungere un tooAzure tooindicate metadati personalizzati proprietà toohello blob ricerca che viene eliminato in modo logico
2. Configurare un criterio di rilevamento di eliminazione temporanea nell'origine dati hello
3. Una volta indicizzatore hello è elaborato blob hello (come illustrato dall'API di stato dell'indicizzatore hello), è possibile eliminare fisicamente blob hello

Ad esempio, hello seguenti criteri considera un toobe blob eliminato se dispone di una proprietà di metadati `IsDeleted` con valore hello `true`:

    PUT https://[service name].search.windows.net/datasources/blob-datasource?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" },
        "dataDeletionDetectionPolicy" : {
            "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",     
            "softDeleteColumnName" : "IsDeleted",
            "softDeleteMarkerValue" : "true"
        }
    }   

## <a name="indexing-large-datasets"></a>Indicizzazione di set di dati di grandi dimensioni

L'indicizzazione di BLOB può richiedere molto tempo. Nei casi in cui si dispongono di milioni di tooindex BLOB, è possibile velocizzare l'indicizzazione per il partizionamento dei dati e l'utilizzo di più indicizzatori tooprocess hello dati in parallelo. A tale scopo, è possibile procedere come segue:

- Partizionare i dati in più contenitori BLOB o cartelle virtuali.
- Impostare diverse origini dati di Ricerca di Azure, una per ogni contenitore o cartella. cartella di toopoint tooa blob, utilizzare hello `query` parametro:

    ```
    {
        "name" : "blob-datasource",
        "type" : "azureblob",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "my-container", "query" : "my-folder" }
    }
    ```

- Creare un indicizzatore corrispondente per ogni origine dati. Tutti gli indicizzatori possono punto toohello di hello stesso indice di ricerca di destinazione.  

- Un'unità di ricerca del servizio permette di eseguire un indicizzatore in qualsiasi momento. La creazione di più indicizzatori come descritto in precedenza è utile solo se effettivamente eseguiti in parallelo. toorun più indicizzatori in parallelo, la scalabilità del servizio di ricerca mediante la creazione di un numero appropriato di partizioni e repliche. Ad esempio, se il servizio di ricerca dispone di 6 unità di ricerca (ad esempio, le repliche di 2 partizioni x 3), quindi 6 indicizzatori possono eseguire contemporaneamente, determinando un aumento della velocità effettiva di indicizzazione hello six-fold. toolearn più sulla scalabilità e la pianificazione della capacità, vedere [livelli di risorsa per query e indicizzazione carichi di lavoro in ricerca di Azure di scala](search-capacity-planning.md).

## <a name="indexing-documents-along-with-related-data"></a>Indicizzazione di documenti con dati correlati

Potrebbe essere troppo "comporre" documenti da più origini nell'indice. Ad esempio, è consigliabile testo toomerge dai BLOB con altri metadati archiviati nel database Cosmos. È anche possibile usare hello API indicizzazione push insieme a diversi indicizzatori troppo compilare i documenti di ricerca da più parti. 

Per questo toowork, tutti gli indicizzatori e altri componenti necessario tooagree nella chiave del documento hello. Per una descrizione dettagliata, vedere l'articolo esterno: [Combinare documenti con altri dati in Ricerca di Azure ](http://blog.lytzen.name/2017/01/combine-documents-with-other-data-in.html).

<a name="IndexingPlainText"></a>
## <a name="indexing-plain-text"></a>Indicizzazione di testo normale 

Se tutti i BLOB contengono testo normale nel hello stessa codifica, è possibile migliorare notevolmente le prestazioni di indicizzazione utilizzando **modalità di analisi del testo**. hello set, la modalità di analisi del testo toouse `parsingMode` proprietà di configurazione troppo`text`:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text" } }
    }

Per impostazione predefinita, hello `UTF-8` verrà utilizzata la codifica. toospecify una codifica diversa, utilizzare hello `encoding` proprietà di configurazione: 

    {
      ... other parts of indexer definition
      "parameters" : { "configuration" : { "parsingMode" : "text", "encoding" : "windows-1252" } }
    }


<a name="ContentSpecificMetadata"></a>
## <a name="content-type-specific-metadata-properties"></a>Proprietà di metadati specifiche del tipo di contenuto
Hello nella tabella seguente riepiloga l'elaborazione eseguita per ogni formato di documento e vengono descritte le proprietà dei metadati hello estratte da ricerca di Azure.

| Formato documento/tipo di contenuto | Proprietà di metadati specifiche del tipo di contenuto | Dettagli elaborazione |
| --- | --- | --- |
| HTML (`text/html`) |`metadata_content_encoding`<br/>`metadata_content_type`<br/>`metadata_language`<br/>`metadata_description`<br/>`metadata_keywords`<br/>`metadata_title` |Rimozione del markup HTML ed estrazione del testo |
| PDF (`application/pdf`) |`metadata_content_type`<br/>`metadata_language`<br/>`metadata_author`<br/>`metadata_title` |Estrazione del testo, inclusi i documenti incorporati (escluse le immagini) |
| DOCX (application/vnd.openxmlformats-officedocument.wordprocessingml.document) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Estrazione del testo, inclusi i documenti incorporati |
| DOC (application/msword) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_character_count`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_page_count`<br/>`metadata_word_count` |Estrazione del testo, inclusi i documenti incorporati |
| XLSX (application/vnd.openxmlformats-officedocument.spreadsheetml.sheet) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Estrazione del testo, inclusi i documenti incorporati |
| XLS (application/vnd.ms-excel) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified` |Estrazione del testo, inclusi i documenti incorporati |
| PPTX (application/vnd.openxmlformats-officedocument.presentationml.presentation) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Estrazione del testo, inclusi i documenti incorporati |
| PPT (application/vnd.ms-powerpoint) |`metadata_content_type`<br/>`metadata_author`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_slide_count`<br/>`metadata_title` |Estrazione del testo, inclusi i documenti incorporati |
| MSG (application/vnd.ms-outlook) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_message_bcc`<br/>`metadata_creation_date`<br/>`metadata_last_modified`<br/>`metadata_subject` |Estrazione del testo, inclusi gli allegati |
| ZIP (application/zip) |`metadata_content_type` |Estrarre il testo da tutti i documenti nell'archivio di hello |
| XML (application/xml) |`metadata_content_type`</br>`metadata_content_encoding`</br> |Rimozione del markup XML ed estrazione del testo |
| JSON (application/json) |`metadata_content_type`</br>`metadata_content_encoding` |Estrazione del testo<br/>Nota: Se è necessario tooextract documento più campi da un blob JSON, vedere [JSON l'indicizzazione BLOB](search-howto-index-json-blobs.md) per informazioni dettagliate |
| EML (message/rfc822) |`metadata_content_type`<br/>`metadata_message_from`<br/>`metadata_message_to`<br/>`metadata_message_cc`<br/>`metadata_creation_date`<br/>`metadata_subject` |Estrazione del testo, inclusi gli allegati |
| RTF (application/rtf) |`metadata_content_type`</br>`metadata_author`</br>`metadata_character_count`</br>`metadata_creation_date`</br>`metadata_page_count`</br>`metadata_word_count`</br> | Estrazione del testo|
| Testo normale (text/plain) |`metadata_content_type`</br>`metadata_content_encoding`</br> | Estrazione del testo|


## <a name="help-us-make-azure-search-better"></a>Come contribuire al miglioramento di Ricerca di Azure
Per richieste di funzionalità o idee su miglioramenti da apportare, è possibile usare il [sito UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
