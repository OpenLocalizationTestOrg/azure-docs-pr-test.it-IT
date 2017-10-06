---
title: criteri di indicizzazione Cosmos DB aaaAzure | Documenti Microsoft
description: Informazioni sull'indicizzazione in Azure Cosmos DB. Informazioni su come tooconfigure e modificare hello criteri di indicizzazione per l'indicizzazione automatica e prestazioni migliori.
keywords: funzionamento dell'indicizzazione, indicizzazione automatica, indicizzazione del database
services: cosmos-db
documentationcenter: 
author: arramac
manager: jhubbard
editor: monicar
ms.assetid: d5e8f338-605d-4dff-8a61-7505d5fc46d7
ms.service: cosmos-db
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 08/17/2017
ms.author: arramac
ms.openlocfilehash: 4f77b352b89382aa3352136038cb0e95c7588aac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-does-azure-cosmos-db-index-data"></a>Come vengono indicizzati i dati da Azure Cosmos DB?

Per impostazione predefinita, tutti i dati di Azure Cosmos DB sono indicizzati. E anche se molti clienti sono soddisfatti toolet DB Cosmos Azure gestiscono automaticamente tutti gli aspetti dell'indicizzazione, DB Cosmos Azure supporta anche la specifica di un oggetto personalizzato **criteri di indicizzazione** per le raccolte durante la creazione. Criteri di indicizzazione nel database di Azure Cosmos sono più flessibili e potenti rispetto agli indici secondari disponibili in altre piattaforme di database, in quanto consentono di progettare e personalizzare la forma hello dell'indice hello senza pregiudicare la flessibilità dello schema. toolearn indicizzazione funzionamento in Azure Cosmos DB, è necessario comprendere che, grazie alla gestione criteri di indicizzazione, è possibile rendere con granularità fine dei compromessi tra overhead di archiviazione dell'indice, scrittura e velocità effettiva di query e la coerenza delle query.  

In questo articolo è esaminare Azure Cosmos DB criteri di indicizzazione, come è possibile personalizzare i criteri di indicizzazione e hello associati vantaggi e svantaggi. 

Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande:

* Come è possibile eseguire l'override di hello proprietà tooinclude o escludere dall'indicizzazione?
* Come è possibile configurare indice hello per eventuali aggiornamenti?
* Come è possibile configurare le query Order By o un intervallo di indicizzazione tooperform?
* Come eseguire i criteri di indicizzazione dell'insieme di modifiche tooa?
* Come confrontare archiviazione e prestazioni dei diversi criteri di indicizzazione?

## <a id="CustomizingIndexingPolicy"></a>Personalizzazione dei criteri di indicizzazione hello di una raccolta
Gli sviluppatori possono personalizzare hello compromessi tra archiviazione, le prestazioni di scrittura/query e la coerenza delle query, eseguendo l'override di criteri di indicizzazione predefiniti hello in una raccolta di Azure Cosmos DB hello seguenti aspetti di configurazione.

* **Includi/escludi documenti e percorsi da/a indice**. Gli sviluppatori possono scegliere toobe determinati documenti, escludere o includere nell'indice hello in fase di hello di inserimento o sostituzione di toohello insieme. Gli sviluppatori possono anche scegliere tooinclude o escludere determinate proprietà JSON, anche noto come i percorsi (inclusi i modelli jolly) toobe indicizzata in tutti i documenti che sono inclusi in un indice.
* **Configurazione di vari tipi di indice**. Per ognuno dei percorsi di hello incluso, gli sviluppatori possono specificare anche il tipo di hello di indice che richiedono in una raccolta in base ai dati e del carico di lavoro di query prevista e hello "precisione" per ogni percorso di stringa o numerico.
* **Configurazione delle modalità di aggiornamento dell’indice**. DB Cosmos Azure supporta tre modalità di indicizzazione che possono essere configurate tramite l'indicizzazione di criteri per una raccolta di Azure Cosmos DB hello: coerente, Lazy e None. 

Hello seguente frammento di codice .NET Mostra come tooset criteri di indicizzazione personalizzati durante la creazione di una raccolta di hello. Qui si configurare il criterio di hello con l'indice dell'intervallo per le stringhe e numeri a precisione massima hello. Questi criteri consentono di eseguire query orderby sulle stringhe.

    DocumentCollection collection = new DocumentCollection { Id = "myCollection" };

    collection.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });
    collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), collection);   


> [!NOTE]
> schema JSON Hello per criteri di indicizzazione è stato modificato con la versione di hello di versione dell'API REST degli indici di intervallo toosupport 2015-06-03 in stringhe. .NET SDK, 1.2.0 e Java, Python e Node.js SDK 1.1.0 supportano hello nuovi criteri schema. SDK precedenti utilizzare hello versione 2015-04-08 dell'API REST e lo schema precedente hello dei criteri di indicizzazione è supportato.
> 
> Per impostazione predefinita, Azure Cosmos DB indicizza tutte le proprietà delle stringhe nei documenti in modo coerente con un indice hash e le proprietà numeriche con un indice di intervallo.  
> 
> 

### <a name="customizing-hello-indexing-policy-using-hello-portal"></a>Personalizzazione dei criteri di indicizzazione hello tramite il portale di hello

È possibile modificare i criteri di una raccolta tramite il portale di Azure hello di indicizzazione hello. Aprire il proprio account Azure Cosmos DB in hello portale di Azure, selezionare la raccolta, dal menu di navigazione a sinistra hello **impostazioni**, quindi fare clic su **criteri di indicizzazione**. In hello **criteri di indicizzazione** pannello, modificare i criteri di indicizzazione e quindi fare clic su **OK** toosave le modifiche. 

### <a id="indexing-modes"></a>Modalità di indicizzazione del database
DB Cosmos Azure supporta tre indicizzazione modalità che possono essere configurate tramite l'indicizzazione di criteri per una raccolta di Azure Cosmos DB: hello coerenti, Lazy e nessuno.

**Coerente**: se i criteri della raccolta di un database di Azure Cosmos sono designato come "coerente", le query hello in poi raccolta Azure Cosmos DB determinato hello stesso livello di coerenza specificato per il punto di hello-letture (vale a dire sicuro, con-obsolescenza, sessione o eventuale). indice di Hello viene aggiornato in modo sincrono come parte dell'aggiornamento del documento hello (ad esempio insert, replace, update e delete di un documento in una raccolta di Azure Cosmos DB).  Indicizzazione coerente supporta le query coerente al costo di hello di riduzione della velocità effettiva di scrittura. La riduzione è una funzione di percorsi hello univoco necessario toobe indicizzati e hello "livello di coerenza". La modalità di indicizzazione coerente è progettata per carichi di lavoro "scrivi rapidamente, esegui query immediatamente".

**Lazy**: velocità di inserimento tooallow massima del documento, una raccolta di Azure Cosmos DB può essere configurata con coerenza lazy, ovvero le query sono alla fine coerente. indice Hello viene aggiornato in modo asincrono quando una raccolta di Azure Cosmos DB è inattivo, ovvero quando la capacità di velocità effettiva della raccolta hello non è completamente utilizzata tooserve le richieste degli utenti. Per carichi di lavoro “inserisci ora, esegui la query più tardi” che richiedono l’inserimento del documento senza alcun impedimento, la modalità di indicizzazione “differita” è più adatta.

**Nessuna**: una raccolta contrassegnata con la modalità "Nessuna" non include indici associati. Questa opzione si usa in genere se Azure Cosmos DB viene usato come archivio di coppie chiave-valore e l'accesso ai documenti avviene solo tramite la relativa proprietà ID. 

> [!NOTE]
> Configurazione hello criteri con "None" di indicizzazione ha effetto collaterale di hello di eliminazione di un indice esistente. Utilizzare questa opzione se i modelli di accesso richiedono solo "id" e/o "self-link".
> 
> 

Hello seguente mostra di esempio come crea una raccolta di Azure Cosmos DB con l'indicizzazione automatica coerente in tutti gli inserimenti documento hello .NET SDK.

Hello nella tabella seguente mostra la coerenza di hello per le query in base alla modalità indicizzazione hello (coerenti e Lazy) configurata per hello insieme e hello coerenza livello specificato per la richiesta di query hello. Questo si applica tooqueries apportate tramite qualsiasi SDK interfaccia - l'API REST o all'interno di stored procedure e trigger. 

|Coerenza|Modalità di indicizzazione: coerente|Modalità di indicizzazione: differita|
|---|---|---|
|Assoluta|Assoluta|Finale|
|Obsolescenza associata|Obsolescenza associata|Finale|
|Sessione|Sessione|Finale|
|Finale|Finale|Finale|

Azure Cosmos DB restituisce un errore per le query eseguite su raccolte con modalità di indicizzazione Nessuna. È possibile eseguire query ancora come analisi tramite hello esplicita `x-ms-documentdb-enable-scan` intestazione hello API REST o hello `EnableScanInQuery` richiesta utilizzando opzione hello .NET SDK. Alcune funzionalità di query, ad esempio ORDER BY, non sono supportati come analisi con `EnableScanInQuery`.

Hello nella tabella seguente viene illustrata la coerenza di hello per le query in base alla modalità di indicizzazione hello (coerenti, Lazy e nessuna) quando è specificato EnableScanInQuery.

|Coerenza|Modalità di indicizzazione: coerente|Modalità di indicizzazione: differita|Modalità di indicizzazione: nessuna|
|---|---|---|---|
|Assoluta|Assoluta|Finale|Assoluta|
|Obsolescenza associata|Obsolescenza associata|Finale|Obsolescenza associata|
|Sessione|Sessione|Finale|Sessione|
|Finale|Finale|Finale|Finale|

Hello seguente Mostra esempio di codice come crea una raccolta di Azure Cosmos DB con hello SDK .NET di indicizzazione coerente in tutti gli inserimenti di documento.

     // Default collection creates a hash index for all string fields and a range index for all numeric    
     // fields. Hash indexes are compact and offer efficient performance for equality queries.

     var collection = new DocumentCollection { Id ="defaultCollection" };

     collection.IndexingPolicy.IndexingMode = IndexingMode.Consistent;

     collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("mydb"), collection);


### <a name="index-paths"></a>Percorsi di indice
Azure DB Cosmos come alberi di modelli di documenti JSON e indice hello e consente toopolicies tootune per i percorsi all'interno dell'albero di hello. All'interno dei documenti è possibile scegliere i percorsi da includere o escludere dall'indicizzazione. Questo può offrire prestazioni migliorate di scrittura e archiviazione per gli scenari di indice inferiore quando i modelli di query hello sono noti in anticipo.

Percorsi di indice iniziano con la radice hello (/) e terminano con hello? carattere jolly, che indica che sono presenti più valori possibili per il prefisso hello. Ad esempio, tooserve SELECT * FROM F.familyName WHERE famiglie F = "Andersen", è necessario includere un percorso di indice per /familyName/? nei criteri di indice della raccolta hello.

Percorsi di indice possono inoltre utilizzare hello * comportamento hello toospecify dell'operatore con caratteri jolly per in modo ricorsivo i percorsi in prefisso hello. Ad esempio, payload / * può essere utilizzato tooexclude tutto proprietà payload hello dall'indicizzazione.

Di seguito sono modelli comuni di hello per specificare i percorsi di indice:

| Path                | Descrizione/Caso d'uso                                                                                                                                                                                                                                                                                         |
| ------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| /                   | Percorso predefinito per la raccolta. Ricorsivo e applica la struttura del documento toowhole.                                                                                                                                                                                                                                   |
| /prop/?             | Percorso di indice richiesto query tooserve hello seguente (con Hash o Range tipi rispettivamente):<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                       |
| /prop/*             | Percorso di indice per tutti i percorsi nell'etichetta specificata hello. Funziona con hello seguente query<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5<br><br>SELECT FROM collection c WHERE c.prop.subprop.nextprop = "value"<br><br>SELECT FROM collection c ORDER BY c.prop         |
| /props/[]/?         | Percorso di indice richiesto tooserve iterazione e query di JOIN su matrici di elementi scalari come ["a", "b", "c"]:<br><br>SELECT tag FROM tag IN collection.props WHERE tag = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag > 5                                                                         |
| /props/[]/subprop/? | Percorso di indice richiesto tooserve iterazione e query JOIN su matrici di oggetti come [{subprop: "a"}, {subprop: "b"}]:<br><br>SELECT tag FROM tag IN collection.props WHERE tag.subprop = "value"<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag.subprop = "value"                                  |
| /prop/subprop/?     | Percorso di indice richiesto tooserve query (con Hash o Range tipi rispettivamente):<br><br>SELECT FROM collection c WHERE c.prop.subprop = "value"<br><br>SELECT FROM collection c WHERE c.prop.subprop > 5                                                                                                                    |

> [!NOTE]
> Durante l'impostazione dei percorsi di indice personalizzato, si è obbligatorio toospecify regola indicizzazione hello predefinita per l'albero intero documento hello identificato dal percorso speciale hello "/ *". 
> 
> 

Hello seguente esempio mostra come configurare un percorso specifico con l'intervallo di indicizzazione e il valore personalizzato di precisione pari a 20 byte:

    var collection = new DocumentCollection { Id = "rangeSinglePathCollection" };    

    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/Title/?", 
            Indexes = new Collection<Index> { 
                new RangeIndex(DataType.String) { Precision = 20 } } 
            });

    // Default for everything else
    collection.IndexingPolicy.IncludedPaths.Add(
        new IncludedPath { 
            Path = "/*" ,
            Indexes = new Collection<Index> {
                new HashIndex(DataType.String) { Precision = 3 }, 
                new RangeIndex(DataType.Number) { Precision = -1 } 
            }
        });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), pathRange);


### <a name="index-data-types-kinds-and-precisions"></a>Tipi di dati, tipologie e precisioni degli indici
Ora che sono state utilizzate descritto toospecify percorsi, è opportuno esaminare opzioni hello possiamo utilizzare tooconfigure hello criteri di indicizzazione per un percorso. È possibile specificare una o più definizioni di indicizzazione per ogni percorso:

* Tipo di dati: **String**, **Number**, **Point**, **Polygon** o **LineString**; può contenere una sola voce per tipo di dati per percorso.
* Tipologia indice: **Hash** (query di uguaglianza), **Range** (query di uguaglianza, intervallo o orderby) o **Spatial** (query spaziali) 
* Precisione: Per l'indice hash questo varia da 1 too8 per stringhe e numeri predefinito è 3. Per l'indice range, questo valore può essere -1 (precisione massima) e variare tra 1 e 100 (precisione massima) per valori di stringa o numerici.

#### <a name="index-kind"></a>Tipologia di indice
Azure Cosmos supporta i tipi di indice hash e di intervallo per ogni percorso (che è possibile configurare per stringhe, numeri o entrambi).

* **Hash** supporta query di uguaglianza efficienti e query JOIN. Per la maggior parte dei casi, gli indici hash non richiedono una precisione superiore al valore predefinito di hello di 3 byte. DataType può essere una stringa o un numero.
* **Range** supporta query di uguaglianza efficienti, query di intervallo (con >, <, >=, <=, !=) e query orderby. Per impostazione predefinita, anche le query orderby richiedono la precisione di indice massima (-1). DataType può essere una stringa o un numero.

DB Cosmos Azure supporta inoltre il tipo di indice spaziale hello per ogni percorso, che può essere specificato per i tipi di dati hello LineString, Polygon o punto. il valore di Hello nel percorso specificato hello deve essere un frammento GeoJSON valido come `{"type": "Point", "coordinates": [0.0, 10.0]}`.

* **Spatial** supporta query spaziali (within e distance) efficienti. DataType può essere Point, Polygon o LineString.

> [!NOTE]
> Azure Cosmos DB supporta l'indicizzazione automatica dei tipi di dati Point, Polygon e LineString.
> 
> 

Di seguito sono tipi di indice supportata hello ed esempi di query che possono essere utilizzati tooserve:

| Tipologia di indice | Descrizione/Caso d'uso                                                                                                                                                                                                                                                                                                                                                                                                              |
| ---------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Hash       | Hash over /prop/? (o /) può essere tooserve utilizzati hello seguente query in modo efficiente:<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>Hash over /props/[]/? (o / o/props) può essere tooserve utilizzati hello seguente query in modo efficiente:<br><br>SELECT tag FROM collection c JOIN tag IN c.props WHERE tag = 5                                                                                                                       |
| Range      | Range over /prop/? (o /) può essere tooserve utilizzati hello seguente query in modo efficiente:<br><br>SELECT FROM collection c WHERE c.prop = "value"<br><br>SELECT FROM collection c WHERE c.prop > 5<br><br>SELECT FROM collection c ORDER BY c.prop                                                                                                                                                                                                              |
| Spatial     | Range over /prop/? (o /) può essere tooserve utilizzati hello seguente query in modo efficiente:<br><br>SELECT FROM collection c<br><br>WHERE ST_DISTANCE(c.prop, {"type": "Point", "coordinates": [0.0, 10.0]}) < 40<br><br>SELECT FROM collection c WHERE ST_WITHIN(c.prop, {"type": "Polygon", ... }) --con indicizzazione su punti abilitata<br><br>SELECT FROM collection c WHERE ST_WITHIN({"type": "Point", ... }, c.prop) --con indicizzazione su poligoni abilitata              |

Per impostazione predefinita, viene restituito un errore per l'intervallo di query con operatori come > = Se è presente alcun indice intervallo (di qualsiasi precisione) in ordine toosignal che un'analisi potrebbe essere necessario tooserve query di hello. Le query di intervallo possono essere eseguite senza un indice di intervallo utilizzando l'intestazione x-ms-documentdb-enable-analisi hello in hello API REST o l'opzione di richiesta EnableScanInQuery hello utilizzando hello .NET SDK. Se sono presenti i filtri nella query hello utilizzabile Azure Cosmos DB hello indice toofilter contro, non verrà restituito alcun errore.

Hello stesse regole valide per le query spaziali. Per impostazione predefinita, viene restituito un errore per le query spaziali se è presente alcun indice spaziale e non sono presenti altri filtri che possono essere utilizzati dall'indice hello. Possono essere eseguite come una scansione con x-ms-documentdb-enable-scan/EnableScanInQuery.

#### <a name="index-precision"></a>Precisione indice
La precisione indice consente di raggiungere un compromesso tra archiviazione indice e prestazioni delle query. Per i numeri, è consigliabile utilizzare configurazione di precisione predefinita hello-1 ("massimo"). Poiché i numeri sono di 8 byte in JSON, si tratta configurazione tooa equivalente di 8 byte. Per selezionare un valore inferiore per la precisione, ad esempio 1-7, significa che i valori all'interno di alcuni toohello mappa intervalli stesso indice voce. Pertanto si ridurrà lo spazio di archiviazione dell'indice, ma l'esecuzione di query sia stata tooprocess più documenti, pertanto utilizzare ad esempio, una velocità effettiva maggiore di unità richieste.

La configurazione di precisione dell'indice ha un'applicazione più pratica con gli intervalli di stringhe. Poiché le stringhe possono essere di qualsiasi lunghezza arbitraria, scelta hello di precisione di hello indice può influire hello di query di intervallo di stringa e impatto hello quantità di spazio di archiviazione dell'indice. Gli indici di intervallo di stringhe possono essere configurati con valori compresi tra 1 e 100 o con il valore di precisione "massima" (-1). Se si desidera tooperform Order By query su proprietà della stringa, è necessario specificare una precisione pari a -1 per i percorsi corrispondenti hello.

Gli indici spaziali sempre utilizzano precisione dell'indice di hello predefinita per tutti i tipi (punti, LineStrings e poligoni) e non possono essere sottoposta a override. 

Hello di esempio seguente viene illustrato come precisione hello tooincrease per intervallo di indici in una raccolta tramite hello .NET SDK. 

**Creare una raccolta con una precisione di indice personalizzata**

    var rangeDefault = new DocumentCollection { Id = "rangeCollection" };

    // Override hello default policy for Strings toorange indexing and "max" (-1) precision
    rangeDefault.IndexingPolicy = new IndexingPolicy(new RangeIndex(DataType.String) { Precision = -1 });

    await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), rangeDefault);   


> [!NOTE]
> Quando una query utilizza Order By, ma non dispone di un indice di intervallo su hello percorso richiesto con la massima precisione hello, Azure Cosmos DB restituisce un errore. 
> 
> 

Allo stesso modo i percorsi possono essere completamente esclusi dall'indicizzazione. Hello nell'esempio successivo viene illustrato come tooexclude un'intera sezione di hello documenti (anche noto come un sottoalbero) dall'indicizzazione mediante hello "*" con caratteri jolly.

    var collection = new DocumentCollection { Id = "excludedPathCollection" };
    collection.IndexingPolicy.IncludedPaths.Add(new IncludedPath { Path = "/*" });
    collection.IndexingPolicy.ExcludedPaths.Add(new ExcludedPath { Path = "/nonIndexedContent/*" });

    collection = await client.CreateDocumentCollectionAsync(UriFactory.CreateDatabaseUri("db"), excluded);



## <a name="opting-in-and-opting-out-of-indexing"></a>Acconsentire e escludere l’indicizzazione
È possibile scegliere se si desidera che l'indice della tooautomatically hello raccolta tutti i documenti. Per impostazione predefinita, tutti i documenti vengono indicizzati automaticamente, ma è possibile scegliere tooturn è off. Quando l'indicizzazione è disattivata, i documenti sono accessibili solo tramite i relativi self link o le query con ID.

Con l'indicizzazione automatica disattivata, è possibile aggiungere comunque in modo selettivo solo un indice toohello documenti specifici. Al contrario, è possibile lasciare l'indicizzazione in automatico e scegliere in modo selettivo tooexclude solo a specifici documenti. L'indicizzazione o disattivare le configurazioni sono utili quando è presente solo un sottoinsieme di documenti che richiedono toobe eseguire una query.

Ad esempio, hello esempio seguente viene illustrata la modalità tooinclude un documento in modo esplicito utilizzando hello [DocumentDB API .NET SDK](https://docs.microsoft.com/en-us/azure/cosmos-db/documentdb-sdk-dotnet) hello e [RequestOptions.IndexingDirective](http://msdn.microsoft.com/library/microsoft.azure.documents.client.requestoptions.indexingdirective.aspx) proprietà.

    // If you want toooverride hello default collection behavior tooeither
    // exclude (or include) a Document from indexing,
    // use hello RequestOptions.IndexingDirective property.
    client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"),
        new { id = "AndersenFamily", isRegistered = true },
        new RequestOptions { IndexingDirective = IndexingDirective.Include });

## <a name="modifying-hello-indexing-policy-of-a-collection"></a>La modifica dei criteri di indicizzazione hello di una raccolta
Azure DB Cosmos consente volo hello toomake modifiche toohello criteri di indicizzazione di una raccolta. Una modifica nei criteri per una raccolta di Azure Cosmos DB di indicizzazione può causare tooa modifica in forma di hello dell'indice hello inclusi i percorsi possono essere indicizzati hello, relativi precisione, nonché il modello di coerenza hello di indice hello stesso. Una modifica nei criteri di indicizzazione, in modo efficace richiede quindi una trasformazione di indice precedente hello in uno nuovo. 

**Trasformazioni di indici online**

![Funzionamento dell'indicizzazione - Trasformazioni di indici online di Azure Cosmos DB](./media/indexing-policies/index-transformations.png)

Trasformazioni di indice vengono apportate in linea, vale a dire che i documenti hello indicizzati per i criteri precedenti hello vengono trasformati in modo efficiente per ogni nuovo criterio di hello **senza influire sulla disponibilità di scrittura hello o velocità effettiva di provisioning hello** di raccolta di Hello. Hello coerenza di lettura e scrittura effettuate utilizzando hello l'API REST di SDK o all'interno di stored procedure e trigger non è compromessa durante la trasformazione di indice. Ciò significa che è in delle prestazioni del sistema o tempi di inattività App tooyour quando si esegue un criterio di indicizzazione di modifica.

Tuttavia, durante la fase di hello di trasformazione di indice è in corso, le query sono alla fine coerente indipendentemente dalla hello l'indicizzazione di configurazione della modalità (Consistent o Lazy). Si applica tooqueries da tutte le interfacce: API REST, SDK, anche e all'interno di stored procedure e trigger. Come con l'indicizzazione, Lazy indice trasformazione viene eseguita in modo asincrono in background hello nelle repliche hello utilizzando risorse riserva hello disponibili per una determinata replica. 

Trasformazioni di indice vengono eseguite anche **in situ** (sul posto), ad esempio Azure Cosmos DB non gestisce due copie dell'indice di hello e scambio hello vecchio indice out con hello uno nuovo. Ciò significa che non è necessario ne consumato ulteriore spazio su disco nelle raccolte durante la trasformazione dell’indice.

Quando si modificano i criteri di indicizzazione, come le modifiche di hello vengono applicati toomove da hello vecchio indice toohello nuovo uno dipendono principalmente dalla hello indicizzazione più configurazioni di modalità quindi di hello altri valori come percorsi inclusi o esclusi, i tipi di indice e precisione. Se entrambi i criteri (vecchio e nuovo) usano l'indicizzazione coerente, Azure Cosmos DB esegue una trasformazione di indici online. Non è possibile applicare un'altra modifica criteri indicizzazione con la modalità di indicizzazione coerente durante la trasformazione hello è in corso.

È tuttavia possibile spostare tooLazy o nessuna modalità di indicizzazione durante una trasformazione è in corso. 

* Quando si sposta tooLazy, modifica dei criteri indice hello viene resa effettiva immediatamente e Azure Cosmos DB avvia ricreazione dell'indice hello in modo asincrono. 
* Quando si sposta tooNone, quindi hello indice viene eliminato effettiva immediatamente. Lo spostamento tooNone è utile quando si desidera un corso toocancel trasformazione e avvio aggiornata con i criteri di indicizzazione diversi. 

Se si utilizza .NET SDK hello, è possibile avviare una modifica dei criteri di indicizzazione utilizzando hello nuovo **ReplaceDocumentCollectionAsync** metodo e tenere traccia hello percentuale lo stato di avanzamento della trasformazione indice hello utilizzando hello  **IndexTransformationProgress** proprietà risposta da un **ReadDocumentCollectionAsync** chiamare. Altri SDK e hello API REST supportano metodi e proprietà equivalenti per apportare modifiche ai criteri di indicizzazione.

Di seguito è riportato un frammento di codice che illustra come toomodify una raccolta di criteri di indicizzazione da coerente tooLazy modalità indicizzazione.

**Modificare i criteri di indicizzazione da tooLazy coerente**

    // Switch toolazy indexing.
    Console.WriteLine("Changing from Default tooLazy IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.Lazy;

    await client.ReplaceDocumentCollectionAsync(collection);


È possibile verificare lo stato di hello di una trasformazione indice ReadDocumentCollectionAsync chiamante, ad esempio, come illustrato di seguito.

**Tenere traccia dell'avanzamento della trasformazione di indice**

    long smallWaitTimeMilliseconds = 1000;
    long progress = 0;

    while (progress < 100)
    {
        ResourceResponse<DocumentCollection> collectionReadResponse = await client.ReadDocumentCollectionAsync(
            UriFactory.CreateDocumentCollectionUri("db", "coll"));

        progress = collectionReadResponse.IndexTransformationProgress;

        await Task.Delay(TimeSpan.FromMilliseconds(smallWaitTimeMilliseconds));
    }

È possibile eliminare l'indice di hello per una raccolta spostando toohello Nessuna modalità di indicizzazione. Potrebbe trattarsi di un utile strumento operativo se si desidera toocancel una trasformazione in corso e avvia immediatamente uno nuovo.

**Eliminazione di hello indice per una raccolta**

    // Switch toolazy indexing.
    Console.WriteLine("Dropping index by changing tootoohello None IndexingMode.");

    collection.IndexingPolicy.IndexingMode = IndexingMode.None;

    await client.ReplaceDocumentCollectionAsync(collection);

Quando si apportate modifiche ai criteri di indicizzazione tooyour Azure Cosmos DB raccolte? di seguito Hello sono casi d'uso più comune di hello:

* Fornire risultati coerenti durante il normale funzionamento, ma tentare toolazy indicizzazione durante l'importazione di dati bulk
* Iniziare a usare nuove funzionalità di indicizzazione su corrente Azure Cosmos DB raccolte, ad esempio, ad esempio una query che richiedono il tipo di indice spaziale hello o Order By geospatial / stringa di query di intervallo che richiedono che la stringa hello tipo di intervallo di indice
* Selezionare manualmente hello toobe proprietà indicizzate e modificarli nel tempo
* Ottimizzare le prestazioni delle query indicizzazione tooimprove precisione o riduce lo spazio utilizzato

> [!NOTE]
> criteri di indicizzazione toomodify ReplaceDocumentCollectionAsync, necessaria la versione > = 1.3.0 di hello .NET SDK
> 
> Per l'indice trasformazione toocomplete correttamente, è necessario assicurarsi che sia sufficiente spazio di archiviazione disponibile nella raccolta di hello. Se la raccolta hello raggiunge la quota di archiviazione, verrà sospeso trasformazione indice hello. La trasformazione di indice verrà ripresa automaticamente quando lo spazio di archiviazione sarà disponibile, ad esempio, se si eliminano alcuni documenti.
> 
> 

## <a name="performance-tuning"></a>Ottimizzazione delle prestazioni
Hello APIs DocumentDB offre informazioni sulle metriche delle prestazioni, ad esempio archiviazione dell'indice hello utilizzato e velocità effettiva di hello costo (unità di richiesta) per ogni operazione. Queste informazioni può essere utilizzati toocompare vari criteri di indicizzazione e per l'ottimizzazione delle prestazioni.

quota di archiviazione toocheck hello e l'utilizzo di una raccolta, eseguire una richiesta GET o HEAD risorsa raccolta hello e controllare hello x-ms-richiesta-quota e intestazioni x-ms-richiesta-usage hello. In .NET SDK hello, hello [DocumentSizeQuota](http://msdn.microsoft.com/library/dn850325.aspx) e [DocumentSizeUsage](http://msdn.microsoft.com/library/azure/dn850324.aspx) proprietà [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) contengono questi valori corrispondenti .

     // Measure hello document size usage (which includes hello index size) against   
     // different policies.
     ResourceResponse<DocumentCollection> collectionInfo = await client.ReadDocumentCollectionAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"));  
     Console.WriteLine("Document size quota: {0}, usage: {1}", collectionInfo.DocumentQuota, collectionInfo.DocumentUsage);


overhead hello toomeasure di indicizzazione in ogni operazione di scrittura (creare, aggiornare o eliminare), esaminare l'intestazione x-ms-richiesta addebito hello (o equivalente hello [RequestCharge](http://msdn.microsoft.com/library/dn799099.aspx) proprietà [ResourceResponse < T\> ](http://msdn.microsoft.com/library/dn799209.aspx) in .NET SDK hello) numero hello toomeasure di unità di richiesta utilizzato da queste operazioni.

     // Measure hello performance (request units) of writes.     
     ResourceResponse<Document> response = await client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), myDocument);              
     Console.WriteLine("Insert of document consumed {0} request units", response.RequestCharge);

     // Measure hello performance (request units) of queries.    
     IDocumentQuery<dynamic> queryable =  client.CreateDocumentQuery(UriFactory.CreateDocumentCollectionUri("db", "coll"), queryString).AsDocumentQuery();

     double totalRequestCharge = 0;
     while (queryable.HasMoreResults)
     {
        FeedResponse<dynamic> queryResponse = await queryable.ExecuteNextAsync<dynamic>(); 
        Console.WriteLine("Query batch consumed {0} request units",queryResponse.RequestCharge);
        totalRequestCharge += queryResponse.RequestCharge;
     }

     Console.WriteLine("Query consumed {0} request units in total", totalRequestCharge);

## <a name="changes-toohello-indexing-policy-specification"></a>Specifica di criteri di indicizzazione toohello di modifiche
7 luglio 2015 con l'API REST versione 2015-06-03 è stata introdotta una modifica nello schema di hello per criteri di indicizzazione. classi corrispondenti Hello versioni SDK hello hanno nuovo schema di hello toomatch implementazioni. 

Hello dopo le modifiche sono stato implementato in hello specifica JSON:

* Il criterio di indicizzazione supporta gli indici di intervallo per le stringhe
* Ogni percorso può avere più definizioni di indice, uno per ogni tipo di dati
* La precisione di indicizzazione supporta valori da 1 a 8 per i numeri, da 1 a 100 per le stringhe e -1 (precisione massima)
* Segmenti di percorsi non richiedono un tooescape doppie ogni percorso. Ad esempio, è possibile aggiungere un percorso per /title/? invece che /"title"/?
* percorso radice Hello che rappresenta "tutti i percorsi" può essere rappresentato come / * (inoltre troppo /)

Se si dispone di codice che esegue il provisioning di raccolte con un criterio di indicizzazione personalizzato scritto con versione 1.1.0 di hello .NET SDK o versioni precedenti, sarà necessario toochange l'applicazione del codice toohandle queste modifiche tooSDK toomove ordine alla versione 1.2.0. Se non si dispone di codice che consente di configurare criteri di indicizzazione o pianificare toocontinue utilizzando una versione precedente di SDK, non sono necessarie modifiche.

Per un confronto pratico, ecco un esempio di criteri di indicizzazione personalizzati scritti utilizzando hello API REST versione 2015-06-03, nonché hello precedente versione 2015-04-08.

**JSON criterio di indicizzazione precedente**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "IncludedPaths":[
          {
             "IndexType":"Hash",
             "Path":"/",
             "NumericPrecision":7,
             "StringPrecision":3
          }
       ],
       "ExcludedPaths":[
          "/\"nonIndexedContent\"/*"
       ]
    }

**JSON criterio di indicizzazione corrente**

    {
       "automatic":true,
       "indexingMode":"Consistent",
       "includedPaths":[
          {
             "path":"/*",
             "indexes":[
                {
                   "kind":"Hash",
                   "dataType":"String",
                   "precision":3
                },
                {
                   "kind":"Hash",
                   "dataType":"Number",
                   "precision":7
                }
             ]
          }
       ],
       "ExcludedPaths":[
          {
             "path":"/nonIndexedContent/*"
          }
       ]
    }

## <a name="next-steps"></a>Passaggi successivi
Usare hello i collegamenti seguenti per esempi di gestione criteri di indice e toolearn informazioni sul linguaggio di query del database di Azure Cosmos.

1. [Esempi di codice di gestione degli indici .NET delle API DocumentDB](https://github.com/Azure/azure-documentdb-net/blob/master/samples/code-samples/IndexManagement/Program.cs)
2. [Operazione sulle raccolte di API REST DocumentDB](https://msdn.microsoft.com/library/azure/dn782195.aspx)
3. [Query con SQL](documentdb-sql-query.md)

