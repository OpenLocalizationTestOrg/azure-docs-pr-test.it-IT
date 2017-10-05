---
title: Impostare come scaduti i dati in Cosmos DB usando la durata (TTL) | Microsoft Docs
description: "Con l'impostazione TTL, Microsoft Azure Cosmos DB offre la possibilità di eliminare automaticamente i documenti dal sistema dopo un periodo di tempo determinato."
services: cosmos-db
documentationcenter: 
keywords: Durata (TTL)
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
ms.openlocfilehash: 6f1c43ca0113dc7579b0fc3743d3314c16ce78a4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="expire-data-in-azure-cosmos-db-collections-automatically-with-time-to-live"></a><span data-ttu-id="fae7f-104">Impostare automaticamente come scaduti i dati nelle raccolte di Cosmos DB usando la durata (TTL)</span><span class="sxs-lookup"><span data-stu-id="fae7f-104">Expire data in Azure Cosmos DB collections automatically with time to live</span></span>
<span data-ttu-id="fae7f-105">Le applicazioni posso produrre e archiviare grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="fae7f-105">Applications can produce and store vast amounts of data.</span></span> <span data-ttu-id="fae7f-106">Alcuni di questi, come i dati eventi generati da computer, i registri e le informazioni sulle sessioni utente sono utili per un periodo di tempo limitato.</span><span class="sxs-lookup"><span data-stu-id="fae7f-106">Some of this data, like machine generated event data, logs, and user session information is only useful for a finite period of time.</span></span> <span data-ttu-id="fae7f-107">Quando i dati eccedono le esigenze dell'applicazione è possibile eliminarli e ridurre le risorse di archiviazione necessarie per l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="fae7f-107">Once the data becomes surplus to the needs of the application it is safe to purge this data and reduce the storage needs of an application.</span></span>

<span data-ttu-id="fae7f-108">Con l'impostazione della durata (TTL), Microsoft Azure Cosmos DB offre la possibilità di eliminare automaticamente i documenti dal database dopo un periodo di tempo determinato.</span><span class="sxs-lookup"><span data-stu-id="fae7f-108">With "time to live" or TTL, Microsoft Azure Cosmos DB provides the ability to have documents automatically purged from the database after a period of time.</span></span> <span data-ttu-id="fae7f-109">La durata predefinita può essere impostata a livello di raccolta ed è possibile eseguirne l'override in base ai singoli documenti.</span><span class="sxs-lookup"><span data-stu-id="fae7f-109">The default time to live can be set at the collection level, and overridden on a per-document basis.</span></span> <span data-ttu-id="fae7f-110">Quando il valore di TTL è impostato, come impostazione predefinita di una raccolta o a livello di documento, Cosmos DB rimuove automaticamente i documenti esistenti dopo un numero di secondi dall'ultima modifica pari a tale valore.</span><span class="sxs-lookup"><span data-stu-id="fae7f-110">Once TTL is set, either as a collection default or at a document level, Cosmos DB will automatically remove documents that exist after that period of time, in seconds, since they were last modified.</span></span>

<span data-ttu-id="fae7f-111">In Cosmos DB la durata usa la differenza dall'ora dell'ultima modifica al documento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-111">Time to live in Cosmos DB uses an offset against when the document was last modified.</span></span> <span data-ttu-id="fae7f-112">A tale scopo usa il campo `_ts` che esiste in ogni documento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-112">To do this it uses the `_ts` field which exists on every document.</span></span> <span data-ttu-id="fae7f-113">Il campo _ts è un timestamp Epoch di tipo Unix che rappresenta la data e l'ora</span><span class="sxs-lookup"><span data-stu-id="fae7f-113">The _ts field is a unix-style epoch timestamp representing the date and time.</span></span> <span data-ttu-id="fae7f-114">e il campo `_ts` viene aggiornato ogni volta che si modifica un documento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-114">The `_ts` field is updated every time a document is modified.</span></span> 

## <a name="ttl-behavior"></a><span data-ttu-id="fae7f-115">Comportamento di TTL</span><span class="sxs-lookup"><span data-stu-id="fae7f-115">TTL behavior</span></span>
<span data-ttu-id="fae7f-116">La funzionalità TTL è controllata dalle proprietà TTL a livello di raccolta e a livello di documento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-116">The TTL feature is controlled by TTL properties at two levels - the collection level and the document level.</span></span> <span data-ttu-id="fae7f-117">I valori sono espressi in secondi e vengono trattati come differenziale dal `_ts` dell'ultima modifica al documento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-117">The values are set in seconds and are treated as a delta from the `_ts` that the document was last modified at.</span></span>

1. <span data-ttu-id="fae7f-118">DefaultTTL per la raccolta:</span><span class="sxs-lookup"><span data-stu-id="fae7f-118">DefaultTTL for the collection</span></span>
   
   * <span data-ttu-id="fae7f-119">Se non è presente o è impostata su Null, i documenti non vengono eliminati automaticamente.</span><span class="sxs-lookup"><span data-stu-id="fae7f-119">If missing (or set to null), documents are not deleted automatically.</span></span>
   * <span data-ttu-id="fae7f-120">Se è presente e il valore è "-1" = infinito, i documenti non scadono per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fae7f-120">If present and the value is "-1" = infinite – documents don’t expire by default</span></span>
   * <span data-ttu-id="fae7f-121">Se è presente e il valore è un numero "n", i documenti scadono "n" secondi dopo l'ultima modifica.</span><span class="sxs-lookup"><span data-stu-id="fae7f-121">If present and the value is some number ("n") – documents expire "n” seconds after last modification</span></span>
2. <span data-ttu-id="fae7f-122">TTL per i documenti:</span><span class="sxs-lookup"><span data-stu-id="fae7f-122">TTL for the documents:</span></span> 
   
   * <span data-ttu-id="fae7f-123">La proprietà è applicabile solo se DefaultTTL è presente per la raccolta padre.</span><span class="sxs-lookup"><span data-stu-id="fae7f-123">Property is applicable only if DefaultTTL is present for the parent collection.</span></span>
   * <span data-ttu-id="fae7f-124">Esegue l'override del valore di DefaultTTL per la raccolta padre.</span><span class="sxs-lookup"><span data-stu-id="fae7f-124">Overrides the DefaultTTL value for the parent collection.</span></span>

<span data-ttu-id="fae7f-125">Nel momento in cui è scade (`ttl` + `_ts` >= ora corrente del server), il documento viene contrassegnato come "scaduto".</span><span class="sxs-lookup"><span data-stu-id="fae7f-125">As soon as the document has expired (`ttl` + `_ts` >= current server time), the document is marked as "expired”.</span></span> <span data-ttu-id="fae7f-126">Da questo momento sui documenti scaduti non è possibile eseguire alcuna operazione e vengono esclusi dai risultati delle query.</span><span class="sxs-lookup"><span data-stu-id="fae7f-126">No operation will be allowed on these documents after this time and they will be excluded from the results of any queries performed.</span></span> <span data-ttu-id="fae7f-127">I documenti vengono eliminati fisicamente dal sistema e vengono eliminati in background in base alle esigenze in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-127">The documents are physically deleted in the system, and are deleted in the background opportunistically at a later time.</span></span> <span data-ttu-id="fae7f-128">L'operazione non utilizza le [unità richiesta (UR)](request-units.md) del budget della raccolta.</span><span class="sxs-lookup"><span data-stu-id="fae7f-128">This does not consume any [Request Units (RUs)](request-units.md) from the collection budget.</span></span>

<span data-ttu-id="fae7f-129">La logica precedente può essere illustrata in questa matrice:</span><span class="sxs-lookup"><span data-stu-id="fae7f-129">The above logic can be shown in the following matrix:</span></span>

|  | <span data-ttu-id="fae7f-130">DefaultTTL mancante o non impostata nella raccolta</span><span class="sxs-lookup"><span data-stu-id="fae7f-130">DefaultTTL missing/not set on the collection</span></span> | <span data-ttu-id="fae7f-131">DefaultTTL = -1 nella raccolta</span><span class="sxs-lookup"><span data-stu-id="fae7f-131">DefaultTTL = -1 on collection</span></span> | <span data-ttu-id="fae7f-132">DefaultTTL = n nella raccolta</span><span class="sxs-lookup"><span data-stu-id="fae7f-132">DefaultTTL = "n" on collection</span></span> |
| --- |:--- |:--- |:--- |
| <span data-ttu-id="fae7f-133">TTL mancante nel documento</span><span class="sxs-lookup"><span data-stu-id="fae7f-133">TTL Missing on document</span></span> |<span data-ttu-id="fae7f-134">Non viene eseguito l'override a livello di documento, perché sia il documento che la raccolta sono privi di TTL.</span><span class="sxs-lookup"><span data-stu-id="fae7f-134">Nothing to override at document level since both the document and collection have no concept of TTL.</span></span> |<span data-ttu-id="fae7f-135">I documenti in questa raccolta non scadono.</span><span class="sxs-lookup"><span data-stu-id="fae7f-135">No documents in this collection will expire.</span></span> |<span data-ttu-id="fae7f-136">I documenti nella raccolta scadono al termine dell'intervallo n.</span><span class="sxs-lookup"><span data-stu-id="fae7f-136">The documents in this collection will expire when interval n elapses.</span></span> |
| <span data-ttu-id="fae7f-137">Durata TTL = -1 nel documento</span><span class="sxs-lookup"><span data-stu-id="fae7f-137">TTL = -1 on document</span></span> |<span data-ttu-id="fae7f-138">Non viene eseguito l'override a livello di documento, perché la raccolta non definisce la proprietà DefaultTTL di cui è possibile eseguire l'override a livello di documento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-138">Nothing to override at the document level since the collection doesn’t define the DefaultTTL property that a document can override.</span></span> <span data-ttu-id="fae7f-139">L'impostazione TTL a livello di documento non viene interpretata dal sistema.</span><span class="sxs-lookup"><span data-stu-id="fae7f-139">TTL on a document is un-interpreted by the system.</span></span> |<span data-ttu-id="fae7f-140">I documenti in questa raccolta non scadono.</span><span class="sxs-lookup"><span data-stu-id="fae7f-140">No documents in this collection will expire.</span></span> |<span data-ttu-id="fae7f-141">Il documento con TTL =-1 in questa raccolta non scade.</span><span class="sxs-lookup"><span data-stu-id="fae7f-141">The document with TTL=-1 in this collection will never expire.</span></span> <span data-ttu-id="fae7f-142">Tutti gli altri documenti scadono dopo l'intervallo di tempo n.</span><span class="sxs-lookup"><span data-stu-id="fae7f-142">All other documents will expire after "n" interval.</span></span> |
| <span data-ttu-id="fae7f-143">TTL = n nel documento</span><span class="sxs-lookup"><span data-stu-id="fae7f-143">TTL = n on document</span></span> |<span data-ttu-id="fae7f-144">Non viene eseguito l'override a livello di documento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-144">Nothing to override at the document level.</span></span> <span data-ttu-id="fae7f-145">L'impostazione TTL a livello di documento non viene interpretata dal sistema.</span><span class="sxs-lookup"><span data-stu-id="fae7f-145">TTL on a document in un-interpreted by the system.</span></span> |<span data-ttu-id="fae7f-146">Il documento con TTL = n scade dopo l'intervallo di tempo n, espresso in secondi.</span><span class="sxs-lookup"><span data-stu-id="fae7f-146">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="fae7f-147">Gli altri documenti ereditano l'intervallo -1 e non scadono.</span><span class="sxs-lookup"><span data-stu-id="fae7f-147">Other documents will inherit interval of -1 and never expire.</span></span> |<span data-ttu-id="fae7f-148">Il documento con TTL = n scade dopo l'intervallo di tempo n, espresso in secondi.</span><span class="sxs-lookup"><span data-stu-id="fae7f-148">The document with TTL = n will expire after interval n, in seconds.</span></span> <span data-ttu-id="fae7f-149">Gli altri documenti ereditano l'intervallo n dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="fae7f-149">Other documents will inherit "n" interval from the collection.</span></span> |

## <a name="configuring-ttl"></a><span data-ttu-id="fae7f-150">Configurazione di TTL</span><span class="sxs-lookup"><span data-stu-id="fae7f-150">Configuring TTL</span></span>
<span data-ttu-id="fae7f-151">Per impostazione predefinita, la durata è disabilitata in tutte le raccolte di Cosmos DB e in tutti i documenti.</span><span class="sxs-lookup"><span data-stu-id="fae7f-151">By default, time to live is disabled by default in all Cosmos DB collections and on all documents.</span></span>

## <a name="enabling-ttl"></a><span data-ttu-id="fae7f-152">Abilitazione di TTL</span><span class="sxs-lookup"><span data-stu-id="fae7f-152">Enabling TTL</span></span>
<span data-ttu-id="fae7f-153">Per abilitare la durata (TTL) in una raccolta o nei documenti all'interno di una raccolta, è necessario impostare la proprietà DefaultTTL della raccolta su -1 o su un numero positivo diverso da zero.</span><span class="sxs-lookup"><span data-stu-id="fae7f-153">To enable TTL on a collection, or the documents within a collection, you need to set the DefaultTTL property of a collection to either -1 or a non-zero positive number.</span></span> <span data-ttu-id="fae7f-154">Quando DefaultTTL = -1, per impostazione predefinita tutti i documenti nella raccolta hanno durata infinita. Il servizio Cosmos DB deve tuttavia monitorare i documenti per cui viene eseguito l'override di questa impostazione predefinita nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="fae7f-154">Setting the DefaultTTL to -1 means that by default all documents in the collection will live forever but the Cosmos DB service should monitor this collection for documents that have overridden this default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive =-1; //never expire by default

    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        UriFactory.CreateDatabaseUri(databaseName),
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });

## <a name="configuring-default-ttl-on-a-collection"></a><span data-ttu-id="fae7f-155">Configurazione del valore TTL predefinito in una raccolta</span><span class="sxs-lookup"><span data-stu-id="fae7f-155">Configuring default TTL on a collection</span></span>
<span data-ttu-id="fae7f-156">È possibile configurare una durata predefinita a livello di raccolta.</span><span class="sxs-lookup"><span data-stu-id="fae7f-156">You are able to configure a default time to live at a collection level.</span></span> <span data-ttu-id="fae7f-157">Per impostare la durata (TTL) in una raccolta, è necessario specificare un numero positivo diverso da zero che indica il periodo di tempo, espresso in secondi, per la scadenza di tutti i documenti nella raccolta dopo l'ultimo timestamp di modifica del documento (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="fae7f-157">To set the TTL on a collection, you need to provide a non-zero positive number that indicates the period, in seconds, to expire all documents in the collection after the last modified timestamp of the document (`_ts`).</span></span> <span data-ttu-id="fae7f-158">In alternativa, è possibile impostare il valore predefinito su -1, per fare in modo che tutti i documenti inseriti nella raccolta abbiano una durata illimitata per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="fae7f-158">Or, you can set the default to -1, which implies that all documents inserted in to the collection will live indefinitely by default.</span></span>

    DocumentCollection collectionDefinition = new DocumentCollection();
    collectionDefinition.Id = "orders";
    collectionDefinition.PartitionKey.Paths.Add("/customerId");
    collectionDefinition.DefaultTimeToLive = 90 * 60 * 60 * 24; // expire all documents after 90 days
    
    DocumentCollection ttlEnabledCollection = await client.CreateDocumentCollectionAsync(
        "/dbs/salesdb",
        collectionDefinition,
        new RequestOptions { OfferThroughput = 20000 });


## <a name="setting-ttl-on-a-document"></a><span data-ttu-id="fae7f-159">Impostazione di TTL in un documento</span><span class="sxs-lookup"><span data-stu-id="fae7f-159">Setting TTL on a document</span></span>
<span data-ttu-id="fae7f-160">Oltre al valore TTL predefinito in una raccolta è possibile impostare una durata (TTL) specifica a livello di documento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-160">In addition to setting a default TTL on a collection you can set specific TTL at a document level.</span></span> <span data-ttu-id="fae7f-161">Questa impostazione esegue l'override dell'impostazione predefinita della raccolta.</span><span class="sxs-lookup"><span data-stu-id="fae7f-161">Doing this will override the default of the collection.</span></span>

* <span data-ttu-id="fae7f-162">Per impostare la durata (TTL) in un documento, è necessario specificare un numero positivo diverso da zero che indica il periodo di tempo, espresso in secondi, per la scadenza del documento dopo l'ultimo timestamp di modifica del documento (`_ts`).</span><span class="sxs-lookup"><span data-stu-id="fae7f-162">To set the TTL on a document, you need to provide a non-zero positive number which indicates the period, in seconds, to expire the document after the last modified timestamp of the document (`_ts`).</span></span>
* <span data-ttu-id="fae7f-163">Se il documento non ha il campo TTL, viene applicata l'impostazione predefinita della raccolta.</span><span class="sxs-lookup"><span data-stu-id="fae7f-163">If a document has no TTL field, then the default of the collection will apply.</span></span>
* <span data-ttu-id="fae7f-164">Se la funzionalità TTL è disabilitata a livello di raccolta, il campo TTL del documento viene ignorato finché non viene abilitata nuovamente la funzionalità TTL per la raccolta.</span><span class="sxs-lookup"><span data-stu-id="fae7f-164">If TTL is disabled at the collection level, the TTL field on the document will be ignored until TTL is enabled again on the collection.</span></span>

<span data-ttu-id="fae7f-165">Di seguito è riportato un frammento di codice che illustra come impostare la scadenza della durata (TTL) su un documento:</span><span class="sxs-lookup"><span data-stu-id="fae7f-165">Here's a snippet showing how to set the TTL expiration on a document:</span></span>

    // Include a property that serializes to "ttl" in JSON
    public class SalesOrder
    {
        [JsonProperty(PropertyName = "id")]
        public string Id { get; set; }
        
        [JsonProperty(PropertyName="cid")]
        public string CustomerId { get; set; }
        
        // used to set expiration policy
        [JsonProperty(PropertyName = "ttl", NullValueHandling = NullValueHandling.Ignore)]
        public int? TimeToLive { get; set; }
        
        //...
    }
    
    // Set the value to the expiration in seconds
    SalesOrder salesOrder = new SalesOrder
    {
        Id = "SO05",
        CustomerId = "CO18009186470",
        TimeToLive = 60 * 60 * 24 * 30;  // Expire sales orders in 30 days 
    };


## <a name="extending-ttl-on-an-existing-document"></a><span data-ttu-id="fae7f-166">Estensione di TTL in un documento esistente</span><span class="sxs-lookup"><span data-stu-id="fae7f-166">Extending TTL on an existing document</span></span>
<span data-ttu-id="fae7f-167">Per reimpostare il valore TTL in un documento è possibile eseguire una qualsiasi operazione di scrittura nel documento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-167">You can reset the TTL on a document by doing any write operation on the document.</span></span> <span data-ttu-id="fae7f-168">L'operazione imposta `_ts` sull'ora corrente e fa ripartire il conto alla rovescia per la scadenza del documento, data dal valore di `ttl`.</span><span class="sxs-lookup"><span data-stu-id="fae7f-168">Doing this will set the `_ts` to the current time, and the countdown to the document expiry, as set by the `ttl`, will begin again.</span></span> <span data-ttu-id="fae7f-169">Per modificare il valore `ttl` di un documento, è possibile aggiornare il campo come si fa con qualsiasi altro campo impostabile.</span><span class="sxs-lookup"><span data-stu-id="fae7f-169">If you wish to change the `ttl` of a document, you can update the field as you can do with any other settable field.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = 60 * 30 * 30; // update time to live
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="removing-ttl-from-a-document"></a><span data-ttu-id="fae7f-170">Rimozione di TTL da un documento</span><span class="sxs-lookup"><span data-stu-id="fae7f-170">Removing TTL from a document</span></span>
<span data-ttu-id="fae7f-171">Se è stato impostato un valore TTL per un documento ma si preferisce non farlo scadere, è possibile recuperare il documento, rimuovere il campo TTL e sostituire il documento nel server.</span><span class="sxs-lookup"><span data-stu-id="fae7f-171">If a TTL has been set on a document and you no longer want that document to expire, then you can retrieve the document, remove the TTL field and replace the document on the server.</span></span> <span data-ttu-id="fae7f-172">Quando il campo TTL viene rimosso dal documento, viene applicata l'impostazione predefinita della raccolta.</span><span class="sxs-lookup"><span data-stu-id="fae7f-172">When the TTL field is removed from the document, the default of the collection will be applied.</span></span> <span data-ttu-id="fae7f-173">Per impedire la scadenza di un documento e fare in modo che non erediti dalla raccolta, è necessario impostare il valore TTL su -1.</span><span class="sxs-lookup"><span data-stu-id="fae7f-173">To stop a document from expiring and not inherit from the collection then you need to set the TTL value to -1.</span></span>

    response = await client.ReadDocumentAsync(
        "/dbs/salesdb/colls/orders/docs/SO05"), 
        new RequestOptions { PartitionKey = new PartitionKey("CO18009186470") });
    
    Document readDocument = response.Resource;
    readDocument.TimeToLive = null; // inherit the default TTL of the collection
    
    response = await client.ReplaceDocumentAsync(salesOrder);

## <a name="disabling-ttl"></a><span data-ttu-id="fae7f-174">Disabilitazione di TTL</span><span class="sxs-lookup"><span data-stu-id="fae7f-174">Disabling TTL</span></span>
<span data-ttu-id="fae7f-175">Per disabilitare del tutto la durata (TTL) in una raccolta e impedire al processo in background di cercare documenti scaduti, è necessario eliminare la proprietà DefaultTTL dalla raccolta.</span><span class="sxs-lookup"><span data-stu-id="fae7f-175">To disable TTL entirely on a collection and stop the background process from looking for expired documents the DefaultTTL property on the collection should be deleted.</span></span> <span data-ttu-id="fae7f-176">Eliminare questa proprietà non equivale a impostarla su -1.</span><span class="sxs-lookup"><span data-stu-id="fae7f-176">Deleting this property is different from setting it to -1.</span></span> <span data-ttu-id="fae7f-177">Se la proprietà è impostata su -1, i nuovi documenti aggiunti alla raccolta non hanno scadenza ma è possibile eseguire l'override dell'impostazione per documenti specifici nella raccolta.</span><span class="sxs-lookup"><span data-stu-id="fae7f-177">Setting to -1 means new documents added to the collection will live forever but you can override this on specific documents in the collection.</span></span> <span data-ttu-id="fae7f-178">Se la proprietà viene rimossa dalla raccolta, nessuno dei documenti ha una scadenza, anche se sono presenti documenti con override esplicito di una impostazione predefinita precedente.</span><span class="sxs-lookup"><span data-stu-id="fae7f-178">Removing this property entirely from the collection means that no documents will expire, even if there are documents that have explicitly overridden a previous default.</span></span>

    DocumentCollection collection = await client.ReadDocumentCollectionAsync("/dbs/salesdb/colls/orders");
    
    // Disable TTL
    collection.DefaultTimeToLive = null;
    
    await client.ReplaceDocumentCollectionAsync(collection);


## <a name="faq"></a><span data-ttu-id="fae7f-179">Domande frequenti</span><span class="sxs-lookup"><span data-stu-id="fae7f-179">FAQ</span></span>
<span data-ttu-id="fae7f-180">**Quanto costa la durata (TTL)?**</span><span class="sxs-lookup"><span data-stu-id="fae7f-180">**What will TTL cost me?**</span></span>

<span data-ttu-id="fae7f-181">Non sono previsti costi aggiuntivi per l'impostazione di una durata (TTL) in un documento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-181">There is no additional cost to setting a TTL on a document.</span></span>

<span data-ttu-id="fae7f-182">**Quanto tempo è necessario per eliminare il documento dopo la scadenza?**</span><span class="sxs-lookup"><span data-stu-id="fae7f-182">**How long will it take to delete my document once the TTL is up?**</span></span>

<span data-ttu-id="fae7f-183">I documenti scadono immediatamente dopo la scadenza e non sarà possibile accedervi usando operazioni CRUD o API di query.</span><span class="sxs-lookup"><span data-stu-id="fae7f-183">The documents are expired immediately once the TTL is up, and will not be accessible via CRUD or query APIs.</span></span> 

<span data-ttu-id="fae7f-184">**La durata (TTL) impostata per un documento influisce sugli addebiti delle unità richiesta?**</span><span class="sxs-lookup"><span data-stu-id="fae7f-184">**Will TTL on a document have any impact on RU charges?**</span></span>

<span data-ttu-id="fae7f-185">No, gli addebiti delle unità richiesta non risentono delle eliminazioni di documenti scaduti con TTL in Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="fae7f-185">No, there will be no impact on RU charges for deletions of expired documents via TTL in Cosmos DB.</span></span>

<span data-ttu-id="fae7f-186">**La funzionalità TTL si applica solo all'intero documento o è possibile impostare come scaduti singoli valori delle proprietà di un documento?**</span><span class="sxs-lookup"><span data-stu-id="fae7f-186">**Does the TTL feature only apply to entire documents, or can I expire individual document property values?**</span></span>

<span data-ttu-id="fae7f-187">La funzionalità TTL si applica all'intero documento.</span><span class="sxs-lookup"><span data-stu-id="fae7f-187">TTL applies to the entire document.</span></span> <span data-ttu-id="fae7f-188">Per impostare come scaduta solo una parte di un documento, è consigliabile estrarla dal documento principale, inserirla in un documento "collegato" separato e usare la funzionalità TTL sul documento estratto.</span><span class="sxs-lookup"><span data-stu-id="fae7f-188">If you would like to expire just a portion of a document, then it is recommended that you extract the portion from the main document in to a separate "linked” document and then use TTL on that extracted document.</span></span>

<span data-ttu-id="fae7f-189">**La funzionalità TTL ha requisiti di indicizzazione specifici?**</span><span class="sxs-lookup"><span data-stu-id="fae7f-189">**Does the TTL feature have any specific indexing requirements?**</span></span>

<span data-ttu-id="fae7f-190">Sì.</span><span class="sxs-lookup"><span data-stu-id="fae7f-190">Yes.</span></span> <span data-ttu-id="fae7f-191">I [criteri di indicizzazione](indexing-policies.md) della raccolta devono essere impostati su Coerente o Differita.</span><span class="sxs-lookup"><span data-stu-id="fae7f-191">The collection must have [indexing policy set](indexing-policies.md) to either Consistent or Lazy.</span></span> <span data-ttu-id="fae7f-192">Il tentativo di impostare DefaultTTL in una raccolta la cui indicizzazione è impostata su None genera un errore, come anche il tentativo di disabilitare l'indicizzazione in una raccolta in cui la proprietà DefaultTTL è già impostata.</span><span class="sxs-lookup"><span data-stu-id="fae7f-192">Trying to set DefaultTTL on a collection with indexing set to None will result in an error, as will trying to turn off indexing on a collection that has a DefaultTTL already set.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fae7f-193">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fae7f-193">Next steps</span></span>
<span data-ttu-id="fae7f-194">Per altre informazioni su Azure Cosmos DB, vedere la pagina della [*documentazione*](https://azure.microsoft.com/documentation/services/cosmos-db/) del servizio.</span><span class="sxs-lookup"><span data-stu-id="fae7f-194">To learn more about Azure Cosmos DB, refer to the service [*documentation*](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span>

