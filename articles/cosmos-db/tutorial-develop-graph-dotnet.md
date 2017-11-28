---
title: "Cosmos Azure DB: Attività di sviluppo hello API Graph in .NET | Documenti Microsoft"
description: Informazioni su come toodevelop con l'API DocumentDB Azure Cosmos DB usando .NET
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
ms.openlocfilehash: 12e435d8169aeee6e818dac4a3b66c7a0ec5f2d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-graph-api-in-net"></a><span data-ttu-id="aed89-103">Cosmos Azure DB: Attività di sviluppo hello API Graph in .NET</span><span class="sxs-lookup"><span data-stu-id="aed89-103">Azure Cosmos DB: Develop with hello Graph API in .NET</span></span>
<span data-ttu-id="aed89-104">Azure Cosmos DB è il servizio di database di Microsoft multimodello distribuito a livello globale.</span><span class="sxs-lookup"><span data-stu-id="aed89-104">Azure Cosmos DB is Microsoft's globally distributed multi-model database service.</span></span> <span data-ttu-id="aed89-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="aed89-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="aed89-106">Questa esercitazione viene illustrato come toocreate un account Azure Cosmos DB usando hello portale di Azure e come toocreate un database di grafico e un contenitore.</span><span class="sxs-lookup"><span data-stu-id="aed89-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal and how toocreate a graph database and container.</span></span> <span data-ttu-id="aed89-107">quindi, l'applicazione Hello crea un social network semplice con quattro utenti che utilizzano hello [API Graph](graph-sdk-dotnet.md) (anteprima), quindi consente di scorrere e grafico hello Gremlin utilizzando una query.</span><span class="sxs-lookup"><span data-stu-id="aed89-107">hello application then creates a simple social network with four people using hello [Graph API](graph-sdk-dotnet.md) (preview), then traverses and queries hello graph using Gremlin.</span></span>

<span data-ttu-id="aed89-108">Questa esercitazione sono trattati hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="aed89-108">This tutorial covers hello following tasks:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aed89-109">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="aed89-109">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="aed89-110">Creare un contenitore e un database di grafi</span><span class="sxs-lookup"><span data-stu-id="aed89-110">Create a graph database and container</span></span>
> * <span data-ttu-id="aed89-111">Serializzare oggetti too.NET vertici e bordi</span><span class="sxs-lookup"><span data-stu-id="aed89-111">Serialize vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="aed89-112">Aggiungere vertici e archi</span><span class="sxs-lookup"><span data-stu-id="aed89-112">Add vertices and edges</span></span>
> * <span data-ttu-id="aed89-113">Grafico di query hello utilizzando Gremlin</span><span class="sxs-lookup"><span data-stu-id="aed89-113">Query hello graph using Gremlin</span></span>

## <a name="graphs-in-azure-cosmos-db"></a><span data-ttu-id="aed89-114">Grafi in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="aed89-114">Graphs in Azure Cosmos DB</span></span>
<span data-ttu-id="aed89-115">È possibile utilizzare Azure Cosmos DB toocreate, update e grafici delle query tramite hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) libreria.</span><span class="sxs-lookup"><span data-stu-id="aed89-115">You can use Azure Cosmos DB toocreate, update, and query graphs using hello [Microsoft.Azure.Graphs](graph-sdk-dotnet.md) library.</span></span> <span data-ttu-id="aed89-116">libreria Microsoft.Azure.Graph Hello fornisce un metodo di estensione singolo `CreateGremlinQuery<T>` sopra hello `DocumentClient` classe query Gremlin tooexecute.</span><span class="sxs-lookup"><span data-stu-id="aed89-116">hello Microsoft.Azure.Graph library provides a single extension method `CreateGremlinQuery<T>` on top of hello `DocumentClient` class tooexecute Gremlin queries.</span></span>

<span data-ttu-id="aed89-117">Il linguaggio di programmazione funzionale Gremlin supporta operazioni di scrittura (DML) e le operazioni di query e attraversamento.</span><span class="sxs-lookup"><span data-stu-id="aed89-117">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="aed89-118">Trattati alcuni esempi in questo articolo di tooget i primi passi Gremlin.</span><span class="sxs-lookup"><span data-stu-id="aed89-118">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="aed89-119">Vedere [Query di Gremlin](gremlin-support.md) per una procedura dettagliata delle funzionalità Gremlin disponibili in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aed89-119">See [Gremlin queries](gremlin-support.md) for a detailed walkthrough of Gremlin capabilities available in Azure Cosmos DB.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="aed89-120">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="aed89-120">Prerequisites</span></span>
<span data-ttu-id="aed89-121">Assicurarsi di avere hello segue:</span><span class="sxs-lookup"><span data-stu-id="aed89-121">Please make sure you have hello following:</span></span>

* <span data-ttu-id="aed89-122">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="aed89-122">An active Azure account.</span></span> <span data-ttu-id="aed89-123">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="aed89-123">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="aed89-124">In alternativa, è possibile utilizzare hello [emulatore di Azure DocumentDB](local-emulator.md) per questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="aed89-124">Alternatively, you can use hello [Azure DocumentDB Emulator](local-emulator.md) for this tutorial.</span></span>
* <span data-ttu-id="aed89-125">[Visual Studio](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="aed89-125">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-database-account"></a><span data-ttu-id="aed89-126">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="aed89-126">Create database account</span></span>

<span data-ttu-id="aed89-127">Iniziamo mediante la creazione di un account Azure Cosmos DB in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="aed89-127">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="aed89-128">È stato già creato un account Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="aed89-128">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="aed89-129">In caso affermativo, andare troppo[configurazione della soluzione di Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="aed89-129">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="aed89-130">Si dispone di un account Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="aed89-130">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="aed89-131">Se in tal caso, l'account è un account Azure Cosmos DB ed è possibile andare troppo[configurazione della soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="aed89-131">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="aed89-132">Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="aed89-132">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
> 

[!INCLUDE [cosmos-db-create-dbaccount-graph](../../includes/cosmos-db-create-dbaccount-graph.md)]

## <span data-ttu-id="aed89-133"><a id="SetupVS"></a>Configurare la soluzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="aed89-133"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="aed89-134">Aprire **Visual Studio** nel computer.</span><span class="sxs-lookup"><span data-stu-id="aed89-134">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="aed89-135">In hello **File** dal menu **New**, quindi scegliere **progetto**.</span><span class="sxs-lookup"><span data-stu-id="aed89-135">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="aed89-136">In hello **nuovo progetto** finestra di dialogo Seleziona **modelli** / **Visual c#** / **applicazione Console (.NET Framework)**, denominare il progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="aed89-136">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
4. <span data-ttu-id="aed89-137">In hello **Esplora**, fare clic con il pulsante destro sulla nuova applicazione console, ovvero in una soluzione di Visual Studio, e quindi fare clic su **Gestisci pacchetti NuGet...**</span><span class="sxs-lookup"><span data-stu-id="aed89-137">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
5. <span data-ttu-id="aed89-138">In hello **NuGet** scheda, fare clic su **Sfoglia**e il tipo **Microsoft.Azure.Graphs** nella casella di ricerca hello e controllo hello **includono le versioni non definitive**.</span><span class="sxs-lookup"><span data-stu-id="aed89-138">In hello **NuGet** tab, click **Browse**, and type **Microsoft.Azure.Graphs** in hello search box, and check hello **Include prerelease versions**.</span></span>
6. <span data-ttu-id="aed89-139">All'interno dei risultati di hello, trovare **Microsoft.Azure.Graphs** e fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="aed89-139">Within hello results, find **Microsoft.Azure.Graphs** and click **Install**.</span></span>
   
   <span data-ttu-id="aed89-140">Se viene visualizzato un messaggio sull'esaminato soluzione toohello modifiche, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="aed89-140">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="aed89-141">Se viene visualizzato un messaggio sull'accettazione della licenza, fare clic su **Accetto**.</span><span class="sxs-lookup"><span data-stu-id="aed89-141">If you get a message about license acceptance, click **I accept**.</span></span>
   
    <span data-ttu-id="aed89-142">Hello `Microsoft.Azure.Graphs` libreria fornisce un metodo di estensione singolo `CreateGremlinQuery<T>` per l'esecuzione di operazioni Gremlin.</span><span class="sxs-lookup"><span data-stu-id="aed89-142">hello `Microsoft.Azure.Graphs` library provides a single extension method `CreateGremlinQuery<T>` for executing Gremlin operations.</span></span> <span data-ttu-id="aed89-143">Il linguaggio di programmazione funzionale Gremlin supporta operazioni di scrittura (DML) e le operazioni di query e attraversamento.</span><span class="sxs-lookup"><span data-stu-id="aed89-143">Gremlin is a functional programming language that supports write operations (DML) and query and traversal operations.</span></span> <span data-ttu-id="aed89-144">Trattati alcuni esempi in questo articolo di tooget i primi passi Gremlin.</span><span class="sxs-lookup"><span data-stu-id="aed89-144">We cover a few examples in this article tooget your started with Gremlin.</span></span> <span data-ttu-id="aed89-145">[Query Gremlin](gremlin-support.md) include una procedura dettagliata delle funzionalità di Gremlin in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="aed89-145">[Gremlin queries](gremlin-support.md) has a detailed walkthrough of Gremlin capabilities in Azure Cosmos DB.</span></span>

## <span data-ttu-id="aed89-146"><a id="add-references"></a>Connessione dell'app</span><span class="sxs-lookup"><span data-stu-id="aed89-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="aed89-147">Aggiungere queste due costanti e la variabile *client* nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aed89-147">Add these two constants and your *client* variable in your application.</span></span> 

```csharp
string endpoint = ConfigurationManager.AppSettings["Endpoint"]; 
string authKey = ConfigurationManager.AppSettings["AuthKey"]; 
``` 
<span data-ttu-id="aed89-148">Successivamente, head nuovamente toohello [portale di Azure](https://portal.azure.com) tooretrieve l'URL dell'endpoint e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="aed89-148">Next, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="aed89-149">URL dell'endpoint Hello e la chiave primaria sono necessari per l'applicazione toounderstand in tooconnect e per Azure Cosmos DB tootrust connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="aed89-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span> 

<span data-ttu-id="aed89-150">In hello portale di Azure passare tooyour Azure Cosmos DB account, fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**.</span><span class="sxs-lookup"><span data-stu-id="aed89-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span> 

<span data-ttu-id="aed89-151">Copiare hello URI dal portale di hello e incollarla su `Endpoint` nella proprietà endpoint hello precedente.</span><span class="sxs-lookup"><span data-stu-id="aed89-151">Copy hello URI from hello portal and paste it over `Endpoint` in hello endpoint property above.</span></span> <span data-ttu-id="aed89-152">Quindi copia hello chiave primaria dal portale hello e incollarlo in hello `AuthKey` proprietà precedente.</span><span class="sxs-lookup"><span data-stu-id="aed89-152">Then copy hello PRIMARY KEY from hello portal and paste it into hello `AuthKey` property above.</span></span> 

<span data-ttu-id="aed89-153">! [Cattura di schermata del portale di Azure hello utilizzato da toocreate esercitazione hello un'applicazione c#.</span><span class="sxs-lookup"><span data-stu-id="aed89-153">![Screen shot of hello Azure portal used by hello tutorial toocreate a C# application.</span></span> <span data-ttu-id="aed89-154">Mostra un hello account Azure Cosmos DB pulsante CHIAVI evidenziato nella hello Azure Cosmos DB spostamento e i valori URI e chiave primaria di hello evidenziati in hello pannello chiavi] [chiavi]</span><span class="sxs-lookup"><span data-stu-id="aed89-154">Shows an Azure Cosmos DB account hello KEYS button highlighted on hello Azure Cosmos DB navigation , and hello URI and PRIMARY KEY values highlighted on hello Keys blade][keys]</span></span> 
 
## <span data-ttu-id="aed89-155"><a id="instantiate"></a>Creare un'istanza di hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="aed89-155"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span> 
<span data-ttu-id="aed89-156">Successivamente, creare una nuova istanza di hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="aed89-156">Next, create a new instance of hello **DocumentClient**.</span></span>  

```csharp 
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey); 
``` 

## <span data-ttu-id="aed89-157"><a id="create-database"></a>Creare un database</span><span class="sxs-lookup"><span data-stu-id="aed89-157"><a id="create-database"></a>Create a database</span></span> 

<span data-ttu-id="aed89-158">A questo punto, creare un database di Azure Cosmos [database](documentdb-resources.md#databases) utilizzando hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metodo o [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metodo hello  **DocumentClient** classe da hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="aed89-158">Now, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span>  

```csharp 
Database database = await client.CreateDatabaseIfNotExistsAsync(new Database { Id = "graphdb" }); 
``` 
 
## <a name="create-a-graph"></a><span data-ttu-id="aed89-159">Creare un grafo</span><span class="sxs-lookup"><span data-stu-id="aed89-159">Create a graph</span></span> 

<span data-ttu-id="aed89-160">Successivamente, creare un contenitore grafico con hello utilizzando hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metodo o [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metodo hello **DocumentClient**  classe.</span><span class="sxs-lookup"><span data-stu-id="aed89-160">Next, create a graph container by using hello using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="aed89-161">Una raccolta è un contenitore di entità di grafi.</span><span class="sxs-lookup"><span data-stu-id="aed89-161">A collection is a container of graph entities.</span></span> 

```csharp 
DocumentCollection graph = await client.CreateDocumentCollectionIfNotExistsAsync( 
    UriFactory.CreateDatabaseUri("graphdb"), 
    new DocumentCollection { Id = "graphcollz" }, 
    new RequestOptions { OfferThroughput = 1000 }); 
``` 

## <span data-ttu-id="aed89-162"><a id="serializing"></a>Serializzare oggetti too.NET vertici e bordi</span><span class="sxs-lookup"><span data-stu-id="aed89-162"><a id="serializing"></a>Serialize vertices and edges too.NET objects</span></span>
<span data-ttu-id="aed89-163">Azure DB Cosmos utilizza hello [formato wire GraphSON](gremlin-support.md), che definisce uno schema JSON per vertici, bordi e le proprietà.</span><span class="sxs-lookup"><span data-stu-id="aed89-163">Azure Cosmos DB uses hello [GraphSON wire format](gremlin-support.md), which defines a JSON schema for vertices, edges, and properties.</span></span> <span data-ttu-id="aed89-164">In questo modo tooserialize/deserializzare GraphSON in oggetti .NET che è possibile utilizzare nel codice Hello Azure Cosmos DB .NET SDK include JSON.NET come dipendenza.</span><span class="sxs-lookup"><span data-stu-id="aed89-164">hello Azure Cosmos DB .NET SDK includes JSON.NET as a dependency, and this allows us tooserialize/deserialize GraphSON into .NET objects that we can work with in code.</span></span>

<span data-ttu-id="aed89-165">Ad esempio, è possibile usare una social network semplice con quattro utenti.</span><span class="sxs-lookup"><span data-stu-id="aed89-165">As an example, let's work with a simple social network with four people.</span></span> <span data-ttu-id="aed89-166">Viene illustrato come toocreate `Person` vertici, aggiungere `Knows` relazioni tra di essi, quindi eseguire una query e attraversare le relazioni di hello grafico toofind "friend di friend".</span><span class="sxs-lookup"><span data-stu-id="aed89-166">We look at how toocreate `Person` vertices, add `Knows` relationships between them, then query and traverse hello graph toofind "friend of friend" relationships.</span></span> 

<span data-ttu-id="aed89-167">Hello `Microsoft.Azure.Graphs.Elements` spazio dei nomi fornisce `Vertex`, `Edge`, `Property` e `VertexProperty` classi per la deserializzazione di oggetti .NET definiti toowell di GraphSON le risposte.</span><span class="sxs-lookup"><span data-stu-id="aed89-167">hello `Microsoft.Azure.Graphs.Elements` namespace provides `Vertex`, `Edge`, `Property` and `VertexProperty` classes for deserializing GraphSON responses toowell-defined .NET objects.</span></span>

## <a name="run-gremlin-using-creategremlinquery"></a><span data-ttu-id="aed89-168">Eseguire Gremlin usando CreateGremlinQuery</span><span class="sxs-lookup"><span data-stu-id="aed89-168">Run Gremlin using CreateGremlinQuery</span></span>
<span data-ttu-id="aed89-169">Gremlin, come SQL, supporta le operazioni di lettura, scrittura e le query.</span><span class="sxs-lookup"><span data-stu-id="aed89-169">Gremlin, like SQL, supports read, write, and query operations.</span></span> <span data-ttu-id="aed89-170">Ad esempio, hello frammento di codice seguente mostra come toocreate vertici, bordi, eseguono alcune query di esempio utilizzando `CreateGremlinQuery<T>`e scorrere in modo asincrono da questi risultati tramite `ExecuteNextAsync` e ' HasMoreResults.</span><span class="sxs-lookup"><span data-stu-id="aed89-170">For example, hello following snippet shows how toocreate vertices, edges, perform some sample queries using `CreateGremlinQuery<T>`, and asynchronously iterate through these results using `ExecuteNextAsync` and \`HasMoreResults.</span></span>

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

    // hello CreateGremlinQuery method extensions allow you tooexecute Gremlin queries and iterate
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

## <a name="add-vertices-and-edges"></a><span data-ttu-id="aed89-171">Aggiungere vertici e archi</span><span class="sxs-lookup"><span data-stu-id="aed89-171">Add vertices and edges</span></span>

<span data-ttu-id="aed89-172">Esaminare le istruzioni Gremlin hello mostrate nella precedente sezione hello maggiori dettagli.</span><span class="sxs-lookup"><span data-stu-id="aed89-172">Let's look at hello Gremlin statements shown in hello preceding section more detail.</span></span> <span data-ttu-id="aed89-173">Prima si aggiungono vertici usando il metodo `addV` Gremlin.</span><span class="sxs-lookup"><span data-stu-id="aed89-173">First we some vertices using Gremlin's `addV` method.</span></span> <span data-ttu-id="aed89-174">Ad esempio, hello frammento di codice seguente crea un vertice "Thomas Andersen" di tipo "Person", con le proprietà per nome, cognome ed età.</span><span class="sxs-lookup"><span data-stu-id="aed89-174">For example, hello following snippet creates a "Thomas Andersen" vertex of type "Person", with properties for first name, last name, and age.</span></span>

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

<span data-ttu-id="aed89-175">Creare quindi alcuni archi tra i vertici usando il metodo `addE` Gremlin.</span><span class="sxs-lookup"><span data-stu-id="aed89-175">Then we create some edges between these vertices using Gremlin's `addE` method.</span></span> 

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

<span data-ttu-id="aed89-176">È possibile aggiornare un vertice esistente usando il comando `properties` Gremlin.</span><span class="sxs-lookup"><span data-stu-id="aed89-176">We can update an existing vertex by using `properties` step in Gremlin.</span></span> <span data-ttu-id="aed89-177">Vengono ignorate query hello di hello chiamata tooexecute tramite `HasMoreResults` e `ExecuteNextAsync` per rest hello degli esempi di hello.</span><span class="sxs-lookup"><span data-stu-id="aed89-177">We skip hello call tooexecute hello query via `HasMoreResults` and `ExecuteNextAsync` for hello rest of hello examples.</span></span>

```cs
// Update a vertex
client.CreateGremlinQuery<Vertex>(
    graphCollection, 
    "g.V('thomas').property('age', 45)");
```

<span data-ttu-id="aed89-178">È possibile trascinare gli archi e i vertici usando il comando `drop` Gremlin.</span><span class="sxs-lookup"><span data-stu-id="aed89-178">You can drop edges and vertices using Gremlin's `drop` step.</span></span> <span data-ttu-id="aed89-179">Di seguito è riportato un frammento che mostra come toodelete vertice e un bordo.</span><span class="sxs-lookup"><span data-stu-id="aed89-179">Here's a snippet that shows how toodelete a vertex and an edge.</span></span> <span data-ttu-id="aed89-180">Si noti che l'eliminazione di un vertice esegue un'eliminazione a catena di hello associati bordi.</span><span class="sxs-lookup"><span data-stu-id="aed89-180">Note that dropping a vertex performs a cascading delete of hello associated edges.</span></span>

```cs
// Drop an edge
client.CreateGremlinQuery(graphCollection, "g.E('thomasKnowsRobin').drop()");

// Drop a vertex
client.CreateGremlinQuery(graphCollection, "g.V('robin').drop()");
```

## <a name="query-hello-graph"></a><span data-ttu-id="aed89-181">Grafico di query hello</span><span class="sxs-lookup"><span data-stu-id="aed89-181">Query hello graph</span></span>

<span data-ttu-id="aed89-182">È possibile anche eseguire operazioni di query e attraversamento usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="aed89-182">You can perform queries and traversals also using Gremlin.</span></span> <span data-ttu-id="aed89-183">Ad esempio, hello frammento di codice seguente viene illustrato come toocount hello numero di vertici nel grafico hello:</span><span class="sxs-lookup"><span data-stu-id="aed89-183">For example, hello following snippet shows how toocount hello number of vertices in hello graph:</span></span>

```cs
// Run a query toocount vertices
IDocumentQuery<int> countQuery = client.CreateGremlinQuery<int>(graphCollection, "g.V().count()");
```
<span data-ttu-id="aed89-184">È possibile eseguire filtri utilizzando Gremlin `has` e `hasLabel` i passaggi e combinarli con `and`, `or`, e `not` toobuild più complessa di filtri:</span><span class="sxs-lookup"><span data-stu-id="aed89-184">You can perform filters using Gremlin's `has` and `hasLabel` steps, and combine them using `and`, `or`, and `not` toobuild more complex filters:</span></span>

```cs
// Run a query with filter
IDocumentQuery<Vertex> personsByAge = client.CreateGremlinQuery<Vertex>(
  graphCollection, 
  "g.V().hasLabel('person').has('age', gt(40))");
```

<span data-ttu-id="aed89-185">È possibile proiettare determinate proprietà nei risultati della query hello utilizzando hello `values` passaggio:</span><span class="sxs-lookup"><span data-stu-id="aed89-185">You can project certain properties in hello query results using hello `values` step:</span></span>

```cs
// Run a query with projection
IDocumentQuery<string> firstNames = client.CreateGremlinQuery<string>(
  graphCollection, 
  $"g.V().hasLabel('person').values('firstName')");
```

<span data-ttu-id="aed89-186">Finora sono stati esaminati solo gli operatori di query che è possibile usare in qualsiasi database.</span><span class="sxs-lookup"><span data-stu-id="aed89-186">So far, we've only seen query operators that work in any database.</span></span> <span data-ttu-id="aed89-187">Grafici sono veloci ed efficienti per le operazioni di attraversamento quando è necessario toonavigate toorelated bordi e i vertici.</span><span class="sxs-lookup"><span data-stu-id="aed89-187">Graphs are fast and efficient for traversal operations when you need toonavigate toorelated edges and vertices.</span></span> <span data-ttu-id="aed89-188">Verranno ora individuati tutti gli amici di Thomas.</span><span class="sxs-lookup"><span data-stu-id="aed89-188">Let's find all friends of Thomas.</span></span> <span data-ttu-id="aed89-189">Facciamo utilizzando del Gremlin `outE` passaggio toofind hello tutti i bordi in uscita da Thomas, quindi attraversamento toohello in vertici da tali usando del Gremlin `inV` passaggio:</span><span class="sxs-lookup"><span data-stu-id="aed89-189">We do this by using Gremlin's `outE` step toofind all hello out-edges from Thomas, then traversing toohello in-vertices from those edges using Gremlin's `inV` step:</span></span>

```cs
// Run a traversal (find friends of Thomas)
IDocumentQuery<Vertex> friendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="aed89-190">la query successiva Hello esegue due hop toofind tutti "agli amici di Thomas di amici", chiamando `outE` e `inV` due volte.</span><span class="sxs-lookup"><span data-stu-id="aed89-190">hello next query performs two hops toofind all of Thomas' "friends of friends", by calling `outE` and `inV` two times.</span></span> 

```cs
// Run a traversal (find friends of friends of Thomas)
IDocumentQuery<Vertex> friendsOfFriendsOfThomas = client.CreateGremlinQuery<Vertex>(
  graphCollection,
  "g.V('thomas').outE('knows').inV().hasLabel('person').outE('knows').inV().hasLabel('person')");
```

<span data-ttu-id="aed89-191">È possibile compilare query più complesse e implementare la logica di attraversamento potente grafico utilizzando Gremlin, tra cui filtro combinazione espressioni, esecuzione di ciclo tramite hello `loop` passaggio e la navigazione condizionale implementazione utilizzando hello `choose` passaggio.</span><span class="sxs-lookup"><span data-stu-id="aed89-191">You can build more complex queries and implement powerful graph traversal logic using Gremlin, including mixing filter expressions, performing looping using hello `loop` step, and implementing conditional navigation using hello `choose` step.</span></span> <span data-ttu-id="aed89-192">Altre informazioni sulle operazioni che è possibile eseguire con il [supporto per Gremlin](gremlin-support.md).</span><span class="sxs-lookup"><span data-stu-id="aed89-192">Learn more about what you can do with [Gremlin support](gremlin-support.md)!</span></span>

<span data-ttu-id="aed89-193">L'esercitazione di Azure Cosmos DB è stata completata.</span><span class="sxs-lookup"><span data-stu-id="aed89-193">That's it, this Azure Cosmos DB tutorial is complete!</span></span> 

## <a name="clean-up-resources"></a><span data-ttu-id="aed89-194">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="aed89-194">Clean up resources</span></span>

<span data-ttu-id="aed89-195">Se non si ha intenzione toocontinue toouse questa app, utilizzare hello seguendo i passaggi toodelete tutte le risorse create da questa esercitazione in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="aed89-195">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>  

1. <span data-ttu-id="aed89-196">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="aed89-196">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span> 
2. <span data-ttu-id="aed89-197">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="aed89-197">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aed89-198">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="aed89-198">Next Steps</span></span>

<span data-ttu-id="aed89-199">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="aed89-199">In this tutorial, you've done hello following:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="aed89-200">Creazione di un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="aed89-200">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="aed89-201">Creazione di un contenitore e un database di grafi</span><span class="sxs-lookup"><span data-stu-id="aed89-201">Created a graph database and container</span></span>
> * <span data-ttu-id="aed89-202">Oggetti too.NET vertici e bordi serializzati</span><span class="sxs-lookup"><span data-stu-id="aed89-202">Serialized vertices and edges too.NET objects</span></span>
> * <span data-ttu-id="aed89-203">Aggiunta di vertici e archi</span><span class="sxs-lookup"><span data-stu-id="aed89-203">Added vertices and edges</span></span>
> * <span data-ttu-id="aed89-204">Grafico di query hello mediante Gremlin</span><span class="sxs-lookup"><span data-stu-id="aed89-204">Queried hello graph using Gremlin</span></span>

<span data-ttu-id="aed89-205">È ora possibile creare query più complesse e implementare la potente logica di attraversamento dei grafi usando Gremlin.</span><span class="sxs-lookup"><span data-stu-id="aed89-205">You can now build more complex queries and implement powerful graph traversal logic using Gremlin.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="aed89-206">Eseguire query con Gremlin</span><span class="sxs-lookup"><span data-stu-id="aed89-206">Query using Gremlin</span></span>](tutorial-query-graph.md)
