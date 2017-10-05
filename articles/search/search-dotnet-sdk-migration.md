---
title: Aggiornamento ad Azure Search .NET SDK versione 1.1 | Documentazione Microsoft
description: Aggiornamento ad Azure Search .NET SDK versione 1.1
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
ms.openlocfilehash: 9782454e3bfc697b63cde8aa28a14be0c393c36b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="upgrading-to-the-azure-search-net-sdk-version-3"></a><span data-ttu-id="12f78-103">Aggiornamento ad Azure Search .NET SDK versione 3</span><span class="sxs-lookup"><span data-stu-id="12f78-103">Upgrading to the Azure Search .NET SDK version 3</span></span>
<span data-ttu-id="12f78-104">Se si usa la versione 2.0 di anteprima o precedente di [Azure Search .NET SDK](https://aka.ms/search-sdk), questo articolo include informazioni utili per aggiornare l'applicazione per l'uso della versione 3.</span><span class="sxs-lookup"><span data-stu-id="12f78-104">If you're using version 2.0-preview or older of the [Azure Search .NET SDK](https://aka.ms/search-sdk), this article will help you upgrade your application to use version 3.</span></span>

<span data-ttu-id="12f78-105">Per una procedura dettagliata più generale relativa all'SDK, inclusi gli esempi, vedere [Come usare Ricerca di Azure da un'applicazione .NET](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="12f78-105">For a more general walkthrough of the SDK including examples, see [How to use Azure Search from a .NET Application](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="12f78-106">La versione 3 di Azure Search .NET SDK contiene alcune modifiche rispetto alle versioni precedenti.</span><span class="sxs-lookup"><span data-stu-id="12f78-106">Version 3 of the Azure Search .NET SDK contains some changes from earlier versions.</span></span> <span data-ttu-id="12f78-107">ma per lo più secondarie, quindi il codice potrà essere modificato facilmente.</span><span class="sxs-lookup"><span data-stu-id="12f78-107">These are mostly minor, so changing your code should require only minimal effort.</span></span> <span data-ttu-id="12f78-108">Per le istruzioni su come modificare il codice per usare la nuova versione dell'SDK, vedere [Passaggi per eseguire l'aggiornamento](#UpgradeSteps) .</span><span class="sxs-lookup"><span data-stu-id="12f78-108">See [Steps to upgrade](#UpgradeSteps) for instructions on how to change your code to use the new SDK version.</span></span>

> [!NOTE]
> <span data-ttu-id="12f78-109">Se si usa la versione 1.0.2-preview o precedente, è consigliabile eseguire prima l'aggiornamento alla versione 1.1 e quindi l'aggiornamento alla versione 3.</span><span class="sxs-lookup"><span data-stu-id="12f78-109">If you're using version 1.0.2-preview or older, you should upgrade to version 1.1 first, and then upgrade to version 3.</span></span> <span data-ttu-id="12f78-110">Per informazioni, vedere [Appendice: Passaggi per l'aggiornamento alla versione 1.1](#UpgradeStepsV1) .</span><span class="sxs-lookup"><span data-stu-id="12f78-110">See [Appendix: Steps to upgrade to version 1.1](#UpgradeStepsV1) for instructions.</span></span>
>
> <span data-ttu-id="12f78-111">L'istanza del servizio Ricerca di Azure supporta diverse versioni di API REST, inclusa quella più recente.</span><span class="sxs-lookup"><span data-stu-id="12f78-111">Your Azure Search service instance supports several REST API versions, including the latest one.</span></span> <span data-ttu-id="12f78-112">È possibile continuare a usare una versione anche se non è la più recente, ma si consiglia di migrare il codice per usare la versione più recente.</span><span class="sxs-lookup"><span data-stu-id="12f78-112">You can continue to use a version when it is no longer the latest one, but we recommend that you migrate your code to use the newest version.</span></span> <span data-ttu-id="12f78-113">Quando si usa l'API REST, è necessario specificare la versione dell'API in tutte le richieste tramite il parametro api-version.</span><span class="sxs-lookup"><span data-stu-id="12f78-113">When using the REST API, you must specify the API version in every request via the api-version parameter.</span></span> <span data-ttu-id="12f78-114">Quando si usa .NET SDK, la versione del componente SDK in uso determina la versione corrispondente dell'API REST.</span><span class="sxs-lookup"><span data-stu-id="12f78-114">When using the .NET SDK, the version of the SDK you’re using determines the corresponding version of the REST API.</span></span> <span data-ttu-id="12f78-115">Se si usa una versione del componente SDK precedente, è possibile continuare a eseguire il codice senza apportare modifiche, anche se il servizio viene aggiornato per supportare una versione API più recente.</span><span class="sxs-lookup"><span data-stu-id="12f78-115">If you are using an older SDK, you can continue to run that code with no changes even if the service is upgraded to support a newer API version.</span></span>

<a name="WhatsNew"></a>

## <a name="whats-new-in-version-3"></a><span data-ttu-id="12f78-116">Novità della versione 3</span><span class="sxs-lookup"><span data-stu-id="12f78-116">What's new in version 3</span></span>
<span data-ttu-id="12f78-117">La versione 3 di Azure Search .NET SDK ha come destinazione la versione più recente disponibile a livello generale dell'API REST di Ricerca di Azure, in particolare la versione 2016-09-01.</span><span class="sxs-lookup"><span data-stu-id="12f78-117">Version 3 of the Azure Search .NET SDK targets the latest generally available version of the Azure Search REST API, specifically 2016-09-01.</span></span> <span data-ttu-id="12f78-118">Questo rende possibile usare molte nuove funzionalità di Ricerca di Azure da un'applicazione .NET, incluse le seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f78-118">This makes it possible to use many new features of Azure Search from a .NET application, including the following:</span></span>

* [<span data-ttu-id="12f78-119">Analizzatori personalizzati</span><span class="sxs-lookup"><span data-stu-id="12f78-119">Custom analyzers</span></span>](https://aka.ms/customanalyzers)
* <span data-ttu-id="12f78-120">Supporto per gli indicizzatori di [Archiviazione BLOB di Azure](search-howto-indexing-azure-blob-storage.md) e [Archiviazione tabelle di Azure](search-howto-indexing-azure-tables.md)</span><span class="sxs-lookup"><span data-stu-id="12f78-120">[Azure Blob Storage](search-howto-indexing-azure-blob-storage.md) and [Azure Table Storage](search-howto-indexing-azure-tables.md) indexer support</span></span>
* <span data-ttu-id="12f78-121">Personalizzazione dell'indicizzatore tramite [mapping dei campi](search-indexer-field-mappings.md)</span><span class="sxs-lookup"><span data-stu-id="12f78-121">Indexer customization via [field mappings](search-indexer-field-mappings.md)</span></span>
* <span data-ttu-id="12f78-122">Supporto di eTag per consentire l'aggiornamento simultaneo sicuro di definizioni di indice, indicizzatori e origini dati</span><span class="sxs-lookup"><span data-stu-id="12f78-122">ETags support to enable safe concurrent updating of index definitions, indexers, and data sources</span></span>
* <span data-ttu-id="12f78-123">Supporto per la creazione di definizioni dei campi di indice in modo dichiarativo, decorando la classe modello e usando la nuova classe `FieldBuilder`.</span><span class="sxs-lookup"><span data-stu-id="12f78-123">Support for building index field definitions declaratively by decorating your model class and using the new `FieldBuilder` class.</span></span>
* <span data-ttu-id="12f78-124">Supporto per .NET Core e .NET Portable Profile 111</span><span class="sxs-lookup"><span data-stu-id="12f78-124">Support for .NET Core and .NET Portable Profile 111</span></span>

<a name="UpgradeSteps"></a>

## <a name="steps-to-upgrade"></a><span data-ttu-id="12f78-125">Passaggi per eseguire l'aggiornamento</span><span class="sxs-lookup"><span data-stu-id="12f78-125">Steps to upgrade</span></span>
<span data-ttu-id="12f78-126">Per prima cosa aggiornare il riferimento a NuGet per `Microsoft.Azure.Search` usando NuGet Package Manager Console o facendo clic con il pulsante destro del mouse sui riferimenti di progetto e scegliendo "Gestisci pacchetti NuGet" in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12f78-126">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="12f78-127">Una volta che NuGet ha scaricato i nuovi pacchetti e le relative dipendenze, ricompilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="12f78-127">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span> <span data-ttu-id="12f78-128">A seconda della struttura del codice, la ricompilazione potrebbe essere eseguita correttamente.</span><span class="sxs-lookup"><span data-stu-id="12f78-128">Depending on how your code is structured, it may rebuild successfully.</span></span> <span data-ttu-id="12f78-129">In questo caso è possibile procedere.</span><span class="sxs-lookup"><span data-stu-id="12f78-129">If so, you're ready to go!</span></span>

<span data-ttu-id="12f78-130">Se la compilazione non riesce, viene visualizzato un errore di compilazione simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="12f78-130">If your build fails, you should see a build error like the following:</span></span>

    Program.cs(31,45,31,86): error CS0266: Cannot implicitly convert type 'Microsoft.Azure.Search.ISearchIndexClient' to 'Microsoft.Azure.Search.SearchIndexClient'. An explicit conversion exists (are you missing a cast?)

<span data-ttu-id="12f78-131">Il passaggio successivo consiste nel correggere l'errore di compilazione.</span><span class="sxs-lookup"><span data-stu-id="12f78-131">The next step is to fix this build error.</span></span> <span data-ttu-id="12f78-132">Vedere [Modifiche di rilievo della versione 3](#ListOfChanges) per informazioni dettagliate sulle cause dell'errore e sulla risoluzione.</span><span class="sxs-lookup"><span data-stu-id="12f78-132">See [Breaking changes in version 3](#ListOfChanges) for details on what causes the error and how to fix it.</span></span>

<span data-ttu-id="12f78-133">È possibile che vengano visualizzati avvisi di compilazione aggiuntivi correlati a proprietà o metodi obsoleti.</span><span class="sxs-lookup"><span data-stu-id="12f78-133">You may see additional build warnings related to obsolete methods or properties.</span></span> <span data-ttu-id="12f78-134">Gli avvisi indicheranno istruzioni sulle operazioni da eseguire al posto della funzionalità deprecata.</span><span class="sxs-lookup"><span data-stu-id="12f78-134">The warnings will include instructions on what to use instead of the deprecated feature.</span></span> <span data-ttu-id="12f78-135">Ad esempio, se l'applicazione usa la proprietà `IndexingParameters.Base64EncodeKeys`, dovrebbe essere visualizzato l'avviso `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span><span class="sxs-lookup"><span data-stu-id="12f78-135">For example, if your application uses the `IndexingParameters.Base64EncodeKeys` property, you should get a warning that says `"This property is obsolete. Please create a field mapping using 'FieldMapping.Base64Encode' instead."`</span></span>

<span data-ttu-id="12f78-136">Dopo avere corretto gli errori di compilazione, è possibile apportare modifiche all'applicazione per sfruttare la nuova funzionalità, se si vuole.</span><span class="sxs-lookup"><span data-stu-id="12f78-136">Once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span> <span data-ttu-id="12f78-137">Le nuove funzionalità nell'SDK sono descritte in dettaglio in [Novità della versione 3](#WhatsNew).</span><span class="sxs-lookup"><span data-stu-id="12f78-137">New features in the SDK are detailed in [What's new in version 3](#WhatsNew).</span></span>

<a name="ListOfChanges"></a>

## <a name="breaking-changes-in-version-3"></a><span data-ttu-id="12f78-138">Modifiche di rilievo nella versione 3</span><span class="sxs-lookup"><span data-stu-id="12f78-138">Breaking changes in version 3</span></span>
<span data-ttu-id="12f78-139">La versione 3 include poche modifiche di rilievo che potrebbero richiedere modifiche al codice oltre alla ricompilazione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="12f78-139">There a small number of breaking changes in version 3 that may require code changes in addition to rebuilding your application.</span></span>

### <a name="indexesgetclient-return-type"></a><span data-ttu-id="12f78-140">Tipo restituito Indexes.GetClient</span><span class="sxs-lookup"><span data-stu-id="12f78-140">Indexes.GetClient return type</span></span>
<span data-ttu-id="12f78-141">Il metodo `Indexes.GetClient` dispone di un nuovo tipo restituito.</span><span class="sxs-lookup"><span data-stu-id="12f78-141">The `Indexes.GetClient` method has a new return type.</span></span> <span data-ttu-id="12f78-142">In precedenza, veniva restituito `SearchIndexClient`, ma questo valore è stato modificato in `ISearchIndexClient` nella versione 2.0-preview e questa modifica è ancora presente nella versione 3.</span><span class="sxs-lookup"><span data-stu-id="12f78-142">Previously, it returned `SearchIndexClient`, but this was changed to `ISearchIndexClient` in version 2.0-preview, and that change carries over to version 3.</span></span> <span data-ttu-id="12f78-143">Serve a supportare i clienti che vogliono simulare il metodo `GetClient` per i test di unità tramite la restituzione di un'implementazione fittizia di `ISearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="12f78-143">This is to support customers that wish to mock the `GetClient` method for unit tests by returning a mock implementation of `ISearchIndexClient`.</span></span>

#### <a name="example"></a><span data-ttu-id="12f78-144">Esempio</span><span class="sxs-lookup"><span data-stu-id="12f78-144">Example</span></span>
<span data-ttu-id="12f78-145">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="12f78-145">If your code looks like this:</span></span>

```csharp
SearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

<span data-ttu-id="12f78-146">È possibile sostituirlo con questo per correggere gli errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="12f78-146">You can change it to this to fix any build errors:</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

### <a name="analyzername-datatype-and-others-are-no-longer-implicitly-convertible-to-strings"></a><span data-ttu-id="12f78-147">AnalyzerName, DataType e altri tipi non possono più essere convertiti in modo implicito in stringhe</span><span class="sxs-lookup"><span data-stu-id="12f78-147">AnalyzerName, DataType, and others are no longer implicitly convertible to strings</span></span>
<span data-ttu-id="12f78-148">Esistono molti tipi in Azure Search .NET SDK che derivano da `ExtensibleEnum`.</span><span class="sxs-lookup"><span data-stu-id="12f78-148">There are many types in the Azure Search .NET SDK that derive from `ExtensibleEnum`.</span></span> <span data-ttu-id="12f78-149">In precedenza, questi tipi erano tutti convertibili in modo implicito nel tipo `string`.</span><span class="sxs-lookup"><span data-stu-id="12f78-149">Previously these types were all implicitly convertible to type `string`.</span></span> <span data-ttu-id="12f78-150">Tuttavia, è stato rilevato un bug nell'implementazione di `Object.Equals` per queste classi e per correggere il bug è stato necessario disabilitare la conversione implicita.</span><span class="sxs-lookup"><span data-stu-id="12f78-150">However, a bug was discovered in the `Object.Equals` implementation for these classes, and fixing the bug required disabling this implicit conversion.</span></span> <span data-ttu-id="12f78-151">La conversione esplicita in `string` è ancora consentita.</span><span class="sxs-lookup"><span data-stu-id="12f78-151">Explicit conversion to `string` is still allowed.</span></span>

#### <a name="example"></a><span data-ttu-id="12f78-152">Esempio</span><span class="sxs-lookup"><span data-stu-id="12f78-152">Example</span></span>
<span data-ttu-id="12f78-153">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="12f78-153">If your code looks like this:</span></span>

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

<span data-ttu-id="12f78-154">È possibile sostituirlo con questo per correggere gli errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="12f78-154">You can change it to this to fix any build errors:</span></span>

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

### <a name="removed-obsolete-members"></a><span data-ttu-id="12f78-155">Rimuovere i membri obsoleti</span><span class="sxs-lookup"><span data-stu-id="12f78-155">Removed obsolete members</span></span>

<span data-ttu-id="12f78-156">È possibile che vengano visualizzati errori di compilazione correlati a metodi o proprietà contrassegnati come obsoleti nella versione 2.0-preview e successivamente rimossi nella versione 3.</span><span class="sxs-lookup"><span data-stu-id="12f78-156">You may see build errors related to methods or properties that were marked as obsolete in version 2.0-preview and subsequently removed in version 3.</span></span> <span data-ttu-id="12f78-157">Se si verificano tali errori, ecco come risolverli:</span><span class="sxs-lookup"><span data-stu-id="12f78-157">If you encounter such errors, here is how to resolve them:</span></span>

- <span data-ttu-id="12f78-158">Se l'errore riguarda il costruttore `ScoringParameter(string name, string value)`, sostituirlo con `ScoringParameter(string name, IEnumerable<string> values)`</span><span class="sxs-lookup"><span data-stu-id="12f78-158">If you were using this constructor: `ScoringParameter(string name, string value)`, use this one instead: `ScoringParameter(string name, IEnumerable<string> values)`</span></span>
- <span data-ttu-id="12f78-159">Se l'errore riguarda la proprietà `ScoringParameter.Value`, sostituirla con la proprietà `ScoringParameter.Values` o il metodo `ToString`.</span><span class="sxs-lookup"><span data-stu-id="12f78-159">If you were using the `ScoringParameter.Value` property, use the `ScoringParameter.Values` property or the `ToString` method instead.</span></span>
- <span data-ttu-id="12f78-160">Se l'errore riguarda la proprietà `SearchRequestOptions.RequestId`, sostituirla con la proprietà `ClientRequestId`.</span><span class="sxs-lookup"><span data-stu-id="12f78-160">If you were using the `SearchRequestOptions.RequestId` property, use the `ClientRequestId` property instead.</span></span>

### <a name="removed-preview-features"></a><span data-ttu-id="12f78-161">Funzionalità di anteprima rimosse</span><span class="sxs-lookup"><span data-stu-id="12f78-161">Removed preview features</span></span>

<span data-ttu-id="12f78-162">Se esegue l'aggiornamento dalla versione 2.0-preview alla versione 3, tenere presente che è stato rimosso il supporto dell'analisi JSON e CSV per gli indicizzatori BLOB, perché queste funzionalità sono ancora in anteprima.</span><span class="sxs-lookup"><span data-stu-id="12f78-162">If you are upgrading from version 2.0-preview to version 3, be aware that JSON and CSV parsing support for Blob Indexers has been removed since these features are still in preview.</span></span> <span data-ttu-id="12f78-163">In particolare, sono stati rimossi i metodi seguenti della classe `IndexingParametersExtensions`:</span><span class="sxs-lookup"><span data-stu-id="12f78-163">Specifically, the following methods of the `IndexingParametersExtensions` class have been removed:</span></span>

- `ParseJson`
- `ParseJsonArrays`
- `ParseDelimitedTextFiles`

<span data-ttu-id="12f78-164">Se l'applicazione dipende in modo sostanziale da queste funzionalità, non sarà possibile completare l'aggiornamento alla versione 3 di Azure Search .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="12f78-164">If your application has a hard dependency on these features, you will not be able to upgrade to version 3 of the Azure Search .NET SDK.</span></span> <span data-ttu-id="12f78-165">È possibile continuare a usare la versione 2.0-preview.</span><span class="sxs-lookup"><span data-stu-id="12f78-165">You can continue to use version 2.0-preview.</span></span> <span data-ttu-id="12f78-166">Tenere presente, tuttavia, che **non è consigliabile usare SDK in anteprima nelle applicazioni di produzione**.</span><span class="sxs-lookup"><span data-stu-id="12f78-166">However, please keep in mind that **we do not recommend using preview SDKs in production applications**.</span></span> <span data-ttu-id="12f78-167">Le funzionalità di anteprima sono destinate esclusivamente alla valutazione e sono soggette a modifiche.</span><span class="sxs-lookup"><span data-stu-id="12f78-167">Preview features are for evaluation only and may change.</span></span>

## <a name="conclusion"></a><span data-ttu-id="12f78-168">Conclusione</span><span class="sxs-lookup"><span data-stu-id="12f78-168">Conclusion</span></span>
<span data-ttu-id="12f78-169">Per altri dettagli sull'uso di Azure Search .NET SDK, vedere gli articoli aggiornati di recente contenenti le [procedure](search-howto-dotnet-sdk.md).</span><span class="sxs-lookup"><span data-stu-id="12f78-169">If you need more details on using the Azure Search .NET SDK, see our recently updated [How-to](search-howto-dotnet-sdk.md).</span></span>

<span data-ttu-id="12f78-170">I commenti degli utenti sull'SDK saranno molto apprezzati.</span><span class="sxs-lookup"><span data-stu-id="12f78-170">We welcome your feedback on the SDK.</span></span> <span data-ttu-id="12f78-171">In caso di problemi, è possibile richiedere assistenza nel [forum MSDN su Ricerca di Azure](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span><span class="sxs-lookup"><span data-stu-id="12f78-171">If you encounter problems, feel free to ask us for help on the [Azure Search MSDN forum](https://social.msdn.microsoft.com/Forums/azure/home?forum=azuresearch).</span></span> <span data-ttu-id="12f78-172">Se si trova un bug, è possibile registrare il problema nel [repository di GitHub su Azure .NET SDK](https://github.com/Azure/azure-sdk-for-net/issues).</span><span class="sxs-lookup"><span data-stu-id="12f78-172">If you find a bug, you can file an issue in the [Azure .NET SDK GitHub repository](https://github.com/Azure/azure-sdk-for-net/issues).</span></span> <span data-ttu-id="12f78-173">Verificare di avere anteposto al titolo del problema il prefisso "Search SDK: ".</span><span class="sxs-lookup"><span data-stu-id="12f78-173">Make sure to prefix your issue title with "Search SDK: ".</span></span>

<span data-ttu-id="12f78-174">Grazie per avere usato Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="12f78-174">Thank you for using Azure Search!</span></span>

<a name="UpgradeStepsV1"></a>

## <a name="appendix-steps-to-upgrade-to-version-11"></a><span data-ttu-id="12f78-175">Appendice: Passaggi per l'aggiornamento alla versione 1.1</span><span class="sxs-lookup"><span data-stu-id="12f78-175">Appendix: Steps to upgrade to version 1.1</span></span>
> [!NOTE]
> <span data-ttu-id="12f78-176">Questa sezione si applica solo agli utenti di Azure Search .NET SDK versione 1.0.2-preview e precedenti.</span><span class="sxs-lookup"><span data-stu-id="12f78-176">This section applies only to users of the Azure Search .NET SDK version 1.0.2-preview and older.</span></span>
> 
> 

<span data-ttu-id="12f78-177">Per prima cosa aggiornare il riferimento a NuGet per `Microsoft.Azure.Search` usando NuGet Package Manager Console o facendo clic con il pulsante destro del mouse sui riferimenti di progetto e scegliendo "Gestisci pacchetti NuGet" in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="12f78-177">First, update your NuGet reference for `Microsoft.Azure.Search` using either the NuGet Package Manager Console or by right-clicking on your project references and selecting "Manage NuGet Packages..." in Visual Studio.</span></span>

<span data-ttu-id="12f78-178">Una volta che NuGet ha scaricato i nuovi pacchetti e le relative dipendenze, ricompilare il progetto.</span><span class="sxs-lookup"><span data-stu-id="12f78-178">Once NuGet has downloaded the new packages and their dependencies, rebuild your project.</span></span>

<span data-ttu-id="12f78-179">Se in precedenza si usava la versione 1.0.0 di anteprima, la versione 1.0.1 di anteprima o la versione 1.0.2 di anteprima, la compilazione dovrebbe avere esito positivo e tutto dovrebbe essere pronto per iniziare.</span><span class="sxs-lookup"><span data-stu-id="12f78-179">If you were previously using version 1.0.0-preview, 1.0.1-preview, or 1.0.2-preview, the build should succeed and you're ready to go!</span></span>

<span data-ttu-id="12f78-180">Se in precedenza si usava versione 0.13.0 di anteprima o una versione precedente, la compilazione dovrebbe generare errori simili ai seguenti:</span><span class="sxs-lookup"><span data-stu-id="12f78-180">If you were previously using version 0.13.0-preview or older, you should see build errors like the following:</span></span>

    Program.cs(137,56,137,62): error CS0117: 'Microsoft.Azure.Search.Models.IndexBatch' does not contain a definition for 'Create'
    Program.cs(137,99,137,105): error CS0117: 'Microsoft.Azure.Search.Models.IndexAction' does not contain a definition for 'Create'
    Program.cs(146,41,146,54): error CS1061: 'Microsoft.Azure.Search.IndexBatchException' does not contain a definition for 'IndexResponse' and no extension method 'IndexResponse' accepting a first argument of type 'Microsoft.Azure.Search.IndexBatchException' could be found (are you missing a using directive or an assembly reference?)
    Program.cs(163,13,163,42): error CS0246: The type or namespace name 'DocumentSearchResponse' could not be found (are you missing a using directive or an assembly reference?)

<span data-ttu-id="12f78-181">Il passaggio successivo consiste nel correggere gli errori di compilazione uno alla volta.</span><span class="sxs-lookup"><span data-stu-id="12f78-181">The next step is to fix the build errors one by one.</span></span> <span data-ttu-id="12f78-182">La maggior parte richiederà di modificare alcuni nomi di classe e di metodo rinominati nell'SDK.</span><span class="sxs-lookup"><span data-stu-id="12f78-182">Most will require changing some class and method names that have been renamed in the SDK.</span></span> <span data-ttu-id="12f78-183">[Elenco di modifiche di rilievo nella versione 1.1](#ListOfChangesV1) contiene l'elenco delle modifiche dei nomi.</span><span class="sxs-lookup"><span data-stu-id="12f78-183">[List of breaking changes in version 1.1](#ListOfChangesV1) contains a list of these name changes.</span></span>

<span data-ttu-id="12f78-184">Se si usano classi personalizzate per modellare i documenti e tali classi hanno proprietà di tipi primitivi non nullable, ad esempio, `int` o `bool` in C#, nella versione 1.1 dell'SDK è presente una correzione di bug che è opportuno conoscere.</span><span class="sxs-lookup"><span data-stu-id="12f78-184">If you're using custom classes to model your documents, and those classes have properties of non-nullable primitive types (for example, `int` or `bool` in C#), there is a bug fix in the 1.1 version of the SDK of which you should be aware.</span></span> <span data-ttu-id="12f78-185">Per altri dettagli, vedere [Correzioni di bug nella versione 1.1](#BugFixesV1) .</span><span class="sxs-lookup"><span data-stu-id="12f78-185">See [Bug fixes in version 1.1](#BugFixesV1) for more details.</span></span>

<span data-ttu-id="12f78-186">Infine, dopo avere corretto gli errori di compilazione, è possibile apportare modifiche all'applicazione per sfruttare la nuova funzionalità, se si vuole.</span><span class="sxs-lookup"><span data-stu-id="12f78-186">Finally, once you've fixed any build errors, you can make changes to your application to take advantage of new functionality if you wish.</span></span>

<a name="ListOfChangesV1"></a>

### <a name="list-of-breaking-changes-in-version-11"></a><span data-ttu-id="12f78-187">Elenco di modifiche di rilievo nella versione 1.1</span><span class="sxs-lookup"><span data-stu-id="12f78-187">List of breaking changes in version 1.1</span></span>
<span data-ttu-id="12f78-188">L'ordinamento dell'elenco seguente segue la probabilità che la modifica abbia effetto sul codice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="12f78-188">The following list is ordered by the likelihood that the change will affect your application code.</span></span>

#### <a name="indexbatch-and-indexaction-changes"></a><span data-ttu-id="12f78-189">Modifiche a IndexBatch e IndexAction</span><span class="sxs-lookup"><span data-stu-id="12f78-189">IndexBatch and IndexAction changes</span></span>
<span data-ttu-id="12f78-190">`IndexBatch.Create` è stato rinominato `IndexBatch.New` e non include più un argomento `params`.</span><span class="sxs-lookup"><span data-stu-id="12f78-190">`IndexBatch.Create` has been renamed to `IndexBatch.New` and no longer has a `params` argument.</span></span> <span data-ttu-id="12f78-191">È possibile usare `IndexBatch.New` per i batch che combinano tipi diversi di azioni (unioni, eliminazioni e così via).</span><span class="sxs-lookup"><span data-stu-id="12f78-191">You can use `IndexBatch.New` for batches that mix different types of actions (merges, deletes, etc.).</span></span> <span data-ttu-id="12f78-192">Sono anche presenti nuovi metodi statici per creare batch in cui tutte le azioni sono le stesse: `Delete`, `Merge`, `MergeOrUpload` e `Upload`.</span><span class="sxs-lookup"><span data-stu-id="12f78-192">In addition, there are new static methods for creating batches where all the actions are the same: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span>

<span data-ttu-id="12f78-193">`IndexAction` non include più costruttori pubblici e le proprietà ora sono non modificabili.</span><span class="sxs-lookup"><span data-stu-id="12f78-193">`IndexAction` no longer has public constructors and its properties are now immutable.</span></span> <span data-ttu-id="12f78-194">È consigliabile usare i nuovi metodi statici per creare azioni con scopi diversi: `Delete`, `Merge`, `MergeOrUpload` e `Upload`.</span><span class="sxs-lookup"><span data-stu-id="12f78-194">You should use the new static methods for creating actions for different purposes: `Delete`, `Merge`, `MergeOrUpload`, and `Upload`.</span></span> <span data-ttu-id="12f78-195">`IndexAction.Create` è stato rimosso.</span><span class="sxs-lookup"><span data-stu-id="12f78-195">`IndexAction.Create` has been removed.</span></span> <span data-ttu-id="12f78-196">Se si è usato l'overload che accetta un solo documento, verificare di usare invece `Upload` .</span><span class="sxs-lookup"><span data-stu-id="12f78-196">If you used the overload that takes only a document, make sure to use `Upload` instead.</span></span>

##### <a name="example"></a><span data-ttu-id="12f78-197">Esempio</span><span class="sxs-lookup"><span data-stu-id="12f78-197">Example</span></span>
<span data-ttu-id="12f78-198">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="12f78-198">If your code looks like this:</span></span>

    var batch = IndexBatch.Create(documents.Select(doc => IndexAction.Create(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="12f78-199">È possibile sostituirlo con questo per correggere gli errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="12f78-199">You can change it to this to fix any build errors:</span></span>

    var batch = IndexBatch.New(documents.Select(doc => IndexAction.Upload(doc)));
    indexClient.Documents.Index(batch);

<span data-ttu-id="12f78-200">Se si vuole, è possibile semplificarlo ulteriormente in questo modo:</span><span class="sxs-lookup"><span data-stu-id="12f78-200">If you want, you can further simplify it to this:</span></span>

    var batch = IndexBatch.Upload(documents);
    indexClient.Documents.Index(batch);

#### <a name="indexbatchexception-changes"></a><span data-ttu-id="12f78-201">Modifiche a IndexBatchException</span><span class="sxs-lookup"><span data-stu-id="12f78-201">IndexBatchException changes</span></span>
<span data-ttu-id="12f78-202">La proprietà `IndexBatchException.IndexResponse` è stata rinominata `IndexingResults` e il tipo ora è `IList<IndexingResult>`.</span><span class="sxs-lookup"><span data-stu-id="12f78-202">The `IndexBatchException.IndexResponse` property has been renamed to `IndexingResults`, and its type is now `IList<IndexingResult>`.</span></span>

##### <a name="example"></a><span data-ttu-id="12f78-203">Esempio</span><span class="sxs-lookup"><span data-stu-id="12f78-203">Example</span></span>
<span data-ttu-id="12f78-204">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="12f78-204">If your code looks like this:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexResponse.Results.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<span data-ttu-id="12f78-205">È possibile sostituirlo con questo per correggere gli errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="12f78-205">You can change it to this to fix any build errors:</span></span>

    catch (IndexBatchException e)
    {
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

<a name="OperationMethodChanges"></a>

#### <a name="operation-method-changes"></a><span data-ttu-id="12f78-206">Modifiche ai metodi delle operazioni</span><span class="sxs-lookup"><span data-stu-id="12f78-206">Operation method changes</span></span>
<span data-ttu-id="12f78-207">Ogni operazione in Azure Search .NET SDK è esposta come set di overload di un metodo per i chiamanti sincroni e asincroni.</span><span class="sxs-lookup"><span data-stu-id="12f78-207">Each operation in the Azure Search .NET SDK is exposed as a set of method overloads for synchronous and asynchronous callers.</span></span> <span data-ttu-id="12f78-208">Le firme e il factoring di questi overload del metodo sono stati modificati nella versione 1.1.</span><span class="sxs-lookup"><span data-stu-id="12f78-208">The signatures and factoring of these method overloads has changed in version 1.1.</span></span>

<span data-ttu-id="12f78-209">Ad esempio, l'operazione "Get Index Statistics" nelle versioni precedenti dell'SDK espone queste firme:</span><span class="sxs-lookup"><span data-stu-id="12f78-209">For example, the "Get Index Statistics" operation in older versions of the SDK exposed these signatures:</span></span>

<span data-ttu-id="12f78-210">In `IIndexOperations`:</span><span class="sxs-lookup"><span data-stu-id="12f78-210">In `IIndexOperations`:</span></span>

    // Asynchronous operation with all parameters
    Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        string indexName,
        CancellationToken cancellationToken);

<span data-ttu-id="12f78-211">In `IndexOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="12f78-211">In `IndexOperationsExtensions`:</span></span>

    // Asynchronous operation with only required parameters
    public static Task<IndexGetStatisticsResponse> GetStatisticsAsync(
        this IIndexOperations operations,
        string indexName);

    // Synchronous operation with only required parameters
    public static IndexGetStatisticsResponse GetStatistics(
        this IIndexOperations operations,
        string indexName);

<span data-ttu-id="12f78-212">Le firme dei metodi per la stessa operazione nella versione 1.1 sono simili a questa:</span><span class="sxs-lookup"><span data-stu-id="12f78-212">The method signatures for the same operation in version 1.1 look like this:</span></span>

<span data-ttu-id="12f78-213">In `IIndexesOperations`:</span><span class="sxs-lookup"><span data-stu-id="12f78-213">In `IIndexesOperations`:</span></span>

    // Asynchronous operation with lower-level HTTP features exposed
    Task<AzureOperationResponse<IndexGetStatisticsResult>> GetStatisticsWithHttpMessagesAsync(
        string indexName,
        SearchRequestOptions searchRequestOptions = default(SearchRequestOptions),
        Dictionary<string, List<string>> customHeaders = null,
        CancellationToken cancellationToken = default(CancellationToken));

<span data-ttu-id="12f78-214">In `IndexesOperationsExtensions`:</span><span class="sxs-lookup"><span data-stu-id="12f78-214">In `IndexesOperationsExtensions`:</span></span>

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

<span data-ttu-id="12f78-215">A partire dalla versione 1.1, Azure Search .NET SDK organizza i metodi delle operazioni in modo diverso:</span><span class="sxs-lookup"><span data-stu-id="12f78-215">Starting with version 1.1, the Azure Search .NET SDK organizes operation methods differently:</span></span>

* <span data-ttu-id="12f78-216">I parametri facoltativi ora vengono modellati come parametri predefiniti invece che come overload dei metodi aggiuntivi.</span><span class="sxs-lookup"><span data-stu-id="12f78-216">Optional parameters are now modeled as default parameters rather than additional method overloads.</span></span> <span data-ttu-id="12f78-217">Questo riduce, in alcuni casi anche considerevolmente, il numero di overload dei metodi.</span><span class="sxs-lookup"><span data-stu-id="12f78-217">This reduces the number of method overloads, sometimes dramatically.</span></span>
* <span data-ttu-id="12f78-218">I metodi di estensione ora nascondono al chiamante numerosi dettagli estranei di HTTP.</span><span class="sxs-lookup"><span data-stu-id="12f78-218">The extension methods now hide a lot of the extraneous details of HTTP from the caller.</span></span> <span data-ttu-id="12f78-219">Ad esempio, le versioni precedenti dell'SDK restituiscono un oggetto risposta con un codice di stato HTTP, che spesso non è necessario controllare perché i metodi delle operazioni generano `CloudException` per tutti i codici di stato indicanti un errore.</span><span class="sxs-lookup"><span data-stu-id="12f78-219">For example, older versions of the SDK returned a response object with an HTTP status code, which you often didn't need to check because operation methods throw `CloudException` for any status code that indicates an error.</span></span> <span data-ttu-id="12f78-220">I nuovi metodi di estensione restituiscono solo oggetti modello, evitando il fastidio di doverne annullare il wrapping nel codice.</span><span class="sxs-lookup"><span data-stu-id="12f78-220">The new extension methods just return model objects, saving you the trouble of having to unwrap them in your code.</span></span>
* <span data-ttu-id="12f78-221">Al contrario, le interfacce principali ora espongono metodi che offrono un maggiore controllo a livello HTTP, se necessario.</span><span class="sxs-lookup"><span data-stu-id="12f78-221">Conversely, the core interfaces now expose methods that give you more control at the HTTP level if you need it.</span></span> <span data-ttu-id="12f78-222">Ora è possibile passare le intestazioni HTTP personalizzate da includere nelle richieste e il nuovo tipo restituito `AzureOperationResponse<T>` consente l'accesso diretto a `HttpRequestMessage` e a `HttpResponseMessage` per l'operazione.</span><span class="sxs-lookup"><span data-stu-id="12f78-222">You can now pass in custom HTTP headers to be included in requests, and the new `AzureOperationResponse<T>` return type gives you direct access to the `HttpRequestMessage` and `HttpResponseMessage` for the operation.</span></span> <span data-ttu-id="12f78-223">`AzureOperationResponse` è definito nello spazio dei nomi `Microsoft.Rest.Azure` e sostituisce `Hyak.Common.OperationResponse`.</span><span class="sxs-lookup"><span data-stu-id="12f78-223">`AzureOperationResponse` is defined in the `Microsoft.Rest.Azure` namespace and replaces `Hyak.Common.OperationResponse`.</span></span>

#### <a name="scoringparameters-changes"></a><span data-ttu-id="12f78-224">Modifiche a ScoringParameters</span><span class="sxs-lookup"><span data-stu-id="12f78-224">ScoringParameters changes</span></span>
<span data-ttu-id="12f78-225">Una nuova classe denominata `ScoringParameter` è stata aggiunta alla versione più recente dell'SDK per semplificare la specifica di parametri per i profili di punteggio in una query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="12f78-225">A new class named `ScoringParameter` has been added in the latest SDK to make it easier to provide parameters to scoring profiles in a search query.</span></span> <span data-ttu-id="12f78-226">In precedenza la proprietà `ScoringProfiles` della classe `SearchParameters` veniva tipizzata come `IList<string>`. Ora viene tipizzata come `IList<ScoringParameter>`.</span><span class="sxs-lookup"><span data-stu-id="12f78-226">Previously the `ScoringProfiles` property of the `SearchParameters` class was typed as `IList<string>`; Now it is typed as `IList<ScoringParameter>`.</span></span>

##### <a name="example"></a><span data-ttu-id="12f78-227">Esempio</span><span class="sxs-lookup"><span data-stu-id="12f78-227">Example</span></span>
<span data-ttu-id="12f78-228">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="12f78-228">If your code looks like this:</span></span>

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters = new[] { "featuredParam-featured", "mapCenterParam-" + lon + "," + lat };

<span data-ttu-id="12f78-229">È possibile sostituirlo con questo per correggere gli errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="12f78-229">You can change it to this to fix any build errors:</span></span> 

    var sp = new SearchParameters();
    sp.ScoringProfile = "jobsScoringFeatured";      // Use a scoring profile
    sp.ScoringParameters =
        new[]
        {
            new ScoringParameter("featuredParam", new[] { "featured" }),
            new ScoringParameter("mapCenterParam", GeographyPoint.Create(lat, lon))
        };

#### <a name="model-class-changes"></a><span data-ttu-id="12f78-230">Modifiche alle classi di modelli</span><span class="sxs-lookup"><span data-stu-id="12f78-230">Model class changes</span></span>
<span data-ttu-id="12f78-231">In seguito alle modifiche apportate alle firme descritte in [Modifiche ai metodi delle operazioni](#OperationMethodChanges), molte classi nello spazio dei nomi `Microsoft.Azure.Search.Models` sono state rinominate o rimosse.</span><span class="sxs-lookup"><span data-stu-id="12f78-231">Due to the signature changes described in [Operation method changes](#OperationMethodChanges), many classes in the `Microsoft.Azure.Search.Models` namespace have been renamed or removed.</span></span> <span data-ttu-id="12f78-232">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="12f78-232">For example:</span></span>

* <span data-ttu-id="12f78-233">`IndexDefinitionResponse` è stata sostituita da `AzureOperationResponse<Index>`</span><span class="sxs-lookup"><span data-stu-id="12f78-233">`IndexDefinitionResponse` has been replaced by `AzureOperationResponse<Index>`</span></span>
* <span data-ttu-id="12f78-234">`DocumentSearchResponse` è stata rinominata `DocumentSearchResult`</span><span class="sxs-lookup"><span data-stu-id="12f78-234">`DocumentSearchResponse` has been renamed to `DocumentSearchResult`</span></span>
* <span data-ttu-id="12f78-235">`IndexResult` è stata rinominata `IndexingResult`</span><span class="sxs-lookup"><span data-stu-id="12f78-235">`IndexResult` has been renamed to `IndexingResult`</span></span>
* <span data-ttu-id="12f78-236">`Documents.Count()` ora restituisce `long` con il conteggio dei documenti invece di `DocumentCountResponse`</span><span class="sxs-lookup"><span data-stu-id="12f78-236">`Documents.Count()` now returns a `long` with the document count instead of a `DocumentCountResponse`</span></span>
* <span data-ttu-id="12f78-237">`IndexGetStatisticsResponse` è stata rinominata `IndexGetStatisticsResult`</span><span class="sxs-lookup"><span data-stu-id="12f78-237">`IndexGetStatisticsResponse` has been renamed to `IndexGetStatisticsResult`</span></span>
* <span data-ttu-id="12f78-238">`IndexListResponse` è stata rinominata `IndexListResult`</span><span class="sxs-lookup"><span data-stu-id="12f78-238">`IndexListResponse` has been renamed to `IndexListResult`</span></span>

<span data-ttu-id="12f78-239">Per riepilogare, le classi derivate da `OperationResponse`che servivano solo a eseguire il wrapping di un oggetto modello sono state rimosse.</span><span class="sxs-lookup"><span data-stu-id="12f78-239">To summarize, `OperationResponse`-derived classes that existed only to wrap a model object have been removed.</span></span> <span data-ttu-id="12f78-240">I suffissi delle altre classi sono passati da `Response` a `Result`.</span><span class="sxs-lookup"><span data-stu-id="12f78-240">The remaining classes have had their suffix changed from `Response` to `Result`.</span></span>

##### <a name="example"></a><span data-ttu-id="12f78-241">Esempio</span><span class="sxs-lookup"><span data-stu-id="12f78-241">Example</span></span>
<span data-ttu-id="12f78-242">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="12f78-242">If your code looks like this:</span></span>

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

<span data-ttu-id="12f78-243">È possibile sostituirlo con questo per correggere gli errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="12f78-243">You can change it to this to fix any build errors:</span></span>

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

##### <a name="response-classes-and-ienumerable"></a><span data-ttu-id="12f78-244">Classi di risposte e IEnumerable</span><span class="sxs-lookup"><span data-stu-id="12f78-244">Response classes and IEnumerable</span></span>
<span data-ttu-id="12f78-245">Un'altra modifica che può avere effetto sul codice è che le classi di risposte contenenti raccolte non implementano più `IEnumerable<T>`.</span><span class="sxs-lookup"><span data-stu-id="12f78-245">An additional change that may affect your code is that response classes that hold collections no longer implement `IEnumerable<T>`.</span></span> <span data-ttu-id="12f78-246">Invece è possibile accedere direttamente alla proprietà della raccolta.</span><span class="sxs-lookup"><span data-stu-id="12f78-246">Instead, you can access the collection property directly.</span></span> <span data-ttu-id="12f78-247">Ad esempio, se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="12f78-247">For example, if your code looks like this:</span></span>

    DocumentSearchResponse<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response)
    {
        Console.WriteLine(result.Document);
    }

<span data-ttu-id="12f78-248">È possibile sostituirlo con questo per correggere gli errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="12f78-248">You can change it to this to fix any build errors:</span></span>

    DocumentSearchResult<Hotel> response = indexClient.Documents.Search<Hotel>(searchText, sp);
    foreach (SearchResult<Hotel> result in response.Results)
    {
        Console.WriteLine(result.Document);
    }

##### <a name="special-case-for-web-applications"></a><span data-ttu-id="12f78-249">Caso speciale per le applicazioni Web</span><span class="sxs-lookup"><span data-stu-id="12f78-249">Special case for web applications</span></span>
<span data-ttu-id="12f78-250">Se è presente un'applicazione Web che serializza direttamente `DocumentSearchResponse` per inviare i risultati della ricerca al browser, sarà necessario modificare il codice o i risultati non verranno serializzati correttamente.</span><span class="sxs-lookup"><span data-stu-id="12f78-250">If you have a web application that serializes `DocumentSearchResponse` directly to send search results to the browser, you will need to change your code or the results will not serialize correctly.</span></span> <span data-ttu-id="12f78-251">Ad esempio, se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="12f78-251">For example, if your code looks like this:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q)
        };
    }

<span data-ttu-id="12f78-252">È possibile modificarla ottenendo la proprietà `.Results` della risposta della ricerca per correggere il rendering dei risultati della ricerca:</span><span class="sxs-lookup"><span data-stu-id="12f78-252">You can change it by getting the `.Results` property of the search response to fix search result rendering:</span></span>

    public ActionResult Search(string q = "")
    {
        // If blank search, assume they want to search everything
        if (string.IsNullOrWhiteSpace(q))
            q = "*";

        return new JsonResult
        {
            JsonRequestBehavior = JsonRequestBehavior.AllowGet,
            Data = _featuresSearch.Search(q).Results
        };
    }

<span data-ttu-id="12f78-253">Sarà necessario cercare manualmente tali casi nel codice. **Il compilatore non genererà avvisi** perché `JsonResult.Data` è di tipo `object`.</span><span class="sxs-lookup"><span data-stu-id="12f78-253">You will have to look for such cases in your code yourself; **The compiler will not warn you** because `JsonResult.Data` is of type `object`.</span></span>

#### <a name="cloudexception-changes"></a><span data-ttu-id="12f78-254">Modifiche a CloudException</span><span class="sxs-lookup"><span data-stu-id="12f78-254">CloudException changes</span></span>
<span data-ttu-id="12f78-255">La classe `CloudException` è stata spostata dallo spazio dei nomi `Hyak.Common` allo spazio dei nomi `Microsoft.Rest.Azure`.</span><span class="sxs-lookup"><span data-stu-id="12f78-255">The `CloudException` class has moved from the `Hyak.Common` namespace to the `Microsoft.Rest.Azure` namespace.</span></span> <span data-ttu-id="12f78-256">Inoltre la proprietà `Error` è stata rinominata `Body`.</span><span class="sxs-lookup"><span data-stu-id="12f78-256">Also, its `Error` property has been renamed to `Body`.</span></span>

#### <a name="searchserviceclient-and-searchindexclient-changes"></a><span data-ttu-id="12f78-257">Modifiche a SearchServiceClient e SearchIndexClient</span><span class="sxs-lookup"><span data-stu-id="12f78-257">SearchServiceClient and SearchIndexClient changes</span></span>
<span data-ttu-id="12f78-258">Il tipo della proprietà `Credentials` è passato da `SearchCredentials` alla relativa classe base, `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="12f78-258">The type of the `Credentials` property has changed from `SearchCredentials` to its base class, `ServiceClientCredentials`.</span></span> <span data-ttu-id="12f78-259">Se è necessario accedere a `SearchCredentials` di un oggetto `SearchIndexClient` o `SearchServiceClient`, usare la nuova proprietà `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="12f78-259">If you need to access the `SearchCredentials` of a `SearchIndexClient` or `SearchServiceClient`, please use the new `SearchCredentials` property.</span></span>

<span data-ttu-id="12f78-260">Nelle versioni precedenti dell'SDK `SearchServiceClient` e `SearchIndexClient` hanno costruttori che accettano un parametro `HttpClient`.</span><span class="sxs-lookup"><span data-stu-id="12f78-260">In older versions of the SDK, `SearchServiceClient` and `SearchIndexClient` had constructors that took an `HttpClient` parameter.</span></span> <span data-ttu-id="12f78-261">Questi sono stati sostituiti con costruttori che accettano `HttpClientHandler` e una matrice di oggetti `DelegatingHandler`.</span><span class="sxs-lookup"><span data-stu-id="12f78-261">These have been replaced with constructors that take an `HttpClientHandler` and an array of `DelegatingHandler` objects.</span></span> <span data-ttu-id="12f78-262">In questo modo è più semplice installare gestori personalizzati per pre-elaborare le richieste HTTP, se necessario.</span><span class="sxs-lookup"><span data-stu-id="12f78-262">This makes it easier to install custom handlers to pre-process HTTP requests if necessary.</span></span>

<span data-ttu-id="12f78-263">Infine sono stati modificati i costruttori che accettano `Uri` e `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="12f78-263">Finally, the constructors that took a `Uri` and `SearchCredentials` have changed.</span></span> <span data-ttu-id="12f78-264">Ad esempio, se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="12f78-264">For example, if you have code that looks like this:</span></span>

    var client =
        new SearchServiceClient(
            new SearchCredentials("abc123"),
            new Uri("http://myservice.search.windows.net"));

<span data-ttu-id="12f78-265">È possibile sostituirlo con questo per correggere gli errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="12f78-265">You can change it to this to fix any build errors:</span></span>

    var client =
        new SearchServiceClient(
            new Uri("http://myservice.search.windows.net"),
            new SearchCredentials("abc123"));

<span data-ttu-id="12f78-266">Si noti anche che il tipo del parametro delle credenziali è diventato `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="12f78-266">Also note that the type of the credentials parameter has changed to `ServiceClientCredentials`.</span></span> <span data-ttu-id="12f78-267">È improbabile che ciò abbia effetto sul codice perché `SearchCredentials` deriva da `ServiceClientCredentials`.</span><span class="sxs-lookup"><span data-stu-id="12f78-267">This is unlikely to affect your code since `SearchCredentials` is derived from `ServiceClientCredentials`.</span></span>

#### <a name="passing-a-request-id"></a><span data-ttu-id="12f78-268">Passaggio di un ID richiesta</span><span class="sxs-lookup"><span data-stu-id="12f78-268">Passing a request ID</span></span>
<span data-ttu-id="12f78-269">Nelle versioni precedenti dell'SDK è possibile impostare un ID richiesta su `SearchServiceClient` o su `SearchIndexClient` per includerlo in ogni richiesta per l'API REST.</span><span class="sxs-lookup"><span data-stu-id="12f78-269">In older versions of the SDK, you could set a request ID on the `SearchServiceClient` or `SearchIndexClient` and it would be included in every request to the REST API.</span></span> <span data-ttu-id="12f78-270">Ciò è utile per la risoluzione dei problemi relativi al servizio di ricerca se è necessario contattare il supporto.</span><span class="sxs-lookup"><span data-stu-id="12f78-270">This is useful for troubleshooting issues with your search service if you need to contact support.</span></span> <span data-ttu-id="12f78-271">È però più utile impostare un ID richiesta univoco per ogni operazione invece di usare lo stesso ID per tutte le operazioni.</span><span class="sxs-lookup"><span data-stu-id="12f78-271">However, it is more useful to set a unique request ID for every operation rather than to use the same ID for all operations.</span></span> <span data-ttu-id="12f78-272">Per questo motivo, i metodi `SetClientRequestId` di `SearchServiceClient` e `SearchIndexClient` sono stati rimossi.</span><span class="sxs-lookup"><span data-stu-id="12f78-272">For this reason, the `SetClientRequestId` methods of `SearchServiceClient` and `SearchIndexClient` have been removed.</span></span> <span data-ttu-id="12f78-273">È invece possibile passare un ID richiesta a ogni metodo di un'operazione tramite il parametro `SearchRequestOptions` facoltativo.</span><span class="sxs-lookup"><span data-stu-id="12f78-273">Instead, you can pass a request ID to each operation method via the optional `SearchRequestOptions` parameter.</span></span>

> [!NOTE]
> <span data-ttu-id="12f78-274">In una delle versioni future dell'SDK verrà aggiunto un nuovo meccanismo per impostare un ID richiesta a livello globale negli oggetti client, con un approccio coerente con quello usato da altri Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="12f78-274">In a future release of the SDK, we will add a new mechanism for setting a request ID globally on the client objects that is consistent with the approach used by other Azure SDKs.</span></span>
> 
> 

#### <a name="example"></a><span data-ttu-id="12f78-275">Esempio</span><span class="sxs-lookup"><span data-stu-id="12f78-275">Example</span></span>
<span data-ttu-id="12f78-276">Se il codice è simile a questo:</span><span class="sxs-lookup"><span data-stu-id="12f78-276">If you have code that looks like this:</span></span>

    client.SetClientRequestId(Guid.NewGuid());
    ...
    long count = client.Documents.Count();

<span data-ttu-id="12f78-277">È possibile sostituirlo con questo per correggere gli errori di compilazione:</span><span class="sxs-lookup"><span data-stu-id="12f78-277">You can change it to this to fix any build errors:</span></span>

    long count = client.Documents.Count(new SearchRequestOptions(requestId: Guid.NewGuid()));

#### <a name="interface-name-changes"></a><span data-ttu-id="12f78-278">Modifiche ai nomi delle interfacce</span><span class="sxs-lookup"><span data-stu-id="12f78-278">Interface name changes</span></span>
<span data-ttu-id="12f78-279">I nomi delle interfacce dei gruppi di operazioni sono stati tutti modificati in modo che fossero coerenti con i corrispondenti nomi di proprietà:</span><span class="sxs-lookup"><span data-stu-id="12f78-279">The operation group interface names have all changed to be consistent with their corresponding property names:</span></span>

* <span data-ttu-id="12f78-280">Il tipo di `ISearchServiceClient.Indexes` è stato rinominato da `IIndexOperations` a `IIndexesOperations`.</span><span class="sxs-lookup"><span data-stu-id="12f78-280">The type of `ISearchServiceClient.Indexes` has been renamed from `IIndexOperations` to `IIndexesOperations`.</span></span>
* <span data-ttu-id="12f78-281">Il tipo di `ISearchServiceClient.Indexers` è stato rinominato da `IIndexerOperations` a `IIndexersOperations`.</span><span class="sxs-lookup"><span data-stu-id="12f78-281">The type of `ISearchServiceClient.Indexers` has been renamed from `IIndexerOperations` to `IIndexersOperations`.</span></span>
* <span data-ttu-id="12f78-282">Il tipo di `ISearchServiceClient.DataSources` è stato rinominato da `IDataSourceOperations` a `IDataSourcesOperations`.</span><span class="sxs-lookup"><span data-stu-id="12f78-282">The type of `ISearchServiceClient.DataSources` has been renamed from `IDataSourceOperations` to `IDataSourcesOperations`.</span></span>
* <span data-ttu-id="12f78-283">Il tipo di `ISearchIndexClient.Documents` è stato rinominato da `IDocumentOperations` a `IDocumentsOperations`.</span><span class="sxs-lookup"><span data-stu-id="12f78-283">The type of `ISearchIndexClient.Documents` has been renamed from `IDocumentOperations` to `IDocumentsOperations`.</span></span>

<span data-ttu-id="12f78-284">Questa modifica potrebbe avere effetto sul codice solo se si creano interfacce fittizie a scopo di test.</span><span class="sxs-lookup"><span data-stu-id="12f78-284">This change is unlikely to affect your code unless you created mocks of these interfaces for test purposes.</span></span>

<a name="BugFixesV1"></a>

### <a name="bug-fixes-in-version-11"></a><span data-ttu-id="12f78-285">Correzioni di bug nella versione 1.1</span><span class="sxs-lookup"><span data-stu-id="12f78-285">Bug fixes in version 1.1</span></span>
<span data-ttu-id="12f78-286">Nelle versioni precedenti di Azure Search .NET SDK esiste un bug relativo alla serializzazione delle classi di modelli personalizzate.</span><span class="sxs-lookup"><span data-stu-id="12f78-286">There was a bug in older versions of the Azure Search .NET SDK relating to serialization of custom model classes.</span></span> <span data-ttu-id="12f78-287">Il bug può verificarsi se si crea una classe di modelli personalizzata con una proprietà di un tipo di valore non nullable.</span><span class="sxs-lookup"><span data-stu-id="12f78-287">The bug could occur if you created a custom model class with a property of a non-nullable value type.</span></span>

#### <a name="steps-to-reproduce"></a><span data-ttu-id="12f78-288">Passaggi per riprodurre il bug</span><span class="sxs-lookup"><span data-stu-id="12f78-288">Steps to reproduce</span></span>
<span data-ttu-id="12f78-289">Creare una classe di modelli personalizzata con una proprietà di tipo di valore non nullable.</span><span class="sxs-lookup"><span data-stu-id="12f78-289">Create a custom model class with a property of non-nullable value type.</span></span> <span data-ttu-id="12f78-290">Ad esempio, aggiungere una proprietà pubblica `UnitCount` di tipo `int` invece che `int?`.</span><span class="sxs-lookup"><span data-stu-id="12f78-290">For example, add a public `UnitCount` property of type `int` instead of `int?`.</span></span>

<span data-ttu-id="12f78-291">Se si indicizza un documento con il valore predefinito di tale tipo (ad esempio, 0 per `int`), il campo sarà null in Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="12f78-291">If you index a document with the default value of that type (for example, 0 for `int`), the field will be null in Azure Search.</span></span> <span data-ttu-id="12f78-292">Se in seguito si cerca tale documento, la chiamata a `Search` genererà `JsonSerializationException` perché non riesce a convertire `null` in `int`.</span><span class="sxs-lookup"><span data-stu-id="12f78-292">If you subsequently search for that document, the `Search` call will throw `JsonSerializationException` complaining that it can't convert `null` to `int`.</span></span>

<span data-ttu-id="12f78-293">Anche i filtri potrebbero non funzionare normalmente perché nell'indice è stato scritto null invece del valore previsto.</span><span class="sxs-lookup"><span data-stu-id="12f78-293">Also, filters may not work as expected since null was written to the index instead of the intended value.</span></span>

#### <a name="fix-details"></a><span data-ttu-id="12f78-294">Dettagli della correzione</span><span class="sxs-lookup"><span data-stu-id="12f78-294">Fix details</span></span>
<span data-ttu-id="12f78-295">Questo problema è stato risolto nella versione 1.1 dell'SDK.</span><span class="sxs-lookup"><span data-stu-id="12f78-295">We have fixed this issue in version 1.1 of the SDK.</span></span> <span data-ttu-id="12f78-296">Se è presente una classe di modelli come questa:</span><span class="sxs-lookup"><span data-stu-id="12f78-296">Now, if you have a model class like this:</span></span>

    public class Model
    {
        public string Key { get; set; }

        public int IntValue { get; set; }
    }

<span data-ttu-id="12f78-297">e si imposta `IntValue` su 0, tale valore ora viene serializzato correttamente come 0 durante il transito e archiviato come 0 nell'indice.</span><span class="sxs-lookup"><span data-stu-id="12f78-297">and you set `IntValue` to 0, that value is now correctly serialized as 0 on the wire and stored as 0 in the index.</span></span> <span data-ttu-id="12f78-298">Anche il round trip funziona come previsto.</span><span class="sxs-lookup"><span data-stu-id="12f78-298">Round tripping also works as expected.</span></span>

<span data-ttu-id="12f78-299">Questo approccio presenta un potenziale problema che è opportuno tenere presente: se si usa un tipo di modello con una proprietà che non ammette i valori null, è necessario **garantire** che nessun documento nell'indice contenga un valore null per il campo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="12f78-299">There is one potential issue to be aware of with this approach: If you use a model type with a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="12f78-300">Né l'SDK né l'API REST per Ricerca di Azure consentiranno di applicare questo valore.</span><span class="sxs-lookup"><span data-stu-id="12f78-300">Neither the SDK nor the Azure Search REST API will help you to enforce this.</span></span>

<span data-ttu-id="12f78-301">Non è solo un problema ipotetico: si pensi a uno scenario in cui si aggiunge un nuovo campo a un indice esistente di tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="12f78-301">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="12f78-302">Dopo l'aggiornamento della definizione dell'indice, tutti i documenti avranno un valore Null per il nuovo campo (perché tutti i tipi sono nullable in Ricerca di Azure).</span><span class="sxs-lookup"><span data-stu-id="12f78-302">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="12f78-303">Se quindi si usa una classe di modelli con una proprietà `int` che non ammette i valori Null per tale campo, verrà restituita un'eccezione `JsonSerializationException`, come questa, quando si cercherà di recuperare i documenti:</span><span class="sxs-lookup"><span data-stu-id="12f78-303">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="12f78-304">Per questo motivo, è ancora consigliabile usare tipi nullable nelle classi di modelli.</span><span class="sxs-lookup"><span data-stu-id="12f78-304">For this reason, we still recommend that you use nullable types in your model classes as a best practice.</span></span>

<span data-ttu-id="12f78-305">Per altri dettagli sul bug e sulla correzione, vedere [questo problema in GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span><span class="sxs-lookup"><span data-stu-id="12f78-305">For more details on this bug and the fix, please see [this issue on GitHub](https://github.com/Azure/azure-sdk-for-net/issues/1063).</span></span>

