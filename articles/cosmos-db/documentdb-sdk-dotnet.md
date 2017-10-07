---
title: aaaAzure Cosmos DB .NET SDK e risorse | Documenti Microsoft
description: Altre informazioni sui hello .NET API e SDK tra date di rilascio, date di ritiro e le modifiche apportate tra ogni versione di hello Azure Cosmos DB .NET SDK.
services: cosmos-db
documentationcenter: .net
author: rnagpal
manager: jhubbard
editor: cgronlun
ms.assetid: 8e239217-9085-49f5-b0a7-58d6e6b61949
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/11/2017
ms.author: rnagpal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0ec30e0130067a9b8d4c9176cf7465bac8925bf9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-net-sdk-download-and-release-notes"></a>Azure Cosmos DB .NET SDK: download e note sulla versione
> [!div class="op_single_selector"]
> * [.NET](documentdb-sdk-dotnet.md)
> * [Feed delle modifiche .NET](documentdb-sdk-dotnet-changefeed.md)
> * [.NET Core](documentdb-sdk-dotnet-core.md)
> * [Node.js](documentdb-sdk-node.md)
> * [Java](documentdb-sdk-java.md)
> * [Python](documentdb-sdk-python.md)
> * [REST](https://docs.microsoft.com/rest/api/documentdb/)
> * [Provider di risorse REST](https://docs.microsoft.com/rest/api/documentdbresourceprovider/)
> * [SQL](https://msdn.microsoft.com/library/azure/dn782250.aspx)
> 
> 

<table>

<tr><td>**Download dell'SDK**</td><td>[NuGet](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB/)</td></tr>

<tr><td>**Documentazione sull'API**</td><td>[Documentazione di riferimento API .NET](/dotnet/api/overview/azure/cosmosdb?view=azure-dotnet)</td></tr>

<tr><td>**Esempi**</td><td>[Esempi di codice .NET](documentdb-dotnet-samples.md)</td></tr>

<tr><td>**Introduzione**</td><td>[Introduzione a hello Azure Cosmos DB .NET SDK](documentdb-get-started.md)</td></tr>

<tr><td>**Esercitazione sull'app Web**</td><td>[Sviluppo di applicazioni Web con Azure Cosmos DB](documentdb-dotnet-application.md)</td></tr>

<tr><td>**Framework attualmente supportato**</td><td>[Microsoft .NET Framework 4.5](https://www.microsoft.com/download/details.aspx?id=30653)</td></tr>
</table></br>

## <a name="release-notes"></a>Note sulla versione

### <a name="a-name11701170"></a><a name="1.17.0"/>1.17.0 

* Aggiunta del supporto per PartitionKeyRangeId come un FeedOption per definire l'ambito di valore di intervallo di chiavi di query risultati tooa partizione specifica. 
* Aggiunta del supporto per StartTime come un toostart ChangeFeedOption cercando modifiche hello dopo tale periodo di tempo.

### <a name="a-name11611161"></a><a name="1.16.1"/>1.16.1
* Risolto un problema in hello classe JsonSerializable che potrebbe causare un'eccezione di overflow dello stack.

### <a name="a-name11601160"></a><a name="1.16.0"/>1.16.0
*   Risolto un problema che hanno richiesto la ricompilazione di un'applicazione hello a causa di introduzione toohello di JsonSerializerSettings come un parametro facoltativo nel costruttore DocumentClient hello.
* Hello contrassegnata DocumentClient costruttore obsoleta necessari JsonSerializerSettings hello tooallow parametro ultimo per i valori predefiniti dei parametri ConnectionPolicy e ConsistencyLevel quando vengono passati nel parametro JsonSerializerSettings.

### <a name="a-name11501150"></a><a name="1.15.0"/>1.15.0
*   Aggiunta del supporto per la definizione di JsonSerializerSettings personalizzate durante la creazione di un'istanza di [DocumentClient](/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet).

### <a name="a-name11411141"></a><a name="1.14.1"/>1.14.1
*   Risolto un problema che interessava i computer x64 che non supportano l'istruzione SSE4 e generano una SEHException durante l'esecuzione di query nell'API di DocumentDB di Azure Cosmos DB.

### <a name="a-name11401140"></a><a name="1.14.0"/>1.14.0
*   Aggiunta del supporto per un nuovo livello di coerenza denominato ConsistentPrefix.
*   Aggiunta del supporto per le metriche delle query per le singole partizioni.
*   Aggiunta del supporto per la limitazione delle dimensioni di hello hello del token di continuazione per le query.
*   Aggiunta del supporto per una traccia più dettagliata delle richieste non riuscite.
*   Introdotti alcuni miglioramenti delle prestazioni hello SDK.

### <a name="a-name11341134"></a><a name="1.13.4"/>1.13.4
* Stesse funzionalità della versione 1.13.3. Alcune modifiche interne.

### <a name="a-name11331133"></a><a name="1.13.3"/>1.13.3
* Stesse funzionalità della versione 1.13.2. Alcune modifiche interne.

### <a name="a-name11321132"></a><a name="1.13.2"/>1.13.2
* Risolto un problema che ignorati valore PartitionKey hello fornito FeedOptions per le query di aggregazione.
* Risolto un problema nella gestione trasparente delle partizioni durante l'esecuzione dell'ordinamento per query della partizione trasversale intermedia.

### <a name="a-name11311131"></a><a name="1.13.1"/>1.13.1
* Risolto un problema che ha causato deadlock in alcune hello async API quando utilizzato all'interno di contesto ASP.NET.

### <a name="a-name11301130"></a><a name="1.13.0"/>1.13.0
* Consente di correggere toomake SDK più failover tooautomatic resiliente a determinate condizioni.

### <a name="a-name11221122"></a><a name="1.12.2"/>1.12.2
* Correzione di un problema che causa un'eccezione WebException: Impossibile risolto nome remoto hello.
* Hello aggiunto il supporto per lettura diretta di un documento tipizzato tramite l'aggiunta di nuove API tooReadDocumentAsync di overload.

### <a name="a-name11211121"></a><a name="1.12.1"/>1.12.1
* Aggiunta del supporto LINQ per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG).
* Correzione per un problema di perdita di memoria per oggetto ConnectionPolicy hello causato dall'uso di hello del gestore eventi.
* Correzione per un problema relativo al mancato funzionamento di UpsertAttachmentAsync in caso di uso di ETag.
* Correzione di un problema relativo al mancato funzionamento della continuazione della query di tipo order-by tra partizioni in caso di ordinamento in un campo di tipo stringa.

### <a name="a-name11201120"></a><a name="1.12.0"/>1.12.0
* Aggiunta del supporto per le query di aggregazione (COUNT, MIN, MAX, SUM e AVG). Vedere [Supporto dell'aggregazione](documentdb-sql-query.md#Aggregates).
* Più basso di velocità effettiva minima per le raccolte partizionate da 10,100 UR/sec too2500 UR/sec.

### <a name="a-name11141114"></a><a name="1.11.4"/>1.11.4
* Correzione di un problema in cui alcune delle query tra partizioni hello non venivano eseguiti nel processo host a 32 bit hello.
* Correzione di un problema in cui il contenitore di sessione hello non è stato viene aggiornato con token hello per le richieste non riuscite in modalità di Gateway.
* Correzione di un problema che causava, in alcuni casi, l'esito negativo di una query con chiamate definite dall'utente nella proiezione.
* Correzioni per le prestazioni sul lato client per aumentare hello lettura e scrittura di velocità effettiva di richieste di hello.

### <a name="a-name11131113"></a><a name="1.11.3"/>1.11.3
* Correzione di un problema in cui il contenitore di sessione hello non è stato viene aggiornato con token hello per le richieste non riuscite.
* Aggiunta del supporto per toowork SDK hello in un processo host a 32 bit. Si noti che se si usano query tra partizioni, è consigliabile usare l'elaborazione dell'host a 64 bit per migliorare le prestazioni.
* Prestazioni migliorate per gli scenari che riguardano query con un numero elevato di valori della chiave di partizione in un'espressione IN.
* Popolato varie statistiche di quota di risorse in hello ResourceResponse per raccolta richieste di lettura quando è impostata l'opzione richiesta PopulateQuotaInfo.

### <a name="a-name11111111"></a><a name="1.11.1"/>1.11.1
* Correzione delle prestazioni secondaria per hello API CreateDocumentCollectionIfNotExistsAsync introdotta in 1.11.0.
* Correzione di prestazioni in hello SDK per scenari che comportano un livello elevato di richieste simultanee.

### <a name="a-name11101110"></a><a name="1.11.0"/>1.11.0
* Supporto per nuove hello di classi e metodi tooprocess [modificare feed](change-feed.md) di documenti all'interno di una raccolta.
* Supporto per la continuazione della query tra partizioni e miglioramenti delle prestazioni per le query tra partizioni.
* Aggiunta dei metodi CreateDatabaseIfNotExistsAsync e CreateDocumentCollectionIfNotExistsAsync.
* Supporto di LINQ per le funzioni di sistema: IsDefined, IsNull e IsPrimitive.
* Correzione automatica binplacing della cartella bin del Microsoft.Azure.Documents.ServiceInterop.dll e DocumentDB.Spatial.Sql.dll assembly tooapplication quando si utilizza il pacchetto Nuget di hello ai progetti con gli strumenti di Project.
* Supporto per l'emissione di tracce ETW lato client che possono essere utili in scenari di debug.

### <a name="a-name11001100"></a><a name="1.10.0"/>1.10.0
* Aggiunto il supporto per la connettività diretta delle raccolte partizionate.
* Prestazioni migliorate per il livello di coerenza con obsolescenza hello.
* Aggiunta Polygon e LineString DataTypes quando si specifica il criterio di indicizzazione per la raccolta criteri per le query spaziali di geo-fencing.
* Aggiunto il supporto LINQ per StringEnumConverter, IsoDateTimeConverter e UnixDateTimeConverter durante la traduzione dei predicati.
* Varie correzioni di bug dell'SDK.

### <a name="a-name195195"></a><a name="1.9.5"/>1.9.5
* Risolto un problema che ha provocato un hello seguente NotFoundException: hello leggere sessione non è disponibile per il token di sessione di input hello. In alcuni casi, questa eccezione si è verificato quando si eseguono query per hello area lettura di un account geograficamente distribuite.
* Proprietà ResponseStream hello in hello ResourceResponse classe, che consente di flusso sottostante toohello di accesso diretto da una risposta esposta.

### <a name="a-name194194"></a><a name="1.9.4"/>1.9.4
* Hello modificato ResourceResponse, FeedResponse, StoredProcedureResponse e MediaResponse classi tooimplement hello corrispondente interfaccia pubblica in modo che può essere esempio per test basati sui distribuzione (TDD).
* Risolto un problema che causava un'intestazione di chiave di partizione non valida con l'uso di un oggetto JsonSerializerSettings personalizzato per la serializzazione dei dati.

### <a name="a-name193193"></a><a name="1.9.3"/>1.9.3
* Risolto un problema che ha causato lunga query toofail con errore: token di autorizzazione non è valido in hello ora corrente.
* Fissa un problema che rimosso hello SqlParameterCollection originale da tra query top/order by della partizione.

### <a name="a-name192192"></a><a name="1.9.2"/>1.9.2
* Aggiunta del supporto per le query parallele nelle raccolte partizionate.
* Aggiunta del supporto ORDER BY e TOP tra partizioni per le raccolte partizionate.
* Hello predefinito mancante riferimenti tooDocumentDB.Spatial.Sql.dll e Microsoft.Azure.Documents.ServiceInterop.dll che sono necessari quando si fa riferimento a un progetto di database Cosmos Azure con un pacchetto Nuget di Azure Cosmos DB toohello di riferimento.
* Fissa il possibilità hello toouse parametri di tipo diverso quando si utilizzano le funzioni definite dall'utente in LINQ. 
* Correzione di un bug per gli account replicati globalmente in chiamate Upsert avveniva percorsi tooread diretto invece dei percorsi di scrittura.
* Interfaccia IDocumentClient toohello metodi aggiunti mancanti: 
  * il metodo UpsertAttachmentAsync che accetta mediaStream e opzioni come parametri
  * il metodo CreateAttachmentAsync che accetta opzioni come parametro
  * il metodo CreateOfferQuery che accetta querySpec come parametro.
* Classi pubbliche non sealed che vengono esposte nell'interfaccia IDocumentClient hello.

### <a name="a-name180180"></a><a name="1.8.0"/>1.8.0
* Supporto aggiunto hello per gli account di database con più aree.
* Aggiunta del supporto per la ripetizione dei tentativi delle richieste limitate.  Utente può personalizzare il numero di hello di tentativi e tempo di attesa massimo hello configurando la proprietà ConnectionPolicy.RetryOptions hello.
* Aggiungere una nuova interfaccia IDocumentClient che definisce le firme di tutti i metodi e proprietà DocumenClient hello.  Come parte di questa modifica, modificare anche i metodi di estensione che creano IQueryable e IOrderedQueryable toomethods sul hello DocumentClient classe stessa.
* Aggiunta hello tooset opzione di configurazione ServicePoint.ConnectionLimit per un determinato endpoint di Azure Cosmos DB Uri.  Utilizzare ConnectionPolicy.MaxConnectionLimit toochange hello valore predefinito, che è impostato too50.
* IPartitionResolver e la relativa implementazione sono stati deprecati.  Il supporto per IPartitionResolver è ora obsoleto. È consigliabile usare le raccolte partizionate per un'archiviazione e una velocità effettiva superiori.

### <a name="a-name171171"></a><a name="1.7.1"/>1.7.1
* Aggiungere un tooUri overload basato su metodo ExecuteStoredProcedureAsync che accetta RequestOptions come parametro.

### <a name="a-name170170"></a><a name="1.7.0"/>1.7.0
* Aggiunto il supporto di (durata TTL) toolive di tempo per i documenti.

### <a name="a-name163163"></a><a name="1.6.3"/>1.6.3
* Correzione di un bug nel pacchetto Nuget di .NET SDK per creare il pacchetto come parte di una soluzione del servizio cloud di Azure.

### <a name="a-name162162"></a><a name="1.6.2"/>1.6.2
* Implementazione delle [raccolte partizionate](partition-data.md) e dei [livelli di prestazioni definiti dall'utente](performance-levels.md). 

### <a name="a-name153153"></a><a name="1.5.3"/>1.5.3
* **[Predefinito]**  Genera query Azure Cosmos DB endpoint: ' System.Net.Http.HttpRequestException: errore durante la copia di flusso di contenuto tooa'.

### <a name="a-name152152"></a><a name="1.5.2"/>1.5.2
* Supporto LINQ espanso, tra cui nuovi operatori per il paging, espressioni condizionali e confronto di intervalli.
  * Richiedere operatore tooenable comportamento SELECT TOP nelle query LINQ
  * Confronti degli intervalli CompareTo operatore tooenable stringa
  * Operatori Conditional (?) e Coalesce (??)
* **[Corretto]** ArgumentOutOfRangeException durante l'unione della proiezione del modello con Where-In in una query LINQ. [N. 81](https://github.com/Azure/azure-documentdb-dotnet/issues/81)

### <a name="a-name151151"></a><a name="1.5.1"/>1.5.1
* **[Predefinito]**  Se selezionare non è di tipo hello ultima espressione hello Provider LINQ non presunto Nessuna proiezione e prodotti selezionare * in modo non corretto.  [#58](https://github.com/Azure/azure-documentdb-dotnet/issues/58)

### <a name="a-name150150"></a><a name="1.5.0"/>1.5.0
* Implementazione di Upsert, aggiunti metodi UpsertXXXAsync
* Miglioramenti delle prestazioni per tutte le richieste
* Supporto del provider LINQ per metodi condizionali, coalesce e CompareTo per le stringhe
* **[Predefinito]**  Provider LINQ--> implementare contiene metodo toogenerate elenco hello SQL stesso come in IEnumerable e matrice
* **[Predefinito]**  BackoffRetryUtility utilizza hello HttpRequestMessage stesso anziché crearne uno nuovo con nuovo tentativo
* **[Obsoleto]** UriFactory.CreateCollection --&gt; Ora deve usare UriFactory.CreateDocumentCollection

### <a name="a-name141141"></a><a name="1.4.1"/>1.4.1
* **[Corretto]** Problemi di localizzazione quando si usano impostazioni cultura diverse dalla lingua inglese, ad esempio nl-NL e così via. 

### <a name="a-name140140"></a><a name="1.4.0"/>1.4.0
* Aggiunto il routing basato su IP
  * Nuovo supporto UriFactory tooassist con la creazione di collegamenti a risorse basate su ID
  * Nuovi overload in tootake DocumentClient nell'URI
* Aggiunti IsValid() and IsValidDetailed() in LINQ per i dati geospaziali
* Migliorato il supporto del provider LINQ:
  * **Matematica** : Abs, Acos, Asin, Atan, Ceiling, Cos, Exp, Floor, Log, Log10, Pow, Round, Sign, Sin, Sqrt, Tan, Truncate
  * **Stringa** : Concat, Contains, EndsWith, IndexOf, Count, ToLower, TrimStart, Replace, Reverse, TrimEnd, StartsWith, SubString, ToUpper
  * **Matrice** : Concat, Contains, Count
  * **IN**

### <a name="a-name130130"></a><a name="1.3.0"/>1.3.0
* Aggiunto il supporto per la modifica dei criteri di indicizzazione.
  * Nuovo metodo ReplaceDocumentCollectionAsync in DocumentClient
  * Nuova proprietà IndexTransformationProgress in ResourceResponse<T> per tenere traccia dello stato percentuale delle modifiche ai criteri di indice
  * DocumentCollection.IndexingPolicy è ora modificabile
* Aggiunto il supporto per query e indicizzazione spaziali.
  * Nuovo spazio dei nomi Microsoft.Azure.Documents.Spatial per la serializzazione/deserializzazione di tipi di dati spaziali come point e polygon
  * Nuova classe SpatialIndex per l'indicizzazione dei dati GeoJSON archiviati in Cosmos DB
* **[Corretto]** Query SQL non corretta generata da un'espressione LINQ [#38](https://github.com/Azure/azure-documentdb-net/issues/38).

### <a name="a-name120120"></a><a name="1.2.0"/>1.2.0
* Aggiunta una dipendenza su Newtonsoft.Json 5.0.7.
* Le modifiche apportate toosupport Order By:
  
  * Supporto del provider LINQ per OrderBy() o OrderByDescending()
  * Toosupport IndexingPolicy Order By 
    
    **Possibile modifica importante** 
    
    Se si dispone di codice esistente raccolte che esegue il provisioning con un criterio personalizzato di indicizzazione, il toobe esigenze di codice esistenti aggiornato la classe toosupport hello nuovo IndexingPolicy. Se non sono presenti criteri di indicizzazione, tale modifica non avrà alcun impatto.

### <a name="a-name110110"></a><a name="1.1.0"/>1.1.0
* Aggiunta del supporto per il partizionamento dei dati utilizzando classi HashPartitionResolver e RangePartitionResolver nuovo hello e hello IPartitionResolver.
* Aggiunta la serializzazione di DataContract.
* Aggiunto il supporto per GUID nel provider LINQ.
* Aggiunto il supporto per UDF in LINQ.

### <a name="a-name100100"></a><a name="1.0.0"/>1.0.0
* SDK con disponibilità generale

## <a name="release--retirement-dates"></a>Date di rilascio e di ritiro
Microsoft fornisce una notifica almeno **12 mesi** prima di ritirare un SDK in ordine toosmooth hello transizione tooa più recente/supportata versione.

Nuove caratteristiche e funzionalità e le ottimizzazioni vengono aggiunti solo toohello corrente SDK, pertanto è consigliabile che è sempre aggiornamento toohello SDK più recente non appena possibile. 

Qualsiasi tooAzure le richieste vengono rifiutate DB Cosmos utilizzando un SDK ritirato dal servizio hello.

<br/>

| Versione | Data di rilascio | Data di ritiro |
| --- | --- | --- |
| [1.17.0](#1.17.0) |10 agosto 2017 |--- |
| [1.16.1](#1.16.1) |07 agosto 2017 |--- |
| [1.16.0](#1.16.0) |02 agosto 2017 |--- |
| [1.15.0](#1.15.0) |30 giugno 2017 |--- |
| [1.14.1](#1.14.1) |23 maggio 2017 |--- |
| [1.14.0](#1.14.0) |10 maggio 2017 |--- |
| [1.13.4](#1.13.4) |09 maggio 2017 |--- |
| [1.13.3](#1.13.3) |06 maggio 2017 |--- |
| [1.13.2](#1.13.2) |19 aprile 2017 |--- |
| [1.13.1](#1.13.1) |29 marzo 2017 |--- |
| [1.13.0](#1.13.0) |24 marzo 2017 |--- |
| [1.12.2](#1.12.2) |20 marzo 2017 |--- |
| [1.12.1](#1.12.1) |14 marzo 2017 |--- |
| [1.12.0](#1.12.0) |15 febbraio 2017 |--- |
| [1.11.4](#1.11.4) |06 febbraio 2017 |--- |
| [1.11.3](#1.11.3) |26 gennaio 2017 |--- |
| [1.11.1](#1.11.1) |21 dicembre 2016 |--- |
| [1.11.0](#1.11.0) |08 dicembre 2016 |--- |
| [1.10.0](#1.10.0) |27 settembre 2016 |--- |
| [1.9.5](#1.9.5) |1° settembre 2016 |--- |
| [1.9.4](#1.9.4) |24 agosto 2016 |--- |
| [1.9.3](#1.9.3) |15 agosto 2016 |--- |
| [1.9.2](#1.9.2) |23 luglio 2016 |--- |
| [1.8.0](#1.8.0) |14 giugno 2016 |--- |
| [1.7.1](#1.7.1) |06 maggio 2016 |--- |
| [1.7.0](#1.7.0) |26 aprile 2016 |--- |
| [1.6.3](#1.6.3) |08 aprile 2016 |--- |
| [1.6.2](#1.6.2) |29 marzo 2016 |--- |
| [1.5.3](#1.5.3) |19 febbraio 2016 |--- |
| [1.5.2](#1.5.2) |14 dicembre 2015 |--- |
| [1.5.1](#1.5.1) |23 novembre 2015 |--- |
| [1.5.0](#1.5.0) |05 ottobre 2015 |--- |
| [1.4.1](#1.4.1) |25 agosto 2015 |--- |
| [1.4.0](#1.4.0) |13 agosto 2015 |--- |
| [1.3.0](#1.3.0) |05 agosto 2015 |--- |
| [1.2.0](#1.2.0) |06 luglio 2015 |--- |
| [1.1.0](#1.1.0) |30 aprile 2015 |--- |
| [1.0.0](#1.0.0) |08 aprile 2015 |--- |


## <a name="faq"></a>domande frequenti
[!INCLUDE [cosmos-db-sdk-faq](../../includes/cosmos-db-sdk-faq.md)]

## <a name="see-also"></a>Vedere anche
toolearn ulteriori informazioni su Cosmos DB, vedere [DB di Microsoft Azure Cosmos](https://azure.microsoft.com/services/cosmos-db/) pagina del servizio. 

