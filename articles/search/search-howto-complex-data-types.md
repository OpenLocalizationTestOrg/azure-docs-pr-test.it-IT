---
title: tipi di dati complessi toomodel aaaHow in ricerca di Azure | Documenti Microsoft
description: "È possibile modellare strutture di dati annidate o gerarchiche in un indice di Ricerca di Azure usando un set di righe bidimensionale e il tipo di dati Collection."
services: search
documentationcenter: 
author: LiamCa
manager: pablocas
editor: 
tags: complex data types; compound data types; aggregate data types
ms.assetid: e4bf86b4-497a-4179-b09f-c1b56c3c0bb2
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/01/2017
ms.author: liamca
ms.openlocfilehash: b330c5b322f4f33123a454be11733b977684b9e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toomodel-complex-data-types-in-azure-search"></a><span data-ttu-id="93cd8-103">Come tipi di dati complessi toomodel in ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="93cd8-103">How toomodel complex data types in Azure Search</span></span>
<span data-ttu-id="93cd8-104">Set di dati esterni utilizzati toopopulate a volte, un indice di ricerca di Azure includono le sottostrutture gerarchiche o annidate che suddivide accuratamente in un set di righe tabulare.</span><span class="sxs-lookup"><span data-stu-id="93cd8-104">External datasets used toopopulate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="93cd8-105">Gli esempi di strutture di questo tipo possono includere più ubicazioni e numeri di telefono per un singolo cliente, più colori e dimensioni per un singolo SKU, più autori di un singolo libro e così via.</span><span class="sxs-lookup"><span data-stu-id="93cd8-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="93cd8-106">In termini di modellazione, è possibile visualizzare queste strutture di cui tooas *tipi di dati complessi*, *tipi di dati composti*, *tipi di dati compositi*, o *aggregazione tipi di dati*, tooname qualche.</span><span class="sxs-lookup"><span data-stu-id="93cd8-106">In modeling terms, you might see these structures referred tooas *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, tooname a few.</span></span>

<span data-ttu-id="93cd8-107">Tipi di dati complessi non sono supportati in modo nativo in ricerca di Azure, ma una soluzione si basa sulla collaudata include fasi di conversione struttura hello e quindi utilizzando un **raccolta** tooreconstitute struttura interna di hello del tipo di dati.</span><span class="sxs-lookup"><span data-stu-id="93cd8-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening hello structure and then using a **Collection** data type tooreconstitute hello interior structure.</span></span> <span data-ttu-id="93cd8-108">Seguendo tecnica hello descritta in questo articolo gli toobe contenuto hello avanzata, con facet, filtrati e ordinati.</span><span class="sxs-lookup"><span data-stu-id="93cd8-108">Following hello technique described in this article allows hello content toobe searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="93cd8-109">Esempio di struttura di dati complessa</span><span class="sxs-lookup"><span data-stu-id="93cd8-109">Example of a complex data structure</span></span>
<span data-ttu-id="93cd8-110">Dati hello in questione si trovano in genere, come un set di documenti JSON o XML o come elementi in un archivio NoSQL, ad esempio Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="93cd8-110">Typically, hello data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="93cd8-111">Richiesta di hello strutturalmente, deriva dalla presenza di più elementi figlio che devono toobe la ricerca e filtrati.</span><span class="sxs-lookup"><span data-stu-id="93cd8-111">Structurally, hello challenge stems from having multiple child items that need toobe searched and filtered.</span></span>  <span data-ttu-id="93cd8-112">Come punto di partenza per illustrare la soluzione alternativa hello, richiedere hello seguente documento JSON che elenca un set di contatti, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="93cd8-112">As a starting point for illustrating hello workaround, take hello following JSON document that lists a set of contacts as an example:</span></span>

~~~~~
[
  {
    "id": "1",
    "name": "John Smith",
    "company": "Adventureworks",
    "locations": [
      {
        "id": "1",
        "description": "Adventureworks Headquarters"
      },
      {
        "id": "2",
        "description": "Home Office"
      }
    ]
  }, 
  {
    "id": "2",
    "name": "Jen Campbell",
    "company": "Northwind",
    "locations": [
      {
        "id": "3",
        "description": "Northwind Headquarter"
      },
      {
        "id": "4",
        "description": "Home Office"
      }
    ]
}]
~~~~~

<span data-ttu-id="93cd8-113">Mentre i campi di hello denominato 'id', 'name' e 'società' è possibile associare facilmente uno a uno come campi all'interno di un indice di ricerca di Azure, campo 'locations' hello contiene una matrice di percorsi, avere sia un set di ID di posizione, nonché le descrizioni di percorso.</span><span class="sxs-lookup"><span data-stu-id="93cd8-113">While hello fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, hello ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="93cd8-114">Dato che ricerca di Azure non dispone di un tipo di dati che supporta questa caratteristica, è necessaria toomodel un modo diverso in ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="93cd8-114">Given that Azure Search does not have a data type that supports this, we need a different way toomodel this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="93cd8-115">Questa tecnica è descritto da Kirk Evans in un post di blog [l'indicizzazione di DocumentDB con ricerca di Azure](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), che illustra una tecnica denominata "conversione dati hello", in base al quale è un campo denominato `locationsID` e `locationsDescription` che sono entrambi [raccolte](https://msdn.microsoft.com/library/azure/dn798938.aspx) (o una matrice di stringhe).</span><span class="sxs-lookup"><span data-stu-id="93cd8-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening hello data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-hello-array-into-individual-fields"></a><span data-ttu-id="93cd8-116">Parte 1: Convertire la matrice hello in singoli campi</span><span class="sxs-lookup"><span data-stu-id="93cd8-116">Part 1: Flatten hello array into individual fields</span></span>
<span data-ttu-id="93cd8-117">toocreate un indice di ricerca di Azure che consente di adattare questo set di dati, creare singoli campi per sottostruttura nidificata hello: `locationsID` e `locationsDescription` con un tipo di dati [raccolte](https://msdn.microsoft.com/library/azure/dn798938.aspx) (o una matrice di stringhe).</span><span class="sxs-lookup"><span data-stu-id="93cd8-117">toocreate an Azure Search index that accommodates this dataset, create individual fields for hello nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="93cd8-118">In questi campi è necessario indicizzare i valori hello '1' e '2' hello `locationsID` campo per i valori di John Smith e hello '3' & '4' in hello `locationsID` field per Jen Campbell.</span><span class="sxs-lookup"><span data-stu-id="93cd8-118">In these fields you would index hello values ‘1’ and ‘2’ into hello `locationsID` field for John Smith and hello values ‘3’ & ‘4’ into hello `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="93cd8-119">I dati in Ricerca di Azure si presenteranno come segue:</span><span class="sxs-lookup"><span data-stu-id="93cd8-119">Your data within Azure Search would look like this:</span></span> 

![Dati di esempio, 2 righe](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-hello-index-definition"></a><span data-ttu-id="93cd8-121">Parte 2: Aggiungere un campo di raccolta nella definizione dell'indice hello</span><span class="sxs-lookup"><span data-stu-id="93cd8-121">Part 2: Add a collection field in hello index definition</span></span>
<span data-ttu-id="93cd8-122">Nello schema di indice hello, definizioni di campo hello potrebbero apparire esempio toothis simile.</span><span class="sxs-lookup"><span data-stu-id="93cd8-122">In hello index schema, hello field definitions might look similar toothis example.</span></span>

~~~~
var index = new Index()
{
    Name = indexName,
    Fields = new[]
    {
        new Field("id", DataType.String) { IsKey = true },
        new Field("name", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("company", DataType.String) { IsSearchable = true, IsFilterable = false, IsSortable = false, IsFacetable = false },
        new Field("locationsId", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true },
        new Field("locationsDescription", DataType.Collection(DataType.String)) { IsSearchable = true, IsFilterable = true, IsFacetable = true }
    }
};
~~~~

## <a name="validate-search-behaviors-and-optionally-extend-hello-index"></a><span data-ttu-id="93cd8-123">Convalidare i comportamenti di ricerca e facoltativamente estendere hello indice</span><span class="sxs-lookup"><span data-stu-id="93cd8-123">Validate search behaviors and optionally extend hello index</span></span>
<span data-ttu-id="93cd8-124">Presupponendo che si indice creato hello e dati hello caricato, è ora possibile testare hello soluzione tooverify ricerca esecuzione delle query in set di dati hello.</span><span class="sxs-lookup"><span data-stu-id="93cd8-124">Assuming you created hello index and loaded hello data, you can now test hello solution tooverify search query execution against hello dataset.</span></span> <span data-ttu-id="93cd8-125">Ogni campo di tipo **raccolta** dovrà essere **ricercabile**, **filtrabile** e **con facet**.</span><span class="sxs-lookup"><span data-stu-id="93cd8-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="93cd8-126">Dovrebbe essere in grado di toorun query come:</span><span class="sxs-lookup"><span data-stu-id="93cd8-126">You should be able toorun queries like:</span></span>

* <span data-ttu-id="93cd8-127">Trovare tutte le persone che lavorano presso hello "Sede centrale Adventureworks".</span><span class="sxs-lookup"><span data-stu-id="93cd8-127">Find all people who work at hello ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="93cd8-128">Ottenere un conteggio del numero di hello di persone che lavorano in un ufficio di Home' '.</span><span class="sxs-lookup"><span data-stu-id="93cd8-128">Get a count of hello number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="93cd8-129">Delle persone hello che lavorano in un "Home Office", indicano quali altri uffici funzionano insieme a un numero di persone hello in ogni posizione.</span><span class="sxs-lookup"><span data-stu-id="93cd8-129">Of hello people who work at a ‘Home Office’, show what other offices they work along with a count of hello people in each location.</span></span>  

<span data-ttu-id="93cd8-130">In questa tecnica rientra distanza è quando è necessario toodo una ricerca che combina id percorso hello nonché a descrizione dell'ubicazione hello.</span><span class="sxs-lookup"><span data-stu-id="93cd8-130">Where this technique falls apart is when you need toodo a search that combines both hello location id as well as hello location description.</span></span> <span data-ttu-id="93cd8-131">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="93cd8-131">For example:</span></span>

* <span data-ttu-id="93cd8-132">Trovare tutte le persone con "Home Office" E con ID ubicazione 4.</span><span class="sxs-lookup"><span data-stu-id="93cd8-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="93cd8-133">Se si ricorda il contenuto originale di hello simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="93cd8-133">If you recall hello original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="93cd8-134">Tuttavia, dopo che è stato suddiviso dati hello in campi separati, non esiste alcun modo di sapere se hello Home Office per Jen Campbell si riferisce troppo`locationsID 3` o `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="93cd8-134">However, now that we have separated hello data into separate fields, we have no way of knowing if hello Home Office for Jen Campbell relates too`locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="93cd8-135">toohandle questo caso, definire un altro campo nell'indice hello che tutti i dati di hello combina in un'unica raccolta.</span><span class="sxs-lookup"><span data-stu-id="93cd8-135">toohandle this case, define another field in hello index that combines all of hello data into a single collection.</span></span>  <span data-ttu-id="93cd8-136">Per questo esempio, questo campo verrà chiamata `locationsCombined` e si separano contenuto hello con un `||` anche se è possibile scegliere qualsiasi separatore che si ritiene sarebbe un set univoco di caratteri per il contenuto.</span><span class="sxs-lookup"><span data-stu-id="93cd8-136">For our example, we will call this field `locationsCombined` and we will separate hello content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="93cd8-137">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="93cd8-137">For example:</span></span> 

![Dati di esempio, 2 righe con separatore](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="93cd8-139">Usando il campo `locationsCombined` , è ora possibile supportare query aggiuntive, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="93cd8-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="93cd8-140">Visualizzare un conteggio delle persone che lavorano in "Home Office" con ID ubicazione "4".</span><span class="sxs-lookup"><span data-stu-id="93cd8-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="93cd8-141">Cercare le persone che lavorano in "Home Office" con ID ubicazione "4".</span><span class="sxs-lookup"><span data-stu-id="93cd8-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="93cd8-142">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="93cd8-142">Limitations</span></span>
<span data-ttu-id="93cd8-143">Questa tecnica è utile per diversi scenari, ma non è applicabile in tutti i casi.</span><span class="sxs-lookup"><span data-stu-id="93cd8-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="93cd8-144">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="93cd8-144">For example:</span></span>

1. <span data-ttu-id="93cd8-145">Se si dispone di un set statico di campi nel tipo di dati complessi e si è verificato alcun toomap modo tutte le possibili hello tipi tooa singolo campo.</span><span class="sxs-lookup"><span data-stu-id="93cd8-145">If you do not have a static set of fields in your complex data type and there was no way toomap all hello possible types tooa single field.</span></span> 
2. <span data-ttu-id="93cd8-146">L'aggiornamento degli oggetti annidato hello richiede toodetermine alcune operazioni aggiuntive esattamente cosa toobe aggiornato nell'indice di ricerca di Azure hello</span><span class="sxs-lookup"><span data-stu-id="93cd8-146">Updating hello nested objects requires some extra work toodetermine exactly what needs toobe updated in hello Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="93cd8-147">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="93cd8-147">Sample code</span></span>
<span data-ttu-id="93cd8-148">È possibile vedere un esempio sulla configurazione tooindex un complessi dati JSON in ricerca di Azure ed eseguire un numero di query su questo set di dati in questo [repository GitHub](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="93cd8-148">You can see an example on how tooindex a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="93cd8-149">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="93cd8-149">Next step</span></span>
<span data-ttu-id="93cd8-150">[Voto per il supporto nativo per i tipi di dati complessi](https://feedback.azure.com/forums/263029-azure-search) pagina hello UserVoice di ricerca di Azure e fornire qualsiasi input aggiuntivo che si desidera tooconsider riguardanti l'implementazione delle funzionalità.</span><span class="sxs-lookup"><span data-stu-id="93cd8-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on hello Azure Search UserVoice page and provide any additional input that you’d like us tooconsider regarding feature implementation.</span></span> <span data-ttu-id="93cd8-151">È inoltre possibile entrare toome direttamente su Twitter in @liamca.</span><span class="sxs-lookup"><span data-stu-id="93cd8-151">You can also reach out toome directly on Twitter at @liamca.</span></span>

