---
title: aaaHow toouse ricerca di Azure da un'applicazione .NET | Documenti Microsoft
description: "La modalità di ricerca di Azure toouse da un'applicazione .NET"
services: search
documentationcenter: 
author: brjohnstmsft
manager: jlembicz
editor: 
ms.assetid: 93653341-c05f-4cfd-be45-bb877f964fcb
ms.service: search
ms.devlang: dotnet
ms.workload: search
ms.topic: article
ms.tgt_pltfrm: na
ms.date: 05/22/2017
ms.author: brjohnst
ms.openlocfilehash: 8e13fbe5549547d65941b856ce5a90611261388f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-search-from-a-net-application"></a><span data-ttu-id="746f0-103">La modalità di ricerca di Azure toouse da un'applicazione .NET</span><span class="sxs-lookup"><span data-stu-id="746f0-103">How toouse Azure Search from a .NET Application</span></span>
<span data-ttu-id="746f0-104">Questo articolo è tooget una procedura dettagliata è attivo e in esecuzione con hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="746f0-104">This article is a walkthrough tooget you up and running with hello [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="746f0-105">È possibile utilizzare hello .NET SDK tooimplement un'avanzata esperienza di ricerca in un'applicazione con ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="746f0-105">You can use hello .NET SDK tooimplement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-hello-azure-search-sdk"></a><span data-ttu-id="746f0-106">Che cos'è hello ricerca di Azure SDK</span><span class="sxs-lookup"><span data-stu-id="746f0-106">What's in hello Azure Search SDK</span></span>
<span data-ttu-id="746f0-107">Hello SDK è costituito da una libreria client, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="746f0-107">hello SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="746f0-108">Consente di toomanage gli indici e le origini dati, gli indicizzatori, nonché caricare e gestire documenti ed esecuzione di query, tutto senza dover toodeal con i dettagli di hello di HTTP e JSON.</span><span class="sxs-lookup"><span data-stu-id="746f0-108">It enables you toomanage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having toodeal with hello details of HTTP and JSON.</span></span>

<span data-ttu-id="746f0-109">libreria client Hello definisce classi come `Index`, `Field`, e `Document`, nonché operazioni quali `Indexes.Create` e `Documents.Search` su hello `SearchServiceClient` e `SearchIndexClient` classi.</span><span class="sxs-lookup"><span data-stu-id="746f0-109">hello client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on hello `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="746f0-110">Queste classi sono organizzate in hello spazi dei nomi seguenti:</span><span class="sxs-lookup"><span data-stu-id="746f0-110">These classes are organized into hello following namespaces:</span></span>

* [<span data-ttu-id="746f0-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="746f0-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="746f0-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="746f0-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="746f0-113">versione corrente di Hello di hello Azure Search .NET SDK è ora disponibile a livello generale.</span><span class="sxs-lookup"><span data-stu-id="746f0-113">hello current version of hello Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="746f0-114">Se si desidera tooprovide feedback per noi tooincorporate nella versione successiva di hello, visitare il nostro [pagina commenti e suggerimenti](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="746f0-114">If you would like tooprovide feedback for us tooincorporate in hello next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="746f0-115">Hello .NET SDK supporta la versione `2016-09-01` di hello [API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="746f0-115">hello .NET SDK supports version `2016-09-01` of hello [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="746f0-116">Questa versione include ora il supporto per gli analizzatori personalizzati, BLOB di Azure e l'Indicizzatore di tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="746f0-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="746f0-117">Le funzionalità di anteprima *non* parte di questa versione, quali il supporto per l'indicizzazione di file JSON e CSV, sono [anteprima](search-api-2015-02-28-preview.md) e disponibile tramite hello precedente [versione 2.0 per l'anteprima di hello .NET SDK ](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="746f0-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via hello older [2.0-preview version of hello .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="746f0-118">Questo SDK non supporta [operazioni di gestione](https://docs.microsoft.com/rest/api/searchmanagement/), come la creazione e la scalabilità di servizi di ricerca e la gestione delle chiavi API.</span><span class="sxs-lookup"><span data-stu-id="746f0-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="746f0-119">Se è necessario toomanage le risorse di ricerca da un'applicazione .NET, è possibile utilizzare hello [Azure Search .NET SDK di gestione](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="746f0-119">If you need toomanage your Search resources from a .NET application, you can use hello [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-toohello-latest-version-of-hello-sdk"></a><span data-ttu-id="746f0-120">L'aggiornamento più recente di hello SDK toohello</span><span class="sxs-lookup"><span data-stu-id="746f0-120">Upgrading toohello latest version of hello SDK</span></span>
<span data-ttu-id="746f0-121">Se già in uso una versione precedente di hello Azure Search .NET SDK e si desidera tooupgrade toohello nuovo generalmente disponibili versione, [questo articolo](search-dotnet-sdk-migration.md) spiega come.</span><span class="sxs-lookup"><span data-stu-id="746f0-121">If you're already using an older version of hello Azure Search .NET SDK and you'd like tooupgrade toohello new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-hello-sdk"></a><span data-ttu-id="746f0-122">Requisiti per hello SDK</span><span class="sxs-lookup"><span data-stu-id="746f0-122">Requirements for hello SDK</span></span>
1. <span data-ttu-id="746f0-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="746f0-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="746f0-124">Un servizio di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="746f0-124">Your own Azure Search service.</span></span> <span data-ttu-id="746f0-125">In hello toouse ordine SDK, sarà necessario nome hello del servizio e una o più chiavi API.</span><span class="sxs-lookup"><span data-stu-id="746f0-125">In order toouse hello SDK, you will need hello name of your service and one or more API keys.</span></span> <span data-ttu-id="746f0-126">[Creare un servizio nel portale di hello](search-create-service-portal.md) consentono di eseguire questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="746f0-126">[Create a service in hello portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="746f0-127">Scaricare hello Azure Search .NET SDK [pacchetto NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) utilizzando "Gestisci pacchetti NuGet" in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="746f0-127">Download hello Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="746f0-128">Solo la ricerca per nome del pacchetto hello `Microsoft.Azure.Search` in NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="746f0-128">Just search for hello package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="746f0-129">Hello Azure Search .NET SDK supporta le applicazioni destinate a .NET Framework 4.6 hello e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="746f0-129">hello Azure Search .NET SDK supports applications targeting hello .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="746f0-130">Scenari chiave</span><span class="sxs-lookup"><span data-stu-id="746f0-130">Core scenarios</span></span>
<span data-ttu-id="746f0-131">Ci sono vari aspetti, occorre toodo nell'applicazione di ricerca.</span><span class="sxs-lookup"><span data-stu-id="746f0-131">There are several things you'll need toodo in your search application.</span></span> <span data-ttu-id="746f0-132">In questa esercitazione saranno illustrati questi scenari chiave:</span><span class="sxs-lookup"><span data-stu-id="746f0-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="746f0-133">Creazione di un indice</span><span class="sxs-lookup"><span data-stu-id="746f0-133">Creating an index</span></span>
* <span data-ttu-id="746f0-134">La compilazione di indice hello con i documenti</span><span class="sxs-lookup"><span data-stu-id="746f0-134">Populating hello index with documents</span></span>
* <span data-ttu-id="746f0-135">Ricerca di documenti mediante filtri e ricerca con testo completo</span><span class="sxs-lookup"><span data-stu-id="746f0-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="746f0-136">codice di esempio Hello che segue illustra ognuno di questi.</span><span class="sxs-lookup"><span data-stu-id="746f0-136">hello sample code that follows illustrates each of these.</span></span> <span data-ttu-id="746f0-137">Se i frammenti di codice hello toouse disponibile nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="746f0-137">Feel free toouse hello code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="746f0-138">Panoramica</span><span class="sxs-lookup"><span data-stu-id="746f0-138">Overview</span></span>
<span data-ttu-id="746f0-139">Hello è sarà possibile esplorare l'applicazione di esempio crea un nuovo indice denominato "Hotel", viene popolato con alcuni documenti, quindi esegue alcune query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="746f0-139">hello sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="746f0-140">Ecco programma principale hello, che mostra hello flusso generale:</span><span class="sxs-lookup"><span data-stu-id="746f0-140">Here is hello main program, showing hello overall flow:</span></span>

```csharp
// This sample shows how toodelete, create, upload documents and query an index
static void Main(string[] args)
{
    IConfigurationBuilder builder = new ConfigurationBuilder().AddJsonFile("appsettings.json");
    IConfigurationRoot configuration = builder.Build();

    SearchServiceClient serviceClient = CreateSearchServiceClient(configuration);

    Console.WriteLine("{0}", "Deleting index...\n");
    DeleteHotelsIndexIfExists(serviceClient);

    Console.WriteLine("{0}", "Creating index...\n");
    CreateHotelsIndex(serviceClient);

    ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");

    Console.WriteLine("{0}", "Uploading documents...\n");
    UploadDocuments(indexClient);

    ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

    RunQueries(indexClientForQueries);

    Console.WriteLine("{0}", "Complete.  Press any key tooend application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="746f0-141">È possibile trovare il codice sorgente completo hello dell'applicazione di esempio hello utilizzato in questa procedura dettagliata su [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="746f0-141">You can find hello full source code of hello sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="746f0-142">La procedura verrà illustrata passo per passo.</span><span class="sxs-lookup"><span data-stu-id="746f0-142">We'll walk through this step by step.</span></span> <span data-ttu-id="746f0-143">È prima necessario toocreate un nuovo `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="746f0-143">First we need toocreate a new `SearchServiceClient`.</span></span> <span data-ttu-id="746f0-144">Questo oggetto consente toomanage indici.</span><span class="sxs-lookup"><span data-stu-id="746f0-144">This object allows you toomanage indexes.</span></span> <span data-ttu-id="746f0-145">In ordine tooconstruct uno, è necessario tooprovide il nome del servizio di ricerca di Azure, nonché una chiave API di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="746f0-145">In order tooconstruct one, you need tooprovide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="746f0-146">È possibile immettere queste informazioni in hello `appsettings.json` file hello [applicazione di esempio](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="746f0-146">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

```csharp
private static SearchServiceClient CreateSearchServiceClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string adminApiKey = configuration["SearchServiceAdminApiKey"];

    SearchServiceClient serviceClient = new SearchServiceClient(searchServiceName, new SearchCredentials(adminApiKey));
    return serviceClient;
}
```

> [!NOTE]
> <span data-ttu-id="746f0-147">Se si specifica una chiave non corretta (ad esempio, una chiave di query in cui una chiave amministratore è obbligatoria), hello `SearchServiceClient` genererà un `CloudException` con hello "Non consentito" messaggio di errore hello prima volta è chiamare un metodo dell'operazione, ad esempio `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="746f0-147">If you provide an incorrect key (for example, a query key where an admin key was required), hello `SearchServiceClient` will throw a `CloudException` with hello error message "Forbidden" hello first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="746f0-148">In questo caso tooyou, verificare la chiave API.</span><span class="sxs-lookup"><span data-stu-id="746f0-148">If this happens tooyou, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="746f0-149">Hello righe successive chiamare metodi toocreate un indice denominato "Hotel", l'eliminazione prima di tutto se esiste già.</span><span class="sxs-lookup"><span data-stu-id="746f0-149">hello next few lines call methods toocreate an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="746f0-150">Tali metodi saranno illustrati più avanti.</span><span class="sxs-lookup"><span data-stu-id="746f0-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="746f0-151">Successivamente, l'indice hello deve toobe popolato.</span><span class="sxs-lookup"><span data-stu-id="746f0-151">Next, hello index needs toobe populated.</span></span> <span data-ttu-id="746f0-152">toodo, è necessario un `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="746f0-152">toodo this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="746f0-153">Esistono due i modi tooobtain uno: costruendo, oppure chiamando `Indexes.GetClient` su hello `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="746f0-153">There are two ways tooobtain one: by constructing it, or by calling `Indexes.GetClient` on hello `SearchServiceClient`.</span></span> <span data-ttu-id="746f0-154">Utilizziamo hello quest'ultimo per praticità.</span><span class="sxs-lookup"><span data-stu-id="746f0-154">We use hello latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="746f0-155">In un'applicazione di ricerca tipica, il popolamento e la gestione degli indici viene gestita da un componente separato dalle query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="746f0-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="746f0-156">`Indexes.GetClient`è utile per la compilazione di un indice perché si salva hello problemi di fornire un altro `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="746f0-156">`Indexes.GetClient` is convenient for populating an index because it saves you hello trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="746f0-157">A tale scopo, passando la chiave di amministrazione hello hello toocreate utilizzati che si `SearchServiceClient` toohello nuova `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="746f0-157">It does this by passing hello admin key that you used toocreate hello `SearchServiceClient` toohello new `SearchIndexClient`.</span></span> <span data-ttu-id="746f0-158">Tuttavia, in parte dell'applicazione che esegue query hello è migliore hello toocreate `SearchIndexClient` direttamente in modo che è possibile passare una chiave di query anziché una chiave amministratore.</span><span class="sxs-lookup"><span data-stu-id="746f0-158">However, in hello part of your application that executes queries, it is better toocreate hello `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="746f0-159">Ciò è coerenza con il principio di hello dei privilegi minimi e aiutano toomake l'applicazione più sicura.</span><span class="sxs-lookup"><span data-stu-id="746f0-159">This is consistent with hello principle of least privilege and will help toomake your application more secure.</span></span> <span data-ttu-id="746f0-160">È possibile trovare ulteriori informazioni su chiavi di amministrazione e chiavi di query [qui](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="746f0-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="746f0-161">Ora che è disponibile un `SearchIndexClient`, è possibile popolare l'indice di hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-161">Now that we have a `SearchIndexClient`, we can populate hello index.</span></span> <span data-ttu-id="746f0-162">A tal fine verrà utilizzato un altro metodo che verrà descritto più avanti.</span><span class="sxs-lookup"><span data-stu-id="746f0-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="746f0-163">Infine, è eseguire alcune query di ricerca e visualizzare i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-163">Finally, we execute a few search queries and display hello results.</span></span> <span data-ttu-id="746f0-164">In questo caso viene utilizzato un `SearchIndexClient` diverso:</span><span class="sxs-lookup"><span data-stu-id="746f0-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="746f0-165">Verrà usato da vicino hello `RunQueries` metodo in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="746f0-165">We will take a closer look at hello `RunQueries` method later.</span></span> <span data-ttu-id="746f0-166">Ecco hello toocreate di codice hello nuovo `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="746f0-166">Here is hello code toocreate hello new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="746f0-167">In questo caso viene utilizzata una chiave di query perché non è necessario l'accesso in scrittura toohello indice.</span><span class="sxs-lookup"><span data-stu-id="746f0-167">This time we use a query key since we do not need write access toohello index.</span></span> <span data-ttu-id="746f0-168">È possibile immettere queste informazioni in hello `appsettings.json` file hello [applicazione di esempio](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="746f0-168">You can enter this information in hello `appsettings.json` file of hello [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="746f0-169">Se si esegue l'applicazione con un nome di servizio valido e le chiavi API, l'output di hello dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="746f0-169">If you run this application with a valid service name and API keys, hello output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents toobe indexed...
    
    Search hello entire index for hello term 'budget' and return only hello hotelName field:
    
    Name: Roach Motel
    
    Apply a filter toohello index toofind hotels cheaper than $150 per night, and return hello hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river
    
    Search hello entire index, order by a specific field (lastRenovationDate) in descending order, take hello top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search hello entire index for hello term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key tooend application...

<span data-ttu-id="746f0-170">il codice sorgente completo Hello di un'applicazione hello viene fornito alla fine di hello di questo articolo.</span><span class="sxs-lookup"><span data-stu-id="746f0-170">hello full source code of hello application is provided at hello end of this article.</span></span>

<span data-ttu-id="746f0-171">Successivamente, verrà usato informazioni dettagliate su ciascuno dei metodi di hello chiamati da `Main`.</span><span class="sxs-lookup"><span data-stu-id="746f0-171">Next, we will take a closer look at each of hello methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="746f0-172">Creazione di un indice</span><span class="sxs-lookup"><span data-stu-id="746f0-172">Creating an index</span></span>
<span data-ttu-id="746f0-173">Dopo aver creato un `SearchServiceClient`, cosa Avanti hello `Main` does è indice di hotel"delete hello", se esiste già.</span><span class="sxs-lookup"><span data-stu-id="746f0-173">After creating a `SearchServiceClient`, hello next thing `Main` does is delete hello "hotels" index if it already exists.</span></span> <span data-ttu-id="746f0-174">Che viene eseguita al metodo hello:</span><span class="sxs-lookup"><span data-stu-id="746f0-174">That is done by hello following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="746f0-175">Questo metodo utilizza hello dato `SearchServiceClient` toocheck se hello indice esistente e, in caso affermativo, eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="746f0-175">This method uses hello given `SearchServiceClient` toocheck if hello index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="746f0-176">codice di esempio Hello in questo articolo utilizza metodi sincroni di hello di hello Azure Search .NET SDK per motivi di semplicità.</span><span class="sxs-lookup"><span data-stu-id="746f0-176">hello example code in this article uses hello synchronous methods of hello Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="746f0-177">È consigliabile utilizzare i metodi asincroni hello nel proprio tookeep applicazioni scalabili e reattive.</span><span class="sxs-lookup"><span data-stu-id="746f0-177">We recommend that you use hello asynchronous methods in your own applications tookeep them scalable and responsive.</span></span> <span data-ttu-id="746f0-178">Ad esempio, in hello metodo sopra riportato è possibile utilizzare `ExistsAsync` e `DeleteAsync` anziché `Exists` e `Delete`.</span><span class="sxs-lookup"><span data-stu-id="746f0-178">For example, in hello method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="746f0-179">Successivamente, `Main` crea un nuovo indice "hotel" chiamando questo metodo:</span><span class="sxs-lookup"><span data-stu-id="746f0-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

```csharp
private static void CreateHotelsIndex(SearchServiceClient serviceClient)
{
    var definition = new Index()
    {
        Name = "hotels",
        Fields = FieldBuilder.BuildForType<Hotel>()
    };

    serviceClient.Indexes.Create(definition);
}
```

<span data-ttu-id="746f0-180">Questo metodo crea un nuovo `Index` oggetto con un elenco di `Field` gli oggetti che definisce schema hello del nuovo indice hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-180">This method creates a new `Index` object with a list of `Field` objects that defines hello schema of hello new index.</span></span> <span data-ttu-id="746f0-181">Ogni campo ha un nome, un tipo di dati e diversi attributi che definiscono il comportamento della ricerca.</span><span class="sxs-lookup"><span data-stu-id="746f0-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="746f0-182">Hello `FieldBuilder` classe utilizza la reflection toocreate un elenco di `Field` oggetti per l'indice di hello esaminando hello proprietà pubbliche e gli attributi di base hello `Hotel` classe del modello.</span><span class="sxs-lookup"><span data-stu-id="746f0-182">hello `FieldBuilder` class uses reflection toocreate a list of `Field` objects for hello index by examining hello public properties and attributes of hello given `Hotel` model class.</span></span> <span data-ttu-id="746f0-183">Ti guideremo vicino hello `Hotel` classe in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="746f0-183">We'll take a closer look at hello `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="746f0-184">È sempre possibile creare l'elenco di hello di `Field` oggetti direttamente anziché `FieldBuilder` se necessario.</span><span class="sxs-lookup"><span data-stu-id="746f0-184">You can always create hello list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="746f0-185">Ad esempio, non è una classe di modello toouse o potrebbe essere necessario toouse una classe di modello esistente che non si desidera toomodify aggiungendo attributi.</span><span class="sxs-lookup"><span data-stu-id="746f0-185">For example, you may not want toouse a model class or you may need toouse an existing model class that you don't want toomodify by adding attributes.</span></span>
>
> 

<span data-ttu-id="746f0-186">Inoltre toofields, è possibile anche aggiungere i profili di punteggio, suggerimento o toohello opzioni CORS indice (omesso dall'esempio hello per brevità).</span><span class="sxs-lookup"><span data-stu-id="746f0-186">In addition toofields, you can also add scoring profiles, suggesters, or CORS options toohello Index (these are omitted from hello sample for brevity).</span></span> <span data-ttu-id="746f0-187">È possibile trovare ulteriori informazioni sull'oggetto Index hello e le relative parti costituenti in hello [riferimento SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), nonché in hello [riferimento API REST di ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="746f0-187">You can find more information about hello Index object and its constituent parts in hello [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in hello [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-hello-index"></a><span data-ttu-id="746f0-188">La compilazione di indice hello</span><span class="sxs-lookup"><span data-stu-id="746f0-188">Populating hello index</span></span>
<span data-ttu-id="746f0-189">passaggio successivo di Hello in `Main` toopopulate hello nuovo indice.</span><span class="sxs-lookup"><span data-stu-id="746f0-189">hello next step in `Main` is toopopulate hello newly-created index.</span></span> <span data-ttu-id="746f0-190">Questa operazione viene eseguita in hello seguente metodo:</span><span class="sxs-lookup"><span data-stu-id="746f0-190">This is done in hello following method:</span></span>

```csharp
private static void UploadDocuments(ISearchIndexClient indexClient)
{
    var hotels = new Hotel[]
    {
        new Hotel()
        { 
            HotelId = "1", 
            BaseRate = 199.0, 
            Description = "Best hotel in town",
            DescriptionFr = "Meilleur hôtel en ville",
            HotelName = "Fancy Stay",
            Category = "Luxury", 
            Tags = new[] { "pool", "view", "wifi", "concierge" },
            ParkingIncluded = false, 
            SmokingAllowed = false,
            LastRenovationDate = new DateTimeOffset(2010, 6, 27, 0, 0, 0, TimeSpan.Zero), 
            Rating = 5, 
            Location = GeographyPoint.Create(47.678581, -122.131577)
        },
        new Hotel()
        { 
            HotelId = "2", 
            BaseRate = 79.99,
            Description = "Cheapest hotel in town",
            DescriptionFr = "Hôtel le moins cher en ville",
            HotelName = "Roach Motel",
            Category = "Budget",
            Tags = new[] { "motel", "budget" },
            ParkingIncluded = true,
            SmokingAllowed = true,
            LastRenovationDate = new DateTimeOffset(1982, 4, 28, 0, 0, 0, TimeSpan.Zero),
            Rating = 1,
            Location = GeographyPoint.Create(49.678581, -122.131577)
        },
        new Hotel() 
        { 
            HotelId = "3", 
            BaseRate = 129.99,
            Description = "Close tootown hall and hello river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of hello documents in
        // hello batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log hello failed document keys and continue.
        Console.WriteLine(
            "Failed tooindex some of hello documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents toobe indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="746f0-191">Questo metodo è costituito da quattro parti.</span><span class="sxs-lookup"><span data-stu-id="746f0-191">This method has four parts.</span></span> <span data-ttu-id="746f0-192">Hello crea innanzitutto una matrice di `Hotel` gli oggetti che verranno utilizzato come indice di toohello tooupload i dati di input.</span><span class="sxs-lookup"><span data-stu-id="746f0-192">hello first creates an array of `Hotel` objects that will serve as our input data tooupload toohello index.</span></span> <span data-ttu-id="746f0-193">Questi dati sono hardcoded per motivi di semplicità.</span><span class="sxs-lookup"><span data-stu-id="746f0-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="746f0-194">Nell'applicazione, i dati probabilmente proverranno da un'origine dati esterna, ad esempio un database SQL.</span><span class="sxs-lookup"><span data-stu-id="746f0-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="746f0-195">seconda parte Hello crea un `IndexBatch` che contengono i documenti hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-195">hello second part creates an `IndexBatch` containing hello documents.</span></span> <span data-ttu-id="746f0-196">Specificare hello operazione che si desidera tooapply toohello batch hello momento della creazione, in questo caso chiamando `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="746f0-196">You specify hello operation you want tooapply toohello batch at hello time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="746f0-197">Hello batch viene quindi caricato toohello ricerca di Azure di indice da hello `Documents.Index` metodo.</span><span class="sxs-lookup"><span data-stu-id="746f0-197">hello batch is then uploaded toohello Azure Search index by hello `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="746f0-198">In questo esempio, verranno semplicemente caricati i documenti.</span><span class="sxs-lookup"><span data-stu-id="746f0-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="746f0-199">Se si desidera toomerge assuma la forma documenti esistenti o eliminare i documenti, è possibile creare batch chiamando `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, o `IndexBatch.Delete` invece.</span><span class="sxs-lookup"><span data-stu-id="746f0-199">If you wanted toomerge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="746f0-200">È inoltre possibile combinare diverse operazioni in un singolo batch chiamando `IndexBatch.New`, che accetta una raccolta di `IndexAction` oggetti, ognuno dei quali indica un'operazione specifica in un documento a tooperform di ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="746f0-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search tooperform a particular operation on a document.</span></span> <span data-ttu-id="746f0-201">È possibile creare ogni `IndexAction` con il proprio operazione mediante la chiamata di metodo corrispondente hello, ad esempio `IndexAction.Merge`, `IndexAction.Upload`e così via.</span><span class="sxs-lookup"><span data-stu-id="746f0-201">You can create each `IndexAction` with its own operation by calling hello corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="746f0-202">Hello terza parte di questo metodo è un blocco catch che gestisce un caso di errore importanti per l'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="746f0-202">hello third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="746f0-203">Se il servizio di ricerca di Azure non riesce tooindex hello alcuni documenti nel batch di hello, un `IndexBatchException` viene generata da `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="746f0-203">If your Azure Search service fails tooindex some of hello documents in hello batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="746f0-204">Questa situazione può verificarsi se l'indicizzazione dei documenti avviene mentre il servizio è sovraccarico.</span><span class="sxs-lookup"><span data-stu-id="746f0-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="746f0-205">**Si consiglia di gestire in modo esplicito questo caso nel codice.**</span><span class="sxs-lookup"><span data-stu-id="746f0-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="746f0-206">È possibile ritardare e quindi ripetere l'indicizzazione documenti hello che non è riuscita oppure è possibile accedere e continuare come esempio hello non oppure è possibile eseguire qualcos'altro a seconda dei requisiti di coerenza dei dati dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="746f0-206">You can delay and then retry indexing hello documents that failed, or you can log and continue like hello sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="746f0-207">È possibile utilizzare hello `FindFailedActionsToRetry` tooconstruct metodo un nuovo batch contenente hello solo le azioni che non è riuscito a una precedente chiamata troppo`Index`.</span><span class="sxs-lookup"><span data-stu-id="746f0-207">You can use hello `FindFailedActionsToRetry` method tooconstruct a new batch containing only hello actions that failed in a previous call too`Index`.</span></span> <span data-ttu-id="746f0-208">metodo Hello è documentato [qui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) ed è presente una discussione sulle modalità d'uso da tooproperly [su StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="746f0-208">hello method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how tooproperly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="746f0-209">Infine, hello `UploadDocuments` ritardi di metodo di due secondi.</span><span class="sxs-lookup"><span data-stu-id="746f0-209">Finally, hello `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="746f0-210">L'indicizzazione avviene in modo asincrono nel servizio di ricerca di Azure, quindi l'applicazione di esempio hello deve toowait tooensure un breve periodo di tempo che sono disponibili per la ricerca di documenti di hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-210">Indexing happens asynchronously in your Azure Search service, so hello sample application needs toowait a short time tooensure that hello documents are available for searching.</span></span> <span data-ttu-id="746f0-211">Ritardi come questi in genere sono necessari solo in applicazioni di esempio, test e demo.</span><span class="sxs-lookup"><span data-stu-id="746f0-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-hello-net-sdk-handles-documents"></a><span data-ttu-id="746f0-212">La modalità di gestione di documenti hello .NET SDK</span><span class="sxs-lookup"><span data-stu-id="746f0-212">How hello .NET SDK handles documents</span></span>
<span data-ttu-id="746f0-213">Per comprendere come hello Azure Search .NET SDK è istanze tooupload in grado di una classe definita dall'utente come `Hotel` toohello indice.</span><span class="sxs-lookup"><span data-stu-id="746f0-213">You may be wondering how hello Azure Search .NET SDK is able tooupload instances of a user-defined class like `Hotel` toohello index.</span></span> <span data-ttu-id="746f0-214">toohelp rispondere alla domanda, si esaminerà hello `Hotel` classe:</span><span class="sxs-lookup"><span data-stu-id="746f0-214">toohelp answer that question, let's look at hello `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// hello SerializePropertyNamesAsCamelCase attribute is defined in hello Azure Search .NET SDK.
// It ensures that Pascal-case property names in hello model class are mapped toocamel-case
// field names in hello index.
[SerializePropertyNamesAsCamelCase]
public partial class Hotel
{
    [System.ComponentModel.DataAnnotations.Key]
    [IsFilterable]
    public string HotelId { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public double? BaseRate { get; set; }

    [IsSearchable]
    public string Description { get; set; }

    [IsSearchable]
    [Analyzer(AnalyzerName.AsString.FrLucene)]
    [JsonProperty("description_fr")]
    public string DescriptionFr { get; set; }

    [IsSearchable, IsFilterable, IsSortable]
    public string HotelName { get; set; }

    [IsSearchable, IsFilterable, IsSortable, IsFacetable]
    public string Category { get; set; }

    [IsSearchable, IsFilterable, IsFacetable]
    public string[] Tags { get; set; }

    [IsFilterable, IsFacetable]
    public bool? ParkingIncluded { get; set; }

    [IsFilterable, IsFacetable]
    public bool? SmokingAllowed { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public DateTimeOffset? LastRenovationDate { get; set; }

    [IsFilterable, IsSortable, IsFacetable]
    public int? Rating { get; set; }

    [IsFilterable, IsSortable]
    public GeographyPoint Location { get; set; }
}
```

<span data-ttu-id="746f0-215">Hello in primo luogo toonotice è che ogni proprietà pubblica di `Hotel` corrisponde tooa campo nella definizione dell'indice hello, ma con una differenza fondamentale: nome hello di ogni campo inizia con una lettera minuscola ("caso camel"), mentre il nome di hello ogni pubblico proprietà di `Hotel` inizia con una lettera maiuscola ("convenzione Pascal").</span><span class="sxs-lookup"><span data-stu-id="746f0-215">hello first thing toonotice is that each public property of `Hotel` corresponds tooa field in hello index definition, but with one crucial difference: hello name of each field starts with a lower-case letter ("camel case"), while hello name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="746f0-216">Si tratta di uno scenario comune in applicazioni .NET che eseguire il binding di dati in cui lo schema di destinazione hello è controllo hello di fuori di sviluppatore dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-216">This is a common scenario in .NET applications that perform data-binding where hello target schema is outside hello control of hello application developer.</span></span> <span data-ttu-id="746f0-217">Invece di tooviolate hello .NET convenzioni di denominazione rendendo proprietà nomi maiuscole-minuscole camel, è possibile indicare hello SDK toomap hello proprietà nomi toocamel caso automaticamente con hello `[SerializePropertyNamesAsCamelCase]` attributo.</span><span class="sxs-lookup"><span data-stu-id="746f0-217">Rather than having tooviolate hello .NET naming guidelines by making property names camel-case, you can tell hello SDK toomap hello property names toocamel-case automatically with hello `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="746f0-218">Hello Azure Search .NET SDK Usa hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) tooserialize libreria e deserializzare tooand di oggetti del modello personalizzato da JSON.</span><span class="sxs-lookup"><span data-stu-id="746f0-218">hello Azure Search .NET SDK uses hello [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library tooserialize and deserialize your custom model objects tooand from JSON.</span></span> <span data-ttu-id="746f0-219">Se necessario, è possibile personalizzare questa serializzazione.</span><span class="sxs-lookup"><span data-stu-id="746f0-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="746f0-220">Per altre informazioni, vedere [Serializzazione personalizzata con JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="746f0-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="746f0-221">Hello secondo toonotice cosa sono gli attributi di hello come `IsFilterable`, `IsSearchable`, `Key`, e `Analyzer` che decorano ogni proprietà pubblica.</span><span class="sxs-lookup"><span data-stu-id="746f0-221">hello second thing toonotice are hello attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="746f0-222">Questi attributi eseguono il mapping direttamente toohello [attributi corrispondenti dell'indice di ricerca di Azure hello](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="746f0-222">These attributes map directly toohello [corresponding attributes of hello Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="746f0-223">Hello `FieldBuilder` classe utilizza le definizioni di campo tooconstruct per indice hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-223">hello `FieldBuilder` class uses these tooconstruct field definitions for hello index.</span></span>

<span data-ttu-id="746f0-224">Hello terzo importante su hello `Hotel` classe sono tipi di dati hello delle proprietà pubbliche di hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-224">hello third important thing about hello `Hotel` class are hello data types of hello public properties.</span></span> <span data-ttu-id="746f0-225">tipi di queste proprietà .NET Hello mappare i tipi di campo equivalente tootheir nella definizione dell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-225">hello .NET types of  these properties map tootheir equivalent field types in hello index definition.</span></span> <span data-ttu-id="746f0-226">Ad esempio, hello `Category` toohello esegue il mapping di proprietà stringa `category` campo, è di tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="746f0-226">For example, hello `Category` string property maps toohello `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="746f0-227">Mapping di tipo simile tra `bool?` e `Edm.Boolean`, `DateTimeOffset?` e `Edm.DateTimeOffset`, regole specifiche di hello e così via per il mapping di tipo hello sono documentate con hello `Documents.Get` metodo hello [Azure Search .NET SDK riferimento](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="746f0-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. hello specific rules for hello type mapping are documented with hello `Documents.Get` method in hello [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="746f0-228">Hello `FieldBuilder` classe si occupa di questo mapping per l'utente, ma può comunque essere toounderstand utile nel caso in cui è necessario tootroubleshoot eventuali problemi di serializzazione.</span><span class="sxs-lookup"><span data-stu-id="746f0-228">hello `FieldBuilder` class takes care of this mapping for you, but it can still be helpful toounderstand in case you need tootroubleshoot any serialization issues.</span></span>

<span data-ttu-id="746f0-229">Questa possibilità toouse le proprie classi come documenti funziona in entrambe le direzioni; È anche possibile recuperare i risultati della ricerca e avere hello SDK automaticamente deserializzare li tooa tipo di propria scelta, come verrà illustrato nella sezione successiva hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-229">This ability toouse your own classes as documents works in both directions; You can also retrieve search results and have hello SDK automatically deserialize them tooa type of your choice, as we will see in hello next section.</span></span>

> [!NOTE]
> <span data-ttu-id="746f0-230">Hello Azure Search .NET SDK supporta anche i documenti tipizzata in modo dinamico utilizzando hello `Document` (classe), ovvero un mapping di chiave/valore nomi toofield dei valori dei campi.</span><span class="sxs-lookup"><span data-stu-id="746f0-230">hello Azure Search .NET SDK also supports dynamically-typed documents using hello `Document` class, which is a key/value mapping of field names toofield values.</span></span> <span data-ttu-id="746f0-231">Ciò è utile negli scenari in cui non si conosce dello schema di indice hello in fase di progettazione o in cui sarebbe scomodo toobind toospecific classi del modello.</span><span class="sxs-lookup"><span data-stu-id="746f0-231">This is useful in scenarios where you don't know hello index schema at design-time, or where it would be inconvenient toobind toospecific model classes.</span></span> <span data-ttu-id="746f0-232">Tutti i metodi di hello hello SDK che gestiscono documenti presentano overload che funzionano con hello `Document` classe, come gli overload fortemente tipizzato che accettano un parametro di tipo generico.</span><span class="sxs-lookup"><span data-stu-id="746f0-232">All hello methods in hello SDK that deal with documents have overloads that work with hello `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="746f0-233">Hello solo quest'ultimo vengono utilizzati nel codice di esempio hello in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="746f0-233">Only hello latter are used in hello sample code in this tutorial.</span></span> <span data-ttu-id="746f0-234">Hello `Document` classe eredita da `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="746f0-234">hello `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="746f0-235">Per informazioni più dettagliate, vedere [qui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="746f0-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="746f0-236">**Perché usare tipi di dati nullable**</span><span class="sxs-lookup"><span data-stu-id="746f0-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="746f0-237">Quando si progetta la propria indice di ricerca di Azure tooan toomap classi di modello, si consiglia di dichiarazione delle proprietà dei tipi di valore, ad esempio `bool` e `int` toobe ammette valori null (ad esempio, `bool?` anziché `bool`).</span><span class="sxs-lookup"><span data-stu-id="746f0-237">When designing your own model classes toomap tooan Azure Search index, we recommend declaring properties of value types such as `bool` and `int` toobe nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="746f0-238">Se si utilizza una proprietà che non ammette valori null, è necessario troppo**garantire** che nessun documenti nell'indice contengono un valore null per il campo corrispondente hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-238">If you use a non-nullable property, you have too**guarantee** that no documents in your index contain a null value for hello corresponding field.</span></span> <span data-ttu-id="746f0-239">Hello SDK né hello del servizio di ricerca di Azure consentirà si tooenforce questo.</span><span class="sxs-lookup"><span data-stu-id="746f0-239">Neither hello SDK nor hello Azure Search service will help you tooenforce this.</span></span>

<span data-ttu-id="746f0-240">Non è un problema di ipotetica: si consideri uno scenario in cui aggiungere un nuovo campo tooan esistente indice di tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="746f0-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field tooan existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="746f0-241">Dopo aver aggiornato la definizione dell'indice hello, tutti i documenti avrà un valore null per il nuovo campo (poiché tutti i tipi nullable in ricerca di Azure).</span><span class="sxs-lookup"><span data-stu-id="746f0-241">After updating hello index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="746f0-242">Se si utilizza una classe di modello con un non-nullable `int` proprietà per il campo, si otterrà un `JsonSerializationException` simile durante il tentativo di tooretrieve documenti:</span><span class="sxs-lookup"><span data-stu-id="746f0-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying tooretrieve documents:</span></span>

    Error converting value {null} tootype 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="746f0-243">Per questo motivo, è consigliabile usare tipi nullable nelle classi di modelli.</span><span class="sxs-lookup"><span data-stu-id="746f0-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="746f0-244">Serializzazione personalizzata con JSON.NET</span><span class="sxs-lookup"><span data-stu-id="746f0-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="746f0-245">Hello SDK utilizza JSON.NET per la serializzazione e la deserializzazione di documenti.</span><span class="sxs-lookup"><span data-stu-id="746f0-245">hello SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="746f0-246">È possibile personalizzare la serializzazione e la deserializzazione se necessario definendo la propria `JsonConverter` o `IContractResolver` (vedere hello [JSON.NET documentazione](http://www.newtonsoft.com/json/help/html/Introduction.htm) per altri dettagli).</span><span class="sxs-lookup"><span data-stu-id="746f0-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see hello [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="746f0-247">Può essere utile quando si desidera che una classe di modello esistente tooadapt dall'applicazione per l'utilizzo con ricerca di Azure e altri scenari più avanzati.</span><span class="sxs-lookup"><span data-stu-id="746f0-247">This can be useful when you want tooadapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="746f0-248">Con la serializzazione personalizzata, ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="746f0-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="746f0-249">Includere o escludere determinate proprietà della classe modello da archiviare come campi di un documento.</span><span class="sxs-lookup"><span data-stu-id="746f0-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="746f0-250">Eseguire il mapping tra i nomi di proprietà nel codice e i nomi di campo nell'indice.</span><span class="sxs-lookup"><span data-stu-id="746f0-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="746f0-251">Creare attributi personalizzati che possono essere utilizzati per il mapping dei campi di proprietà toodocument.</span><span class="sxs-lookup"><span data-stu-id="746f0-251">Create custom attributes that can be used for mapping properties toodocument fields.</span></span>

<span data-ttu-id="746f0-252">È possibile trovare esempi di implementazione di serializzazione personalizzata in hello unit test per hello Azure Search .NET SDK in GitHub.</span><span class="sxs-lookup"><span data-stu-id="746f0-252">You can find examples of implementing custom serialization in hello unit tests for hello Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="746f0-253">È consigliabile iniziare da [questa cartella](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models),</span><span class="sxs-lookup"><span data-stu-id="746f0-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="746f0-254">Contiene classi che vengono utilizzate dai test di serializzazione personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-254">It contains classes that are used by hello custom serialization tests.</span></span>

### <a name="searching-for-documents-in-hello-index"></a><span data-ttu-id="746f0-255">Ricerca di documenti nell'indice hello</span><span class="sxs-lookup"><span data-stu-id="746f0-255">Searching for documents in hello index</span></span>
<span data-ttu-id="746f0-256">ultimo passaggio di Hello nell'applicazione di esempio hello è toosearch per alcuni documenti nell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-256">hello last step in hello sample application is toosearch for some documents in hello index.</span></span> <span data-ttu-id="746f0-257">metodo Hello esegue questa operazione:</span><span class="sxs-lookup"><span data-stu-id="746f0-257">hello following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search hello entire index for hello term 'budget' and return only hello hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter toohello index toofind hotels cheaper than $150 per night, ");
    Console.WriteLine("and return hello hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search hello entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take hello top two results, and show only hotelName and ");
    Console.WriteLine("lastRenovationDate:\n");

    parameters =
        new SearchParameters()
        {
            OrderBy = new[] { "lastRenovationDate desc" },
            Select = new[] { "hotelName", "lastRenovationDate" },
            Top = 2
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.WriteLine("Search hello entire index for hello term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="746f0-258">Ogni volta che viene eseguita una query, questo metodo crea prima un nuovo oggetto `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="746f0-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="746f0-259">Si tratta di toospecify utilizzate opzioni aggiuntive per query hello, ad esempio l'ordinamento, filtro, paging e facet.</span><span class="sxs-lookup"><span data-stu-id="746f0-259">This is used toospecify additional options for hello query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="746f0-260">In questo metodo, è in corso configurazione hello `Filter`, `Select`, `OrderBy`, e `Top` proprietà per query diverse.</span><span class="sxs-lookup"><span data-stu-id="746f0-260">In this method, we're setting hello `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="746f0-261">Hello tutti `SearchParameters` le proprietà vengono documentate [qui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="746f0-261">All hello `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="746f0-262">passaggio successivo Hello è tooactually eseguire query di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-262">hello next step is tooactually execute hello search query.</span></span> <span data-ttu-id="746f0-263">Questa operazione viene eseguita utilizzando hello `Documents.Search` metodo.</span><span class="sxs-lookup"><span data-stu-id="746f0-263">This is done using hello `Documents.Search` method.</span></span> <span data-ttu-id="746f0-264">Per ogni query, hello ricerca testo toouse viene passato come stringa (o `"*"` se non è presente testo di ricerca), nonché hello creati in precedenza di parametri di ricerca.</span><span class="sxs-lookup"><span data-stu-id="746f0-264">For each query, we pass hello search text toouse as a string (or `"*"` if there is no search text), plus hello search parameters created earlier.</span></span> <span data-ttu-id="746f0-265">È inoltre possibile specificare `Hotel` come parametro di tipo hello `Documents.Search`, che indica i documenti toodeserialize SDK hello nei risultati della ricerca hello in oggetti di tipo `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="746f0-265">We also specify `Hotel` as hello type parameter for `Documents.Search`, which tells hello SDK toodeserialize documents in hello search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="746f0-266">È possibile trovare ulteriori informazioni sulla sintassi delle espressioni di query ricerca hello [qui](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="746f0-266">You can find more information about hello search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="746f0-267">Infine, dopo ogni query questo metodo scorre tutte le corrispondenze di hello nei risultati della ricerca hello, stampa di ogni console toohello documento:</span><span class="sxs-lookup"><span data-stu-id="746f0-267">Finally, after each query this method iterates through all hello matches in hello search results, printing each document toohello console:</span></span>

```csharp
private static void WriteDocuments(DocumentSearchResult<Hotel> searchResults)
{
    foreach (SearchResult<Hotel> result in searchResults.Results)
    {
        Console.WriteLine(result.Document);
    }

    Console.WriteLine();
}
```

<span data-ttu-id="746f0-268">Prendiamo a sua volta informazioni dettagliate su ognuna delle query hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-268">Let's take a closer look at each of hello queries in turn.</span></span> <span data-ttu-id="746f0-269">Ecco hello codice tooexecute hello prima query:</span><span class="sxs-lookup"><span data-stu-id="746f0-269">Here is hello code tooexecute hello first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="746f0-270">In questo caso, viene eseguita la ricerca per gli alberghi parola hello "budget" e si desidera tooget nuovamente solo hello hotel i nomi, come specificato da hello `Select` parametro.</span><span class="sxs-lookup"><span data-stu-id="746f0-270">In this case, we're searching for hotels that match hello word "budget", and we want tooget back only hello hotel names, as specified by hello `Select` parameter.</span></span> <span data-ttu-id="746f0-271">Di seguito sono risultati hello:</span><span class="sxs-lookup"><span data-stu-id="746f0-271">Here are hello results:</span></span>

    Name: Roach Motel

<span data-ttu-id="746f0-272">Successivamente, si desidera che gli hotel hello toofind con una frequenza minore di $ 150 notturna e restituire solo hello hotel ID e la descrizione:</span><span class="sxs-lookup"><span data-stu-id="746f0-272">Next, we want toofind hello hotels with a nightly rate of less than $150, and return only hello hotel ID and description:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Filter = "baseRate lt 150",
        Select = new[] { "hotelId", "description" }
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="746f0-273">Questa query utilizza OData `$filter` espressione, `baseRate lt 150`, documenti hello toofilter nell'indice hello.</span><span class="sxs-lookup"><span data-stu-id="746f0-273">This query uses an OData `$filter` expression, `baseRate lt 150`, toofilter hello documents in hello index.</span></span> <span data-ttu-id="746f0-274">È possibile trovare ulteriori informazioni su sintassi OData che supporta la ricerca di Azure hello [qui](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="746f0-274">You can find out more about hello OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="746f0-275">Di seguito sono risultati hello di query di hello:</span><span class="sxs-lookup"><span data-stu-id="746f0-275">Here are hello results of hello query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close tootown hall and hello river

<span data-ttu-id="746f0-276">A questo punto, è opportuno toofind hello superiore due gli hotel sono stati rimodernati più di recente, che mostrano il nome di hotel hello e data di rinnovo.</span><span class="sxs-lookup"><span data-stu-id="746f0-276">Next, we want toofind hello top two hotels that have been most recently renovated, and show hello hotel name and last renovation date.</span></span> <span data-ttu-id="746f0-277">Ecco il codice hello:</span><span class="sxs-lookup"><span data-stu-id="746f0-277">Here is hello code:</span></span> 

```csharp
parameters =
    new SearchParameters()
    {
        OrderBy = new[] { "lastRenovationDate desc" },
        Select = new[] { "hotelName", "lastRenovationDate" },
        Top = 2
    };

results = indexClient.Documents.Search<Hotel>("*", parameters);

WriteDocuments(results);
```

<span data-ttu-id="746f0-278">In questo caso, utilizziamo nuovamente hello toospecify sintassi di OData `OrderBy` parametro come `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="746f0-278">In this case, we again use OData syntax toospecify hello `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="746f0-279">È inoltre possibile impostare `Top` too2 tooensure è solo ottenere hello primi due documenti.</span><span class="sxs-lookup"><span data-stu-id="746f0-279">We also set `Top` too2 tooensure we only get hello top two documents.</span></span> <span data-ttu-id="746f0-280">Come prima, impostiamo `Select` toospecify i campi devono essere restituiti.</span><span class="sxs-lookup"><span data-stu-id="746f0-280">As before, we set `Select` toospecify which fields should be returned.</span></span>

<span data-ttu-id="746f0-281">Di seguito sono risultati hello:</span><span class="sxs-lookup"><span data-stu-id="746f0-281">Here are hello results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="746f0-282">Infine, è necessario toofind tutti gli alberghi parola hello "motel":</span><span class="sxs-lookup"><span data-stu-id="746f0-282">Finally, we want toofind all hotels that match hello word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="746f0-283">Ecco i risultati di hello, che includono tutti i campi, poiché non è stato specificato hello `Select` proprietà:</span><span class="sxs-lookup"><span data-stu-id="746f0-283">And here are hello results, which include all fields since we did not specify hello `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="746f0-284">Questo passaggio di completamento dell'esercitazione hello, ma non interrompere qui.</span><span class="sxs-lookup"><span data-stu-id="746f0-284">This step completes hello tutorial, but don't stop here.</span></span> <span data-ttu-id="746f0-285">**Passaggi successivi** vengono fornite risorse aggiuntive per ottenere ulteriori informazioni su Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="746f0-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="746f0-286">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="746f0-286">Next steps</span></span>
* <span data-ttu-id="746f0-287">Individuare i riferimenti di hello per hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) e [API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="746f0-287">Browse hello references for hello [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="746f0-288">Approfondire l'argomento tramite [video e altri esempi ed esercitazioni](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="746f0-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="746f0-289">Revisione [convenzioni di denominazione](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) regole hello toolearn per la denominazione dei vari oggetti.</span><span class="sxs-lookup"><span data-stu-id="746f0-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) toolearn hello rules for naming various objects.</span></span>
* <span data-ttu-id="746f0-290">Rivedere i [tipi di dati supportati](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="746f0-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
