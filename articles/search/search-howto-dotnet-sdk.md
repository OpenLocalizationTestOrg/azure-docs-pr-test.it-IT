---
title: Come usare Ricerca di Azure da un'applicazione .NET | Documentazione Microsoft
description: Come utilizzare Ricerca di Azure da un'applicazione .NET
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
ms.openlocfilehash: 552a7ab193e12d2e72da494166d774e974c85d47
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-search-from-a-net-application"></a><span data-ttu-id="2bf77-103">Come utilizzare Ricerca di Azure da un'applicazione .NET</span><span class="sxs-lookup"><span data-stu-id="2bf77-103">How to use Azure Search from a .NET Application</span></span>
<span data-ttu-id="2bf77-104">In questo articolo è descritta una procedura dettagliata per eseguire [.NET SDK di Ricerca di Azure](https://aka.ms/search-sdk).</span><span class="sxs-lookup"><span data-stu-id="2bf77-104">This article is a walkthrough to get you up and running with the [Azure Search .NET SDK](https://aka.ms/search-sdk).</span></span> <span data-ttu-id="2bf77-105">È possibile utilizzare .NET SDK per implementare un'esperienza di ricerca completa nell'applicazione tramite Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="2bf77-105">You can use the .NET SDK to implement a rich search experience in your application using Azure Search.</span></span>

## <a name="whats-in-the-azure-search-sdk"></a><span data-ttu-id="2bf77-106">Novità dell'SDK di Ricerca di Azure</span><span class="sxs-lookup"><span data-stu-id="2bf77-106">What's in the Azure Search SDK</span></span>
<span data-ttu-id="2bf77-107">Questo SDK è costituito da una libreria client, `Microsoft.Azure.Search`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-107">The SDK consists of a client library, `Microsoft.Azure.Search`.</span></span> <span data-ttu-id="2bf77-108">Consente di gestire indici, origini dati e indicizzatori, nonché di caricare e gestire documenti ed eseguire query, senza la necessità di affrontare i dettagli di HTTP e JSON.</span><span class="sxs-lookup"><span data-stu-id="2bf77-108">It enables you to manage your indexes, data sources, and indexers, as well as upload and manage documents, and execute queries, all without having to deal with the details of HTTP and JSON.</span></span>

<span data-ttu-id="2bf77-109">La libreria client definisce classi come `Index`, `Field`, e `Document`, nonché operazioni quali `Indexes.Create` e `Documents.Search` sulle classi `SearchServiceClient` e `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-109">The client library defines classes like `Index`, `Field`, and `Document`, as well as operations like `Indexes.Create` and `Documents.Search` on the `SearchServiceClient` and `SearchIndexClient` classes.</span></span> <span data-ttu-id="2bf77-110">Le classi sono organizzate negli spazi dei nomi seguenti:</span><span class="sxs-lookup"><span data-stu-id="2bf77-110">These classes are organized into the following namespaces:</span></span>

* [<span data-ttu-id="2bf77-111">Microsoft.Azure.Search</span><span class="sxs-lookup"><span data-stu-id="2bf77-111">Microsoft.Azure.Search</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search)
* [<span data-ttu-id="2bf77-112">Microsoft.Azure.Search.Models</span><span class="sxs-lookup"><span data-stu-id="2bf77-112">Microsoft.Azure.Search.Models</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models)

<span data-ttu-id="2bf77-113">La versione corrente di Azure Search .NET SDK è ora in disponibilità generale.</span><span class="sxs-lookup"><span data-stu-id="2bf77-113">The current version of the Azure Search .NET SDK is now generally available.</span></span> <span data-ttu-id="2bf77-114">Per fornire a Microsoft commenti e suggerimenti da incorporare nella prima versione successiva, visitare la [pagina dei commenti](https://feedback.azure.com/forums/263029-azure-search/).</span><span class="sxs-lookup"><span data-stu-id="2bf77-114">If you would like to provide feedback for us to incorporate in the next version, please visit our [feedback page](https://feedback.azure.com/forums/263029-azure-search/).</span></span>

<span data-ttu-id="2bf77-115">.NET SDK supporta la versione `2016-09-01` dell'[API REST di Ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="2bf77-115">The .NET SDK supports version `2016-09-01` of the [Azure Search REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span> <span data-ttu-id="2bf77-116">Questa versione include ora il supporto per gli analizzatori personalizzati, BLOB di Azure e l'Indicizzatore di tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="2bf77-116">This version now includes support for custom analyzers and Azure Blob and Azure Table indexer support.</span></span> <span data-ttu-id="2bf77-117">Le funzionalità di anteprima che *non* sono incluse in questa versione, ad esempio il supporto per l'indicizzazione di file JSON e CSV, sono disponibili in [anteprima](search-api-2015-02-28-preview.md) e tramite la precedente [versione 2.0-preview di .NET SDK](https://aka.ms/search-sdk-preview).</span><span class="sxs-lookup"><span data-stu-id="2bf77-117">Preview features that are *not* part of this version, such as support for indexing JSON and CSV files, are in [preview](search-api-2015-02-28-preview.md) and available via the older [2.0-preview version of the .NET SDK](https://aka.ms/search-sdk-preview).</span></span>

<span data-ttu-id="2bf77-118">Questo SDK non supporta [operazioni di gestione](https://docs.microsoft.com/rest/api/searchmanagement/), come la creazione e la scalabilità di servizi di ricerca e la gestione delle chiavi API.</span><span class="sxs-lookup"><span data-stu-id="2bf77-118">This SDK does not support [Management Operations](https://docs.microsoft.com/rest/api/searchmanagement/) such as creating and scaling Search services and managing API keys.</span></span> <span data-ttu-id="2bf77-119">Se è necessario gestire le risorse di ricerca da un'applicazione .NET, è possibile utilizzare l'[SDK di gestione .NET di Ricerca di Azure](https://aka.ms/search-mgmt-sdk).</span><span class="sxs-lookup"><span data-stu-id="2bf77-119">If you need to manage your Search resources from a .NET application, you can use the [Azure Search .NET Management SDK](https://aka.ms/search-mgmt-sdk).</span></span>

## <a name="upgrading-to-the-latest-version-of-the-sdk"></a><span data-ttu-id="2bf77-120">Aggiornamento alla versione più recente dell'SDK</span><span class="sxs-lookup"><span data-stu-id="2bf77-120">Upgrading to the latest version of the SDK</span></span>
<span data-ttu-id="2bf77-121">Se si usa già una versione precedente di Azure Search .NET SDK e si vuole eseguire l'aggiornamento alla nuova versione in disponibilità generale, seguire le indicazioni in [questo articolo](search-dotnet-sdk-migration.md) .</span><span class="sxs-lookup"><span data-stu-id="2bf77-121">If you're already using an older version of the Azure Search .NET SDK and you'd like to upgrade to the new generally available version, [this article](search-dotnet-sdk-migration.md) explains how.</span></span>

## <a name="requirements-for-the-sdk"></a><span data-ttu-id="2bf77-122">Requisiti per l'SDK</span><span class="sxs-lookup"><span data-stu-id="2bf77-122">Requirements for the SDK</span></span>
1. <span data-ttu-id="2bf77-123">Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="2bf77-123">Visual Studio 2017.</span></span>
2. <span data-ttu-id="2bf77-124">Un servizio di Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="2bf77-124">Your own Azure Search service.</span></span> <span data-ttu-id="2bf77-125">Per utilizzare l'SDK, è necessario il nome del servizio e una o più chiavi API.</span><span class="sxs-lookup"><span data-stu-id="2bf77-125">In order to use the SDK, you will need the name of your service and one or more API keys.</span></span> <span data-ttu-id="2bf77-126">[Creare un servizio nel portale](search-create-service-portal.md) per eseguire facilmente questi passaggi.</span><span class="sxs-lookup"><span data-stu-id="2bf77-126">[Create a service in the portal](search-create-service-portal.md) will help you through these steps.</span></span>
3. <span data-ttu-id="2bf77-127">Scaricare il [pacchetto NuGet](http://www.nuget.org/packages/Microsoft.Azure.Search) di SDK .NET di Ricerca di Azure tramite "Gestisci pacchetti NuGet" in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2bf77-127">Download the Azure Search .NET SDK [NuGet package](http://www.nuget.org/packages/Microsoft.Azure.Search) by using "Manage NuGet Packages" in Visual Studio.</span></span> <span data-ttu-id="2bf77-128">Cercare il nome del pacchetto `Microsoft.Azure.Search` su NuGet.org.</span><span class="sxs-lookup"><span data-stu-id="2bf77-128">Just search for the package name `Microsoft.Azure.Search` on NuGet.org.</span></span>

<span data-ttu-id="2bf77-129">Azure Search .NET SDK supporta applicazioni destinate a .NET Framework 4.6 e .NET Core.</span><span class="sxs-lookup"><span data-stu-id="2bf77-129">The Azure Search .NET SDK supports applications targeting the .NET Framework 4.6 and .NET Core.</span></span>

## <a name="core-scenarios"></a><span data-ttu-id="2bf77-130">Scenari chiave</span><span class="sxs-lookup"><span data-stu-id="2bf77-130">Core scenarios</span></span>
<span data-ttu-id="2bf77-131">Esistono diverse operazioni che è necessario eseguire nell'applicazione di ricerca.</span><span class="sxs-lookup"><span data-stu-id="2bf77-131">There are several things you'll need to do in your search application.</span></span> <span data-ttu-id="2bf77-132">In questa esercitazione saranno illustrati questi scenari chiave:</span><span class="sxs-lookup"><span data-stu-id="2bf77-132">In this tutorial, we'll cover these core scenarios:</span></span>

* <span data-ttu-id="2bf77-133">Creazione di un indice</span><span class="sxs-lookup"><span data-stu-id="2bf77-133">Creating an index</span></span>
* <span data-ttu-id="2bf77-134">Popolamento dell’indice con i documenti</span><span class="sxs-lookup"><span data-stu-id="2bf77-134">Populating the index with documents</span></span>
* <span data-ttu-id="2bf77-135">Ricerca di documenti mediante filtri e ricerca con testo completo</span><span class="sxs-lookup"><span data-stu-id="2bf77-135">Searching for documents using full-text search and filters</span></span>

<span data-ttu-id="2bf77-136">Il codice di esempio che segue illustra ciascuna di queste operazioni.</span><span class="sxs-lookup"><span data-stu-id="2bf77-136">The sample code that follows illustrates each of these.</span></span> <span data-ttu-id="2bf77-137">È possibile utilizzare i frammenti di codice nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-137">Feel free to use the code snippets in your own application.</span></span>

### <a name="overview"></a><span data-ttu-id="2bf77-138">Overview</span><span class="sxs-lookup"><span data-stu-id="2bf77-138">Overview</span></span>
<span data-ttu-id="2bf77-139">L'applicazione di esempio crea un nuovo indice denominato "hotels", vi inserisce alcuni documenti, quindi esegue alcune query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="2bf77-139">The sample application we'll be exploring creates a new index named "hotels", populates it with a few documents, then executes some search queries.</span></span> <span data-ttu-id="2bf77-140">Ecco il programma principale che mostra il flusso generale:</span><span class="sxs-lookup"><span data-stu-id="2bf77-140">Here is the main program, showing the overall flow:</span></span>

```csharp
// This sample shows how to delete, create, upload documents and query an index
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

    Console.WriteLine("{0}", "Complete.  Press any key to end application...\n");
    Console.ReadKey();
}
```

> [!NOTE]
> <span data-ttu-id="2bf77-141">Il codice sorgente completo dell'applicazione di esempio utilizzata è disponibile in questa procedura dettagliata su [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="2bf77-141">You can find the full source code of the sample application used in this walk through on [GitHub](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>
> 
>

<span data-ttu-id="2bf77-142">La procedura verrà illustrata passo per passo.</span><span class="sxs-lookup"><span data-stu-id="2bf77-142">We'll walk through this step by step.</span></span> <span data-ttu-id="2bf77-143">In primo luogo è necessario creare un nuovo `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-143">First we need to create a new `SearchServiceClient`.</span></span> <span data-ttu-id="2bf77-144">Questo oggetto consente di gestire gli indici.</span><span class="sxs-lookup"><span data-stu-id="2bf77-144">This object allows you to manage indexes.</span></span> <span data-ttu-id="2bf77-145">Per creare uno, è necessario fornire il nome del servizio Ricerca di Azure, nonché una chiave API di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-145">In order to construct one, you need to provide your Azure Search service name as well as an admin API key.</span></span> <span data-ttu-id="2bf77-146">È possibile immettere queste informazioni nel file `appsettings.json` dell'[applicazione di esempio](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="2bf77-146">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

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
> <span data-ttu-id="2bf77-147">Se si fornisce una chiave non corretta (ad esempio una chiave di query dove era richiesta una chiave di amministrazione), `SearchServiceClient` invierà un `CloudException` con il messaggio di errore "Non consentito" la prima volta che si chiama un metodo di operazione, ad esempio `Indexes.Create`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-147">If you provide an incorrect key (for example, a query key where an admin key was required), the `SearchServiceClient` will throw a `CloudException` with the error message "Forbidden" the first time you call an operation method on it, such as `Indexes.Create`.</span></span> <span data-ttu-id="2bf77-148">In questo caso, eseguire una doppia verifica della chiave API.</span><span class="sxs-lookup"><span data-stu-id="2bf77-148">If this happens to you, double-check our API key.</span></span>
> 
> 

<span data-ttu-id="2bf77-149">Le righe successive chiamano i metodi per creare un indice denominato "hotels", eliminandolo prima se esiste già.</span><span class="sxs-lookup"><span data-stu-id="2bf77-149">The next few lines call methods to create an index named "hotels", deleting it first if it already exists.</span></span> <span data-ttu-id="2bf77-150">Tali metodi saranno illustrati più avanti.</span><span class="sxs-lookup"><span data-stu-id="2bf77-150">We will walk through these methods a little later.</span></span>

```csharp
Console.WriteLine("{0}", "Deleting index...\n");
DeleteHotelsIndexIfExists(serviceClient);

Console.WriteLine("{0}", "Creating index...\n");
CreateHotelsIndex(serviceClient);
```

<span data-ttu-id="2bf77-151">Successivamente, l'indice deve essere popolato.</span><span class="sxs-lookup"><span data-stu-id="2bf77-151">Next, the index needs to be populated.</span></span> <span data-ttu-id="2bf77-152">A tale scopo, è necessario un `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-152">To do this, we will need a `SearchIndexClient`.</span></span> <span data-ttu-id="2bf77-153">Esistono due modi per ottenere uno: creandolo oppure chiamando `Indexes.GetClient` sul `SearchServiceClient`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-153">There are two ways to obtain one: by constructing it, or by calling `Indexes.GetClient` on the `SearchServiceClient`.</span></span> <span data-ttu-id="2bf77-154">Per comodità, sarà utilizzato il secondo.</span><span class="sxs-lookup"><span data-stu-id="2bf77-154">We use the latter for convenience.</span></span>

```csharp
ISearchIndexClient indexClient = serviceClient.Indexes.GetClient("hotels");
```

> [!NOTE]
> <span data-ttu-id="2bf77-155">In un'applicazione di ricerca tipica, il popolamento e la gestione degli indici viene gestita da un componente separato dalle query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="2bf77-155">In a typical search application, index management and population is handled by a separate component from search queries.</span></span> <span data-ttu-id="2bf77-156">`Indexes.GetClient` è utile per il popolamento di un indice perché evita di specificare un altro `SearchCredentials`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-156">`Indexes.GetClient` is convenient for populating an index because it saves you the trouble of providing another `SearchCredentials`.</span></span> <span data-ttu-id="2bf77-157">Questa operazione viene eseguita passando la chiave di amministrazione utilizzata per creare il `SearchServiceClient` al nuovo `SearchIndexClient`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-157">It does this by passing the admin key that you used to create the `SearchServiceClient` to the new `SearchIndexClient`.</span></span> <span data-ttu-id="2bf77-158">Tuttavia, nella parte dell'applicazione che esegue le query, è preferibile creare il `SearchIndexClient` direttamente in modo che sia possibile passare una chiave di query anziché una chiave di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-158">However, in the part of your application that executes queries, it is better to create the `SearchIndexClient` directly so that you can pass in a query key instead of an admin key.</span></span> <span data-ttu-id="2bf77-159">Questo procedimento è coerente con il principio del privilegio minimo e consente di rendere più sicura l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-159">This is consistent with the principle of least privilege and will help to make your application more secure.</span></span> <span data-ttu-id="2bf77-160">È possibile trovare ulteriori informazioni su chiavi di amministrazione e chiavi di query [qui](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span><span class="sxs-lookup"><span data-stu-id="2bf77-160">You can find out more about admin keys and query keys [here](https://docs.microsoft.com/rest/api/searchservice/#authentication-and-authorization).</span></span>
> 
> 

<span data-ttu-id="2bf77-161">Ora che è disponibile un `SearchIndexClient`, è possibile popolare l'indice.</span><span class="sxs-lookup"><span data-stu-id="2bf77-161">Now that we have a `SearchIndexClient`, we can populate the index.</span></span> <span data-ttu-id="2bf77-162">A tal fine verrà utilizzato un altro metodo che verrà descritto più avanti.</span><span class="sxs-lookup"><span data-stu-id="2bf77-162">This is done by another method that we will walk through later.</span></span>

```csharp
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(indexClient);
```

<span data-ttu-id="2bf77-163">Infine, saranno eseguite alcune query di ricerca e visualizzati i risultati.</span><span class="sxs-lookup"><span data-stu-id="2bf77-163">Finally, we execute a few search queries and display the results.</span></span> <span data-ttu-id="2bf77-164">In questo caso viene utilizzato un `SearchIndexClient` diverso:</span><span class="sxs-lookup"><span data-stu-id="2bf77-164">This time we use a different `SearchIndexClient`:</span></span>

```csharp
ISearchIndexClient indexClientForQueries = CreateSearchIndexClient(configuration);

RunQueries(indexClientForQueries);
```

<span data-ttu-id="2bf77-165">Esamineremo il metodo `RunQueries` più da vicino in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="2bf77-165">We will take a closer look at the `RunQueries` method later.</span></span> <span data-ttu-id="2bf77-166">Ecco il codice per creare il nuovo `SearchIndexClient`:</span><span class="sxs-lookup"><span data-stu-id="2bf77-166">Here is the code to create the new `SearchIndexClient`:</span></span>

```csharp
private static SearchIndexClient CreateSearchIndexClient(IConfigurationRoot configuration)
{
    string searchServiceName = configuration["SearchServiceName"];
    string queryApiKey = configuration["SearchServiceQueryApiKey"];

    SearchIndexClient indexClient = new SearchIndexClient(searchServiceName, "hotels", new SearchCredentials(queryApiKey));
    return indexClient;
}
```

<span data-ttu-id="2bf77-167">In questo caso è utilizzata una chiave di query poiché non è necessario l'accesso in scrittura all'indice.</span><span class="sxs-lookup"><span data-stu-id="2bf77-167">This time we use a query key since we do not need write access to the index.</span></span> <span data-ttu-id="2bf77-168">È possibile immettere queste informazioni nel file `appsettings.json` dell'[applicazione di esempio](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span><span class="sxs-lookup"><span data-stu-id="2bf77-168">You can enter this information in the `appsettings.json` file of the [sample application](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowTo).</span></span>

<span data-ttu-id="2bf77-169">Se si esegue questa applicazione con un nome di servizio valido e le chiavi API, l'output dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2bf77-169">If you run this application with a valid service name and API keys, the output should look like this:</span></span>

    Deleting index...
    
    Creating index...
    
    Uploading documents...
    
    Waiting for documents to be indexed...
    
    Search the entire index for the term 'budget' and return only the hotelName field:
    
    Name: Roach Motel
    
    Apply a filter to the index to find hotels cheaper than $150 per night, and return the hotelId and description:
    
    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river
    
    Search the entire index, order by a specific field (lastRenovationDate) in descending order, take the top two results, and show only hotelName and lastRenovationDate:
    
    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00
    
    Search the entire index for the term 'motel':
    
    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577
    
    Complete.  Press any key to end application...

<span data-ttu-id="2bf77-170">Alla fine di questo articolo viene fornito il codice sorgente completo dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-170">The full source code of the application is provided at the end of this article.</span></span>

<span data-ttu-id="2bf77-171">Successivamente, verrà esaminato ognuno dei metodi chiamati da `Main`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-171">Next, we will take a closer look at each of the methods called by `Main`.</span></span>

### <a name="creating-an-index"></a><span data-ttu-id="2bf77-172">Creazione di un indice</span><span class="sxs-lookup"><span data-stu-id="2bf77-172">Creating an index</span></span>
<span data-ttu-id="2bf77-173">Dopo aver creato un `SearchServiceClient`, l'operazione successiva `Main` è l’eliminazione dell’indice "hotel" se esiste già.</span><span class="sxs-lookup"><span data-stu-id="2bf77-173">After creating a `SearchServiceClient`, the next thing `Main` does is delete the "hotels" index if it already exists.</span></span> <span data-ttu-id="2bf77-174">Questa operazione viene eseguita con il metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="2bf77-174">That is done by the following method:</span></span>

```csharp
private static void DeleteHotelsIndexIfExists(SearchServiceClient serviceClient)
{
    if (serviceClient.Indexes.Exists("hotels"))
    {
        serviceClient.Indexes.Delete("hotels");
    }
}
```

<span data-ttu-id="2bf77-175">Questo metodo utilizza il `SearchServiceClient` fornito per verificare l'esistenza dell'indice ed eventualmente eliminarlo.</span><span class="sxs-lookup"><span data-stu-id="2bf77-175">This method uses the given `SearchServiceClient` to check if the index exists, and if so, delete it.</span></span>

> [!NOTE]
> <span data-ttu-id="2bf77-176">Il codice di esempio riportato in questo articolo utilizza i metodi sincroni di .NET SDK di Ricerca di Azure per motivi di semplicità.</span><span class="sxs-lookup"><span data-stu-id="2bf77-176">The example code in this article uses the synchronous methods of the Azure Search .NET SDK for simplicity.</span></span> <span data-ttu-id="2bf77-177">È consigliabile utilizzare i metodi asincroni nelle proprie applicazioni per mantenerle scalabili e reattive.</span><span class="sxs-lookup"><span data-stu-id="2bf77-177">We recommend that you use the asynchronous methods in your own applications to keep them scalable and responsive.</span></span> <span data-ttu-id="2bf77-178">Ad esempio, nel metodo precedente è possibile utilizzare `ExistsAsync` e `DeleteAsync` anziché `Exists` e `Delete`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-178">For example, in the method above you could use `ExistsAsync` and `DeleteAsync` instead of `Exists` and `Delete`.</span></span>
> 
> 

<span data-ttu-id="2bf77-179">Successivamente, `Main` crea un nuovo indice "hotel" chiamando questo metodo:</span><span class="sxs-lookup"><span data-stu-id="2bf77-179">Next, `Main` creates a new "hotels" index by calling this method:</span></span>

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

<span data-ttu-id="2bf77-180">Questo metodo crea un nuovo oggetto `Index` con un elenco di oggetti `Field` che definisce lo schema del nuovo indice.</span><span class="sxs-lookup"><span data-stu-id="2bf77-180">This method creates a new `Index` object with a list of `Field` objects that defines the schema of the new index.</span></span> <span data-ttu-id="2bf77-181">Ogni campo ha un nome, un tipo di dati e diversi attributi che definiscono il comportamento della ricerca.</span><span class="sxs-lookup"><span data-stu-id="2bf77-181">Each field has a name, data type, and several attributes that define its search behavior.</span></span> <span data-ttu-id="2bf77-182">La classe `FieldBuilder` utilizza la reflection per creare un elenco di oggetti `Field` per l'indice esaminando le proprietà pubbliche e gli attributi della classe modello `Hotel` specificata.</span><span class="sxs-lookup"><span data-stu-id="2bf77-182">The `FieldBuilder` class uses reflection to create a list of `Field` objects for the index by examining the public properties and attributes of the given `Hotel` model class.</span></span> <span data-ttu-id="2bf77-183">Esamineremo la classe `Hotel` più da vicino in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="2bf77-183">We'll take a closer look at the `Hotel` class later on.</span></span>

> [!NOTE]
> <span data-ttu-id="2bf77-184">Se necessario, è inoltre possibile creare l'elenco di oggetti `Field` direttamente anziché utilizzando `FieldBuilder`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-184">You can always create the list of `Field` objects directly instead of using `FieldBuilder` if needed.</span></span> <span data-ttu-id="2bf77-185">Ad esempio, è possibile evitare di utilizzare una classe modello o potrebbe essere necessario utilizzare una classe modello esistente che non si desidera modificare aggiungendo attributi.</span><span class="sxs-lookup"><span data-stu-id="2bf77-185">For example, you may not want to use a model class or you may need to use an existing model class that you don't want to modify by adding attributes.</span></span>
>
> 

<span data-ttu-id="2bf77-186">Oltre ai campi, è possibile aggiungere anche profili di punteggio, suggerimenti di alternative o opzioni CORS per l'indice. Per motivi di brevità nell’esempio questi elementi sono stati omessi.</span><span class="sxs-lookup"><span data-stu-id="2bf77-186">In addition to fields, you can also add scoring profiles, suggesters, or CORS options to the Index (these are omitted from the sample for brevity).</span></span> <span data-ttu-id="2bf77-187">Altre informazioni sull'oggetto indice e le relative parti costituenti sono disponibili nella [guida di riferimento dell'SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index) e nella [guida di riferimento dell'interfaccia API REST di Ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="2bf77-187">You can find more information about the Index object and its constituent parts in the [SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.index#microsoft_azure_search_models_index), as well as in the [Azure Search REST API reference](https://docs.microsoft.com/rest/api/searchservice/).</span></span>

### <a name="populating-the-index"></a><span data-ttu-id="2bf77-188">Popolamento dell'indice</span><span class="sxs-lookup"><span data-stu-id="2bf77-188">Populating the index</span></span>
<span data-ttu-id="2bf77-189">Il passaggio successivo in `Main` è il popolamento dell'indice appena creato.</span><span class="sxs-lookup"><span data-stu-id="2bf77-189">The next step in `Main` is to populate the newly-created index.</span></span> <span data-ttu-id="2bf77-190">Questa operazione viene eseguita nel metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="2bf77-190">This is done in the following method:</span></span>

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
            Description = "Close to town hall and the river"
        }
    };

    var batch = IndexBatch.Upload(hotels);

    try
    {
        indexClient.Documents.Index(batch);
    }
    catch (IndexBatchException e)
    {
        // Sometimes when your Search service is under load, indexing will fail for some of the documents in
        // the batch. Depending on your application, you can take compensating actions like delaying and
        // retrying. For this simple demo, we just log the failed document keys and continue.
        Console.WriteLine(
            "Failed to index some of the documents: {0}",
            String.Join(", ", e.IndexingResults.Where(r => !r.Succeeded).Select(r => r.Key)));
    }

    Console.WriteLine("Waiting for documents to be indexed...\n");
    Thread.Sleep(2000);
}
```

<span data-ttu-id="2bf77-191">Questo metodo è costituito da quattro parti.</span><span class="sxs-lookup"><span data-stu-id="2bf77-191">This method has four parts.</span></span> <span data-ttu-id="2bf77-192">La prima crea una matrice di oggetti `Hotel` che verranno utilizzati come dati di input per caricare l'indice.</span><span class="sxs-lookup"><span data-stu-id="2bf77-192">The first creates an array of `Hotel` objects that will serve as our input data to upload to the index.</span></span> <span data-ttu-id="2bf77-193">Questi dati sono hardcoded per motivi di semplicità.</span><span class="sxs-lookup"><span data-stu-id="2bf77-193">This data is hard-coded for simplicity.</span></span> <span data-ttu-id="2bf77-194">Nell'applicazione, i dati probabilmente proverranno da un'origine dati esterna, ad esempio un database SQL.</span><span class="sxs-lookup"><span data-stu-id="2bf77-194">In your own application, your data will likely come from an external data source such as a SQL database.</span></span>

<span data-ttu-id="2bf77-195">La seconda parte crea un oggetto `IndexBatch` contenente i documenti.</span><span class="sxs-lookup"><span data-stu-id="2bf77-195">The second part creates an `IndexBatch` containing the documents.</span></span> <span data-ttu-id="2bf77-196">Specificare l'operazione che si vuole applicare al batch al momento della creazione, in questo caso chiamando `IndexBatch.Upload`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-196">You specify the operation you want to apply to the batch at the time you create it, in this case by calling `IndexBatch.Upload`.</span></span> <span data-ttu-id="2bf77-197">Il batch viene quindi caricato nell'indice di Ricerca di Azure dal metodo `Documents.Index` .</span><span class="sxs-lookup"><span data-stu-id="2bf77-197">The batch is then uploaded to the Azure Search index by the `Documents.Index` method.</span></span>

> [!NOTE]
> <span data-ttu-id="2bf77-198">In questo esempio, verranno semplicemente caricati i documenti.</span><span class="sxs-lookup"><span data-stu-id="2bf77-198">In this example, we are just uploading documents.</span></span> <span data-ttu-id="2bf77-199">Se invece si vogliono unire le modifiche in documenti esistenti o eliminare documenti, creare batch chiamando `IndexBatch.Merge`, `IndexBatch.MergeOrUpload` o `IndexBatch.Delete`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-199">If you wanted to merge changes into existing documents or delete documents, you could create batches by calling `IndexBatch.Merge`, `IndexBatch.MergeOrUpload`, or `IndexBatch.Delete` instead.</span></span> <span data-ttu-id="2bf77-200">È inoltre possibile combinare diverse operazioni in un singolo batch chiamando `IndexBatch.New`, che accetta una raccolta di oggetti `IndexAction`, ognuno dei quali indica a Ricerca di Azure di eseguire una particolare operazione su un documento.</span><span class="sxs-lookup"><span data-stu-id="2bf77-200">You can also mix different operations in a single batch by calling `IndexBatch.New`, which takes a collection of `IndexAction` objects, each of which tells Azure Search to perform a particular operation on a document.</span></span> <span data-ttu-id="2bf77-201">È possibile creare ogni oggetto `IndexAction` con la propria operazione chiamando il metodo corrispondente, ad esempio `IndexAction.Merge`, `IndexAction.Upload` e così via.</span><span class="sxs-lookup"><span data-stu-id="2bf77-201">You can create each `IndexAction` with its own operation by calling the corresponding method such as `IndexAction.Merge`, `IndexAction.Upload`, and so on.</span></span>
> 
> 

<span data-ttu-id="2bf77-202">La terza parte di questo metodo è un blocco catch che gestisce un caso di errore importante per l'indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-202">The third part of this method is a catch block that handles an important error case for indexing.</span></span> <span data-ttu-id="2bf77-203">Se il servizio Ricerca di Azure non riesce a indicizzare alcuni dei documenti nel batch, viene generato un `IndexBatchException` da `Documents.Index`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-203">If your Azure Search service fails to index some of the documents in the batch, an `IndexBatchException` is thrown by `Documents.Index`.</span></span> <span data-ttu-id="2bf77-204">Questa situazione può verificarsi se l'indicizzazione dei documenti avviene mentre il servizio è sovraccarico.</span><span class="sxs-lookup"><span data-stu-id="2bf77-204">This can happen if you are indexing documents while your service is under heavy load.</span></span> <span data-ttu-id="2bf77-205">**Si consiglia di gestire in modo esplicito questo caso nel codice.**</span><span class="sxs-lookup"><span data-stu-id="2bf77-205">**We strongly recommend explicitly handling this case in your code.**</span></span> <span data-ttu-id="2bf77-206">È possibile ritardare e quindi ritentare l'indicizzazione di documenti, accedere e continuare come nell'esempio,  oppure eseguire altre attività a seconda dei requisiti di coerenza di dati dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-206">You can delay and then retry indexing the documents that failed, or you can log and continue like the sample does, or you can do something else depending on your application's data consistency requirements.</span></span>

> [!NOTE]
> <span data-ttu-id="2bf77-207">È possibile utilizzare il metodo `FindFailedActionsToRetry` per costruire un nuovo batch contenente solo le azioni non riuscite in una precedente chiamata a `Index`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-207">You can use the `FindFailedActionsToRetry` method to construct a new batch containing only the actions that failed in a previous call to `Index`.</span></span> <span data-ttu-id="2bf77-208">Il metodo è documentato [qui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) ed è una discussione su come utilizzarlo in modo corretto [su StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span><span class="sxs-lookup"><span data-stu-id="2bf77-208">The method is documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.indexbatchexception#Microsoft_Azure_Search_IndexBatchException_FindFailedActionsToRetry_Microsoft_Azure_Search_Models_IndexBatch_System_String_) and there is a discussion of how to properly use it [on StackOverflow](http://stackoverflow.com/questions/40012885/azure-search-net-sdk-how-to-use-findfailedactionstoretry).</span></span>
>
>

<span data-ttu-id="2bf77-209">Infine, il metodo `UploadDocuments` ritarda per due secondi.</span><span class="sxs-lookup"><span data-stu-id="2bf77-209">Finally, the `UploadDocuments` method delays for two seconds.</span></span> <span data-ttu-id="2bf77-210">L'indicizzazione avviene in modo asincrono nel servizio Ricerca di Azure, pertanto l'applicazione di esempio deve attendere un breve periodo per garantire che i documenti siano disponibili per la ricerca.</span><span class="sxs-lookup"><span data-stu-id="2bf77-210">Indexing happens asynchronously in your Azure Search service, so the sample application needs to wait a short time to ensure that the documents are available for searching.</span></span> <span data-ttu-id="2bf77-211">Ritardi come questi in genere sono necessari solo in applicazioni di esempio, test e demo.</span><span class="sxs-lookup"><span data-stu-id="2bf77-211">Delays like this are typically only necessary in demos, tests, and sample applications.</span></span>

#### <a name="how-the-net-sdk-handles-documents"></a><span data-ttu-id="2bf77-212">Modalità di gestione dei documenti in .NET SDK</span><span class="sxs-lookup"><span data-stu-id="2bf77-212">How the .NET SDK handles documents</span></span>
<span data-ttu-id="2bf77-213">Per capire in che modo .NET SDK di Ricerca di Azure è in grado di caricare le istanze di una classe definita dall'utente come `Hotel` nell'indice,</span><span class="sxs-lookup"><span data-stu-id="2bf77-213">You may be wondering how the Azure Search .NET SDK is able to upload instances of a user-defined class like `Hotel` to the index.</span></span> <span data-ttu-id="2bf77-214">è possibile esaminare la classe `Hotel`:</span><span class="sxs-lookup"><span data-stu-id="2bf77-214">To help answer that question, let's look at the `Hotel` class:</span></span>

```csharp
using System;
using Microsoft.Azure.Search;
using Microsoft.Azure.Search.Models;
using Microsoft.Spatial;
using Newtonsoft.Json;

// The SerializePropertyNamesAsCamelCase attribute is defined in the Azure Search .NET SDK.
// It ensures that Pascal-case property names in the model class are mapped to camel-case
// field names in the index.
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

<span data-ttu-id="2bf77-215">La prima cosa da notare è che ogni proprietà pubblica di `Hotel` corrisponde a un campo nella definizione dell'indice, ma con una differenza fondamentale: il nome di ogni campo inizia con una lettera minuscola ("convenzione camel"), mentre il nome di ogni proprietà pubblica di `Hotel` inizia con una lettera maiuscola ("convenzione Pascal").</span><span class="sxs-lookup"><span data-stu-id="2bf77-215">The first thing to notice is that each public property of `Hotel` corresponds to a field in the index definition, but with one crucial difference: The name of each field starts with a lower-case letter ("camel case"), while the name of each public property of `Hotel` starts with an upper-case letter ("Pascal case").</span></span> <span data-ttu-id="2bf77-216">Si tratta di uno scenario comune in applicazioni .NET che consentono di eseguire l'associazione dati in cui lo schema di destinazione è fuori dal controllo dello sviluppatore dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-216">This is a common scenario in .NET applications that perform data-binding where the target schema is outside the control of the application developer.</span></span> <span data-ttu-id="2bf77-217">Anziché dover violare linee guida sulla denominazione di .NET seguendo la convenzione camel per i nomi delle proprietà, è possibile indicare a SDK di eseguire automaticamente il mapping dei nomi delle proprietà alla convenzione camel con l’attributo `[SerializePropertyNamesAsCamelCase]` .</span><span class="sxs-lookup"><span data-stu-id="2bf77-217">Rather than having to violate the .NET naming guidelines by making property names camel-case, you can tell the SDK to map the property names to camel-case automatically with the `[SerializePropertyNamesAsCamelCase]` attribute.</span></span>

> [!NOTE]
> <span data-ttu-id="2bf77-218">Azure Search .NET SDK usa la libreria [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) per serializzare e deserializzare gli oggetti modello personalizzati in e da JSON.</span><span class="sxs-lookup"><span data-stu-id="2bf77-218">The Azure Search .NET SDK uses the [NewtonSoft JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) library to serialize and deserialize your custom model objects to and from JSON.</span></span> <span data-ttu-id="2bf77-219">Se necessario, è possibile personalizzare questa serializzazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-219">You can customize this serialization if needed.</span></span> <span data-ttu-id="2bf77-220">Per altre informazioni, vedere [Serializzazione personalizzata con JSON.NET](#JsonDotNet).</span><span class="sxs-lookup"><span data-stu-id="2bf77-220">For more details, see [Custom Serialization with JSON.NET](#JsonDotNet).</span></span>
> 
> 

<span data-ttu-id="2bf77-221">La seconda cosa da notare sono gli attributi, ad esempio `IsFilterable`, `IsSearchable`, `Key` e `Analyzer`, che decorano ogni proprietà pubblica.</span><span class="sxs-lookup"><span data-stu-id="2bf77-221">The second thing to notice are the attributes such as `IsFilterable`, `IsSearchable`, `Key`, and `Analyzer` that decorate each public property.</span></span> <span data-ttu-id="2bf77-222">Questi attributi eseguono il mapping direttamente agli [attributi corrispondenti dell'indice di Ricerca di Azure](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span><span class="sxs-lookup"><span data-stu-id="2bf77-222">These attributes map directly to the [corresponding attributes of the Azure Search index](https://docs.microsoft.com/rest/api/searchservice/create-index#request).</span></span> <span data-ttu-id="2bf77-223">La classe `FieldBuilder` li utilizza per creare definizioni di campo per l'indice.</span><span class="sxs-lookup"><span data-stu-id="2bf77-223">The `FieldBuilder` class uses these to construct field definitions for the index.</span></span>

<span data-ttu-id="2bf77-224">Il terzo aspetto importante della classe `Hotel` sono i tipi di dati delle proprietà pubbliche.</span><span class="sxs-lookup"><span data-stu-id="2bf77-224">The third important thing about the `Hotel` class are the data types of the public properties.</span></span> <span data-ttu-id="2bf77-225">I tipi .NET di queste proprietà eseguono il mapping ai tipi di campi equivalenti nella definizione dell'indice.</span><span class="sxs-lookup"><span data-stu-id="2bf77-225">The .NET types of  these properties map to their equivalent field types in the index definition.</span></span> <span data-ttu-id="2bf77-226">Ad esempio, viene eseguito il mapping della proprietà stringa `Category` al campo `category`, che è di tipo `Edm.String`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-226">For example, the `Category` string property maps to the `category` field, which is of type `Edm.String`.</span></span> <span data-ttu-id="2bf77-227">Esistono mapping di tipi simili tra `bool?` e `Edm.Boolean`, `DateTimeOffset?` e `Edm.DateTimeOffset` ecc. Le regole specifiche per il mapping dei tipi sono documentate con il metodo `Documents.Get` nella [documentazione di riferimento relativa a .NET SDK di Ricerca di Azure](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span><span class="sxs-lookup"><span data-stu-id="2bf77-227">There are similar type mappings between `bool?` and `Edm.Boolean`, `DateTimeOffset?` and `Edm.DateTimeOffset`, etc. The specific rules for the type mapping are documented with the `Documents.Get` method in the [Azure Search .NET SDK reference](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.idocumentsoperations#Microsoft_Azure_Search_IDocumentsOperations_GetWithHttpMessagesAsync__1_System_String_System_Collections_Generic_IEnumerable_System_String__Microsoft_Azure_Search_Models_SearchRequestOptions_System_Collections_Generic_Dictionary_System_String_System_Collections_Generic_List_System_String___System_Threading_CancellationToken_).</span></span> <span data-ttu-id="2bf77-228">La classe `FieldBuilder` si occupa di questo mapping automaticamente, ma la comprensione può comunque essere utile nel caso in cui sia necessario risolvere eventuali problemi di serializzazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-228">The `FieldBuilder` class takes care of this mapping for you, but it can still be helpful to understand in case you need to troubleshoot any serialization issues.</span></span>

<span data-ttu-id="2bf77-229">La possibilità di utilizzare le proprie classi come documenti funziona in entrambe le direzioni; è possibile, inoltre, recuperare i risultati della ricerca e far sì che SDK li deserializzi automaticamente in un tipo di propria scelta, come sarà illustrato nella prossima sezione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-229">This ability to use your own classes as documents works in both directions; You can also retrieve search results and have the SDK automatically deserialize them to a type of your choice, as we will see in the next section.</span></span>

> [!NOTE]
> <span data-ttu-id="2bf77-230">.NET SDK di Ricerca di Azure supporta anche documenti tipizzati in modo dinamico utilizzando la classe `Document`, un mapping chiave/valore dei campi e valori dei campi.</span><span class="sxs-lookup"><span data-stu-id="2bf77-230">The Azure Search .NET SDK also supports dynamically-typed documents using the `Document` class, which is a key/value mapping of field names to field values.</span></span> <span data-ttu-id="2bf77-231">Ciò è utile negli scenari in cui non si conosce lo schema di indice in fase di progettazione o quando l’associazione a classi di modello specifico non sarebbe conveniente.</span><span class="sxs-lookup"><span data-stu-id="2bf77-231">This is useful in scenarios where you don't know the index schema at design-time, or where it would be inconvenient to bind to specific model classes.</span></span> <span data-ttu-id="2bf77-232">Tutti i metodi in SDK che gestiscono documenti dispongono di overload che funzionano con la classe `Document` , nonché overload fortemente tipizzati che accettano un parametro di tipo generico.</span><span class="sxs-lookup"><span data-stu-id="2bf77-232">All the methods in the SDK that deal with documents have overloads that work with the `Document` class, as well as strongly-typed overloads that take a generic type parameter.</span></span> <span data-ttu-id="2bf77-233">Solo questi ultimi vengono utilizzati nell'esempio di codice fornito in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-233">Only the latter are used in the sample code in this tutorial.</span></span> <span data-ttu-id="2bf77-234">La classe `Document` eredita da `Dictionary<string, object>`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-234">The `Document` class inherits from `Dictionary<string, object>`.</span></span> <span data-ttu-id="2bf77-235">Per informazioni più dettagliate, vedere [qui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span><span class="sxs-lookup"><span data-stu-id="2bf77-235">You can find other details [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.document#microsoft_azure_search_models_document).</span></span>
> 
> 

<span data-ttu-id="2bf77-236">**Perché usare tipi di dati nullable**</span><span class="sxs-lookup"><span data-stu-id="2bf77-236">**Why you should use nullable data types**</span></span>

<span data-ttu-id="2bf77-237">Quando si progettano classi di modello personalizzate per eseguire il mapping a un indice di Ricerca di Azure, è consigliabile dichiarare le proprietà dei tipi di valore, ad esempio `bool` e `int` da rendere nullable (ad esempio, `bool?` invece di `bool`).</span><span class="sxs-lookup"><span data-stu-id="2bf77-237">When designing your own model classes to map to an Azure Search index, we recommend declaring properties of value types such as `bool` and `int` to be nullable (for example, `bool?` instead of `bool`).</span></span> <span data-ttu-id="2bf77-238">Se si usa una proprietà che non ammette i valori Null, è necessario **garantire** che nessun documento nell'indice contenga un valore Null per il campo corrispondente.</span><span class="sxs-lookup"><span data-stu-id="2bf77-238">If you use a non-nullable property, you have to **guarantee** that no documents in your index contain a null value for the corresponding field.</span></span> <span data-ttu-id="2bf77-239">Né l'SDK né il servizio di Ricerca di Azure consentiranno di applicare questo valore.</span><span class="sxs-lookup"><span data-stu-id="2bf77-239">Neither the SDK nor the Azure Search service will help you to enforce this.</span></span>

<span data-ttu-id="2bf77-240">Non è solo un problema ipotetico: si pensi a uno scenario in cui si aggiunge un nuovo campo a un indice esistente di tipo `Edm.Int32`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-240">This is not just a hypothetical concern: Imagine a scenario where you add a new field to an existing index that is of type `Edm.Int32`.</span></span> <span data-ttu-id="2bf77-241">Dopo l'aggiornamento della definizione dell'indice, tutti i documenti avranno un valore Null per il nuovo campo (perché tutti i tipi sono nullable in Ricerca di Azure).</span><span class="sxs-lookup"><span data-stu-id="2bf77-241">After updating the index definition, all documents will have a null value for that new field (since all types are nullable in Azure Search).</span></span> <span data-ttu-id="2bf77-242">Se quindi si usa una classe di modelli con una proprietà `int` che non ammette i valori Null per tale campo, verrà restituita un'eccezione `JsonSerializationException`, come questa, quando si cercherà di recuperare i documenti:</span><span class="sxs-lookup"><span data-stu-id="2bf77-242">If you then use a model class with a non-nullable `int` property for that field, you will get a `JsonSerializationException` like this when trying to retrieve documents:</span></span>

    Error converting value {null} to type 'System.Int32'. Path 'IntValue'.

<span data-ttu-id="2bf77-243">Per questo motivo, è consigliabile usare tipi nullable nelle classi di modelli.</span><span class="sxs-lookup"><span data-stu-id="2bf77-243">For this reason, we recommend that you use nullable types in your model classes as a best practice.</span></span>

<a name="JsonDotNet"></a>

#### <a name="custom-serialization-with-jsonnet"></a><span data-ttu-id="2bf77-244">Serializzazione personalizzata con JSON.NET</span><span class="sxs-lookup"><span data-stu-id="2bf77-244">Custom Serialization with JSON.NET</span></span>
<span data-ttu-id="2bf77-245">L'SDK usa JSON.NET per serializzare e deserializzare i documenti.</span><span class="sxs-lookup"><span data-stu-id="2bf77-245">The SDK uses JSON.NET for serializing and deserializing documents.</span></span> <span data-ttu-id="2bf77-246">Se necessario, è possibile personalizzare la serializzazione e deserializzazione definendo il proprio `JsonConverter` o `IContractResolver` (vedere la [ documentazione di JSON.NET](http://www.newtonsoft.com/json/help/html/Introduction.htm) per altri dettagli).</span><span class="sxs-lookup"><span data-stu-id="2bf77-246">You can customize serialization and deserialization if needed by defining your own `JsonConverter` or `IContractResolver` (see the [JSON.NET documentation](http://www.newtonsoft.com/json/help/html/Introduction.htm) for more details).</span></span> <span data-ttu-id="2bf77-247">Ciò può risultare utile quando si vuole adattare una classe modello esistente dell'applicazione per usarla con Ricerca di Azure e in altri scenari più avanzati.</span><span class="sxs-lookup"><span data-stu-id="2bf77-247">This can be useful when you want to adapt an existing model class from your application for use with Azure Search, and other more advanced scenarios.</span></span> <span data-ttu-id="2bf77-248">Con la serializzazione personalizzata, ad esempio, è possibile:</span><span class="sxs-lookup"><span data-stu-id="2bf77-248">For example, with custom serialization you can:</span></span>

* <span data-ttu-id="2bf77-249">Includere o escludere determinate proprietà della classe modello da archiviare come campi di un documento.</span><span class="sxs-lookup"><span data-stu-id="2bf77-249">Include or exclude certain properties of your model class from being stored as document fields.</span></span>
* <span data-ttu-id="2bf77-250">Eseguire il mapping tra i nomi di proprietà nel codice e i nomi di campo nell'indice.</span><span class="sxs-lookup"><span data-stu-id="2bf77-250">Map between property names in your code and field names in your index.</span></span>
* <span data-ttu-id="2bf77-251">Creare gli attributi personalizzati che possono essere utilizzati per il mapping di proprietà ai campi di documento.</span><span class="sxs-lookup"><span data-stu-id="2bf77-251">Create custom attributes that can be used for mapping properties to document fields.</span></span>

<span data-ttu-id="2bf77-252">Esempi di implementazione della serializzazione personalizzata sono disponibili negli unit test per Azure Search .NET SDK in GitHub.</span><span class="sxs-lookup"><span data-stu-id="2bf77-252">You can find examples of implementing custom serialization in the unit tests for the Azure Search .NET SDK on GitHub.</span></span> <span data-ttu-id="2bf77-253">È consigliabile iniziare da [questa cartella](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models),</span><span class="sxs-lookup"><span data-stu-id="2bf77-253">A good starting point is [this folder](https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Search/Search.Tests/Tests/Models).</span></span> <span data-ttu-id="2bf77-254">che contiene le classi usate dai test di serializzazione personalizzata.</span><span class="sxs-lookup"><span data-stu-id="2bf77-254">It contains classes that are used by the custom serialization tests.</span></span>

### <a name="searching-for-documents-in-the-index"></a><span data-ttu-id="2bf77-255">Ricerca di documenti nell'indice</span><span class="sxs-lookup"><span data-stu-id="2bf77-255">Searching for documents in the index</span></span>
<span data-ttu-id="2bf77-256">L'ultimo passaggio nell'applicazione di esempio è cercare alcuni documenti nell'indice.</span><span class="sxs-lookup"><span data-stu-id="2bf77-256">The last step in the sample application is to search for some documents in the index.</span></span> <span data-ttu-id="2bf77-257">A tale scopo viene utilizzato il metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="2bf77-257">The following method does this:</span></span>

```csharp
private static void RunQueries(ISearchIndexClient indexClient)
{
    SearchParameters parameters;
    DocumentSearchResult<Hotel> results;

    Console.WriteLine("Search the entire index for the term 'budget' and return only the hotelName field:\n");

    parameters =
        new SearchParameters()
        {
            Select = new[] { "hotelName" }
        };

    results = indexClient.Documents.Search<Hotel>("budget", parameters);

    WriteDocuments(results);

    Console.Write("Apply a filter to the index to find hotels cheaper than $150 per night, ");
    Console.WriteLine("and return the hotelId and description:\n");

    parameters =
        new SearchParameters()
        {
            Filter = "baseRate lt 150",
            Select = new[] { "hotelId", "description" }
        };

    results = indexClient.Documents.Search<Hotel>("*", parameters);

    WriteDocuments(results);

    Console.Write("Search the entire index, order by a specific field (lastRenovationDate) ");
    Console.Write("in descending order, take the top two results, and show only hotelName and ");
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

    Console.WriteLine("Search the entire index for the term 'motel':\n");

    parameters = new SearchParameters();
    results = indexClient.Documents.Search<Hotel>("motel", parameters);

    WriteDocuments(results);
}
```

<span data-ttu-id="2bf77-258">Ogni volta che viene eseguita una query, questo metodo crea prima un nuovo oggetto `SearchParameters`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-258">Each time it executes a query, this method first creates a new `SearchParameters` object.</span></span> <span data-ttu-id="2bf77-259">Consente di specificare opzioni aggiuntive per la query di ordinamento, filtro, impaginazione e faceting.</span><span class="sxs-lookup"><span data-stu-id="2bf77-259">This is used to specify additional options for the query such as sorting, filtering, paging, and faceting.</span></span> <span data-ttu-id="2bf77-260">In questo metodo, impostiamo le proprietà `Filter`, `Select`, `OrderBy` e `Top` per diverse query.</span><span class="sxs-lookup"><span data-stu-id="2bf77-260">In this method, we're setting the `Filter`, `Select`, `OrderBy`, and `Top` property for different queries.</span></span> <span data-ttu-id="2bf77-261">Tutte le proprietà `SearchParameters` sono documentate [qui](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span><span class="sxs-lookup"><span data-stu-id="2bf77-261">All the `SearchParameters` properties are documented [here](https://docs.microsoft.com/dotnet/api/microsoft.azure.search.models.searchparameters).</span></span>

<span data-ttu-id="2bf77-262">Il passaggio successivo consiste nell’esecuzione effettiva della query di ricerca.</span><span class="sxs-lookup"><span data-stu-id="2bf77-262">The next step is to actually execute the search query.</span></span> <span data-ttu-id="2bf77-263">Questa operazione viene effettuata con il metodo `Documents.Search` .</span><span class="sxs-lookup"><span data-stu-id="2bf77-263">This is done using the `Documents.Search` method.</span></span> <span data-ttu-id="2bf77-264">Per ogni query, è possibile passare il testo di ricerca da utilizzare come stringa (o `"*"` se non è presente il testo di ricerca), oltre ai parametri di ricerca creati in precedenza.</span><span class="sxs-lookup"><span data-stu-id="2bf77-264">For each query, we pass the search text to use as a string (or `"*"` if there is no search text), plus the search parameters created earlier.</span></span> <span data-ttu-id="2bf77-265">Viene inoltre specificato `Hotel` come parametro di tipo per `Documents.Search`, che indica all'SDK di deserializzare i documenti nei risultati della ricerca in oggetti di tipo `Hotel`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-265">We also specify `Hotel` as the type parameter for `Documents.Search`, which tells the SDK to deserialize documents in the search results into objects of type `Hotel`.</span></span>

> [!NOTE]
> <span data-ttu-id="2bf77-266">È possibile trovare ulteriori informazioni sulla sintassi delle espressioni di query di ricerca [qui](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="2bf77-266">You can find more information about the search query expression syntax [here](https://docs.microsoft.com/rest/api/searchservice/Simple-query-syntax-in-Azure-Search).</span></span>
> 
> 

<span data-ttu-id="2bf77-267">Infine, dopo ogni query questo metodo scorre tutte le corrispondenze nei risultati della ricerca, stampando tutti i documenti nella console:</span><span class="sxs-lookup"><span data-stu-id="2bf77-267">Finally, after each query this method iterates through all the matches in the search results, printing each document to the console:</span></span>

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

<span data-ttu-id="2bf77-268">Queste query saranno ora esaminate in maggiore dettaglio.</span><span class="sxs-lookup"><span data-stu-id="2bf77-268">Let's take a closer look at each of the queries in turn.</span></span> <span data-ttu-id="2bf77-269">Ecco il codice per eseguire la prima query:</span><span class="sxs-lookup"><span data-stu-id="2bf77-269">Here is the code to execute the first query:</span></span>

```csharp
parameters =
    new SearchParameters()
    {
        Select = new[] { "hotelName" }
    };

results = indexClient.Documents.Search<Hotel>("budget", parameters);

WriteDocuments(results);
```

<span data-ttu-id="2bf77-270">In questo caso, viene eseguita la ricerca degli hotel che corrispondono alla parola "budget". Verranno visualizzati solo i nomi degli hotel, come specificato dal parametro `Select`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-270">In this case, we're searching for hotels that match the word "budget", and we want to get back only the hotel names, as specified by the `Select` parameter.</span></span> <span data-ttu-id="2bf77-271">Ecco i risultati:</span><span class="sxs-lookup"><span data-stu-id="2bf77-271">Here are the results:</span></span>

    Name: Roach Motel

<span data-ttu-id="2bf77-272">Poi, si desidera trovare gli hotel con una tariffa notturna inferiore a 150 dollari e visualizzare solo l'ID dell'hotel e la descrizione:</span><span class="sxs-lookup"><span data-stu-id="2bf77-272">Next, we want to find the hotels with a nightly rate of less than $150, and return only the hotel ID and description:</span></span>

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

<span data-ttu-id="2bf77-273">Questa query utilizza un'espressione `$filter` OData, `baseRate lt 150`, per filtrare i documenti nell'indice.</span><span class="sxs-lookup"><span data-stu-id="2bf77-273">This query uses an OData `$filter` expression, `baseRate lt 150`, to filter the documents in the index.</span></span> <span data-ttu-id="2bf77-274">È possibile trovare informazioni sulla sintassi OData supportata da Ricerca di Azure [qui](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span><span class="sxs-lookup"><span data-stu-id="2bf77-274">You can find out more about the OData syntax that Azure Search supports [here](https://docs.microsoft.com/rest/api/searchservice/OData-Expression-Syntax-for-Azure-Search).</span></span>

<span data-ttu-id="2bf77-275">Di seguito sono riportati i risultati della query:</span><span class="sxs-lookup"><span data-stu-id="2bf77-275">Here are the results of the query:</span></span>

    ID: 2   Description: Cheapest hotel in town
    ID: 3   Description: Close to town hall and the river

<span data-ttu-id="2bf77-276">Ora, si desidera individuare i due hotel ristrutturati più di recente e visualizzare il nome dell'hotel e la data dell'ultima ristrutturazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-276">Next, we want to find the top two hotels that have been most recently renovated, and show the hotel name and last renovation date.</span></span> <span data-ttu-id="2bf77-277">Il codice è il seguente:</span><span class="sxs-lookup"><span data-stu-id="2bf77-277">Here is the code:</span></span> 

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

<span data-ttu-id="2bf77-278">In questo caso, viene nuovamente utilizzata la sintassi di OData per specificare il parametro `OrderBy` come `lastRenovationDate desc`.</span><span class="sxs-lookup"><span data-stu-id="2bf77-278">In this case, we again use OData syntax to specify the `OrderBy` parameter as `lastRenovationDate desc`.</span></span> <span data-ttu-id="2bf77-279">È inoltre possibile impostare `Top` su 2 per avere la certezza che la ricerca restituisca solo i 2 documenti principali.</span><span class="sxs-lookup"><span data-stu-id="2bf77-279">We also set `Top` to 2 to ensure we only get the top two documents.</span></span> <span data-ttu-id="2bf77-280">Come in precedenza, viene impostato `Select` per specificare quali campi devono essere visualizzati.</span><span class="sxs-lookup"><span data-stu-id="2bf77-280">As before, we set `Select` to specify which fields should be returned.</span></span>

<span data-ttu-id="2bf77-281">Ecco i risultati:</span><span class="sxs-lookup"><span data-stu-id="2bf77-281">Here are the results:</span></span>

    Name: Fancy Stay        Last renovated on: 6/27/2010 12:00:00 AM +00:00
    Name: Roach Motel       Last renovated on: 4/28/1982 12:00:00 AM +00:00

<span data-ttu-id="2bf77-282">Si desidera infine trovare tutti gli hotel che corrispondono alla parola "motel":</span><span class="sxs-lookup"><span data-stu-id="2bf77-282">Finally, we want to find all hotels that match the word "motel":</span></span>

```csharp
parameters = new SearchParameters();
results = indexClient.Documents.Search<Hotel>("motel", parameters);

WriteDocuments(results);
```

<span data-ttu-id="2bf77-283">Di seguito sono riportati i risultati, che includono tutti i campi, poiché non è stata specificata la proprietà `Select`:</span><span class="sxs-lookup"><span data-stu-id="2bf77-283">And here are the results, which include all fields since we did not specify the `Select` property:</span></span>

    ID: 2   Base rate: 79.99        Description: Cheapest hotel in town     Description (French): Hôtel le moins cher en ville      Name: Roach Motel       Category: Budget        Tags: [motel, budget]   Parking included: yes   Smoking allowed: yes    Last renovated on: 4/28/1982 12:00:00 AM +00:00 Rating: 1/5     Location: Latitude 49.678581, longitude -122.131577

<span data-ttu-id="2bf77-284">Questo passaggio completa l'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="2bf77-284">This step completes the tutorial, but don't stop here.</span></span> <span data-ttu-id="2bf77-285">**Passaggi successivi** vengono fornite risorse aggiuntive per ottenere ulteriori informazioni su Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="2bf77-285">**Next steps** provides additional resources for learning more about Azure Search.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2bf77-286">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2bf77-286">Next steps</span></span>
* <span data-ttu-id="2bf77-287">Vedere le guide di riferimento di [SDK di .NET](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) e [API REST](https://docs.microsoft.com/rest/api/searchservice/).</span><span class="sxs-lookup"><span data-stu-id="2bf77-287">Browse the references for the [.NET SDK](https://docs.microsoft.com/dotnet/api/microsoft.azure.search) and [REST API](https://docs.microsoft.com/rest/api/searchservice/).</span></span>
* <span data-ttu-id="2bf77-288">Approfondire l'argomento tramite [video e altri esempi ed esercitazioni](search-video-demo-tutorial-list.md).</span><span class="sxs-lookup"><span data-stu-id="2bf77-288">Deepen your knowledge through [videos and other samples and tutorials](search-video-demo-tutorial-list.md).</span></span>
* <span data-ttu-id="2bf77-289">Rivedere le [convenzioni di denominazione](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) per informazioni sulle regole per la denominazione dei vari oggetti.</span><span class="sxs-lookup"><span data-stu-id="2bf77-289">Review [naming conventions](https://docs.microsoft.com/rest/api/searchservice/Naming-rules) to learn the rules for naming various objects.</span></span>
* <span data-ttu-id="2bf77-290">Rivedere i [tipi di dati supportati](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Ricerca di Azure.</span><span class="sxs-lookup"><span data-stu-id="2bf77-290">Review [supported data types](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types) in Azure Search.</span></span>
