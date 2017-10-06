---
title: 'Operazioni sull''indicizzatore (API REST di Ricerca di Azure: 2015-02-28-Preview) | Documentazione Microsoft'
description: 'Operazioni sull''indicizzatore (API REST di Ricerca di Azure: 2015-02-28-Preview)'
services: search
documentationcenter: 
author: chaosrealm
manager: pablocas
editor: 
ms.assetid: 42b5f85c-8304-4bc7-8e1e-a9c76b8ca25a
ms.service: search
ms.devlang: rest-api
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: eugenesh
ms.openlocfilehash: 4dd9591072b44eeabae6eac1182b4eea10fd4a22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="indexer-operations-azure-search-service-rest-api-2015-02-28-preview"></a>Operazioni sull'indicizzatore (API REST di Ricerca di Azure: 2015-02-28-Preview)
> [!NOTE]
> Questo articolo vengono descritti gli indicizzatori di hello [API REST 2015-02-28-Preview](search-api-2015-02-28-preview.md). Questa versione dell'API aggiunge le versioni di anteprima dell'indicizzatore di archiviazione BLOB di Azure con estrazione di documenti, l'indicizzatore di archiviazione tabelle e altri miglioramenti. Hello API supporta inoltre in genere disponibili indicizzatori (GA), compresi gli indicizzatori per Database SQL di Azure, SQL Server in macchine virtuali di Azure e Azure Cosmos DB.
> 
> 

## <a name="overview"></a>Panoramica
Ricerca di Azure può integrarsi direttamente con alcune origini dati comuni, la rimozione di hello necessità toowrite codice tooindex i dati. tooset la configurazione, è possibile chiamare hello toocreate di API di ricerca di Azure e gestire **indicizzatori** e **origini dati**. 

Un **indicizzatore** è una risorsa che connette le origini dati agli indici di ricerca di destinazione. Un indicizzatore viene usato in hello seguenti modi: 

* Eseguire una copia occasionale dei dati di hello toopopulate un indice.
* Un indice con le modifiche nell'origine dati hello in una pianificazione di sincronizzazione. pianificazione di Hello fa parte della definizione di indicizzatore hello.
* Richiamare tooupdate su richiesta un indice in base alle esigenze. 

Un **indicizzatore** è utile quando si desidera che gli aggiornamenti periodici tooan indice. È possibile impostare una pianificazione inline come parte di una definizione di indicizzatore oppure eseguire una pianificazione su richiesta usando l'operazione di [esecuzione di un indicizzatore](#RunIndexer). 

Oggetto **origine dati** specifica quali dati devono toobe indicizzata, le credenziali tooaccess hello dati e criteri tooenable ricerca di Azure tooefficiently identificare le modifiche nei dati di hello (ad esempio righe modificate o eliminate in una tabella di database). È definita come risorsa indipendente affinché possa essere usata da più indicizzatori.

Hello seguenti origini dati è attualmente supportata:

* **Database SQL di Azure** e **SQL Server in Macchine virtuali di Azure**. Per una procedura dettagliata, vedere [questo articolo](search-howto-connecting-azure-sql-database-to-azure-search-using-indexers.md). 
* **Azure Cosmos DB**. Per una procedura dettagliata, vedere [questo articolo](search-howto-index-documentdb.md). 
* **Archiviazione Blob di Azure**, tra cui seguente hello formati di documenti: PDF, Microsoft Office (DOCX/DOC, XSLX o XLS, PPTX/PPT, MSG), HTML, XML, ZIP e testo normale file (inclusi JSON). Per una procedura dettagliata, vedere [questo articolo](search-howto-indexing-azure-blob-storage.md).
* **Archivio tabelle di Azure**. Per una procedura dettagliata, vedere [questo articolo](search-howto-indexing-azure-tables.md).

Microsoft sta esaminando l'aggiunta del supporto per origini dati aggiuntive in hello future. toohelp ci priorità queste decisioni, fornire commenti e suggerimenti su hello [forum sul feedback su ricerca di Azure](http://feedback.azure.com/forums/263029-azure-search).

Vedere [limiti dei servizi](search-limits-quotas-capacity.md) per massimo limita risorse correlate a tooindexer e dati di origine.

## <a name="typical-usage-flow"></a>Flusso di utilizzo tipico
È possibile creare e gestire le origini dati e gli indicizzatori tramite semplici richieste HTTP (POST, GET, PUT, DELETE) su una risorsa `data source` o `indexer` specifica.

Per l'impostazione dell'indicizzazione automatica è in genere necessario un processo in quattro fasi:

1. Identificare hello dati origine che contiene dati hello deve toobe indicizzato. Tenere presente che ricerca di Azure potrebbe non supportare tutti i tipi di dati hello presenti nell'origine dati. Vedere [tipi di dati supportati](https://msdn.microsoft.com/library/azure/dn798938.aspx) per elenco hello.
2. Creare un indice di Ricerca di Azure con uno schema compatibile con l'origine dati.
3. Creare un'origine dati di Ricerca di Azure, come descritto nella sezione [Creare un'origine dati](#CreateDataSource).
4. Creare un indicizzatore di ricerca di Azure, come descritto in [Creare un indicizzatore](#CreateIndexer).

È consigliabile pianificare la creazione di un indicizzatore per ogni combinazione di indice di destinazione e origine dati. È possibile avere più indicizzatori scrivano nello hello stesso indice ed è possibile riutilizzare hello stessa origine dati per più indicizzatori. Tuttavia, un indicizzatore può utilizzare solo un'origine dati alla volta e può solo scrivere tooa singolo indice. 

Dopo aver creato un indicizzatore, è possibile recuperare lo stato di esecuzione mediante hello [ottenere lo stato dell'indicizzatore](#GetIndexerStatus) operazione. È anche possibile eseguire un indicizzatore in qualsiasi momento (anziché o in aggiunta toorunning periodicamente in base a una pianificazione) utilizzando hello [eseguire indicizzatore](#RunIndexer) operazione.

<!-- MSDN has 2 art files plus a API topic link list -->


## <a name="create-data-source"></a>Creare un'origine dati
In ricerca di Azure, un'origine dati viene utilizzata con gli indicizzatori, che fornisce informazioni di connessione hello per l'aggiornamento dei dati ad hoc o pianificato di un indice di destinazione. È possibile creare una nuova origine dati in Ricerca di Azure mediante una richiesta HTTP POST.

    POST https://[service name].search.windows.net/datasources?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

In alternativa, è possibile usare PUT e specificare il nome di origine dati hello in hello URI. Se l'origine dati hello non esiste, verrà creato.

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]

> [!NOTE]
> numero massimo di Hello di origini dati consentito varia in base al piano tariffario. servizio gratuito Hello consente le origini dati too3. Nel servizio standard sono consentite 50 origini dati. Per informazioni dettagliate, vedere l'articolo relativo ai [limiti del servizio](search-limits-quotas-capacity.md) .
> 
> 

**Richiesta**

Per tutte le richieste del servizio, è necessario usare il protocollo HTTPS. Hello **Crea origine dati** richiesta può essere costruita utilizzando un metodo POST o PUT. Quando si usa POST, è necessario fornire un nome dell'origine dati nel corpo di richiesta hello insieme definizione dell'origine dati hello. Con PUT, il nome di hello fa parte dell'URL hello. Se l'origine dati hello non esiste, viene creato. Se esiste già, è aggiornato toohello nuova definizione. 

nome dell'origine dati Hello deve essere in minuscolo, iniziare con una lettera o un numero, avere senza barre o punti e minore di 128 caratteri. Dopo l'avvio di nome dell'origine dati hello con una lettera o un numero, il resto di hello del nome hello può includere qualsiasi lettera, numero e trattino, purché i trattini hello non siano consecutivi. Per informazioni dettagliare, vedere [Regole di denominazione](https://msdn.microsoft.com/library/azure/dn857353.aspx) .

Hello `api-version` è obbligatorio. la versione corrente di Hello è `2015-02-28`.

**Intestazioni della richiesta**

Hello seguente elenco descrive hello necessari e le intestazioni di richiesta facoltativo. 

* `Content-Type`: elemento obbligatorio. Impostare questa proprietà troppo`application/json`
* `api-key`: elemento obbligatorio. Hello `api-key` è usato tooauthenticate hello richiesta tooyour servizio di ricerca. È un valore stringa, il servizio tooyour univoco. Hello **Crea origine dati** richiesta deve includere un `api-key` tooyour chiave di amministrazione (come chiave di query anziché tooa) impostare l'intestazione. 

È necessario anche l'URL della richiesta hello tooconstruct nome servizio hello. È possibile ottenere nome servizio hello e `api-key` dal dashboard servizi nel hello [portale Azure](https://portal.azure.com/). Vedere [creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) per informazioni sull'esplorazione della pagina.

<a name="CreateDataSourceRequestSyntax"></a>
**Sintassi del corpo della richiesta**

corpo Hello della richiesta di hello contiene una definizione dell'origine dati, inclusi tipo di origine dati hello, dati di hello tooread credenziali, nonché un rilevamento delle modifiche dati facoltativi e modificata i criteri che sono utilizzati tooefficiently identificare rilevamento dell'eliminazione dei dati o eliminati dati nell'origine dati di hello se usato con un indicizzatore pianificato periodicamente. 

sintassi di Hello per la struttura di payload della richiesta hello è come indicato di seguito. Più avanti in questo argomento è riportata una richiesta di esempio.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello data source",
        "description" : "Optional. Anything you want, or nothing at all",
        "type" : "Required. Must be one of 'azuresql', 'documentdb', 'azureblob', or 'azuretable'",
        "credentials" : { "connectionString" : "Required. Connection string for your data source" },
        "container" : { "name" : "Required. hello name of hello table, collection, or blob container you wish tooindex" },
        "dataChangeDetectionPolicy" : { Optional. See below for details }, 
        "dataDeletionDetectionPolicy" : { Optional. See below for details }
    }

Richiesta contiene hello le proprietà seguenti: 

* `name`: elemento obbligatorio. nome Hello dell'origine dati hello. Nome dell'origine dati deve solo contenere lettere minuscole, cifre o trattini, non può iniziare o terminare con trattini e caratteri too128 limitato.
* `description`: descrizione facoltativa. 
* `type`: elemento obbligatorio. Deve essere uno dei tipi di origini dati hello è supportato:
  * `azuresql` - database SQL di Azure e SQL Server in macchine virtuali di Azure
  * `documentdb` - Azure Cosmos DB
  * `azureblob` - Archiviazione BLOB di Azure
  * `azuretable` - Archivio tabelle di Azure
* `credentials`:
  * Hello necessario `connectionString` proprietà specifica la stringa di connessione hello per l'origine dati hello. formato di Hello hello della stringa di connessione dipende dal tipo di origine dati hello: 
    * Per SQL Azure, si tratta di stringa di connessione SQL Server normale hello. Se si sta utilizzando una stringa di connessione hello hello tooretrieve portale Azure, utilizzare hello `ADO.NET connection string` opzione.
    * Per Azure Cosmos DB, la stringa di connessione hello deve essere nel seguente formato hello: `"AccountEndpoint=https://[your account name].documents.azure.com;AccountKey=[your account key];Database=[your database id]"`. Tutti i valori hello sono obbligatori. È possibile trovarli in hello [portale di Azure](https://portal.azure.com/).  
    * Per i Blob di Azure e l'archiviazione tabelle, si tratta di stringa di connessione di account di archiviazione hello. viene descritto il formato di Hello [qui](https://azure.microsoft.com/documentation/articles/storage-configure-connection-string/). È richiesto un protocollo HTTPS per l'endpoint.  
* `container`, obbligatorio: specifica tooindex dati hello utilizzando hello `name` e `query` proprietà: 
  * `name`, elemento obbligatorio:
    * SQL Azure: specifica hello tabella o vista. È possibile usare nomi completi di schema, ad esempio `[dbo].[mytable]`.
    * DocumentDB: specifica una raccolta di hello. 
    * Archiviazione Blob di Azure: Specifica il contenitore di archiviazione hello.
    * Archiviazione tabelle di Azure: Specifica il nome di hello della tabella di hello. 
  * `query`, elemento facoltativo:
    * DocumentDB: consente di toospecify una query che appiattisce un documento JSON arbitrario in uno schema flat che ricerca di Azure può essere indicizzata.  
    * Archiviazione Blob di Azure: consente di toospecify una cartella virtuale all'interno del contenitore blob hello. Ad esempio, per il percorso blob `mycontainer/documents/blob.pdf`, `documents` può essere utilizzato come cartelle virtuali hello.
    * Archiviazione tabelle di Azure: consente di toospecify una query che i filtri hello set di righe toobe importati.
    * SQL Azure: la query non è supportata. Se questa funzionalità è necessaria, votare per [questo suggerimento](https://feedback.azure.com/forums/263029-azure-search/suggestions/9893490-support-user-provided-query-in-sql-indexer)
* Hello facoltativo `dataChangeDetectionPolicy` e `dataDeletionDetectionPolicy` proprietà sono descritte di seguito.

<a name="DataChangeDetectionPolicies"></a>
**Criteri di rilevamento delle modifiche dei dati**

scopo di Hello dei dati di modifica dei criteri di rilevamento è tooefficiently identificare gli elementi di dati modificati. I criteri supportati variano in base al tipo di origine dati hello. Le sezioni seguenti descrivono ognuno di questi criteri. 

***Criteri di rilevamento delle modifiche con limite massimo*** 

Usare questi criteri quando l'origine dati contiene una colonna o proprietà che soddisfa hello seguenti criteri:

* Tutti gli inserimenti specificano un valore per la colonna hello. 
* Elemento tooan di tutti gli aggiornamenti anche modificare il valore di hello della colonna hello. 
* il valore di Hello di questa colonna aumenta con ogni modifica.
* Le query che utilizzano un esempio di toohello simile clausola filtro `WHERE [High Water Mark Column] > [Current High Water Mark Value]` può essere eseguito in modo efficiente.

Ad esempio, quando si utilizzano origini dati SQL di Azure, un indicizzata `rowversion` è hello candidato ideale per l'utilizzo con con i criteri di limite massimo di hello. 

Questi criteri possono essere specificati come indicato di seguito:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
        "highWaterMarkColumnName" : "[a row version or last_updated column name]" 
    } 

Quando si utilizzano origini dati DB Cosmos Azure, è necessario utilizzare hello `_ts` proprietà fornita da Azure Cosmos DB. 

Quando si utilizza automaticamente le origini dati Blob di Azure, ricerca di Azure Usa un limite massimo modificare i criteri di rilevamento in base al timestamp di ultima modifica di un blob; non è necessario toospecify questo criterio manualmente.   

***Criteri di rilevamento delle modifiche integrati di SQL***

Se il database SQL supporta il [rilevamento delle modifiche](https://msdn.microsoft.com/library/bb933875.aspx), è consigliabile usare i criteri di rilevamento delle modifiche integrati di SQL. Questo criterio consente hello più efficiente il rilevamento delle modifiche, nonché le righe eliminate tooidentify di ricerca di Azure senza dover toohave una colonna esplicita "eliminazione temporanea" nello schema.

Rilevamento modifiche integrato è supportato a partire da hello seguenti versioni del database di SQL Server: 

* SQL Server 2008 R2 e versioni successive, se si usa SQL Server nelle VM di Azure.
* Database SQL di Azure V12, se si utilizza il database SQL di Azure SQL.  

Quando si usano i criteri di rilevamento delle modifiche integrati di SQL, non specificare criteri di rilevamento dell'eliminazione dei dati separati, perché questi ultimi includono il supporto predefinito per l'identificazione delle righe eliminate. 

Questi criteri possono essere usati solo con le tabelle, ma non con le visualizzazioni. È necessario tooenable rilevamento delle modifiche per tabella hello in uso prima di poter usare questo criterio. Per istruzioni, vedere [Abilitare e disabilitare il rilevamento delle modifiche](https://msdn.microsoft.com/library/bb964713.aspx) .    

Quando si struttura hello **Crea origine dati** richiesta, SQL, criteri di rilevamento modifiche integrato può essere specificato come indicato di seguito:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SqlIntegratedChangeTrackingPolicy" 
    }

<a name="DataDeletionDetectionPolicies"></a>
**Criteri di rilevamento dell'eliminazione dei dati**

scopo di Hello di criteri di rilevamento di eliminazione di dati è tooefficiently identificare gli elementi dati eliminati. Attualmente, i criteri di hello è supportato solo sono hello `Soft Delete` criteri, che consentono l'identificazione di elementi in base al valore di hello di eliminati un `soft delete` colonna o proprietà nell'origine dati hello. Questi criteri possono essere specificati come indicato di seguito:

    { 
        "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
        "softDeleteColumnName" : "hello column that specifies whether a row was deleted", 
        "softDeleteMarkerValue" : "hello value that identifies a row as deleted" 
    }

> [!NOTE]
> Sono supportate solo le colonne con valori di stringa, interi o booleani. valore utilizzato come Hello `softDeleteMarkerValue` deve essere una stringa, anche se la colonna corrispondente hello contiene valori interi o valori booleani. Ad esempio, se il valore di hello viene visualizzato nell'origine dati è 1, utilizzare `"1"` come hello `softDeleteMarkerValue`.    
> 
> 

<a name="CreateDataSourceRequestExamples"></a>
**Esempi del corpo della richiesta**

Se si prevede di origine di dati toouse hello con un indicizzatore che viene eseguito in una pianificazione, questo esempio viene illustrato come toospecify modifica e l'eliminazione di criteri di rilevamento: 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy", "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" }
    }

Se si prevede solo l'origine dati di hello toouse copia occasionale dei dati hello, possono essere omesso criteri hello:

    { 
        "name" : "asqldatasource",
        "description" : "anything you want, or nothing at all",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" }
    } 

**Risposta**

Se la richiesta ha esito positivo, viene restituito il codice di stato 201 - Creato. 

<a name="UpdateDataSource"></a>

## <a name="update-data-source"></a>Aggiornare un'origine dati
È possibile aggiornare un'origine dati esistente mediante una richiesta HTTP PUT. Specificare il nome di hello di hello dati origine tooupdate nell'URI richiesta hello:

    PUT https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Hello `api-version` è obbligatorio. la versione corrente di Hello è `2015-02-28`. In [Controllo delle API di Ricerca di Azure](https://msdn.microsoft.com/library/azure/dn864560.aspx) sono presenti informazioni dettagliate sulle versioni alternative.

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

**Richiesta**

Hello sintassi del corpo della richiesta è hello stesso [Crea origine dati richieste](#CreateDataSourceRequestSyntax).

Alcune proprietà non possono essere aggiornate in un'origine dati esistente. Ad esempio, è possibile modificare il tipo di hello di un'origine dati esistente.  

Se non si desidera stringa di connessione hello toochange per un'origine dati esistente, è possibile specificare un valore letterale hello `<unchanged>` hello stringa di connessione. Ciò risulta utile nelle situazioni in cui è necessario tooupdate un'origine dati ma non dispone di stringa di connessione di accedere agevolmente toohello poiché si tratta di dati sensibili alla sicurezza.

**Risposta**

Se la richiesta ha esito positivo, viene restituito il codice di stato 201 - Creato se è stata creata una nuova origine dati, e il codice di stato 204 - Nessun contenuto se è stata aggiornata un'origine dati esistente.

<a name="ListDataSource"></a>

## <a name="list-data-sources"></a>Elencare le origini dati
Hello **List Data Sources** operazione restituisce un elenco di origini dati hello nel servizio di ricerca di Azure. 

    GET https://[service name].search.windows.net/datasources?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` è obbligatorio. la versione corrente di Hello è `2015-02-28`. 

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

**Risposta**

Se la richiesta ha esito positivo, viene restituito il codice di stato 200 - OK.

Di seguito è riportato il corpo di una risposta di esempio:

    {
      "value" : [
        {
          "name": "datasource1",
          "type": "azuresql",
          ... other data source properties
        }]
    }

Si noti che è possibile filtrare la risposta hello delle proprietà hello toojust che si è interessati. Ad esempio, se si desidera solo un elenco di nomi di origine dati, utilizzare hello OData `$select` opzione di query:

    GET /datasources?api-version=205-02-28&$select=name

In questo caso, la risposta hello hello sopra riportato sarebbe simile al seguente: 

    {
      "value" : [ { "name": "datasource1" }, ... ]
    }

Si tratta di una larghezza di banda toosave tecnica utile se si dispone di numerose origini dati nel servizio di ricerca.

<a name="GetDataSource"></a>

## <a name="get-data-source"></a>Ottenere un'origine dati
Hello **ottenere origine dati** operazione Ottiene una definizione dell'origine dati hello da ricerca di Azure.

    GET https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` è obbligatorio. la versione corrente di Hello è `2015-02-28`. 

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.

risposta Hello è simile tooexamples in [richieste di esempio che crea origine dati](#CreateDataSourceRequestExamples): 

    { 
        "name" : "asqldatasource",
        "description" : "a description",
        "type" : "azuresql",
        "credentials" : { "connectionString" : "Server=tcp:....database.windows.net,1433;Database=...;User ID=...;Password=...;Trusted_Connection=False;Encrypt=True;Connection Timeout=30;" },
        "container" : { "name" : "sometable" },
        "dataChangeDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
            "highWaterMarkColumnName" : "RowVersion" }, 
        "dataDeletionDetectionPolicy" : { 
            "@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
            "softDeleteColumnName" : "IsDeleted", 
            "softDeleteMarkerValue" : "true" }
    }

> [!NOTE]
> Non impostare hello `Accept` intestazione della richiesta troppo`application/json;odata.metadata=none` quando chiama questa API perché questa operazione causa `@odata.type` toobe attributo omesso dalla risposta hello e non sarà in grado di toodifferentiate tra rilevamento dell'eliminazione dei dati e di modifica dei dati criteri di tipi diversi. 
> 
> 

<a name="DeleteDataSource"></a>

## <a name="delete-data-source"></a>Eliminare un'origine dati
Hello **Elimina origine dati** operazione rimuove un'origine dati dal servizio di ricerca di Azure.

    DELETE https://[service name].search.windows.net/datasources/[datasource name]?api-version=[api-version]
    api-key: [admin key]

> [!NOTE]
> Se alcuni indicizzatori fanno riferimento a origine dati hello che si vuole eliminare, operazione di eliminazione hello continuerà comunque. Questi indicizzatori, tuttavia, effettueranno una transizione a uno stato di errore all'esecuzione successiva.  
> 
> 

Hello `api-version` è obbligatorio. la versione corrente di Hello è `2015-02-28`. 

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 204 Nessun contenuto.

<a name="CreateIndexer"></a>

## <a name="create-indexer"></a>Creare un indicizzatore
È possibile creare un nuovo indicizzatore in Ricerca di Azure mediante una richiesta HTTP POST.

    POST https://[service name].search.windows.net/indexers?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

In alternativa, è possibile usare PUT e specificare il nome di origine dati hello in hello URI. Se l'origine dati hello non esiste, verrà creato.

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]

> [!NOTE]
> numero massimo di Hello di indicizzatori consentito varia in base al livello di prezzo. servizio gratuito Hello consente backup too3 indicizzatori. Nel servizio standard sono consentiti 50 indicizzatori. Per informazioni dettagliate, vedere l'articolo relativo ai [limiti del servizio](search-limits-quotas-capacity.md) .
> 
> 

Hello `api-version` è obbligatorio. la versione corrente di Hello è `2015-02-28`. 

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

<a name="CreateIndexerRequestSyntax"></a>
**Sintassi del corpo della richiesta**

il corpo di Hello di hello richiesta contiene una definizione di indicizzatore, che specifica l'origine di dati di hello e hello indice di destinazione per l'indicizzazione, nonché la pianificazione di indicizzazione facoltativa e i parametri. 

sintassi di Hello per la struttura di payload della richiesta hello è come indicato di seguito. Più avanti in questo argomento è riportata una richiesta di esempio.

    { 
        "name" : "Required for POST, optional for PUT. hello name of hello indexer",
        "description" : "Optional. Anything you want, or null",
        "dataSourceName" : "Required. hello name of an existing data source",
        "targetIndexName" : "Required. hello name of an existing index",
        "schedule" : { Optional. See Indexing Schedule below. },
        "parameters" : { Optional. See Indexing Parameters below. },
        "fieldMappings" : { Optional. See Field Mappings below. },
        "disabled" : Optional boolean value indicating whether hello indexer is disabled. False by default.  
    }

**Pianificazione dell'indicizzatore**

Facoltativamente, un indicizzatore può specificare una pianificazione. Se è presente una pianificazione, indicizzatore hello viene eseguito periodicamente in base alla pianificazione. Pianificazione è hello gli attributi seguenti:

* `interval`: elemento obbligatorio. Valore di durata che specifica un intervallo o un periodo per l'esecuzione dell'indicizzatore. Hello più piccolo consentito intervallo è 5 minuti. Hello più lungo è un giorno. Il valore deve essere formattato come valore XSD "dayTimeDuration" (un subset limitato di un valore [duration ISO 8601](http://www.w3.org/TR/xmlschema11-2/#dayTimeDuration) ). modello Hello è: `"P[nD][T[nH][nM]]"`. Esempi: `PT15M` ogni 15 minuti, `PT2H` ogni due ore. 
* `startTime`: elemento obbligatorio. Data e ora UTC quando indicizzatore hello dovrebbe iniziare l'esecuzione. 

**Parametri dell'indicizzatore**

Un indicizzatore può facoltativamente specificare diversi parametri che ne influenzano il comportamento. Tutti i parametri di hello sono facoltativi.  

* `maxFailedItems`: numero hello di elementi possono avere esito negativo toobe indicizzazione prima che l'esecuzione dell'indicizzatore venga considerato in errore. Il valore predefinito è 0. Vengono restituite informazioni sugli elementi non riusciti da hello [ottenere lo stato dell'indicizzatore](#GetIndexerStatus) operazione. 
* `maxFailedItemsPerBatch`: il numero di hello di elementi possono avere esito negativo toobe indicizzate in ogni batch prima che l'esecuzione dell'indicizzatore venga considerato un errore. Il valore predefinito è 0.
* `base64EncodeKeys`: specifica se le chiavi del documento saranno codificate in base 64. Ricerca di Azure impone restrizioni sui caratteri che possono essere presenti in una chiave del documento. Tuttavia, i valori hello nei dati di origine possono contenere caratteri non validi. Se è necessario tooindex tali valori come chiavi del documento, è possibile impostare questo flag tootrue. Il valore predefinito è `false`.
* `batchSize`: Specifica il numero di hello di elementi che vengono letti dall'origine dati hello e indicizzati come singolo batch prestazioni tooimprove ordine. valore predefinito di Hello dipende dal tipo di origine dati hello: è 1000 per SQL Azure e Azure Cosmos DB e 10 per archiviazione Blob di Azure.

**Mapping dei campi**

È possibile utilizzare i mapping di campo toomap un nome di campo in hello tooa altro campo nome dell'origine dati nell'indice di destinazione hello. Si consideri ad esempio una tabella di origine con un campo `_id`. Ricerca di Azure non consente un nome di campo a partire da un carattere di sottolineatura, in modo hello campo deve essere rinominato. Questa operazione può essere eseguita utilizzando hello `fieldMappings` proprietà dell'indicizzatore hello come indicato di seguito: 

    "fieldMappings" : [ { "sourceFieldName" : "_id", "targetFieldName" : "id" } ] 

È possibile specificare più mapping dei campi. 

    "fieldMappings" : [ 
        { "sourceFieldName" : "_id", "targetFieldName" : "id" },
        { "sourceFieldName" : "_timestamp", "targetFieldName" : "timestamp" },
     ]

Per i nomi dei campi di origine e destinazione non viene fatta distinzione tra maiuscole e minuscole.

<a name="FieldMappingFunctions"></a>
***Funzioni del mapping dei campi***

Mapping dei campi può anche essere tootransform utilizzati i valori di campo di origine utilizzando *mapping di funzioni*.

Attualmente è supportata solo una di queste funzioni: `jsonArrayToStringCollection`. Analizza un campo che contiene una stringa formattata come una matrice JSON in un campo Collection nell'indice di destinazione hello. È destinata in particolare all'uso con l'indicizzatore di SQL Azure, poiché SQL non ha un tipo di dati nativo per le raccolte. È possibile usare questa funzione come descritto di seguito: 

    "fieldMappings" : [ { "sourceFieldName" : "tags", "mappingFunction" : { "name" : "jsonArrayToStringCollection" } } ] 

Ad esempio, se hello campo di origine contiene la stringa hello `["red", "white", "blue"]`, quindi il campo di destinazione hello di tipo `Collection(Edm.String)` verrà popolato con i valori hello tre `"red"`, `"white"` e `"blue"`.

Si noti che hello `targetFieldName` proprietà è facoltativa; se omesso, hello `sourceFieldName` valore viene utilizzato. 

<a name="CreateIndexerRequestExamples"></a>
**Esempi del corpo della richiesta**

esempio Hello crea un indicizzatore che copia i dati dalla tabella hello a cui fa riferimento hello `ordersds` toohello dell'origine dati `orders` indice in base a una pianificazione che inizia il 1 gennaio 2015 UTC e viene eseguito ogni ora. Ogni chiamata all'indicizzatore riuscirà se non più di 5 elementi esito negativo toobe indicizzate in ogni batch, di non più di 10 elementi toobe indicizzato in totale. 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }

**Risposta**

Se la richiesta ha esito positivo, viene restituito il codice di stato 201 - Creato.

<a name="UpdateIndexer"></a>

## <a name="update-indexer"></a>Aggiornare un indicizzatore
È possibile aggiornare un indicizzatore esistente mediante una richiesta HTTP PUT. Specificare il nome di hello di hello indicizzatore tooupdate nell'URI richiesta hello:

    PUT https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    Content-Type: application/json
    api-key: [admin key]

Hello `api-version` è obbligatorio. la versione corrente di Hello è `2015-02-28`. 

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

**Richiesta**

Hello sintassi del corpo della richiesta è hello stesso [indicizzatore creare richieste](#CreateIndexerRequestSyntax).

**Risposta**

Se la richiesta ha esito positivo, viene restituito il codice di stato 201 - Creato se è stato creato un nuovo indicizzatore, e il codice di stato 204 - Nessun contenuto se è stato aggiornato un indicizzatore esistente.

<a name="ListIndexers"></a>

## <a name="list-indexers"></a>Elencare gli indicizzatori
Hello **List Indexers** operazione restituisce l'elenco di hello di indicizzatori nel servizio di ricerca di Azure. 

    GET https://[service name].search.windows.net/indexers?api-version=[api-version]
    api-key: [admin key]


Hello `api-version` è obbligatorio. versione di anteprima Hello è `2015-02-28-Preview`. [Controllo delle versioni di Ricerca di Azure](https://msdn.microsoft.com/library/azure/dn864560.aspx) sono presenti informazioni dettagliate sulle versioni alternative.

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

**Risposta**

Se la richiesta ha esito positivo, viene restituito il codice di stato 200 - OK.

Di seguito è riportato il corpo di una risposta di esempio:

    {
      "value" : [
      {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        ... other indexer properties
      }]
    }

Si noti che è possibile filtrare la risposta hello delle proprietà hello toojust che si è interessati. Ad esempio, se si vuole solo un elenco di nomi di indicizzatore, utilizzare hello OData `$select` opzione di query:

    GET /indexers?api-version=2014-10-20-Preview&$select=name

In questo caso, la risposta hello hello sopra riportato sarebbe simile al seguente: 

    {
      "value" : [ { "name": "myindexer" } ]
    }

Si tratta di una larghezza di banda toosave tecnica utile se si dispone di molti indicizzatori nel servizio di ricerca.

<a name="GetIndexer"></a>

## <a name="get-indexer"></a>Ottenere un indicizzatore
Hello **Get Indexer** operazione Ottiene la definizione di indicizzatore hello da ricerca di Azure.

    GET https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` è obbligatorio. versione di anteprima Hello è `2015-02-28-Preview`. 

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.

risposta Hello è simile tooexamples in [indicizzatore creare richieste di esempio](#CreateIndexerRequestExamples): 

    {
        "name" : "myindexer",
        "description" : "a cool indexer",
        "dataSourceName" : "ordersds",
        "targetIndexName" : "orders",
        "schedule" : { "interval" : "PT1H", "startTime" : "2015-01-01T00:00:00Z" },
        "parameters" : { "maxFailedItems" : 10, "maxFailedItemsPerBatch" : 5, "base64EncodeKeys": false }
    }


<a name="DeleteIndexer"></a>

## <a name="delete-indexer"></a>Eliminare un indicizzatore
Hello **eliminare indicizzatore** operazione rimuove un indicizzatore dal servizio di ricerca di Azure.

    DELETE https://[service name].search.windows.net/indexers/[indexer name]?api-version=[api-version]
    api-key: [admin key]

Quando viene eliminato un indicizzatore, esecuzioni dell'indicizzatore di hello in corso in quel momento funzioneranno toocompletion, ma non altre esecuzioni verranno pianificate. Tentativi toouse che un indicizzatore inesistente comporterà il codice di stato HTTP 404 non trovato. 

Hello `api-version` è obbligatorio. versione di anteprima Hello è `2015-02-28-Preview`. 

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 204 Nessun contenuto.

<a name="RunIndexer"></a>

## <a name="run-indexer"></a>esecuzione di un indicizzatore
In aggiunta toorunning periodicamente in base alla pianificazione, un indicizzatore può anche essere richiamato su richiesta tramite hello **eseguire indicizzatore** operazione: 

    POST https://[service name].search.windows.net/indexers/[indexer name]/run?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` è obbligatorio. versione di anteprima Hello è `2015-02-28-Preview`. 

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 202 Accettato.

<a name="GetIndexerStatus"></a>

## <a name="get-indexer-status"></a>ottenere lo stato di un indicizzatore
Hello **ottenere lo stato dell'indicizzatore** operazione recupera hello corrente lo stato e cronologia di esecuzione di un indicizzatore: 

    GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=[api-version]
    api-key: [admin key]


Hello `api-version` è obbligatorio. versione di anteprima Hello è `2015-02-28-Preview`. 

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 200 OK.

corpo della risposta Hello contiene informazioni sull'ultima chiamata all'indicizzatore di hello, stato di integrità complessivo dell'indicizzatore, nonché la cronologia hello delle chiamate recenti (se presente). 

Un corpo della risposta di esempio è simile al seguente: 

    {
        "status":"running",
        "lastResult": {
            "status":"success",
            "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
         },
        "executionHistory":[ {
            "status":"success",
             "errorMessage":null,
            "startTime":"2014-11-26T03:37:18.853Z",
            "endTime":"2014-11-26T03:37:19.012Z",
            "errors":[],
            "itemsProcessed":11,
            "itemsFailed":0,
            "initialTrackingState":null,
            "finalTrackingState":null
        }]
    }

**Stato dell'indicizzatore**

Lo stato dell'indicizzatore può essere uno dei seguenti valori hello:

* `running`indica che indicizzatore hello viene eseguito normalmente. Si noti che alcune esecuzioni dell'indicizzatore hello potrebbero ancora presentare errori, pertanto è un hello toocheck buona `lastResult` anche la proprietà. 
* `error`indica che indicizzatore hello si è verificato un errore che non può essere corretto senza intervento umano. Ad esempio, le credenziali dell'origine dati hello potrebbero essere scaduto o hello schema dell'origine dati hello o dell'indice di destinazione hello è stato modificato in un rilievo modo. 

**Risultato dell'esecuzione dell'indicizzatore**

Il risultato dell'esecuzione dell'indicizzatore contiene informazioni su una singola esecuzione dell'indicizzatore. risultato più recente di Hello viene esposto come hello `lastResult` proprietà dello stato di indicizzatore hello. Altri risultati recenti, se presente, vengono restituiti come hello `executionHistory` proprietà dello stato di indicizzatore hello. 

Risultato dell'esecuzione dell'indicizzatore contiene hello le proprietà seguenti: 

* `status`: hello lo stato di esecuzione. Per informazioni dettagliate, vedere [Stato di esecuzione dell'indicizzatore](#IndexerExecutionStatus) più avanti. 
* `errorMessage`: messaggio di errore per un'esecuzione non riuscita. 
* `startTime`: ora hello UTC di avvio dell'esecuzione.
* `endTime`: ora di hello in formato UTC quando è terminata l'esecuzione. Questo valore non è impostato se l'esecuzione di hello è ancora in corso.
* `errors`: array di errori a livello di elemento, se presenti. Ogni voce contiene una chiave di documento (proprietà `key`) e un messaggio di errore (proprietà `errorMessage`). 
* `itemsProcessed`: hello numero di elementi di origine dati (ad esempio, le righe di tabella) che hello tooindex indicizzatore ha tentato durante questa esecuzione. 
* `itemsFailed`: hello numero di elementi non riusciti durante questa esecuzione.  
* `initialTrackingState`: sempre `null` per la prima esecuzione dell'indicizzatore di hello, o se i criteri di rilevamento delle modifiche dati hello non sono abilitato sull'origine dati hello usata. Se questo criterio è abilitato, nelle esecuzioni successive questo valore indica hello primo (minimo) valore di rilevamento delle elaborato da questa esecuzione. 
* `finalTrackingState`: sempre `null` se i criteri di rilevamento delle modifiche dati hello non è abilitata sull'origine dati hello usata. In caso contrario, indica hello più recente (massimo) valore di rilevamento delle elaborato correttamente da questa esecuzione. 

<a name="IndexerExecutionStatus"></a>
**Stato di esecuzione dell'indicizzatore**

Lo stato di esecuzione dell'indicizzatore acquisisce lo stato di hello di una singola esecuzione dell'indicizzatore. Hello seguente i valori possibili sono:

* `success`indica che l'esecuzione dell'indicizzatore hello è stata completata.
* `inProgress`indica che l'esecuzione dell'indicizzatore hello è in corso. 
* `transientFailure` indica che l'esecuzione dell'indicizzatore ha avuto esito negativo. Per informazioni dettagliate, vedere la proprietà `errorMessage` . Errore Hello può o non richiedere l'intervento toofix - ad esempio, la correzione di un'incompatibilità dello schema tra l'origine dati hello e indice di destinazione hello richiede intervento dell'utente, mentre un tempo di inattività di origine di dati temporanei non. Le chiamate all'indicizzatore continuano in base alla pianificazione, se presente. 
* `persistentFailure`indica che un indicizzatore hello non è riuscito in modo che richiede l'intervento. Le esecuzioni pianificate dell'indicizzatore vengono arrestate. Dopo aver risolto il problema di hello, utilizzare esecuzioni di reimpostazione delle API di indicizzatore toorestart hello pianificata. 
* `reset`indica che un indicizzatore hello è stato ripristinato da un tooReset chiamata API di indicizzatore (vedere sotto). 

<a name="ResetIndexer"></a>

## <a name="reset-indexer"></a>Reimpostare un indicizzatore
Hello **reimpostare indicizzatore** operazione Reimposta stato associato all'indicizzatore hello di rilevamento delle modifiche di hello. In questo modo si tootrigger da zero evita la reindicizzazione (ad esempio, se è stato modificato lo schema di origine dati) o toochange hello dati Modifica criteri di rilevamento per un'origine dati associata a un indicizzatore hello.   

    POST https://[service name].search.windows.net/indexers/[indexer name]/reset?api-version=[api-version]
    api-key: [admin key]

Hello `api-version` è obbligatorio. versione di anteprima Hello è `2015-02-28-Preview`. 

Hello `api-key` deve essere una chiave amministratore (come chiave di query anziché tooa). Fare riferimento a sezione autenticazione toohello in [API REST di ricerca](https://msdn.microsoft.com/library/azure/dn798935.aspx) toolearn ulteriori informazioni sulle chiavi. [Creare un servizio di ricerca nel portale di hello](search-create-service-portal.md) viene illustrato l'URL del servizio tooget hello e proprietà chiave utilizzato nella richiesta di hello.

**Risposta**

Se la risposta ha esito positivo, viene restituito il codice di stato 204 Nessun contenuto.

## <a name="mapping-between-sql-data-types-and-azure-search-data-types"></a>Mapping tra tipi di dati SQL e tipi di dati di Ricerca di Azure
<table style="font-size:12">
<tr>
<td>Tipo di dati SQL</td>    
<td>Tipi di campi dell'indice di destinazione consentiti</td>
<td>Note</td>
</tr>
<tr>
<td>bit</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>int, smallint, tinyint</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>bigint</td>
<td>Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>real, float</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>smallmoney, money<br>decimal<br>numeric
</td>
<td>Edm.String</td>
<td>Ricerca di Azure non supporta la conversione di tipi decimali in Edm.Double, perché in tal caso si perderebbe la precisione
</td>
</tr>
<tr>
<td>char, nchar, varchar, nvarchar</td>
<td>Edm.String<br/>Collection(Edm.String)</td>
<td>Vedere [funzioni di Mapping campi](#FieldMappingFunctions) in questo documento per informazioni dettagliate su come una colonna stringa in una Collection tootransform</td>
</tr>
<tr>
<td>smalldatetime, datetime, datetime2, date, datetimeoffset</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>uniqueidentifer</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>geography</td>
<td>Edm.GeographyPoint</td>
<td>Sono supportate solo le istanze geografiche di tipo POINT con SRID 4326 (ovvero hello (impostazione predefinita)</td>
</tr>
<tr>
<td>rowversion</td>
<td>N/D</td>
<td>Colonne di versione di riga non possono essere archiviate nell'indice di ricerca hello, ma possono essere utilizzati per il rilevamento delle modifiche</td>
</tr>
<tr>
<td>time, timespan<br>binary, varbinary, image<br>XML, geometry, tipi CLR</td>
<td>N/D</td>
<td>Non supportate</td>
</tr>
</table>

## <a name="mapping-between-json-data-types-and-azure-search-data-types"></a>Mapping tra tipi di dati JSON e tipi di dati di Ricerca di Azure
<table style="font-size:12">
<tr>
<td>Tipo di dati JSON</td>    
<td>Tipi di campi dell'indice di destinazione consentiti</td>
<td>Note</td>
</tr>
<tr>
<td>bool</td>
<td>Edm.Boolean, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Numeri integrali</td>
<td>Edm.Int32, Edm.Int64, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Numeri a virgola mobile</td>
<td>Edm.Double, Edm.String</td>
<td></td>
</tr>
<tr>
<td>string</td>
<td>Edm.String</td>
<td></td>
</tr>
<tr>
<td>Matrici di tipi primitivi, ad esempio "a", "b", "c"</td>
<td>Collection(Edm.String)</td>
<td></td>
</tr>
<tr>
<td>Stringhe che rappresentano date</td>
<td>Edm.DateTimeOffset, Edm.String</td>
<td></td>
</tr>
<tr>
<td>Oggetti punto GeoJSON</td>
<td>Edm.GeographyPoint</td>
<td>I punti GeoJSON sono oggetti JSON in hello seguente formato: {"type": "Punto", "coordinate": [lat lunga]} </td>
</tr>
<tr>
<td>Altri oggetti JSON</td>
<td>N/D</td>
<td>Non supportati. Ricerca di Azure attualmente supporta solo tipi primitivi e raccolte di stringhe</td>
</tr>
</table>
