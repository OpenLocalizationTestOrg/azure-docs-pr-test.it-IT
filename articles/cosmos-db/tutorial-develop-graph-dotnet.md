---
title: 'Azure Cosmos DB: Sviluppare con l''API Graph in .NET | Documentazione Microsoft'
description: Informazioni su come sviluppare con l'API di DocumentDB di Azure Cosmos DB usando .NET
services: cosmos-db
documentationcenter: 
author: dennyglee
manager: jhubbard
editor: 
ms.assetid: cc8df0be-672b-493e-95a4-26dd52632261
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: denlee
ms.custom: mvc
ms.openlocfilehash: eeaa0c4f84a408815371742334d2ba7ce600b72f
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmos-db-develop-with-the-graph-api-in-net"></a><span data-ttu-id="eb887-103">Azure Cosmos DB: Sviluppare con l'API Graph in .NET</span><span class="sxs-lookup"><span data-stu-id="eb887-103">Azure Cosmos DB: Develop with the Graph API in .NET</span></span>
<span data-ttu-id="eb887-104">Azure Cosmos DB è il servizio di database di Microsoft multimodello distribuito a livello globale.</span><span class="sxs-lookup"><span data-stu-id="eb887-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="eb887-105">È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave-valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eb887-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="eb887-106">Questa esercitazione illustra come creare un account Azure Cosmos DB usando il portale di Azure e come creare un contenitore e un database di grafi.</span><span class="sxs-lookup"><span data-stu-id="eb887-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal and how to create a graph database and container.</span></span> <span data-ttu-id="eb887-107">L'applicazione crea quindi una social network semplice con quattro utenti usando l'[API Graph](graph-sdk-dotnet.md) (anteprima), quindi attraversa ed esegue query sul grafo usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eb887-107">The application then creates a simple social network with four people using the [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries the graph using Gremlin.</span></span>

<span data-ttu-id="eb887-108">Questa esercitazione illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb887-108">This tutorial covers the following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb887-109">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eb887-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="eb887-110">Creare un contenitore e un database di grafi</span><span class="sxs-lookup"><span data-stu-id="eb887-110">Create a graph database and container</span></span>
> * <span data-ttu-id="eb887-111">Serializzare vertici e archi negli oggetti .NET</span><span class="sxs-lookup"><span data-stu-id="eb887-111">Serialize vertices and edges to .NET objects</span></span>
> * <span data-ttu-id="eb887-112">Aggiungere vertici e archi</span><span class="sxs-lookup"><span data-stu-id="eb887-112">Add vertices and edges</span></span>
> * <span data-ttu-id="eb887-113">Eseguire query sul grafo usando Gremlin</span><span class="sxs-lookup"><span data-stu-id="eb887-113">Query the graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="eb887-114">Grafi in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eb887-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="eb887-115">È possibile usare Azure Cosmos DB per creare, aggiornare ed eseguire query di grafi usando la libreria [Microsoft.Azure.Graphs](graph-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="eb887-115">You can use Azure Cosmos DB to create, update, and query graphs using the [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="eb887-116">La libreria Microsoft.Azure.Graph offre un metodo di estensione singolo `CreateGremlinQuery<T>` oltre alla classe `DocumentClient` per eseguire query Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eb887-116">The Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of the `DocumentClient` class to execute Gremlin queries.</span></span>

<span data-ttu-id="eb887-117">Il linguaggio di programmazione funzionale Gremlin supporta operazioni di scrittura (DML) e le operazioni di query e attraversamento.</span><span class="sxs-lookup"><span data-stu-id="eb887-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="eb887-118">Questo articolo descrive alcuni esempi per iniziare a usare Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eb887-118">We cover a few examples in this article to get your started with Gremlin.</span></span> <span data-ttu-id="eb887-119">Vedere [Query di Gremlin](gremlin-support.md) per una procedura dettagliata delle funzionalità Gremlin disponibili in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eb887-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="eb887-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="eb887-120">Prerequisites</span></span>
<span data-ttu-id="eb887-121">Assicurarsi di disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="eb887-121">Please make sure you have the following:</span></span>

* <span data-ttu-id="eb887-122">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="eb887-122">An active Azure account.</span></span> <span data-ttu-id="eb887-123">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="eb887-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="eb887-124">In alternativa, per questa esercitazione è possibile usare l'[emulatore DocumentDB di Azure](local-emulator.md).</span><span class="sxs-lookup"><span data-stu-id="eb887-124">Alternatively, you can use the [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="eb887-125">[Visual Studio](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="eb887-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="eb887-126">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="eb887-126">Create database account</span></span>

<span data-ttu-id="eb887-127">Si inizia creando un account Azure Cosmos DB nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb887-127">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="eb887-128">È stato già creato un account Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="eb887-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="eb887-129">In questo caso passare a [Configurare la soluzione di Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="eb887-129">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="eb887-130">Si dispone di un account Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="eb887-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="eb887-131">In questo caso l'account è ora un account Azure Cosmos DB ed è possibile passare a [Configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="eb887-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="eb887-132">Se si usa l'emulatore Azure Cosmos DB, seguire i passaggi descritti nell'articolo [Azure Cosmos DB Emulator](local-emulator.md) (Emulatore Azure Cosmos DB) per configurare l'emulatore e proseguire con il passaggio [Configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="eb887-132">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="eb887-133"><a id="SetupVS"></a>Configurare la soluzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="eb887-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="eb887-134">Aprire **Visual Studio** nel computer.</span><span class="sxs-lookup"><span data-stu-id="eb887-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="eb887-135">Scegliere **Nuovo** dal menu **File** e quindi selezionare **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="eb887-135">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="eb887-136">Nella finestra di dialogo **Nuovo progetto** selezionare **Modelli** / **Visual C#** / **App console (.NET Framework)**, assegnare un nome al progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb887-136">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="eb887-137">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla nuova applicazione console, disponibile nella soluzione di Visual Studio, quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="eb887-137">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="eb887-138">Nella scheda **NuGet** fare clic su **Sfoglia**e digitare **Microsoft.Azure.Graphs** nella casella di ricerca e selezionare **Includi versione preliminare**.</span><span class="sxs-lookup"><span data-stu-id="eb887-138">In the **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in the search box, and check the **Include prerelease versions**.</span></span>
6. <span data-ttu-id="eb887-139">Nei risultati trovare **Microsoft.Azure.Graphs** e fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="eb887-139">Within the results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="eb887-140">Se viene visualizzato un messaggio sulla verifica delle modifiche alla soluzione, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="eb887-140">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="eb887-141">Se viene visualizzato un messaggio sull'accettazione della licenza, fare clic su **Accetto**.</span><span class="sxs-lookup"><span data-stu-id="eb887-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="eb887-142">La libreria`Microsoft.Azure.Graphs` fornisce un metodo di estensione singolo `CreateGremlinQuery<T>` per l'esecuzione di operazioni Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eb887-142">The `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="eb887-143">Il linguaggio di programmazione funzionale Gremlin supporta operazioni di scrittura (DML) e le operazioni di query e attraversamento.</span><span class="sxs-lookup"><span data-stu-id="eb887-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="eb887-144">Questo articolo descrive alcuni esempi per iniziare a usare Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eb887-144">We cover a few examples in this article to get your started with Gremlin.</span></span> <span data-ttu-id="eb887-145">[Query Gremlin](gremlin-support.md) include una procedura dettagliata delle funzionalità di Gremlin in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="eb887-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="eb887-146"><a id="add-references"></a>Connessione dell'app</span><span class="sxs-lookup"><span data-stu-id="eb887-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="eb887-147">Aggiungere queste due costanti e la variabile *client* nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb887-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="eb887-148">Tornare al [portale di Azure](https://portal.azure.com) per recuperare la chiave primaria e l'URL dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="eb887-148">Next, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="eb887-149">L'URL e la chiave primaria dell'endpoint sono necessari all'applicazione per conoscere la destinazione della connessione e ad Azure Cosmos DB per considerare attendibile la connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="eb887-149">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span> 

<span data-ttu-id="eb887-150">Nel portale di Azure passare all'account Azure Cosmos DB, fare clic su **Chiavi**, quindi su **Chiavi di lettura/scrittura**.</span><span class="sxs-lookup"><span data-stu-id="eb887-150">In the Azure portal, navigate to your Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="eb887-151">Copiare l'URI dal portale e incollarlo su `Endpoint` nella proprietà dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="eb887-151">Copy the URI from the portal and paste it over `Endpoint` in the endpoint property above.</span></span> <span data-ttu-id="eb887-152">Copiare quindi la CHIAVE PRIMARIA dal portale e incollarla nella proprietà `AuthKey` precedente.</span><span class="sxs-lookup"><span data-stu-id="eb887-152">Then copy the PRIMARY KEY from the portal and paste it into the `AuthKey` property above.</span></span> 

<span data-ttu-id="eb887-153">![Screenshot del portale di Azure usato nell'esercitazione per creare un'applicazione C#.</span><span class="sxs-lookup"><span data-stu-id="eb887-153">![Screen shot of the Azure portal used by the tutorial to create a C# application.</span></span> <span data-ttu-id="eb887-154">Mostra un account Azure Cosmos DB, il pulsante CHIAVI evidenziato nel Pannello di navigazione Azure Cosmos DB e i valori URI e CHIAVE PRIMARIA evidenziati nel pannello chiavi] [keys]</span><span class="sxs-lookup"><span data-stu-id="eb887-154">Shows an Azure Cosmos DB account the KEYS button highlighted on the Azure Cosmos DB navigation , and the URI and PRIMARY KEY values highlighted on the Keys blade][keys]</span></span> 
 
## <span data-ttu-id="eb887-155"><a id="instantiate"></a>Creare un'istanza di DocumentClient</span><span class="sxs-lookup"><span data-stu-id="eb887-155"><a id="instantiate"></a>Instantiate the DocumentClient</span></span> 
<span data-ttu-id="eb887-156">Creare quindi una nuova istanza di **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="eb887-156">Next, create a new instance of the **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="eb887-157"><a id="create-database"></a>Creare un database</span><span class="sxs-lookup"><span data-stu-id="eb887-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="eb887-158">A questo punto creare un [database](documentdb-resources.md#databases) di Azure Cosmos DB usando il metodo [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) o [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) della classe **DocumentClient** da [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="eb887-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class from the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="eb887-159">Creare un grafo</span><span class="sxs-lookup"><span data-stu-id="eb887-159">Create a graph</span></span> 

<span data-ttu-id="eb887-160">Creare quindi un contenitore di grafi usando il metodo [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) o [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="eb887-160">Next, create a graph container by using the using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="eb887-161">Una raccolta è un contenitore di entità di grafi.</span><span class="sxs-lookup"><span data-stu-id="eb887-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="eb887-162"><a id="serializing"></a>Serializzare vertici e archi negli oggetti .NET</span><span class="sxs-lookup"><span data-stu-id="eb887-162"><a id="serializing"></a>Serialize vertices and edges to .NET objects</span></span>
<span data-ttu-id="eb887-163">Azure Cosmos DB usa il [formato wire GraphSON](gremlin-support.md), che definisce uno schema JSON per vertici, archi e proprietà.</span><span class="sxs-lookup"><span data-stu-id="eb887-163">Azure Cosmos DB uses the [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="eb887-164">Azure Cosmos DB .NET SDK include JSON.NET come dipendenza e ciò consente di serializzare o deserializzare GraphSON negli oggetti .NET che è possibile usare nel codice.</span><span class="sxs-lookup"><span data-stu-id="eb887-164">The Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us to serialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="eb887-165">Ad esempio, è possibile usare una social network semplice con quattro utenti.</span><span class="sxs-lookup"><span data-stu-id="eb887-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="eb887-166">Verrà illustrato come creare vertici `Person`, aggiungere relazioni `Knows` tra i vertici, quindi eseguire query e attraversare il grafo per individuare le relazioni "amico di amico".</span><span class="sxs-lookup"><span data-stu-id="eb887-166">We look at how to create `Person` vertices, add `Knows` relationships between them, then query and traverse the graph to find "friend of friend" relationships.</span></span> 

<span data-ttu-id="eb887-167">Lo spazio dei nomi `Microsoft.Azure.Graphs.Elements` fornisce le classi `Vertex`, `Edge`, `Property` e `VertexProperty` per la deserializzazione delle risposte GraphSON a oggetti .NET ben definiti.</span><span class="sxs-lookup"><span data-stu-id="eb887-167">The `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses to well-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="eb887-168">Eseguire Gremlin usando CreateGremlinQuery</span><span class="sxs-lookup"><span data-stu-id="eb887-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="eb887-169">Gremlin, come SQL, supporta le operazioni di lettura, scrittura e le query.</span><span class="sxs-lookup"><span data-stu-id="eb887-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="eb887-170">Ad esempio, il frammento seguente illustra come creare vertici e archi, eseguire alcune query di esempio usando `CreateGremlinQuery<T>` e iterare in modo asincrono questi risultati usando `ExecuteNextAsync` e 'HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="eb887-170">For example, the following snippet shows how to create vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

```cs
Dictionary<string, string> gremlinQueries = new Dictionary<string, string>
{
    { "Cleanup",        "g.V().drop()" },
    { "AddVertex 1",    "g.addV('person').property('id', 'thomas').property('firstName', 'Thomas').property('age', 44)" },
    { "AddVertex 2",    "g.addV('person').property('id', 'mary').property('firstName', 'Mary').property('lastName', 'Andersen').property('age', 39)" },
    { "AddVertex 3",    "g.addV('person').property('id', 'ben').property('firstName', 'Ben').property('lastName', 'Miller')" },
    { "AddVertex 4",    "g.addV('person').property('id', 'robin').property('firstName', 'Robin').property('lastName', 'Wakefield')" },
    { "AddEdge 1",      "g.V('thomas').addE('knows').to(g.V('mary'))" },
    { "AddEdge 2",      "g.V('thomas').addE('knows').to(g.V('ben'))" },
    { "AddEdge 3",      "g.V('ben').addE('knows').to(g.V('robin'))" },
    { "UpdateVertex",   "g.V('thomas').property('age', 44)" },
    { "CountVertices",  "g.V().count()" },
    { "Filter Range",   "g.V().hasLabel('person').has('age', gt(40))" },
    { "Project",        "g.V().hasLabel('person').values('firstName')" },
    { "Sort",           "g.V().hasLabel('person').order().by('firstName', decr)" },
    { "Traverse",       "g.V('thomas').outE('knows').inV().hasLabel('person')" },
    { "Traverse 2x",    "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')" },
    { "Loop",           "g.V('thomas').repeat(out()).until(has('id', 'robin')).path()" },
    { "DropEdge",       "g.V('thomas').outE('knows').where(inV().has('id', 'mary')).drop()" },
    { "CountEdges",     "g.E().count()" },
    { "DropVertex",     "g.V('thomas').drop()" },
};

foreach (KeyValuePair<string, string> gremlinQuery in gremlinQueries)
{
    Console.WriteLine($"Running {gremlinQuery.Key}: {gremlinQuery.Value}");

    // The CreateGremlinQuery method extensions allow you to execute Gremlin queries and iterate
    // results asychronously
    IDocumentQuery<dynamic> query = client.CreateGremlinQuery<dynamic>(graph, gremlinQuery.Value);
    while (query.HasMoreResults)
    {
        foreach (dynamic result in await query.ExecuteNextAsync())
        {
            Console.WriteLine($"\t {JsonConvert.SerializeObject(result)}");
        }
    }

    Console.WriteLine();
}
```

## <a name="add-vertices-and-edges"></a><span data-ttu-id="eb887-171">Aggiungere vertici e archi</span><span class="sxs-lookup"><span data-stu-id="eb887-171">Add vertices and edges</span></span>

<span data-ttu-id="eb887-172">Verranno esaminati in maggiore dettaglio i comandi Gremlin illustrati nella sezione precedente.</span><span class="sxs-lookup"><span data-stu-id="eb887-172">Let's look at the Gremlin statements shown in the preceding section more detail.</span></span> <span data-ttu-id="eb887-173">Prima si aggiungono vertici usando il metodo `addV` Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eb887-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="eb887-174">Ad esempio, il frammento seguente crea un vertice "Thomas Andersen" di tipo "Person", con proprietà per il nome, il cognome e l'età.</span><span class="sxs-lookup"><span data-stu-id="eb887-174">For example, the following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

```cs
// Create a vertex
IDocumentQuery<Vertex> createVertexQuery = client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.addV('person').property('firstName', 'Thomas')");

while (createVertexQuery.HasMoreResults)
{
    Vertex thomas = (await create.ExecuteNextAsync<Vertex>()).First();
}
```

<span data-ttu-id="eb887-175">Creare quindi alcuni archi tra i vertici usando il metodo `addE` Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eb887-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

```cs
// Add a "knows" edge
IDocumentQuery<Edge> createEdgeQuery = client.CreateGremlinQuery<Edge>(
    graphCollection, 
    "g.V('thomas').addE('knows').to(g.V('mary'))");

while (create.HasMoreResults)
{
    Edge thomasKnowsMaryEdge = (await create.ExecuteNextAsync<Edge>()).First();
}
```

<span data-ttu-id="eb887-176">È possibile aggiornare un vertice esistente usando il comando `properties` Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eb887-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="eb887-177">Non verrà esaminata la chiamata per eseguire la query tramite `HasMoreResults` e `ExecuteNextAsync` negli altri esempi.</span><span class="sxs-lookup"><span data-stu-id="eb887-177">We skip the call to execute the query via `HasMoreResults` and `ExecuteNextAsync` for the rest of the examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="eb887-178">È possibile trascinare gli archi e i vertici usando il comando `drop` Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eb887-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="eb887-179">Ecco un frammento di codice che illustra come eliminare un vertice e un arco.</span><span class="sxs-lookup"><span data-stu-id="eb887-179">Here's a snippet that shows how to delete a vertex and an edge.</span></span> <span data-ttu-id="eb887-180">Si noti che l'eliminazione di un vertice implica l'eliminazione a catena degli archi associati.</span><span class="sxs-lookup"><span data-stu-id="eb887-180">Note that dropping a vertex performs a cascading delete of the associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-the-graph"></a><span data-ttu-id="eb887-181">Eseguire una query sul grafo</span><span class="sxs-lookup"><span data-stu-id="eb887-181">Query the graph</span></span>

<span data-ttu-id="eb887-182">È possibile anche eseguire operazioni di query e attraversamento usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eb887-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="eb887-183">Ad esempio, il frammento seguente illustra come contare il numero di vertici nel grafo:</span><span class="sxs-lookup"><span data-stu-id="eb887-183">For example, the following snippet shows how to count the number of vertices in the graph:</span></span>

```cs
// Run a query to count vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="eb887-184">È possibile eseguire filtri usando i comandi `has` e `hasLabel` Gremlin e combinarli usando `and`, `or` e `not` per creare filtri più complessi:</span><span class="sxs-lookup"><span data-stu-id="eb887-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` to build more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="eb887-185">È possibile proiettare determinate proprietà nei risultati della query usando il comando `values`:</span><span class="sxs-lookup"><span data-stu-id="eb887-185">You can project certain properties in the query results using the `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="eb887-186">Finora sono stati esaminati solo gli operatori di query che è possibile usare in qualsiasi database.</span><span class="sxs-lookup"><span data-stu-id="eb887-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="eb887-187">I grafi sono veloci ed efficienti per le operazioni di attraversamento quando è necessario passare agli archi e ai vertici correlati.</span><span class="sxs-lookup"><span data-stu-id="eb887-187">Graphs are fast and efficient for traversal operations when you need to navigate to related edges and vertices.</span></span> <span data-ttu-id="eb887-188">Verranno ora individuati tutti gli amici di Thomas.</span><span class="sxs-lookup"><span data-stu-id="eb887-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="eb887-189">Questa operazione viene eseguita usando il comando `outE` di Gremlin per individuare tutti gli archi in uscita da Thomas, quindi attraversando i vertici in ingresso da tali archi usando il comando `inV` di Gremlin:</span><span class="sxs-lookup"><span data-stu-id="eb887-189">We do this by using Gremlin's `outE` step to find all the out-edges from Thomas, then traversing to the in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="eb887-190">La query successiva esegue due passaggi per trovare tutti "gli amici di amici" di Thomas chiamando `outE` e `inV` due volte.</span><span class="sxs-lookup"><span data-stu-id="eb887-190">The next query performs two hops to find all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="eb887-191">È possibile creare query più complesse e implementare la potente logica di attraversamento di grafi usando Gremlin, incluse la combinazione di espressioni di filtro, l'esecuzione di cicli con il comando `loop` e l'implementazione dello spostamento condizionale usando il comando `choose`.</span><span class="sxs-lookup"><span data-stu-id="eb887-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using the `loop` step, and implementing conditional navigation using the `choose` step.</span></span> <span data-ttu-id="eb887-192">Altre informazioni sulle operazioni che è possibile eseguire con il [supporto per Gremlin](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="eb887-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="eb887-193">L'esercitazione di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="eb887-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="eb887-194">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="eb887-194">Clean up resources</span></span>

<span data-ttu-id="eb887-195">Se non si prevede di continuare a usare questa app, seguire questa procedura per eliminare tutte le risorse create da questa esercitazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="eb887-195">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>  

1. <span data-ttu-id="eb887-196">Scegliere **Gruppi di risorse** dal menu a sinistra del portale di Azure e quindi fare clic sul nome della risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="eb887-196">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span> 
2. <span data-ttu-id="eb887-197">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare il nome della risorsa da eliminare nella casella di testo e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="eb887-197">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb887-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="eb887-198">Next Steps</span></span>

<span data-ttu-id="eb887-199">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="eb887-199">In this tutorial, you've done the following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="eb887-200">Creazione di un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="eb887-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="eb887-201">Creazione di un contenitore e un database di grafi</span><span class="sxs-lookup"><span data-stu-id="eb887-201">Created a graph database and container</span></span>
> * <span data-ttu-id="eb887-202">Serializzazione di vertici e archi negli oggetti .NET</span><span class="sxs-lookup"><span data-stu-id="eb887-202">Serialized vertices and edges to .NET objects</span></span>
> * <span data-ttu-id="eb887-203">Aggiunta di vertici e archi</span><span class="sxs-lookup"><span data-stu-id="eb887-203">Added vertices and edges</span></span>
> * <span data-ttu-id="eb887-204">Esecuzione di query sul grafo usando Gremlin</span><span class="sxs-lookup"><span data-stu-id="eb887-204">Queried the graph using Gremlin</span></span>

<span data-ttu-id="eb887-205">È ora possibile creare query più complesse e implementare la potente logica di attraversamento di grafi usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="eb887-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="eb887-206">Eseguire query con Gremlin</span><span class="sxs-lookup"><span data-stu-id="eb887-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
