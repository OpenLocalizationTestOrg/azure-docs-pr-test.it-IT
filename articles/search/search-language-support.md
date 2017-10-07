---
title: "linguaggio di ricerca più aaaAzure | Documenti Microsoft"
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
ms.openlocfilehash: 9a2e567a82ee563521c12ea320f6c484a8e73f04
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-index-for-documents-in-multiple-languages-in-azure-search"></a><span data-ttu-id="17a7c-103">Creare un indice per i documenti in più lingue in Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="17a7c-103">Create an index for documents in multiple languages in Azure Search</span></span>
> [!div class="op_single_selector"]
>
> * [<span data-ttu-id="17a7c-104">Portale</span><span class="sxs-lookup"><span data-stu-id="17a7c-104">Portal</span></span>](search-language-support.md)
> * [<span data-ttu-id="17a7c-105">REST</span><span class="sxs-lookup"><span data-stu-id="17a7c-105">REST</span></span>](https://msdn.microsoft.com/library/azure/dn879793.aspx)
> * [<span data-ttu-id="17a7c-106">.NET</span><span class="sxs-lookup"><span data-stu-id="17a7c-106">.NET</span></span>](https://msdn.microsoft.com/library/azure/microsoft.azure.search.models.analyzername.aspx)
>
>

<span data-ttu-id="17a7c-107">Unleashing hello potenza gli analizzatori del linguaggio è semplice come una proprietà di impostazione su un campo nella definizione dell'indice hello ricercabile.</span><span class="sxs-lookup"><span data-stu-id="17a7c-107">Unleashing hello power of language analyzers is as easy as setting one property on a searchable field in hello index definition.</span></span> <span data-ttu-id="17a7c-108">È ora possibile eseguire questo passaggio nel portale di hello.</span><span class="sxs-lookup"><span data-stu-id="17a7c-108">Now you can do this step in hello portal.</span></span>

<span data-ttu-id="17a7c-109">Di seguito sono schermate di hello pannelli portale di Azure per la ricerca di Azure che consentono agli utenti toodefine uno schema di indice.</span><span class="sxs-lookup"><span data-stu-id="17a7c-109">Below are screenshots of hello Azure Portal blades for Azure Search that allow users toodefine an index schema.</span></span> <span data-ttu-id="17a7c-110">Da questo pannello, gli utenti possono creare tutti i campi di hello e impostare proprietà analyzer hello per ognuno di essi.</span><span class="sxs-lookup"><span data-stu-id="17a7c-110">From this blade, users can create all of hello fields and set hello analyzer property for each of them.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="17a7c-111">È possibile impostare solo un analizzatore di lingua durante la definizione di campo, ad esempio quando si crea un nuovo indice dall'hello messa a terra o quando si aggiunge un nuovo indice esistente tooan di campo.</span><span class="sxs-lookup"><span data-stu-id="17a7c-111">You can only set a language analyzer during field definition, as in when creating a new index from hello ground up, or when adding a new field tooan existing index.</span></span> <span data-ttu-id="17a7c-112">Assicurarsi di specificare completamente tutti gli attributi, inclusi analyzer hello, durante la creazione di campo hello.</span><span class="sxs-lookup"><span data-stu-id="17a7c-112">Make sure you fully specify all attributes, including hello analyzer, while creating hello field.</span></span> <span data-ttu-id="17a7c-113">È non essere in grado di tooedit attributi hello o modificare il tipo di Analizzatore hello dopo aver salvato le modifiche.</span><span class="sxs-lookup"><span data-stu-id="17a7c-113">You won't be able tooedit hello attributes or change hello analyzer type once you save your changes.</span></span>
>
>

## <a name="define-a-new-field-definition"></a><span data-ttu-id="17a7c-114">Definire una nuova definizione di campo</span><span class="sxs-lookup"><span data-stu-id="17a7c-114">Define a new field definition</span></span>
1. <span data-ttu-id="17a7c-115">Accedi toohello [portale di Azure](https://portal.azure.com) e aprire hello blade di servizio del servizio di ricerca.</span><span class="sxs-lookup"><span data-stu-id="17a7c-115">Sign in toohello [Azure portal](https://portal.azure.com) and open hello service blade of your search service.</span></span>
2. <span data-ttu-id="17a7c-116">Fare clic su **Aggiungi indice** nel comando hello barra nella parte superiore di hello di hello servizio dashboard toostart un nuovo indice o aprire un tooset indice esistente in nuovi campi che si sta aggiungendo un analizzatore di indice esistente tooan.</span><span class="sxs-lookup"><span data-stu-id="17a7c-116">Click **Add index** in hello command bar at hello top of hello service dashboard toostart a new index, or open an existing index tooset an analyzer on new fields you're adding tooan existing index.</span></span>
3. <span data-ttu-id="17a7c-117">viene visualizzato il pannello di campi Hello, contenente le opzioni per la definizione dello schema hello dell'indice di hello, incluso tab Analyzer hello utilizzato per la scelta di un analizzatore di lingua.</span><span class="sxs-lookup"><span data-stu-id="17a7c-117">hello Fields blade appears, giving you options for defining hello schema of hello index, including hello Analyzer tab used for choosing a language analyzer.</span></span>
4. <span data-ttu-id="17a7c-118">Nei campi, avviare una definizione di campo che fornisce un nome, scelta del tipo di dati hello e impostazione di attributi toomark hello campo come full-text ricercabili, recuperabile nei risultati della ricerca, può essere usati in strutture di navigazione di facet, ordinabile e così via.</span><span class="sxs-lookup"><span data-stu-id="17a7c-118">In Fields, start a field definition by providing a name, choosing hello data type, and setting attributes toomark hello field as full text searchable, retrievable in search results, usable in facet navigation structures, sortable, and so forth.</span></span>
5. <span data-ttu-id="17a7c-119">Prima di proseguire campo successivo toohello aprire hello **Analyzer** scheda.</span><span class="sxs-lookup"><span data-stu-id="17a7c-119">Before moving on toohello next field, open hello **Analyzer** tab.</span></span>

<span data-ttu-id="17a7c-120">![][1]
*tooselect un analizzatore, fare clic su scheda Analyzer hello nel pannello campi hello*</span><span class="sxs-lookup"><span data-stu-id="17a7c-120">![][1]
*tooselect an analyzer, click hello Analyzer tab on hello Fields blade*</span></span>

## <a name="choose-an-analyzer"></a><span data-ttu-id="17a7c-121">Scegliere un analizzatore</span><span class="sxs-lookup"><span data-stu-id="17a7c-121">Choose an analyzer</span></span>
1. <span data-ttu-id="17a7c-122">La definizione di campo hello toofind di scorrimento.</span><span class="sxs-lookup"><span data-stu-id="17a7c-122">Scroll toofind hello field you are defining.</span></span>
2. <span data-ttu-id="17a7c-123">Se non sono stati contrassegnati campo hello come disponibile per la ricerca, fare clic su hello casella di controllo ora toomark come **Searchable**.</span><span class="sxs-lookup"><span data-stu-id="17a7c-123">If you haven't marked hello field as searchable, click hello checkbox now toomark it as **Searchable**.</span></span>
3. <span data-ttu-id="17a7c-124">Fare clic su elenco hello Analyzer area toodisplay hello di analizzatori disponibili.</span><span class="sxs-lookup"><span data-stu-id="17a7c-124">Click hello Analyzer area toodisplay hello list of available analyzers.</span></span>
4. <span data-ttu-id="17a7c-125">Scegliere analyzer hello desiderato toouse.</span><span class="sxs-lookup"><span data-stu-id="17a7c-125">Choose hello analyzer you want toouse.</span></span>

<span data-ttu-id="17a7c-126">![][2]
*Selezionare una delle analizzatori hello è supportato per ogni campo*</span><span class="sxs-lookup"><span data-stu-id="17a7c-126">![][2]
*Select one of hello supported analyzers for each field*</span></span>

<span data-ttu-id="17a7c-127">Per impostazione predefinita, tutti i campi ricercabili utilizzano hello [analizzatore Lucene Standard](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) che è indipendente dalla lingua.</span><span class="sxs-lookup"><span data-stu-id="17a7c-127">By default, all searchable fields use hello [Standard Lucene analyzer](http://lucene.apache.org/core/4_10_0/analyzers-common/org/apache/lucene/analysis/standard/StandardAnalyzer.html) which is language agnostic.</span></span> <span data-ttu-id="17a7c-128">elenco completo di hello tooview di analizzatori di supportati, vedere [supporto della lingua nella ricerca di Azure](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span><span class="sxs-lookup"><span data-stu-id="17a7c-128">tooview hello full list of supported analyzers, see [Language Support in Azure Search](https://msdn.microsoft.com/library/azure/dn879793.aspx).</span></span>

<span data-ttu-id="17a7c-129">Una volta l'analizzatore di lingua hello è selezionata per un campo, verrà utilizzata con ogni richiesta di ricerca e indicizzazione per il campo.</span><span class="sxs-lookup"><span data-stu-id="17a7c-129">Once hello language analyzer is selected for a field, it will be used with each indexing and search request for that field.</span></span> <span data-ttu-id="17a7c-130">Quando una query viene eseguita in più campi usando gli analizzatori di diversi, hello query viene elaborata in modo indipendente dagli analizzatori di destra hello per ogni campo.</span><span class="sxs-lookup"><span data-stu-id="17a7c-130">When a query is issued against multiple fields using different analyzers, hello query will be processed independently by hello right analyzers for each field.</span></span>

<span data-ttu-id="17a7c-131">Molte applicazioni web e mobili servono gli utenti in tutto il mondo hello utilizzando diversi linguaggi.</span><span class="sxs-lookup"><span data-stu-id="17a7c-131">Many web and mobile applications serve users around hello globe using different languages.</span></span> <span data-ttu-id="17a7c-132">È possibile toodefine un indice per uno scenario simile mediante la creazione di un campo per ogni lingua supportata.</span><span class="sxs-lookup"><span data-stu-id="17a7c-132">It’s possible toodefine an index for a scenario like this by creating a field for each language supported.</span></span>

<span data-ttu-id="17a7c-133">![][3]
*Definizione di indice con un campo di descrizione per ogni lingua supportata*</span><span class="sxs-lookup"><span data-stu-id="17a7c-133">![][3]
*Index definition with a description field for each language supported*</span></span>

<span data-ttu-id="17a7c-134">Se è noto linguaggio hello dell'agente di hello esecuzione di una query, una richiesta di ricerca può essere tooa con ambito di campo specifico utilizzando hello **searchFields** parametro di query.</span><span class="sxs-lookup"><span data-stu-id="17a7c-134">If hello language of hello agent issuing a query is known, a search request can be scoped tooa specific field using hello **searchFields** query parameter.</span></span> <span data-ttu-id="17a7c-135">Hello nella query seguente verrà eseguita solo sul descrizione hello in polacco:</span><span class="sxs-lookup"><span data-stu-id="17a7c-135">hello following query will be issued only against hello description in Polish:</span></span>

`https://[service name].search.windows.net/indexes/[index name]/docs?search=darmowy&searchFields=description_pl&api-version=2016-09-01`

<span data-ttu-id="17a7c-136">È possibile eseguire query di indice dal portale hello utilizzando **Esplora ricerche** toopaste in un toohello simile a query illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="17a7c-136">You can query your index from hello portal, using **Search explorer** toopaste in a query similar toohello one shown above.</span></span> <span data-ttu-id="17a7c-137">Esplora ricerche è disponibile dalla barra dei comandi hello nel pannello service hello.</span><span class="sxs-lookup"><span data-stu-id="17a7c-137">Search explorer is available from hello command bar in hello service blade.</span></span> <span data-ttu-id="17a7c-138">Vedere [Query sull'indice ricerca di Azure nel portale di hello](search-explorer.md) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="17a7c-138">See [Query your Azure Search index in hello portal](search-explorer.md) for details.</span></span>

<span data-ttu-id="17a7c-139">In alcuni casi hello lingua dell'agente di hello esecuzione di una query non è noto, in cui hello case possono essere eseguite su tutti i campi contemporaneamente.</span><span class="sxs-lookup"><span data-stu-id="17a7c-139">Sometimes hello language of hello agent issuing a query is not known, in which case hello query can be issued against all fields simultaneously.</span></span> <span data-ttu-id="17a7c-140">Se necessario, è possibile definire delle preferenze per i risultati in una determinata lingua usando i [profili di punteggio](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span><span class="sxs-lookup"><span data-stu-id="17a7c-140">If needed, preference for results in a certain language can be defined using [scoring profiles](https://msdn.microsoft.com/library/azure/dn798928.aspx).</span></span> <span data-ttu-id="17a7c-141">Nel seguente esempio hello corrispondenze trovate nella descrizione hello in lingua inglese verranno considerato equivalente toomatches relativo superiore in polacco e il francese:</span><span class="sxs-lookup"><span data-stu-id="17a7c-141">In hello example below, matches found in hello description in English will be scored higher relative toomatches in Polish and French:</span></span>

    "scoringProfiles": [
      {
        "name": "englishFirst",
        "text": {
          "weights": { "description_en": 2 }
        }
      }
    ]

`https://[service name].search.windows.net/indexes/[index name]/docs?search=Microsoft&scoringProfile=englishFirst&api-version=2016-09-01`

<span data-ttu-id="17a7c-142">Se si è uno sviluppatore di .NET, si noti che è possibile configurare gli analizzatori del linguaggio mediante hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span><span class="sxs-lookup"><span data-stu-id="17a7c-142">If you're a .NET developer, note that you can configure language analyzers using hello [Azure Search .NET SDK](http://www.nuget.org/packages/Microsoft.Azure.Search).</span></span> <span data-ttu-id="17a7c-143">la versione più recente di Hello include il supporto per hello Microsoft gli analizzatori del linguaggio nonché.</span><span class="sxs-lookup"><span data-stu-id="17a7c-143">hello latest release includes support for hello Microsoft language analyzers as well.</span></span>

<!-- Image References -->
[1]: ./media/search-language-support/AnalyzerTab.png
[2]: ./media/search-language-support/SelectAnalyzer.png
[3]: ./media/search-language-support/IndexDefinition.png
