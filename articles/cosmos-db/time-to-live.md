---
title: aaaExpire dati nel database di Azure Cosmos con tempo toolive | Documenti Microsoft
description: "Con durata (TTL), database di Microsoft Azure Cosmos fornisce documenti toohave possibilità di hello eliminati automaticamente dal sistema hello dopo un periodo di tempo."
services: cosmos-db
documentationcenter: 
keywords: tempo toolive
author: arramac
manager: jhubbard
editor: 
ms.assetid: 25fcbbda-71f7-414a-bf57-d8671358ca3f
ms.service: cosmos-db
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: arramac
ms.openlocfilehash: 51d8ec46add72c9624457316a4ccd1e23fb83ad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a>Dati in raccolte di Azure Cosmos DB automaticamente con toolive ora di scadenza
Le applicazioni posso produrre e archiviare grandi quantità di dati. Alcuni di questi, come i dati eventi generati da computer, i registri e le informazioni sulle sessioni utente sono utili per un periodo di tempo limitato. Una volta dati hello diventano toohello surplus esigenze dell'applicazione hello è sicuro toopurge questi dati e ridurre esigenze di archiviazione hello di un'applicazione.

Con "toolive" o di durata (TTL) Cosmos DB di Microsoft Azure fornisce documenti toohave possibilità di hello eliminati dal database hello automaticamente dopo un periodo di tempo. tempo predefinito Hello toolive può essere impostato a livello di raccolta hello e sottoposto a override in una base per ogni documento. Quando il valore di TTL è impostato, come impostazione predefinita di una raccolta o a livello di documento, Cosmos DB rimuove automaticamente i documenti esistenti dopo un numero di secondi dall'ultima modifica pari a tale valore.

Tempo toolive in DB Cosmos utilizza un offset rispetto quando il documento hello dell'ultima modifica. toodo questo it Usa hello `_ts` campo disponibile per ogni documento. campo TS Hello è di tipo unix epoch timestamp che rappresentano hello data e ora. Hello `_ts` campo viene aggiornato ogni volta che un documento viene modificato. 

## <a name="ttl-behavior"></a>Comportamento di TTL
funzionalità di durata (TTL) Hello è controllata dalle proprietà di durata (TTL) a due livelli - livello di raccolta hello e livello di documento hello. i valori Hello in secondi e vengono considerati come un delta da hello `_ts` ultima modifica al documento hello.

1. DefaultTTL per raccolta hello
   
   * Se mancanti (o set toonull), i documenti non vengono eliminati automaticamente.
   * Se è presente e il valore di hello è "-1" = infinito – documenti senza scadenza per impostazione predefinita
   * Se è presente e il valore di hello è un numero ("n"), documenti scadono "n" secondi dopo l'ultima modifica
2. Durata (TTL) per i documenti hello: 
   
   * Proprietà è applicabile solo se è presente per la raccolta padre hello DefaultTTL.
   * Sostituisce il valore DefaultTTL hello per la raccolta padre hello.

Come documento hello è scaduto (`ttl`  +  `_ts` > = ora corrente del server), documento hello viene contrassegnato come "scaduto". Nessuna operazione sarà possibile in tali documenti dopo questo periodo di tempo e verranno esclusi dai risultati di hello di qualsiasi query eseguita. documenti Hello vengono eliminati fisicamente nel sistema hello e vengono eliminati in background hello in base alle esigenze in un secondo momento. Questo non utilizzare qualsiasi [unità richiesta (RUs)](request-units.md) dal budget raccolta hello.

Hello sopra logica può essere visualizzata in hello seguente matrice:

|  | DefaultTTL mancante o non è impostato su raccolta hello | DefaultTTL = -1 nella raccolta | DefaultTTL = n nella raccolta |
| --- |:--- |:--- |:--- |
| TTL mancante nel documento |Nothing toooverride a livello di documento, poiché sia il documento hello e raccolta non includono alcun concetto di durata (TTL). |I documenti in questa raccolta non scadono. |documenti Hello in questa raccolta scadrà quando n intervallo scade. |
| Durata TTL = -1 nel documento |Nothing toooverride a livello di documento hello poiché non definisce l'insieme di hello hello DefaultTTL proprietà che è possibile eseguire l'override di un documento. Durata (TTL) in un documento è non interpretato dal sistema hello. |I documenti in questa raccolta non scadono. |documento Hello con durata (TTL) =-1 in questa raccolta non ha scadenza. Tutti gli altri documenti scadono dopo l'intervallo di tempo n. |
| TTL = n nel documento |Nothing toooverride a livello di documento hello. Durata (TTL) su un documento non interpretato dal sistema hello. |documento Hello con durata (TTL) = n scadranno dopo un intervallo n, in secondi. Gli altri documenti ereditano l'intervallo -1 e non scadono. |documento Hello con durata (TTL) = n scadranno dopo un intervallo n, in secondi. Altri documenti eredita "n" l'intervallo di raccolta hello. |

## <a name="configuring-ttl"></a>Configurazione di TTL
Per impostazione predefinita, l'ora toolive è disabilitata per impostazione predefinita in tutte le raccolte di DB Cosmos e su tutti i documenti.

## <a name="enabling-ttl"></a>Abilitazione di TTL
tooenable durata (TTL) su una raccolta o documenti hello all'interno di una raccolta, è necessario tooset hello DefaultTTL proprietà tooeither una raccolta -1 o un numero positivo diverso da zero. Impostazione hello DefaultTTL troppo-1 indica che per impostazione predefinita tutti i documenti nella raccolta hello risiederanno forever ma hello servizio DB Cosmos deve monitorare questa raccolta per i documenti che hanno eseguito l'override di questa impostazione predefinita.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a>Configurazione del valore TTL predefinito in una raccolta
Si è in grado di tooconfigure toolive di tempo predefinito a un livello di raccolta. hello tooset durata (TTL) su una raccolta, è necessario un numero positivo diverso da zero che indica il periodo di hello, in secondi, tooexpire tooprovide tutti i documenti nella raccolta hello dopo hello ultima modifica del timestamp del documento hello (`_ts`). In alternativa, è possibile impostare hello predefinito troppo-1, che implica che tutti i documenti inseriti nella raccolta toohello risiederanno all'infinito per impostazione predefinita.

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a>Impostazione di TTL in un documento
Inoltre toosetting TTL predefinito su una raccolta è possibile impostare TTL specifico a un livello di documento. In questo modo sostituirà predefinito hello raccolta hello.

* hello tooset durata (TTL) in un documento, è necessario un numero positivo diverso da zero indica hello periodo, espresso in secondi, il documento hello tooexpire dopo hello ultima modifica del timestamp del documento hello tooprovide (`_ts`).
* Se un documento dispone di alcun campo di durata (TTL), quindi hello predefinito della raccolta hello verrà applicate.
* Se la durata (TTL) è disabilitata a livello di raccolta hello, campo TTL hello documento hello verrà ignorato fino durata (TTL) sia abilitata di nuovo nella raccolta di hello.

Di seguito è riportato un frammento di codice che illustra come tooset hello scadenza di durata (TTL) in un documento:

    // Include a property that serializes too"ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used tooset expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set hello value toohello expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a>Estensione di TTL in un documento esistente
È possibile reimpostare hello durata (TTL) in un documento, eseguire qualsiasi operazione di scrittura sul documento hello. In questo modo verrà impostato hello `_ts` toohello ora corrente e hello conto alla rovescia toohello documento scadenza, l'impostazione hello `ttl`, inizierà nuovamente. Se si desidera hello toochange `ttl` di un documento, è possibile aggiornare il campo hello come avviene con qualsiasi altro campo impostabile.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a>Rimozione di TTL da un documento
Se è stata impostata una durata (TTL) in un documento e non si desidera più che tooexpire documento, quindi recuperare il documento hello, rimuovere il campo di durata (TTL) hello e sostituire hello documento sul server hello. Quando il campo di durata (TTL) hello viene rimosso dal documento hello, verrà applicata predefinito hello raccolta hello. toostop un documento da scade e non erediti dall'insieme di hello è necessario tooset hello TTL valore troppo-1.

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a>Disabilitazione di TTL
toodisable TTL interamente in una raccolta e l'arresto hello background elaborare la ricerca di documenti scaduti proprietà DefaultTTL hello raccolta hello devono essere eliminati. Eliminazione di questa proprietà è diversa dall'impostazione di troppo-1. Impostazione troppo-1 significa nuovi documenti aggiunti insieme toohello risiederanno forever ma è possibile ignorare questa in documenti specifici nella raccolta di hello. Rimozione di questa proprietà dalla raccolta hello indica che i documenti non ha scadenza, anche se sono presenti documenti che hanno sottoposto a override esplicito predefinito precedente.

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a>domande frequenti
**Quanto costa la durata (TTL)?**

Non vi è alcun toosetting costi aggiuntivi una durata (TTL) in un documento.

**Quanto tempo sarà necessario toodelete documento una volta hello TTL backup?**

documenti Hello scaduti immediatamente dopo aver hello durata (TTL) sia attivo e non saranno accessibile tramite CRUD o API di query. 

**La durata (TTL) impostata per un documento influisce sugli addebiti delle unità richiesta?**

No, gli addebiti delle unità richiesta non risentono delle eliminazioni di documenti scaduti con TTL in Cosmos DB.

**Funzionalità di durata (TTL) hello si applicano solo documenti tooentire o posso scadere i valori delle proprietà di singoli documenti?**

Durata (TTL) applica toohello intero documento. Se si desidera tooexpire solo una parte di un documento, la si consiglia di estrarre la parte hello hello il documento principale nel documento "collegate" separato tooa e quindi utilizzare durata (TTL) su tale documento estratta.

**Funzionalità di durata (TTL) hello dispone di requisiti specifici di indicizzazione?**

Sì. raccolta di Hello deve contenere [set di criteri di indicizzazione](indexing-policies.md) tooeither Consistent o Lazy. Il tentativo di tooset DefaultTTL su una raccolta con l'indicizzazione set tooNone genererà un errore, come durante il tentativo di tooturn disattivare l'indicizzazione in una raccolta che dispone di un DefaultTTL già impostato.

## <a name="next-steps"></a>Passaggi successivi
toolearn ulteriori informazioni su Azure Cosmos DB, fare riferimento a servizio toohello [ *documentazione* ](https://azure.microsoft.com/documentation/services/cosmos-db/) pagina.

