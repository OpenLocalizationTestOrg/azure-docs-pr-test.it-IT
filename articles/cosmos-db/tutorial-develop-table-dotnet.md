---
title: 'Azure Cosmos DB: Sviluppare con API di tabelle in .NET hello | Documenti Microsoft'
description: Informazioni su come toodevelop con API di tabelle del database di Azure Cosmos usando .NET
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
ms.openlocfilehash: 70c6985a1dffdbcdb07e377f8ad10355bb97712a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cosmos-db-develop-with-hello-table-api-in-net"></a><span data-ttu-id="e4f1d-103">Cosmos Azure DB: Attività di sviluppo hello tabella API in .NET</span><span class="sxs-lookup"><span data-stu-id="e4f1d-103">Azure Cosmos DB: Develop with hello Table API in .NET</span></span>

<span data-ttu-id="e4f1d-104">Azure Cosmos DB è il servizio di database multimodello distribuito a livello globale di Microsoft.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-104">Azure Cosmos DB is Microsoft’s globally distributed multi-model database service.</span></span> <span data-ttu-id="e4f1d-105">Creare rapidamente e query chiave/valore, il documento e database grafico, ognuno dei quali trarre vantaggio dalla distribuzione globale hello e funzionalità di scalabilità orizzontale di base di Azure Cosmos DB hello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-105">You can quickly create and query document, key/value, and graph databases, all of which benefit from hello global distribution and horizontal scale capabilities at hello core of Azure Cosmos DB.</span></span>

<span data-ttu-id="e4f1d-106">Questa esercitazione sono trattati hello seguenti attività:</span><span class="sxs-lookup"><span data-stu-id="e4f1d-106">This tutorial covers hello following tasks:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="e4f1d-107">Creare un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e4f1d-107">Create an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="e4f1d-108">Abilitare la funzionalità nel file app. config hello</span><span class="sxs-lookup"><span data-stu-id="e4f1d-108">Enable functionality in hello app.config file</span></span> 
> * <span data-ttu-id="e4f1d-109">Creare una tabella utilizzando hello [tabella API](table-introduction.md) (anteprima)</span><span class="sxs-lookup"><span data-stu-id="e4f1d-109">Create a table using hello [Table API](table-introduction.md) (preview)</span></span>
> * <span data-ttu-id="e4f1d-110">Aggiungere una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-110">Add an entity tooa table</span></span> 
> * <span data-ttu-id="e4f1d-111">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-111">Insert a batch of entities</span></span> 
> * <span data-ttu-id="e4f1d-112">Recuperare una singola entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-112">Retrieve a single entity</span></span> 
> * <span data-ttu-id="e4f1d-113">Eseguire query su entità tramite indici secondari automatici</span><span class="sxs-lookup"><span data-stu-id="e4f1d-113">Query entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="e4f1d-114">Sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-114">Replace an entity</span></span> 
> * <span data-ttu-id="e4f1d-115">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-115">Delete an entity</span></span> 
> * <span data-ttu-id="e4f1d-116">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="e4f1d-116">Delete a table</span></span>
 
## <a name="tables-in-azure-cosmos-db"></a><span data-ttu-id="e4f1d-117">Tabelle in Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e4f1d-117">Tables in Azure Cosmos DB</span></span> 

<span data-ttu-id="e4f1d-118">DB Cosmos Azure fornisce hello [tabella API](table-introduction.md) (anteprima) per applicazioni che richiedono un archivio chiave-valore con una progettazione senza schema.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-118">Azure Cosmos DB provides hello [Table API](table-introduction.md) (preview) for applications that need a key-value store with a schema-less design.</span></span> <span data-ttu-id="e4f1d-119">[Archiviazione tabelle di Azure](../storage/common/storage-introduction.md) SDK e API REST possono essere utilizzati toowork con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-119">[Azure Table storage](../storage/common/storage-introduction.md) SDKs and REST APIs can be used toowork with Azure Cosmos DB.</span></span> <span data-ttu-id="e4f1d-120">È possibile utilizzare le tabelle di Azure Cosmos DB toocreate con requisiti di velocità effettiva elevata.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-120">You can use Azure Cosmos DB toocreate tables with high throughput requirements.</span></span> <span data-ttu-id="e4f1d-121">Azure Cosmos DB supporta le tabelle ottimizzate per la velocità effettiva, chiamate in modo informale "tabelle Premium", attualmente disponibili in anteprima pubblica.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-121">Azure Cosmos DB supports throughput-optimized tables (informally called "premium tables"), currently in public preview.</span></span> 

<span data-ttu-id="e4f1d-122">È possibile continuare toouse archiviazione tabelle di Azure per le tabelle con archiviazione elevate e minori requisiti di velocità effettiva.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-122">You can continue toouse Azure Table storage for tables with high storage and lower throughput requirements.</span></span> <span data-ttu-id="e4f1d-123">Azure DB Cosmos introduce anche il supporto per le tabelle con ottimizzazione per la memoria in un aggiornamento futuro e tabelle di Azure di nuove ed esistenti saranno facilmente gli account di archiviazione aggiornato tooAzure DB Cosmos.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-123">Azure Cosmos DB will introduce support for storage-optimized tables in a future update, and existing and new Azure Table storage accounts will be seamlessly upgraded tooAzure Cosmos DB.</span></span>

<span data-ttu-id="e4f1d-124">Se si utilizza archiviazione tabelle di Azure, si otterranno i seguenti vantaggi con anteprima di "tabella premium" hello hello:</span><span class="sxs-lookup"><span data-stu-id="e4f1d-124">If you currently use Azure Table storage, you gain hello following benefits with hello "premium table" preview:</span></span>

- <span data-ttu-id="e4f1d-125">[Distribuzione globale](distribute-data-globally.md) chiavi in mano con multihosting e [failover automatici e manuali](regional-failover.md)</span><span class="sxs-lookup"><span data-stu-id="e4f1d-125">Turn-key [global distribution](distribute-data-globally.md) with multi-homing and [automatic and manual failovers](regional-failover.md)</span></span>
- <span data-ttu-id="e4f1d-126">Supporto per l'indicizzazione automatica indipendente dallo schema su tutte le proprietà ("indici secondari") e query rapide</span><span class="sxs-lookup"><span data-stu-id="e4f1d-126">Support for automatic schema-agnostic indexing against all properties ("secondary indexes"), and fast queries</span></span> 
- <span data-ttu-id="e4f1d-127">Supporto per la [scalabilità indipendente di archiviazione e velocità effettiva](partition-data.md) in un numero qualsiasi di aree</span><span class="sxs-lookup"><span data-stu-id="e4f1d-127">Support for [independent scaling of storage and throughput](partition-data.md), across any number of regions</span></span>
- <span data-ttu-id="e4f1d-128">Supporto per [velocità effettiva dedicata per ogni tabella](request-units.md) che possono essere scalati da centinaia toomillions di richieste al secondo</span><span class="sxs-lookup"><span data-stu-id="e4f1d-128">Support for [dedicated throughput per table](request-units.md) that can be scaled from hundreds toomillions of requests per second</span></span>
- <span data-ttu-id="e4f1d-129">Supporto per [cinque livelli di coerenza ottimizzabili](consistency-levels.md) tootrade off disponibilità, latenza e la coerenza in base alle esigenze dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="e4f1d-129">Support for [five tunable consistency levels](consistency-levels.md) tootrade off availability, latency, and consistency based on your application needs</span></span>
- <span data-ttu-id="e4f1d-130">disponibilità del 99,99% all'interno di una singola area e possibilità tooadd altre aree per una maggiore disponibilità, e [SLA completi leader del settore](https://azure.microsoft.com/support/legal/sla/cosmos-db/) sulla disponibilità generale</span><span class="sxs-lookup"><span data-stu-id="e4f1d-130">99.99% availability within a single region, and ability tooadd more regions for higher availability, and [industry-leading comprehensive SLAs](https://azure.microsoft.com/support/legal/sla/cosmos-db/) on general availability</span></span>
- <span data-ttu-id="e4f1d-131">Utilizzo di archiviazione di Azure esistente hello .NET SDK e nessuna applicazione tooyour modifiche di codice</span><span class="sxs-lookup"><span data-stu-id="e4f1d-131">Work with hello existing Azure storage .NET SDK, and no code changes tooyour application</span></span>

<span data-ttu-id="e4f1d-132">Durante l'anteprima di hello, Azure Cosmos DB supporta hello API tabelle utilizzando hello .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-132">During hello preview, Azure Cosmos DB supports hello Table API using hello .NET SDK.</span></span> <span data-ttu-id="e4f1d-133">È possibile scaricare hello [anteprima di Azure Storage SDK](https://aka.ms/premiumtablenuget) da NuGet, che ha hello stesse classi e le firme del metodo come hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), ma anche possibile connettersi tooAzure DB Cosmos account utilizzando hello Tabella API.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-133">You can download hello [Azure Storage Preview SDK](https://aka.ms/premiumtablenuget) from NuGet, that has hello same classes and method signatures as hello [Azure Storage SDK](https://www.nuget.org/packages/WindowsAzure.Storage), but also can connect tooAzure Cosmos DB accounts using hello Table API.</span></span>

<span data-ttu-id="e4f1d-134">toolearn sulle attività di archiviazione Azure Table complesse, vedere:</span><span class="sxs-lookup"><span data-stu-id="e4f1d-134">toolearn more about complex Azure Table storage tasks, see:</span></span>

* [<span data-ttu-id="e4f1d-135">Introduzione tooAzure DB Cosmos: API di tabella</span><span class="sxs-lookup"><span data-stu-id="e4f1d-135">Introduction tooAzure Cosmos DB: Table API</span></span>](table-introduction.md)
* <span data-ttu-id="e4f1d-136">la documentazione di riferimento del servizio di tabella per informazioni dettagliate sulle API disponibili Hello [libreria Client di archiviazione per il riferimento di .NET](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span><span class="sxs-lookup"><span data-stu-id="e4f1d-136">hello Table service reference documentation for complete details about available APIs [Storage Client Library for .NET reference](http://go.microsoft.com/fwlink/?LinkID=390731&clcid=0x409)</span></span>

### <a name="about-this-tutorial"></a><span data-ttu-id="e4f1d-137">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="e4f1d-137">About this tutorial</span></span>
<span data-ttu-id="e4f1d-138">Per gli sviluppatori che hanno familiarità con hello archiviazione tabelle di Azure SDK e si desiderano toouse hello premium le funzionalità disponibili in questa esercitazione è utilizzando Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-138">This tutorial is for developers who are familiar with hello Azure Table storage SDK, and would like toouse hello premium features available using Azure Cosmos DB.</span></span> <span data-ttu-id="e4f1d-139">È basato su [Introduzione all'archiviazione tabelle di Azure usando .NET](table-storage-how-to-use-dotnet.md) e Mostra come tootake sfruttare le funzionalità aggiuntive come indici secondari, velocità effettiva di provisioning e multihoming.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-139">It is based on [Get Started with Azure Table storage using .NET](table-storage-how-to-use-dotnet.md) and shows how tootake advantage of additional capabilities like secondary indexes, provisioned throughput, and multi-homing.</span></span> <span data-ttu-id="e4f1d-140">Viene illustrata la modalità toouse hello toocreate portale Azure un account Azure Cosmos DB, quindi compilare e distribuire un'applicazione di tabella.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-140">We cover how toouse hello Azure portal toocreate an Azure Cosmos DB account, and then build and deploy a Table application.</span></span> <span data-ttu-id="e4f1d-141">Verranno esaminati anche esempi .NET per la creazione e l'eliminazione di una tabella, l'inserimento, l'aggiornamento, l'eliminazione e l'esecuzione di query per i dati delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-141">We also walk through .NET examples for creating and deleting a table, and inserting, updating, deleting, and querying table data.</span></span> 

<span data-ttu-id="e4f1d-142">Se si dispone già di Visual Studio 2017, che installata, è possibile scaricare e utilizzare hello **libero** [2017 di Visual Studio Community Edition](https://www.visualstudio.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="e4f1d-142">If you don't already have Visual Studio 2017 installed, you can download and use hello **free** [Visual Studio 2017 Community Edition](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="e4f1d-143">Assicurarsi di abilitare **lo sviluppo di Azure** durante l'installazione di Visual Studio hello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-143">Make sure that you enable **Azure development** during hello Visual Studio setup.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="create-a-database-account"></a><span data-ttu-id="e4f1d-144">Creare un account di database</span><span class="sxs-lookup"><span data-stu-id="e4f1d-144">Create a database account</span></span>

<span data-ttu-id="e4f1d-145">Iniziamo mediante la creazione di un account Azure Cosmos DB in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-145">Let's start by creating an Azure Cosmos DB account in hello Azure portal.</span></span>  

> [!TIP]
> * <span data-ttu-id="e4f1d-146">È stato già creato un account Azure Cosmos DB?</span><span class="sxs-lookup"><span data-stu-id="e4f1d-146">Already have an Azure Cosmos DB account?</span></span> <span data-ttu-id="e4f1d-147">In caso affermativo, andare troppo[configurazione della soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="e4f1d-147">If so, skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>
> * <span data-ttu-id="e4f1d-148">Si dispone di un account Azure DocumentDB?</span><span class="sxs-lookup"><span data-stu-id="e4f1d-148">Did you have an Azure DocumentDB account?</span></span> <span data-ttu-id="e4f1d-149">Se in tal caso, l'account è un account Azure Cosmos DB ed è possibile andare troppo[configurazione della soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="e4f1d-149">If so, your account is now an Azure Cosmos DB account and you can skip ahead too[Set up your Visual Studio solution](#SetupVS).</span></span>  
> * <span data-ttu-id="e4f1d-150">Se si utilizza hello Azure Cosmos DB emulatore, eseguire le operazioni di hello in [emulatore di Azure Cosmos DB](local-emulator.md) toosetup hello emulatore e andare troppo[configurare la soluzione di Visual Studio](#SetupVS).</span><span class="sxs-lookup"><span data-stu-id="e4f1d-150">If you are using hello Azure Cosmos DB Emulator, please follow hello steps at [Azure Cosmos DB Emulator](local-emulator.md) toosetup hello emulator and skip ahead too[Set up your Visual Studio Solution](#SetupVS).</span></span>
<!---Loc Comment: Please, check link [Set up your Visual Studio solution] since it's not redirecting tooany location.---> 
>
>

[!INCLUDE [cosmosdb-create-dbaccount-table](../../includes/cosmos-db-create-dbaccount-table.md)] 

## <a name="clone-hello-sample-application"></a><span data-ttu-id="e4f1d-151">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="e4f1d-151">Clone hello sample application</span></span>

<span data-ttu-id="e4f1d-152">Ora si clonare un'app di tabella da github, impostare la stringa di connessione hello ed eseguirlo.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-152">Now let's clone a Table app from github, set hello connection string, and run it.</span></span>

1. <span data-ttu-id="e4f1d-153">Aprire una finestra terminale git, ad esempio git bash, e `cd` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-153">Open a git terminal window, such as git bash, and `cd` tooa working directory.</span></span>  

2. <span data-ttu-id="e4f1d-154">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-154">Run hello following command tooclone hello sample repository.</span></span> 

    ```bash
    git clone https://github.com/Azure-Samples/azure-cosmos-db-table-dotnet-getting-started
    ```

3. <span data-ttu-id="e4f1d-155">Aprire quindi il file di soluzione hello in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-155">Then open hello solution file in Visual Studio.</span></span>

## <a name="update-your-connection-string"></a><span data-ttu-id="e4f1d-156">Aggiornare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="e4f1d-156">Update your connection string</span></span>

<span data-ttu-id="e4f1d-157">Tornare toohello tooget portale Azure le informazioni sulla stringa di connessione e copiarla in app hello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-157">Now go back toohello Azure portal tooget your connection string information and copy it into hello app.</span></span>

1. <span data-ttu-id="e4f1d-158">In hello [portale di Azure](http://portal.azure.com/)il Cosmos Azure DB account, nel riquadro di spostamento sinistro hello fare clic su **chiavi**, quindi fare clic su **le chiavi di lettura / scrittura**.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-158">In hello [Azure portal](http://portal.azure.com/), in your Azure Cosmos DB account, in hello left navigation click **Keys**, and then click **Read-write Keys**.</span></span> <span data-ttu-id="e4f1d-159">Si userà pulsanti copia hello sul lato destro hello hello schermata toocopy hello della stringa di connessione nel file app. config hello nel passaggio successivo hello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-159">You'll use hello copy buttons on hello right side of hello screen toocopy hello connection string into hello app.config file in hello next step.</span></span>

2. <span data-ttu-id="e4f1d-160">In Visual Studio, aprire il file app. config hello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-160">In Visual Studio, open hello app.config file.</span></span> 

3. <span data-ttu-id="e4f1d-161">Copiare il valore dell'URI dal portale di hello (con il pulsante di copia hello) e renderlo hello valore della chiave account hello in App. config. Utilizzare il nome di account hello creato in precedenza per il nome di account in App. config.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-161">Copy your URI value from hello portal (using hello copy button) and make it hello value of hello account-key in app.config. Use hello account name created earlier for account-name in app.config.</span></span>
  
```
<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;TableEndpoint=https://account-name.documents.azure.com" />
```

> [!NOTE]
> <span data-ttu-id="e4f1d-162">toouse questa app con l'archiviazione tabelle di Azure standard, è necessario toochange hello stringa di connessione `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-162">toouse this app with standard Azure Table Storage, you need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="e4f1d-163">Usa il nome di account di hello come nome dell'account di tabella e la chiave come chiave primaria di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-163">Use hello account name as Table-account name and key as Azure Storage Primary key.</span></span> <br>
>`<add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key;EndpointSuffix=core.windows.net" />`
> 
>

## <a name="build-and-deploy-hello-app"></a><span data-ttu-id="e4f1d-164">Compilare e distribuire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="e4f1d-164">Build and deploy hello app</span></span>
1. <span data-ttu-id="e4f1d-165">In Visual Studio, fare clic su progetto hello in **Esplora** e quindi fare clic su **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-165">In Visual Studio, right-click on hello project in **Solution Explorer** and then click **Manage NuGet Packages**.</span></span> 

2. <span data-ttu-id="e4f1d-166">In hello NuGet **Sfoglia** digitare ***Windowsazure PremiumTable***.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-166">In hello NuGet **Browse** box, type ***WindowsAzure.Storage-PremiumTable***.</span></span> <span data-ttu-id="e4f1d-167">Selezionare **Includi versione preliminare**.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-167">Check **Include prerelease versions**.</span></span>

3. <span data-ttu-id="e4f1d-168">Dai risultati di hello, installare hello **Windowsazure PremiumTable** e scegliere una build di anteprima hello `0.0.1-preview`.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-168">From hello results, install hello **WindowsAzure.Storage-PremiumTable** and choose hello preview build `0.0.1-preview`.</span></span> <span data-ttu-id="e4f1d-169">Questa azione Installa pacchetto di archiviazione Azure Table hello e tutte le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-169">This action installs hello Azure Table storage package and all dependencies.</span></span>

4. <span data-ttu-id="e4f1d-170">Premere CTRL + F5 applicazione hello toorun.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-170">Click CTRL + F5 toorun hello application.</span></span> 

<span data-ttu-id="e4f1d-171">È ora possibile tornare tooData Explorer e vedere query, modificare e lavorare con i dati nella tabella.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-171">You can now go back tooData Explorer and see query, modify, and work with this table data.</span></span> 

> [!NOTE]
> <span data-ttu-id="e4f1d-172">toouse toochange hello stringa di connessione è necessario che l'app con un emulatore DB Cosmos di Azure, è sufficiente `app.config file`.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-172">toouse this app with an Azure Cosmos DB Emulator, you just need toochange hello connection string in `app.config file`.</span></span> <span data-ttu-id="e4f1d-173">Hello utilizzare sotto il valore per l'emulatore.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-173">Use hello below value for emulator.</span></span> <br>
>`<add key="StorageConnectionString" value=DefaultEndpointsProtocol=https;AccountName=localhost;AccountKey=<insertkey>==;TableEndpoint=https://localhost -->`
> 
>

## <a name="azure-cosmos-db-capabilities"></a><span data-ttu-id="e4f1d-174">Funzionalità di Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e4f1d-174">Azure Cosmos DB capabilities</span></span>
<span data-ttu-id="e4f1d-175">DB Cosmos Azure supporta un numero di funzionalità che non sono disponibili nell'API di archiviazione Azure Table hello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-175">Azure Cosmos DB supports a number of capabilities that are not available in hello Azure Table storage API.</span></span> <span data-ttu-id="e4f1d-176">Hello nuova funzionalità può essere abilitata tramite il seguente hello `appSettings` i valori di configurazione.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-176">hello new functionality can be enabled via hello following `appSettings` configuration values.</span></span> <span data-ttu-id="e4f1d-177">Non si introdurre qualsiasi nuovo firme di overload toohello anteprima o Azure Storage SDK.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-177">We did not introduce any new signatures or overloads toohello preview Azure Storage SDK.</span></span> <span data-ttu-id="e4f1d-178">In questo modo si tooconnect tooboth standard e premium tabelle e lavoro con altri servizi di archiviazione di Azure come BLOB e code.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-178">This allows you tooconnect tooboth standard and premium tables, and work with other Azure Storage services like Blobs and Queues.</span></span> 


| <span data-ttu-id="e4f1d-179">Chiave</span><span class="sxs-lookup"><span data-stu-id="e4f1d-179">Key</span></span> | <span data-ttu-id="e4f1d-180">Descrizione</span><span class="sxs-lookup"><span data-stu-id="e4f1d-180">Description</span></span> |
| --- | --- |
| <span data-ttu-id="e4f1d-181">TableConnectionMode</span><span class="sxs-lookup"><span data-stu-id="e4f1d-181">TableConnectionMode</span></span>  | <span data-ttu-id="e4f1d-182">Azure Cosmos DB supporta due modalità di connettività.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-182">Azure Cosmos DB supports two connectivity modes.</span></span> <span data-ttu-id="e4f1d-183">In `Gateway` modalità, le richieste vengono inviate sempre toohello DB Cosmos Azure gateway, che inoltra toohello partizioni di dati corrispondente.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-183">In `Gateway` mode, requests are always made toohello Azure Cosmos DB gateway, which forwards it toohello corresponding data partitions.</span></span> <span data-ttu-id="e4f1d-184">In `Direct` modalità di connettività client hello recupera i mapping di hello di toopartitions di tabelle e le richieste vengono effettuate direttamente per le partizioni di dati.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-184">In `Direct` connectivity mode, hello client fetches hello mapping of tables toopartitions, and requests are made directly against data partitions.</span></span> <span data-ttu-id="e4f1d-185">È consigliabile `Direct`, hello predefinito.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-185">We recommend `Direct`, hello default.</span></span>  |
| <span data-ttu-id="e4f1d-186">TableConnectionProtocol</span><span class="sxs-lookup"><span data-stu-id="e4f1d-186">TableConnectionProtocol</span></span> | <span data-ttu-id="e4f1d-187">Azure Cosmos DB supporta due protocolli di connessione: `Https` e `Tcp`.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-187">Azure Cosmos DB supports two connection protocols - `Https` and `Tcp`.</span></span> <span data-ttu-id="e4f1d-188">`Tcp`hello predefinito e consigliato perché è più semplice.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-188">`Tcp` is hello default, and recommended because it is more lightweight.</span></span> |
| <span data-ttu-id="e4f1d-189">TablePreferredLocations</span><span class="sxs-lookup"><span data-stu-id="e4f1d-189">TablePreferredLocations</span></span> | <span data-ttu-id="e4f1d-190">Elenco delimitato da virgole dei percorsi (multihosting) preferiti per le letture.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-190">Comma-separated list of preferred (multi-homing) locations for reads.</span></span> <span data-ttu-id="e4f1d-191">Ogni account Azure Cosmos DB può essere associato a 1-30+ aree.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-191">Each Azure Cosmos DB account can be associated with 1-30+ regions.</span></span> <span data-ttu-id="e4f1d-192">Ogni istanza del client è possibile specificare un subset di queste aree nell'ordine preferito hello per le letture di bassa latenza.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-192">Each client instance can specify a subset of these regions in hello preferred order for low latency reads.</span></span> <span data-ttu-id="e4f1d-193">aree Hello devono essere denominate con i relativi [i nomi visualizzati](https://msdn.microsoft.com/library/azure/gg441293.aspx), ad esempio, `West US`.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-193">hello regions must be named using their [display names](https://msdn.microsoft.com/library/azure/gg441293.aspx), for example, `West US`.</span></span> <span data-ttu-id="e4f1d-194">Vedere anche [API multihosting](tutorial-global-distribution-table.md).</span><span class="sxs-lookup"><span data-stu-id="e4f1d-194">Also see [Multi-homing APIs](tutorial-global-distribution-table.md).</span></span>
| <span data-ttu-id="e4f1d-195">TableConsistencyLevel</span><span class="sxs-lookup"><span data-stu-id="e4f1d-195">TableConsistencyLevel</span></span> | <span data-ttu-id="e4f1d-196">È possibile ottenere un compromesso ottimale tra disponibilità, coerenza e latenza scegliendo tra cinque livelli di coerenza ben definiti: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix` ed `Eventual`.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-196">You can trade off between latency, consistency, and availability by choosing between five well-defined consistency levels: `Strong`, `Session`, `Bounded-Staleness`, `ConsistentPrefix`, and `Eventual`.</span></span> <span data-ttu-id="e4f1d-197">Il valore predefinito è `Session`.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-197">Default is `Session`.</span></span> <span data-ttu-id="e4f1d-198">scelta di Hello del livello di coerenza rende una differenza significativa nelle installazioni con più aree.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-198">hello choice of consistency level makes a significant performance difference in multi-region setups.</span></span> <span data-ttu-id="e4f1d-199">Per i dettagli, vedere [Livelli di coerenza](consistency-levels.md).</span><span class="sxs-lookup"><span data-stu-id="e4f1d-199">See [Consistency levels](consistency-levels.md) for details.</span></span> |
| <span data-ttu-id="e4f1d-200">TableThroughput</span><span class="sxs-lookup"><span data-stu-id="e4f1d-200">TableThroughput</span></span> | <span data-ttu-id="e4f1d-201">Velocità effettiva riservati per la tabella hello espressa in unità di richiesta (RU) al secondo.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-201">Reserved throughput for hello table expressed in request units (RU) per second.</span></span> <span data-ttu-id="e4f1d-202">Le singole tabelle possono supportare centinaia di milioni di UR/s.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-202">Single tables can support 100s-millions of RU/s.</span></span> <span data-ttu-id="e4f1d-203">Vedere [Unità richiesta](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="e4f1d-203">See [Request units](request-units.md).</span></span> <span data-ttu-id="e4f1d-204">Il valore predefinito è `400`</span><span class="sxs-lookup"><span data-stu-id="e4f1d-204">Default is `400`</span></span> |
| <span data-ttu-id="e4f1d-205">TableIndexingPolicy</span><span class="sxs-lookup"><span data-stu-id="e4f1d-205">TableIndexingPolicy</span></span> | <span data-ttu-id="e4f1d-206">Indicizzazione secondaria coerente e automatica di tutte le colonne all'interno di tabelle</span><span class="sxs-lookup"><span data-stu-id="e4f1d-206">Consistent and automatic secondary indexing of all columns within tables</span></span> | <span data-ttu-id="e4f1d-207">JSON stringa conforme toohello specifica di criteri di indicizzazione.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-207">JSON string conforming toohello indexing policy specification.</span></span> <span data-ttu-id="e4f1d-208">Vedere [criteri di indicizzazione](indexing-policies.md) toosee come è possibile modificare l'indicizzazione di colonne specifiche dei criteri di tooinclude/exclude.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-208">See [Indexing Policy](indexing-policies.md) toosee how you can change indexing policy tooinclude/exclude specific columns.</span></span> | <span data-ttu-id="e4f1d-209">Indicizzazione automatica di tutte le proprietà (hash per le stringhe e range per i numeri)</span><span class="sxs-lookup"><span data-stu-id="e4f1d-209">Automatic indexing of all properties (hash for strings, and range for numbers)</span></span> |
| <span data-ttu-id="e4f1d-210">TableQueryMaxItemCount</span><span class="sxs-lookup"><span data-stu-id="e4f1d-210">TableQueryMaxItemCount</span></span> | <span data-ttu-id="e4f1d-211">Configurare hello il numero massimo di elementi restituiti per ogni query di tabella in un unico round trip.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-211">Configure hello maximum number of items returned per table query in a single round trip.</span></span> <span data-ttu-id="e4f1d-212">Valore predefinito è `-1`, che consente di determinare in modo dinamico il valore di hello in fase di esecuzione Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-212">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |
| <span data-ttu-id="e4f1d-213">TableQueryEnableScan</span><span class="sxs-lookup"><span data-stu-id="e4f1d-213">TableQueryEnableScan</span></span> | <span data-ttu-id="e4f1d-214">Se query hello non è possibile utilizzare indice hello per qualsiasi filtro, quindi eseguirlo comunque tramite un'analisi.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-214">If hello query cannot use hello index for any filter, then run it anyway via a scan.</span></span> <span data-ttu-id="e4f1d-215">Il valore predefinito è `false`.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-215">Default is `false`.</span></span>|
| <span data-ttu-id="e4f1d-216">TableQueryMaxDegreeOfParallelism</span><span class="sxs-lookup"><span data-stu-id="e4f1d-216">TableQueryMaxDegreeOfParallelism</span></span> | <span data-ttu-id="e4f1d-217">Hello grado di parallelismo per l'esecuzione di una query tra partizioni.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-217">hello degree of parallelism for execution of a cross-partition query.</span></span> <span data-ttu-id="e4f1d-218">`0`seriale con nessun recupero preliminare, `1` seriale con la prelettura e i valori più elevati di velocità di aumento hello di parallelismo.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-218">`0` is serial with no pre-fetching, `1` is serial with pre-fetching, and higher values increase hello rate of parallelism.</span></span> <span data-ttu-id="e4f1d-219">Valore predefinito è `-1`, che consente di determinare in modo dinamico il valore di hello in fase di esecuzione Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-219">Default is `-1`, which lets Azure Cosmos DB dynamically determine hello value at runtime.</span></span> |

<span data-ttu-id="e4f1d-220">valore predefinito di hello toochange, aprire hello `app.config` file da Esplora soluzioni in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-220">toochange hello default value, open hello `app.config` file from Solution Explorer in Visual Studio.</span></span> <span data-ttu-id="e4f1d-221">Aggiungere contenuto hello di hello `<appSettings>` elemento riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-221">Add hello contents of hello `<appSettings>` element shown below.</span></span> <span data-ttu-id="e4f1d-222">Sostituire `account-name` con nome hello dell'account di archiviazione, e `account-key` con la chiave di accesso di account.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-222">Replace `account-name` with hello name of your storage account, and `account-key` with your account access key.</span></span> 

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

<span data-ttu-id="e4f1d-223">Questo punto, eseguire una rapida panoramica delle operazioni eseguite nell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-223">Let's make a quick review of what's happening in hello app.</span></span> <span data-ttu-id="e4f1d-224">Aprire hello `Program.cs` file si scopre che le righe di codice creano hello risorse tabella.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-224">Open hello `Program.cs` file and you find that these lines of code create hello Table resources.</span></span> 

## <a name="create-hello-table-client"></a><span data-ttu-id="e4f1d-225">Creare hello tabella client</span><span class="sxs-lookup"><span data-stu-id="e4f1d-225">Create hello table client</span></span>
<span data-ttu-id="e4f1d-226">Inizializzare un `CloudTableClient` conto tabella di tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-226">You initialize a `CloudTableClient` tooconnect toohello table account.</span></span>

```csharp
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();
```
<span data-ttu-id="e4f1d-227">Questo client viene inizializzato con hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, e `TablePreferredLocations` i valori di configurazione se è specificato nelle impostazioni dell'app hello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-227">This client is initialized using hello `TableConnectionMode`, `TableConnectionProtocol`, `TableConsistencyLevel`, and `TablePreferredLocations` configuration values if specified in hello app settings.</span></span>
    
## <a name="create-a-table"></a><span data-ttu-id="e4f1d-228">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="e4f1d-228">Create a table</span></span>
<span data-ttu-id="e4f1d-229">Creare quindi una tabella usando `CloudTable`.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-229">Then, you create a table using `CloudTable`.</span></span> <span data-ttu-id="e4f1d-230">Le tabelle nel database di Azure Cosmos possono aumentare in modo indipendente in termini di archiviazione e la velocità effettiva e il partizionamento viene gestito automaticamente dal servizio hello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-230">Tables in Azure Cosmos DB can scale independently in terms of storage and throughput, and partitioning is handled automatically by hello service.</span></span> <span data-ttu-id="e4f1d-231">Azure Cosmos DB supporta le tabelle sia senza limitazioni sia con dimensioni fisse.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-231">Azure Cosmos DB supports both fixed size and unlimited tables.</span></span> <span data-ttu-id="e4f1d-232">Vedere [Partizionamento in Azure Cosmos DB](partition-data.md) per informazioni dettagliate.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-232">See [Partitioning in Azure Cosmos DB](partition-data.md) for details.</span></span> 

```csharp
CloudTable table = tableClient.GetTableReference("people");

table.CreateIfNotExists();
```

<span data-ttu-id="e4f1d-233">Esiste una differenza importante nella creazione delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-233">There is an important difference in how tables are created.</span></span> <span data-ttu-id="e4f1d-234">Azure Cosmos DB riserva la velocità effettiva, a differenza del modello in base al consumo di Archiviazione di Azure per le transazioni.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-234">Azure Cosmos DB reserves throughput, unlike Azure storage's consumption-based model for transactions.</span></span> <span data-ttu-id="e4f1d-235">modello di prenotazione Hello presenta due vantaggi principali:</span><span class="sxs-lookup"><span data-stu-id="e4f1d-235">hello reservation model has two key benefits:</span></span>

* <span data-ttu-id="e4f1d-236">La velocità effettiva è dedicata/riservata e quindi non viene mai limitata, se la frequenza di richiesta è pari o inferiore alla velocità effettiva con provisioning</span><span class="sxs-lookup"><span data-stu-id="e4f1d-236">Your throughput is dedicated/reserved, so you never get throttled if your request rate is at or below your provisioned throughput</span></span>
* <span data-ttu-id="e4f1d-237">modello di prenotazione Hello è più [economicamente conveniente per carichi di lavoro elevati in termini di velocità effettiva](key-value-store-cost.md)</span><span class="sxs-lookup"><span data-stu-id="e4f1d-237">hello reservation model is more [cost effective for throughput-heavy workloads](key-value-store-cost.md)</span></span>

<span data-ttu-id="e4f1d-238">È possibile configurare la velocità effettiva di hello predefinito configurando l'impostazione di hello per `TableThroughput` in termini di UR (unità di richiesta) al secondo.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-238">You can configure hello default throughput by configuring hello setting for `TableThroughput` in terms of RU (request units) per second.</span></span> 

<span data-ttu-id="e4f1d-239">Una lettura di un'entità di 1 KB viene normalizzata come 1 UR e altre operazioni vengono normalizzato tooa UR valore in base al loro consumo di CPU, memoria e IOPS fissato.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-239">A read of a 1-KB entity is normalized as 1 RU, and other operations are normalized tooa fixed RU value based on their CPU, memory, and IOPS consumption.</span></span> <span data-ttu-id="e4f1d-240">Altre informazioni sulle [unità richiesta in Azure Cosmos DB](request-units.md).</span><span class="sxs-lookup"><span data-stu-id="e4f1d-240">Learn more about [Request units in Azure Cosmos DB](request-units.md).</span></span>

> [!NOTE]
> <span data-ttu-id="e4f1d-241">Durante l'archiviazione tabelle SDK attualmente non supporta la modifica della velocità effettiva, è possibile modificare la velocità effettiva hello immediatamente in qualsiasi momento usando hello portale di Azure o CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-241">While Table storage SDK does not currently support modifying throughput, you can change hello throughput instantaneously at any time using hello Azure portal or Azure CLI.</span></span>

<span data-ttu-id="e4f1d-242">Successivamente, si analizzerà lettura semplice hello operazioni e scrittura (CRUD) utilizza hello l'archiviazione tabelle di Azure SDK.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-242">Next, we walk through hello simple read and write (CRUD) operations using hello Azure Table storage SDK.</span></span> <span data-ttu-id="e4f1d-243">Questa esercitazione illustra le latenze pari a singole unità di millisecondi e le query rapide fornite da Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-243">This tutorial demonstrates predictable low single-digit millisecond latencies and fast queries provided by Azure Cosmos DB.</span></span>

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="e4f1d-244">Aggiungere una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-244">Add an entity tooa table</span></span>
<span data-ttu-id="e4f1d-245">Entità nell'archiviazione tabelle di Azure si estendono da hello `TableEntity` classe e deve avere `PartitionKey` e `RowKey` proprietà.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-245">Entities in Azure Table storage extend from hello `TableEntity` class and must have `PartitionKey` and `RowKey` properties.</span></span> <span data-ttu-id="e4f1d-246">Di seguito è riportata una definizione di esempio per un'entità cliente.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-246">Here's a sample definition for a customer entity.</span></span>

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

<span data-ttu-id="e4f1d-247">Hello frammento di codice seguente viene illustrato come tooinsert un'entità con hello Azure storage SDK.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-247">hello following snippet shows how tooinsert an entity with hello Azure storage SDK.</span></span> <span data-ttu-id="e4f1d-248">Azure DB Cosmos è progettato per garantito a bassa latenza la scala, tutto il mondo hello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-248">Azure Cosmos DB is designed for guaranteed low latency at any scale, across hello world.</span></span>

<span data-ttu-id="e4f1d-249">Completamento di scritture < 15 ms p99 e ms ~ 6 in p50 per le applicazioni in esecuzione in hello hello account Azure Cosmos DB stessa area.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-249">Writes complete <15 ms at p99 and ~6 ms at p50 for applications running in hello same region as hello Azure Cosmos DB account.</span></span> <span data-ttu-id="e4f1d-250">E questa durata gli account per il fatto di hello che scrive vengano riconosciuti toohello indietro client solo dopo che vengono replicati in modo sincrono, in modo durevole committed, e tutto il contenuto viene indicizzato.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-250">And this duration accounts for hello fact that writes are acknowledged back toohello client only after they are synchronously replicated, durably committed, and all content is indexed.</span></span>

<span data-ttu-id="e4f1d-251">API di tabelle di Azure Cosmos DB Hello è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-251">hello Table API for Azure Cosmos DB is in preview.</span></span> <span data-ttu-id="e4f1d-252">Al momento della disponibilità generale, le garanzie di latenza p99 hello sono supportate da contratti di servizio come altre API DB Cosmos di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-252">At general availability, hello p99 latency guarantees are backed by SLAs like other Azure Cosmos DB APIs.</span></span> 

```csharp
// Create a new customer entity.
CustomerEntity customer1 = new CustomerEntity("Harp", "Walter");
customer1.Email = "Walter@contoso.com";
customer1.PhoneNumber = "425-555-0101";

// Create hello TableOperation object that inserts hello customer entity.
TableOperation insertOperation = TableOperation.Insert(customer1);

// Execute hello insert operation.
table.Execute(insertOperation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="e4f1d-253">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-253">Insert a batch of entities</span></span>
<span data-ttu-id="e4f1d-254">Archiviazione tabella Azure supporta un'API di operazione batch, che consente di combina aggiornamenti, eliminazioni e inserimenti in hello stessa singola operazione batch.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-254">Azure Table storage supports a batch operation API, that lets you combine updates, deletes, and inserts in hello same single batch operation.</span></span> <span data-ttu-id="e4f1d-255">Azure Cosmos DB non è disponibile alcune delle limitazioni di hello in batch hello API come archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-255">Azure Cosmos DB does not have some of hello limitations on hello batch API as Azure Table storage.</span></span> <span data-ttu-id="e4f1d-256">Ad esempio, è possibile eseguire più operazioni di lettura in un batch, è possibile eseguire più operazioni di scrittura toohello stessa entità all'interno di un batch, e non vi sono limiti su 100 operazioni per ogni batch.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-256">For example, you can perform multiple reads within a batch, you can perform multiple writes toohello same entity within a batch, and there is no limit on 100 operations per batch.</span></span> 

```csharp
// Create hello batch operation.
TableBatchOperation batchOperation = new TableBatchOperation();

// Create a customer entity and add it toohello table.
CustomerEntity customer1 = new CustomerEntity("Smith", "Jeff");
customer1.Email = "Jeff@contoso.com";
customer1.PhoneNumber = "425-555-0104";

// Create another customer entity and add it toohello table.
CustomerEntity customer2 = new CustomerEntity("Smith", "Ben");
customer2.Email = "Ben@contoso.com";
customer2.PhoneNumber = "425-555-0102";

// Add both customer entities toohello batch insert operation.
batchOperation.Insert(customer1);
batchOperation.Insert(customer2);

// Execute hello batch operation.
table.ExecuteBatch(batchOperation);
```
## <a name="retrieve-a-single-entity"></a><span data-ttu-id="e4f1d-257">Recuperare una singola entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-257">Retrieve a single entity</span></span>
<span data-ttu-id="e4f1d-258">Recupera (ottiene) nel database di Azure Cosmos completo < 10 ms p99 e ~ 1 ms in p50 in hello stessa area di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-258">Retrieves (GETs) in Azure Cosmos DB complete <10 ms at p99 and ~1 ms at p50 in hello same Azure region.</span></span> <span data-ttu-id="e4f1d-259">È possibile aggiungere account di tooyour tante aree per le letture di bassa latenza e distribuire applicazioni tooread da loro area locale ("multihomed") tramite l'impostazione `TablePreferredLocations`.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-259">You can add as many regions tooyour account for low latency reads, and deploy applications tooread from their local region ("multi-homed") by setting `TablePreferredLocations`.</span></span> 

<span data-ttu-id="e4f1d-260">È possibile recuperare una singola entità utilizzando hello frammento di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="e4f1d-260">You can retrieve a single entity using hello following snippet:</span></span>

```csharp
// Create a retrieve operation that takes a customer entity.
TableOperation retrieveOperation = TableOperation.Retrieve<CustomerEntity>("Smith", "Ben");

// Execute hello retrieve operation.
TableResult retrievedResult = table.Execute(retrieveOperation);
```
> [!TIP]
> <span data-ttu-id="e4f1d-261">Informazioni sulle API multihosting in [Sviluppo con più aree](tutorial-global-distribution-table.md)</span><span class="sxs-lookup"><span data-stu-id="e4f1d-261">Learn about multi-homing APIs at [Developing with multiple regions](tutorial-global-distribution-table.md)</span></span>
>

## <a name="query-entities-using-automatic-secondary-indexes"></a><span data-ttu-id="e4f1d-262">Eseguire query su entità tramite indici secondari automatici</span><span class="sxs-lookup"><span data-stu-id="e4f1d-262">Query entities using automatic secondary indexes</span></span>
<span data-ttu-id="e4f1d-263">Le tabelle possono essere eseguite utilizzando hello `TableQuery` classe.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-263">Tables can be queried using hello `TableQuery` class.</span></span> <span data-ttu-id="e4f1d-264">Azure Cosmos DB dispone di un motore di database con ottimizzazione per la scrittura che indicizza automaticamente tutte le colonne all'interno della tabella.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-264">Azure Cosmos DB has a write-optimized database engine that automatically indexes all columns within your table.</span></span> <span data-ttu-id="e4f1d-265">L'indicizzazione nel database di Azure Cosmos è tooschema agnostico.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-265">Indexing in Azure Cosmos DB is agnostic tooschema.</span></span> <span data-ttu-id="e4f1d-266">Pertanto, anche se lo schema è diverso tra le righe o schema hello si evolve nel tempo, viene automaticamente indicizzato.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-266">Therefore, even if your schema is different between rows, or if hello schema evolves over time, it is automatically indexed.</span></span> <span data-ttu-id="e4f1d-267">Poiché Azure Cosmos DB supporta gli indici secondari automatico, le query su qualsiasi proprietà possono utilizzare l'indice di hello e fornite in modo efficiente.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-267">Since Azure Cosmos DB supports automatic secondary indexes, queries against any property can use hello index and be served efficiently.</span></span>

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

<span data-ttu-id="e4f1d-268">Nell'anteprima di Azure Cosmos DB supporta hello stessa funzionalità dell'archiviazione tabelle di Azure per hello tabella API di query.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-268">In preview, Azure Cosmos DB supports hello same query functionality as Azure Table storage for hello Table API.</span></span> <span data-ttu-id="e4f1d-269">Azure Cosmos DB supporta anche l'ordinamento, le aggregazioni, le query geospaziali, la gerarchia e un'ampia gamma di funzioni predefinite.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-269">Azure Cosmos DB also supports sorting, aggregates, geospatial query, hierarchy, and a wide range of built-in functions.</span></span> <span data-ttu-id="e4f1d-270">funzionalità aggiuntive di Hello verrà fornita in hello API tabelle in un futuro aggiornamento del servizio.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-270">hello additional functionality will be provided in hello Table API in a future service update.</span></span> <span data-ttu-id="e4f1d-271">Vedere [Query in Azure Cosmos DB](documentdb-sql-query.md) per una panoramica di queste funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-271">See [Azure Cosmos DB query](documentdb-sql-query.md) for an overview of these capabilities.</span></span> 

## <a name="replace-an-entity"></a><span data-ttu-id="e4f1d-272">Sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-272">Replace an entity</span></span>
<span data-ttu-id="e4f1d-273">tooupdate un'entità, recuperarlo dal servizio tabelle hello, modificare l'oggetto entità hello e quindi salvare le modifiche apportate hello eseguire il servizio tabelle toohello.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-273">tooupdate an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="e4f1d-274">Hello codice seguente modifica il numero di telefono del cliente esistente.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-274">hello following code changes an existing customer's phone number.</span></span> 

```csharp
TableOperation updateOperation = TableOperation.Replace(updateEntity);
table.Execute(updateOperation);
```
<span data-ttu-id="e4f1d-275">Analogamente, è possibile eseguire operazioni `InsertOrMerge` o `Merge`.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-275">Similarly, you can perform `InsertOrMerge` or `Merge` operations.</span></span>  

## <a name="delete-an-entity"></a><span data-ttu-id="e4f1d-276">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-276">Delete an entity</span></span>
<span data-ttu-id="e4f1d-277">È possibile eliminare un'entità facilmente dopo avere recuperato utilizzando hello stesso modello visualizzato per l'aggiornamento di un'entità.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-277">You can easily delete an entity after you have retrieved it by using hello same pattern shown for updating an entity.</span></span> <span data-ttu-id="e4f1d-278">Hello seguente codice recupera ed elimina un'entità customer.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-278">hello following code retrieves and deletes a customer entity.</span></span>

```csharp
TableOperation deleteOperation = TableOperation.Delete(deleteEntity);
table.Execute(deleteOperation);
```

## <a name="delete-a-table"></a><span data-ttu-id="e4f1d-279">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="e4f1d-279">Delete a table</span></span>
<span data-ttu-id="e4f1d-280">Infine, hello esempio di codice seguente elimina una tabella da un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-280">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="e4f1d-281">È possibile eliminare e ricreare una tabella immediatamente con Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-281">You can delete and recreate a table immediately with Azure Cosmos DB.</span></span>

```csharp
CloudTable table = tableClient.GetTableReference("people");
table.DeleteIfExists();
```

## <a name="clean-up-resources"></a><span data-ttu-id="e4f1d-282">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="e4f1d-282">Clean up resources</span></span> 

<span data-ttu-id="e4f1d-283">Se non si ha intenzione toocontinue toouse questa app, utilizzare hello seguendo i passaggi toodelete tutte le risorse create da questa esercitazione in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-283">If you're not going toocontinue toouse this app, use hello following steps toodelete all resources created by this tutorial in hello Azure portal.</span></span>   

1. <span data-ttu-id="e4f1d-284">Dal menu a sinistra di hello in hello portale di Azure, fare clic su **gruppi di risorse** e quindi fare clic su nome hello della risorsa di hello è stato creato.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-284">From hello left-hand menu in hello Azure portal, click **Resource groups** and then click hello name of hello resource you created.</span></span>  
2. <span data-ttu-id="e4f1d-285">Nella pagina di gruppo di risorse, fare clic su **eliminare**, digitare il nome di hello di hello risorsa toodelete nella casella di testo hello e quindi fare clic su **eliminare**.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-285">On your resource group page, click **Delete**, type hello name of hello resource toodelete in hello text box, and then click **Delete**.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="e4f1d-286">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="e4f1d-286">Next steps</span></span>

<span data-ttu-id="e4f1d-287">In questa esercitazione, trattati come tooget iniziare con Azure Cosmos DB hello tabella API e aver eseguito l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="e4f1d-287">In this tutorial, we covered how tooget started using Azure Cosmos DB with hello Table API, and you've done hello following:</span></span> 

> [!div class="checklist"] 
> * <span data-ttu-id="e4f1d-288">Creazione di un account Azure Cosmos DB</span><span class="sxs-lookup"><span data-stu-id="e4f1d-288">Created an Azure Cosmos DB account</span></span> 
> * <span data-ttu-id="e4f1d-289">Funzionalità abilitata nel file app. config hello</span><span class="sxs-lookup"><span data-stu-id="e4f1d-289">Enabled functionality in hello app.config file</span></span> 
> * <span data-ttu-id="e4f1d-290">Creazione di una tabella</span><span class="sxs-lookup"><span data-stu-id="e4f1d-290">Created a table</span></span> 
> * <span data-ttu-id="e4f1d-291">Aggiunta di una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-291">Added an entity tooa table</span></span> 
> * <span data-ttu-id="e4f1d-292">Inserimento di un batch di entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-292">Inserted a batch of entities</span></span> 
> * <span data-ttu-id="e4f1d-293">Recupero di una singola entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-293">Retrieved a single entity</span></span> 
> * <span data-ttu-id="e4f1d-294">Esecuzione di query di entità tramite indici secondari automatici</span><span class="sxs-lookup"><span data-stu-id="e4f1d-294">Queried entities using automatic secondary indexes</span></span> 
> * <span data-ttu-id="e4f1d-295">Sostituzione di un'entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-295">Replaced an entity</span></span> 
> * <span data-ttu-id="e4f1d-296">Eliminazione di un'entità</span><span class="sxs-lookup"><span data-stu-id="e4f1d-296">Deleted an entity</span></span> 
> * <span data-ttu-id="e4f1d-297">Eliminazione di una tabella</span><span class="sxs-lookup"><span data-stu-id="e4f1d-297">Deleted a table</span></span>  

<span data-ttu-id="e4f1d-298">È possibile continuare l'esercitazione successiva toohello e altre informazioni su come eseguire query di dati della tabella.</span><span class="sxs-lookup"><span data-stu-id="e4f1d-298">You can now proceed toohello next tutorial and learn more about querying table data.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="e4f1d-299">Eseguire una query con hello tabella API</span><span class="sxs-lookup"><span data-stu-id="e4f1d-299">Query with hello Table API</span></span>](tutorial-query-table.md)
