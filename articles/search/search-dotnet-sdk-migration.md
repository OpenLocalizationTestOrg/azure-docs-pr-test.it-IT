---
title: aaaUpgrading toohello Azure Search .NET SDK versione 1.1 | Documenti Microsoft
description: L'aggiornamento toohello Azure Search .NET SDK versione 1.1
services: search
documentationcenter: 
author: brjohnstmsft
manager: pablocas
editor: 
ms.assetid: 66f89958-a320-4a24-87f9-69315848909f
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 01/11/2017
ms.author: brjohnst
ms.openlocfilehash: 291ae5731546e47b3c22c721d3552a79bdea80c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="upgrading-toohello-azure-search-net-sdk-version-3"></a><span data-ttu-id="c7e58-103">L'aggiornamento toohello Azure Search .NET SDK versione 3</span><span class="sxs-lookup"><span data-stu-id="c7e58-103">Upgrading toohello Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="c7e58-104">Se si usa versione 2.0 per l'anteprima o meno recenti di hello [Azure Search .NET SDK](https://aka.ms/search-sdk), in questo articolo consentirà di aggiornare la versione di toouse applicazione 3.</span><span class="sxs-lookup"><span data-stu-id="c7e58-104">If you're using version 2.0-preview or older of hello [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application toouse version 3.</span></span>

<span data-ttu-id="c7e58-105">Per una procedura dettagliata più generale di hello SDK inclusi esempi, vedere [come toouse ricerca di Azure da un'applicazione .NET](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="c7e58-105">For a more general walkthrough of hello SDK including examples, see [How toouse Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="c7e58-106">Versione 3 di hello Azure Search .NET SDK include alcune modifiche apportate da versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="c7e58-106">Version 3 of hello Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="c7e58-107">ma per lo più secondarie, quindi il codice potrà essere modificato facilmente.</span><span class="sxs-lookup"><span data-stu-id="c7e58-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="c7e58-108">Vedere [tooupgrade passaggi](#UpgradeSteps) per istruzioni su come toochange la versione del SDK nuovo codice toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c7e58-108">See [Steps tooupgrade](#UpgradeSteps) for instructions on how toochange your code toouse hello new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="c7e58-109">Se si utilizza una versione 1.0.2-preview o precedente, è necessario eseguire prima l'aggiornamento tooversion 1.1 e quindi Aggiorna tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="c7e58-109">If you're using version 1.0.2-preview or older, you should upgrade tooversion 1.1 first, and then upgrade tooversion 3.</span></span> <span data-ttu-id="c7e58-110">Vedere [appendice: passaggi tooupgrade tooversion 1.1](#UpgradeStepsV1) per le istruzioni.</span><span class="sxs-lookup"><span data-stu-id="c7e58-110">See [Appendix: Steps tooupgrade tooversion 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="c7e58-111">L'istanza del servizio di ricerca di Azure supporta più versioni API REST, tra cui hello più recente.</span><span class="sxs-lookup"><span data-stu-id="c7e58-111">Your Azure Search service instance supports several REST API versions, including hello latest one.</span></span> <span data-ttu-id="c7e58-112">È possibile continuare toouse una versione quando non è più hello più recente, ma è consigliabile eseguire la migrazione la versione più recente del codice toouse hello.</span><span class="sxs-lookup"><span data-stu-id="c7e58-112">You can continue toouse a version when it is no longer hello latest one, but we recommend that you migrate your code toouse hello newest version.</span></span> <span data-ttu-id="c7e58-113">Quando si utilizza l'API REST di hello, è necessario specificare una versione dell'API hello in ogni richiesta tramite il parametro api-version hello.</span><span class="sxs-lookup"><span data-stu-id="c7e58-113">When using hello REST API, you must specify hello API version in every request via hello api-version parameter.</span></span> <span data-ttu-id="c7e58-114">Quando si utilizza hello .NET SDK, versione di hello di hello SDK in uso determina versione corrispondente di hello di hello API REST.</span><span class="sxs-lookup"><span data-stu-id="c7e58-114">When using hello .NET SDK, hello version of hello SDK you’re using determines hello corresponding version of hello REST API.</span></span> <span data-ttu-id="c7e58-115">Se si utilizza un SDK precedente, è possibile continuare toorun che il codice senza apportare modifiche anche se il servizio di hello è la versione aggiornata toosupport un'API più recente.</span><span class="sxs-lookup"><span data-stu-id="c7e58-115">If you are using an older SDK, you can continue toorun that code with no changes even if hello service is upgraded toosupport a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="c7e58-116">Novità della versione 3</span><span class="sxs-lookup"><span data-stu-id="c7e58-116">What's new in version 3</span></span>
<span data-ttu-id="c7e58-117">Versione 3 di hello destinazioni Azure Search .NET SDK di hello ultima versione disponibile in genere di hello API REST di ricerca di Azure, in particolare 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="c7e58-117">Version 3 of hello Azure Search .NET SDK targets hello latest generally available version of hello Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="c7e58-118">In questo modo è possibile toouse numerose nuove funzionalità di ricerca di Azure da un'applicazione .NET, inclusi hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="c7e58-118">This makes it possible toouse many new features of Azure Search from a .NET application, including hello following:</span></span>

* [<span data-ttu-id="c7e58-119">Analizzatori personalizzati</span><span class="sxs-lookup"><span data-stu-id="c7e58-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="c7e58-120">Supporto per gli indicizzatori di [Archiviazione BLOB di Azure](search-howto-indexing-azure-blob-storage.md) e [Archiviazione tabelle di Azure](search-howto-indexing-azure-tables.md)</span><span class="sxs-lookup"><span data-stu-id="c7e58-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="c7e58-121">Personalizzazione dell'indicizzatore tramite [mapping dei campi](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="c7e58-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="c7e58-122">ETag supporta tooenable provvisoria simultanee l'aggiornamento di indicizzare le origini dati, gli indicizzatori e definizioni</span><span class="sxs-lookup"><span data-stu-id="c7e58-122">ETags support tooenable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="c7e58-123">Supporto per la creazione di definizioni di campo di indice in modo dichiarativo decorando la classe di modello e utilizzando la nuova hello `FieldBuilder` classe.</span><span class="sxs-lookup"><span data-stu-id="c7e58-123">Support for building index field definitions declaratively by decorating your model class and using hello new `FieldBuilder` class.</span></span>
* <span data-ttu-id="c7e58-124">Supporto per .NET Core e .NET Portable Profile 111</span><span class="sxs-lookup"><span data-stu-id="c7e58-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-tooupgrade"></a><span data-ttu-id="c7e58-125">Passaggi tooupgrade</span><span class="sxs-lookup"><span data-stu-id="c7e58-125">Steps tooupgrade</span></span>
<span data-ttu-id="c7e58-126">Innanzitutto, aggiornare il riferimento di NuGet per `Microsoft.Azure.Search` utilizzando una Console di gestione pacchetti NuGet hello o facendo clic sul riferimenti del progetto e selezionare "Gestisci pacchetti NuGet..." in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c7e58-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="c7e58-127">Una volta NuGet è stato scaricato hello nuovi pacchetti e le relative dipendenze, ricompilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="c7e58-127">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="c7e58-128">A seconda della struttura del codice, la ricompilazione potrebbe essere eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="c7e58-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="c7e58-129">In questo caso, si è pronto toogo!</span><span class="sxs-lookup"><span data-stu-id="c7e58-129">If so, you're ready toogo!</span></span>

<span data-ttu-id="c7e58-130">Se la compilazione non riesce, verrà visualizzato un errore di compilazione hello seguente:</span><span class="sxs-lookup"><span data-stu-id="c7e58-130">If your build fails, you should see a build error like hello following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' too'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="c7e58-131">passaggio successivo Hello è toofix l'errore di compilazione.</span><span class="sxs-lookup"><span data-stu-id="c7e58-131">hello next step is toofix this build error.</span></span> <span data-ttu-id="c7e58-132">Vedere [modifiche di rilievo nella versione 3](#ListOfChanges) per informazioni dettagliate sulle cause di errore hello e come toofix è.</span><span class="sxs-lookup"><span data-stu-id="c7e58-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes hello error and how toofix it.</span></span>

<span data-ttu-id="c7e58-133">Si può vedere compilazione aggiuntive avvisi correlati tooobsolete metodi o proprietà.</span><span class="sxs-lookup"><span data-stu-id="c7e58-133">You may see additional build warnings related tooobsolete methods or properties.</span></span> <span data-ttu-id="c7e58-134">gli avvisi di Hello include istruzioni su quali toouse invece di hello funzionalità deprecata.</span><span class="sxs-lookup"><span data-stu-id="c7e58-134">hello warnings will include instructions on what toouse instead of hello deprecated feature.</span></span> <span data-ttu-id="c7e58-135">Ad esempio, se l'applicazione usa hello `IndexingParameters.Base64EncodeKeys` proprietà, è necessario ottenere un avviso per segnalare che`"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="c7e58-135">For example, if your application uses hello `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="c7e58-136">Una volta che è stato risolto eventuali errori di compilazione, è possibile apportare modifiche tooyour applicazione tootake sfruttare nuove funzionalità se si desidera.</span><span class="sxs-lookup"><span data-stu-id="c7e58-136">Once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span> <span data-ttu-id="c7e58-137">Vengono descritti in dettaglio le nuove funzionalità hello SDK [novità nella versione 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="c7e58-137">New features in hello SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="c7e58-138">Modifiche di rilievo nella versione 3</span><span class="sxs-lookup"><span data-stu-id="c7e58-138">Breaking changes in version 3</span></span>
<span data-ttu-id="c7e58-139">Non esiste un numero ridotto di modifiche di rilievo nella versione 3 che potrebbero richiedere codice cambia inoltre toorebuilding l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7e58-139">There a small number of breaking changes in version 3 that may require code changes in addition toorebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="c7e58-140">Tipo restituito Indexes.GetClient</span><span class="sxs-lookup"><span data-stu-id="c7e58-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="c7e58-141">Hello `Indexes.GetClient` dispone di un nuovo tipo restituito.</span><span class="sxs-lookup"><span data-stu-id="c7e58-141">hello `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="c7e58-142">In precedenza, restituiva `SearchIndexClient`, ma questo è stato modificato troppo`ISearchIndexClient` nella versione 2.0 per l'anteprima e che modifica si riflette direttamente tooversion 3.</span><span class="sxs-lookup"><span data-stu-id="c7e58-142">Previously, it returned `SearchIndexClient`, but this was changed too`ISearchIndexClient` in version 2.0-preview, and that change carries over tooversion 3.</span></span> <span data-ttu-id="c7e58-143">Si tratta di toosupport clienti che desiderano hello toomock `GetClient` metodo per gli unit test restituendo un'implementazione fittizia del `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-143">This is toosupport customers that wish toomock hello `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="c7e58-144">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7e58-144">Example</span></span>
<span data-ttu-id="c7e58-145">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="c7e58-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="c7e58-146">È possibile modificarla toothis toofix eventuali errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="c7e58-146">You can change it toothis toofix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-toostrings"></a><span data-ttu-id="c7e58-147">AnalyzerName, tipo di dati e altri utenti non sono più toostrings convertibile in modo implicito</span><span class="sxs-lookup"><span data-stu-id="c7e58-147">AnalyzerName, DataType, and others are no longer implicitly convertible toostrings</span></span>
<span data-ttu-id="c7e58-148">Esistono molti tipi di hello Azure Search .NET SDK che derivano da `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-148">There are many types in hello Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="c7e58-149">In precedenza questi tipi sono stati tutti implicitamente convertibile tootype `string`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-149">Previously these types were all implicitly convertible tootype `string`.</span></span> <span data-ttu-id="c7e58-150">Tuttavia, in cui è stato individuato un bug in hello `Object.Equals` implementazione di queste classi e correzione bug hello necessario disabilitare la conversione implicita.</span><span class="sxs-lookup"><span data-stu-id="c7e58-150">However, a bug was discovered in hello `Object.Equals` implementation for these classes, and fixing hello bug required disabling this implicit conversion.</span></span> <span data-ttu-id="c7e58-151">Conversione esplicita troppo`string` è comunque consentita.</span><span class="sxs-lookup"><span data-stu-id="c7e58-151">Explicit conversion too`string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="c7e58-152">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7e58-152">Example</span></span>
<span data-ttu-id="c7e58-153">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="c7e58-153">If your code looks like this:</span></span>

```csharp
var customTokenizerName = TokenizerName.Create("my_tokenizer"); 
var customTokenFilterName = TokenFilterName.Create("my_tokenfilter"); 
var customCharFilterName = CharFilterName.Create("my_charfilter"); 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        customTokenizerName,  
        new[] { customTokenFilterName },  
        new[] { customCharFilterName }), 
}; 
```

<span data-ttu-id="c7e58-154">È possibile modificarla toothis toofix eventuali errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="c7e58-154">You can change it toothis toofix any build errors:</span></span>

```csharp
const string CustomTokenizerName = "my_tokenizer"; 
const string CustomTokenFilterName = "my_tokenfilter"; 
const string CustomCharFilterName = "my_charfilter"; 
 
var index = new Index();
index.Analyzers = new Analyzer[] 
{ 
    new CustomAnalyzer( 
        "my_analyzer",  
        CustomTokenizerName,  
        new TokenFilterName[] { CustomTokenFilterName },  
        new CharFilterName[] { CustomCharFilterName })
}; 
```

### <a name="removed-obsolete-members"></a><span data-ttu-id="c7e58-155">Rimuovere i membri obsoleti</span><span class="sxs-lookup"><span data-stu-id="c7e58-155">Removed obsolete members</span></span>

<span data-ttu-id="c7e58-156">È possibile visualizzare le proprietà sono state contrassegnate come obsolete nella versione 2.0 per l'anteprima e viene successivamente rimosso nella versione 3 o toomethods correlati gli errori di compilazione.</span><span class="sxs-lookup"><span data-stu-id="c7e58-156">You may see build errors related toomethods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="c7e58-157">Se si verificano questi errori, ecco come tooresolve loro:</span><span class="sxs-lookup"><span data-stu-id="c7e58-157">If you encounter such errors, here is how tooresolve them:</span></span>

- <span data-ttu-id="c7e58-158">Se l'errore riguarda il costruttore `ScoringParameter(string name, string value)`, sostituirlo con `ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="c7e58-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="c7e58-159">Se si utilizza hello `ScoringParameter.Value` proprietà, utilizzare hello `ScoringParameter.Values` proprietà o hello `ToString` metodo invece.</span><span class="sxs-lookup"><span data-stu-id="c7e58-159">If you were using hello `ScoringParameter.Value` property, use hello `ScoringParameter.Values` property or hello `ToString` method instead.</span></span>
- <span data-ttu-id="c7e58-160">Se si utilizza hello `SearchRequestOptions.RequestId` proprietà, utilizzare hello `ClientRequestId` proprietà invece.</span><span class="sxs-lookup"><span data-stu-id="c7e58-160">If you were using hello `SearchRequestOptions.RequestId` property, use hello `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="c7e58-161">Funzionalità di anteprima rimosse</span><span class="sxs-lookup"><span data-stu-id="c7e58-161">Removed preview features</span></span>

<span data-ttu-id="c7e58-162">Se si esegue l'aggiornamento dalla versione 2.0 preview tooversion 3, tenere presente che JSON e CSV l'analisi di supporto per gli indicizzatori di Blob è stato rimosso dal momento che queste funzionalità sono ancora in anteprima.</span><span class="sxs-lookup"><span data-stu-id="c7e58-162">If you are upgrading from version 2.0-preview tooversion 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="c7e58-163">In particolare, hello dei seguenti metodi di hello `IndexingParametersExtensions` classe sono state rimosse:</span><span class="sxs-lookup"><span data-stu-id="c7e58-163">Specifically, hello following methods of hello `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="c7e58-164">Se l'applicazione ha una dipendenza rigida da queste funzionalità, non sarà in grado di tooupgrade tooversion 3 di hello Azure Search .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="c7e58-164">If your application has a hard dependency on these features, you will not be able tooupgrade tooversion 3 of hello Azure Search .NET SDK.</span></span> <span data-ttu-id="c7e58-165">È possibile continuare toouse versione 2.0 per l'anteprima.</span><span class="sxs-lookup"><span data-stu-id="c7e58-165">You can continue toouse version 2.0-preview.</span></span> <span data-ttu-id="c7e58-166">Tenere presente, tuttavia, che **non è consigliabile usare SDK in anteprima nelle applicazioni di produzione**.</span><span class="sxs-lookup"><span data-stu-id="c7e58-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="c7e58-167">Le funzionalità di anteprima sono destinate esclusivamente alla valutazione e sono soggette a modifiche.</span><span class="sxs-lookup"><span data-stu-id="c7e58-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="c7e58-168">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="c7e58-168">Conclusion</span></span>
<span data-ttu-id="c7e58-169">Per ulteriori dettagli sull'utilizzo di hello Azure Search .NET SDK, vedere il nostro aggiornato di recente [procedure](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="c7e58-169">If you need more details on using hello Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="c7e58-170">Invitiamo i commenti e suggerimenti su hello SDK.</span><span class="sxs-lookup"><span data-stu-id="c7e58-170">We welcome your feedback on hello SDK.</span></span> <span data-ttu-id="c7e58-171">Se si verificano problemi, è disponibile tooask ci per informazioni su hello [forum MSDN di ricerca di Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="c7e58-171">If you encounter problems, feel free tooask us for help on hello [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="c7e58-172">Se si trova un bug, è possibile segnalare un problema in hello [repository GitHub di Azure .NET SDK](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="c7e58-172">If you find a bug, you can file an issue in hello [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="c7e58-173">Verificare che tooprefix con il titolo del problema "Search SDK:".</span><span class="sxs-lookup"><span data-stu-id="c7e58-173">Make sure tooprefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="c7e58-174">Grazie per avere usato Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e58-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-tooupgrade-tooversion-11"></a><span data-ttu-id="c7e58-175">Appendice: Passaggi tooupgrade tooversion 1.1</span><span class="sxs-lookup"><span data-stu-id="c7e58-175">Appendix: Steps tooupgrade tooversion 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="c7e58-176">Questa sezione si applica solo toousers di hello Azure Search .NET SDK versione 1.0.2-preview e precedenti.</span><span class="sxs-lookup"><span data-stu-id="c7e58-176">This section applies only toousers of hello Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="c7e58-177">Innanzitutto, aggiornare il riferimento di NuGet per `Microsoft.Azure.Search` utilizzando una Console di gestione pacchetti NuGet hello o facendo clic sul riferimenti del progetto e selezionare "Gestisci pacchetti NuGet..." in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c7e58-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either hello NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="c7e58-178">Una volta NuGet è stato scaricato hello nuovi pacchetti e le relative dipendenze, ricompilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="c7e58-178">Once NuGet has downloaded hello new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="c7e58-179">Se fosse in precedenza usando versione 1.0.0-preview, 1.0.1-preview o 1.0.2-preview, compilazione hello dovrebbe avere esito positivo e si è pronto toogo!</span><span class="sxs-lookup"><span data-stu-id="c7e58-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, hello build should succeed and you're ready toogo!</span></span>

<span data-ttu-id="c7e58-180">Se in precedenza si utilizzava 0.13.0-preview versione o versioni precedenti, dovrebbe essere simile hello seguente errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="c7e58-180">If you were previously using version 0.13.0-preview or older, you should see build errors like hello following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: hello type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="c7e58-181">passaggio successivo Hello è uno degli errori di compilazione di hello toofix.</span><span class="sxs-lookup"><span data-stu-id="c7e58-181">hello next step is toofix hello build errors one by one.</span></span> <span data-ttu-id="c7e58-182">La maggior parte sarà necessario modificare alcuni nomi di classe e metodo che sono stati rinominati in hello SDK.</span><span class="sxs-lookup"><span data-stu-id="c7e58-182">Most will require changing some class and method names that have been renamed in hello SDK.</span></span> <span data-ttu-id="c7e58-183">[Elenco di modifiche di rilievo nella versione 1.1](#ListOfChangesV1) contiene l'elenco delle modifiche dei nomi.</span><span class="sxs-lookup"><span data-stu-id="c7e58-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="c7e58-184">Se si utilizza le classi personalizzate toomodel i documenti e tali classi dispongono di proprietà di tipi primitivi non nullable (ad esempio, `int` o `bool` in c#), è presente una correzione di bug nella versione 1.1 hello di hello SDK di cui è necessario essere consapevoli.</span><span class="sxs-lookup"><span data-stu-id="c7e58-184">If you're using custom classes toomodel your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in hello 1.1 version of hello SDK of which you should be aware.</span></span> <span data-ttu-id="c7e58-185">Per altri dettagli, vedere [Correzioni di bug nella versione 1.1](#BugFixesV1) .</span><span class="sxs-lookup"><span data-stu-id="c7e58-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="c7e58-186">Infine, dopo che è stato risolto eventuali errori di compilazione, è possibile apportare modifiche di tooyour applicazione tootake sfruttare nuove funzionalità se si desidera.</span><span class="sxs-lookup"><span data-stu-id="c7e58-186">Finally, once you've fixed any build errors, you can make changes tooyour application tootake advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="c7e58-187">Elenco di modifiche di rilievo nella versione 1.1</span><span class="sxs-lookup"><span data-stu-id="c7e58-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="c7e58-188">Hello seguente elenco viene ordinato in base probabilità hello che hello modifica influirà sul codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c7e58-188">hello following list is ordered by hello likelihood that hello change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="c7e58-189">Modifiche a IndexBatch e IndexAction</span><span class="sxs-lookup"><span data-stu-id="c7e58-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="c7e58-190">`IndexBatch.Create`è stato rinominato troppo`IndexBatch.New` e non dispone più di un `params` argomento.</span><span class="sxs-lookup"><span data-stu-id="c7e58-190">`IndexBatch.Create` has been renamed too`IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="c7e58-191">È possibile usare `IndexBatch.New` per i batch che combinano tipi diversi di azioni (unioni, eliminazioni e così via).</span><span class="sxs-lookup"><span data-stu-id="c7e58-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="c7e58-192">Inoltre, sono disponibili nuovi metodi statici per la creazione di batch in cui tutte le azioni hello sono hello stesso: `Delete`, `Merge`, `MergeOrUpload`, e `Upload`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-192">In addition, there are new static methods for creating batches where all hello actions are hello same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="c7e58-193">`IndexAction` non include più costruttori pubblici e le proprietà ora sono non modificabili.</span><span class="sxs-lookup"><span data-stu-id="c7e58-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="c7e58-194">È consigliabile utilizzare i nuovi metodi statici hello per la creazione di azioni per scopi diversi: `Delete`, `Merge`, `MergeOrUpload`, e `Upload`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-194">You should use hello new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="c7e58-195">`IndexAction.Create` è stato rimosso.</span><span class="sxs-lookup"><span data-stu-id="c7e58-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="c7e58-196">Se si usa l'overload di hello che accetta solo un documento, assicurarsi che toouse `Upload` invece.</span><span class="sxs-lookup"><span data-stu-id="c7e58-196">If you used hello overload that takes only a document, make sure toouse `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="c7e58-197">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7e58-197">Example</span></span>
<span data-ttu-id="c7e58-198">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="c7e58-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="c7e58-199">È possibile modificarla toothis toofix eventuali errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="c7e58-199">You can change it toothis toofix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="c7e58-200">Se si desidera, è possibile semplificare ulteriormente la toothis:</span><span class="sxs-lookup"><span data-stu-id="c7e58-200">If you want, you can further simplify it toothis:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="c7e58-201">Modifiche a IndexBatchException</span><span class="sxs-lookup"><span data-stu-id="c7e58-201">IndexBatchException changes</span></span>
<span data-ttu-id="c7e58-202">Hello `IndexBatchException.IndexResponse` proprietà è stata rinominata troppo`IndexingResults`, e il tipo è ora `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-202">hello `IndexBatchException.IndexResponse` property has been renamed too`IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="c7e58-203">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7e58-203">Example</span></span>
<span data-ttu-id="c7e58-204">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="c7e58-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="c7e58-205">È possibile modificarla toothis toofix eventuali errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="c7e58-205">You can change it toothis toofix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="c7e58-206">Modifiche ai metodi delle operazioni</span><span class="sxs-lookup"><span data-stu-id="c7e58-206">Operation method changes</span></span>
<span data-ttu-id="c7e58-207">Ogni operazione hello Azure Search .NET SDK viene esposto come un set di overload del metodo per i chiamanti sincroni e asincroni.</span><span class="sxs-lookup"><span data-stu-id="c7e58-207">Each operation in hello Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="c7e58-208">Hello firme e separazione di questi overload del metodo è stato modificato nella versione 1.1.</span><span class="sxs-lookup"><span data-stu-id="c7e58-208">hello signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="c7e58-209">Ad esempio, hello operazione "Get statistiche dell'indice" nelle versioni precedenti di hello SDK esposte queste firme:</span><span class="sxs-lookup"><span data-stu-id="c7e58-209">For example, hello "Get Index Statistics" operation in older versions of hello SDK exposed these signatures:</span></span>

<span data-ttu-id="c7e58-210">In `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="c7e58-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="c7e58-211">In `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="c7e58-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="c7e58-212">le firme di metodo Hello per hello stessa operazione nella versione 1.1 è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="c7e58-212">hello method signatures for hello same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="c7e58-213">In `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="c7e58-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="c7e58-214">In `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="c7e58-214">In `IndexesOperationsExtensions`:</span></span>

    // Simplified asynchronous operation
    public static Task<IndexGetStatisticsResult> GetStatisticsAsync(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        CancellationToken cancellationToken = default(CancellationToken));

    // Simplified synchronous operation
    public static IndexGetStatisticsResult GetStatistics(
        this IIndexesOperations operations,
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions));

<span data-ttu-id="c7e58-215">A partire dalla versione 1.1, hello Azure Search .NET SDK consente di organizzare i metodi di operazione in modo diverso:</span><span class="sxs-lookup"><span data-stu-id="c7e58-215">Starting with version 1.1, hello Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="c7e58-216">I parametri facoltativi ora vengono modellati come parametri predefiniti invece che come overload dei metodi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="c7e58-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="c7e58-217">Questo riduce il numero di hello degli overload del metodo, talvolta significativa.</span><span class="sxs-lookup"><span data-stu-id="c7e58-217">This reduces hello number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="c7e58-218">metodi di estensione Hello nascondono ora molti dettagli estranei hello HTTP dal chiamante hello.</span><span class="sxs-lookup"><span data-stu-id="c7e58-218">hello extension methods now hide a lot of hello extraneous details of HTTP from hello caller.</span></span> <span data-ttu-id="c7e58-219">Ad esempio, le versioni precedenti di hello SDK ha restituito un oggetto di risposta con codice di stato HTTP, viene spesso non mi serviva toocheck quanto i metodi di operazione generare `CloudException` per qualsiasi codice di stato che indica un errore.</span><span class="sxs-lookup"><span data-stu-id="c7e58-219">For example, older versions of hello SDK returned a response object with an HTTP status code, which you often didn't need toocheck because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="c7e58-220">salve nuovi oggetti modello restituire metodi di estensione, il salvataggio di hello evitare toounwrap nel codice.</span><span class="sxs-lookup"><span data-stu-id="c7e58-220">hello new extension methods just return model objects, saving you hello trouble of having toounwrap them in your code.</span></span>
* <span data-ttu-id="c7e58-221">Al contrario, hello interfacce core ora espongono metodi che offrono maggiore controllo a livello di hello HTTP se è necessario.</span><span class="sxs-lookup"><span data-stu-id="c7e58-221">Conversely, hello core interfaces now expose methods that give you more control at hello HTTP level if you need it.</span></span> <span data-ttu-id="c7e58-222">È ora possibile passare toobe di intestazioni HTTP personalizzate incluse nelle richieste e hello nuovo `AzureOperationResponse<T>` restituire tipo consente l'accesso diretto toohello `HttpRequestMessage` e `HttpResponseMessage` per l'operazione di hello.</span><span class="sxs-lookup"><span data-stu-id="c7e58-222">You can now pass in custom HTTP headers toobe included in requests, and hello new `AzureOperationResponse<T>` return type gives you direct access toohello `HttpRequestMessage` and `HttpResponseMessage` for hello operation.</span></span> <span data-ttu-id="c7e58-223">`AzureOperationResponse`è definito in hello `Microsoft.Rest.Azure` dello spazio dei nomi e lo sostituisce `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-223">`AzureOperationResponse` is defined in hello `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="c7e58-224">Modifiche a ScoringParameters</span><span class="sxs-lookup"><span data-stu-id="c7e58-224">ScoringParameters changes</span></span>
<span data-ttu-id="c7e58-225">Una nuova classe denominata `ScoringParameter` è stato aggiunto in toomake SDK più recente di hello profili di tooscoring parametri tooprovide più semplici in una query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="c7e58-225">A new class named `ScoringParameter` has been added in hello latest SDK toomake it easier tooprovide parameters tooscoring profiles in a search query.</span></span> <span data-ttu-id="c7e58-226">In precedenza hello `ScoringProfiles` proprietà di hello `SearchParameters` digitata come classe `IList<string>`; Ora è digitato come `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-226">Previously hello `ScoringProfiles` property of hello `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="c7e58-227">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7e58-227">Example</span></span>
<span data-ttu-id="c7e58-228">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="c7e58-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="c7e58-229">È possibile modificarla toothis toofix eventuali errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="c7e58-229">You can change it toothis toofix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="c7e58-230">Modifiche alle classi di modelli</span><span class="sxs-lookup"><span data-stu-id="c7e58-230">Model class changes</span></span>
<span data-ttu-id="c7e58-231">A causa di modifiche alla firma digitale toohello descritto in [le modifiche al metodo di operazione](#OperationMethodChanges), molte classi di hello `Microsoft.Azure.Search.Models` dello spazio dei nomi sono stati rinominati o rimossi.</span><span class="sxs-lookup"><span data-stu-id="c7e58-231">Due toohello signature changes described in [Operation method changes](#OperationMethodChanges), many classes in hello `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="c7e58-232">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="c7e58-232">For example:</span></span>

* <span data-ttu-id="c7e58-233">`IndexDefinitionResponse` è stata sostituita da `AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="c7e58-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="c7e58-234">`DocumentSearchResponse`è stato rinominato troppo`DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="c7e58-234">`DocumentSearchResponse` has been renamed too`DocumentSearchResult`</span></span>
* <span data-ttu-id="c7e58-235">`IndexResult`è stato rinominato troppo`IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="c7e58-235">`IndexResult` has been renamed too`IndexingResult`</span></span>
* <span data-ttu-id="c7e58-236">`Documents.Count()`Restituisce un `long` con numero di documenti hello anziché di un`DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="c7e58-236">`Documents.Count()` now returns a `long` with hello document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="c7e58-237">`IndexGetStatisticsResponse`è stato rinominato troppo`IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="c7e58-237">`IndexGetStatisticsResponse` has been renamed too`IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="c7e58-238">`IndexListResponse`è stato rinominato troppo`IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="c7e58-238">`IndexListResponse` has been renamed too`IndexListResult`</span></span>

<span data-ttu-id="c7e58-239">toosummarize, `OperationResponse`-le classi derivate che esisteva solo toowrap un oggetto modello sono state rimosse.</span><span class="sxs-lookup"><span data-stu-id="c7e58-239">toosummarize, `OperationResponse`-derived classes that existed only toowrap a model object have been removed.</span></span> <span data-ttu-id="c7e58-240">Hello altre classi hanno il suffisso modificato da `Response` troppo`Result`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-240">hello remaining classes have had their suffix changed from `Response` too`Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="c7e58-241">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7e58-241">Example</span></span>
<span data-ttu-id="c7e58-242">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="c7e58-242">If your code looks like this:</span></span>

    IndexerGetStatusResponse statusResponse = null;

    try
    {
        statusResponse = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = statusResponse.ExecutionInfo.LastResult;

<span data-ttu-id="c7e58-243">È possibile modificarla toothis toofix eventuali errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="c7e58-243">You can change it toothis toofix any build errors:</span></span>

    IndexerExecutionInfo status = null;

    try
    {
        status = _searchClient.Indexers.GetStatus(indexer.Name);
    }
    catch (Exception ex)
    {
        Console.WriteLine("Error polling for indexer status: {0}", ex.Message);
        return;
    }

    IndexerExecutionResult lastResult = status.LastResult;

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="c7e58-244">Classi di risposte e IEnumerable</span><span class="sxs-lookup"><span data-stu-id="c7e58-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="c7e58-245">Un'altra modifica che può avere effetto sul codice è che le classi di risposte contenenti raccolte non implementano più `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="c7e58-246">Al contrario, è possibile accedere direttamente la proprietà di raccolta hello.</span><span class="sxs-lookup"><span data-stu-id="c7e58-246">Instead, you can access hello collection property directly.</span></span> <span data-ttu-id="c7e58-247">Ad esempio, se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="c7e58-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="c7e58-248">È possibile modificarla toothis toofix eventuali errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="c7e58-248">You can change it toothis toofix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="c7e58-249">Caso speciale per le applicazioni Web</span><span class="sxs-lookup"><span data-stu-id="c7e58-249">Special case for web applications</span></span>
<span data-ttu-id="c7e58-250">Se si dispone di un'applicazione web che serializza `DocumentSearchResponse` direttamente i risultati della ricerca di toosend toohello browser, sarà necessario toochange il codice o risultati hello non serializzerà correttamente.</span><span class="sxs-lookup"><span data-stu-id="c7e58-250">If you have a web application that serializes `DocumentSearchResponse` directly toosend search results toohello browser, you will need toochange your code or hello results will not serialize correctly.</span></span> <span data-ttu-id="c7e58-251">Ad esempio, se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="c7e58-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="c7e58-252">È possibile modificarlo tramite il recupero hello `.Results` proprietà di hello ricerca risposta toofix ricerca risultati per il rendering:</span><span class="sxs-lookup"><span data-stu-id="c7e58-252">You can change it by getting hello `.Results` property of hello search response toofix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want toosearch everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="c7e58-253">Sarà necessario toolook in questo caso nel codice manualmente. **compilatore hello non segnalerà** perché `JsonResult.Data` è di tipo `object`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-253">You will have toolook for such cases in your code yourself; **hello compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="c7e58-254">Modifiche a CloudException</span><span class="sxs-lookup"><span data-stu-id="c7e58-254">CloudException changes</span></span>
<span data-ttu-id="c7e58-255">Hello `CloudException` classe è stata spostata da hello `Hyak.Common` toohello dello spazio dei nomi `Microsoft.Rest.Azure` dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="c7e58-255">hello `CloudException` class has moved from hello `Hyak.Common` namespace toohello `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="c7e58-256">Inoltre, il relativo `Error` proprietà è stata rinominata troppo`Body`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-256">Also, its `Error` property has been renamed too`Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="c7e58-257">Modifiche a SearchServiceClient e SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="c7e58-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="c7e58-258">tipo di hello Hello `Credentials` proprietà è stata modificata da `SearchCredentials` tooits classe base, `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-258">hello type of hello `Credentials` property has changed from `SearchCredentials` tooits base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="c7e58-259">Se è necessario hello tooaccess `SearchCredentials` di un `SearchIndexClient` o `SearchServiceClient`, usare hello nuovo `SearchCredentials` proprietà.</span><span class="sxs-lookup"><span data-stu-id="c7e58-259">If you need tooaccess hello `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use hello new `SearchCredentials` property.</span></span>

<span data-ttu-id="c7e58-260">Nelle versioni precedenti del SDK, hello `SearchServiceClient` e `SearchIndexClient` ha costruttori che ha richiesto un `HttpClient` parametro.</span><span class="sxs-lookup"><span data-stu-id="c7e58-260">In older versions of hello SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="c7e58-261">Questi sono stati sostituiti con costruttori che accettano `HttpClientHandler` e una matrice di oggetti `DelegatingHandler`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="c7e58-262">Questo rende più semplice tooinstall gestori personalizzati toopre-elaborano le richieste HTTP se necessario.</span><span class="sxs-lookup"><span data-stu-id="c7e58-262">This makes it easier tooinstall custom handlers toopre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="c7e58-263">Infine, hello costruttori che ha richiesto un `Uri` e `SearchCredentials` sono stati modificati.</span><span class="sxs-lookup"><span data-stu-id="c7e58-263">Finally, hello constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="c7e58-264">Ad esempio, se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="c7e58-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="c7e58-265">È possibile modificarla toothis toofix eventuali errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="c7e58-265">You can change it toothis toofix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="c7e58-266">Si noti che il tipo di hello di hello credenziali parametro ha modificato anche troppo`ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-266">Also note that hello type of hello credentials parameter has changed too`ServiceClientCredentials`.</span></span> <span data-ttu-id="c7e58-267">Si tratta di tooaffect improbabile che il codice dal `SearchCredentials` è derivato da `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-267">This is unlikely tooaffect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="c7e58-268">Passaggio di un ID richiesta</span><span class="sxs-lookup"><span data-stu-id="c7e58-268">Passing a request ID</span></span>
<span data-ttu-id="c7e58-269">Nelle versioni precedenti di hello SDK, è possibile impostare un ID di richiesta su hello `SearchServiceClient` o `SearchIndexClient` e potrebbe essere incluso in ogni toohello richiesta API REST.</span><span class="sxs-lookup"><span data-stu-id="c7e58-269">In older versions of hello SDK, you could set a request ID on hello `SearchServiceClient` or `SearchIndexClient` and it would be included in every request toohello REST API.</span></span> <span data-ttu-id="c7e58-270">Ciò è utile per la risoluzione dei problemi con il servizio di ricerca se è necessario il supporto toocontact.</span><span class="sxs-lookup"><span data-stu-id="c7e58-270">This is useful for troubleshooting issues with your search service if you need toocontact support.</span></span> <span data-ttu-id="c7e58-271">Tuttavia, è più utile tooset ID richiesta univoco per ogni operazione anziché toouse hello lo stesso ID per tutte le operazioni.</span><span class="sxs-lookup"><span data-stu-id="c7e58-271">However, it is more useful tooset a unique request ID for every operation rather than toouse hello same ID for all operations.</span></span> <span data-ttu-id="c7e58-272">Per questo motivo, hello `SetClientRequestId` metodi di `SearchServiceClient` e `SearchIndexClient` sono state rimosse.</span><span class="sxs-lookup"><span data-stu-id="c7e58-272">For this reason, hello `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="c7e58-273">In alternativa, è possibile passare un metodo dell'operazione richiesta ID tooeach tramite hello facoltativo `SearchRequestOptions` parametro.</span><span class="sxs-lookup"><span data-stu-id="c7e58-273">Instead, you can pass a request ID tooeach operation method via hello optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="c7e58-274">In una versione futura di hello SDK, verranno aggiunti un nuovo meccanismo per impostare un ID di richiesta a livello globale in client hello gli oggetti che è coerenza con l'approccio di hello utilizzato da altri SDK di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e58-274">In a future release of hello SDK, we will add a new mechanism for setting a request ID globally on hello client objects that is consistent with hello approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="c7e58-275">Esempio</span><span class="sxs-lookup"><span data-stu-id="c7e58-275">Example</span></span>
<span data-ttu-id="c7e58-276">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="c7e58-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="c7e58-277">È possibile modificarla toothis toofix eventuali errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="c7e58-277">You can change it toothis toofix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="c7e58-278">Modifiche ai nomi delle interfacce</span><span class="sxs-lookup"><span data-stu-id="c7e58-278">Interface name changes</span></span>
<span data-ttu-id="c7e58-279">nomi di interfaccia di Hello operazione gruppo hanno tutti toobe modificate coerente con i nomi delle proprietà corrispondenti:</span><span class="sxs-lookup"><span data-stu-id="c7e58-279">hello operation group interface names have all changed toobe consistent with their corresponding property names:</span></span>

* <span data-ttu-id="c7e58-280">tipo di Hello `ISearchServiceClient.Indexes` è stato rinominato da `IIndexOperations` troppo`IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-280">hello type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` too`IIndexesOperations`.</span></span>
* <span data-ttu-id="c7e58-281">tipo di Hello `ISearchServiceClient.Indexers` è stato rinominato da `IIndexerOperations` troppo`IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-281">hello type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` too`IIndexersOperations`.</span></span>
* <span data-ttu-id="c7e58-282">tipo di Hello `ISearchServiceClient.DataSources` è stato rinominato da `IDataSourceOperations` troppo`IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-282">hello type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` too`IDataSourcesOperations`.</span></span>
* <span data-ttu-id="c7e58-283">tipo di Hello `ISearchIndexClient.Documents` è stato rinominato da `IDocumentOperations` troppo`IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-283">hello type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` too`IDocumentsOperations`.</span></span>

<span data-ttu-id="c7e58-284">Questa modifica è tooaffect improbabile che il codice a meno che non è stato creato le simulazioni di queste interfacce per scopi di test.</span><span class="sxs-lookup"><span data-stu-id="c7e58-284">This change is unlikely tooaffect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="c7e58-285">Correzioni di bug nella versione 1.1</span><span class="sxs-lookup"><span data-stu-id="c7e58-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="c7e58-286">Si è verificato un bug nelle versioni precedenti di hello Azure Search .NET SDK di tooserialization relative classi di modello personalizzato.</span><span class="sxs-lookup"><span data-stu-id="c7e58-286">There was a bug in older versions of hello Azure Search .NET SDK relating tooserialization of custom model classes.</span></span> <span data-ttu-id="c7e58-287">bug Hello può verificarsi se una classe di modello personalizzato è stato creato con una proprietà di un tipo di valore non nullable.</span><span class="sxs-lookup"><span data-stu-id="c7e58-287">hello bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-tooreproduce"></a><span data-ttu-id="c7e58-288">Passaggi tooreproduce</span><span class="sxs-lookup"><span data-stu-id="c7e58-288">Steps tooreproduce</span></span>
<span data-ttu-id="c7e58-289">Creare una classe di modelli personalizzata con una proprietà di tipo di valore non nullable.</span><span class="sxs-lookup"><span data-stu-id="c7e58-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="c7e58-290">Ad esempio, aggiungere una proprietà pubblica `UnitCount` di tipo `int` invece che `int?`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="c7e58-291">Se un documento con il valore predefinito hello di quel tipo di indice (ad esempio, 0 per `int`), campo hello sarà null in ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="c7e58-291">If you index a document with hello default value of that type (for example, 0 for `int`), hello field will be null in Azure Search.</span></span> <span data-ttu-id="c7e58-292">Se successivamente esegue la ricerca per il documento, hello `Search` chiamata genererà `JsonSerializationException` che segnala che che non è possibile convertire `null` troppo`int`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-292">If you subsequently search for that document, hello `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` too`int`.</span></span>

<span data-ttu-id="c7e58-293">Inoltre, i filtri potrebbero non funzionare come previsto dopo la scrittura di indice toohello anziché il valore previsto hello null.</span><span class="sxs-lookup"><span data-stu-id="c7e58-293">Also, filters may not work as expected since null was written toohello index instead of hello intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="c7e58-294">Dettagli della correzione</span><span class="sxs-lookup"><span data-stu-id="c7e58-294">Fix details</span></span>
<span data-ttu-id="c7e58-295">Questo problema è stato risolto nella versione 1.1 di hello SDK.</span><span class="sxs-lookup"><span data-stu-id="c7e58-295">We have fixed this issue in version 1.1 of hello SDK.</span></span> <span data-ttu-id="c7e58-296">Se è presente una classe di modelli come questa:</span><span class="sxs-lookup"><span data-stu-id="c7e58-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="c7e58-297">e si imposta `IntValue` too0, che valore è ora correttamente serializzato come 0 in transito hello e archiviato come indice hello 0.</span><span class="sxs-lookup"><span data-stu-id="c7e58-297">and you set `IntValue` too0, that value is now correctly serialized as 0 on hello wire and stored as 0 in hello index.</span></span> <span data-ttu-id="c7e58-298">Anche il round trip funziona come previsto.</span><span class="sxs-lookup"><span data-stu-id="c7e58-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="c7e58-299">È compatibile con questo approccio richiede una toobe problema potenziale: se si utilizza un tipo di modello con una proprietà che non ammette valori null, è necessario troppo**garantire** che nessun documenti nell'indice contengono un valore null per il campo corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="c7e58-299">There is one potential issue toobe aware of with this approach: If you use a model type with a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="c7e58-300">Hello SDK né hello API REST di ricerca di Azure consentirà si tooenforce questo.</span><span class="sxs-lookup"><span data-stu-id="c7e58-300">Neither hello SDK nor hello Azure Search REST API will help you tooenforce this.</span></span>

<span data-ttu-id="c7e58-301">Non è un problema di ipotetica: si consideri uno scenario in cui aggiungere un nuovo campo tooan esistente indice di tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="c7e58-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="c7e58-302">Dopo aver aggiornato la definizione dell'indice hello, tutti i documenti avrà un valore null per il nuovo campo (poiché tutti i tipi nullable in ricerca di Azure).</span><span class="sxs-lookup"><span data-stu-id="c7e58-302">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="c7e58-303">Se si utilizza una classe di modello con un non-nullable `int` proprietà per il campo, si otterrà un `JsonSerializationException` simile durante il tentativo di tooretrieve documenti:</span><span class="sxs-lookup"><span data-stu-id="c7e58-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="c7e58-304">Per questo motivo, è ancora consigliabile usare tipi nullable nelle classi di modelli.</span><span class="sxs-lookup"><span data-stu-id="c7e58-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="c7e58-305">Per ulteriori informazioni su questa correzione di bug e hello, vedere [questo problema in GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="c7e58-305">For more details on this bug and hello fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

