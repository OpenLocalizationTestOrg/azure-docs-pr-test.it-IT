---
title: Come modellare tipi di dati complessi in Ricerca di Azure | Documentazione Microsoft
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
ms.openlocfilehash: d576fd7bb267ae7a100589413185b595e3b2be42
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-model-complex-data-types-in-azure-search"></a><span data-ttu-id="c6a4a-103">Come modellare tipi di dati complessi in Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="c6a4a-103">How to model complex data types in Azure Search</span></span>
<span data-ttu-id="c6a4a-104">I set di dati esterni usati per popolare un indice di Ricerca di Azure includono talvolta sottostrutture gerarchiche o annidate che non vengono suddivise con precisione in un set di righe tabulare.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-104">External datasets used to populate an Azure Search index sometimes include hierarchical or nested substructures that do not break down neatly into a tabular rowset.</span></span> <span data-ttu-id="c6a4a-105">Gli esempi di strutture di questo tipo possono includere più ubicazioni e numeri di telefono per un singolo cliente, più colori e dimensioni per un singolo SKU, più autori di un singolo libro e così via.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-105">Examples of such structures might include multiple locations and phone numbers for a single customer, multiple colors and sizes for a single SKU, multiple authors of a single book, and so on.</span></span> <span data-ttu-id="c6a4a-106">In termini di modellazione, queste strutture possono essere definite, ad esempio, *tipi di dati complessi*, *tipi di dati composti*, *tipi di dati compositi* o *tipi di dati aggregati*.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-106">In modeling terms, you might see these structures referred to as *complex data types*, *compound data types*, *composite data types*, or *aggregate data types*, to name a few.</span></span>

<span data-ttu-id="c6a4a-107">Ricerca di Azure non offre supporto nativo per i tipi di dati complessi. Una soluzione alternativa collaudata include tuttavia un processo in due passaggi con cui la struttura viene resa flat e quindi viene usato un tipo di dati **Collection** per ricostituire la struttura interna.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-107">Complex data types are not natively supported in Azure Search, but a proven workaround includes a two-step process of flattening the structure and then using a **Collection** data type to reconstitute the interior structure.</span></span> <span data-ttu-id="c6a4a-108">Seguendo la tecnica descritta in questo articolo, il contenuto risulta disponibile per l'esecuzione di ricerche, facet, l'applicazione di filtri e l'ordinamento.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-108">Following the technique described in this article allows the content to be searched, faceted, filtered, and sorted.</span></span>

## <a name="example-of-a-complex-data-structure"></a><span data-ttu-id="c6a4a-109">Esempio di struttura di dati complessa</span><span class="sxs-lookup"><span data-stu-id="c6a4a-109">Example of a complex data structure</span></span>
<span data-ttu-id="c6a4a-110">I dati in questione si trovano in genere come set di documenti JSON o XML oppure come elementi di un archivio NoSQL, ad esempio Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-110">Typically, the data in question resides as a set of JSON or XML documents, or as items in a NoSQL store such as Azure Cosmos DB.</span></span> <span data-ttu-id="c6a4a-111">Strutturalmente, il problema deriva dalla presenza di più elementi figlio su cui è necessario eseguire ricerche e applicare filtri.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-111">Structurally, the challenge stems from having multiple child items that need to be searched and filtered.</span></span>  <span data-ttu-id="c6a4a-112">Come punto di partenza per illustrare la soluzione alternativa verrà usato il documento JSON seguente che elenca una serie di contatti di esempio:</span><span class="sxs-lookup"><span data-stu-id="c6a4a-112">As a starting point for illustrating the workaround, take the following JSON document that lists a set of contacts as an example:</span></span>

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

<span data-ttu-id="c6a4a-113">Mentre per i campi denominati "id", "name" e "company" è possibile eseguire facilmente il mapping uno-a-uno come campi in un indice di Ricerca di Azure, il campo "locations" contiene una matrice di ubicazioni che include sia un set di ID ubicazione sia le descrizioni delle ubicazioni.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-113">While the fields named ‘id’, ‘name’ and ‘company’ can easily be mapped one-to-one as fields within an Azure Search index, the ‘locations’ field contains an array of locations, having both a set of location IDs as well as location descriptions.</span></span> <span data-ttu-id="c6a4a-114">Dato che Ricerca di Azure non ha un tipo di dati che supporta questa caratteristica, è necessario modellare i dati in modo diverso in Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-114">Given that Azure Search does not have a data type that supports this, we need a different way to model this in Azure Search.</span></span> 

> [!NOTE]
> <span data-ttu-id="c6a4a-115">Questa tecnica è descritta anche da Kirk Evans nel post di blog [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/) (Indicizzazione di DocumentDB con Ricerca di Azure), che illustra una tecnica per rendere flat i dati e ottenere così un campo denominato `locationsID` e un campo `locationsDescription` che sono entrambi [raccolte](https://msdn.microsoft.com/library/azure/dn798938.aspx), ovvero una matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-115">This technique is also described by Kirk Evans in a blog post [Indexing DocumentDB with Azure Search](https://blogs.msdn.microsoft.com/kaevans/2015/03/09/indexing-documentdb-with-azure-seach/), which shows a technique called "flattening the data", whereby you would have a field called `locationsID` and `locationsDescription` that are both [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span>   
> 
> 

## <a name="part-1-flatten-the-array-into-individual-fields"></a><span data-ttu-id="c6a4a-116">Parte 1: Rendere flat la matrice convertendola in singoli campi</span><span class="sxs-lookup"><span data-stu-id="c6a4a-116">Part 1: Flatten the array into individual fields</span></span>
<span data-ttu-id="c6a4a-117">Per creare un indice di Ricerca di Azure appropriato per questo set di dati, creare singoli campi per la sottostruttura annidata, `locationsID` e `locationsDescription`, con il tipo di dati delle [raccolte](https://msdn.microsoft.com/library/azure/dn798938.aspx), ovvero una matrice di stringhe.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-117">To create an Azure Search index that accommodates this dataset, create individual fields for the nested substructure: `locationsID` and `locationsDescription` with a data type of [collections](https://msdn.microsoft.com/library/azure/dn798938.aspx) (or an array of strings).</span></span> <span data-ttu-id="c6a4a-118">In questi campi verranno indicizzati i valori "1" e "2" nel campo `locationsID` per John Smith e i valori "3" e "4" nel campo `locationsID` per Jen Campbell.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-118">In these fields you would index the values ‘1’ and ‘2’ into the `locationsID` field for John Smith and the values ‘3’ & ‘4’ into the `locationsID` field for Jen Campbell.</span></span>  

<span data-ttu-id="c6a4a-119">I dati in Ricerca di Azure si presenteranno come segue:</span><span class="sxs-lookup"><span data-stu-id="c6a4a-119">Your data within Azure Search would look like this:</span></span> 

![Dati di esempio, 2 righe](./media/search-howto-complex-data-types/sample-data.png)

## <a name="part-2-add-a-collection-field-in-the-index-definition"></a><span data-ttu-id="c6a4a-121">Parte 2: Aggiungere un campo di tipo raccolta nella definizione dell'indice</span><span class="sxs-lookup"><span data-stu-id="c6a4a-121">Part 2: Add a collection field in the index definition</span></span>
<span data-ttu-id="c6a4a-122">Nello schema dell'indice, le definizioni dei campi possono avere un aspetto simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-122">In the index schema, the field definitions might look similar to this example.</span></span>

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

## <a name="validate-search-behaviors-and-optionally-extend-the-index"></a><span data-ttu-id="c6a4a-123">Convalidare i comportamenti di ricerca ed estendere facoltativamente l'indice</span><span class="sxs-lookup"><span data-stu-id="c6a4a-123">Validate search behaviors and optionally extend the index</span></span>
<span data-ttu-id="c6a4a-124">Supponendo che l'indice sia stato creato e che i dati siano stati caricati, è ora possibile testare la soluzione per verificare l'esecuzione di query di ricerca sul set di dati.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-124">Assuming you created the index and loaded the data, you can now test the solution to verify search query execution against the dataset.</span></span> <span data-ttu-id="c6a4a-125">Ogni campo di tipo **raccolta** dovrà essere **ricercabile**, **filtrabile** e **con facet**.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-125">Each **collection** field should be **searchable**, **filterable** and **facetable**.</span></span> <span data-ttu-id="c6a4a-126">Dovrebbe essere possibile eseguire query come le seguenti:</span><span class="sxs-lookup"><span data-stu-id="c6a4a-126">You should be able to run queries like:</span></span>

* <span data-ttu-id="c6a4a-127">Trovare tutte le persone che lavorano presso "Adventureworks Headquarters".</span><span class="sxs-lookup"><span data-stu-id="c6a4a-127">Find all people who work at the ‘Adventureworks Headquarters’.</span></span>
* <span data-ttu-id="c6a4a-128">Ottenere il conteggio del numero di persone che lavorano in "Home Office".</span><span class="sxs-lookup"><span data-stu-id="c6a4a-128">Get a count of the number of people who work in a ‘Home Office’.</span></span>  
* <span data-ttu-id="c6a4a-129">In relazione alle persone che lavorano in "Home Office", visualizzare gli altri uffici in cui lavorano con un conteggio delle persone in ogni ubicazione.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-129">Of the people who work at a ‘Home Office’, show what other offices they work along with a count of the people in each location.</span></span>  

<span data-ttu-id="c6a4a-130">Questa tecnica si rivela inadeguata quando è necessario eseguire una ricerca che combina sia l'ID che la descrizione dell'ubicazione,</span><span class="sxs-lookup"><span data-stu-id="c6a4a-130">Where this technique falls apart is when you need to do a search that combines both the location id as well as the location description.</span></span> <span data-ttu-id="c6a4a-131">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c6a4a-131">For example:</span></span>

* <span data-ttu-id="c6a4a-132">Trovare tutte le persone con "Home Office" E con ID ubicazione 4.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-132">Find all people where they have a Home Office AND has a location ID of 4.</span></span>  

<span data-ttu-id="c6a4a-133">Come si ricorderà, il contenuto originale si presentava come segue:</span><span class="sxs-lookup"><span data-stu-id="c6a4a-133">If you recall the original content looked like this:</span></span>

~~~~
   {
        id: '4',
        description: 'Home Office'
   }
~~~~

<span data-ttu-id="c6a4a-134">Ora che i dati sono stati separati in campi distinti, tuttavia, non è possibile sapere se il valore "Home Office" per Jen Campbell è correlato a `locationsID 3` o `locationsID 4`.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-134">However, now that we have separated the data into separate fields, we have no way of knowing if the Home Office for Jen Campbell relates to `locationsID 3` or `locationsID 4`.</span></span>  

<span data-ttu-id="c6a4a-135">Per gestire questo caso, definire un altro campo dell'indice che combina tutti i dati in una singola raccolta.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-135">To handle this case, define another field in the index that combines all of the data into a single collection.</span></span>  <span data-ttu-id="c6a4a-136">In questo esempio, il campo verrà denominato `locationsCombined` e il contenuto verrà separato con `||`. È tuttavia possibile scegliere qualsiasi separatore che si ritiene possa essere una serie di caratteri univoca per il contenuto specifico.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-136">For our example, we will call this field `locationsCombined` and we will separate the content with a `||` although you can choose any separator that you think would be a unique set of characters for your content.</span></span> <span data-ttu-id="c6a4a-137">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c6a4a-137">For example:</span></span> 

![Dati di esempio, 2 righe con separatore](./media/search-howto-complex-data-types/sample-data-2.png)

<span data-ttu-id="c6a4a-139">Usando il campo `locationsCombined` , è ora possibile supportare query aggiuntive, ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c6a4a-139">Using this `locationsCombined` field, we can now accommodate even more queries, such as:</span></span>

* <span data-ttu-id="c6a4a-140">Visualizzare un conteggio delle persone che lavorano in "Home Office" con ID ubicazione "4".</span><span class="sxs-lookup"><span data-stu-id="c6a4a-140">Show a count of people who work at a ‘Home Office’ with location Id of ‘4’.</span></span>  
* <span data-ttu-id="c6a4a-141">Cercare le persone che lavorano in "Home Office" con ID ubicazione "4".</span><span class="sxs-lookup"><span data-stu-id="c6a4a-141">Search for people who work at a ‘Home Office’ with location Id ‘4’.</span></span> 

## <a name="limitations"></a><span data-ttu-id="c6a4a-142">Limitazioni</span><span class="sxs-lookup"><span data-stu-id="c6a4a-142">Limitations</span></span>
<span data-ttu-id="c6a4a-143">Questa tecnica è utile per diversi scenari, ma non è applicabile in tutti i casi.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-143">This technique is useful for a number of scenarios, but it is not applicable in every case.</span></span>  <span data-ttu-id="c6a4a-144">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c6a4a-144">For example:</span></span>

1. <span data-ttu-id="c6a4a-145">Se il tipo di dati complesso non include un set statico di campi e non è stato possibile eseguire il mapping di tutti i tipi possibili a un singolo campo.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-145">If you do not have a static set of fields in your complex data type and there was no way to map all the possible types to a single field.</span></span> 
2. <span data-ttu-id="c6a4a-146">L'aggiornamento degli oggetti annidati richiede operazioni aggiuntive per determinare esattamente gli elementi da aggiornare nell'indice di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-146">Updating the nested objects requires some extra work to determine exactly what needs to be updated in the Azure Search index</span></span>

## <a name="sample-code"></a><span data-ttu-id="c6a4a-147">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="c6a4a-147">Sample code</span></span>
<span data-ttu-id="c6a4a-148">Un esempio dell'indicizzazione di un set di dati JSON complesso in Ricerca di Azure e dell'esecuzione di diverse query su tale set di dati è disponibile in questo [repository GitHub](https://github.com/liamca/AzureSearchComplexTypes).</span><span class="sxs-lookup"><span data-stu-id="c6a4a-148">You can see an example on how to index a complex JSON data set into Azure Search and perform a number of queries over this dataset at this [GitHub repo](https://github.com/liamca/AzureSearchComplexTypes).</span></span>

## <a name="next-step"></a><span data-ttu-id="c6a4a-149">Passaggio successivo</span><span class="sxs-lookup"><span data-stu-id="c6a4a-149">Next step</span></span>
<span data-ttu-id="c6a4a-150">[Votare per il supporto nativo di tipi di dati complessi](https://feedback.azure.com/forums/263029-azure-search) nella pagina UserVoice relativa a Ricerca di Azure e fornire eventuali input aggiuntivi da prendere in considerazione in merito all'implementazione di questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-150">[Vote for native support for complex data types](https://feedback.azure.com/forums/263029-azure-search) on the Azure Search UserVoice page and provide any additional input that you’d like us to consider regarding feature implementation.</span></span> <span data-ttu-id="c6a4a-151">È anche possibile contattare direttamente @liamca su Twitter.</span><span class="sxs-lookup"><span data-stu-id="c6a4a-151">You can also reach out to me directly on Twitter at @liamca.</span></span>

