---
title: aaaHow toouse archiviazione tabella (C++) | Documenti Microsoft
description: Archiviare dati strutturati in un cloud di hello tramite l'archiviazione tabelle di Azure, un archivio dati NoSQL.
services: storage
documentationcenter: .net
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: seguler
ms.openlocfilehash: 8eee0031350ab6ff3f76fb288b2f896687aa17a3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-table-storage-from-c"></a><span data-ttu-id="bec1e-103">Come toouse archiviazione tabelle da C++</span><span class="sxs-lookup"><span data-stu-id="bec1e-103">How toouse Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="bec1e-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="bec1e-104">Overview</span></span>
<span data-ttu-id="bec1e-105">Questa guida illustra come gli scenari comuni di tooperform usando hello servizio di archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="bec1e-105">This guide will show you how tooperform common scenarios by using hello Azure Table storage service.</span></span> <span data-ttu-id="bec1e-106">esempi di Hello sono scritti in C++ e utilizzare hello [libreria Client di archiviazione di Azure per C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="bec1e-106">hello samples are written in C++ and use hello [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="bec1e-107">Hello scenari trattati includono **creazione ed eliminazione di una tabella** e **utilizzo delle entità tabella**.</span><span class="sxs-lookup"><span data-stu-id="bec1e-107">hello scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="bec1e-108">Le destinazioni di questa guida hello Azure Storage Client Library per la versione 1.0.0 di C++ e versioni successive.</span><span class="sxs-lookup"><span data-stu-id="bec1e-108">This guide targets hello Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="bec1e-109">Hello consiglia versione libreria di Client di archiviazione 2.2.0, disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="bec1e-109">hello recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="bec1e-110">Creazione di un’applicazione C++</span><span class="sxs-lookup"><span data-stu-id="bec1e-110">Create a C++ application</span></span>
<span data-ttu-id="bec1e-111">In questa guida verranno usate le funzionalità di archiviazione che è possibile eseguire all'interno di un'applicazione C++.</span><span class="sxs-lookup"><span data-stu-id="bec1e-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="bec1e-112">toodo in tal caso, sarà necessario tooinstall hello Azure Storage Client Library per C++ e creare un account di archiviazione di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="bec1e-112">toodo so, you will need tooinstall hello Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="bec1e-113">tooinstall hello Azure Storage Client Library per C++, è possibile utilizzare hello dei seguenti metodi:</span><span class="sxs-lookup"><span data-stu-id="bec1e-113">tooinstall hello Azure Storage Client Library for C++, you can use hello following methods:</span></span>

* <span data-ttu-id="bec1e-114">**Linux:** seguire le istruzioni di hello fornite hello [Azure Storage Client Library per il file README C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) pagina.</span><span class="sxs-lookup"><span data-stu-id="bec1e-114">**Linux:** Follow hello instructions given on hello [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="bec1e-115">**Windows:** in Visual Studio, fare clic su **Strumenti &gt; Gestione pacchetti NuGet &gt; console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="bec1e-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="bec1e-116">Comando che segue di tipo hello in hello [console di gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="bec1e-116">Type hello following command into hello [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="bec1e-117">Install-Package knockoutjs</span><span class="sxs-lookup"><span data-stu-id="bec1e-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-tooaccess-table-storage"></a><span data-ttu-id="bec1e-118">Configurare l'archiviazione tabelle di tooaccess applicazione</span><span class="sxs-lookup"><span data-stu-id="bec1e-118">Configure your application tooaccess Table storage</span></span>
<span data-ttu-id="bec1e-119">Aggiungere i seguenti hello includono hello C++ file in cui tabelle di tooaccess le API di archiviazione di Azure di toouse hello cima toohello istruzioni:</span><span class="sxs-lookup"><span data-stu-id="bec1e-119">Add hello following include statements toohello top of hello C++ file where you want toouse hello Azure storage APIs tooaccess tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="bec1e-120">Impostare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="bec1e-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="bec1e-121">Un client di archiviazione di Azure Usa un endpoint di toostore stringa di connessione archiviazione e le credenziali per l'accesso a servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="bec1e-121">An Azure storage client uses a storage connection string toostore endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="bec1e-122">Quando si esegue un'applicazione client, è necessario fornire una stringa di connessione di archiviazione hello nel seguente formato hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-122">When running a client application, you must provide hello storage connection string in hello following format.</span></span> <span data-ttu-id="bec1e-123">Utilizza il nome di hello dell'archiviazione hello e account di archiviazione chiave di accesso per account di archiviazione hello elencati in hello [portale Azure](https://portal.azure.com) per hello *AccountName* e *AccountKey* valori.</span><span class="sxs-lookup"><span data-stu-id="bec1e-123">Use hello name of your storage account and hello storage access key for hello storage account listed in hello [Azure Portal](https://portal.azure.com) for hello *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="bec1e-124">Per informazioni sugli account di archiviazione e sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="bec1e-124">For information on storage accounts and access keys, see [About Azure storage accounts](storage-create-storage-account.md).</span></span> <span data-ttu-id="bec1e-125">In questo esempio viene illustrato come dichiarare una stringa di connessione di un campo statico toohold hello:</span><span class="sxs-lookup"><span data-stu-id="bec1e-125">This example shows how you can declare a static field toohold hello connection string:</span></span>  

```cpp
// Define hello connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="bec1e-126">tootest l'applicazione in computer basati su Windows locale, è possibile utilizzare hello Azure [emulatore di archiviazione](storage-use-emulator.md) che viene installato con hello [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bec1e-126">tootest your application in your local Windows-based computer, you can use hello Azure [storage emulator](storage-use-emulator.md) that is installed with hello [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="bec1e-127">emulatore di archiviazione Hello è un'utilità che simula hello Azure Blob, coda e tabella servizi disponibili nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="bec1e-127">hello storage emulator is a utility that simulates hello Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="bec1e-128">Hello esempio seguente viene illustrato come è possibile dichiarare un emulatore di archiviazione locale di un campo statico toohold hello connessione stringa tooyour:</span><span class="sxs-lookup"><span data-stu-id="bec1e-128">hello following example shows how you can declare a static field toohold hello connection string tooyour local storage emulator:</span></span>  

```cpp
// Define hello connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="bec1e-129">toostart hello emulatore di archiviazione di Azure, fare clic su hello **avviare** o preme tasto di Windows hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-129">toostart hello Azure storage emulator, click hello **Start** button or press hello Windows key.</span></span> <span data-ttu-id="bec1e-130">Iniziare a digitare **emulatore di archiviazione Azure**, quindi selezionare **emulatore di archiviazione di Microsoft Azure** elenco hello di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="bec1e-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from hello list of applications.</span></span>  

<span data-ttu-id="bec1e-131">Hello negli esempi seguenti si presuppongono che si usa uno di questi due metodi tooget hello stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="bec1e-131">hello following samples assume that you have used one of these two methods tooget hello storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="bec1e-132">Recuperare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="bec1e-132">Retrieve your connection string</span></span>
<span data-ttu-id="bec1e-133">È possibile utilizzare hello **cloud_storage_account** classe toorepresent le informazioni sull'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bec1e-133">You can use hello **cloud_storage_account** class toorepresent your storage account information.</span></span> <span data-ttu-id="bec1e-134">tooretrieve informazioni dalla stringa di connessione di archiviazione hello dell'account di archiviazione, è possibile utilizzare il metodo di analisi hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-134">tooretrieve your storage account information from hello storage connection string, you can use hello parse method.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="bec1e-135">Quindi, ottenere un riferimento tooa **cloud_table_client** classe, consente di ottenere gli oggetti di riferimento per le tabelle e le entità archiviate all'interno di hello servizio di archiviazione tabelle.</span><span class="sxs-lookup"><span data-stu-id="bec1e-135">Next, get a reference tooa **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within hello Table storage service.</span></span> <span data-ttu-id="bec1e-136">Hello codice seguente viene creata una **cloud_table_client** oggetto utilizzando l'oggetto account di archiviazione hello è recuperato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="bec1e-136">hello following code creates a **cloud_table_client** object by using hello storage account object we retrieved above:</span></span>  

```cpp
// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="bec1e-137">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="bec1e-137">Create a table</span></span>
<span data-ttu-id="bec1e-138">L'oggetto **cloud_table_client** consente di ottenere oggetti di riferimento per tabelle ed entità.</span><span class="sxs-lookup"><span data-stu-id="bec1e-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="bec1e-139">Hello codice seguente viene creata una **cloud_table_client** dell'oggetto e lo usa toocreate una nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="bec1e-139">hello following code creates a **cloud_table_client** object and uses it toocreate a new table.</span></span>

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="bec1e-140">Aggiungere una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="bec1e-140">Add an entity tooa table</span></span>
<span data-ttu-id="bec1e-141">creare una nuova tabella tooa un'entità, tooadd **table_entity** e passarlo troppo**table_operation:: insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="bec1e-141">tooadd an entity tooa table, create a new **table_entity** object and pass it too**table_operation::insert_entity**.</span></span> <span data-ttu-id="bec1e-142">Hello codice seguente Usa nome hello del cliente come chiave di riga hello e last name come chiave di partizione hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-142">hello following code uses hello customer's first name as hello row key and last name as hello partition key.</span></span> <span data-ttu-id="bec1e-143">Insieme, di partizione e chiave di riga identificano entità hello nella tabella di hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-143">Together, an entity's partition and row key uniquely identify hello entity in hello table.</span></span> <span data-ttu-id="bec1e-144">Le entità con hello stessa chiave di partizione è possibile eseguire query più velocemente rispetto a quelle con diverse chiavi di partizione, ma con le chiavi di partizione diverse consente una maggiore scalabilità operazione parallela.</span><span class="sxs-lookup"><span data-stu-id="bec1e-144">Entities with hello same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="bec1e-145">Per altre informazioni, vedere [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="bec1e-145">For more information, see [Microsoft Azure storage performance and scalability checklist](storage-performance-checklist.md).</span></span>

<span data-ttu-id="bec1e-146">Hello codice seguente viene creata una nuova istanza della **table_entity** con alcuni toobe dati cliente archiviati.</span><span class="sxs-lookup"><span data-stu-id="bec1e-146">hello following code creates a new instance of **table_entity** with some customer data toobe stored.</span></span> <span data-ttu-id="bec1e-147">Hello successiva chiama codice **table_operation:: insert_entity** toocreate un **table_operation** tooinsert un'entità dell'oggetto in una tabella, e associa hello nuova entità di tabella con esso.</span><span class="sxs-lookup"><span data-stu-id="bec1e-147">hello code next calls **table_operation::insert_entity** toocreate a **table_operation** object tooinsert an entity into a table, and associates hello new table entity with it.</span></span> <span data-ttu-id="bec1e-148">Infine, chiama codice hello hello eseguire il metodo su hello **cloud_table** oggetto.</span><span class="sxs-lookup"><span data-stu-id="bec1e-148">Finally, hello code calls hello execute method on hello **cloud_table** object.</span></span> <span data-ttu-id="bec1e-149">Nuovo hello e **table_operation** invia un toohello richiesta tabella servizio tooinsert hello nuova entità cliente nella tabella "persone" hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-149">And hello new **table_operation** sends a request toohello Table service tooinsert hello new customer entity into hello "people" table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference tooa table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create hello table operation that inserts hello customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute hello insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="bec1e-150">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="bec1e-150">Insert a batch of entities</span></span>
<span data-ttu-id="bec1e-151">È possibile inserire un batch di entità toohello del servizio tabelle in un'unica operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="bec1e-151">You can insert a batch of entities toohello Table service in one write operation.</span></span> <span data-ttu-id="bec1e-152">Hello codice seguente viene creata una **table_batch_operation** e quindi aggiunge tre tooit operazioni di inserimento.</span><span class="sxs-lookup"><span data-stu-id="bec1e-152">hello following code creates a **table_batch_operation** object, and then adds three insert operations tooit.</span></span> <span data-ttu-id="bec1e-153">Ogni operazione di inserimento viene aggiunto tramite la creazione di un nuovo oggetto entità, impostarne i valori e chiamando quindi hello insert (metodo) su hello **table_batch_operation** entità hello tooassociate di oggetto con una nuova operazione di inserimento.</span><span class="sxs-lookup"><span data-stu-id="bec1e-153">Each insert operation is added by creating a new entity object, setting its values, and then calling hello insert method on hello **table_batch_operation** object tooassociate hello entity with a new insert operation.</span></span> <span data-ttu-id="bec1e-154">Quindi, **cloud_table.execute** viene chiamato l'operazione di hello tooexecute.</span><span class="sxs-lookup"><span data-stu-id="bec1e-154">Then, **cloud_table.execute** is called tooexecute hello operation.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it toohello table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it toohello table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity tooadd toohello table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities toohello batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute hello batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="bec1e-155">Toonote alcune operazioni per le operazioni batch:</span><span class="sxs-lookup"><span data-stu-id="bec1e-155">Some things toonote on batch operations:</span></span>  

* <span data-ttu-id="bec1e-156">È possibile eseguire backup too100 insert, delete, merge, replace, insert o merge e inserire o sostituire operazioni in qualsiasi combinazione in un unico batch.</span><span class="sxs-lookup"><span data-stu-id="bec1e-156">You can perform up too100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="bec1e-157">Un'operazione batch può avere un'operazione di recupero, se è l'unica operazione di hello in batch hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-157">A batch operation can have a retrieve operation, if it is hello only operation in hello batch.</span></span>  
* <span data-ttu-id="bec1e-158">Tutte le entità in una singola operazione batch devono avere hello stessa chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="bec1e-158">All entities in a single batch operation must have hello same partition key.</span></span>  
* <span data-ttu-id="bec1e-159">Un'operazione batch è limitato tooa payload dei dati di 4 MB.</span><span class="sxs-lookup"><span data-stu-id="bec1e-159">A batch operation is limited tooa 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="bec1e-160">Recuperare tutte le entità di una partizione</span><span class="sxs-lookup"><span data-stu-id="bec1e-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="bec1e-161">tooquery una tabella per tutte le entità in una partizione, utilizzare un **table_query** oggetto.</span><span class="sxs-lookup"><span data-stu-id="bec1e-161">tooquery a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="bec1e-162">Hello esempio di codice seguente specifica un filtro per le entità in cui la chiave di partizione hello 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="bec1e-162">hello following code example specifies a filter for entities where 'Smith' is hello partition key.</span></span> <span data-ttu-id="bec1e-163">In questo esempio visualizza i campi di ogni entità nella console di toohello risultati query hello hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-163">This example prints hello fields of each entity in hello query results toohello console.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct hello query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print hello fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="bec1e-164">query Hello in questo esempio visualizza tutte le entità hello che soddisfano i criteri di filtro hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-164">hello query in this example brings all hello entities that match hello filter criteria.</span></span> <span data-ttu-id="bec1e-165">Se si dispongono di tabelle di grandi dimensioni e le entità di tabella hello toodownload spesso, è consigliabile archiviare i dati nei blob di archiviazione di Azure invece.</span><span class="sxs-lookup"><span data-stu-id="bec1e-165">If you have large tables and need toodownload hello table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="bec1e-166">Recuperare un intervallo di entità in una partizione</span><span class="sxs-lookup"><span data-stu-id="bec1e-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="bec1e-167">Se non si desidera tooquery tutte le entità hello in una partizione, è possibile specificare un intervallo mediante la combinazione di filtri chiave di partizione hello con un filtro di riga di chiave.</span><span class="sxs-lookup"><span data-stu-id="bec1e-167">If you don't want tooquery all hello entities in a partition, you can specify a range by combining hello partition key filter with a row key filter.</span></span> <span data-ttu-id="bec1e-168">Hello esempio di codice seguente usa due filtri tooget tutte le entità nella partizione "Smith" in cui la chiave di riga hello (nome) inizia con una lettera precedente a 'E' alfabeto hello e quindi Visualizza i risultati della query hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-168">hello following code example uses two filters tooget all entities in partition 'Smith' where hello row key (first name) starts with a letter earlier than 'E' in hello alphabet and then prints hello query results.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create hello table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through hello results, displaying information about hello entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="bec1e-169">Recuperare una singola entità</span><span class="sxs-lookup"><span data-stu-id="bec1e-169">Retrieve a single entity</span></span>
<span data-ttu-id="bec1e-170">È possibile scrivere un tooretrieve query un'entità singola e specifica.</span><span class="sxs-lookup"><span data-stu-id="bec1e-170">You can write a query tooretrieve a single, specific entity.</span></span> <span data-ttu-id="bec1e-171">codice Hello seguente usa **table_operation:: retrieve_entity** cliente hello toospecify "Jeff Smith".</span><span class="sxs-lookup"><span data-stu-id="bec1e-171">hello following code uses **table_operation::retrieve_entity** toospecify hello customer 'Jeff Smith'.</span></span> <span data-ttu-id="bec1e-172">Questo metodo restituisce una sola entità, anziché una raccolta e hello valore restituito è **table_result**.</span><span class="sxs-lookup"><span data-stu-id="bec1e-172">This method returns just one entity, rather than a collection, and hello returned value is in **table_result**.</span></span> <span data-ttu-id="bec1e-173">Specifica le chiavi di partizione e di riga in una query è tooretrieve modo più veloce di hello una singola entità dal servizio tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-173">Specifying both partition and row keys in a query is hello fastest way tooretrieve a single entity from hello Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output hello entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="bec1e-174">Sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="bec1e-174">Replace an entity</span></span>
<span data-ttu-id="bec1e-175">tooreplace un'entità, recuperarlo dal servizio tabelle hello, modificare l'oggetto entità hello e quindi salvare le modifiche apportate hello eseguire il servizio tabelle toohello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-175">tooreplace an entity, retrieve it from hello Table service, modify hello entity object, and then save hello changes back toohello Table service.</span></span> <span data-ttu-id="bec1e-176">Hello codice riportato di seguito modifica indirizzo di posta elettronica e il numero di telefono del cliente esistente.</span><span class="sxs-lookup"><span data-stu-id="bec1e-176">hello following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="bec1e-177">Anziché chiamare **table_operation:: insert_entity**, in questo codice viene usato **table_operation:: replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="bec1e-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="bec1e-178">In questo modo hello entità toobe completamente sostituito nel server di hello, a meno che l'entità di hello sul server hello è stato modificato dopo che è stata recuperata, nel qual caso hello operazione non riuscirà.</span><span class="sxs-lookup"><span data-stu-id="bec1e-178">This causes hello entity toobe fully replaced on hello server, unless hello entity on hello server has changed since it was retrieved, in which case hello operation will fail.</span></span> <span data-ttu-id="bec1e-179">Questo errore è tooprevent l'applicazione di sovrascrivere accidentalmente una modifica apportata tra hello il recupero e l'aggiornamento da un altro componente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="bec1e-179">This failure is tooprevent your application from inadvertently overwriting a change made between hello retrieval and update by another component of your application.</span></span> <span data-ttu-id="bec1e-180">Hello la corretta gestione di questo errore è tooretrieve hello entità nuovamente, apportare le modifiche (se è ancora valida) e quindi eseguire un altro **table_operation:: replace_entity** operazione.</span><span class="sxs-lookup"><span data-stu-id="bec1e-180">hello proper handling of this failure is tooretrieve hello entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="bec1e-181">Nella sezione successiva Hello viene illustrato come toooverride questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="bec1e-181">hello next section will show you how toooverride this behavior.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation tooreplace hello entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="bec1e-182">Inserire o sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="bec1e-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="bec1e-183">**table_operation:: replace_entity** operazioni hanno esito negativo se l'entità hello è stato modificato dopo che è stata recuperata dal server hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-183">**table_operation::replace_entity** operations will fail if hello entity has been changed since it was retrieved from hello server.</span></span> <span data-ttu-id="bec1e-184">Inoltre, è necessario recuperare entità hello dal server hello prima in ordine per **table_operation:: replace_entity** toobe ha esito positivo.</span><span class="sxs-lookup"><span data-stu-id="bec1e-184">Furthermore, you must retrieve hello entity from hello server first in order for **table_operation::replace_entity** toobe successful.</span></span> <span data-ttu-id="bec1e-185">In alcuni casi, tuttavia, non si conosce se entità hello esista nel server di hello e i valori correnti di hello in essa archiviati sono irrilevanti, ovvero l'aggiornamento deve sovrascrivere tutti.</span><span class="sxs-lookup"><span data-stu-id="bec1e-185">Sometimes, however, you don't know if hello entity exists on hello server and hello current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="bec1e-186">tooaccomplish, si utilizzerebbe un **table_operation:: insert_or_replace_entity** operazione.</span><span class="sxs-lookup"><span data-stu-id="bec1e-186">tooaccomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="bec1e-187">Questa operazione inserisce l'entità di hello se non esiste oppure lo sostituisce in caso affermativo, indipendentemente dal fatto se hello ultimo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="bec1e-187">This operation inserts hello entity if it doesn't exist, or replaces it if it does, regardless of when hello last update was made.</span></span> <span data-ttu-id="bec1e-188">Nell'esempio di codice seguente di hello, entità customer hello per Jeff Smith viene ancora recuperato, ma viene quindi salvato server back-toohello tramite **table_operation:: insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="bec1e-188">In hello following code example, hello customer entity for Jeff Smith is still retrieved, but it is then saved back toohello server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="bec1e-189">Gli aggiornamenti effettuati toohello entità di operazione di aggiornamento e recupero hello verranno sovrascritto.</span><span class="sxs-lookup"><span data-stu-id="bec1e-189">Any updates made toohello entity between hello retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation tooinsert-or-replace hello entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit hello operation toohello Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="bec1e-190">Eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="bec1e-190">Query a subset of entity properties</span></span>
<span data-ttu-id="bec1e-191">Una tabella di tooa query è possibile recuperare solo alcune proprietà di un'entità.</span><span class="sxs-lookup"><span data-stu-id="bec1e-191">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="bec1e-192">query nel seguente codice hello Hello utilizza hello **table_query:: set_select_columns** metodo tooreturn solo hello indirizzi di posta elettronica di entità nella tabella hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-192">hello query in hello following code uses hello **table_query::set_select_columns** method tooreturn only hello email addresses of entities in hello table.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define hello query, and select only hello Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute hello query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display hello results.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key();

    const azure::storage::table_entity::properties_type& properties = it->properties();
    for (auto prop_it = properties.begin(); prop_it != properties.end(); ++prop_it)
    {
        std::wcout << ", " << prop_it->first << ": " << prop_it->second.str();
    }

    std::wcout << std::endl;
}
```

> [!NOTE]
> <span data-ttu-id="bec1e-193">L'esecuzione di una query di alcune proprietà di un'entità è un'operazione più efficiente rispetto al recupero di tutte le proprietà.</span><span class="sxs-lookup"><span data-stu-id="bec1e-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="bec1e-194">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="bec1e-194">Delete an entity</span></span>
<span data-ttu-id="bec1e-195">È possibile eliminare facilmente un'entità dopo averla recuperata.</span><span class="sxs-lookup"><span data-stu-id="bec1e-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="bec1e-196">Una volta recuperato entità hello, chiamare **table_operation:: delete_entity** con toodelete entità hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-196">Once hello entity is retrieved, call **table_operation::delete_entity** with hello entity toodelete.</span></span> <span data-ttu-id="bec1e-197">Chiamare quindi hello **cloud_table.execute** metodo.</span><span class="sxs-lookup"><span data-stu-id="bec1e-197">Then call hello **cloud_table.execute** method.</span></span> <span data-ttu-id="bec1e-198">Hello codice seguente recupera ed elimina un'entità con una chiave di partizione "Smith" e una chiave di riga di "Jeff".</span><span class="sxs-lookup"><span data-stu-id="bec1e-198">hello following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="bec1e-199">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="bec1e-199">Delete a table</span></span>
<span data-ttu-id="bec1e-200">Infine, hello esempio di codice seguente elimina una tabella da un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="bec1e-200">Finally, hello following code example deletes a table from a storage account.</span></span> <span data-ttu-id="bec1e-201">Una tabella in cui è stata eliminata, sarà disponibile toobe ricreati per un periodo di tempo dopo l'eliminazione di hello.</span><span class="sxs-lookup"><span data-stu-id="bec1e-201">A table that has been deleted will be unavailable toobe re-created for a period of time following hello deletion.</span></span>  

```cpp
// Retrieve hello storage account from hello connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create hello table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for hello table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation tooretrieve hello entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation toodelete hello entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit hello delete operation toohello Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="bec1e-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="bec1e-202">Next steps</span></span>
<span data-ttu-id="bec1e-203">Ora che si sono appreso i concetti fondamentali di hello dell'archiviazione tabelle, seguire questi toolearn collegamenti ulteriori informazioni sull'archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="bec1e-203">Now that you've learned hello basics of table storage, follow these links toolearn more about Azure Storage:</span></span>  

* <span data-ttu-id="bec1e-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="bec1e-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="bec1e-205">Come toouse archiviazione Blob da C++</span><span class="sxs-lookup"><span data-stu-id="bec1e-205">How toouse Blob storage from C++</span></span>](storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="bec1e-206">Come toouse l'archiviazione delle code da C++</span><span class="sxs-lookup"><span data-stu-id="bec1e-206">How toouse Queue storage from C++</span></span>](storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="bec1e-207">Elenco delle risorse di archiviazione di Azure in C++</span><span class="sxs-lookup"><span data-stu-id="bec1e-207">List Azure Storage resources in C++</span></span>](storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="bec1e-208">Informazioni di riferimento sulla libreria client di archiviazione per C++</span><span class="sxs-lookup"><span data-stu-id="bec1e-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="bec1e-209">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="bec1e-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
