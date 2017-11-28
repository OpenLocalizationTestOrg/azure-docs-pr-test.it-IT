---
title: 'Azure Cosmos DB: sviluppare con l''API Table in .NET | Documentazione Microsoft'
description: Informazioni su come sviluppare con l'API Table di Azure Cosmos DB usando .NET
services: cosmos-db
documentationcenter: 
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 4b22cb49-8ea2-483d-bc95-1172cd009498
ms.service: cosmos-db
ms.workload: 
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/10/2017
ms.author: arramac
ms.custom: mvc
ms.openlocfilehash: 52cb5f2569b6c3a5301752b1e8bfb6cea13ff7f6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="azure-cosmos-db-develop-with-the-table-api-in-net"></a><span data-ttu-id="cf20a-103">Azure Cosmos DB: sviluppare con l'API Table in .NET</span><span class="sxs-lookup"><span data-stu-id="cf20a-103">Azure Cosmos DB: Develop with the Table API in .NET</span></span>

<span data-ttu-id="cf20a-104">Azure Cosmos DB è il servizio di database di Microsoft multimodello distribuito a livello globale.</span><span class="sxs-lookup"><span data-stu-id="cf20a-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="cf20a-105">È possibile creare ed eseguire rapidamente query su database di documenti, coppie chiave-valore e grafi, sfruttando in ognuno dei casi i vantaggi offerti dalle funzionalità di scalabilità orizzontale e distribuzione globale alla base di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf20a-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from the global distribution and horizontal scale capabilities at the core of Azure Cosmos DB.</span></span>

<span data-ttu-id="cf20a-106">Questa esercitazione illustra le attività seguenti:</span><span class="sxs-lookup"><span data-stu-id="cf20a-106">This tutorial covers the following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="cf20a-107">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cf20a-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="cf20a-108">Abilitare la funzionalità nel file app.config</span><span class="sxs-lookup"><span data-stu-id="cf20a-108">Enable functionality in the app.config file</span></span> 
> * <span data-ttu-id="cf20a-109">Creare una tabella usando l'[API Table](table-introduction.md) (anteprima)</span><span class="sxs-lookup"><span data-stu-id="cf20a-109">Create a table using the [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="cf20a-110">Aggiungere un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="cf20a-110">Add an entity to a table</span></span> 
> * <span data-ttu-id="cf20a-111">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="cf20a-112">Recuperare una singola entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="cf20a-113">Eseguire query su entità tramite indici secondari automatici</span><span class="sxs-lookup"><span data-stu-id="cf20a-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="cf20a-114">Sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-114">Replace an entity</span></span> 
> * <span data-ttu-id="cf20a-115">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-115">Delete an entity</span></span> 
> * <span data-ttu-id="cf20a-116">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="cf20a-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="cf20a-117">Tabelle in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cf20a-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="cf20a-118">Azure Cosmos DB fornisce l'[API Table](table-introduction.md) (anteprima) per le applicazioni che necessitano di un archivio di coppie chiave-valore con una struttura senza schema.</span><span class="sxs-lookup"><span data-stu-id="cf20a-118">Azure Cosmos DB provides the [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="cf20a-119">È possibile usare gli SDK e le API REST di [archiviazione tabelle di Azure](../storage/common/storage-introduction.md) insieme ad Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf20a-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used to work with Azure Cosmos DB.</span></span> <span data-ttu-id="cf20a-120">È possibile usare Azure Cosmos DB per creare tabelle con requisiti di velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="cf20a-120">You can use Azure Cosmos DB to create tables with high throughput requirements.</span></span> <span data-ttu-id="cf20a-121">Azure Cosmos DB supporta le tabelle ottimizzate per la velocità effettiva, chiamate in modo informale "tabelle Premium", attualmente disponibili in anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="cf20a-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="cf20a-122">È possibile continuare a usare l'archiviazione tabelle di Azure per le tabelle con requisiti di archiviazione elevati e di velocità effettiva inferiori.</span><span class="sxs-lookup"><span data-stu-id="cf20a-122">You can continue to use Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="cf20a-123">Azure Cosmos DB introdurrà il supporto per le tabelle ottimizzate per l'archiviazione in uno dei prossimi aggiornamenti e gli account di archiviazione tabelle di Azure nuovi ed esistenti verranno aggiornati facilmente ad Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf20a-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded to Azure Cosmos DB.</span></span>

<span data-ttu-id="cf20a-124">Se attualmente si usa l'archiviazione tabelle di Azure, è possibile ottenere i vantaggi seguenti con "tabella Premium" in anteprima:</span><span class="sxs-lookup"><span data-stu-id="cf20a-124">If you currently use Azure Table storage, you gain the following benefits with the "premium table" preview:</span></span>

- <span data-ttu-id="cf20a-125">[Distribuzione globale](distribute-data-globally.md) chiavi in mano con multihosting e [failover automatici e manuali](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="cf20a-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="cf20a-126">Supporto per l'indicizzazione automatica indipendente dallo schema su tutte le proprietà ("indici secondari") e query rapide</span><span class="sxs-lookup"><span data-stu-id="cf20a-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="cf20a-127">Supporto per la [scalabilità indipendente di archiviazione e velocità effettiva](partition-data.md) in un numero qualsiasi di aree</span><span class="sxs-lookup"><span data-stu-id="cf20a-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="cf20a-128">Supporto per la [velocità effettiva dedicata per ogni tabella](request-units.md) scalabile da centinaia a milioni di richieste al secondo</span><span class="sxs-lookup"><span data-stu-id="cf20a-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds to millions of requests per second</span></span>
- <span data-ttu-id="cf20a-129">Supporto per [cinque livelli di coerenza perfezionabili](consistency-levels.md) per ottenere un compromesso ottimale tra disponibilità, latenza e coerenza in base alle esigenze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="cf20a-129">Support for [five tunable consistency levels](consistency-levels.md) to trade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="cf20a-130">Disponibilità al 99,99% all'interno di una singola area, possibilità di aggiungere altre aree per aumentare la disponibilità e [contratti di servizio completi leader nel settore](https://azure.microsoft.com/support/legal/sla/cosmos-db/) sulla disponibilità generale</span><span class="sxs-lookup"><span data-stu-id="cf20a-130">99.99% availability within a single region, and ability to add more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="cf20a-131">Usare la versione esistente di .NET SDK di Archiviazione di Azure senza apportare modifiche al codice dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="cf20a-131">Work with the existing Azure storage .NET SDK, and no code changes to your application</span></span>

<span data-ttu-id="cf20a-132">Nella fase di anteprima Azure Cosmos DB supporta l'API Table usando .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="cf20a-132">During the preview, Azure Cosmos DB supports the Table API using the .NET SDK.</span></span> <span data-ttu-id="cf20a-133">È possibile scaricare [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) da NuGet, che include le stesse classi e firme di metodi disponibili in [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), ma che permette anche di connettersi agli account Azure Cosmos DB tramite l'API Table.</span><span class="sxs-lookup"><span data-stu-id="cf20a-133">You can download the [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has the same classes and method signatures as the [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect to Azure Cosmos DB accounts using the Table API.</span></span>

<span data-ttu-id="cf20a-134">Per altre informazioni sulle attività complesse di archiviazione tabelle di Azure, vedere:</span><span class="sxs-lookup"><span data-stu-id="cf20a-134">To learn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="cf20a-135">Introduzione ad Azure Cosmos DB: API Table</span><span class="sxs-lookup"><span data-stu-id="cf20a-135">Introduction to Azure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="cf20a-136">Vedere la documentazione di riferimento del servizio tabelle per informazioni dettagliate sulle API disponibili nella[libreria client di archiviazione di Azure per .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409).</span><span class="sxs-lookup"><span data-stu-id="cf20a-136">The Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="cf20a-137">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="cf20a-137">About this tutorial</span></span>
<span data-ttu-id="cf20a-138">Questa esercitazione è rivolta agli sviluppatori con familiarità con l'SDK di archiviazione tabelle di Azure e che intendono usare le funzionalità Premium disponibili usando Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf20a-138">This tutorial is for developers who are familiar with the Azure Table storage SDK, and would like to use the premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="cf20a-139">È basata su [Introduzione all'archiviazione tabelle di Azure con .NET](table-storage-how-to-use-dotnet.md) e illustra come sfruttare le funzionalità aggiuntive, come gli indici secondari, la velocità effettiva con provisioning e il multihosting.</span><span class="sxs-lookup"><span data-stu-id="cf20a-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how to take advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="cf20a-140">Verrà illustrato come usare il portale di Azure per creare un account Azure Cosmos DB e quindi come compilare e distribuire un'applicazione di tabelle.</span><span class="sxs-lookup"><span data-stu-id="cf20a-140">We cover how to use the Azure portal to create an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="cf20a-141">Verranno esaminati anche esempi .NET per la creazione e l'eliminazione di una tabella, l'inserimento, l'aggiornamento, l'eliminazione e l'esecuzione di query per i dati delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="cf20a-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="cf20a-142">Se Visual Studio 2017 non è ancora installato, è possibile scaricare e usare la versione **gratuita** di [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="cf20a-142">If you don't already have Visual Studio 2017 installed, you can download and use the **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="cf20a-143">Durante l'installazione di Visual Studio abilitare **Sviluppo di Azure**.</span><span class="sxs-lookup"><span data-stu-id="cf20a-143">Make sure that you enable **Azure development** during the Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="cf20a-144">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="cf20a-144">Create a database account</span></span>

<span data-ttu-id="cf20a-145">Si inizia creando un account Azure Cosmos DB nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cf20a-145">Let's start by creating an Azure Cosmos DB account in the Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="cf20a-146">È stato già creato un account Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="cf20a-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="cf20a-147">In questo caso passare a [Configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="cf20a-147">If so, skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="cf20a-148">Si dispone di un account Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="cf20a-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="cf20a-149">In questo caso l'account è ora un account Azure Cosmos DB ed è possibile passare a [Configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="cf20a-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead to [Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="cf20a-150">Se si usa l'emulatore Azure Cosmos DB, seguire i passaggi descritti nell'articolo [Azure Cosmos DB Emulator](local-emulator.md) (Emulatore Azure Cosmos DB) per configurare l'emulatore e proseguire con il passaggio [Configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="cf20a-150">If you are using the Azure Cosmos DB Emulator, please follow the steps at [Azure Cosmos DB Emulator](local-emulator.md) to setup the emulator and skip ahead to [Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting to any location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-the-sample-application"></a><span data-ttu-id="cf20a-151">Clonare l'applicazione di esempio</span><span class="sxs-lookup"><span data-stu-id="cf20a-151">Clone the sample application</span></span>

<span data-ttu-id="cf20a-152">A questo punto è possibile clonare un'app Table da GitHub, impostare la stringa di connessione ed eseguirla.</span><span class="sxs-lookup"><span data-stu-id="cf20a-152">Now let's clone a Table app from github, set the connection string, and run it.</span></span>

1. <span data-ttu-id="cf20a-153">Aprire una finestra del terminale Git, ad esempio Git Bash ed eseguire il comando `cd` per passare a una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="cf20a-153">Open a git terminal window, such as git bash, and `cd` to a working directory.</span></span>  

2. <span data-ttu-id="cf20a-154">Eseguire il comando seguente per clonare l'archivio di esempio.</span><span class="sxs-lookup"><span data-stu-id="cf20a-154">Run the following command to clone the sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="cf20a-155">Aprire quindi il file della soluzione in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cf20a-155">Then open the solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="cf20a-156">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="cf20a-156">Update your connection string</span></span>

<span data-ttu-id="cf20a-157">Tornare ora al portale di Azure per recuperare le informazioni sulla stringa di connessione e copiarle nell'app.</span><span class="sxs-lookup"><span data-stu-id="cf20a-157">Now go back to the Azure portal to get your connection string information and copy it into the app.</span></span>

1. <span data-ttu-id="cf20a-158">Nell'account Azure Cosmos DB nel [portale di Azure](http://portal.azure.com/) fare clic su **Chiavi** nel riquadro di spostamento a sinistra e quindi su **Chiavi di lettura/scrittura**.</span><span class="sxs-lookup"><span data-stu-id="cf20a-158">In the [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in the left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="cf20a-159">Usare i pulsanti di copia sul lato destro dello schermo per copiare la stringa di connessione nel file app.config nel passaggio seguente.</span><span class="sxs-lookup"><span data-stu-id="cf20a-159">You'll use the copy buttons on the right side of the screen to copy the connection string into the app.config file in the next step.</span></span>

2. <span data-ttu-id="cf20a-160">In Visual Studio aprire il file app.config.</span><span class="sxs-lookup"><span data-stu-id="cf20a-160">In Visual Studio, open the app.config file.</span></span> 

3. <span data-ttu-id="cf20a-161">Copiare il valore di URI dal portale usando il pulsante di copia e impostarlo come valore della chiave dell'account in app.config. Usare il nome dell'account creato in precedenza per il nome dell'account in app.config.</span><span class="sxs-lookup"><span data-stu-id="cf20a-161">Copy your URI value from the portal (using the copy button) and make it the value of the account-key in app.config. Use the account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="cf20a-162">Per usare questa app con archiviazione tabelle di Azure standard, è necessario modificare la stringa di connessione in `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-162">To use this app with standard Azure Table Storage, you need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="cf20a-163">Usare il nome dell'account come nome dell'account Table e la chiave come chiave primaria di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cf20a-163">Use the account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-the-app"></a><span data-ttu-id="cf20a-164">Compilare e distribuire l'app</span><span class="sxs-lookup"><span data-stu-id="cf20a-164">Build and deploy the app</span></span>
1. <span data-ttu-id="cf20a-165">In Visual Studio fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="cf20a-165">In Visual Studio, right-click on the project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="cf20a-166">Nella casella **Sfoglia** di NuGet digitare ***WindowsAzure.Storage-PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="cf20a-166">In the NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="cf20a-167">Selezionare **Includi versione preliminare**.</span><span class="sxs-lookup"><span data-stu-id="cf20a-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="cf20a-168">Dai risultati installare **WindowsAzure.Storage-PremiumTable** e scegliere la compilazione di anteprima `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-168">From the results, install the **WindowsAzure.Storage-PremiumTable** and choose the preview build `0.0.1-preview`.</span></span> <span data-ttu-id="cf20a-169">Questa azione consente di installare il pacchetto di archiviazione tabelle di Azure e tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="cf20a-169">This action installs the Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="cf20a-170">Premere CTRL + F5 per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cf20a-170">Click CTRL + F5 to run the application.</span></span> 

<span data-ttu-id="cf20a-171">È ora possibile tornare a Esplora dati ed esaminare, eseguire query, modificare e lavorare con i dati di tabella.</span><span class="sxs-lookup"><span data-stu-id="cf20a-171">You can now go back to Data Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="cf20a-172">Per usare questa app con un emulatore Azure Cosmos DB, è sufficiente modificare la stringa di connessione in `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-172">To use this app with an Azure Cosmos DB Emulator, you just need to change the connection string in `app.config file`.</span></span> <span data-ttu-id="cf20a-173">Usare il valore seguente per l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="cf20a-173">Use the below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="cf20a-174">Funzionalità di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cf20a-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="cf20a-175">Azure Cosmos DB supporta numerose funzionalità non disponibili nell'API di archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="cf20a-175">Azure Cosmos DB supports a number of capabilities that are not available in the Azure Table storage API.</span></span> <span data-ttu-id="cf20a-176">La nuova funzionalità può essere abilitata tramite i valori di configurazione di `appSettings` seguenti.</span><span class="sxs-lookup"><span data-stu-id="cf20a-176">The new functionality can be enabled via the following `appSettings` configuration values.</span></span> <span data-ttu-id="cf20a-177">Non sono stati introdotti nuovi overload o firme nell'SDK di Archiviazione in anteprima.</span><span class="sxs-lookup"><span data-stu-id="cf20a-177">We did not introduce any new signatures or overloads to the preview Azure Storage SDK.</span></span> <span data-ttu-id="cf20a-178">È quindi possibile connettersi alle tabelle sia Standard sia Premium e usare gli altri servizi di Archiviazione di Azure, come BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="cf20a-178">This allows you to connect to both standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="cf20a-179">Chiave</span><span class="sxs-lookup"><span data-stu-id="cf20a-179">Key</span></span> | <span data-ttu-id="cf20a-180">Descrizione</span><span class="sxs-lookup"><span data-stu-id="cf20a-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cf20a-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="cf20a-181">TableConnectionMode</span></span>  | <span data-ttu-id="cf20a-182">Azure Cosmos DB supporta due modalità di connettività.</span><span class="sxs-lookup"><span data-stu-id="cf20a-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="cf20a-183">Nella modalità `Gateway` le richieste vengono sempre eseguite al gateway di Azure Cosmos DB, che le inoltra alle partizioni di dati corrispondenti.</span><span class="sxs-lookup"><span data-stu-id="cf20a-183">In `Gateway` mode, requests are always made to the Azure Cosmos DB gateway, which forwards it to the corresponding data partitions.</span></span> <span data-ttu-id="cf20a-184">Nella modalità di connettività `Direct` il client recupera il mapping delle tabelle alle partizioni e le richieste vengono eseguite direttamente nelle partizioni di dati.</span><span class="sxs-lookup"><span data-stu-id="cf20a-184">In `Direct` connectivity mode, the client fetches the mapping of tables to partitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="cf20a-185">È consigliabile usare il valore predefinito `Direct`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-185">We recommend `Direct`, the default.</span></span>  |
| <span data-ttu-id="cf20a-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="cf20a-186">TableConnectionProtocol</span></span> | <span data-ttu-id="cf20a-187">Azure Cosmos DB supporta due protocolli di connessione: `Https` e `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="cf20a-188">`Tcp` è il valore predefinito e consigliato perché si tratta di un protocollo più leggero.</span><span class="sxs-lookup"><span data-stu-id="cf20a-188">`Tcp` is the default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="cf20a-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="cf20a-189">TablePreferredLocations</span></span> | <span data-ttu-id="cf20a-190">Elenco delimitato da virgole dei percorsi (multihosting) preferiti per le letture.</span><span class="sxs-lookup"><span data-stu-id="cf20a-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="cf20a-191">Ogni account Azure Cosmos DB può essere associato a 1-30+ aree.</span><span class="sxs-lookup"><span data-stu-id="cf20a-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="cf20a-192">Ogni istanza del client può specificare un sottoinsieme di queste aree nell'ordine preferito per le letture a bassa latenza.</span><span class="sxs-lookup"><span data-stu-id="cf20a-192">Each client instance can specify a subset of these regions in the preferred order for low latency reads.</span></span> <span data-ttu-id="cf20a-193">Le aree devono essere denominate usando i [nomi visualizzati](https://msdn.microsoft.com/library/azure/gg441293.aspx), ad esempio, `West US`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-193">The regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="cf20a-194">Vedere anche [API multihosting](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="cf20a-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="cf20a-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="cf20a-195">TableConsistencyLevel</span></span> | <span data-ttu-id="cf20a-196">È possibile ottenere un compromesso ottimale tra disponibilità, coerenza e latenza scegliendo tra cinque livelli di coerenza ben definiti: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` ed `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="cf20a-197">Il valore predefinito è `Session`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-197">Default is `Session`.</span></span> <span data-ttu-id="cf20a-198">La scelta del livello di coerenza implica una differenza significativa a livello di prestazioni nelle installazioni con più aree.</span><span class="sxs-lookup"><span data-stu-id="cf20a-198">The choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="cf20a-199">Per i dettagli, vedere [Livelli di coerenza](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="cf20a-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="cf20a-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="cf20a-200">TableThroughput</span></span> | <span data-ttu-id="cf20a-201">Velocità effettiva riservata per la tabella espressa in unità di richiesta (UR) al secondo.</span><span class="sxs-lookup"><span data-stu-id="cf20a-201">Reserved throughput for the table expressed in request units (RU) per second.</span></span> <span data-ttu-id="cf20a-202">Le singole tabelle possono supportare centinaia di milioni di UR/s.</span><span class="sxs-lookup"><span data-stu-id="cf20a-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="cf20a-203">Vedere [Unità richiesta](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="cf20a-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="cf20a-204">Il valore predefinito è `400`</span><span class="sxs-lookup"><span data-stu-id="cf20a-204">Default is `400`</span></span> |
| <span data-ttu-id="cf20a-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="cf20a-205">TableIndexingPolicy</span></span> | <span data-ttu-id="cf20a-206">Indicizzazione secondaria coerente e automatica di tutte le colonne all'interno di tabelle</span><span class="sxs-lookup"><span data-stu-id="cf20a-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="cf20a-207">Conformazione delle stringhe JSON alla specifica dei criteri di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="cf20a-207">JSON string conforming to the indexing policy specification.</span></span> <span data-ttu-id="cf20a-208">Vedere [Criteri di indicizzazione](indexing-policies.md) per informazioni su come modificare i criteri di indicizzazione in modo da includere o escludere colonne specifiche.</span><span class="sxs-lookup"><span data-stu-id="cf20a-208">See [Indexing Policy](indexing-policies.md) to see how you can change indexing policy to include/exclude specific columns.</span></span> | <span data-ttu-id="cf20a-209">Indicizzazione automatica di tutte le proprietà (hash per le stringhe e range per i numeri)</span><span class="sxs-lookup"><span data-stu-id="cf20a-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="cf20a-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="cf20a-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="cf20a-211">Configurare il numero massimo di elementi restituiti per ogni query di tabella in un unico round trip.</span><span class="sxs-lookup"><span data-stu-id="cf20a-211">Configure the maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="cf20a-212">Il valore predefinito è `-1`, che consente ad Azure Cosmos DB di determinare in modo dinamico il valore in fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="cf20a-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |
| <span data-ttu-id="cf20a-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="cf20a-213">TableQueryEnableScan</span></span> | <span data-ttu-id="cf20a-214">Se la query non può usare l'indice per tutti i filtri, eseguirla comunque tramite un'analisi.</span><span class="sxs-lookup"><span data-stu-id="cf20a-214">If the query cannot use the index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="cf20a-215">Il valore predefinito è `false`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-215">Default is `false`.</span></span>|
| <span data-ttu-id="cf20a-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="cf20a-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="cf20a-217">Il grado di parallelismo per l'esecuzione di una query tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="cf20a-217">The degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="cf20a-218">`0` è seriale senza prelettura, `1` è seriale con prelettura e valori più alti aumentano il grado di parallelismo.</span><span class="sxs-lookup"><span data-stu-id="cf20a-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase the rate of parallelism.</span></span> <span data-ttu-id="cf20a-219">Il valore predefinito è `-1`, che consente ad Azure Cosmos DB di determinare in modo dinamico il valore in fase di runtime.</span><span class="sxs-lookup"><span data-stu-id="cf20a-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine the value at runtime.</span></span> |

<span data-ttu-id="cf20a-220">Per cambiare il valore predefinito, aprire il file `app.config` da Esplora soluzioni in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="cf20a-220">To change the default value, open the `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="cf20a-221">Aggiungere il contenuto dell'elemento `<appSettings>` illustrato di seguito.</span><span class="sxs-lookup"><span data-stu-id="cf20a-221">Add the contents of the `<appSettings>` element shown below.</span></span> <span data-ttu-id="cf20a-222">Sostituire `account-name` con il nome dell'account di archiviazione e `account-key` con la chiave di accesso dell'account.</span><span class="sxs-lookup"><span data-stu-id="cf20a-222">Replace `account-name` with the name of your storage account, and `account-key` with your account access key.</span></span> 

```xml
<configuration>
    <startup> 
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
    </startup>
    <appSettings>
      <!-- Client options -->
      <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key; TableEndpoint=https://account-name.documents.azure.com" />
      <add key="TableConnectionMode" value="Direct"/>
      <add key="TableConnectionProtocol" value="Tcp"/>
      <add key="TablePreferredLocations" value="East US, West US, North Europe"/>
      <add key="TableConsistencyLevel" value="Eventual"/>

      <!--Table creation options -->
      <add key="TableThroughput" value="700"/>
      <add key="TableIndexingPolicy" value="{""indexingMode"": ""Consistent""}"/>

      <!-- Table query options -->
      <add key="TableQueryMaxItemCount" value="-1"/>
      <add key="TableQueryEnableScan" value="false"/>
      <add key="TableQueryMaxDegreeOfParallelism" value="-1"/>
      <add key="TableQueryContinuationTokenLimitInKb" value="16"/>
            
    </appSettings>
</configuration>
```

<span data-ttu-id="cf20a-223">Ecco una breve panoramica delle operazioni eseguire nell'app.</span><span class="sxs-lookup"><span data-stu-id="cf20a-223">Let's make a quick review of what's happening in the app.</span></span> <span data-ttu-id="cf20a-224">Aprire il file `Program.cs`. Come si noterà, queste righe di codice creano le risorse di tabella.</span><span class="sxs-lookup"><span data-stu-id="cf20a-224">Open the `Program.cs` file and you find that these lines of code create the Table resources.</span></span> 

## <a name="create-the-table-client"></a><span data-ttu-id="cf20a-225">Creare il client di tabella</span><span class="sxs-lookup"><span data-stu-id="cf20a-225">Create the table client</span></span>
<span data-ttu-id="cf20a-226">Inizializzare `CloudTableClient` per connettersi all'account di tabella.</span><span class="sxs-lookup"><span data-stu-id="cf20a-226">You initialize a `CloudTableClient` to connect to the table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="cf20a-227">Questo client viene inizializzato usando i valori di configurazione `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel` e `TablePreferredLocations`, se specificato nelle impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="cf20a-227">This client is initialized using the `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in the app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="cf20a-228">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="cf20a-228">Create a table</span></span>
<span data-ttu-id="cf20a-229">Creare quindi una tabella usando `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="cf20a-230">La scalabilità delle tabelle in Azure Cosmos DB può essere indipendente in termini di archiviazione e velocità effettiva e il partizionamento viene gestito automaticamente dal servizio.</span><span class="sxs-lookup"><span data-stu-id="cf20a-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by the service.</span></span> <span data-ttu-id="cf20a-231">Azure Cosmos DB supporta le tabelle sia senza limitazioni sia con dimensioni fisse.</span><span class="sxs-lookup"><span data-stu-id="cf20a-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="cf20a-232">Vedere [Partizionamento in Azure Cosmos DB](partition-data.md) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="cf20a-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="cf20a-233">Esiste una differenza importante nella creazione delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="cf20a-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="cf20a-234">Azure Cosmos DB riserva la velocità effettiva, a differenza del modello in base al consumo di Archiviazione di Azure per le transazioni.</span><span class="sxs-lookup"><span data-stu-id="cf20a-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="cf20a-235">Il modello di prenotazione offre due vantaggi principali:</span><span class="sxs-lookup"><span data-stu-id="cf20a-235">The reservation model has two key benefits:</span></span>

* <span data-ttu-id="cf20a-236">La velocità effettiva è dedicata/riservata e quindi non viene mai limitata, se la frequenza di richiesta è pari o inferiore alla velocità effettiva con provisioning</span><span class="sxs-lookup"><span data-stu-id="cf20a-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="cf20a-237">Il modello di prenotazione è più [conveniente economicamente per carichi di lavoro elevati in termini di velocità effettiva](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="cf20a-237">The reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="cf20a-238">È possibile configurare la velocità effettiva predefinita configurando l'impostazione per `TableThroughput` in termini di UR (unità di richiesta) al secondo.</span><span class="sxs-lookup"><span data-stu-id="cf20a-238">You can configure the default throughput by configuring the setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="cf20a-239">La lettura di un'entità di 1 KB viene normalizzata come 1 UR e le altre operazioni vengono normalizzate in una UR a valore fisso in base al consumo di CPU, memoria e IOPS.</span><span class="sxs-lookup"><span data-stu-id="cf20a-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized to a fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="cf20a-240">Altre informazioni sulle [unità richiesta in Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="cf20a-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cf20a-241">Anche se l'SDK di archiviazione tabelle non supporta attualmente la modifica della velocità effettiva, è possibile modificare questo valore in qualsiasi momento tramite il portale di Azure o l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="cf20a-241">While Table storage SDK does not currently support modifying throughput, you can change the throughput instantaneously at any time using the Azure portal or Azure CLI.</span></span>

<span data-ttu-id="cf20a-242">Verranno quindi illustrate le semplici operazioni di lettura e scrittura (CRUD) usando questo SDK.</span><span class="sxs-lookup"><span data-stu-id="cf20a-242">Next, we walk through the simple read and write (CRUD) operations using the Azure Table storage SDK.</span></span> <span data-ttu-id="cf20a-243">Questa esercitazione illustra le latenze pari a singole unità di millisecondi e le query rapide fornite da Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf20a-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="cf20a-244">Aggiungere un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="cf20a-244">Add an entity to a table</span></span>
<span data-ttu-id="cf20a-245">Le entità in archiviazione tabelle di Azure si estendono dalla classe `TableEntity` e devono avere le proprietà `PartitionKey` e `RowKey`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-245">Entities in Azure Table storage extend from the `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="cf20a-246">Di seguito è riportata una definizione di esempio per un'entità cliente.</span><span class="sxs-lookup"><span data-stu-id="cf20a-246">Here's a sample definition for a customer entity.</span></span>

```csharp
public class CustomerEntity : TableEntity
{
    public CustomerEntity(string lastName, string firstName)
    {
        this.PartitionKey = lastName;
        this.RowKey = firstName;
    }

    public CustomerEntity() { }

    public string Email { get; set; }

    public string PhoneNumber { get; set; }
}
```

<span data-ttu-id="cf20a-247">Il frammento di codice seguente illustra come inserire un'entità con l'SDK di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cf20a-247">The following snippet shows how to insert an entity with the Azure storage SDK.</span></span> <span data-ttu-id="cf20a-248">Azure Cosmos DB è progettato per garantire una latenza ridotta su qualsiasi unità di scala, in tutto il mondo.</span><span class="sxs-lookup"><span data-stu-id="cf20a-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across the world.</span></span>

<span data-ttu-id="cf20a-249">Le scritture vengono completate in < 15 ms a p99 e ms ~ 6 a p50 per le applicazioni in esecuzione nella stessa area dell'account Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf20a-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in the same region as the Azure Cosmos DB account.</span></span> <span data-ttu-id="cf20a-250">Questa durata tiene conto del fatto che le scritture vengono confermate al client solo dopo la relativa replica sincrona, il commit permanente e l'indicizzazione di tutto il contenuto.</span><span class="sxs-lookup"><span data-stu-id="cf20a-250">And this duration accounts for the fact that writes are acknowledged back to the client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="cf20a-251">L'API Table di Azure Cosmos DB è disponibile in anteprima.</span><span class="sxs-lookup"><span data-stu-id="cf20a-251">The Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="cf20a-252">A livello di disponibilità generale, le garanzia di latenza p99 sono supportate dai contratti di servizio, come per le altre API di Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf20a-252">At general availability, the p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create the TableOperation object that inserts the customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute the insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="cf20a-253">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-253">Insert a batch of entities</span></span>
<span data-ttu-id="cf20a-254">Archiviazione tabelle di Azure supporta un'API di operazioni batch che consente di combinare gli aggiornamenti, le eliminazioni e gli inserimenti nella stessa singola operazione batch.</span><span class="sxs-lookup"><span data-stu-id="cf20a-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in the same single batch operation.</span></span> <span data-ttu-id="cf20a-255">Azure Cosmos DB non prevede alcune limitazioni all'API batch come archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="cf20a-255">Azure Cosmos DB does not have some of the limitations on the batch API as Azure Table storage.</span></span> <span data-ttu-id="cf20a-256">Ad esempio, è possibile eseguire più letture all'interno di un batch, più scritture nella stessa entità all'interno di un batch e non esiste il limite di 100 operazioni per ogni batch.</span><span class="sxs-lookup"><span data-stu-id="cf20a-256">For example, you can perform multiple reads within a batch, you can perform multiple writes to the same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create the batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it to the table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it to the table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities to the batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute the batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="cf20a-257">Recuperare una singola entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-257">Retrieve a single entity</span></span>
<span data-ttu-id="cf20a-258">I recuperi (GET) in Azure Cosmos DB vengono completati in < 10 ms a p99 e ~ 1 ms a p50 nella stessa area di Azure.</span><span class="sxs-lookup"><span data-stu-id="cf20a-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in the same Azure region.</span></span> <span data-ttu-id="cf20a-259">È possibile aggiungere il numero desiderato di aree al proprio account per le letture a bassa latenza e distribuire le applicazioni da leggere dall'area locale ("multihosting") impostando `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-259">You can add as many regions to your account for low latency reads, and deploy applications to read from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="cf20a-260">È possibile recuperare una singola entità tramite il frammento seguente:</span><span class="sxs-lookup"><span data-stu-id="cf20a-260">You can retrieve a single entity using the following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute the retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="cf20a-261">Informazioni sulle API multihosting in [Sviluppo con più aree](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="cf20a-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="cf20a-262">Eseguire query su entità tramite indici secondari automatici</span><span class="sxs-lookup"><span data-stu-id="cf20a-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="cf20a-263">È possibile eseguire query sulle tabelle usando la classe `TableQuery`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-263">Tables can be queried using the `TableQuery` class.</span></span> <span data-ttu-id="cf20a-264">Azure Cosmos DB dispone di un motore di database con ottimizzazione per la scrittura che indicizza automaticamente tutte le colonne all'interno della tabella.</span><span class="sxs-lookup"><span data-stu-id="cf20a-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="cf20a-265">L'indicizzazione in Azure Cosmos DB è indipendente dallo schema.</span><span class="sxs-lookup"><span data-stu-id="cf20a-265">Indexing in Azure Cosmos DB is agnostic to schema.</span></span> <span data-ttu-id="cf20a-266">Anche se lo schema è diverso da una riga all'altra o se lo schema cambia nel tempo, l'indicizzazione viene eseguita automaticamente.</span><span class="sxs-lookup"><span data-stu-id="cf20a-266">Therefore, even if your schema is different between rows, or if the schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="cf20a-267">Poiché Azure Cosmos DB supporta gli indici secondari automatici, le query su qualsiasi proprietà possono usare l'indice e possono essere gestite in modo efficiente.</span><span class="sxs-lookup"><span data-stu-id="cf20a-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use the index and be served efficiently.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");

// Filter against a property that's not partition key or row key
TableQuery<CustomerEntity> emailQuery = new TableQuery<CustomerEntity>().Where(
    TableQuery.GenerateFilterCondition("Email", QueryComparisons.Equal, "Ben@contoso.com"));

foreach (CustomerEntity entity in table.ExecuteQuery(emailQuery))
{
    Console.WriteLine("{0}, {1}\t{2}\t{3}", entity.PartitionKey, entity.RowKey,
        entity.Email, entity.PhoneNumber);
}
```

<span data-ttu-id="cf20a-268">In anteprima Azure Cosmos DB supporta le stesse funzionalità relative alle query di archiviazione tabelle di Azure per l'API Table.</span><span class="sxs-lookup"><span data-stu-id="cf20a-268">In preview, Azure Cosmos DB supports the same query functionality as Azure Table storage for the Table API.</span></span> <span data-ttu-id="cf20a-269">Azure Cosmos DB supporta anche l'ordinamento, le aggregazioni, le query geospaziali, la gerarchia e un'ampia gamma di funzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="cf20a-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="cf20a-270">La funzionalità aggiuntiva verrà fornita nell'API Table in un aggiornamento futuro del servizio.</span><span class="sxs-lookup"><span data-stu-id="cf20a-270">The additional functionality will be provided in the Table API in a future service update.</span></span> <span data-ttu-id="cf20a-271">Vedere [Query in Azure Cosmos DB](documentdb-sql-query.md) per una panoramica di queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="cf20a-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="cf20a-272">Sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-272">Replace an entity</span></span>
<span data-ttu-id="cf20a-273">Per aggiornare un'entità, recuperarla dal servizio tabelle, modificare l'oggetto entità e quindi salvare le modifiche nel servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="cf20a-273">To update an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="cf20a-274">Il codice seguente consente di modificare il numero di telefono di un cliente esistente.</span><span class="sxs-lookup"><span data-stu-id="cf20a-274">The following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="cf20a-275">Analogamente, è possibile eseguire operazioni `InsertOrMerge` o `Merge`.</span><span class="sxs-lookup"><span data-stu-id="cf20a-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="cf20a-276">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-276">Delete an entity</span></span>
<span data-ttu-id="cf20a-277">Per eliminare facilmente un'entità dopo averla recuperata, è possibile usare lo stesso modello illustrato per aggiornare un'entità.</span><span class="sxs-lookup"><span data-stu-id="cf20a-277">You can easily delete an entity after you have retrieved it by using the same pattern shown for updating an entity.</span></span> <span data-ttu-id="cf20a-278">Il codice seguente consente di recuperare ed eliminare un'entità customer.</span><span class="sxs-lookup"><span data-stu-id="cf20a-278">The following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="cf20a-279">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="cf20a-279">Delete a table</span></span>
<span data-ttu-id="cf20a-280">L'esempio di codice seguente consente infine di eliminare una tabella dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cf20a-280">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="cf20a-281">È possibile eliminare e ricreare una tabella immediatamente con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="cf20a-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="cf20a-282">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="cf20a-282">Clean up resources</span></span> 

<span data-ttu-id="cf20a-283">Se non si prevede di continuare a usare questa app, seguire questa procedura per eliminare tutte le risorse create da questa esercitazione nel portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="cf20a-283">If you're not going to continue to use this app, use the following steps to delete all resources created by this tutorial in the Azure portal.</span></span>   

1. <span data-ttu-id="cf20a-284">Scegliere **Gruppi di risorse** dal menu a sinistra del portale di Azure e quindi fare clic sul nome della risorsa creata.</span><span class="sxs-lookup"><span data-stu-id="cf20a-284">From the left-hand menu in the Azure portal, click **Resource groups** and then click the name of the resource you created.</span></span>  
2. <span data-ttu-id="cf20a-285">Nella pagina del gruppo di risorse fare clic su **Elimina**, digitare il nome della risorsa da eliminare nella casella di testo e quindi fare clic su **Elimina**.</span><span class="sxs-lookup"><span data-stu-id="cf20a-285">On your resource group page, click **Delete**, type the name of the resource to delete in the text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="cf20a-286">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cf20a-286">Next steps</span></span>

<span data-ttu-id="cf20a-287">In questa esercitazione è stato illustrato come iniziare a usare Azure Cosmos DB con l'API Table e sono state eseguite le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="cf20a-287">In this tutorial, we covered how to get started using Azure Cosmos DB with the Table API, and you've done the following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="cf20a-288">Creazione di un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="cf20a-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="cf20a-289">Abilitazione della funzionalità nel file app.config</span><span class="sxs-lookup"><span data-stu-id="cf20a-289">Enabled functionality in the app.config file</span></span> 
> * <span data-ttu-id="cf20a-290">Creazione di una tabella</span><span class="sxs-lookup"><span data-stu-id="cf20a-290">Created a table</span></span> 
> * <span data-ttu-id="cf20a-291">Aggiunta di un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="cf20a-291">Added an entity to a table</span></span> 
> * <span data-ttu-id="cf20a-292">Inserimento di un batch di entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="cf20a-293">Recupero di una singola entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="cf20a-294">Esecuzione di query di entità tramite indici secondari automatici</span><span class="sxs-lookup"><span data-stu-id="cf20a-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="cf20a-295">Sostituzione di un'entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-295">Replaced an entity</span></span> 
> * <span data-ttu-id="cf20a-296">Eliminazione di un'entità</span><span class="sxs-lookup"><span data-stu-id="cf20a-296">Deleted an entity</span></span> 
> * <span data-ttu-id="cf20a-297">Eliminazione di una tabella</span><span class="sxs-lookup"><span data-stu-id="cf20a-297">Deleted a table</span></span>  

<span data-ttu-id="cf20a-298">È ora possibile passare all'esercitazione successiva per altre informazioni sull'esecuzione di query sui dati di tabelle.</span><span class="sxs-lookup"><span data-stu-id="cf20a-298">You can now proceed to the next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="cf20a-299">Eseguire query con l'API Table</span><span class="sxs-lookup"><span data-stu-id="cf20a-299">Query with the Table API</span></span>](tutorial-query-table.md)
