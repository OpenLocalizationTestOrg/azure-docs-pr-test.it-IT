---
title: "Cosmos Azure DB: Attività di sviluppo hello API DocumentDB in .NET | Documenti Microsoft"
description: Informazioni su come toodevelop con l'API DocumentDB Azure Cosmos DB usando .NET
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
ms.openlocfilehash: 0d3d17afa782054c8fdf3cbac421e5a5d0a6800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmosdb-develop-with-hello-documentdb-api-in-net"></a><span data-ttu-id="4b013-103">Azure CosmosDB: Sviluppare con hello API DocumentDB in .NET</span><span class="sxs-lookup"><span data-stu-id="4b013-103">Azure CosmosDB: Develop with hello DocumentDB API in .NET</span></span>

<span data-ttu-id="4b013-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="4b013-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="4b013-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="4b013-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span> 

<span data-ttu-id="4b013-106">Questa esercitazione viene illustrato come toocreate un account Azure Cosmos DB usando hello portale di Azure e quindi creare un database di documenti e una raccolta con un [chiave di partizione](documentdb-partition-data.md#partition-keys) utilizzando hello [API .NET di DocumentDB](documentdb-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="4b013-106">This tutorial demonstrates how toocreate an Azure Cosmos DB account using hello Azure portal, and then create a document database and collection with a [partition key](documentdb-partition-data.md#partition-keys) using hello [DocumentDB .NET API](documentdb-introduction.md).</span></span> <span data-ttu-id="4b013-107">Definendo una chiave di partizione quando si crea una raccolta, l'applicazione è pronta tooscale facilmente alla crescita dei dati.</span><span class="sxs-lookup"><span data-stu-id="4b013-107">By defining a partition key when you create a collection, your application is prepared tooscale effortlessly as your data grows.</span></span> 

<span data-ttu-id="4b013-108">Seguito hello esercitazione vengono illustrate le attività tramite hello [API .NET di DocumentDB](documentdb-sdk-dotnet.md):</span><span class="sxs-lookup"><span data-stu-id="4b013-108">This tutorial covers hello following tasks by using hello [DocumentDB .NET API](documentdb-sdk-dotnet.md):</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4b013-109">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4b013-109">Create an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="4b013-110">Creare una raccolta e un database con una chiave di partizione</span><span class="sxs-lookup"><span data-stu-id="4b013-110">Create a database and collection with a partition key</span></span>
> * <span data-ttu-id="4b013-111">Creare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="4b013-111">Create JSON documents</span></span>
> * <span data-ttu-id="4b013-112">Aggiornare un documento</span><span class="sxs-lookup"><span data-stu-id="4b013-112">Update a document</span></span>
> * <span data-ttu-id="4b013-113">Eseguire query su raccolte partizionate</span><span class="sxs-lookup"><span data-stu-id="4b013-113">Query partitioned collections</span></span>
> * <span data-ttu-id="4b013-114">Eseguire stored procedure</span><span class="sxs-lookup"><span data-stu-id="4b013-114">Run stored procedures</span></span>
> * <span data-ttu-id="4b013-115">Eliminare un documento</span><span class="sxs-lookup"><span data-stu-id="4b013-115">Delete a document</span></span>
> * <span data-ttu-id="4b013-116">Eliminare un database</span><span class="sxs-lookup"><span data-stu-id="4b013-116">Delete a database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b013-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="4b013-117">Prerequisites</span></span>
<span data-ttu-id="4b013-118">Assicurarsi di avere hello segue:</span><span class="sxs-lookup"><span data-stu-id="4b013-118">Please make sure you have hello following:</span></span>

* <span data-ttu-id="4b013-119">Un account Azure attivo.</span><span class="sxs-lookup"><span data-stu-id="4b013-119">An active Azure account.</span></span> <span data-ttu-id="4b013-120">Se non si ha un account, è possibile iscriversi per ottenere un [account gratuito](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="4b013-120">If you don't have one, you can sign up for a [free account](https://azure.microsoft.com/free/).</span></span> 
    * <span data-ttu-id="4b013-121">In alternativa, è possibile utilizzare hello [Azure Cosmos DB emulatore](local-emulator.md) per questa esercitazione, se si desidera toouse un ambiente locale che emula il servizio di Azure DocumentDB hello per scopi di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="4b013-121">Alternatively, you can use hello [Azure Cosmos DB Emulator](local-emulator.md) for this tutorial if you'd like toouse a local environment that emulates hello Azure DocumentDB service for development purposes.</span></span>
* <span data-ttu-id="4b013-122">[Visual Studio](http://www.visualstudio.com/)</span><span class="sxs-lookup"><span data-stu-id="4b013-122">[Visual Studio](http://www.visualstudio.com/).</span></span>

## <a name="create-an-azure-cosmos-db-account"></a><span data-ttu-id="4b013-123">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4b013-123">Create an Azure Cosmos DB account</span></span>

<span data-ttu-id="4b013-124">Iniziamo mediante la creazione di un account Azure Cosmos DB in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="4b013-124">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>

> [!TIP]
> * <span data-ttu-id="4b013-125">È stato già creato un account Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="4b013-125">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="4b013-126">In caso affermativo, andare troppo[configurazione della soluzione di Visual Studio](#SetupVS)</span><span class="sxs-lookup"><span data-stu-id="4b013-126">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS)</span></span>
> * <span data-ttu-id="4b013-127">Si dispone di un account Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="4b013-127">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="4b013-128">Se in tal caso, l'account è un account Azure Cosmos DB ed è possibile andare troppo[configurazione della soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="4b013-128">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="4b013-129">Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="4b013-129">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span> 
>
>

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

## <span data-ttu-id="4b013-130"><a id="SetupVS"></a>Configurare la soluzione di Visual Studio</span><span class="sxs-lookup"><span data-stu-id="4b013-130"><a id="SetupVS"></a>Set up your Visual Studio solution</span></span>
1. <span data-ttu-id="4b013-131">Aprire **Visual Studio** nel computer.</span><span class="sxs-lookup"><span data-stu-id="4b013-131">Open **Visual Studio** on your computer.</span></span>
2. <span data-ttu-id="4b013-132">In hello **File** dal menu **New**, quindi scegliere **progetto**.</span><span class="sxs-lookup"><span data-stu-id="4b013-132">On hello **File** menu, select **New**, and then choose **Project**.</span></span>
3. <span data-ttu-id="4b013-133">In hello **nuovo progetto** finestra di dialogo Seleziona **modelli** / **Visual c#** / **applicazione Console (.NET Framework)**, denominare il progetto e quindi fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b013-133">In hello **New Project** dialog, select **Templates** / **Visual C#** / **Console App (.NET Framework)**, name your project, and then click **OK**.</span></span>
   <span data-ttu-id="4b013-134">![Cattura di schermata della finestra Nuovo progetto hello](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span><span class="sxs-lookup"><span data-stu-id="4b013-134">![Screen shot of hello New Project window](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-new-project-2.png)</span></span>

4. <span data-ttu-id="4b013-135">In hello **Esplora**, fare clic con il pulsante destro sulla nuova applicazione console, ovvero in una soluzione di Visual Studio, e quindi fare clic su **Gestisci pacchetti NuGet...**</span><span class="sxs-lookup"><span data-stu-id="4b013-135">In hello **Solution Explorer**, right click on your new console application, which is under your Visual Studio solution, and then click **Manage NuGet Packages...**</span></span>
    
    ![Cattura di schermata del diritto hello Menu selezionato per hello progetto](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges.png)
5. <span data-ttu-id="4b013-137">In hello **NuGet** scheda, fare clic su **Sfoglia**e il tipo **documentdb** nella casella di ricerca hello.</span><span class="sxs-lookup"><span data-stu-id="4b013-137">In hello **NuGet** tab, click **Browse**, and type **documentdb** in hello search box.</span></span>
<!---stopped here--->
6. <span data-ttu-id="4b013-138">All'interno dei risultati di hello, trovare **Microsoft.Azure.DocumentDB** e fare clic su **installare**.</span><span class="sxs-lookup"><span data-stu-id="4b013-138">Within hello results, find **Microsoft.Azure.DocumentDB** and click **Install**.</span></span>
   <span data-ttu-id="4b013-139">ID del pacchetto per la libreria Client di Azure Cosmos DB hello Hello è [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span><span class="sxs-lookup"><span data-stu-id="4b013-139">hello package ID for hello Azure Cosmos DB Client Library is [Microsoft.Azure.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.DocumentDB).</span></span>
   <span data-ttu-id="4b013-140">![Cattura di schermata di hello NuGet Menu per la ricerca di Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span><span class="sxs-lookup"><span data-stu-id="4b013-140">![Screen shot of hello NuGet Menu for finding Azure Cosmos DB Client SDK](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-manage-nuget-pacakges-2.png)</span></span>

    <span data-ttu-id="4b013-141">Se viene visualizzato un messaggio sull'esaminato soluzione toohello modifiche, fare clic su **OK**.</span><span class="sxs-lookup"><span data-stu-id="4b013-141">If you get a message about reviewing changes toohello solution, click **OK**.</span></span> <span data-ttu-id="4b013-142">Se viene visualizzato un messaggio sull'accettazione della licenza, fare clic su **Accetto**.</span><span class="sxs-lookup"><span data-stu-id="4b013-142">If you get a message about license acceptance, click **I accept**.</span></span>

## <span data-ttu-id="4b013-143"><a id="Connect"></a>Aggiungere riferimenti tooyour progetto</span><span class="sxs-lookup"><span data-stu-id="4b013-143"><a id="Connect"></a>Add references tooyour project</span></span>
<span data-ttu-id="4b013-144">Hello rimanenti passaggi di questa esercitazione specificare hello API DocumentDB codice frammenti toocreate e aggiornare Azure Cosmos DB risorse necessarie nel progetto.</span><span class="sxs-lookup"><span data-stu-id="4b013-144">hello remaining steps in this tutorial provide hello DocumentDB API code snippets required toocreate and update Azure Cosmos DB resources in your project.</span></span>

<span data-ttu-id="4b013-145">Innanzitutto, aggiungere tali applicazioni, tooyour riferimenti.</span><span class="sxs-lookup"><span data-stu-id="4b013-145">First, add these references tooyour application.</span></span>
<!---These aren't added by default when you install hello pkg?--->

```csharp
using System.Net;
using Microsoft.Azure.Documents;
using Microsoft.Azure.Documents.Client;
using Newtonsoft.Json;
```

## <span data-ttu-id="4b013-146"><a id="add-references"></a>Connessione dell'app</span><span class="sxs-lookup"><span data-stu-id="4b013-146"><a id="add-references"></a>Connect your app</span></span>

<span data-ttu-id="4b013-147">Aggiungere quindi queste due costanti e la variabile *client* nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b013-147">Next, add these two constants and your *client* variable in your application.</span></span>

```csharp
private const string EndpointUrl = "<your endpoint URL>";
private const string PrimaryKey = "<your primary key>";
private DocumentClient client;
```

<span data-ttu-id="4b013-148">Head nuovamente toohello [portale di Azure](https://portal.azure.com) tooretrieve l'URL dell'endpoint e la chiave primaria.</span><span class="sxs-lookup"><span data-stu-id="4b013-148">Then, head back toohello [Azure portal](https://portal.azure.com) tooretrieve your endpoint URL and primary key.</span></span> <span data-ttu-id="4b013-149">URL dell'endpoint Hello e la chiave primaria sono necessari per l'applicazione toounderstand in tooconnect e per Azure Cosmos DB tootrust connessione dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="4b013-149">hello endpoint URL and primary key are necessary for your application toounderstand where tooconnect to, and for Azure Cosmos DB tootrust your application's connection.</span></span>

<span data-ttu-id="4b013-150">In hello portale di Azure passare tooyour Azure Cosmos DB account, fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**.</span><span class="sxs-lookup"><span data-stu-id="4b013-150">In hello Azure portal, navigate tooyour Azure Cosmos DB account, click **Keys**, and then click **Read-write Keys**.</span></span>

<span data-ttu-id="4b013-151">Copiare hello URI dal portale di hello e incollarla su `<your endpoint URL>` nel file program.cs hello.</span><span class="sxs-lookup"><span data-stu-id="4b013-151">Copy hello URI from hello portal and paste it over `<your endpoint URL>` in hello program.cs file.</span></span> <span data-ttu-id="4b013-152">Quindi copia hello chiave primaria dal portale hello e incollarla su `<your primary key>`.</span><span class="sxs-lookup"><span data-stu-id="4b013-152">Then copy hello PRIMARY KEY from hello portal and paste it over `<your primary key>`.</span></span> <span data-ttu-id="4b013-153">Essere certi hello tooremove `<` e `>` dai valori.</span><span class="sxs-lookup"><span data-stu-id="4b013-153">Be sure tooremove hello `<` and `>` from your values.</span></span>

![Cattura di schermata del portale di Azure hello utilizzato hello NoSQL esercitazione toocreate un'applicazione console c#.](./media/tutorial-develop-documentdb-dotnet/nosql-tutorial-keys.png)

## <span data-ttu-id="4b013-156"><a id="instantiate"></a>Creare un'istanza di hello DocumentClient</span><span class="sxs-lookup"><span data-stu-id="4b013-156"><a id="instantiate"></a>Instantiate hello DocumentClient</span></span>

<span data-ttu-id="4b013-157">A questo punto, creare una nuova istanza di hello **DocumentClient**.</span><span class="sxs-lookup"><span data-stu-id="4b013-157">Now, create a new instance of hello **DocumentClient**.</span></span>

```csharp
DocumentClient client = new DocumentClient(new Uri(endpoint), authKey);
```

## <span data-ttu-id="4b013-158"><a id="create-database"></a>Creare un database</span><span class="sxs-lookup"><span data-stu-id="4b013-158"><a id="create-database"></a>Create a database</span></span>

<span data-ttu-id="4b013-159">Successivamente, creare un database di Azure Cosmos [database](documentdb-resources.md#databases) utilizzando hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) metodo o [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) metodo hello  **DocumentClient** classe da hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span><span class="sxs-lookup"><span data-stu-id="4b013-159">Next, create an Azure Cosmos DB [database](documentdb-resources.md#databases) by using hello [CreateDatabaseAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdatabaseasync.aspx) method or [CreateDatabaseIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdatabaseifnotexistsasync.aspx) method of hello **DocumentClient** class from hello [DocumentDB .NET SDK](documentdb-sdk-dotnet.md).</span></span> <span data-ttu-id="4b013-160">Un database è contenitore logico di hello di archiviazione di documenti JSON partizionato nelle raccolte.</span><span class="sxs-lookup"><span data-stu-id="4b013-160">A database is hello logical container of JSON document storage partitioned across collections.</span></span>

```csharp
await client.CreateDatabaseAsync(new Database { Id = "db" });
```
## <a name="decide-on-a-partition-key"></a><span data-ttu-id="4b013-161">Scegliere una chiave di partizione</span><span class="sxs-lookup"><span data-stu-id="4b013-161">Decide on a partition key</span></span> 

<span data-ttu-id="4b013-162">Le raccolte sono contenitori per l'archiviazione di documenti.</span><span class="sxs-lookup"><span data-stu-id="4b013-162">Collections are containers for storing documents.</span></span> <span data-ttu-id="4b013-163">Le raccolte sono risorse logiche e possono [comprendere una o più partizioni fisiche](partition-data.md).</span><span class="sxs-lookup"><span data-stu-id="4b013-163">They are logical resources and can [span one or more physical partitions](partition-data.md).</span></span> <span data-ttu-id="4b013-164">Oggetto [chiave di partizione](documentdb-partition-data.md) è una proprietà (o percorso) all'interno dei documenti che viene utilizzato toodistribute i dati tra server hello o partizioni.</span><span class="sxs-lookup"><span data-stu-id="4b013-164">A [partition key](documentdb-partition-data.md) is a property (or path) within your documents that is used toodistribute your data among hello servers or partitions.</span></span> <span data-ttu-id="4b013-165">Tutti i documenti con hello stessa chiave di partizione vengono archiviati in hello stessa partizione.</span><span class="sxs-lookup"><span data-stu-id="4b013-165">All documents with hello same partition key are stored in hello same partition.</span></span> 

<span data-ttu-id="4b013-166">Individuazione di una chiave di partizione è un'importante decisione toomake prima di creare una raccolta.</span><span class="sxs-lookup"><span data-stu-id="4b013-166">Determining a partition key is an important decision toomake before you create a collection.</span></span> <span data-ttu-id="4b013-167">Le chiavi di partizione sono una proprietà (o percorso) all'interno dei documenti che possono essere utilizzati da Azure Cosmos DB toodistribute i dati tra più server o le partizioni.</span><span class="sxs-lookup"><span data-stu-id="4b013-167">Partition keys are a property (or path) within your documents that can be used by Azure Cosmos DB toodistribute your data among multiple servers or partitions.</span></span> <span data-ttu-id="4b013-168">COSMOS DB genera un hash per valore di chiave di partizione hello e partizione di hello eseguito l'hashing risultato toodetermine hello nella quale documento hello toostore.</span><span class="sxs-lookup"><span data-stu-id="4b013-168">Cosmos DB hashes hello partition key value and uses hello hashed result toodetermine hello partition in which toostore hello document.</span></span> <span data-ttu-id="4b013-169">Tutti i documenti con hello stessa chiave di partizione vengono archiviati nella stessa partizione di hello e le chiavi di partizione non possono essere modificate dopo aver creata una raccolta.</span><span class="sxs-lookup"><span data-stu-id="4b013-169">All documents with hello same partition key are stored in hello same partition, and partition keys cannot be changed once a collection is created.</span></span> 

<span data-ttu-id="4b013-170">Per questa esercitazione, si userà la chiave di partizione hello tooset troppo`/deviceId` così che hello tutti i dati di hello per un singolo dispositivo è archiviato in una singola partizione.</span><span class="sxs-lookup"><span data-stu-id="4b013-170">For this tutorial, we're going tooset hello partition key too`/deviceId` so that hello all hello data for a single device is stored in a single partition.</span></span> <span data-ttu-id="4b013-171">Si desidera toochoose una chiave di partizione che include un numero elevato di valori, ognuno dei quali vengono utilizzati in su hello stessa frequenza tooensure DB Cosmos possibile bilanciare il carico dei dati cresce e raggiungere una velocità effettiva completo hello dell'insieme di hello.</span><span class="sxs-lookup"><span data-stu-id="4b013-171">You want toochoose a partition key that has a large number of values, each of which are used at about hello same frequency tooensure Cosmos DB can load balance as your data grows and achieve hello full throughput of hello collection.</span></span> 

<span data-ttu-id="4b013-172">Per ulteriori informazioni sul partizionamento, vedere [come toopartition e la scala in Azure Cosmos DB?](partition-data.md)</span><span class="sxs-lookup"><span data-stu-id="4b013-172">For more information about partitioning, see [How toopartition and scale in Azure Cosmos DB?](partition-data.md)</span></span> 

## <span data-ttu-id="4b013-173"><a id="CreateColl"></a>Creare una raccolta</span><span class="sxs-lookup"><span data-stu-id="4b013-173"><a id="CreateColl"></a>Create a collection</span></span> 

<span data-ttu-id="4b013-174">Ora che si conosce la chiave di partizione, `/deviceId`, consente di creare un [raccolta](documentdb-resources.md#collections) utilizzando hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) metodo o [ CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) metodo hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="4b013-174">Now that we know our partition key, `/deviceId`, lets create a [collection](documentdb-resources.md#collections) by using hello [CreateDocumentCollectionAsync](https://msdn.microsoft.com/library/azure/microsoft.azure.documents.client.documentclient.createdocumentcollectionasync.aspx) method or [CreateDocumentCollectionIfNotExistsAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentcollectionifnotexistsasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="4b013-175">Una raccolta è un contenitore di documenti JSON e di eventuale logica dell'applicazione JavaScript associata.</span><span class="sxs-lookup"><span data-stu-id="4b013-175">A collection is a container of JSON documents and any associated JavaScript application logic.</span></span> 

> [!WARNING]
> <span data-ttu-id="4b013-176">Creazione di una raccolta ha implicazioni, prezzi che si desidera riservare una velocità effettiva per toocommunicate applicazione hello con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4b013-176">Creating a collection has pricing implications, as you are reserving throughput for hello application toocommunicate with Azure Cosmos DB.</span></span> <span data-ttu-id="4b013-177">Per altre informazioni, visitare la [pagina relativa ai prezzi](https://azure.microsoft.com/pricing/details/cosmos-db/).</span><span class="sxs-lookup"><span data-stu-id="4b013-177">For more details, please visit our [pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/)</span></span>
> 
> 

```csharp
// Collection for device telemetry. Here hello JSON property deviceId is used  
// as hello partition key toospread across partitions. Configured for 2500 RU/s  
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

<span data-ttu-id="4b013-178">Metodo lo rende un'API REST chiamare tooAzure DB Cosmos e hello esegue il provisioning del servizio di un numero di partizioni in base alla velocità effettiva richiesta hello.</span><span class="sxs-lookup"><span data-stu-id="4b013-178">This method makes a REST API call tooAzure Cosmos DB, and hello service provisions a number of partitions based on hello requested throughput.</span></span> <span data-ttu-id="4b013-179">È possibile modificare la velocità effettiva hello di una raccolta necessarie prestazioni più elevate evolvere utilizzando hello SDK o hello [portale di Azure](set-throughput.md).</span><span class="sxs-lookup"><span data-stu-id="4b013-179">You can change hello throughput of a collection as your performance needs evolve using hello SDK or hello [Azure portal](set-throughput.md).</span></span>

## <span data-ttu-id="4b013-180"><a id="CreateDoc"></a>Creare documenti JSON</span><span class="sxs-lookup"><span data-stu-id="4b013-180"><a id="CreateDoc"></a>Create JSON documents</span></span>
<span data-ttu-id="4b013-181">Verranno ora inseriti alcuni documenti JSON in Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="4b013-181">Let's insert some JSON documents into Azure Cosmos DB.</span></span> <span data-ttu-id="4b013-182">Oggetto [documento](documentdb-resources.md#documents) possono essere create usando hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) metodo hello **DocumentClient** classe.</span><span class="sxs-lookup"><span data-stu-id="4b013-182">A [document](documentdb-resources.md#documents) can be created by using hello [CreateDocumentAsync](https://msdn.microsoft.com/library/microsoft.azure.documents.client.documentclient.createdocumentasync.aspx) method of hello **DocumentClient** class.</span></span> <span data-ttu-id="4b013-183">I documenti sono contenuto JSON definito dall'utente (arbitrario).</span><span class="sxs-lookup"><span data-stu-id="4b013-183">Documents are user-defined (arbitrary) JSON content.</span></span> <span data-ttu-id="4b013-184">Questa classe di esempio contiene la lettura di un dispositivo e un tooinsert tooCreateDocumentAsync chiamata di un nuovo dispositivo di lettura in una raccolta.</span><span class="sxs-lookup"><span data-stu-id="4b013-184">This sample class contains a device reading, and a call tooCreateDocumentAsync tooinsert a new device reading into a collection.</span></span>

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

// Create a document. Here hello partition key is extracted 
// as "XMS-0001" based on hello collection definition
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
## <a name="read-data"></a><span data-ttu-id="4b013-185">Leggere i dati</span><span class="sxs-lookup"><span data-stu-id="4b013-185">Read data</span></span>

<span data-ttu-id="4b013-186">Di seguito, leggere il documento di hello la chiave di partizione e Id utilizzando il metodo ReadDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="4b013-186">Let's read hello document by its partition key and Id using hello ReadDocumentAsync method.</span></span> <span data-ttu-id="4b013-187">Si noti che le letture hello includano un valore PartitionKey (toohello corrispondente `x-ms-documentdb-partitionkey` intestazione della richiesta in hello API REST).</span><span class="sxs-lookup"><span data-stu-id="4b013-187">Note that hello reads include a PartitionKey value (corresponding toohello `x-ms-documentdb-partitionkey` request header in hello REST API).</span></span>

```csharp
// Read document. Needs hello partition key and hello Id toobe specified
Document result = await client.ReadDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });

DeviceReading reading = (DeviceReading)(dynamic)result;
```

## <a name="update-data"></a><span data-ttu-id="4b013-188">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="4b013-188">Update data</span></span>

<span data-ttu-id="4b013-189">Ora consente di aggiornare alcuni dati utilizzando il metodo ReplaceDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="4b013-189">Now let's update some data using hello ReplaceDocumentAsync method.</span></span>

```csharp
// Update hello document. Partition key is not required, again extracted from hello document
reading.MetricValue = 104;
reading.ReadingTime = DateTime.UtcNow;

await client.ReplaceDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  reading);
```

## <a name="delete-data"></a><span data-ttu-id="4b013-190">Eliminare i dati</span><span class="sxs-lookup"><span data-stu-id="4b013-190">Delete data</span></span>

<span data-ttu-id="4b013-191">Ora consente di eliminare un documento con chiave di partizione e id utilizzando il metodo DeleteDocumentAsync hello.</span><span class="sxs-lookup"><span data-stu-id="4b013-191">Now lets delete a document by partition key and id by using hello DeleteDocumentAsync method.</span></span>

```csharp
// Delete a document. hello partition key is required.
await client.DeleteDocumentAsync(
  UriFactory.CreateDocumentUri("db", "coll", "XMS-001-FE24C"), 
  new RequestOptions { PartitionKey = new PartitionKey("XMS-0001") });
```
## <a name="query-partitioned-collections"></a><span data-ttu-id="4b013-192">Eseguire query su raccolte partizionate</span><span class="sxs-lookup"><span data-stu-id="4b013-192">Query partitioned collections</span></span>

<span data-ttu-id="4b013-193">Quando si eseguono query dati in raccolte partizionate, Azure Cosmos DB automaticamente le route hello partizioni toohello query corrispondenti valori di chiave partizione toohello specificati nel filtro hello (se presenti).</span><span class="sxs-lookup"><span data-stu-id="4b013-193">When you query data in partitioned collections, Azure Cosmos DB automatically routes hello query toohello partitions corresponding toohello partition key values specified in hello filter (if there are any).</span></span> <span data-ttu-id="4b013-194">Ad esempio, questa query è indirizzato toojust hello partizione contenente hello chiave di partizione "XMS-0001".</span><span class="sxs-lookup"><span data-stu-id="4b013-194">For example, this query is routed toojust hello partition containing hello partition key "XMS-0001".</span></span>

```csharp
// Query using partition key
IQueryable<DeviceReading> query = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"))
    .Where(m => m.MetricType == "Temperature" && m.DeviceId == "XMS-0001");
```
    
<span data-ttu-id="4b013-195">Hello query seguente non dispone di un filtro sulla chiave di partizione hello (DeviceId) e viene disposta tooall partizioni in cui viene eseguita sull'indice della partizione hello.</span><span class="sxs-lookup"><span data-stu-id="4b013-195">hello following query does not have a filter on hello partition key (DeviceId) and is fanned out tooall partitions where it is executed against hello partition's index.</span></span> <span data-ttu-id="4b013-196">Si noti che è necessario toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello API REST) toohave hello SDK tooexecute una query tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="4b013-196">Note that you have toospecify hello EnableCrossPartitionQuery (`x-ms-documentdb-query-enablecrosspartition` in hello REST API) toohave hello SDK tooexecute a query across partitions.</span></span>

```csharp
// Query across partition keys
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true })
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100);
```

## <a name="parallel-query-execution"></a><span data-ttu-id="4b013-197">Esecuzione di query in parallelo</span><span class="sxs-lookup"><span data-stu-id="4b013-197">Parallel query execution</span></span>
<span data-ttu-id="4b013-198">Hello Azure Cosmos DB DocumentDB SDK alla 1.9.0 e versioni successive supportano opzioni di esecuzione di query parallele, che consentono a bassa latenza tooperform esegue query su raccolte partizionate, anche quando sono necessari tootouch un numero elevato di partizioni.</span><span class="sxs-lookup"><span data-stu-id="4b013-198">hello Azure Cosmos DB DocumentDB SDKs 1.9.0 and above support parallel query execution options, which allow you tooperform low latency queries against partitioned collections, even when they need tootouch a large number of partitions.</span></span> <span data-ttu-id="4b013-199">Ad esempio, hello seguente query è configurato toorun in parallelo tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="4b013-199">For example, hello following query is configured toorun in parallel across partitions.</span></span>

```csharp
// Cross-partition Order By queries
IQueryable<DeviceReading> crossPartitionQuery = client.CreateDocumentQuery<DeviceReading>(
    UriFactory.CreateDocumentCollectionUri("db", "coll"), 
    new FeedOptions { EnableCrossPartitionQuery = true, MaxDegreeOfParallelism = 10, MaxBufferedItemCount = 100})
    .Where(m => m.MetricType == "Temperature" && m.MetricValue > 100)
    .OrderBy(m => m.MetricValue);
```
    
<span data-ttu-id="4b013-200">È possibile gestire l'esecuzione parallela di query ottimizzando hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="4b013-200">You can manage parallel query execution by tuning hello following parameters:</span></span>

* <span data-ttu-id="4b013-201">Impostando `MaxDegreeOfParallelism`, è possibile controllare hello grado di parallelismo, ovvero hello massimo numero di partizioni della raccolta toohello connessioni di rete simultanee.</span><span class="sxs-lookup"><span data-stu-id="4b013-201">By setting `MaxDegreeOfParallelism`, you can control hello degree of parallelism i.e., hello maximum number of simultaneous network connections toohello collection's partitions.</span></span> <span data-ttu-id="4b013-202">Se si imposta questo troppo-1, livello hello di parallelismo è gestito da hello SDK.</span><span class="sxs-lookup"><span data-stu-id="4b013-202">If you set this too-1, hello degree of parallelism is managed by hello SDK.</span></span> <span data-ttu-id="4b013-203">Se hello `MaxDegreeOfParallelism` viene omesso o impostato too0, ovvero il valore di predefinito hello, saranno presenti partizioni di rete singola connessione toohello di una raccolta.</span><span class="sxs-lookup"><span data-stu-id="4b013-203">If hello `MaxDegreeOfParallelism` is not specified or set too0, which is hello default value, there will be a single network connection toohello collection's partitions.</span></span>
* <span data-ttu-id="4b013-204">Impostando `MaxBufferedItemCount` è possibile raggiungere un compromesso tra latenza della query e uso della memoria dal lato client.</span><span class="sxs-lookup"><span data-stu-id="4b013-204">By setting `MaxBufferedItemCount`, you can trade off query latency and client-side memory utilization.</span></span> <span data-ttu-id="4b013-205">Se si omette questo parametro o impostare troppo-1, numero di hello di elementi memorizzato nel buffer durante l'esecuzione di query parallele è gestito da hello SDK.</span><span class="sxs-lookup"><span data-stu-id="4b013-205">If you omit this parameter or set this too-1, hello number of items buffered during parallel query execution is managed by hello SDK.</span></span>

<span data-ttu-id="4b013-206">Dato hello stesso stato dell'insieme di hello, una query parallela restituisce risultati hello stesso ordine come in esecuzione seriale.</span><span class="sxs-lookup"><span data-stu-id="4b013-206">Given hello same state of hello collection, a parallel query will return results in hello same order as in serial execution.</span></span> <span data-ttu-id="4b013-207">Quando si esegue una query tra partizioni che include l'ordinamento (ORDER BY e/o superiore), hello DocumentDB SDK genera query hello in parallelo tra le partizioni e unisce parzialmente ordinato i risultati in hello client side tooproduce risultati ordinati globalmente.</span><span class="sxs-lookup"><span data-stu-id="4b013-207">When performing a cross-partition query that includes sorting (ORDER BY and/or TOP), hello DocumentDB SDK issues hello query in parallel across partitions and merges partially sorted results in hello client side tooproduce globally ordered results.</span></span>

## <a name="execute-stored-procedures"></a><span data-ttu-id="4b013-208">Eseguire stored procedure</span><span class="sxs-lookup"><span data-stu-id="4b013-208">Execute stored procedures</span></span>
<span data-ttu-id="4b013-209">Infine, è possibile eseguire le transazioni atomiche sui documenti con hello stesso ID del dispositivo, ad esempio, se si gestiscono le aggregazioni o hello stato più recente di un dispositivo in un unico documento aggiungendo hello progetto tooyour di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="4b013-209">Lastly, you can execute atomic transactions against documents with hello same device ID, e.g. if you're maintaining aggregates or hello latest state of a device in a single document by adding hello following code tooyour project.</span></span>

```csharp
await client.ExecuteStoredProcedureAsync<DeviceReading>(
    UriFactory.CreateStoredProcedureUri("db", "coll", "SetLatestStateAcrossReadings"),
    new RequestOptions { PartitionKey = new PartitionKey("XMS-001") }, 
    "XMS-001-FE24C");
```

<span data-ttu-id="4b013-210">L'attività è terminata.</span><span class="sxs-lookup"><span data-stu-id="4b013-210">And that's it!</span></span> <span data-ttu-id="4b013-211">Questi sono i componenti principali di hello di un'applicazione Azure Cosmos DB che utilizza una distribuzione di dati di partizione tooefficiently chiave scala tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="4b013-211">those are hello main components of an Azure Cosmos DB application that uses a partition key tooefficiently scale data distribution across partitions.</span></span>  

## <a name="clean-up-resources"></a><span data-ttu-id="4b013-212">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="4b013-212">Clean up resources</span></span>

<span data-ttu-id="4b013-213">Se non si ha intenzione toocontinue toouse questa app, eliminare tutte le risorse create da questa esercitazione hello portale di Azure con hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="4b013-213">If you're not going toocontinue toouse this app, delete all resources created by this tutorial in hello Azure portal with hello following steps:</span></span>

1. <span data-ttu-id="4b013-214">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic hello nome univoco della risorsa hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="4b013-214">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello unique name of hello resource you created.</span></span> 
2. <span data-ttu-id="4b013-215">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="4b013-215">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b013-216">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="4b013-216">Next steps</span></span>

<span data-ttu-id="4b013-217">In questa esercitazione, effettuata seguente hello:</span><span class="sxs-lookup"><span data-stu-id="4b013-217">In this tutorial, you've done hello following:</span></span> 

> [!div class="checklist"]
> * <span data-ttu-id="4b013-218">Creazione di un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4b013-218">Created an Azure Cosmos DB account</span></span>
> * <span data-ttu-id="4b013-219">Creazione di una raccolta e un database con una chiave di partizione</span><span class="sxs-lookup"><span data-stu-id="4b013-219">Created a database and collection with a partition key</span></span>
> * <span data-ttu-id="4b013-220">Creazione di documenti JSON</span><span class="sxs-lookup"><span data-stu-id="4b013-220">Created JSON documents</span></span>
> * <span data-ttu-id="4b013-221">Aggiornamento di un documento</span><span class="sxs-lookup"><span data-stu-id="4b013-221">Updated a document</span></span>
> * <span data-ttu-id="4b013-222">Esecuzione di query su raccolte partizionate</span><span class="sxs-lookup"><span data-stu-id="4b013-222">Queried partitioned collections</span></span>
> * <span data-ttu-id="4b013-223">Esecuzione di una stored procedure</span><span class="sxs-lookup"><span data-stu-id="4b013-223">Ran a stored procedure</span></span>
> * <span data-ttu-id="4b013-224">Eliminazione di un documento</span><span class="sxs-lookup"><span data-stu-id="4b013-224">Deleted a document</span></span>
> * <span data-ttu-id="4b013-225">Eliminazione di un database</span><span class="sxs-lookup"><span data-stu-id="4b013-225">Deleted a database</span></span>

<span data-ttu-id="4b013-226">È possibile continuare l'esercitazione successiva toohello e importare dati aggiuntivi tooyour DB Cosmos account.</span><span class="sxs-lookup"><span data-stu-id="4b013-226">You can now proceed toohello next tutorial and import additional data tooyour Cosmos DB account.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b013-227">Importare dati in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="4b013-227">Import data into Azure Cosmos DB</span></span>](import-data.md)
