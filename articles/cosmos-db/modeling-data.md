---
title: dati del documento per un database NoSQL aaaModeling | Documenti Microsoft
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
ms.openlocfilehash: 2e388c833f204287896dfa8e6f79c88073731b6b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="modeling-document-data-for-nosql-databases"></a><span data-ttu-id="2a136-104">Modellazione dei dati di un documento per un database NoSQL</span><span class="sxs-lookup"><span data-stu-id="2a136-104">Modeling document data for NoSQL databases</span></span>
<span data-ttu-id="2a136-105">Database privi di schema, come Azure Cosmos DB, semplificano super tooembrace modello di dati tooyour modifiche ancora dedicare alcuni tempo concepire i dati.</span><span class="sxs-lookup"><span data-stu-id="2a136-105">While schema-free databases, like Azure Cosmos DB, make it super easy tooembrace changes tooyour data model you should still spend some time thinking about your data.</span></span> 

<span data-ttu-id="2a136-106">Dati modalità toobe archiviati?</span><span class="sxs-lookup"><span data-stu-id="2a136-106">How is data going toobe stored?</span></span> <span data-ttu-id="2a136-107">Quali sono i dati dell'applicazione continua tooretrieve e query?</span><span class="sxs-lookup"><span data-stu-id="2a136-107">How is your application going tooretrieve and query data?</span></span> <span data-ttu-id="2a136-108">L'applicazione esegue un'intensa attività di lettura o un'intensa attività di scrittura?</span><span class="sxs-lookup"><span data-stu-id="2a136-108">Is your application read heavy, or write heavy?</span></span> 

<span data-ttu-id="2a136-109">Dopo aver letto questo articolo, sarà in grado di tooanswer hello seguenti domande:</span><span class="sxs-lookup"><span data-stu-id="2a136-109">After reading this article, you will be able tooanswer hello following questions:</span></span>

* <span data-ttu-id="2a136-110">Come si deve considerare un documento in un database di documenti?</span><span class="sxs-lookup"><span data-stu-id="2a136-110">How should I think about a document in a document database?</span></span>
* <span data-ttu-id="2a136-111">Cos'è la modellazione dei dati e perché è importante?</span><span class="sxs-lookup"><span data-stu-id="2a136-111">What is data modeling and why should I care?</span></span> 
* <span data-ttu-id="2a136-112">Come viene modellare i dati in un database relazionale di database diversi tooa documento?</span><span class="sxs-lookup"><span data-stu-id="2a136-112">How is modeling data in a document database different tooa relational database?</span></span>
* <span data-ttu-id="2a136-113">Come si esprimono le relazioni tra i dati in un database non relazionale?</span><span class="sxs-lookup"><span data-stu-id="2a136-113">How do I express data relationships in a non-relational database?</span></span>
* <span data-ttu-id="2a136-114">Quando si incorporano dati e quando si collega toodata?</span><span class="sxs-lookup"><span data-stu-id="2a136-114">When do I embed data and when do I link toodata?</span></span>

## <a name="embedding-data"></a><span data-ttu-id="2a136-115">Incorporamento dei dati</span><span class="sxs-lookup"><span data-stu-id="2a136-115">Embedding data</span></span>
<span data-ttu-id="2a136-116">Quando si avvia modellazione dei dati in un archivio di documento, ad esempio Azure Cosmos DB, provare a tootreat le entità come **documenti indipendenti** rappresentato in JSON.</span><span class="sxs-lookup"><span data-stu-id="2a136-116">When you start modeling data in a document store, such as Azure Cosmos DB, try tootreat your entities as **self-contained documents** represented in JSON.</span></span>

<span data-ttu-id="2a136-117">Prima di proseguire, è meglio fare un passo indietro e pensare a come sia possibile modellare qualcosa in un database relazionale, un argomento con cui molti hanno già familiarità.</span><span class="sxs-lookup"><span data-stu-id="2a136-117">Before we dive in too much further, let us take a few steps back and have a look at how we might model something in a relational database, a subject many of us are already familiar with.</span></span> <span data-ttu-id="2a136-118">Hello esempio seguente viene illustrato come una persona potrebbe essere archiviata in un database relazionale.</span><span class="sxs-lookup"><span data-stu-id="2a136-118">hello following example shows how a person might be stored in a relational database.</span></span> 

![Database relazionale](./media/documentdb-modeling-data/relational-data-model.png)

<span data-ttu-id="2a136-120">Quando si lavora con i database relazionali, è state illustrate per toonormalize anni, la normalizzazione, normalizzare.</span><span class="sxs-lookup"><span data-stu-id="2a136-120">When working with relational databases, we've been taught for years toonormalize, normalize, normalize.</span></span>

<span data-ttu-id="2a136-121">Normalizzazione dei dati in genere implica l'esecuzione di un'entità, ad esempio una persona, nonché suddividere in toodiscrete porzioni di dati.</span><span class="sxs-lookup"><span data-stu-id="2a136-121">Normalizing your data typically involves taking an entity, such as a person, and breaking it down in toodiscrete pieces of data.</span></span> <span data-ttu-id="2a136-122">Nell'esempio hello sopra, una persona può disporre di più record di informazioni di contatto, nonché di più record di indirizzo.</span><span class="sxs-lookup"><span data-stu-id="2a136-122">In hello example above, a person can have multiple contact detail records as well as multiple address records.</span></span> <span data-ttu-id="2a136-123">È possibile andare oltre e suddividere i dettagli contatto estraendo anche i campi comuni come tipo.</span><span class="sxs-lookup"><span data-stu-id="2a136-123">We even go one step further and break down contact details by further extracting common fields like a type.</span></span> <span data-ttu-id="2a136-124">Lo stesso per l'indirizzo: ogni record qui ha un tipo, ad esempio *Abitazione* o *Ufficio*</span><span class="sxs-lookup"><span data-stu-id="2a136-124">Same for address, each record here has a type like *Home* or *Business*</span></span> 

<span data-ttu-id="2a136-125">Guida locale quando normalizzazione dei dati è troppo Hello**evitare di archiviare dati ridondanti** in ogni record e invece fare riferimento toodata.</span><span class="sxs-lookup"><span data-stu-id="2a136-125">hello guiding premise when normalizing data is too**avoid storing redundant data** on each record and rather refer toodata.</span></span> <span data-ttu-id="2a136-126">In questo esempio, tooread una persona, con tutti i relativi dettagli di contatto e gli indirizzi, è necessario toouse join tooeffectively aggregare i dati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2a136-126">In this example, tooread a person, with all their contact details and addresses, you need toouse JOINS tooeffectively aggregate your data at run time.</span></span>

    SELECT p.FirstName, p.LastName, a.City, cd.Detail
    FROM Person p
    JOIN ContactDetail cd ON cd.PersonId = p.Id
    JOIN ContactDetailType on cdt ON cdt.Id = cd.TypeId
    JOIN Address a ON a.PersonId = p.Id

<span data-ttu-id="2a136-127">Per aggiornare una singola persona con i dettagli contatto e gli indirizzi, è necessario eseguire operazioni di scrittura in più tabelle.</span><span class="sxs-lookup"><span data-stu-id="2a136-127">Updating a single person with their contact details and addresses requires write operations across many individual tables.</span></span> 

<span data-ttu-id="2a136-128">Ora è possibile osservare come si sarebbe modello hello stessi dati come entità indipendenti in un database di documenti.</span><span class="sxs-lookup"><span data-stu-id="2a136-128">Now let's take a look at how we would model hello same data as a self-contained entity in a document database.</span></span>

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

<span data-ttu-id="2a136-129">Approccio hello precedente abbiamo ora **denormalizzati** hello record utente in cui è **incorporato** tutti hello informazioni relative a toothis persona, ad esempio le informazioni di contatto e indirizzi in tooa singolo Documento JSON.</span><span class="sxs-lookup"><span data-stu-id="2a136-129">Using hello approach above we have now **denormalized** hello person record where we **embedded** all hello information relating toothis person, such as their contact details and addresses, in tooa single JSON document.</span></span>
<span data-ttu-id="2a136-130">Inoltre, poiché non ci stiamo limitati tooa uno schema fisso che abbiamo hello flessibilità toodo quali con i dettagli di contatto di diverse forme completamente.</span><span class="sxs-lookup"><span data-stu-id="2a136-130">In addition, because we're not confined tooa fixed schema we have hello flexibility toodo things like having contact details of different shapes entirely.</span></span> 

<span data-ttu-id="2a136-131">Il recupero di un record utente completo dal database hello è ora una singola operazione su una singola raccolta e di un singolo documento di lettura.</span><span class="sxs-lookup"><span data-stu-id="2a136-131">Retrieving a complete person record from hello database is now a single read operation against a single collection and for a single document.</span></span> <span data-ttu-id="2a136-132">Anche l'aggiornamento del record di una persona, con i dettagli contatto e gli indirizzi, richiede una sola operazione di scrittura in un solo documento.</span><span class="sxs-lookup"><span data-stu-id="2a136-132">Updating a person record, with their contact details and addresses, is also a single write operation against a single document.</span></span>

<span data-ttu-id="2a136-133">Da denormalizzazione dei dati, l'applicazione potrebbe essere necessario tooissue meno query e aggiornamenti toocomplete operazioni comuni.</span><span class="sxs-lookup"><span data-stu-id="2a136-133">By denormalizing data, your application may need tooissue fewer queries and updates toocomplete common operations.</span></span> 

### <a name="when-tooembed"></a><span data-ttu-id="2a136-134">Quando tooembed</span><span class="sxs-lookup"><span data-stu-id="2a136-134">When tooembed</span></span>
<span data-ttu-id="2a136-135">In generale, usare i modelli di dati incorporati quando:</span><span class="sxs-lookup"><span data-stu-id="2a136-135">In general, use embedded data models when:</span></span>

* <span data-ttu-id="2a136-136">Esistono relazioni **contains** tra le entità.</span><span class="sxs-lookup"><span data-stu-id="2a136-136">There are **contains** relationships between entities.</span></span>
* <span data-ttu-id="2a136-137">Esistono relazioni **one-to-few** tra le entità.</span><span class="sxs-lookup"><span data-stu-id="2a136-137">There are **one-to-few** relationships between entities.</span></span>
* <span data-ttu-id="2a136-138">Esistono dati incorporati che **cambiano raramente**.</span><span class="sxs-lookup"><span data-stu-id="2a136-138">There is embedded data that **changes infrequently**.</span></span>
* <span data-ttu-id="2a136-139">Esistono dati incorporati che non aumenteranno **senza limiti**.</span><span class="sxs-lookup"><span data-stu-id="2a136-139">There is embedded data won't grow **without bound**.</span></span>
* <span data-ttu-id="2a136-140">Non ci sono dati incorporati che sono **integrale** toodata in un documento.</span><span class="sxs-lookup"><span data-stu-id="2a136-140">There is embedded data that is **integral** toodata in a document.</span></span>

> [!NOTE]
> <span data-ttu-id="2a136-141">I modelli di dati denormalizzati garantiscono di solito prestazioni di **lettura** più elevate.</span><span class="sxs-lookup"><span data-stu-id="2a136-141">Typically denormalized data models provide better **read** performance.</span></span>
> 
> 

### <a name="when-not-tooembed"></a><span data-ttu-id="2a136-142">Quando non tooembed</span><span class="sxs-lookup"><span data-stu-id="2a136-142">When not tooembed</span></span>
<span data-ttu-id="2a136-143">Mentre hello regola empirica in un database di documenti è toodenormalize tutto quello che incorpora tutti i dati nel documento singolo tooa, ciò può comportare situazioni toosome che dovrebbero essere evitate.</span><span class="sxs-lookup"><span data-stu-id="2a136-143">While hello rule of thumb in a document database is toodenormalize everything and embed all data in tooa single document, this can lead toosome situations that should be avoided.</span></span>

<span data-ttu-id="2a136-144">Consideriamo questo frammento JSON.</span><span class="sxs-lookup"><span data-stu-id="2a136-144">Take this JSON snippet.</span></span>

    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "comments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            …
            {"id": 100001, "author": "jane", "comment": "and on we go ..."},
            …
            {"id": 1000000001, "author": "angry", "comment": "blah angry blah angry"},
            …
            {"id": ∞ + 1, "author": "bored", "comment": "oh man, will this ever end?"},
        ]
    }

<span data-ttu-id="2a136-145">Questo potrebbe essere l'aspetto di un'entità post con commenti incorporati, se si modellasse un tipico sistema di blog, o CMS.</span><span class="sxs-lookup"><span data-stu-id="2a136-145">This might be what a post entity with embedded comments would look like if we were modeling a typical blog, or CMS, system.</span></span> <span data-ttu-id="2a136-146">problema con questo esempio Hello è tale hello matrice commenti è **unbounded**, non ovvero non esiste alcun toohello (pratiche) limitazione del numero dei commenti può avere qualsiasi singolo post.</span><span class="sxs-lookup"><span data-stu-id="2a136-146">hello problem with this example is that hello comments array is **unbounded**, meaning that there is no (practical) limit toohello number of comments any single post can have.</span></span> <span data-ttu-id="2a136-147">Dimensioni di hello del documento hello potrebbero aumentare notevolmente diventerà un problema.</span><span class="sxs-lookup"><span data-stu-id="2a136-147">This will become a problem as hello size of hello document could grow significantly.</span></span>

<span data-ttu-id="2a136-148">Come dimensione hello di hello documento aumenta dati hello tootransmit possibilità di hello in transito hello, nonché la lettura e aggiornamento documento hello, su larga scala, sarà interessato.</span><span class="sxs-lookup"><span data-stu-id="2a136-148">As hello size of hello document grows hello ability tootransmit hello data over hello wire as well as reading and updating hello document, at scale, will be impacted.</span></span>

<span data-ttu-id="2a136-149">In questo caso sarebbe migliore hello tooconsider seguente modello.</span><span class="sxs-lookup"><span data-stu-id="2a136-149">In this case it would be better tooconsider hello following model.</span></span>

    Post document:
    {
        "id": "1",
        "name": "What's new in hello coolest Cloud",
        "summary": "A blog post by someone real famous",
        "recentComments": [
            {"id": 1, "author": "anon", "comment": "something useful, I'm sure"},
            {"id": 2, "author": "bob", "comment": "wisdom from hello interwebs"},
            {"id": 3, "author": "jane", "comment": "....."}
        ]
    }

    Comment documents:
    {
        "postId": "1"
        "comments": [
            {"id": 4, "author": "anon", "comment": "more goodness"},
            {"id": 5, "author": "bob", "comment": "tails from hello field"},
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

<span data-ttu-id="2a136-150">Questo modello contiene i commenti più recente di hello tre incorporati in hello post stessa, ovvero una matrice con un limite fisso in questo momento.</span><span class="sxs-lookup"><span data-stu-id="2a136-150">This model has hello three most recent comments embedded on hello post itself, which is an array with a fixed bound this time.</span></span> <span data-ttu-id="2a136-151">Hello altri commenti vengono raggruppati in toobatches dei 100 commenti e archiviate in documenti distinti.</span><span class="sxs-lookup"><span data-stu-id="2a136-151">hello other comments are grouped in toobatches of 100 comments and stored in separate documents.</span></span> <span data-ttu-id="2a136-152">dimensioni di Hello di hello batch è stato scelto come 100 perché l'applicazione fittizia consente hello 100 commenti tooload dell'utente alla volta.</span><span class="sxs-lookup"><span data-stu-id="2a136-152">hello size of hello batch was chosen as 100 because our fictitious application allows hello user tooload 100 comments at a time.</span></span>  

<span data-ttu-id="2a136-153">Un altro caso in cui incorporare i dati non sono una buona idea è quando hello incorporato dati vengono utilizzati spesso in documenti e verranno modificati di frequente.</span><span class="sxs-lookup"><span data-stu-id="2a136-153">Another case where embedding data is not a good idea is when hello embedded data is used often across documents and will change frequently.</span></span> 

<span data-ttu-id="2a136-154">Consideriamo questo frammento JSON.</span><span class="sxs-lookup"><span data-stu-id="2a136-154">Take this JSON snippet.</span></span>

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

<span data-ttu-id="2a136-155">Questo potrebbe essere il portafoglio azionario di una persona.</span><span class="sxs-lookup"><span data-stu-id="2a136-155">This could represent a person's stock portfolio.</span></span> <span data-ttu-id="2a136-156">Informazioni sui titoli di hello tooembed scelto nel documento portfolio tooeach.</span><span class="sxs-lookup"><span data-stu-id="2a136-156">We have chosen tooembed hello stock information in tooeach portfolio document.</span></span> <span data-ttu-id="2a136-157">Incorporamento di dati che cambiano frequentemente in un ambiente in cui i dati correlati cambia di frequente, ad esempio un'applicazione che, in corso toomean che si sta aggiornando ogni documento portfolio costantemente ogni volta che vengono scambiate un azioni.</span><span class="sxs-lookup"><span data-stu-id="2a136-157">In an environment where related data is changing frequently, like a stock trading application, embedding data that changes frequently is going toomean that you are constantly updating each portfolio document every time a stock is traded.</span></span>

<span data-ttu-id="2a136-158">Il titolo *zaza* potrebbe essere scambiato diverse centinaia di volte in un solo giorno e migliaia di utenti potrebbero avere *zaza* nel portafoglio.</span><span class="sxs-lookup"><span data-stu-id="2a136-158">Stock *zaza* may be traded many hundreds of times in a single day and thousands of users could have *zaza* on their portfolio.</span></span> <span data-ttu-id="2a136-159">Con un modello di dati come hello sopra sono tooupdate molte migliaia di documenti portfolio molte volte ogni giorno tooa sistema che non verrà ridimensionato molto bene.</span><span class="sxs-lookup"><span data-stu-id="2a136-159">With a data model like hello above we would have tooupdate many thousands of portfolio documents many times every day leading tooa system that won't scale very well.</span></span> 

## <span data-ttu-id="2a136-160"><a id="Refer"></a>Dati di riferimento</span><span class="sxs-lookup"><span data-stu-id="2a136-160"><a id="Refer"></a>Referencing data</span></span>
<span data-ttu-id="2a136-161">L'incorporamento dei dati quindi funziona senza problemi in molti casi, ma è evidente che in altri scenari la denormalizzazione dei dati è più che altro causa di problemi.</span><span class="sxs-lookup"><span data-stu-id="2a136-161">So, embedding data works nicely for many cases but it is clear that there are scenarios when denormalizing your data will cause more problems than it is worth.</span></span> <span data-ttu-id="2a136-162">Cosa si può fare dunque?</span><span class="sxs-lookup"><span data-stu-id="2a136-162">So what do we do now?</span></span> 

<span data-ttu-id="2a136-163">Database relazionali non sono unico luogo hello in cui è possibile creare relazioni tra entità.</span><span class="sxs-lookup"><span data-stu-id="2a136-163">Relational databases are not hello only place where you can create relationships between entities.</span></span> <span data-ttu-id="2a136-164">In un database di documenti è possibile disporre di informazioni in un documento che effettivamente si riferisce toodata in altri documenti.</span><span class="sxs-lookup"><span data-stu-id="2a136-164">In a document database you can have information in one document that actually relates toodata in other documents.</span></span> <span data-ttu-id="2a136-165">A questo punto, sono non, promuovendo anche un minuto è creare sistemi che sarebbero migliori tooa adatto di database relazionale nel database di Azure Cosmos o qualsiasi altro database di documento, ma relazioni semplici sono supportate e possono essere molto utili.</span><span class="sxs-lookup"><span data-stu-id="2a136-165">Now, I am not advocating for even one minute that we build systems that would be better suited tooa relational database in Azure Cosmos DB, or any other document database, but simple relationships are fine and can be very useful.</span></span> 

<span data-ttu-id="2a136-166">In hello JSON seguente è stato scelto toouse hello ad esempio un portafoglio di titoli da versioni precedenti ma questa volta che viene fatto riferimento toohello magazzino nel portfolio di hello anziché incorporarlo.</span><span class="sxs-lookup"><span data-stu-id="2a136-166">In hello JSON below we chose toouse hello example of a stock portfolio from earlier but this time we refer toohello stock item on hello portfolio instead of embedding it.</span></span> <span data-ttu-id="2a136-167">In questo modo, quando in magazzino hello cambiano frequentemente in tutta hello giorno hello solo documento toobe aggiornato è documento azionari singolo hello.</span><span class="sxs-lookup"><span data-stu-id="2a136-167">This way, when hello stock item changes frequently throughout hello day hello only document that needs toobe updated is hello single stock document.</span></span> 

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


<span data-ttu-id="2a136-168">Un approccio toothis immediato svantaggio, tuttavia è se l'applicazione è necessario tooshow informazioni ogni titolo che viene mantenuto per la visualizzazione di raccolte di progetti di una persona; In questo caso sarà necessario toomake più trip toohello tooload hello informazioni sul database per ogni documento predefinita.</span><span class="sxs-lookup"><span data-stu-id="2a136-168">An immediate downside toothis approach though is if your application is required tooshow information about each stock that is held when displaying a person's portfolio; in this case you would need toomake multiple trips toohello database tooload hello information for each stock document.</span></span> <span data-ttu-id="2a136-169">Di seguito sono stati apportati efficienza di hello tooimprove una decisione di operazioni di scrittura, che si verifica frequentemente durante il giorno hello, ma anche a sua volta su hello operazioni potenzialmente con un impatto minore sulle prestazioni di hello questo particolare sistema di lettura.</span><span class="sxs-lookup"><span data-stu-id="2a136-169">Here we've made a decision tooimprove hello efficiency of write operations, which happen frequently throughout hello day, but in turn compromised on hello read operations that potentially have less impact on hello performance of this particular system.</span></span>

> [!NOTE]
> <span data-ttu-id="2a136-170">I modelli di dati normalizzato **può richiedere più round trip** toohello server.</span><span class="sxs-lookup"><span data-stu-id="2a136-170">Normalized data models **can require more round trips** toohello server.</span></span>
> 
> 

### <a name="what-about-foreign-keys"></a><span data-ttu-id="2a136-171">Chiavi esterne</span><span class="sxs-lookup"><span data-stu-id="2a136-171">What about foreign keys?</span></span>
<span data-ttu-id="2a136-172">Poiché attualmente non è disponibile alcun concetto di un vincolo, chiave esterna o in caso contrario, tutte le relazioni tra i documenti contenenti nei documenti sono effettivamente "punti deboli" e non verranno verificate dal database hello stesso.</span><span class="sxs-lookup"><span data-stu-id="2a136-172">Because there is currently no concept of a constraint, foreign-key or otherwise, any inter-document relationships that you have in documents are effectively "weak links" and will not be verified by hello database itself.</span></span> <span data-ttu-id="2a136-173">Se si desidera tooensure che hello dati che fa riferimento un documento tooactually esista, quindi è necessario toodo questo nell'applicazione o tramite l'utilizzo di hello del lato server trigger o stored procedure nel database di Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2a136-173">If you want tooensure that hello data a document is referring tooactually exists, then you need toodo this in your application, or through hello use of server-side triggers or stored procedures on Azure Cosmos DB.</span></span>

### <a name="when-tooreference"></a><span data-ttu-id="2a136-174">Quando tooreference</span><span class="sxs-lookup"><span data-stu-id="2a136-174">When tooreference</span></span>
<span data-ttu-id="2a136-175">In generale, usare i modelli di dati denormalizzati quando:</span><span class="sxs-lookup"><span data-stu-id="2a136-175">In general, use normalized data models when:</span></span>

* <span data-ttu-id="2a136-176">Si rappresentano relazioni **uno a molti** .</span><span class="sxs-lookup"><span data-stu-id="2a136-176">Representing **one-to-many** relationships.</span></span>
* <span data-ttu-id="2a136-177">Si rappresentano relazioni **molti a molti** .</span><span class="sxs-lookup"><span data-stu-id="2a136-177">Representing **many-to-many** relationships.</span></span>
* <span data-ttu-id="2a136-178">I dati correlati **cambiano spesso**.</span><span class="sxs-lookup"><span data-stu-id="2a136-178">Related data **changes frequently**.</span></span>
* <span data-ttu-id="2a136-179">È possibile che i dati a cui si fa riferimento **non siamo limitati**.</span><span class="sxs-lookup"><span data-stu-id="2a136-179">Referenced data could be **unbounded**.</span></span>

> [!NOTE]
> <span data-ttu-id="2a136-180">La normalizzazione offre di solito migliori prestazioni di **scrittura** .</span><span class="sxs-lookup"><span data-stu-id="2a136-180">Typically normalizing provides better **write** performance.</span></span>
> 
> 

### <a name="where-do-i-put-hello-relationship"></a><span data-ttu-id="2a136-181">Posizionamento di relazione hello</span><span class="sxs-lookup"><span data-stu-id="2a136-181">Where do I put hello relationship?</span></span>
<span data-ttu-id="2a136-182">aumento delle dimensioni Hello di relazione hello consentono di determinare in quale riferimento hello toostore del documento.</span><span class="sxs-lookup"><span data-stu-id="2a136-182">hello growth of hello relationship will help determine in which document toostore hello reference.</span></span>

<span data-ttu-id="2a136-183">Se si esamina hello JSON seguente che modella i server di pubblicazione e la documentazione.</span><span class="sxs-lookup"><span data-stu-id="2a136-183">If we look at hello JSON below that models publishers and books.</span></span>

    Publisher document:
    {
        "id": "mspress",
        "name": "Microsoft Press",
        "books": [ 1, 2, 3, ..., 100, ..., 1000]
    }

    Book documents:
    {"id": "1", "name": "Azure Cosmos DB 101" }
    {"id": "2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "3", "name": "Taking over hello world one JSON doc at a time" }
    ...
    {"id": "100", "name": "Learn about Azure Cosmos DB" }
    ...
    {"id": "1000", "name": "Deep Dive in tooAzure Cosmos DB" }

<span data-ttu-id="2a136-184">Se il numero di hello di libri hello al server di pubblicazione è ridotto con crescita limitata, può risultare utile la memorizzazione dei hello libro di riferimento interno hello publisher documento.</span><span class="sxs-lookup"><span data-stu-id="2a136-184">If hello number of hello books per publisher is small with limited growth, then storing hello book reference inside hello publisher document may be useful.</span></span> <span data-ttu-id="2a136-185">Tuttavia, se il numero di hello di documentazione per ogni server di pubblicazione è non associato, questo modello di dati potrebbe causare toomutable, aumento delle dimensioni di matrici, come hello esempio server di pubblicazione nel documento precedente.</span><span class="sxs-lookup"><span data-stu-id="2a136-185">However, if hello number of books per publisher is unbounded, then this data model would lead toomutable, growing arrays, as in hello example publisher document above.</span></span> 

<span data-ttu-id="2a136-186">Cambio di diversi elementi un bit sarebbe risultato in un modello che rappresenta ancora hello stessi dati ma ora consente di evitare questi grandi raccolte modificabile.</span><span class="sxs-lookup"><span data-stu-id="2a136-186">Switching things around a bit would result in a model that still represents hello same data but now avoids these large mutable collections.</span></span>

    Publisher document: 
    {
        "id": "mspress",
        "name": "Microsoft Press"
    }

    Book documents: 
    {"id": "1","name": "Azure Cosmos DB 101", "pub-id": "mspress"}
    {"id": "2","name": "Azure Cosmos DB for RDBMS Users", "pub-id": "mspress"}
    {"id": "3","name": "Taking over hello world one JSON doc at a time"}
    ...
    {"id": "100","name": "Learn about Azure Cosmos DB", "pub-id": "mspress"}
    ...
    {"id": "1000","name": "Deep Dive in tooAzure Cosmos DB", "pub-id": "mspress"}

<span data-ttu-id="2a136-187">In hello esempio precedente, è stato eliminato hello unbounded insieme nel documento di publisher hello.</span><span class="sxs-lookup"><span data-stu-id="2a136-187">In hello above example, we have dropped hello unbounded collection on hello publisher document.</span></span> <span data-ttu-id="2a136-188">Invece è disponibile solo un server di pubblicazione di toohello riferimento nel documento di ciascun libro.</span><span class="sxs-lookup"><span data-stu-id="2a136-188">Instead we just have a a reference toohello publisher on each book document.</span></span>

### <a name="how-do-i-model-manymany-relationships"></a><span data-ttu-id="2a136-189">Come modellare le relazioni many:many?</span><span class="sxs-lookup"><span data-stu-id="2a136-189">How do I model many:many relationships?</span></span>
<span data-ttu-id="2a136-190">In un database relazionale le relazioni *molti a molti* vengono spesso modellate con le tabelle join, che creano un join dei record delle altre tabelle.</span><span class="sxs-lookup"><span data-stu-id="2a136-190">In a relational database *many:many* relationships are often modeled with join tables, which just join records from other tables together.</span></span> 

![Unione di tabelle](./media/documentdb-modeling-data/join-table.png)

<span data-ttu-id="2a136-192">Potrebbe essere tentati tooreplicate hello stessa operazione usando i documenti e producono un modello di dati che sembra simile toohello seguente.</span><span class="sxs-lookup"><span data-stu-id="2a136-192">You might be tempted tooreplicate hello same thing using documents and produce a data model that looks similar toohello following.</span></span>

    Author documents: 
    {"id": "a1", "name": "Thomas Andersen" }
    {"id": "a2", "name": "William Wakefield" }

    Book documents:
    {"id": "b1", "name": "Azure Cosmos DB 101" }
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users" }
    {"id": "b3", "name": "Taking over hello world one JSON doc at a time" }
    {"id": "b4", "name": "Learn about Azure Cosmos DB" }
    {"id": "b5", "name": "Deep Dive in tooAzure Cosmos DB" }

    Joining documents: 
    {"authorId": "a1", "bookId": "b1" }
    {"authorId": "a2", "bookId": "b1" }
    {"authorId": "a1", "bookId": "b2" }
    {"authorId": "a1", "bookId": "b3" }

<span data-ttu-id="2a136-193">Funzionerebbe,</span><span class="sxs-lookup"><span data-stu-id="2a136-193">This would work.</span></span> <span data-ttu-id="2a136-194">Tuttavia, il caricamento di entrambi un autore e la documentazione o il caricamento di un libro con autore, sempre richiede almeno due query aggiuntive hello database.</span><span class="sxs-lookup"><span data-stu-id="2a136-194">However, loading either an author with their books, or loading a book with its author, would always require at least two additional queries against hello database.</span></span> <span data-ttu-id="2a136-195">Unione di documenti e quindi un'altra query toofetch hello documento effettivo da unire in join toohello di una query.</span><span class="sxs-lookup"><span data-stu-id="2a136-195">One query toohello joining document and then another query toofetch hello actual document being joined.</span></span> 

<span data-ttu-id="2a136-196">Se la tabella join si limita a incollare insieme due gruppi di dati, allora perché non eliminarla del tutto?</span><span class="sxs-lookup"><span data-stu-id="2a136-196">If all this join table is doing is gluing together two pieces of data, then why not drop it completely?</span></span>
<span data-ttu-id="2a136-197">Prendere in considerazione i seguenti hello.</span><span class="sxs-lookup"><span data-stu-id="2a136-197">Consider hello following.</span></span>

    Author documents:
    {"id": "a1", "name": "Thomas Andersen", "books": ["b1, "b2", "b3"]}
    {"id": "a2", "name": "William Wakefield", "books": ["b1", "b4"]}

    Book documents: 
    {"id": "b1", "name": "Azure Cosmos DB 101", "authors": ["a1", "a2"]}
    {"id": "b2", "name": "Azure Cosmos DB for RDBMS Users", "authors": ["a1"]}
    {"id": "b3", "name": "Learn about Azure Cosmos DB", "authors": ["a1"]}
    {"id": "b4", "name": "Deep Dive in tooAzure Cosmos DB", "authors": ["a2"]}

<span data-ttu-id="2a136-198">A questo punto, se ci fosse un autore, posso sapere immediatamente quali libri che hanno scritto e viceversa se è stato caricato un documento di libro SO ID hello degli autori hello.</span><span class="sxs-lookup"><span data-stu-id="2a136-198">Now, if I had an author, I immediately know which books they have written, and conversely if I had a book document loaded I would know hello ids of hello author(s).</span></span> <span data-ttu-id="2a136-199">Ciò consente di risparmiare intermediario query sulla tabella di join hello riducendo il numero di hello del server dell'applicazione è toomake di round trip.</span><span class="sxs-lookup"><span data-stu-id="2a136-199">This saves that intermediary query against hello join table reducing hello number of server round trips your application has toomake.</span></span> 

## <span data-ttu-id="2a136-200"><a id="WrapUp"></a>Modelli di dati ibridi</span><span class="sxs-lookup"><span data-stu-id="2a136-200"><a id="WrapUp"></a>Hybrid data models</span></span>
<span data-ttu-id="2a136-201">Come si è visto, sia l'incorporamento (o denormalizzazione) che il riferimento (o normalizzazione) ai dati presentano vantaggi e compromessi.</span><span class="sxs-lookup"><span data-stu-id="2a136-201">We've now looked embedding (or denormalizing) and referencing (or normalizing) data, each have their upsides and each have compromises as we have seen.</span></span> 

<span data-ttu-id="2a136-202">L'operazione non sempre disporre di un toobe o, non essere toomix impaurito operazioni backup a breve.</span><span class="sxs-lookup"><span data-stu-id="2a136-202">It doesn't always have toobe either or, don't be scared toomix things up a little.</span></span> 

<span data-ttu-id="2a136-203">In base a modelli di utilizzo specifico e i carichi di lavoro può accadere in combinazione incorporata dell'applicazione e dati di riferimento ha senso e Impossibile logica dell'applicazione responsabile toosimpler con server meno round trip pur mantenendo un buon livello di prestazioni .</span><span class="sxs-lookup"><span data-stu-id="2a136-203">Based on your application's specific usage patterns and workloads there may be cases where mixing embedded and referenced data makes sense and could lead toosimpler application logic with fewer server round trips while still maintaining a good level of performance.</span></span>

<span data-ttu-id="2a136-204">Prendere in considerazione hello seguente JSON.</span><span class="sxs-lookup"><span data-stu-id="2a136-204">Consider hello following JSON.</span></span> 

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

<span data-ttu-id="2a136-205">Qui è stata seguita (principalmente) modello incorporato hello, in cui i dati da altre entità sono incorporati nel documento di primo livello hello, ma fa riferimento ad altri dati.</span><span class="sxs-lookup"><span data-stu-id="2a136-205">Here we've (mostly) followed hello embedded model, where data from other entities are embedded in hello top-level document, but other data is referenced.</span></span> 

<span data-ttu-id="2a136-206">Se si esamina il documento di libro hello, possiamo vedere alcuni interessanti campi quando si esamina la matrice hello degli autori.</span><span class="sxs-lookup"><span data-stu-id="2a136-206">If you look at hello book document, we can see a few interesting fields when we look at hello array of authors.</span></span> <span data-ttu-id="2a136-207">È presente un *id* campo campo hello utilizziamo documento di autore di toorefer tooan indietro, procedura standard in un modello normalizzato, ma è anche avere *nome* e *thumbnailUrl*.</span><span class="sxs-lookup"><span data-stu-id="2a136-207">There is an *id* field which is hello field we use toorefer back tooan author document, standard practice in a normalized model, but then we also have *name* and *thumbnailUrl*.</span></span> <span data-ttu-id="2a136-208">È possibile avere solo bloccato con *id* e ha lasciato tooget applicazione hello eventuali informazioni aggiuntive necessarie dal documento di autore rispettivi hello utilizzando hello "collegamento", ma poiché l'applicazione consente di visualizzare il nome dell'autore hello e un immagine di anteprima con ogni libro visualizzato per salvare un server di andata e ritorno toohello per ogni libro in un elenco da denormalizzazione **alcuni** dati da un autore hello.</span><span class="sxs-lookup"><span data-stu-id="2a136-208">We could've just stuck with *id* and left hello application tooget any additional information it needed from hello respective author document using hello "link", but because our application displays hello author's name and a thumbnail picture with every book displayed we can save a round trip toohello server per book in a list by denormalizing **some** data from hello author.</span></span>

<span data-ttu-id="2a136-209">Assicurarsi che, se il nome dell'autore hello modificato o volevano tooupdate le foto sono toogo un aggiornamento ogni libro viene sempre la pubblicazione, ma per l'applicazione, in base a ipotesi di hello che gli autori di non modificare i relativi nomi, molto spesso, si tratta di una progettazione accettabile decisione.</span><span class="sxs-lookup"><span data-stu-id="2a136-209">Sure, if hello author's name changed or they wanted tooupdate their photo we'd have toogo an update every book they ever published but for our application, based on hello assumption that authors don't change their names very often, this is an acceptable design decision.</span></span>  

<span data-ttu-id="2a136-210">Nell'esempio hello esistono **pre-calcolate aggregazioni** valori toosave costosa l'elaborazione in un'operazione di lettura.</span><span class="sxs-lookup"><span data-stu-id="2a136-210">In hello example there are **pre-calculated aggregates** values toosave expensive processing on a read operation.</span></span> <span data-ttu-id="2a136-211">Nell'esempio hello, alcuni dati hello incorporati nel documento di autore hello sono dati che viene calcolati in fase di esecuzione.</span><span class="sxs-lookup"><span data-stu-id="2a136-211">In hello example, some of hello data embedded in hello author document is data that is calculated at run-time.</span></span> <span data-ttu-id="2a136-212">Ogni volta che un nuovo libro viene pubblicato, viene creato un documento di libro **e** campo countOfBooks hello è impostato un valore tooa calcolato in base al numero di hello libro di documenti esistenti per un determinato autore.</span><span class="sxs-lookup"><span data-stu-id="2a136-212">Every time a new book is published, a book document is created **and** hello countOfBooks field is set tooa calculated value based on hello number of book documents that exist for a particular author.</span></span> <span data-ttu-id="2a136-213">Questa ottimizzazione sono utili nei sistemi pesanti letti in cui che possiamo permetterci toodo calcoli su operazioni di scrittura in ordine toooptimize legge.</span><span class="sxs-lookup"><span data-stu-id="2a136-213">This optimization would be good in read heavy systems where we can afford toodo computations on writes in order toooptimize reads.</span></span>

<span data-ttu-id="2a136-214">Hello toohave possibilità è reso possibile un modello con campi pre-calcolati perché supporta Azure Cosmos DB **transazioni più documenti**.</span><span class="sxs-lookup"><span data-stu-id="2a136-214">hello ability toohave a model with pre-calculated fields is made possible because Azure Cosmos DB supports **multi-document transactions**.</span></span> <span data-ttu-id="2a136-215">Molti archivi NoSQL non possono eseguire transazioni in tutti i documenti e pertanto sostenere decisioni di progettazione, ad esempio "sempre incorpora tutti gli elementi", a causa di limitazione toothis.</span><span class="sxs-lookup"><span data-stu-id="2a136-215">Many NoSQL stores cannot do transactions across documents and therefore advocate design decisions, such as "always embed everything", due toothis limitation.</span></span> <span data-ttu-id="2a136-216">Con Azure Cosmos DB è possibile usare trigger lato server, o stored procedure, che inseriscono i libri e aggiornano gli autori in una sola transazione ACID.</span><span class="sxs-lookup"><span data-stu-id="2a136-216">With Azure Cosmos DB, you can use server-side triggers, or stored procedures, that insert books and update authors all within an ACID transaction.</span></span> <span data-ttu-id="2a136-217">Ora non sono presenti **hanno** tooembed tutti gli elementi di tooone documento toobe sufficiente Assicurarsi che i dati rimangono coerenti.</span><span class="sxs-lookup"><span data-stu-id="2a136-217">Now you don't **have** tooembed everything in tooone document just toobe sure that your data remains consistent.</span></span>

## <span data-ttu-id="2a136-218"><a name="NextSteps"></a>Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2a136-218"><a name="NextSteps"></a>Next steps</span></span>
<span data-ttu-id="2a136-219">informazioni chiave più grande di Hello in questo articolo è toounderstand che modellazione dei dati in un mondo privi di schema sono importanti che mai.</span><span class="sxs-lookup"><span data-stu-id="2a136-219">hello biggest takeaways from this article is toounderstand that data modeling in a schema-free world is just as important as ever.</span></span> 

<span data-ttu-id="2a136-220">Come non è presente alcun toorepresent modo solo una parte dei dati in una schermata, non è toomodel alcun modo singolo i dati.</span><span class="sxs-lookup"><span data-stu-id="2a136-220">Just as there is no single way toorepresent a piece of data on a screen, there is no single way toomodel your data.</span></span> <span data-ttu-id="2a136-221">È necessario toounderstand l'applicazione e come verrà generato, utilizzare ed elaborare dati hello.</span><span class="sxs-lookup"><span data-stu-id="2a136-221">You need toounderstand your application and how it will produce, consume, and process hello data.</span></span> <span data-ttu-id="2a136-222">Quindi, applicando alcune hello linee guida riportate qui è possono impostare sulla creazione di un modello che risponde alle esigenze immediate hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2a136-222">Then, by applying some of hello guidelines presented here you can set about creating a model that addresses hello immediate needs of your application.</span></span> <span data-ttu-id="2a136-223">Quando le applicazioni devono toochange, è possibile sfruttare la flessibilità di hello di un tooembrace privi di schema di database che modificano ed evolvere facilmente il modello di dati.</span><span class="sxs-lookup"><span data-stu-id="2a136-223">When your applications need toochange, you can leverage hello flexibility of a schema-free database tooembrace that change and evolve your data model easily.</span></span> 

<span data-ttu-id="2a136-224">toolearn ulteriori informazioni su Azure Cosmos DB, fare riferimento del servizio toohello [documentazione](https://azure.microsoft.com/documentation/services/cosmos-db/) pagina.</span><span class="sxs-lookup"><span data-stu-id="2a136-224">toolearn more about Azure Cosmos DB, refer toohello service's [documentation](https://azure.microsoft.com/documentation/services/cosmos-db/) page.</span></span> 

<span data-ttu-id="2a136-225">toounderstand come tooshard i dati tra più partizioni, fare riferimento troppo[partizionamento dei dati nel database di Azure Cosmos](documentdb-partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="2a136-225">toounderstand how tooshard your data across multiple partitions, refer too[Partitioning Data in Azure Cosmos DB](documentdb-partition-data.md).</span></span> 
