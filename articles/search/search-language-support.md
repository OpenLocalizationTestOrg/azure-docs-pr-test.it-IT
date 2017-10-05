---
title: "Ricerca di Azure disponibile in più lingue | Documentazione Microsoft"
description: Ricerca di Azure supporta 56 lingue, grazie ai vantaggi offerti dagli analizzatori delle lingue della tecnologia Lucene e di elaborazione del linguaggio naturale di Microsoft.
services: search
documentationcenter: 
author: yahnoosh
manager: pablocas
editor: 
ms.assetid: 55a00b44-804d-41bb-9c96-e6ea498616f5
ms.service: search
ms.devlang: na
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/23/2017
ms.author: jlembicz
ms.openlocfilehash: dbbab31bac66ce73dbf9883992713a2c16581e19
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="ffd37-103">Creare un indice per i documenti in più lingue in Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="ffd37-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="ffd37-104">Portale</span><span class="sxs-lookup"><span data-stu-id="ffd37-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="ffd37-105">REST</span><span class="sxs-lookup"><span data-stu-id="ffd37-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="ffd37-106">.NET</span><span class="sxs-lookup"><span data-stu-id="ffd37-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="ffd37-107">Consentire l'espressione della potenza degli analizzatori delle lingue è semplice come l'impostazione di una proprietà in un campo di ricerca nella definizione dell'indice.</span><span class="sxs-lookup"><span data-stu-id="ffd37-107">Unleashing the power of language analyzers is as easy as setting one property on a searchable field in the index definition.</span></span> <span data-ttu-id="ffd37-108">Questo passaggio può ora essere eseguito nel portale.</span><span class="sxs-lookup"><span data-stu-id="ffd37-108">Now you can do this step in the portal.</span></span>

<span data-ttu-id="ffd37-109">Di seguito sono riportate schermate dei pannelli del portale di Azure relativi a Ricerca di Azure che consentono agli utenti di definire uno schema di indice.</span><span class="sxs-lookup"><span data-stu-id="ffd37-109">Below are screenshots of the Azure Portal blades for Azure Search that allow users to define an index schema.</span></span> <span data-ttu-id="ffd37-110">Da questi pannelli, gli utenti possono creare tutti i campi e impostare la proprietà analyzer per ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="ffd37-110">From this blade, users can create all of the fields and set the analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ffd37-111">È possibile impostare solo un analizzatore della lingua durante la definizione del campo, come quando si crea un nuovo indice da zero o si aggiunge un nuovo campo a un indice esistente.</span><span class="sxs-lookup"><span data-stu-id="ffd37-111">You can only set a language analyzer during field definition, as in when creating a new index from the ground up, or when adding a new field to an existing index.</span></span> <span data-ttu-id="ffd37-112">Assicurarsi di specificare completamente tutti gli attributi, incluso l'analizzatore, durante la creazione del campo.</span><span class="sxs-lookup"><span data-stu-id="ffd37-112">Make sure you fully specify all attributes, including the analyzer, while creating the field.</span></span> <span data-ttu-id="ffd37-113">Non sarà possibile modificare gli attributi o cambiare il tipo di analizzatore dopo avere salvato le modifiche.</span><span class="sxs-lookup"><span data-stu-id="ffd37-113">You won't be able to edit the attributes or change the analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="ffd37-114">Definire una nuova definizione di campo</span><span class="sxs-lookup"><span data-stu-id="ffd37-114">Define a new field definition</span></span>
1. <span data-ttu-id="ffd37-115">Accedere al [portale di Azure](https://portal.azure.com) e aprire il pannello del servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="ffd37-115">Sign in to the [Azure portal](https://portal.azure.com) and open the service blade of your search service.</span></span>
2. <span data-ttu-id="ffd37-116">Fare clic su **Aggiungi un indice** nella barra di comando del dashboard del servizio per avviare un nuovo indice oppure aprire un indice esistente per impostare un analizzatore nei nuovi campi aggiunti a un indice esistente.</span><span class="sxs-lookup"><span data-stu-id="ffd37-116">Click **Add index** in the command bar at the top of the service dashboard to start a new index, or open an existing index to set an analyzer on new fields you're adding to an existing index.</span></span>
3. <span data-ttu-id="ffd37-117">Viene visualizzato il pannello Campi, con opzioni per la definizione dello schema dell'indice, inclusa la scheda Analizzatore usata per la scelta di un analizzatore della lingua.</span><span class="sxs-lookup"><span data-stu-id="ffd37-117">The Fields blade appears, giving you options for defining the schema of the index, including the Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="ffd37-118">In Campi avviare una definizione di campo fornendo un nome, scegliendo il tipo di dati e impostando gli attributi per contrassegnare il campo come disponibile per la ricerca full-text, recuperabile nei risultati della ricerca, utilizzabile nelle strutture di navigazione facet, ordinabile e così via.</span><span class="sxs-lookup"><span data-stu-id="ffd37-118">In Fields, start a field definition by providing a name, choosing the data type, and setting attributes to mark the field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="ffd37-119">Prima di passare al campo successivo, aprire la scheda **Analizzatore** .</span><span class="sxs-lookup"><span data-stu-id="ffd37-119">Before moving on to the next field, open the **Analyzer** tab.</span></span>

<span data-ttu-id="ffd37-120">![][1]
*Per selezionare un analizzatore, fare clic sulla scheda Analizzatore nel pannello Campi*</span><span class="sxs-lookup"><span data-stu-id="ffd37-120">![][1]
*To select an analyzer, click the Analyzer tab on the Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="ffd37-121">Scegliere un analizzatore</span><span class="sxs-lookup"><span data-stu-id="ffd37-121">Choose an analyzer</span></span>
1. <span data-ttu-id="ffd37-122">Scorrere per trovare il campo che si sta definendo.</span><span class="sxs-lookup"><span data-stu-id="ffd37-122">Scroll to find the field you are defining.</span></span>
2. <span data-ttu-id="ffd37-123">Se il campo non è stato contrassegnato come ricercabile, fare clic sulla casella di controllo per contrassegnarlo come **Ricercabile**.</span><span class="sxs-lookup"><span data-stu-id="ffd37-123">If you haven't marked the field as searchable, click the checkbox now to mark it as **Searchable**.</span></span>
3. <span data-ttu-id="ffd37-124">Fare clic sull'area dell'analizzatore per visualizzare l'elenco degli analizzatori disponibili.</span><span class="sxs-lookup"><span data-stu-id="ffd37-124">Click the Analyzer area to display the list of available analyzers.</span></span>
4. <span data-ttu-id="ffd37-125">Scegliere l'analizzatore che si desidera usare.</span><span class="sxs-lookup"><span data-stu-id="ffd37-125">Choose the analyzer you want to use.</span></span>

<span data-ttu-id="ffd37-126">![][2]
*Selezionare uno degli analizzatori supportati per ogni campo*</span><span class="sxs-lookup"><span data-stu-id="ffd37-126">![][2]
*Select one of the supported analyzers for each field*</span></span>

<span data-ttu-id="ffd37-127">Per impostazione predefinita, tutti i campi di ricerca usano l' [analizzatore Standard Lucene](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) che è indipendente dalla lingua.</span><span class="sxs-lookup"><span data-stu-id="ffd37-127">By default, all searchable fields use the [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="ffd37-128">Per visualizzare l'elenco completo degli analizzatori supportati, vedere il post di blog relativo alle [lingue supportate in Ricerca di Azure](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="ffd37-128">To view the full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="ffd37-129">Dopo aver selezionato l'analizzatore della lingua per un campo, verrà usato per ogni richiesta di ricerca e indicizzazione relativa a quel campo.</span><span class="sxs-lookup"><span data-stu-id="ffd37-129">Once the language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="ffd37-130">Quando viene eseguita una query su più campi usando analizzatori diversi, la query verrà elaborata in modo indipendente dagli analizzatori specifici di ciascun campo.</span><span class="sxs-lookup"><span data-stu-id="ffd37-130">When a query is issued against multiple fields using different analyzers, the query will be processed independently by the right analyzers for each field.</span></span>

<span data-ttu-id="ffd37-131">Molte applicazioni Web e per dispositivi mobili vengono sfruttate dagli utenti in tutto il mondo in diverse lingue.</span><span class="sxs-lookup"><span data-stu-id="ffd37-131">Many web and mobile applications serve users around the globe using different languages.</span></span> <span data-ttu-id="ffd37-132">È possibile definire un indice per uno scenario simile al seguente mediante la creazione di un campo per ogni lingua supportata.</span><span class="sxs-lookup"><span data-stu-id="ffd37-132">It’s possible to define an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="ffd37-133">![][3]
*Definizione di indice con un campo di descrizione per ogni lingua supportata*</span><span class="sxs-lookup"><span data-stu-id="ffd37-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="ffd37-134">Se la lingua dell'agente che esegue una query è nota, è possibile definire per una richiesta di ricerca un ambito relativo a un campo specifico usando il parametro di query **searchFields** .</span><span class="sxs-lookup"><span data-stu-id="ffd37-134">If the language of the agent issuing a query is known, a search request can be scoped to a specific field using the **searchFields** query parameter.</span></span> <span data-ttu-id="ffd37-135">La query seguente verrà generata solo per la descrizione in polacco:</span><span class="sxs-lookup"><span data-stu-id="ffd37-135">The following query will be issued only against the description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="ffd37-136">È possibile eseguire query sull'indice dal portale, usando **Esplora ricerche** per incollare una query simile a quello illustrata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="ffd37-136">You can query your index from the portal, using **Search explorer** to paste in a query similar to the one shown above.</span></span> <span data-ttu-id="ffd37-137">Esplora ricerche è disponibile nella barra dei comandi nel pannello del servizio.</span><span class="sxs-lookup"><span data-stu-id="ffd37-137">Search explorer is available from the command bar in the service blade.</span></span> <span data-ttu-id="ffd37-138">Per informazioni dettagliate, vedere [Eseguire query su un indice di Ricerca di Azure](search-explorer.md) .</span><span class="sxs-lookup"><span data-stu-id="ffd37-138">See [Query your Azure Search index in the portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="ffd37-139">È possibile che la lingua dell'agente che esegue una query non sia nota, in tal caso la query può essere inviata a tutti i campi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="ffd37-139">Sometimes the language of the agent issuing a query is not known, in which case the query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="ffd37-140">Se necessario, è possibile definire delle preferenze per i risultati in una determinata lingua usando i [profili di punteggio](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="ffd37-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="ffd37-141">Nell'esempio seguente, alle corrispondenze trovate nella descrizione in inglese viene assegnato un punteggio più elevato rispetto alle corrispondenze in polacco e francese:</span><span class="sxs-lookup"><span data-stu-id="ffd37-141">In the example below, matches found in the description in English will be scored higher relative to matches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="ffd37-142">Per gli sviluppatori .NET, si noti che è possibile configurare analizzatori delle lingue mediante l' [SDK .NET di Ricerca di Azure](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="ffd37-142">If you're a .NET developer, note that you can configure language analyzers using the [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="ffd37-143">La versione più recente supporta anche gli analizzatori delle lingue di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ffd37-143">The latest release includes support for the Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
