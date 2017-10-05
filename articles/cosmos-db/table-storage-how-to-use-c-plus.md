---
title: Come usare l'archiviazione tabelle (C++) | Microsoft Docs
description: Archiviare dati non strutturati nel cloud con il servizio di archiviazione tabelle di Azure, ovvero un archivio dati NoSQL.
services: cosmos-db
documentationcenter: .net
author: mimig1
manager: jahogg
editor: tysonn
ms.assetid: f191f308-e4b2-4de9-85cb-551b82b1ea7c
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/28/2017
ms.author: mimig
ms.openlocfilehash: 8314292cdb9b7a3f464c60119ed10f6b06ed4d10
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-table-storage-from-c"></a><span data-ttu-id="8a9e1-103">Come usare l'archiviazione tabelle da C++</span><span class="sxs-lookup"><span data-stu-id="8a9e1-103">How to use Table storage from C++</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="8a9e1-104">Overview</span><span class="sxs-lookup"><span data-stu-id="8a9e1-104">Overview</span></span>
<span data-ttu-id="8a9e1-105">In questa guida sono illustrati diversi scenari di utilizzo comuni del servizio di archiviazione tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-105">This guide will show you how to perform common scenarios by using the Azure Table storage service.</span></span> <span data-ttu-id="8a9e1-106">Gli esempi sono scritti in C++ e utilizzano la [libreria client di Archiviazione di Azure per C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span><span class="sxs-lookup"><span data-stu-id="8a9e1-106">The samples are written in C++ and use the [Azure Storage Client Library for C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md).</span></span> <span data-ttu-id="8a9e1-107">Gli scenari presentati includono **creazione ed eliminazione di una tabella** e **uso di entità di tabella**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-107">The scenarios covered include **creating and deleting a table** and **working with table entities**.</span></span>

> [!NOTE]
> <span data-ttu-id="8a9e1-108">Questa guida fa riferimento alla libreria client di Archiviazione di Azure per C++ versione 1.0.0 e successive.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-108">This guide targets the Azure Storage Client Library for C++ version 1.0.0 and above.</span></span> <span data-ttu-id="8a9e1-109">La versione consigliata per la libreria client di archiviazione è la 2.2.0, disponibile tramite [NuGet](http://www.nuget.org/packages/wastorage) o [GitHub](https://github.com/Azure/azure-storage-cpp/).</span><span class="sxs-lookup"><span data-stu-id="8a9e1-109">The recommended version is Storage Client Library 2.2.0, which is available via [NuGet](http://www.nuget.org/packages/wastorage) or [GitHub](https://github.com/Azure/azure-storage-cpp/).</span></span>
> 
> 

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-c-application"></a><span data-ttu-id="8a9e1-110">Creazione di un’applicazione C++</span><span class="sxs-lookup"><span data-stu-id="8a9e1-110">Create a C++ application</span></span>
<span data-ttu-id="8a9e1-111">In questa guida verranno usate le funzionalità di archiviazione che è possibile eseguire all'interno di un'applicazione C++.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-111">In this guide, you will use storage features that can be run within a C++ application.</span></span> <span data-ttu-id="8a9e1-112">A tal fine, sarà necessario installare la libreria client di Archiviazione di Azure per C++ e creare un account di archiviazione Azure nella propria sottoscrizione Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-112">To do so, you will need to install the Azure Storage Client Library for C++ and create an Azure storage account in your Azure subscription.</span></span>  

<span data-ttu-id="8a9e1-113">Per installare la libreria client di Archiviazione di Azure per C++, è possibile utilizzare i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="8a9e1-113">To install the Azure Storage Client Library for C++, you can use the following methods:</span></span>

* <span data-ttu-id="8a9e1-114">**Linux:** seguire le istruzioni fornite nella pagina relativa al [README della libreria client di Archiviazione di Azure per C++](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) .</span><span class="sxs-lookup"><span data-stu-id="8a9e1-114">**Linux:** Follow the instructions given on the [Azure Storage Client Library for C++ README](https://github.com/Azure/azure-storage-cpp/blob/master/README.md) page.</span></span>  
* <span data-ttu-id="8a9e1-115">**Windows:** in Visual Studio, fare clic su **Strumenti > Gestione pacchetti NuGet > console di Gestione pacchetti**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-115">**Windows:** In Visual Studio, click **Tools > NuGet Package Manager > Package Manager Console**.</span></span> <span data-ttu-id="8a9e1-116">Digitare il comando seguente nella [console Gestione pacchetti NuGet](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) e premere INVIO.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-116">Type the following command into the [NuGet Package Manager console](http://docs.nuget.org/docs/start-here/using-the-package-manager-console) and press Enter.</span></span>  
  
     <span data-ttu-id="8a9e1-117">Install-Package knockoutjs</span><span class="sxs-lookup"><span data-stu-id="8a9e1-117">Install-Package wastorage</span></span>

## <a name="configure-your-application-to-access-table-storage"></a><span data-ttu-id="8a9e1-118">Configurare l'applicazione per l'accesso all'archiviazione tabelle</span><span class="sxs-lookup"><span data-stu-id="8a9e1-118">Configure your application to access Table storage</span></span>
<span data-ttu-id="8a9e1-119">Aggiungere le istruzioni include seguenti all'inizio del file C++ in cui si desidera utilizzare le API di archiviazione di Azure per accedere alle tabelle:</span><span class="sxs-lookup"><span data-stu-id="8a9e1-119">Add the following include statements to the top of the C++ file where you want to use the Azure storage APIs to access tables:</span></span>  

```cpp
#include <was/storage_account.h>
#include <was/table.h>
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="8a9e1-120">Impostare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8a9e1-120">Set up an Azure storage connection string</span></span>
<span data-ttu-id="8a9e1-121">I client di archiviazione di Azure usano le stringhe di connessione di archiviazione per archiviare endpoint e credenziali per l'accesso ai servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-121">An Azure storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="8a9e1-122">Quando si esegue un'applicazione client, è necessario specificare la stringa di connessione di archiviazione nel formato seguente.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-122">When running a client application, you must provide the storage connection string in the following format.</span></span> <span data-ttu-id="8a9e1-123">Usare il nome del proprio account di archiviazione e la chiave di accesso alle risorse di archiviazione indicata nel [portale di Azure](https://portal.azure.com) per i valori *AccountName* e *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-123">Use the name of your storage account and the storage access key for the storage account listed in the [Azure Portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="8a9e1-124">Per informazioni sugli account di archiviazione e sulle chiavi di accesso, vedere [Informazioni sugli account di archiviazione di Azure](../storage/common/storage-create-storage-account.md).</span><span class="sxs-lookup"><span data-stu-id="8a9e1-124">For information on storage accounts and access keys, see [About Azure storage accounts](../storage/common/storage-create-storage-account.md).</span></span> <span data-ttu-id="8a9e1-125">In questo esempio viene illustrato come dichiarare un campo statico per memorizzare la stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="8a9e1-125">This example shows how you can declare a static field to hold the connection string:</span></span>  

```cpp
// Define the connection string with your values.
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;AccountName=your_storage_account;AccountKey=your_storage_account_key"));
```

<span data-ttu-id="8a9e1-126">Per testare l'applicazione nel proprio computer Windows locale, è possibile usare l'[emulatore di archiviazione](../storage/common/storage-use-emulator.md) di Azure che viene installato con [Azure SDK](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="8a9e1-126">To test your application in your local Windows-based computer, you can use the Azure [storage emulator](../storage/common/storage-use-emulator.md) that is installed with the [Azure SDK](https://azure.microsoft.com/downloads/).</span></span> <span data-ttu-id="8a9e1-127">L'emulatore di archiviazione è un'utilità che simula i servizi BLOB, tabelle e di accodamento di Azure nel computer di sviluppo locale.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-127">The storage emulator is a utility that simulates the Azure Blob, Queue, and Table services available on your local development machine.</span></span> <span data-ttu-id="8a9e1-128">Nell’esempio seguente viene illustrato come dichiarare un campo statico per memorizzare la stringa di connessione all’emulatore di archiviazione locale:</span><span class="sxs-lookup"><span data-stu-id="8a9e1-128">The following example shows how you can declare a static field to hold the connection string to your local storage emulator:</span></span>  

```cpp
// Define the connection string with Azure storage emulator.
const utility::string_t storage_connection_string(U("UseDevelopmentStorage=true;"));  
```

<span data-ttu-id="8a9e1-129">Per avviare l'emulatore di archiviazione di Azure, fare clic sul pulsante **Start** o premere il tasto WINDOWS.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-129">To start the Azure storage emulator, click the **Start** button or press the Windows key.</span></span> <span data-ttu-id="8a9e1-130">Iniziare a digitare **Emulatore di archiviazione di Azure** e quindi selezionare **Emulatore di archiviazione di Microsoft Azure** nell'elenco di applicazioni.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-130">Begin typing **Azure Storage Emulator**, and then select **Microsoft Azure Storage Emulator** from the list of applications.</span></span>  

<span data-ttu-id="8a9e1-131">Gli esempi seguenti presumono che sia stato usato uno di questi due metodi per ottenere la stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-131">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>  

## <a name="retrieve-your-connection-string"></a><span data-ttu-id="8a9e1-132">Recuperare la stringa di connessione</span><span class="sxs-lookup"><span data-stu-id="8a9e1-132">Retrieve your connection string</span></span>
<span data-ttu-id="8a9e1-133">Per visualizzare le informazioni dell'account di archiviazione, è possibile usare la classe **cloud_storage_account**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-133">You can use the **cloud_storage_account** class to represent your storage account information.</span></span> <span data-ttu-id="8a9e1-134">Per recuperare le informazioni sull'account di archiviazione dalla stringa di connessione alla risorsa di archiviazione, è possibile utilizzare il metodo parse.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-134">To retrieve your storage account information from the storage connection string, you can use the parse method.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);
```

<span data-ttu-id="8a9e1-135">Ottenere quindi un riferimento a una classe **cloud_table_client** poiché consente di ottenere gli oggetti di riferimento per le tabelle e le entità archiviate all'interno del servizio di archiviazione tabelle.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-135">Next, get a reference to a **cloud_table_client** class, as it lets you get reference objects for tables and entities stored within the Table storage service.</span></span> <span data-ttu-id="8a9e1-136">Il codice seguente crea un oggetto **cloud_table_client** usando l'oggetto account di archiviazione recuperato in precedenza:</span><span class="sxs-lookup"><span data-stu-id="8a9e1-136">The following code creates a **cloud_table_client** object by using the storage account object we retrieved above:</span></span>  

```cpp
// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();
```

## <a name="create-a-table"></a><span data-ttu-id="8a9e1-137">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="8a9e1-137">Create a table</span></span>
<span data-ttu-id="8a9e1-138">L'oggetto **cloud_table_client** consente di ottenere oggetti di riferimento per tabelle ed entità.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-138">A **cloud_table_client** object lets you get reference objects for tables and entities.</span></span> <span data-ttu-id="8a9e1-139">Il codice seguente consente di creare un oggetto **cloud_table_client** e di usarlo per creare una nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-139">The following code creates a **cloud_table_client** object and uses it to create a new table.</span></span>

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);  

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();  
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="8a9e1-140">Aggiungere un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="8a9e1-140">Add an entity to a table</span></span>
<span data-ttu-id="8a9e1-141">Per aggiungere un'entità a una tabella, creare un nuovo oggetto **table_entity** e passarlo a **table_operation::insert_entity**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-141">To add an entity to a table, create a new **table_entity** object and pass it to **table_operation::insert_entity**.</span></span> <span data-ttu-id="8a9e1-142">Nel codice seguente il nome del cliente viene utilizzato come chiave di riga e il cognome come chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-142">The following code uses the customer's first name as the row key and last name as the partition key.</span></span> <span data-ttu-id="8a9e1-143">La combinazione della chiave di riga e della chiave di partizione di un'entità consentono di identificare in modo univoco l'entità nella tabella.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-143">Together, an entity's partition and row key uniquely identify the entity in the table.</span></span> <span data-ttu-id="8a9e1-144">Le query su entità con la stessa chiave di partizione vengono eseguite più rapidamente di quelle con chiavi di partizione diverse, tuttavia l'utilizzo di chiavi di partizione diverse assicura una maggiore scalabilità in caso di operazioni parallele.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-144">Entities with the same partition key can be queried faster than those with different partition keys, but using diverse partition keys allows for greater parallel operation scalability.</span></span> <span data-ttu-id="8a9e1-145">Per altre informazioni, vedere [Elenco di controllo di prestazioni e scalabilità per Archiviazione di Microsoft Azure](../storage/common/storage-performance-checklist.md).</span><span class="sxs-lookup"><span data-stu-id="8a9e1-145">For more information, see [Microsoft Azure storage performance and scalability checklist](../storage/common/storage-performance-checklist.md).</span></span>

<span data-ttu-id="8a9e1-146">Il codice seguente consente di creare una nuova istanza della classe **table_entity** con alcuni dati del cliente da memorizzare.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-146">The following code creates a new instance of **table_entity** with some customer data to be stored.</span></span> <span data-ttu-id="8a9e1-147">Il codice quindi chiama **table_operation::insert_entity** per creare un oggetto **table_operation** per inserire un'entità in una tabella e associa la nuova entità di tabella all'oggetto.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-147">The code next calls **table_operation::insert_entity** to create a **table_operation** object to insert an entity into a table, and associates the new table entity with it.</span></span> <span data-ttu-id="8a9e1-148">Infine, il codice chiama il metodo execute sull'oggetto **cloud_table**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-148">Finally, the code calls the execute method on the **cloud_table** object.</span></span> <span data-ttu-id="8a9e1-149">Il nuovo oggetto **table_operation** invia una richiesta al servizio tabelle per inserire la nuova entità cliente nella tabella "people".</span><span class="sxs-lookup"><span data-stu-id="8a9e1-149">And the new **table_operation** sends a request to the Table service to insert the new customer entity into the "people" table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Retrieve a reference to a table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table if it doesn't exist.
table.create_if_not_exists();

// Create a new customer entity.
azure::storage::table_entity customer1(U("Harp"), U("Walter"));

azure::storage::table_entity::properties_type& properties = customer1.properties();
properties.reserve(2);
properties[U("Email")] = azure::storage::entity_property(U("Walter@contoso.com"));

properties[U("Phone")] = azure::storage::entity_property(U("425-555-0101"));

// Create the table operation that inserts the customer entity.
azure::storage::table_operation insert_operation = azure::storage::table_operation::insert_entity(customer1);

// Execute the insert operation.
azure::storage::table_result insert_result = table.execute(insert_operation);
```

## <a name="insert-a-batch-of-entities"></a><span data-ttu-id="8a9e1-150">Inserire un batch di entità</span><span class="sxs-lookup"><span data-stu-id="8a9e1-150">Insert a batch of entities</span></span>
<span data-ttu-id="8a9e1-151">Per inserire un batch di entità nel servizio tabelle, è possibile usare un'unica operazione di scrittura.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-151">You can insert a batch of entities to the Table service in one write operation.</span></span> <span data-ttu-id="8a9e1-152">Il codice seguente crea un oggetto **table_batch_operation** e quindi vi aggiunge tre operazioni di inserimento.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-152">The following code creates a **table_batch_operation** object, and then adds three insert operations to it.</span></span> <span data-ttu-id="8a9e1-153">Ciascuna operazione di inserimento viene aggiunta creando un nuovo oggetto entità, impostandone i valori, quindi chiamando il metodo insert sull'oggetto **table_batch_operation** per associare l'entità a una nuova operazione di inserimento.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-153">Each insert operation is added by creating a new entity object, setting its values, and then calling the insert method on the **table_batch_operation** object to associate the entity with a new insert operation.</span></span> <span data-ttu-id="8a9e1-154">Per eseguire l'operazione, viene quindi chiamato **cloud_table.execute**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-154">Then, **cloud_table.execute** is called to execute the operation.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define a batch operation.
azure::storage::table_batch_operation batch_operation;

// Create a customer entity and add it to the table.
azure::storage::table_entity customer1(U("Smith"), U("Jeff"));

azure::storage::table_entity::properties_type& properties1 = customer1.properties();
properties1.reserve(2);
properties1[U("Email")] = azure::storage::entity_property(U("Jeff@contoso.com"));
properties1[U("Phone")] = azure::storage::entity_property(U("425-555-0104"));

// Create another customer entity and add it to the table.
azure::storage::table_entity customer2(U("Smith"), U("Ben"));

azure::storage::table_entity::properties_type& properties2 = customer2.properties();
properties2.reserve(2);
properties2[U("Email")] = azure::storage::entity_property(U("Ben@contoso.com"));
properties2[U("Phone")] = azure::storage::entity_property(U("425-555-0102"));

// Create a third customer entity to add to the table.
azure::storage::table_entity customer3(U("Smith"), U("Denise"));

azure::storage::table_entity::properties_type& properties3 = customer3.properties();
properties3.reserve(2);
properties3[U("Email")] = azure::storage::entity_property(U("Denise@contoso.com"));
properties3[U("Phone")] = azure::storage::entity_property(U("425-555-0103"));

// Add customer entities to the batch insert operation.
batch_operation.insert_or_replace_entity(customer1);
batch_operation.insert_or_replace_entity(customer2);
batch_operation.insert_or_replace_entity(customer3);

// Execute the batch operation.
std::vector<azure::storage::table_result> results = table.execute_batch(batch_operation);
```

<span data-ttu-id="8a9e1-155">Di seguito sono riportate alcune informazioni sulle operazioni batch:</span><span class="sxs-lookup"><span data-stu-id="8a9e1-155">Some things to note on batch operations:</span></span>  

* <span data-ttu-id="8a9e1-156">È possibile eseguire fino a 100 operazioni di inserimento, eliminazione, unione, sostituzione, inserimento o unione e inserimento o sostituzione in qualsiasi combinazione in un unico batch.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-156">You can perform up to 100 insert, delete, merge, replace, insert-or-merge, and insert-or-replace operations in any combination in a single batch.</span></span>  
* <span data-ttu-id="8a9e1-157">Un'operazione batch può prevedere un'operazione di recupero, se è l'unica operazione nel batch.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-157">A batch operation can have a retrieve operation, if it is the only operation in the batch.</span></span>  
* <span data-ttu-id="8a9e1-158">A tutte le entità di una singola operazione batch deve essere associata la stessa chiave di partizione.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-158">All entities in a single batch operation must have the same partition key.</span></span>  
* <span data-ttu-id="8a9e1-159">Un'operazione batch è limitata a un payload di dati di 4 MB.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-159">A batch operation is limited to a 4-MB data payload.</span></span>  

## <a name="retrieve-all-entities-in-a-partition"></a><span data-ttu-id="8a9e1-160">Recuperare tutte le entità di una partizione</span><span class="sxs-lookup"><span data-stu-id="8a9e1-160">Retrieve all entities in a partition</span></span>
<span data-ttu-id="8a9e1-161">Per eseguire una query su una tabella e recuperare tutte le entità di una partizione, usare un oggetto **table_query**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-161">To query a table for all entities in a partition, use a **table_query** object.</span></span> <span data-ttu-id="8a9e1-162">Nell'esempio di codice seguente viene specificato un filtro per le entità in cui la chiave di partizione è 'Smith'.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-162">The following code example specifies a filter for entities where 'Smith' is the partition key.</span></span> <span data-ttu-id="8a9e1-163">Questo esempio consente di stampare sulla console i campi di ogni entità inclusa nei risultati della query.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-163">This example prints the fields of each entity in the query results to the console.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Construct the query operation for all customer entities where PartitionKey="Smith".
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::generate_filter_condition(U("PartitionKey"), azure::storage::query_comparison_operator::equal, U("Smith")));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Print the fields for each customer.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

<span data-ttu-id="8a9e1-164">La query di questo esempio consente di visualizzare tutte le entità che soddisfano i criteri di filtro.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-164">The query in this example brings all the entities that match the filter criteria.</span></span> <span data-ttu-id="8a9e1-165">Se si dispone di tabelle di grandi dimensioni ed è necessario scaricare le entità di tabella di frequente, è invece consigliabile archiviare i dati nei BLOB di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-165">If you have large tables and need to download the table entities often, we recommend that you store your data in Azure storage blobs instead.</span></span>

## <a name="retrieve-a-range-of-entities-in-a-partition"></a><span data-ttu-id="8a9e1-166">Recuperare un intervallo di entità in una partizione</span><span class="sxs-lookup"><span data-stu-id="8a9e1-166">Retrieve a range of entities in a partition</span></span>
<span data-ttu-id="8a9e1-167">Se non si desidera eseguire una query su tutte le entità di una partizione, è possibile specificare un intervallo combinando il filtro della chiave di partizione con quello della chiave di riga.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-167">If you don't want to query all the entities in a partition, you can specify a range by combining the partition key filter with a row key filter.</span></span> <span data-ttu-id="8a9e1-168">Nell'esempio di codice seguente vengono usati due filtri per recuperare tutte le entità della partizione 'Smith' in cui la chiave di riga (nome) inizia con una lettera che precede la 'E' nell'alfabeto e quindi stampare i risultati della query.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-168">The following code example uses two filters to get all entities in partition 'Smith' where the row key (first name) starts with a letter earlier than 'E' in the alphabet and then prints the query results.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create the table query.
azure::storage::table_query query;

query.set_filter_string(azure::storage::table_query::combine_filter_conditions(
    azure::storage::table_query::generate_filter_condition(U("PartitionKey"),
    azure::storage::query_comparison_operator::equal, U("Smith")),
    azure::storage::query_logical_operator::op_and,
    azure::storage::table_query::generate_filter_condition(U("RowKey"), azure::storage::query_comparison_operator::less_than, U("E"))));

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Loop through the results, displaying information about the entity.
azure::storage::table_query_iterator end_of_results;
for (; it != end_of_results; ++it)
{
    const azure::storage::table_entity::properties_type& properties = it->properties();

    std::wcout << U("PartitionKey: ") << it->partition_key() << U(", RowKey: ") << it->row_key()
        << U(", Property1: ") << properties.at(U("Email")).string_value()
        << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
}  
```

## <a name="retrieve-a-single-entity"></a><span data-ttu-id="8a9e1-169">Recuperare una singola entità</span><span class="sxs-lookup"><span data-stu-id="8a9e1-169">Retrieve a single entity</span></span>
<span data-ttu-id="8a9e1-170">Per recuperare una singola entità specifica, è possibile scrivere una query.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-170">You can write a query to retrieve a single, specific entity.</span></span> <span data-ttu-id="8a9e1-171">Il codice seguente usa **table_operation::retrive_entity** per specificare il cliente 'Jeff Smith'.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-171">The following code uses **table_operation::retrieve_entity** to specify the customer 'Jeff Smith'.</span></span> <span data-ttu-id="8a9e1-172">Questo metodo restituisce una sola entità anziché una raccolta, e il valore restituito si trova in **table_result**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-172">This method returns just one entity, rather than a collection, and the returned value is in **table_result**.</span></span> <span data-ttu-id="8a9e1-173">La specifica delle chiavi di partizione e di riga in una query costituisce la soluzione più rapida per recuperare una singola entità dal servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-173">Specifying both partition and row keys in a query is the fastest way to retrieve a single entity from the Table service.</span></span>  

```cpp
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Output the entity.
azure::storage::table_entity entity = retrieve_result.entity();
const azure::storage::table_entity::properties_type& properties = entity.properties();

std::wcout << U("PartitionKey: ") << entity.partition_key() << U(", RowKey: ") << entity.row_key()
    << U(", Property1: ") << properties.at(U("Email")).string_value()
    << U(", Property2: ") << properties.at(U("Phone")).string_value() << std::endl;
```

## <a name="replace-an-entity"></a><span data-ttu-id="8a9e1-174">Sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="8a9e1-174">Replace an entity</span></span>
<span data-ttu-id="8a9e1-175">Per sostituire un'entità, recuperarla dal servizio tabelle, modificare l'oggetto entità e quindi salvare le modifiche nuovamente nel servizio tabelle.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-175">To replace an entity, retrieve it from the Table service, modify the entity object, and then save the changes back to the Table service.</span></span> <span data-ttu-id="8a9e1-176">Il codice seguente consente di modificare il numero di telefono e l’indirizzo di posta elettronica di un cliente esistente.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-176">The following code changes an existing customer's phone number and email address.</span></span> <span data-ttu-id="8a9e1-177">Anziché chiamare **table_operation:: insert_entity**, in questo codice viene usato **table_operation:: replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-177">Instead of calling **table_operation::insert_entity**, this code uses **table_operation::replace_entity**.</span></span> <span data-ttu-id="8a9e1-178">In questo modo l'entità viene completamente sostituita nel server, a meno che non sia stata modificata da quando è stata recuperata.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-178">This causes the entity to be fully replaced on the server, unless the entity on the server has changed since it was retrieved, in which case the operation will fail.</span></span> <span data-ttu-id="8a9e1-179">In questo caso, infatti, l'operazione non viene eseguita per impedire all'applicazione di sovrascrivere inavvertitamente una modifica effettuata tra il recupero e l'aggiornamento da parte di un altro componente dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-179">This failure is to prevent your application from inadvertently overwriting a change made between the retrieval and update by another component of your application.</span></span> <span data-ttu-id="8a9e1-180">Per risolvere questo errore, recuperare di nuovo l'entità, apportare le modifiche, se ancora valide, quindi eseguire un'altra operazione **table_operation::replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-180">The proper handling of this failure is to retrieve the entity again, make your changes (if still valid), and then perform another **table_operation::replace_entity** operation.</span></span> <span data-ttu-id="8a9e1-181">La sezione successiva illustra come ovviare a questo comportamento.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-181">The next section will show you how to override this behavior.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Replace an entity.
azure::storage::table_entity entity_to_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_replace = entity_to_replace.properties();
properties_to_replace.reserve(2);

// Specify a new phone number.
properties_to_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0106"));

// Specify a new email address.
properties_to_replace[U("Email")] = azure::storage::entity_property(U("JeffS@contoso.com"));

// Create an operation to replace the entity.
azure::storage::table_operation replace_operation = azure::storage::table_operation::replace_entity(entity_to_replace);

// Submit the operation to the Table service.
azure::storage::table_result replace_result = table.execute(replace_operation);
```

## <a name="insert-or-replace-an-entity"></a><span data-ttu-id="8a9e1-182">Inserire o sostituire un'entità</span><span class="sxs-lookup"><span data-stu-id="8a9e1-182">Insert-or-replace an entity</span></span>
<span data-ttu-id="8a9e1-183">Le operazioni **table_operation::replace_entity** non vengono eseguite se l'entità è stata modificata rispetto a quando è stata recuperata dal server.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-183">**table_operation::replace_entity** operations will fail if the entity has been changed since it was retrieved from the server.</span></span> <span data-ttu-id="8a9e1-184">Per la corretta esecuzione di **table_operation::replace_entity**, è inoltre necessario recuperare prima l'entità dal server.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-184">Furthermore, you must retrieve the entity from the server first in order for **table_operation::replace_entity** to be successful.</span></span> <span data-ttu-id="8a9e1-185">In alcuni casi, tuttavia, non è noto se l'entità già esista nel server e i valori correnti in essa archiviati sono irrilevanti, pertanto devono essere sovrascritti completamente dall'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-185">Sometimes, however, you don't know if the entity exists on the server and the current values stored in it are irrelevant—your update should overwrite them all.</span></span> <span data-ttu-id="8a9e1-186">A tale scopo, si userà un'operazione **table_operation:: insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-186">To accomplish this, you would use a **table_operation::insert_or_replace_entity** operation.</span></span> <span data-ttu-id="8a9e1-187">Questa operazione inserisce l'entità se non è già esistente oppure la sostituisce se esiste già, indipendentemente dalla data dell'ultimo aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-187">This operation inserts the entity if it doesn't exist, or replaces it if it does, regardless of when the last update was made.</span></span> <span data-ttu-id="8a9e1-188">Nell'esempio di codice seguente l'entità customer per Jeff Smith viene recuperata comunque, ma viene salvata di nuovo nel server usando **table_operation::insert_or_replace_entity**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-188">In the following code example, the customer entity for Jeff Smith is still retrieved, but it is then saved back to the server via **table_operation::insert_or_replace_entity**.</span></span> <span data-ttu-id="8a9e1-189">Tutte le modifiche apportate all'entità tra le operazioni di recupero e aggiornamento verranno sovrascritte.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-189">Any updates made to the entity between the retrieval and update operation will be overwritten.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Insert-or-replace an entity.
azure::storage::table_entity entity_to_insert_or_replace(U("Smith"), U("Jeff"));
azure::storage::table_entity::properties_type& properties_to_insert_or_replace = entity_to_insert_or_replace.properties();

properties_to_insert_or_replace.reserve(2);

// Specify a phone number.
properties_to_insert_or_replace[U("Phone")] = azure::storage::entity_property(U("425-555-0107"));

// Specify an email address.
properties_to_insert_or_replace[U("Email")] = azure::storage::entity_property(U("Jeffsm@contoso.com"));

// Create an operation to insert-or-replace the entity.
azure::storage::table_operation insert_or_replace_operation = azure::storage::table_operation::insert_or_replace_entity(entity_to_insert_or_replace);

// Submit the operation to the Table service.
azure::storage::table_result insert_or_replace_result = table.execute(insert_or_replace_operation);
```

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="8a9e1-190">Eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="8a9e1-190">Query a subset of entity properties</span></span>
<span data-ttu-id="8a9e1-191">Mediante una query su una tabella è possibile recuperare solo alcune proprietà da un'entità.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-191">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="8a9e1-192">La query nel codice seguente usa il metodo **table_query::set_select_columns** per restituire solo gli indirizzi di posta elettronica delle entità nella tabella.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-192">The query in the following code uses the **table_query::set_select_columns** method to return only the email addresses of entities in the table.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Define the query, and select only the Email property.
azure::storage::table_query query;
std::vector<utility::string_t> columns;

columns.push_back(U("Email"));
query.set_select_columns(columns);

// Execute the query.
azure::storage::table_query_iterator it = table.execute_query(query);

// Display the results.
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
> <span data-ttu-id="8a9e1-193">L'esecuzione di una query di alcune proprietà di un'entità è un'operazione più efficiente rispetto al recupero di tutte le proprietà.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-193">Querying a few properties from an entity is a more efficient operation than retrieving all properties.</span></span>
> 
> 

## <a name="delete-an-entity"></a><span data-ttu-id="8a9e1-194">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="8a9e1-194">Delete an entity</span></span>
<span data-ttu-id="8a9e1-195">È possibile eliminare facilmente un'entità dopo averla recuperata.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-195">You can easily delete an entity after you have retrieved it.</span></span> <span data-ttu-id="8a9e1-196">Dopo il recupero dell'entità, chiamare **table_operation::delete_entity** con l'entità da eliminare.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-196">Once the entity is retrieved, call **table_operation::delete_entity** with the entity to delete.</span></span> <span data-ttu-id="8a9e1-197">Chiamare quindi il metodo **cloud_table.execute**.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-197">Then call the **cloud_table.execute** method.</span></span> <span data-ttu-id="8a9e1-198">Il codice seguente recupera ed elimina un'entità con la chiave di partizione "Smith" e la chiave di riga "Jeff".</span><span class="sxs-lookup"><span data-stu-id="8a9e1-198">The following code retrieves and deletes an entity with a partition key of "Smith" and a row key of "Jeff".</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);  
```

## <a name="delete-a-table"></a><span data-ttu-id="8a9e1-199">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="8a9e1-199">Delete a table</span></span>
<span data-ttu-id="8a9e1-200">L'esempio di codice seguente consente infine di eliminare una tabella dall'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-200">Finally, the following code example deletes a table from a storage account.</span></span> <span data-ttu-id="8a9e1-201">Una tabella eliminata non potrà essere creata nuovamente per un certo periodo di tempo.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-201">A table that has been deleted will be unavailable to be re-created for a period of time following the deletion.</span></span>  

```cpp
// Retrieve the storage account from the connection string.
azure::storage::cloud_storage_account storage_account = azure::storage::cloud_storage_account::parse(storage_connection_string);

// Create the table client.
azure::storage::cloud_table_client table_client = storage_account.create_cloud_table_client();

// Create a cloud table object for the table.
azure::storage::cloud_table table = table_client.get_table_reference(U("people"));

// Create an operation to retrieve the entity with partition key of "Smith" and row key of "Jeff".
azure::storage::table_operation retrieve_operation = azure::storage::table_operation::retrieve_entity(U("Smith"), U("Jeff"));
azure::storage::table_result retrieve_result = table.execute(retrieve_operation);

// Create an operation to delete the entity.
azure::storage::table_operation delete_operation = azure::storage::table_operation::delete_entity(retrieve_result.entity());

// Submit the delete operation to the Table service.
azure::storage::table_result delete_result = table.execute(delete_operation);
```

## <a name="next-steps"></a><span data-ttu-id="8a9e1-202">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="8a9e1-202">Next steps</span></span>
<span data-ttu-id="8a9e1-203">A questo punto, dopo aver appreso le nozioni di base dell'archiviazione tabelle, visitare i collegamenti seguenti per accedere ad altre informazioni su Archiviazione di Azure:</span><span class="sxs-lookup"><span data-stu-id="8a9e1-203">Now that you've learned the basics of table storage, follow these links to learn more about Azure Storage:</span></span>  

* <span data-ttu-id="8a9e1-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma gratuita di Microsoft che consente di rappresentare facilmente dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="8a9e1-204">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* [<span data-ttu-id="8a9e1-205">Come usare l'archiviazione BLOB da C++</span><span class="sxs-lookup"><span data-stu-id="8a9e1-205">How to use Blob storage from C++</span></span>](../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [<span data-ttu-id="8a9e1-206">Come usare l'archiviazione delle code da C++</span><span class="sxs-lookup"><span data-stu-id="8a9e1-206">How to use Queue storage from C++</span></span>](../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [<span data-ttu-id="8a9e1-207">Elenco delle risorse di archiviazione di Azure in C++</span><span class="sxs-lookup"><span data-stu-id="8a9e1-207">List Azure Storage resources in C++</span></span>](../storage/common/storage-c-plus-plus-enumeration.md)
* [<span data-ttu-id="8a9e1-208">Informazioni di riferimento sulla libreria client di archiviazione per C++</span><span class="sxs-lookup"><span data-stu-id="8a9e1-208">Storage Client Library for C++ reference</span></span>](http://azure.github.io/azure-storage-cpp)
* [<span data-ttu-id="8a9e1-209">Documentazione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="8a9e1-209">Azure Storage documentation</span></span>](https://azure.microsoft.com/documentation/services/storage/)
