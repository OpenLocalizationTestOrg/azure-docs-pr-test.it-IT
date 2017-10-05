---
title: 'Azure Cosmos DB: sviluppare con l''API di DocumentDB in .NET | Documentazione Microsoft'
description: Informazioni su come sviluppare con l'API di DocumentDB di Azure Cosmos DB usando .NET
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
tags: 
ms.assetid: 
ms.service: cosmos-db
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: 
ms.date: 05/10/2017
ms.author: mimig
ms.custom: mvc
ms.openlocfilehash: 2eed74ae9bd173b0944ec190dfe5d9a4bdc54c37
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="azure-cosmosdb-develop-with-the-documentdb-api-in-net"></a><span data-ttu-id="cb7f7-103">Azure Cosmos DB: sviluppare con l'API di DocumentDB in .NET</span><span class="sxs-lookup"><span data-stu-id="cb7f7-103">Azure CosmosDB: Develop with the DocumentDB API in .NET</span></span>

<span data-ttu-id="cb7f7-104">Azure Cosmos DB è il servizio di database di Microsoft multimodello distribuito a livello globale.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="cb7f7-105">È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave-valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="cb7f7-106">Questa esercitazione illustra come creare un account Azure Cosmos DB usando il portale di Azure e come creare una raccolta e un database di documenti con una [chiave di partizione](documentdb-partition-data.md#partition-keys) usando l'[API .NET di DocumentDB ](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-106">This tutorial demonstrates how to create an Azure Cosmos DB account using the Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using the [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="cb7f7-107">Definendo una chiave di partizione quando si crea una raccolta, l'applicazione viene preparata ad una facile scalabilità in linea con la crescita dei dati.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-107">By defining a partition key when you create a collection, your application is prepared to scale effortlessly as your data grows.</span></span> 

<span data-ttu-id="cb7f7-108">Questa esercitazione illustra le attività seguenti usando l'[API .NET DocumentDB](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="cb7f7-108">This tutorial covers the following tasks by using the [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="cb7f7-109">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cb7f7-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="cb7f7-110">Creare una raccolta e un database con una chiave di partizione</span><span class="sxs-lookup"><span data-stu-id="cb7f7-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="cb7f7-111">Creare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="cb7f7-111">Create JSON documents</span></span>
> * <span data-ttu-id="cb7f7-112">Aggiornare un documento</span><span class="sxs-lookup"><span data-stu-id="cb7f7-112">Update a document</span></span>
> * <span data-ttu-id="cb7f7-113">Eseguire query su raccolte partizionate</span><span class="sxs-lookup"><span data-stu-id="cb7f7-113">Query partitioned collections</span></span>
> * <span data-ttu-id="cb7f7-114">Eseguire stored procedure</span><span class="sxs-lookup"><span data-stu-id="cb7f7-114">Run stored procedures</span></span>
> * <span data-ttu-id="cb7f7-115">Eliminare un documento</span><span class="sxs-lookup"><span data-stu-id="cb7f7-115">Delete a document</span></span>
> * <span data-ttu-id="cb7f7-116">Eliminare un database</span><span class="sxs-lookup"><span data-stu-id="cb7f7-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb7f7-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="cb7f7-117">Prerequisites</span></span>
<span data-ttu-id="cb7f7-118">Assicurarsi di disporre di quanto segue:</span><span class="sxs-lookup"><span data-stu-id="cb7f7-118">Please make sure you have the following:</span></span>

* <span data-ttu-id="cb7f7-119">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-119">An active Azure account.</span></span> <span data-ttu-id="cb7f7-120">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="cb7f7-121">In alternativa è possibile usare l'[emulatore Azure Cosmos DB](local-emulator.md) per questa esercitazione, se si intende usare un ambiente locale che emula il servizio Azure DocumentDB per lo sviluppo.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-121">Alternatively, you can use the [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like to use a local environment that emulates the Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="cb7f7-122">[Visual Studio](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="cb7f7-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="cb7f7-123">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cb7f7-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="cb7f7-124">Si inizia creando un account Azure Cosmos DB nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-124">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="cb7f7-125">È stato già creato un account Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="cb7f7-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="cb7f7-126">In questo caso passare a [Configurare la soluzione di Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="cb7f7-126">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="cb7f7-127">Si dispone di un account Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="cb7f7-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="cb7f7-128">In questo caso l'account è ora un account Azure Cosmos DB ed è possibile passare a [Configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="cb7f7-129">Se si usa l'emulatore Azure Cosmos DB, seguire i passaggi descritti nell'articolo [Azure Cosmos DB Emulator](local-emulator.md) (Emulatore Azure Cosmos DB) per configurare l'emulatore e proseguire con il passaggio [Configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-129">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="cb7f7-130"><a id="SetupVS"></a>Configurare la soluzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="cb7f7-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="cb7f7-131">Aprire **Visual Studio** nel computer.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="cb7f7-132">Scegliere **Nuovo** dal menu **File** e quindi selezionare **Progetto**.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-132">On the **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="cb7f7-133">Nella finestra di dialogo **Nuovo progetto** selezionare **Modelli** / **Visual C#** / **App console (.NET Framework)**, assegnare un nome al progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-133">In the **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="cb7f7-134">![Screenshot della finestra Nuovo progetto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="cb7f7-134">![Screen shot of the New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="cb7f7-135">In **Esplora soluzioni** fare clic con il pulsante destro del mouse sulla nuova applicazione console, disponibile nella soluzione di Visual Studio, quindi scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-135">In the **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Screenshot del menu selezionato con il pulsante destro del mouse per il progetto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="cb7f7-137">Nella scheda **NuGet** fare clic su **Sfoglia** e digitare **documentdb** nella casella di ricerca.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-137">In the **NuGet** tab, click **Browse**, and type **documentdb** in the search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="cb7f7-138">Nei risultati trovare **Microsoft.Azure.DocumentDB** e fare clic su **Installa**.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-138">Within the results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="cb7f7-139">L'ID pacchetto per la libreria client di Azure Cosmos DB è [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-139">The package ID for the Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="cb7f7-140">![Screenshot del menu di NuGet per l'individuazione dell'SDK client di Cosmos DB](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="cb7f7-140">![Screen shot of the NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="cb7f7-141">Se viene visualizzato un messaggio sulla verifica delle modifiche alla soluzione, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-141">If you get a message about reviewing changes to the solution, click **OK**.</span></span> <span data-ttu-id="cb7f7-142">Se viene visualizzato un messaggio sull'accettazione della licenza, fare clic su **Accetto**.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="cb7f7-143"><a id="Connect"></a>Aggiungere riferimenti al progetto</span><span class="sxs-lookup"><span data-stu-id="cb7f7-143"><a id="Connect"></a>Add references to your project</span></span>
<span data-ttu-id="cb7f7-144">I passaggi rimanenti di questa esercitazione specificano i frammenti di codice dell'API di DocumentDB necessari per creare e aggiornare le risorse di Azure Cosmos DB nel progetto.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-144">The remaining steps in this tutorial provide the DocumentDB API code snippets required to create and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="cb7f7-145">Aggiungere questi riferimenti all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-145">First, add these references to your application.</span></span>
<!---These aren't added by default when you install the pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="cb7f7-146"><a id="add-references"></a>Connessione dell'app</span><span class="sxs-lookup"><span data-stu-id="cb7f7-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="cb7f7-147">Aggiungere quindi queste due costanti e la variabile *client* nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="cb7f7-148">Tornare al [portale di Azure](https://portal.azure.com) per recuperare la chiave primaria e l'URL dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-148">Then, head back to the [Azure portal](https://portal.azure.com) to retrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="cb7f7-149">L'URL e la chiave primaria dell'endpoint sono necessari all'applicazione per conoscere la destinazione della connessione e ad Azure Cosmos DB per considerare attendibile la connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-149">The endpoint URL and primary key are necessary for your application to understand where to connect to, and for Azure Cosmos DB to trust your application's connection.</span></span>

<span data-ttu-id="cb7f7-150">Nel portale di Azure passare all'account Azure Cosmos DB, fare clic su **Chiavi**, quindi su **Chiavi di lettura/scrittura**.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-150">In the Azure portal, navigate to your Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="cb7f7-151">Copiare l'URI dal portale e incollarlo su `<your endpoint URL>` nel file program.cs.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-151">Copy the URI from the portal and paste it over `<your endpoint URL>` in the program.cs file.</span></span> <span data-ttu-id="cb7f7-152">Copiare quindi la CHIAVE PRIMARIA dal portale e incollarla su `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-152">Then copy the PRIMARY KEY from the portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="cb7f7-153">Assicurarsi di rimuovere `<` e `>` dai valori.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-153">Be sure to remove the `<` and `>` from your values.</span></span>

![Screenshot del portale di Azure usato nell'esercitazione su NoSQL per creare un'applicazione console C#.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="cb7f7-156"><a id="instantiate"></a>Creare un'istanza di DocumentClient</span><span class="sxs-lookup"><span data-stu-id="cb7f7-156"><a id="instantiate"></a>Instantiate the DocumentClient</span></span>

<span data-ttu-id="cb7f7-157">Creare ora una nuova istanza di **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-157">Now, create a new instance of the **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="cb7f7-158"><a id="create-database"></a>Creare un database</span><span class="sxs-lookup"><span data-stu-id="cb7f7-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="cb7f7-159">Creare quindi un [database](documentdb-resources.md#databases) di Azure Cosmos DB usando il metodo [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) o [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) della classe **DocumentClient** da [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using the [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of the **DocumentClient** class from the [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="cb7f7-160">Un database è il contenitore logico per l'archiviazione di documenti JSON partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-160">A database is the logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="cb7f7-161">Scegliere una chiave di partizione</span><span class="sxs-lookup"><span data-stu-id="cb7f7-161">Decide on a partition key</span></span> 

<span data-ttu-id="cb7f7-162">Le raccolte sono contenitori per l'archiviazione di documenti.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="cb7f7-163">Le raccolte sono risorse logiche e possono [comprendere una o più partizioni fisiche](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="cb7f7-164">Una [chiave di partizione](documentdb-partition-data.md) è una proprietà (o percorso) all'interno dei documenti che possono essere usati per distribuire i dati tra i server o le partizioni.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used to distribute your data among the servers or partitions.</span></span> <span data-ttu-id="cb7f7-165">Tutti i documenti con la stessa chiave di partizione vengono archiviati nella stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-165">All documents with the same partition key are stored in the same partition.</span></span> 

<span data-ttu-id="cb7f7-166">L'individuazione di una chiave di partizione è una decisione importante da prendere prima di creare una raccolta.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-166">Determining a partition key is an important decision to make before you create a collection.</span></span> <span data-ttu-id="cb7f7-167">Le chiavi di partizione sono una proprietà o percorso all'interno di documenti che possono essere usate da Azure Cosmos DB per distribuire i dati tra più server o più partizioni.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB to distribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="cb7f7-168">Cosmos DB eseguirà l'hashing del valore della chiave di partizione e userà il risultato con hash per determinare la partizione in cui archiviare il documento.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-168">Cosmos DB hashes the partition key value and uses the hashed result to determine the partition in which to store the document.</span></span> <span data-ttu-id="cb7f7-169">Tutti i documenti con la stessa chiave di partizione vengono archiviati nella stessa partizione e le chiavi di partizione non possono essere modificate dopo la creazione di una raccolta.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-169">All documents with the same partition key are stored in the same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="cb7f7-170">In questa esercitazione verrà impostata la chiave di partizione su `/deviceId` in modo che tutti i dati per un singolo dispositivo vengano archiviati in una singola partizione.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-170">For this tutorial, we're going to set the partition key to `/deviceId` so that the all the data for a single device is stored in a single partition.</span></span> <span data-ttu-id="cb7f7-171">È possibile scegliere una chiave di partizione contenente un numero elevato di valori, ognuno dei quali viene usato approssimativamente alla stessa frequenza per garantire che Cosmos DB possa bilanciare il carico in linea con la crescita dei dati e ottenere la velocità effettiva completa della raccolta.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-171">You want to choose a partition key that has a large number of values, each of which are used at about the same frequency to ensure Cosmos DB can load balance as your data grows and achieve the full throughput of the collection.</span></span> 

<span data-ttu-id="cb7f7-172">Per altre informazioni sul partizionamento, vedere [Come eseguire il partizionamento e il ridimensionamento in Azure Cosmos DB](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-172">For more information about partitioning, see [How to partition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="cb7f7-173"><a id="CreateColl"></a>Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="cb7f7-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="cb7f7-174">Ora che si conosce la chiave di partizione, `/deviceId`, è possibile creare una [raccolta](documentdb-resources.md#collections) usando il metodo [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) o [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using the [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="cb7f7-175">Una raccolta è un contenitore di documenti JSON e di eventuale logica dell'applicazione JavaScript associata.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="cb7f7-176">La creazione di una raccolta ha implicazioni a livello di prezzi, poiché si sta riservando velocità effettiva per l'applicazione per comunicare con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-176">Creating a collection has pricing implications, as you are reserving throughput for the application to communicate with Azure Cosmos DB.</span></span> <span data-ttu-id="cb7f7-177">Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here the JSON property deviceId is used  
// as the partition key to spread across partitions. Configured for 2500 RU/s  
// throughput and an indexing policy that supports sorting against any  
// number or string property. .
DocumentCollection myCollection = new DocumentCollection();
myCollection.Id = "coll";
myCollection.PartitionKey.Paths.Add("/deviceId");

await client.CreateDocumentCollectionAsync(
    UriFactory.CreateDatabaseUri("db"),
    myCollection,
    new RequestOptions { OfferThroughput = 2500 });
```

<span data-ttu-id="cb7f7-178">Questo metodo effettua una chiamata API REST ad Azure Cosmos DB e il servizio esegue il provisioning di una serie di partizioni in base alla velocità effettiva richiesta.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-178">This method makes a REST API call to Azure Cosmos DB, and the service provisions a number of partitions based on the requested throughput.</span></span> <span data-ttu-id="cb7f7-179">È possibile modificare la velocità effettiva di una raccolta se le esigenze in termini di prestazioni cambiano usando l'SDK o il [portale di Azure](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-179">You can change the throughput of a collection as your performance needs evolve using the SDK or the [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="cb7f7-180"><a id="CreateDoc"></a>Creare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="cb7f7-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="cb7f7-181">Verranno ora inseriti alcuni documenti JSON in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="cb7f7-182">È possibile creare un [documento](documentdb-resources.md#documents) usando il metodo [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) della classe **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-182">A [document](documentdb-resources.md#documents) can be created by using the [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of the **DocumentClient** class.</span></span> <span data-ttu-id="cb7f7-183">I documenti sono contenuto JSON definito dall'utente (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="cb7f7-184">Questa classe di esempio contiene una lettura di dispositivo e una chiamata a CreateDocumentAsync per inserire una nuova lettura di dispositivo in una raccolta.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-184">This sample class contains a device reading, and a call to CreateDocumentAsync to insert a new device reading into a collection.</span></span>

```csharp
public class DeviceReading
{
    [JsonProperty("id")]
    public string Id;

    [JsonProperty("deviceId")]
    public string DeviceId;

    [JsonConverter(typeof(IsoDateTimeConverter))]
    [JsonProperty("readingTime")]
    public DateTime ReadingTime;

    [JsonProperty("metricType")]
    public string MetricType;

    [JsonProperty("unit")]
    public string Unit;

    [JsonProperty("metricValue")]
    public double MetricValue;
  }

// Create a document. Here the partition key is extracted 
// as "XMS-0001" based on the collection definition
await client.CreateDocumentAsync(
    UriFactory.CreateDocumentCollectionUri("db", "coll"),
    new DeviceReading
    {
        Id = "XMS-001-FE24C",
        DeviceId = "XMS-0001",
        MetricType = "Temperature",
        MetricValue = 105.00,
        Unit = "Fahrenheit",
        ReadingTime = DateTime.UtcNow
    });
```
## <a name="read-data"></a><span data-ttu-id="cb7f7-185">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="cb7f7-185">Read data</span></span>

<span data-ttu-id="cb7f7-186">Leggere il documento in base alla chiave di partizione e l'ID usando il metodo ReadDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-186">Let's read the document by its partition key and Id using the ReadDocumentAsync method.</span></span> <span data-ttu-id="cb7f7-187">Si noti che le letture includono un valore PartitionKey, corrispondente all'intestazione di richiesta `x-ms-documentdb-partitionkey` nell'API REST.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-187">Note that the reads include a PartitionKey value (corresponding to the `x-ms-documentdb-partitionkey` request header in the REST API).</span></span>

```csharp
// Read document. Needs the partition key and the Id to be specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="cb7f7-188">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="cb7f7-188">Update data</span></span>

<span data-ttu-id="cb7f7-189">Ora si procederà all'aggiornamento di alcuni dati usando il metodo ReplaceDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-189">Now let's update some data using the ReplaceDocumentAsync method.</span></span>

```csharp
// Update the document. Partition key is not required, again extracted from the document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="cb7f7-190">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="cb7f7-190">Delete data</span></span>

<span data-ttu-id="cb7f7-191">Eliminare quindi un documento in base a chiave di partizione e ID usando il metodo DeleteDocumentAsync.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-191">Now lets delete a document by partition key and id by using the DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. The partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="cb7f7-192">Eseguire query su raccolte partizionate</span><span class="sxs-lookup"><span data-stu-id="cb7f7-192">Query partitioned collections</span></span>

<span data-ttu-id="cb7f7-193">Quando viene eseguita una query sui dati delle raccolte partizionate, Azure Cosmos DB instrada automaticamente la query alle partizioni corrispondenti ai valori della chiave di partizione specificati nel filtro (se presenti).</span><span class="sxs-lookup"><span data-stu-id="cb7f7-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes the query to the partitions corresponding to the partition key values specified in the filter (if there are any).</span></span> <span data-ttu-id="cb7f7-194">Ad esempio, questa query viene instradata solo alla partizione contenente la chiave di partizione "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="cb7f7-194">For example, this query is routed to just the partition containing the partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="cb7f7-195">La query seguente non dispone di un filtro per la chiave di partizione (DeviceId) e viene effettuato il fan-out a tutte le partizioni in cui viene eseguita a fronte dell'indice della partizione.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-195">The following query does not have a filter on the partition key (DeviceId) and is fanned out to all partitions where it is executed against the partition's index.</span></span> <span data-ttu-id="cb7f7-196">Si noti che è necessario specificare EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` nell'API REST) affinché l'SDK esegua una query tra le partizioni.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-196">Note that you have to specify the EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in the REST API) to have the SDK to execute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="cb7f7-197">Esecuzione di query in parallelo</span><span class="sxs-lookup"><span data-stu-id="cb7f7-197">Parallel query execution</span></span>
<span data-ttu-id="cb7f7-198">Gli SDK DocumentDB 1.9.0 e versioni successive di Azure Cosmos DB supportano le opzioni di esecuzione di query in parallelo, che consentono di eseguire query a bassa latenza sulle raccolte partizionate, anche quando è necessario toccare un numero elevato di partizioni.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-198">The Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you to perform low latency queries against partitioned collections, even when they need to touch a large number of partitions.</span></span> <span data-ttu-id="cb7f7-199">Ad esempio, la query seguente è configurata in modo da essere eseguita in parallelo tra le partizioni.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-199">For example, the following query is configured to run in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="cb7f7-200">È possibile gestire l'esecuzione di query in parallelo, ottimizzando i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb7f7-200">You can manage parallel query execution by tuning the following parameters:</span></span>

* <span data-ttu-id="cb7f7-201">Impostando `MaxDegreeOfParallelism`è possibile controllare il grado di parallelismo, ovvero il numero massimo di connessioni di rete simultanee alle partizioni della raccolta.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-201">By setting `MaxDegreeOfParallelism`, you can control the degree of parallelism i.e., the maximum number of simultaneous network connections to the collection's partitions.</span></span> <span data-ttu-id="cb7f7-202">Se si imposta questo valore su -1, il grado di parallelismo viene gestito dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-202">If you set this to -1, the degree of parallelism is managed by the SDK.</span></span> <span data-ttu-id="cb7f7-203">Se `MaxDegreeOfParallelism` non è specificato o è impostato su 0, ovvero il valore predefinito, esisterà una sola connessione di rete per le partizioni della raccolta.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-203">If the `MaxDegreeOfParallelism` is not specified or set to 0, which is the default value, there will be a single network connection to the collection's partitions.</span></span>
* <span data-ttu-id="cb7f7-204">Impostando `MaxBufferedItemCount` è possibile raggiungere un compromesso tra latenza della query e uso della memoria dal lato client.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="cb7f7-205">Se si omette questo parametro o si imposta su -1, il numero di elementi memorizzati nel buffer durante l'esecuzione di query in parallelo viene gestito dall'SDK.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-205">If you omit this parameter or set this to -1, the number of items buffered during parallel query execution is managed by the SDK.</span></span>

<span data-ttu-id="cb7f7-206">Considerato lo stato della raccolta, una query in parallelo restituirà i risultati nello stesso ordine dell'esecuzione seriale.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-206">Given the same state of the collection, a parallel query will return results in the same order as in serial execution.</span></span> <span data-ttu-id="cb7f7-207">Quando si esegue una query tra partizioni che include l'ordinamento (ORDER BY e/o TOP), l'SDK di DocumentDB esegue la query in parallelo tra le partizioni e unisce i risultati ordinati parzialmente sul lato client per produrre risultati ordinati a livello globale.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), the DocumentDB SDK issues the query in parallel across partitions and merges partially sorted results in the client side to produce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="cb7f7-208">Eseguire stored procedure</span><span class="sxs-lookup"><span data-stu-id="cb7f7-208">Execute stored procedures</span></span>
<span data-ttu-id="cb7f7-209">Infine è possibile eseguire transazioni atomiche rispetto a documenti con lo stesso ID dispositivo, ad esempio se si gestiscono aggregazioni o lo stato più recente di un dispositivo in un unico documento aggiungendo il codice seguente al progetto.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-209">Lastly, you can execute atomic transactions against documents with the same device ID, e.g. if you're maintaining aggregates or the latest state of a device in a single document by adding the following code to your project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="cb7f7-210">L'attività è terminata.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-210">And that's it!</span></span> <span data-ttu-id="cb7f7-211">Questi sono i componenti principali di un'applicazione Azure Cosmos DB che usa una chiave di partizione per scalare in modo efficiente la distribuzione dei dati tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-211">those are the main components of an Azure Cosmos DB application that uses a partition key to efficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="cb7f7-212">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="cb7f7-212">Clean up resources</span></span>

<span data-ttu-id="cb7f7-213">Se non si intende continuare a usare l'app, eliminare tutte le risorse create tramite l'esercitazione nel portale di Azure eseguendo questi passaggi:</span><span class="sxs-lookup"><span data-stu-id="cb7f7-213">If you're not going to continue to use this app, delete all resources created by this tutorial in the Azure portal with the following steps:</span></span>

1. <span data-ttu-id="cb7f7-214">Scegliere **Gruppi di risorse** dal menu a sinistra del portale di Azure e quindi fare clic sul nome univoco della risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-214">From the left-hand menu in the Azure portal, click **Resource groups** and then click the unique name of the resource you created.</span></span> 
2. <span data-ttu-id="cb7f7-215">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare il nome della risorsa da eliminare nella casella di testo e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-215">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cb7f7-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cb7f7-216">Next steps</span></span>

<span data-ttu-id="cb7f7-217">In questa esercitazione sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cb7f7-217">In this tutorial, you've done the following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="cb7f7-218">Creazione di un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cb7f7-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="cb7f7-219">Creazione di una raccolta e un database con una chiave di partizione</span><span class="sxs-lookup"><span data-stu-id="cb7f7-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="cb7f7-220">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="cb7f7-220">Created JSON documents</span></span>
> * <span data-ttu-id="cb7f7-221">Aggiornamento di un documento</span><span class="sxs-lookup"><span data-stu-id="cb7f7-221">Updated a document</span></span>
> * <span data-ttu-id="cb7f7-222">Esecuzione di query su raccolte partizionate</span><span class="sxs-lookup"><span data-stu-id="cb7f7-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="cb7f7-223">Esecuzione di una stored procedure</span><span class="sxs-lookup"><span data-stu-id="cb7f7-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="cb7f7-224">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="cb7f7-224">Deleted a document</span></span>
> * <span data-ttu-id="cb7f7-225">Eliminazione di un database</span><span class="sxs-lookup"><span data-stu-id="cb7f7-225">Deleted a database</span></span>

<span data-ttu-id="cb7f7-226">È ora possibile passare all'esercitazione successiva e importare i dati aggiuntivi nell'account Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cb7f7-226">You can now proceed to the next tutorial and import additional data to your Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="cb7f7-227">Importare dati in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cb7f7-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
