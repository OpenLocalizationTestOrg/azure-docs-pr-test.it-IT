---
title: Modellazione dei dati di un documento per un database NoSQL | Microsoft Docs
description: Informazioni sulla modellazione dei dati per i database NoSQL
keywords: modellazione di dati
services: cosmos-db
author: arramac
manager: jhubbard
editor: mimig1
documentationcenter: 
ms.assetid: 69521eb9-590b-403c-9b36-98253a4c88b5
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/29/2016
ms.author: arramac
ms.openlocfilehash: 16c387fe574243544cf54cf283c7713ddcaa1942
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="e2538-104">Modellazione dei dati di un documento per un database NoSQL</span><span class="sxs-lookup"><span data-stu-id="e2538-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="e2538-105">Anche se con i database privi di schema, come Azure Cosmos DB, è facilissimo accettare le modifiche apportate al modello di dati, è consigliabile valutare bene tutto ciò che riguarda i dati.</span><span class="sxs-lookup"><span data-stu-id="e2538-105">While schema-free databases, like Azure Cosmos DB, make it super easy to embrace changes to your data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="e2538-106">Come verranno archiviati i dati?</span><span class="sxs-lookup"><span data-stu-id="e2538-106">How is data going to be stored?</span></span> <span data-ttu-id="e2538-107">In che modo l'applicazione recupererà i dati e ne eseguirà la query?</span><span class="sxs-lookup"><span data-stu-id="e2538-107">How is your application going to retrieve and query data?</span></span> <span data-ttu-id="e2538-108">L'applicazione esegue un'intensa attività di lettura o un'intensa attività di scrittura?</span><span class="sxs-lookup"><span data-stu-id="e2538-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="e2538-109">Dopo la lettura di questo articolo, si potrà rispondere alle domande seguenti:</span><span class="sxs-lookup"><span data-stu-id="e2538-109">After reading this article, you will be able to answer the following questions:</span></span>

* <span data-ttu-id="e2538-110">Come si deve considerare un documento in un database di documenti?</span><span class="sxs-lookup"><span data-stu-id="e2538-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="e2538-111">Cos'è la modellazione dei dati e perché è importante?</span><span class="sxs-lookup"><span data-stu-id="e2538-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="e2538-112">Come si distingue la modellazione dei dati in un database di documenti da quella in un database relazionale?</span><span class="sxs-lookup"><span data-stu-id="e2538-112">How is modeling data in a document database different to a relational database?</span></span>
* <span data-ttu-id="e2538-113">Come si esprimono le relazioni tra i dati in un database non relazionale?</span><span class="sxs-lookup"><span data-stu-id="e2538-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="e2538-114">Quando si incorporano i dati e quando si creano i collegamenti ai dati?</span><span class="sxs-lookup"><span data-stu-id="e2538-114">When do I embed data and when do I link to data?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="e2538-115">Incorporamento dei dati</span><span class="sxs-lookup"><span data-stu-id="e2538-115">Embedding data</span></span>
<span data-ttu-id="e2538-116">Quando si inizia a modellare i dati in un archivio documenti, ad esempio Cosmos DB, cercare di considerare le entità come **documenti autosufficienti** rappresentati in JSON.</span><span class="sxs-lookup"><span data-stu-id="e2538-116">When you start modeling data in a document store, such as Azure Cosmos DB, try to treat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="e2538-117">Prima di proseguire, è meglio fare un passo indietro e pensare a come sia possibile modellare qualcosa in un database relazionale, un argomento con cui molti hanno già familiarità.</span><span class="sxs-lookup"><span data-stu-id="e2538-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="e2538-118">L'esempio seguente mostra come una persona possa essere archiviata in un database relazionale.</span><span class="sxs-lookup"><span data-stu-id="e2538-118">The following example shows how a person might be stored in a relational database.</span></span> 

![Database relazionale](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="e2538-120">Quando si lavora con i database relazionali, tutti hanno imparato ormai da anni a normalizzare, normalizzare, normalizzare.</span><span class="sxs-lookup"><span data-stu-id="e2538-120">When working with relational databases, we've been taught for years to normalize, normalize, normalize.</span></span>

<span data-ttu-id="e2538-121">Di solito nella normalizzazione dei dati si prende un'entità, ad esempio una persona, e la si suddivide in porzioni di dati distinte.</span><span class="sxs-lookup"><span data-stu-id="e2538-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in to discrete pieces of data.</span></span> <span data-ttu-id="e2538-122">Nell'esempio precedente, una persona può avere più record di dettagli contatto e più record di indirizzi.</span><span class="sxs-lookup"><span data-stu-id="e2538-122">In the example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="e2538-123">È possibile andare oltre e suddividere i dettagli contatto estraendo anche i campi comuni come tipo.</span><span class="sxs-lookup"><span data-stu-id="e2538-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="e2538-124">Lo stesso per l'indirizzo: ogni record qui ha un tipo, ad esempio *Abitazione* o *Ufficio*</span><span class="sxs-lookup"><span data-stu-id="e2538-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="e2538-125">Il presupposto principale quando si normalizzano i dati è **evitare di archiviare i dati ridondanti** in ogni record e fare invece riferimento ai dati.</span><span class="sxs-lookup"><span data-stu-id="e2538-125">The guiding premise when normalizing data is to **avoid storing redundant data** on each record and rather refer to data.</span></span> <span data-ttu-id="e2538-126">In questo esempio, per leggere una persona, con tutti i dettagli contatto e gli indirizzi, è necessario usare i JOIN per aggregare in modo efficace i dati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e2538-126">In this example, to read a person, with all their contact details and addresses, you need to use JOINS to effectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="e2538-127">Per aggiornare una singola persona con i dettagli contatto e gli indirizzi, è necessario eseguire operazioni di scrittura in più tabelle.</span><span class="sxs-lookup"><span data-stu-id="e2538-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="e2538-128">Ora si esaminerà come si modellano gli stessi dati come entità autosufficiente in un database di documenti.</span><span class="sxs-lookup"><span data-stu-id="e2538-128">Now let's take a look at how we would model the same data as a self-contained entity in a document database.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "addresses": [
            {            
                "line1": "100 Some Street",
                "line2": "Unit 1",
                "city": "Seattle",
                "state": "WA",
                "zip": 98012
            }
        ],
        "contactDetails": [
            {"email: "thomas@andersen.com"},
            {"phone": "+1 555 555-5555", "extension": 5555}
        ] 
    }

<span data-ttu-id="e2538-129">Con questo approccio ora è stato **denormalizzato** il record della persona, in cui sono state **incorporate** tutte le informazioni relative a questa persona, ad esempio i dettagli di contatto e gli indirizzi, in un singolo documento JSON.</span><span class="sxs-lookup"><span data-stu-id="e2538-129">Using the approach above we have now **denormalized** the person record where we **embedded** all the information relating to this person, such as their contact details and addresses, in to a single JSON document.</span></span>
<span data-ttu-id="e2538-130">Inoltre, dal momento che non esistono limiti imposti da uno schema fisso, abbiamo la flessibilità necessaria, ad esempio, per avere dettagli contatto di forme completamente diverse.</span><span class="sxs-lookup"><span data-stu-id="e2538-130">In addition, because we're not confined to a fixed schema we have the flexibility to do things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="e2538-131">Il recupero del record completo di una persona dal database richiede ora una sola operazione di lettura in una sola raccolta e per un solo documento.</span><span class="sxs-lookup"><span data-stu-id="e2538-131">Retrieving a complete person record from the database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="e2538-132">Anche l'aggiornamento del record di una persona, con i dettagli contatto e gli indirizzi, richiede una sola operazione di scrittura in un solo documento.</span><span class="sxs-lookup"><span data-stu-id="e2538-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="e2538-133">Denormalizzando i dati, è possibile che l'applicazione debba eseguire meno query e aggiornamenti per completare le comuni operazioni.</span><span class="sxs-lookup"><span data-stu-id="e2538-133">By denormalizing data, your application may need to issue fewer queries and updates to complete common operations.</span></span> 

### <a name="when-to-embed"></a><span data-ttu-id="e2538-134">Quando eseguire l'incorporamento</span><span class="sxs-lookup"><span data-stu-id="e2538-134">When to embed</span></span>
<span data-ttu-id="e2538-135">In generale, usare i modelli di dati incorporati quando:</span><span class="sxs-lookup"><span data-stu-id="e2538-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="e2538-136">Esistono relazioni **contains** tra le entità.</span><span class="sxs-lookup"><span data-stu-id="e2538-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="e2538-137">Esistono relazioni **one-to-few** tra le entità.</span><span class="sxs-lookup"><span data-stu-id="e2538-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="e2538-138">Esistono dati incorporati che **cambiano raramente**.</span><span class="sxs-lookup"><span data-stu-id="e2538-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="e2538-139">Esistono dati incorporati che non aumenteranno **senza limiti**.</span><span class="sxs-lookup"><span data-stu-id="e2538-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="e2538-140">Esistono dati incorporati che sono parte **integrante** dei dati in un documento.</span><span class="sxs-lookup"><span data-stu-id="e2538-140">There is embedded data that is **integral** to data in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="e2538-141">I modelli di dati denormalizzati garantiscono di solito prestazioni di **lettura** più elevate.</span><span class="sxs-lookup"><span data-stu-id="e2538-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-to-embed"></a><span data-ttu-id="e2538-142">Quando non eseguire l'incorporamento</span><span class="sxs-lookup"><span data-stu-id="e2538-142">When not to embed</span></span>
<span data-ttu-id="e2538-143">Anche se in linea generale in un database di documenti si denormalizza tutto e si incorporano tutti i dati in un solo documento, questo può creare situazioni che sarebbe meglio evitare.</span><span class="sxs-lookup"><span data-stu-id="e2538-143">While the rule of thumb in a document database is to denormalize everything and embed all data in to a single document, this can lead to some situations that should be avoided.</span></span>

<span data-ttu-id="e2538-144">Consideriamo questo frammento JSON.</span><span class="sxs-lookup"><span data-stu-id="e2538-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="e2538-145">Questo potrebbe essere l'aspetto di un'entità post con commenti incorporati, se si modellasse un tipico sistema di blog, o CMS.</span><span class="sxs-lookup"><span data-stu-id="e2538-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="e2538-146">Il problema di questo esempio è che la matrice di commenti non è **limitata**, vale a dire che non esiste in pratica un limite al numero di commenti per i singoli post.</span><span class="sxs-lookup"><span data-stu-id="e2538-146">The problem with this example is that the comments array is **unbounded**, meaning that there is no (practical) limit to the number of comments any single post can have.</span></span> <span data-ttu-id="e2538-147">Questo sarà un problema qualora le dimensioni del documento aumentassero considerevolmente.</span><span class="sxs-lookup"><span data-stu-id="e2538-147">This will become a problem as the size of the document could grow significantly.</span></span>

<span data-ttu-id="e2538-148">Quando le dimensioni del documento aumentano, diventa più difficile trasmettere i dati nella rete come anche leggere e aggiornare il documento.</span><span class="sxs-lookup"><span data-stu-id="e2538-148">As the size of the document grows the ability to transmit the data over the wire as well as reading and updating the document, at scale, will be impacted.</span></span>

<span data-ttu-id="e2538-149">In questo caso, sarebbe meglio prendere in considerazione il modello seguente.</span><span class="sxs-lookup"><span data-stu-id="e2538-149">In this case it would be better to consider the following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in the coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from the interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from the field"},
            ...
            {"id": 99, "author": "angry", "comment": "blah angry blah angry"}
        ]
    },
    {
        "postId": "1"
        "comments": [
            {"id": 100, "author": "anon", "comment": "yet more"},
            ...
            {"id": 199, "author": "bored", "comment": "will this ever end?"}
        ]
    }

<span data-ttu-id="e2538-150">Questo modello ha i tre commenti più recenti incorporati nel post, che questa volta è una matrice con un limite fisso.</span><span class="sxs-lookup"><span data-stu-id="e2538-150">This model has the three most recent comments embedded on the post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="e2538-151">Gli altri commenti sono raggruppati in batch di 100 commenti e archiviati in documenti separati.</span><span class="sxs-lookup"><span data-stu-id="e2538-151">The other comments are grouped in to batches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="e2538-152">La dimensione scelta per il batch è 100 perché l'applicazione fittizia consente all'utente di caricare 100 commenti per volta.</span><span class="sxs-lookup"><span data-stu-id="e2538-152">The size of the batch was chosen as 100 because our fictitious application allows the user to load 100 comments at a time.</span></span>  

<span data-ttu-id="e2538-153">Un altro caso in cui non è consigliabile ricorrere all'incorporamento dei dati è quando i dati incorporati vengono usati spesso nei documenti e cambiano spesso.</span><span class="sxs-lookup"><span data-stu-id="e2538-153">Another case where embedding data is not a good idea is when the embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="e2538-154">Consideriamo questo frammento JSON.</span><span class="sxs-lookup"><span data-stu-id="e2538-154">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            {
                "numberHeld": 100,
                "stock": { "symbol": "zaza", "open": 1, "high": 2, "low": 0.5 }
            },
            {
                "numberHeld": 50,
                "stock": { "symbol": "xcxc", "open": 89, "high": 93.24, "low": 88.87 }
            }
        ]
    }

<span data-ttu-id="e2538-155">Questo potrebbe essere il portafoglio azionario di una persona.</span><span class="sxs-lookup"><span data-stu-id="e2538-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="e2538-156">Abbiamo scelto di incorporare le informazioni sulle azioni in ogni documento del portafoglio.</span><span class="sxs-lookup"><span data-stu-id="e2538-156">We have chosen to embed the stock information in to each portfolio document.</span></span> <span data-ttu-id="e2538-157">In un ambiente in cui i dati correlati cambieranno spesso, come in un'applicazione per le contrattazioni azionarie, l'incorporamento di dati che cambiano spesso obbligherà ad aggiornare continuamente ogni documento del portafoglio ogni volta che viene scambiata un'azione.</span><span class="sxs-lookup"><span data-stu-id="e2538-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going to mean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="e2538-158">Il titolo *zaza* potrebbe essere scambiato diverse centinaia di volte in un solo giorno e migliaia di utenti potrebbero avere *zaza* nel portafoglio.</span><span class="sxs-lookup"><span data-stu-id="e2538-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="e2538-159">Con un modello di dati come quello sopra sarebbe necessario aggiornare diverse migliaia di documenti del portfolio più volte al giorno e la scalabilità del sistema non sarebbe efficiente.</span><span class="sxs-lookup"><span data-stu-id="e2538-159">With a data model like the above we would have to update many thousands of portfolio documents many times every day leading to a system that won't scale very well.</span></span> 

## <span data-ttu-id="e2538-160"><a id="Refer"></a>Dati di riferimento</span><span class="sxs-lookup"><span data-stu-id="e2538-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="e2538-161">L'incorporamento dei dati quindi funziona senza problemi in molti casi, ma è evidente che in altri scenari la denormalizzazione dei dati è più che altro causa di problemi.</span><span class="sxs-lookup"><span data-stu-id="e2538-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="e2538-162">Cosa si può fare dunque?</span><span class="sxs-lookup"><span data-stu-id="e2538-162">So what do we do now?</span></span> 

<span data-ttu-id="e2538-163">Le relazioni tra entità non devono essere necessariamente create in un database relazionale.</span><span class="sxs-lookup"><span data-stu-id="e2538-163">Relational databases are not the only place where you can create relationships between entities.</span></span> <span data-ttu-id="e2538-164">In un database di documenti è possibile tenere in un documento informazioni che sono effettivamente correlate ai dati in altri documenti.</span><span class="sxs-lookup"><span data-stu-id="e2538-164">In a document database you can have information in one document that actually relates to data in other documents.</span></span> <span data-ttu-id="e2538-165">Non si consiglia di creare sistemi che sarebbero più appropriati per un database relazionale in Azure Cosmos DB o in qualsiasi altro database di documenti, tuttavia le relazioni semplici vanno bene e possono essere molto utili.</span><span class="sxs-lookup"><span data-stu-id="e2538-165">Now, I am not advocating for even one minute that we build systems that would be better suited to a relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="e2538-166">Nel codice JSON seguente abbiamo scelto di usare l'esempio del portafoglio di azioni di prima, ma questa volta facciamo riferimento all'elemento titolo nel portafoglio invece di incorporarlo.</span><span class="sxs-lookup"><span data-stu-id="e2538-166">In the JSON below we chose to use the example of a stock portfolio from earlier but this time we refer to the stock item on the portfolio instead of embedding it.</span></span> <span data-ttu-id="e2538-167">In questo modo, anche se l'elemento titolo cambia più volte nel corso della giornata, il solo documento da aggiornare è il documento del titolo.</span><span class="sxs-lookup"><span data-stu-id="e2538-167">This way, when the stock item changes frequently throughout the day the only document that needs to be updated is the single stock document.</span></span> 

    Person document:
    {
        "id": "1",
        "firstName": "Thomas",
        "lastName": "Andersen",
        "holdings": [
            { "numberHeld":  100, "stockId": 1},
            { "numberHeld":  50, "stockId": 2}
        ]
    }

    Stock documents:
    {
        "id": "1",
        "symbol": "zaza",
        "open": 1,
        "high": 2,
        "low": 0.5,
        "vol": 11970000,
        "mkt-cap": 42000000,
        "pe": 5.89
    },
    {
        "id": "2",
        "symbol": "xcxc",
        "open": 89,
        "high": 93.24,
        "low": 88.87,
        "vol": 2970200,
        "mkt-cap": 1005000,
        "pe": 75.82
    }


<span data-ttu-id="e2538-168">L'aspetto negativo di questo approccio diventa però immediatamente evidente se l'applicazione deve mostrare informazioni su ogni titolo disponibile quando si visualizza il portafoglio di una persona. In questo caso, sarebbe necessario accedere più volte al database per caricare le informazioni del documento di ogni titolo.</span><span class="sxs-lookup"><span data-stu-id="e2538-168">An immediate downside to this approach though is if your application is required to show information about each stock that is held when displaying a person's portfolio; in this case you would need to make multiple trips to the database to load the information for each stock document.</span></span> <span data-ttu-id="e2538-169">Qui è stata presa la decisione di aumentare l'efficienza delle operazioni di scrittura, che vengono eseguite spesso durante la giornata, compromettendo però le operazioni di lettura che hanno un impatto potenzialmente minore sulle prestazioni di questo particolare sistema.</span><span class="sxs-lookup"><span data-stu-id="e2538-169">Here we've made a decision to improve the efficiency of write operations, which happen frequently throughout the day, but in turn compromised on the read operations that potentially have less impact on the performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="e2538-170">I modelli di dati normalizzati **possono richiedere più round trip** al server.</span><span class="sxs-lookup"><span data-stu-id="e2538-170">Normalized data models **can require more round trips** to the server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="e2538-171">Chiavi esterne</span><span class="sxs-lookup"><span data-stu-id="e2538-171">What about foreign keys?</span></span>
<span data-ttu-id="e2538-172">Poiché attualmente non esiste alcun vincolo, chiave esterna o altro, le relazioni esistenti tra i documenti sono di fatto "collegamenti deboli" e non verranno verificate dal database.</span><span class="sxs-lookup"><span data-stu-id="e2538-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by the database itself.</span></span> <span data-ttu-id="e2538-173">Per essere certi che i dati a cui un documento fa riferimento esistano davvero, è eseguire questa operazione nell'applicazione oppure tramite trigger lato server o stored procedure in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e2538-173">If you want to ensure that the data a document is referring to actually exists, then you need to do this in your application, or through the use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-to-reference"></a><span data-ttu-id="e2538-174">Quando fare riferimento</span><span class="sxs-lookup"><span data-stu-id="e2538-174">When to reference</span></span>
<span data-ttu-id="e2538-175">In generale, usare i modelli di dati denormalizzati quando:</span><span class="sxs-lookup"><span data-stu-id="e2538-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="e2538-176">Si rappresentano relazioni **uno a molti** .</span><span class="sxs-lookup"><span data-stu-id="e2538-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="e2538-177">Si rappresentano relazioni **molti a molti** .</span><span class="sxs-lookup"><span data-stu-id="e2538-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="e2538-178">I dati correlati **cambiano spesso**.</span><span class="sxs-lookup"><span data-stu-id="e2538-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="e2538-179">È possibile che i dati a cui si fa riferimento **non siamo limitati**.</span><span class="sxs-lookup"><span data-stu-id="e2538-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="e2538-180">La normalizzazione offre di solito migliori prestazioni di **scrittura** .</span><span class="sxs-lookup"><span data-stu-id="e2538-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-the-relationship"></a><span data-ttu-id="e2538-181">Dove inserire le relazioni</span><span class="sxs-lookup"><span data-stu-id="e2538-181">Where do I put the relationship?</span></span>
<span data-ttu-id="e2538-182">La crescita della relazione aiuterà a determinare in quale documento archiviare il riferimento.</span><span class="sxs-lookup"><span data-stu-id="e2538-182">The growth of the relationship will help determine in which document to store the reference.</span></span>

<span data-ttu-id="e2538-183">Il codice JSON seguente modella editori e libri.</span><span class="sxs-lookup"><span data-stu-id="e2538-183">If we look at the JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over the world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in to Azure Cosmos DB" }

<span data-ttu-id="e2538-184">Se il numero di libri per editore è piccolo e ha una crescita limitata, può essere utile archiviare il riferimento ai libri nel documento dell'editore.</span><span class="sxs-lookup"><span data-stu-id="e2538-184">If the number of the books per publisher is small with limited growth, then storing the book reference inside the publisher document may be useful.</span></span> <span data-ttu-id="e2538-185">Se invece il numero di libri per editore è illimitato, questo modello di dati darà origine a matrici modificabili e in costante crescita, come nel documento dell'editore di esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="e2538-185">However, if the number of books per publisher is unbounded, then this data model would lead to mutable, growing arrays, as in the example publisher document above.</span></span> 

<span data-ttu-id="e2538-186">Cambiando un po' le cose, si ottiene un modello che rappresenta sempre gli stessi dati, ma che ora evita queste grandi raccolte modificabili.</span><span class="sxs-lookup"><span data-stu-id="e2538-186">Switching things around a bit would result in a model that still represents the same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over the world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in to Azure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="e2538-187">Nell'esempio precedente, abbiamo eliminato la raccolta illimitata nel documento dell'editore.</span><span class="sxs-lookup"><span data-stu-id="e2538-187">In the above example, we have dropped the unbounded collection on the publisher document.</span></span> <span data-ttu-id="e2538-188">Ora abbiamo un solo riferimento all'editore nel documento di ogni libro.</span><span class="sxs-lookup"><span data-stu-id="e2538-188">Instead we just have a a reference to the publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="e2538-189">Come modellare le relazioni many:many?</span><span class="sxs-lookup"><span data-stu-id="e2538-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="e2538-190">In un database relazionale le relazioni *molti a molti* vengono spesso modellate con le tabelle join, che creano un join dei record delle altre tabelle.</span><span class="sxs-lookup"><span data-stu-id="e2538-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Unione di tabelle](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="e2538-192">Si potrebbe essere tentati di replicare la stessa cosa con i documenti e di generare un modello di dati simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="e2538-192">You might be tempted to replicate the same thing using documents and produce a data model that looks similar to the following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over the world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in to Azure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="e2538-193">Funzionerebbe,</span><span class="sxs-lookup"><span data-stu-id="e2538-193">This would work.</span></span> <span data-ttu-id="e2538-194">ma, per caricare un autore con i suoi libri o un libro con il suo autore, sarebbero sempre necessarie almeno altre due query sul database;</span><span class="sxs-lookup"><span data-stu-id="e2538-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against the database.</span></span> <span data-ttu-id="e2538-195">una query per creare un join del documento e quindi un'altra query per recuperare il documento effettivo di cui viene creato il join.</span><span class="sxs-lookup"><span data-stu-id="e2538-195">One query to the joining document and then another query to fetch the actual document being joined.</span></span> 

<span data-ttu-id="e2538-196">Se la tabella join si limita a incollare insieme due gruppi di dati, allora perché non eliminarla del tutto?</span><span class="sxs-lookup"><span data-stu-id="e2538-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="e2538-197">Tenere in considerazione quanto segue.</span><span class="sxs-lookup"><span data-stu-id="e2538-197">Consider the following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in to Azure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="e2538-198">Se avessimo un autore, sapremmo immediatamente quali libri ha scritto e, al contrario, se avessimo caricato un documento relativo ai libri, conosceremmo gli ID degli autori.</span><span class="sxs-lookup"><span data-stu-id="e2538-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know the ids of the author(s).</span></span> <span data-ttu-id="e2538-199">Questo evita la query intermedia sulla tabella join riducendo il numero di round trip al server che l'applicazione deve eseguire.</span><span class="sxs-lookup"><span data-stu-id="e2538-199">This saves that intermediary query against the join table reducing the number of server round trips your application has to make.</span></span> 

## <span data-ttu-id="e2538-200"><a id="WrapUp"></a>Modelli di dati ibridi</span><span class="sxs-lookup"><span data-stu-id="e2538-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="e2538-201">Come si è visto, sia l'incorporamento (o denormalizzazione) che il riferimento (o normalizzazione) ai dati presentano vantaggi e compromessi.</span><span class="sxs-lookup"><span data-stu-id="e2538-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="e2538-202">Ma non è sempre necessario scegliere uno dei due. È anche possibile mischiare un po' le cose.</span><span class="sxs-lookup"><span data-stu-id="e2538-202">It doesn't always have to be either or, don't be scared to mix things up a little.</span></span> 

<span data-ttu-id="e2538-203">In base ai modelli di utilizzo e ai carichi di lavoro specifici dell'applicazione, in certi casi può avere senso unire i dati incorporati e quelli a cui si fa riferimento per ottenere una logica dell'applicazione più semplice con meno round trip al server, mantenendo ugualmente un buon livello di prestazioni.</span><span class="sxs-lookup"><span data-stu-id="e2538-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead to simpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="e2538-204">Si consideri il codice JSON seguente.</span><span class="sxs-lookup"><span data-stu-id="e2538-204">Consider the following JSON.</span></span> 

    Author documents: 
    {
        "id": "a1",
        "firstName": "Thomas",
        "lastName": "Andersen",        
        "countOfBooks": 3,
         "books": ["b1", "b2", "b3"],
        "images": [
            {"thumbnail": "http://....png"}
            {"profile": "http://....png"}
            {"large": "http://....png"}
        ]
    },
    {
        "id": "a2",
        "firstName": "William",
        "lastName": "Wakefield",
        "countOfBooks": 1,
        "books": ["b1"],
        "images": [
            {"thumbnail": "http://....png"}
        ]
    }

    Book documents:
    {
        "id": "b1",
        "name": "Azure Cosmos DB 101",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
            {"id": "a2", "name": "William Wakefield", "thumbnailUrl": "http://....png"}
        ]
    },
    {
        "id": "b2",
        "name": "Azure Cosmos DB for RDBMS Users",
        "authors": [
            {"id": "a1", "name": "Thomas Andersen", "thumbnailUrl": "http://....png"},
        ]
    }

<span data-ttu-id="e2538-205">Qui abbiamo per lo più seguito il modello incorporato, in cui i dati delle altre entità vengono incorporati nel documento di primo livello, ma viene fatto riferimento agli altri dati.</span><span class="sxs-lookup"><span data-stu-id="e2538-205">Here we've (mostly) followed the embedded model, where data from other entities are embedded in the top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="e2538-206">Se si osserva il documento dei libri, si possono vedere alcuni campi interessanti quando si considera la matrice degli autori.</span><span class="sxs-lookup"><span data-stu-id="e2538-206">If you look at the book document, we can see a few interesting fields when we look at the array of authors.</span></span> <span data-ttu-id="e2538-207">È presente un campo *id*che viene usato per fare riferimento al documento di un autore, che è una procedura standard in un modello normalizzato, ma poi sono presenti anche *name* e *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="e2538-207">There is an *id* field which is the field we use to refer back to an author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="e2538-208">Avremmo potuto limitarci a *id* e lasciare che l'applicazione recuperasse le altre informazioni necessarie dal relativo documento dell'autore usando il "collegamento", ma, dal momento che l'applicazione visualizza il nome e un'immagine di anteprima dell'autore con ogni libro visualizzato, è possibile evitare un round trip al server per ogni libro di un elenco denormalizzando **alcuni** dati dall'autore.</span><span class="sxs-lookup"><span data-stu-id="e2538-208">We could've just stuck with *id* and left the application to get any additional information it needed from the respective author document using the "link", but because our application displays the author's name and a thumbnail picture with every book displayed we can save a round trip to the server per book in a list by denormalizing **some** data from the author.</span></span>

<span data-ttu-id="e2538-209">Ovviamente, se l'autore cambiasse nome o se volesse aggiornare la foto, sarebbe necessario eseguire un aggiornamento per ogni libro pubblicato, ma per la nostra applicazione, che si basa sul presupposto che gli autori non cambino nome molto spesso, questa è una decisione di progettazione accettabile.</span><span class="sxs-lookup"><span data-stu-id="e2538-209">Sure, if the author's name changed or they wanted to update their photo we'd have to go an update every book they ever published but for our application, based on the assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="e2538-210">Nell'esempio ci sono valori di **aggregati precalcolati** per evitare la costosa elaborazione di un'operazione di lettura.</span><span class="sxs-lookup"><span data-stu-id="e2538-210">In the example there are **pre-calculated aggregates** values to save expensive processing on a read operation.</span></span> <span data-ttu-id="e2538-211">Nell'esempio, alcuni dati incorporati nel documento dell'autore vengono calcolati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="e2538-211">In the example, some of the data embedded in the author document is data that is calculated at run-time.</span></span> <span data-ttu-id="e2538-212">Ogni volta che viene pubblicato un nuovo libro, viene creato un documento per il libro **e** il campo countOfBooks viene impostato su un valore calcolato in base al numero di documenti dei libri esistenti per un determinato autore.</span><span class="sxs-lookup"><span data-stu-id="e2538-212">Every time a new book is published, a book document is created **and** the countOfBooks field is set to a calculated value based on the number of book documents that exist for a particular author.</span></span> <span data-ttu-id="e2538-213">Questa ottimizzazione andrebbe bene nei sistemi che eseguono un'intensa attività di lettura, in cui si è disposti a effettuare calcoli nelle scritture per ottimizzare le letture.</span><span class="sxs-lookup"><span data-stu-id="e2538-213">This optimization would be good in read heavy systems where we can afford to do computations on writes in order to optimize reads.</span></span>

<span data-ttu-id="e2538-214">Azure Cosmos DB supporta le transazioni in più documenti e consente quindi di usare **transazioni su più documenti**.</span><span class="sxs-lookup"><span data-stu-id="e2538-214">The ability to have a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="e2538-215">Molti archivi NoSQL non possono eseguire le transazioni nei documenti e, a causa di questa limitazione, inducono a prendere decisioni di progettazione, ad esempio "incorporare sempre tutto".</span><span class="sxs-lookup"><span data-stu-id="e2538-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due to this limitation.</span></span> <span data-ttu-id="e2538-216">Con Azure Cosmos DB è possibile usare trigger lato server, o stored procedure, che inseriscono i libri e aggiornano gli autori in una sola transazione ACID.</span><span class="sxs-lookup"><span data-stu-id="e2538-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="e2538-217">Ora non è **necessario** incorporare tutto in un documento solo per essere sicuri che i dati rimangano coerenti.</span><span class="sxs-lookup"><span data-stu-id="e2538-217">Now you don't **have** to embed everything in to one document just to be sure that your data remains consistent.</span></span>

## <span data-ttu-id="e2538-218"><a name="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e2538-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="e2538-219">Il concetto principale espresso in questo articolo è che la modellazione dei dati in un ambiente senza schema è più importante che mai.</span><span class="sxs-lookup"><span data-stu-id="e2538-219">The biggest takeaways from this article is to understand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="e2538-220">Come non esiste un solo modo per rappresentare i dati in una schermata, così non esiste un solo modo per modellare i dati.</span><span class="sxs-lookup"><span data-stu-id="e2538-220">Just as there is no single way to represent a piece of data on a screen, there is no single way to model your data.</span></span> <span data-ttu-id="e2538-221">È necessario conoscere l'applicazione e come genererà, userà ed elaborerà i dati.</span><span class="sxs-lookup"><span data-stu-id="e2538-221">You need to understand your application and how it will produce, consume, and process the data.</span></span> <span data-ttu-id="e2538-222">Quindi, applicando alcune delle linee guida presentate qui, è possibile iniziare a creare un modello che risponda alle esigenze immediate dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="e2538-222">Then, by applying some of the guidelines presented here you can set about creating a model that addresses the immediate needs of your application.</span></span> <span data-ttu-id="e2538-223">Quando le applicazioni devono essere modificate, è possibile sfruttare la flessibilità di un database senza schema per accettare la modifica e far evolvere facilmente il modello di dati.</span><span class="sxs-lookup"><span data-stu-id="e2538-223">When your applications need to change, you can leverage the flexibility of a schema-free database to embrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="e2538-224">Per altre informazioni su Azure Cosmos DB, vedere la pagina della [documentazione](https://azure.microsoft.com/documentation/services/cosmos-db/) del servizio.</span><span class="sxs-lookup"><span data-stu-id="e2538-224">To learn more about Azure Cosmos DB, refer to the service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="e2538-225">Per informazioni su come suddividere i dati in più partizioni, vedere [Partizionamento dei dati in Azure Cosmos DB](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="e2538-225">To understand how to shard your data across multiple partitions, refer to [Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
