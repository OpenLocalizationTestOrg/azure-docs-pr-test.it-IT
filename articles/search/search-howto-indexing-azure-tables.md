---
title: aaaIndexing archiviazione tabelle di Azure con ricerca di Azure | Documenti Microsoft
description: Informazioni su come i dati tooindex archiviati nell'archiviazione tabelle di Azure con ricerca di Azure
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 1cc27411-d0cc-40ed-8aed-c7cb9ab402b9
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 04/10/2017
ms.author: eugenesh
ms.openlocfilehash: abb01a4d807cede310246b34775d8059fceb4456
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="index-azure-table-storage-with-azure-search"></a>Indicizzare in Archiviazione tabelle di Azure con Ricerca di Azure
Questo articolo illustra come dati di ricerca di Azure tooindex toouse archiviati nell'archiviazione tabelle di Azure.

## <a name="set-up-azure-table-storage-indexing"></a>Configurare l'indicizzazione in Archiviazione tabelle di Azure

È possibile configurare un indicizzatore dell'Archiviazione tabelle di Azure mediante queste risorse:

* [Portale di Azure](https://ms.portal.azure.com)
* [API REST](https://docs.microsoft.com/rest/api/searchservice/Indexer-operations) Ricerca di Azure
* [.NET SDK](https://aka.ms/search-sdk) Ricerca di Azure

Qui viene descritto come flusso hello utilizzando hello API REST. 

### <a name="step-1-create-a-datasource"></a>Passaggio 1: Creare un'origine dati

Un'origine dati specifica quali tooindex dati hello credenziali tooaccess hello dati richiesti e i criteri che consentono la ricerca di Azure tooefficiently hello identificano le modifiche nei dati hello.

Per l'indice della tabella, hello datasource deve avere hello le proprietà seguenti:

- **nome** è hello nome univoco dell'origine dati hello all'interno del servizio di ricerca.
- **type** deve essere `azuretable`.
- **credenziali** parametro contiene una stringa di connessione di account di archiviazione hello. Vedere hello [specificare credenziali](#Credentials) sezione per informazioni dettagliate.
- **contenitore** set hello nome della tabella e una query facoltativa.
    - Specificare il nome di tabella hello utilizzando hello `name` parametro.
    - Facoltativamente, specificare una query utilizzando hello `query` parametro. 

> [!IMPORTANT] 
> Se possibile, usare un filtro sul parametro PartitionKey per ottimizzare le prestazioni. Qualsiasi altra query comporterà un'analisi completa delle tabelle e un conseguente peggioramento delle prestazioni in caso di tabelle di grandi dimensioni. Vedere hello [considerazioni sulle prestazioni](#Performance) sezione.


toocreate un'origine dati:

    POST https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" },
        "container" : { "name" : "my-table", "query" : "PartitionKey eq '123'" }
    }   

Per ulteriori informazioni su hello Datasource creare API, vedere [Datasource creare](https://docs.microsoft.com/rest/api/searchservice/create-data-source).

<a name="Credentials"></a>
#### <a name="ways-toospecify-credentials"></a>Credenziali toospecify modi ####

È possibile specificare le credenziali di hello tabella hello in uno dei modi seguenti: 

- **Stringa di connessione di account di archiviazione accesso completo**: `DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>` è possibile ottenere la stringa di connessione hello dal portale di Azure hello passare toohello **blade di account di archiviazione** > **impostazioni**   >  **Chiavi** (per gli account di archiviazione della versione classica) o **impostazioni** > **le chiavi di accesso** (per la risorsa di Azure Account di archiviazione Manager).
- **Account di archiviazione condiviso stringa di connessione di firma di accesso**: `TableEndpoint=https://<your account>.table.core.windows.net/;SharedAccessSignature=?sv=2016-05-31&sig=<hello signature>&spr=https&se=<hello validity end time>&srt=co&ss=t&sp=rl` firma di accesso condiviso hello deve avere hello elenco e autorizzazioni di lettura per i contenitori (le tabelle in questo caso) e gli oggetti (righe di tabella).
-  **Firma di accesso condiviso tabella**: `ContainerSharedAccessUri=https://<your storage account>.table.core.windows.net/<table name>?tn=<table name>&sv=2016-05-31&sig=<hello signature>&se=<hello validity end time>&sp=r` firma di accesso condiviso hello deve disporre delle autorizzazioni di query (lettura) sulla tabella hello.

Per altre informazioni sulle firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

> [!NOTE]
> Se si utilizzano credenziali di firma di accesso condiviso, è necessario credenziali dell'origine dati hello tooupdate periodicamente con le firme rinnovato tooprevent scadenza. Se le credenziali di firma di accesso condiviso hanno una scadenza, un indicizzatore hello ha esito negativo con un messaggio di errore simile troppo "credenziali specificate nella stringa di connessione hello sono valide o sono scadute."  

### <a name="step-2-create-an-index"></a>Passaggio 2: Creare un indice
indice Hello specifica campi hello in un documento, gli attributi di hello, e altri costrutti di un'esperienza di ricerca hello tale forma.

toocreate un indice:

    POST https://[service name].search.windows.net/indexes?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
          "name" : "my-target-index",
          "fields": [
            { "name": "key", "type": "Edm.String", "key": true, "searchable": false },
            { "name": "SomeColumnInMyTable", "type": "Edm.String", "searchable": true }
          ]
    }

Per altre informazioni sulla creazione di indici, vedere [Creare un indice](https://docs.microsoft.com/rest/api/searchservice/create-index).

### <a name="step-3-create-an-indexer"></a>Passaggio 3: Creare un indicizzatore
Un indicizzatore si connette a un'origine dati con un indice di ricerca di destinazione e fornisce un aggiornamento di dati di pianificazione tooautomate hello. 

Dopo aver creati l'origine dati e indice hello, si è l'indicizzatore hello toocreate pronto:

    POST https://[service name].search.windows.net/indexers?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
      "name" : "table-indexer",
      "dataSourceName" : "table-datasource",
      "targetIndexName" : "my-target-index",
      "schedule" : { "interval" : "PT2H" }
    }

L'indicizzatore verrà eseguito ogni due ore. (l'intervallo di pianificazione hello è troppo "PT2H".) un indicizzatore toorun ogni 30 minuti, impostare l'intervallo di hello troppo "PT30M". intervallo supportato di Hello minimo è 5 minuti. pianificazione di Hello è facoltativo. Se omesso, viene eseguito un indicizzatore solo una volta al momento della creazione. Tuttavia, è possibile eseguire un indicizzatore su richiesta in qualsiasi momento.   

Per ulteriori informazioni su hello Create Indexer API, vedere [indicizzatore creare](https://docs.microsoft.com/rest/api/searchservice/create-indexer).

## <a name="deal-with-different-field-names"></a>Gestire nomi campo diversi
In alcuni casi, i nomi dei campi hello in un indice esistente sono diversi dai nomi delle proprietà hello nella tabella. È possibile utilizzare i nomi campo mapping toomap hello proprietà da nomi di campo toohello hello tabella nell'indice di ricerca. toolearn ulteriori informazioni sui mapping dei campi, vedere [mapping dei campi dell'indicizzatore di ricerca di Azure bridge differenze hello tra origini dati e la ricerca degli indici](search-indexer-field-mappings.md).

## <a name="handle-document-keys"></a>Gestire le chiavi del documento
In ricerca di Azure, hello documento chiave identifica in modo univoco un documento. Ogni indice di ricerca deve avere esclusivamente un campo chiave di tipo `Edm.String`. campo chiave Hello è obbligatorio per ogni documento che viene aggiunto toohello indice. (In realtà, di hello solo obbligatorio campo).

La chiave delle righe è composta. Ricerca di Azure genera pertanto un campo sintetico denominato `Key`, vale a dire una concatenazione di valori di chiave di partizione e chiave di riga. Ad esempio, se una riga del PartitionKey è `PK1` e RowKey `RK1`, quindi hello `Key` valore del campo è `PK1RK1`.

> [!NOTE]
> Hello `Key` valore può contenere caratteri non validi nelle chiavi di documento, ad esempio trattini. È possibile gestire con caratteri non validi usando hello `base64Encode` [funzione di mapping di campo](search-indexer-field-mappings.md#base64EncodeFunction). In questo caso, tenere presente tooalso 64 sicura URL utilizzano la codifica quando passando le chiavi dei documenti nell'API chiama ad esempio di ricerca.
>
>

## <a name="incremental-indexing-and-deletion-detection"></a>Indicizzazione incrementale e rilevamento delle eliminazioni
Quando si configura un toorun indicizzatore di tabella in una pianificazione, reindexes righe solo nuove o aggiornate, come determinato da una riga `Timestamp` valore. Non è necessario toospecify un criteri di rilevamento delle modifiche. L'indicizzazione incrementale viene abilitata automaticamente.

tooindicate che alcuni documenti devono essere rimosso dall'indice hello, è possibile usare una strategia di eliminazione temporanea. Eliminazione di una riga, invece di aggiungere un tooindicate proprietà eliminato, e impostare un criterio di rilevamento eliminazione temporanea di hello datasource. Ad esempio, hello seguente criteri considera che viene eliminata una riga se la riga hello ha una proprietà `IsDeleted` con valore hello `"true"`:

    PUT https://[service name].search.windows.net/datasources?api-version=2016-09-01
    Content-Type: application/json
    api-key: [admin key]

    {
        "name" : "my-table-datasource",
        "type" : "azuretable",
        "credentials" : { "connectionString" : "<your storage connection string>" },
        "container" : { "name" : "table name", "query" : "<query>" },
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }   

<a name="Performance"></a>
## <a name="performance-considerations"></a>Considerazioni sulle prestazioni

Per impostazione predefinita, ricerca di Azure Usa hello seguente filtro di query: `Timestamp >= HighWaterMarkValue`. Poiché le tabelle di Azure non sono un indice secondario in hello `Timestamp` campo, questo tipo di query richiede un'analisi completa della tabella e pertanto è lento per tabelle di grandi dimensioni.


Ecco due possibili approcci per migliorare le prestazioni dell'indicizzazione delle tabelle. Entrambi gli approcci si basano sull'utilizzo delle partizioni delle tabelle: 

- Se i dati possono essere partizionati naturalmente in diversi intervalli della partizione, creare un'origine dati e un indicizzatore corrispondente per ogni intervallo della partizione. Ogni indicizzatore dispone ora tooprocess solo un intervallo di partizione specifica, consentendo così migliori prestazioni di query. Se i dati di hello che devono essere indicizzati toobe dispone di un numero ridotto di partizioni fisse, ancora migliore: ogni indicizzatore esegue solo un'analisi di partizione. Ad esempio, toocreate un'origine dati per l'elaborazione di un intervallo di partizione con le chiavi da `000` troppo`100`, utilizzare una query simile alla seguente: 
    ```
    "container" : { "name" : "my-table", "query" : "PartitionKey ge '000' and PartitionKey lt '100' " }
    ```

- Se i dati vengono partizionati per ora (ad esempio, si crea una nuova partizione di ogni giorno o settimana), prendere in considerazione hello approccio: 
    - Utilizzare una query del modulo hello: `(PartitionKey ge <TimeStamp>) and (other filters)`. 
    - Monitorare lo stato di avanzamento di un indicizzatore con [ottenere indicizzatore stato API](https://docs.microsoft.com/rest/api/searchservice/get-indexer-status)e aggiornare periodicamente hello `<TimeStamp>` condizione della query hello in base a hello più recente limite massimo valore correttamente. 
    - Con questo approccio, se è necessario tootrigger reindicizzazione completa, è necessario tooreset hello datasource query indicizzatore hello tooresetting di addizione. 


## <a name="help-us-make-azure-search-better"></a>Come contribuire al miglioramento di Ricerca di Azure
Se si hanno domande sulle funzionalità o idee per apportare miglioramenti, contattare Microsoft sul [sito UserVoice](https://feedback.azure.com/forums/263029-azure-search/).
