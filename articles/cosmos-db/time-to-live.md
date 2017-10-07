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
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-toolive"></a><span data-ttu-id="dab51-104">Dati in raccolte di Azure Cosmos DB automaticamente con toolive ora di scadenza</span><span class="sxs-lookup"><span data-stu-id="dab51-104">Expire data in Azure Cosmos DB collections automatically with time toolive</span></span>
<span data-ttu-id="dab51-105">Le applicazioni posso produrre e archiviare grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="dab51-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="dab51-106">Alcuni di questi, come i dati eventi generati da computer, i registri e le informazioni sulle sessioni utente sono utili per un periodo di tempo limitato.</span><span class="sxs-lookup"><span data-stu-id="dab51-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="dab51-107">Una volta dati hello diventano toohello surplus esigenze dell'applicazione hello è sicuro toopurge questi dati e ridurre esigenze di archiviazione hello di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="dab51-107">Once hello data becomes surplus toohello needs of hello application it is safe toopurge this data and reduce hello storage needs of an application.</span></span>

<span data-ttu-id="dab51-108">Con "toolive" o di durata (TTL) Cosmos DB di Microsoft Azure fornisce documenti toohave possibilità di hello eliminati dal database hello automaticamente dopo un periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="dab51-108">With "time toolive" or TTL, Microsoft Azure Cosmos DB provides hello ability toohave documents automatically purged from hello database after a period of time.</span></span> <span data-ttu-id="dab51-109">tempo predefinito Hello toolive può essere impostato a livello di raccolta hello e sottoposto a override in una base per ogni documento.</span><span class="sxs-lookup"><span data-stu-id="dab51-109">hello default time toolive can be set at hello collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="dab51-110">Quando il valore di TTL è impostato, come impostazione predefinita di una raccolta o a livello di documento, Cosmos DB rimuove automaticamente i documenti esistenti dopo un numero di secondi dall'ultima modifica pari a tale valore.</span><span class="sxs-lookup"><span data-stu-id="dab51-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="dab51-111">Tempo toolive in DB Cosmos utilizza un offset rispetto quando il documento hello dell'ultima modifica.</span><span class="sxs-lookup"><span data-stu-id="dab51-111">Time toolive in Cosmos DB uses an offset against when hello document was last modified.</span></span> <span data-ttu-id="dab51-112">toodo questo it Usa hello `_ts` campo disponibile per ogni documento.</span><span class="sxs-lookup"><span data-stu-id="dab51-112">toodo this it uses hello `_ts` field which exists on every document.</span></span> <span data-ttu-id="dab51-113">campo TS Hello è di tipo unix epoch timestamp che rappresentano hello data e ora.</span><span class="sxs-lookup"><span data-stu-id="dab51-113">hello _ts field is a unix-style epoch timestamp representing hello date and time.</span></span> <span data-ttu-id="dab51-114">Hello `_ts` campo viene aggiornato ogni volta che un documento viene modificato.</span><span class="sxs-lookup"><span data-stu-id="dab51-114">hello `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="dab51-115">Comportamento di TTL</span><span class="sxs-lookup"><span data-stu-id="dab51-115">TTL behavior</span></span>
<span data-ttu-id="dab51-116">funzionalità di durata (TTL) Hello è controllata dalle proprietà di durata (TTL) a due livelli - livello di raccolta hello e livello di documento hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-116">hello TTL feature is controlled by TTL properties at two levels - hello collection level and hello document level.</span></span> <span data-ttu-id="dab51-117">i valori Hello in secondi e vengono considerati come un delta da hello `_ts` ultima modifica al documento hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-117">hello values are set in seconds and are treated as a delta from hello `_ts` that hello document was last modified at.</span></span>

1. <span data-ttu-id="dab51-118">DefaultTTL per raccolta hello</span><span class="sxs-lookup"><span data-stu-id="dab51-118">DefaultTTL for hello collection</span></span>
   
   * <span data-ttu-id="dab51-119">Se mancanti (o set toonull), i documenti non vengono eliminati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="dab51-119">If missing (or set toonull), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="dab51-120">Se è presente e il valore di hello è "-1" = infinito – documenti senza scadenza per impostazione predefinita</span><span class="sxs-lookup"><span data-stu-id="dab51-120">If present and hello value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="dab51-121">Se è presente e il valore di hello è un numero ("n"), documenti scadono "n" secondi dopo l'ultima modifica</span><span class="sxs-lookup"><span data-stu-id="dab51-121">If present and hello value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="dab51-122">Durata (TTL) per i documenti hello:</span><span class="sxs-lookup"><span data-stu-id="dab51-122">TTL for hello documents:</span></span> 
   
   * <span data-ttu-id="dab51-123">Proprietà è applicabile solo se è presente per la raccolta padre hello DefaultTTL.</span><span class="sxs-lookup"><span data-stu-id="dab51-123">Property is applicable only if DefaultTTL is present for hello parent collection.</span></span>
   * <span data-ttu-id="dab51-124">Sostituisce il valore DefaultTTL hello per la raccolta padre hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-124">Overrides hello DefaultTTL value for hello parent collection.</span></span>

<span data-ttu-id="dab51-125">Come documento hello è scaduto (`ttl`  +  `_ts` > = ora corrente del server), documento hello viene contrassegnato come "scaduto".</span><span class="sxs-lookup"><span data-stu-id="dab51-125">As soon as hello document has expired (`ttl` + `_ts` >= current server time), hello document is marked as "expired”.</span></span> <span data-ttu-id="dab51-126">Nessuna operazione sarà possibile in tali documenti dopo questo periodo di tempo e verranno esclusi dai risultati di hello di qualsiasi query eseguita.</span><span class="sxs-lookup"><span data-stu-id="dab51-126">No operation will be allowed on these documents after this time and they will be excluded from hello results of any queries performed.</span></span> <span data-ttu-id="dab51-127">documenti Hello vengono eliminati fisicamente nel sistema hello e vengono eliminati in background hello in base alle esigenze in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="dab51-127">hello documents are physically deleted in hello system, and are deleted in hello background opportunistically at a later time.</span></span> <span data-ttu-id="dab51-128">Questo non utilizzare qualsiasi [unità richiesta (RUs)](request-units.md) dal budget raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-128">This does not consume any [Request Units (RUs)](request-units.md) from hello collection budget.</span></span>

<span data-ttu-id="dab51-129">Hello sopra logica può essere visualizzata in hello seguente matrice:</span><span class="sxs-lookup"><span data-stu-id="dab51-129">hello above logic can be shown in hello following matrix:</span></span>

|  | <span data-ttu-id="dab51-130">DefaultTTL mancante o non è impostato su raccolta hello</span><span class="sxs-lookup"><span data-stu-id="dab51-130">DefaultTTL missing/not set on hello collection</span></span> | <span data-ttu-id="dab51-131">DefaultTTL = -1 nella raccolta</span><span class="sxs-lookup"><span data-stu-id="dab51-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="dab51-132">DefaultTTL = n nella raccolta</span><span class="sxs-lookup"><span data-stu-id="dab51-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="dab51-133">TTL mancante nel documento</span><span class="sxs-lookup"><span data-stu-id="dab51-133">TTL Missing on document</span></span> |<span data-ttu-id="dab51-134">Nothing toooverride a livello di documento, poiché sia il documento hello e raccolta non includono alcun concetto di durata (TTL).</span><span class="sxs-lookup"><span data-stu-id="dab51-134">Nothing toooverride at document level since both hello document and collection have no concept of TTL.</span></span> |<span data-ttu-id="dab51-135">I documenti in questa raccolta non scadono.</span><span class="sxs-lookup"><span data-stu-id="dab51-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="dab51-136">documenti Hello in questa raccolta scadrà quando n intervallo scade.</span><span class="sxs-lookup"><span data-stu-id="dab51-136">hello documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="dab51-137">Durata TTL = -1 nel documento</span><span class="sxs-lookup"><span data-stu-id="dab51-137">TTL = -1 on document</span></span> |<span data-ttu-id="dab51-138">Nothing toooverride a livello di documento hello poiché non definisce l'insieme di hello hello DefaultTTL proprietà che è possibile eseguire l'override di un documento.</span><span class="sxs-lookup"><span data-stu-id="dab51-138">Nothing toooverride at hello document level since hello collection doesn’t define hello DefaultTTL property that a document can override.</span></span> <span data-ttu-id="dab51-139">Durata (TTL) in un documento è non interpretato dal sistema hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-139">TTL on a document is un-interpreted by hello system.</span></span> |<span data-ttu-id="dab51-140">I documenti in questa raccolta non scadono.</span><span class="sxs-lookup"><span data-stu-id="dab51-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="dab51-141">documento Hello con durata (TTL) =-1 in questa raccolta non ha scadenza.</span><span class="sxs-lookup"><span data-stu-id="dab51-141">hello document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="dab51-142">Tutti gli altri documenti scadono dopo l'intervallo di tempo n.</span><span class="sxs-lookup"><span data-stu-id="dab51-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="dab51-143">TTL = n nel documento</span><span class="sxs-lookup"><span data-stu-id="dab51-143">TTL = n on document</span></span> |<span data-ttu-id="dab51-144">Nothing toooverride a livello di documento hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-144">Nothing toooverride at hello document level.</span></span> <span data-ttu-id="dab51-145">Durata (TTL) su un documento non interpretato dal sistema hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-145">TTL on a document in un-interpreted by hello system.</span></span> |<span data-ttu-id="dab51-146">documento Hello con durata (TTL) = n scadranno dopo un intervallo n, in secondi.</span><span class="sxs-lookup"><span data-stu-id="dab51-146">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="dab51-147">Gli altri documenti ereditano l'intervallo -1 e non scadono.</span><span class="sxs-lookup"><span data-stu-id="dab51-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="dab51-148">documento Hello con durata (TTL) = n scadranno dopo un intervallo n, in secondi.</span><span class="sxs-lookup"><span data-stu-id="dab51-148">hello document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="dab51-149">Altri documenti eredita "n" l'intervallo di raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-149">Other documents will inherit "n" interval from hello collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="dab51-150">Configurazione di TTL</span><span class="sxs-lookup"><span data-stu-id="dab51-150">Configuring TTL</span></span>
<span data-ttu-id="dab51-151">Per impostazione predefinita, l'ora toolive è disabilitata per impostazione predefinita in tutte le raccolte di DB Cosmos e su tutti i documenti.</span><span class="sxs-lookup"><span data-stu-id="dab51-151">By default, time toolive is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="dab51-152">Abilitazione di TTL</span><span class="sxs-lookup"><span data-stu-id="dab51-152">Enabling TTL</span></span>
<span data-ttu-id="dab51-153">tooenable durata (TTL) su una raccolta o documenti hello all'interno di una raccolta, è necessario tooset hello DefaultTTL proprietà tooeither una raccolta -1 o un numero positivo diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="dab51-153">tooenable TTL on a collection, or hello documents within a collection, you need tooset hello DefaultTTL property of a collection tooeither -1 or a non-zero positive number.</span></span> <span data-ttu-id="dab51-154">Impostazione hello DefaultTTL troppo-1 indica che per impostazione predefinita tutti i documenti nella raccolta hello risiederanno forever ma hello servizio DB Cosmos deve monitorare questa raccolta per i documenti che hanno eseguito l'override di questa impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="dab51-154">Setting hello DefaultTTL too-1 means that by default all documents in hello collection will live forever but hello Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="dab51-155">Configurazione del valore TTL predefinito in una raccolta</span><span class="sxs-lookup"><span data-stu-id="dab51-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="dab51-156">Si è in grado di tooconfigure toolive di tempo predefinito a un livello di raccolta.</span><span class="sxs-lookup"><span data-stu-id="dab51-156">You are able tooconfigure a default time toolive at a collection level.</span></span> <span data-ttu-id="dab51-157">hello tooset durata (TTL) su una raccolta, è necessario un numero positivo diverso da zero che indica il periodo di hello, in secondi, tooexpire tooprovide tutti i documenti nella raccolta hello dopo hello ultima modifica del timestamp del documento hello (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="dab51-157">tooset hello TTL on a collection, you need tooprovide a non-zero positive number that indicates hello period, in seconds, tooexpire all documents in hello collection after hello last modified timestamp of hello document (`_ts`).</span></span> <span data-ttu-id="dab51-158">In alternativa, è possibile impostare hello predefinito troppo-1, che implica che tutti i documenti inseriti nella raccolta toohello risiederanno all'infinito per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="dab51-158">Or, you can set hello default too-1, which implies that all documents inserted in toohello collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="dab51-159">Impostazione di TTL in un documento</span><span class="sxs-lookup"><span data-stu-id="dab51-159">Setting TTL on a document</span></span>
<span data-ttu-id="dab51-160">Inoltre toosetting TTL predefinito su una raccolta è possibile impostare TTL specifico a un livello di documento.</span><span class="sxs-lookup"><span data-stu-id="dab51-160">In addition toosetting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="dab51-161">In questo modo sostituirà predefinito hello raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-161">Doing this will override hello default of hello collection.</span></span>

* <span data-ttu-id="dab51-162">hello tooset durata (TTL) in un documento, è necessario un numero positivo diverso da zero indica hello periodo, espresso in secondi, il documento hello tooexpire dopo hello ultima modifica del timestamp del documento hello tooprovide (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="dab51-162">tooset hello TTL on a document, you need tooprovide a non-zero positive number which indicates hello period, in seconds, tooexpire hello document after hello last modified timestamp of hello document (`_ts`).</span></span>
* <span data-ttu-id="dab51-163">Se un documento dispone di alcun campo di durata (TTL), quindi hello predefinito della raccolta hello verrà applicate.</span><span class="sxs-lookup"><span data-stu-id="dab51-163">If a document has no TTL field, then hello default of hello collection will apply.</span></span>
* <span data-ttu-id="dab51-164">Se la durata (TTL) è disabilitata a livello di raccolta hello, campo TTL hello documento hello verrà ignorato fino durata (TTL) sia abilitata di nuovo nella raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-164">If TTL is disabled at hello collection level, hello TTL field on hello document will be ignored until TTL is enabled again on hello collection.</span></span>

<span data-ttu-id="dab51-165">Di seguito è riportato un frammento di codice che illustra come tooset hello scadenza di durata (TTL) in un documento:</span><span class="sxs-lookup"><span data-stu-id="dab51-165">Here's a snippet showing how tooset hello TTL expiration on a document:</span></span>

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


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="dab51-166">Estensione di TTL in un documento esistente</span><span class="sxs-lookup"><span data-stu-id="dab51-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="dab51-167">È possibile reimpostare hello durata (TTL) in un documento, eseguire qualsiasi operazione di scrittura sul documento hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-167">You can reset hello TTL on a document by doing any write operation on hello document.</span></span> <span data-ttu-id="dab51-168">In questo modo verrà impostato hello `_ts` toohello ora corrente e hello conto alla rovescia toohello documento scadenza, l'impostazione hello `ttl`, inizierà nuovamente.</span><span class="sxs-lookup"><span data-stu-id="dab51-168">Doing this will set hello `_ts` toohello current time, and hello countdown toohello document expiry, as set by hello `ttl`, will begin again.</span></span> <span data-ttu-id="dab51-169">Se si desidera hello toochange `ttl` di un documento, è possibile aggiornare il campo hello come avviene con qualsiasi altro campo impostabile.</span><span class="sxs-lookup"><span data-stu-id="dab51-169">If you wish toochange hello `ttl` of a document, you can update hello field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time toolive
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="dab51-170">Rimozione di TTL da un documento</span><span class="sxs-lookup"><span data-stu-id="dab51-170">Removing TTL from a document</span></span>
<span data-ttu-id="dab51-171">Se è stata impostata una durata (TTL) in un documento e non si desidera più che tooexpire documento, quindi recuperare il documento hello, rimuovere il campo di durata (TTL) hello e sostituire hello documento sul server hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-171">If a TTL has been set on a document and you no longer want that document tooexpire, then you can retrieve hello document, remove hello TTL field and replace hello document on hello server.</span></span> <span data-ttu-id="dab51-172">Quando il campo di durata (TTL) hello viene rimosso dal documento hello, verrà applicata predefinito hello raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-172">When hello TTL field is removed from hello document, hello default of hello collection will be applied.</span></span> <span data-ttu-id="dab51-173">toostop un documento da scade e non erediti dall'insieme di hello è necessario tooset hello TTL valore troppo-1.</span><span class="sxs-lookup"><span data-stu-id="dab51-173">toostop a document from expiring and not inherit from hello collection then you need tooset hello TTL value too-1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit hello default TTL of hello collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="dab51-174">Disabilitazione di TTL</span><span class="sxs-lookup"><span data-stu-id="dab51-174">Disabling TTL</span></span>
<span data-ttu-id="dab51-175">toodisable TTL interamente in una raccolta e l'arresto hello background elaborare la ricerca di documenti scaduti proprietà DefaultTTL hello raccolta hello devono essere eliminati.</span><span class="sxs-lookup"><span data-stu-id="dab51-175">toodisable TTL entirely on a collection and stop hello background process from looking for expired documents hello DefaultTTL property on hello collection should be deleted.</span></span> <span data-ttu-id="dab51-176">Eliminazione di questa proprietà è diversa dall'impostazione di troppo-1.</span><span class="sxs-lookup"><span data-stu-id="dab51-176">Deleting this property is different from setting it too-1.</span></span> <span data-ttu-id="dab51-177">Impostazione troppo-1 significa nuovi documenti aggiunti insieme toohello risiederanno forever ma è possibile ignorare questa in documenti specifici nella raccolta di hello.</span><span class="sxs-lookup"><span data-stu-id="dab51-177">Setting too-1 means new documents added toohello collection will live forever but you can override this on specific documents in hello collection.</span></span> <span data-ttu-id="dab51-178">Rimozione di questa proprietà dalla raccolta hello indica che i documenti non ha scadenza, anche se sono presenti documenti che hanno sottoposto a override esplicito predefinito precedente.</span><span class="sxs-lookup"><span data-stu-id="dab51-178">Removing this property entirely from hello collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="dab51-179">domande frequenti</span><span class="sxs-lookup"><span data-stu-id="dab51-179">FAQ</span></span>
<span data-ttu-id="dab51-180">**Quanto costa la durata (TTL)?**</span><span class="sxs-lookup"><span data-stu-id="dab51-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="dab51-181">Non vi è alcun toosetting costi aggiuntivi una durata (TTL) in un documento.</span><span class="sxs-lookup"><span data-stu-id="dab51-181">There is no additional cost toosetting a TTL on a document.</span></span>

<span data-ttu-id="dab51-182">**Quanto tempo sarà necessario toodelete documento una volta hello TTL backup?**</span><span class="sxs-lookup"><span data-stu-id="dab51-182">**How long will it take toodelete my document once hello TTL is up?**</span></span>

<span data-ttu-id="dab51-183">documenti Hello scaduti immediatamente dopo aver hello durata (TTL) sia attivo e non saranno accessibile tramite CRUD o API di query.</span><span class="sxs-lookup"><span data-stu-id="dab51-183">hello documents are expired immediately once hello TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="dab51-184">**La durata (TTL) impostata per un documento influisce sugli addebiti delle unità richiesta?**</span><span class="sxs-lookup"><span data-stu-id="dab51-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="dab51-185">No, gli addebiti delle unità richiesta non risentono delle eliminazioni di documenti scaduti con TTL in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="dab51-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="dab51-186">**Funzionalità di durata (TTL) hello si applicano solo documenti tooentire o posso scadere i valori delle proprietà di singoli documenti?**</span><span class="sxs-lookup"><span data-stu-id="dab51-186">**Does hello TTL feature only apply tooentire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="dab51-187">Durata (TTL) applica toohello intero documento.</span><span class="sxs-lookup"><span data-stu-id="dab51-187">TTL applies toohello entire document.</span></span> <span data-ttu-id="dab51-188">Se si desidera tooexpire solo una parte di un documento, la si consiglia di estrarre la parte hello hello il documento principale nel documento "collegate" separato tooa e quindi utilizzare durata (TTL) su tale documento estratta.</span><span class="sxs-lookup"><span data-stu-id="dab51-188">If you would like tooexpire just a portion of a document, then it is recommended that you extract hello portion from hello main document in tooa separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="dab51-189">**Funzionalità di durata (TTL) hello dispone di requisiti specifici di indicizzazione?**</span><span class="sxs-lookup"><span data-stu-id="dab51-189">**Does hello TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="dab51-190">Sì.</span><span class="sxs-lookup"><span data-stu-id="dab51-190">Yes.</span></span> <span data-ttu-id="dab51-191">raccolta di Hello deve contenere [set di criteri di indicizzazione](indexing-policies.md) tooeither Consistent o Lazy.</span><span class="sxs-lookup"><span data-stu-id="dab51-191">hello collection must have [indexing policy set](indexing-policies.md) tooeither Consistent or Lazy.</span></span> <span data-ttu-id="dab51-192">Il tentativo di tooset DefaultTTL su una raccolta con l'indicizzazione set tooNone genererà un errore, come durante il tentativo di tooturn disattivare l'indicizzazione in una raccolta che dispone di un DefaultTTL già impostato.</span><span class="sxs-lookup"><span data-stu-id="dab51-192">Trying tooset DefaultTTL on a collection with indexing set tooNone will result in an error, as will trying tooturn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="dab51-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="dab51-193">Next steps</span></span>
<span data-ttu-id="dab51-194">toolearn ulteriori informazioni su Azure Cosmos DB, fare riferimento a servizio toohello [ *documentazione* ](https://azure.microsoft.com/documentation/services/cosmos-db/) pagina.</span><span class="sxs-lookup"><span data-stu-id="dab51-194">toolearn more about Azure Cosmos DB, refer toohello service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

