---
title: Come usare l'archiviazione tabelle di Azure da Ruby | Microsoft Docs
description: Archiviare dati non strutturati nel cloud con il servizio di archiviazione tabelle di Azure, ovvero un archivio dati NoSQL.
services: cosmos-db
documentationcenter: ruby
author: mimig1
manager: jhubbard
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: cosmos-db
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: 372bc89f75ad4730f0defbf9d6f9f041ae5ce1bf
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-azure-table-storage-from-ruby"></a><span data-ttu-id="67316-103">Come usare l'archiviazione tabelle di Azure da Ruby</span><span class="sxs-lookup"><span data-stu-id="67316-103">How to use Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="67316-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="67316-104">Overview</span></span>
<span data-ttu-id="67316-105">Questa guida illustra come eseguire scenari comuni con il servizio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="67316-105">This guide shows you how to perform common scenarios using the Azure Table service.</span></span> <span data-ttu-id="67316-106">Gli esempi sono scritti utilizzando l'API Ruby.</span><span class="sxs-lookup"><span data-stu-id="67316-106">The samples are written using the Ruby API.</span></span> <span data-ttu-id="67316-107">Gli scenari presentati includono **creazione ed eliminazione di una tabella, inserimento di entità ed esecuzione di query sulle entità in una tabella**.</span><span class="sxs-lookup"><span data-stu-id="67316-107">The scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="67316-108">Creare un'applicazione Ruby</span><span class="sxs-lookup"><span data-stu-id="67316-108">Create a Ruby application</span></span>
<span data-ttu-id="67316-109">Per istruzioni su come creare un'applicazione Ruby, vedere [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md) (Applicazione Web Ruby on Rails in una VM di Azure).</span><span class="sxs-lookup"><span data-stu-id="67316-109">For instructions how to create a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="67316-110">Configurare l'applicazione per l'accesso all'archiviazione</span><span class="sxs-lookup"><span data-stu-id="67316-110">Configure your application to access Storage</span></span>
<span data-ttu-id="67316-111">Per usare l'archiviazione di Azure, è necessario scaricare e usare il pacchetto Ruby Azure, che comprende un set di pratiche librerie che comunicano con i servizi di archiviazione REST.</span><span class="sxs-lookup"><span data-stu-id="67316-111">To use Azure Storage, you need to download and use the Ruby azure package which includes a set of convenience libraries that communicate with the Storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="67316-112">Utilizzare RubyGems per ottenere il pacchetto</span><span class="sxs-lookup"><span data-stu-id="67316-112">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="67316-113">Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="67316-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="67316-114">Digitare **gem install azure** nella finestra di comando per installare la gemma e le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="67316-114">Type **gem install azure** in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="67316-115">Importare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="67316-115">Import the package</span></span>
<span data-ttu-id="67316-116">Usando l'editor di testo preferito aggiungere quanto segue alla parte superiore del file Ruby dove si intende usare l'archiviazione:</span><span class="sxs-lookup"><span data-stu-id="67316-116">Use your favorite text editor, add the following to the top of the Ruby file where you intend to use Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="67316-117">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="67316-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="67316-118">Il modulo di Azure leggerà le variabili di ambiente **AZURE\_STORAGE\_ACCOUNT** e **AZURE\_STORAGE\_ACCESS\_KEY** per ottenere le informazioni necessarie per la connessione all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="67316-118">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required to connect to your Azure Storage account.</span></span> <span data-ttu-id="67316-119">Se queste variabili di ambiente non sono impostate, sarà necessario specificare le informazioni relative all'account prima di utilizzare **Azure::TableService** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="67316-119">If these environment variables are not set, you must specify the account information before using **Azure::TableService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="67316-120">Per ottenere questi valori da un account di archiviazione classico o di Resource Manager nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="67316-120">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="67316-121">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67316-121">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="67316-122">Passare all'account di archiviazione che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="67316-122">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="67316-123">Nel pannello Impostazioni a destra fare clic su **Chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="67316-123">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="67316-124">Nel pannello Chiavi di accesso visualizzato notare la chiave di accesso 1 e la chiave di accesso 2.</span><span class="sxs-lookup"><span data-stu-id="67316-124">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="67316-125">È possibile usare una di queste indifferentemente.</span><span class="sxs-lookup"><span data-stu-id="67316-125">You can use either of these.</span></span>
5. <span data-ttu-id="67316-126">Fare clic sull'icona Copia per copiare la chiave negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="67316-126">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="67316-127">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="67316-127">Create a table</span></span>
<span data-ttu-id="67316-128">L'oggetto **Azure::TableService** consente di utilizzare tabelle ed entità.</span><span class="sxs-lookup"><span data-stu-id="67316-128">The **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="67316-129">Per creare una tabella, usare il metodo **create\_table()**.</span><span class="sxs-lookup"><span data-stu-id="67316-129">To create a table, use the **create\_table()** method.</span></span> <span data-ttu-id="67316-130">Nell'esempio seguente viene creata una tabella o stampato l'eventuale errore.</span><span class="sxs-lookup"><span data-stu-id="67316-130">The following example creates a table or prints the error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="67316-131">Aggiungere un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="67316-131">Add an entity to a table</span></span>
<span data-ttu-id="67316-132">Per aggiungere un'entità, creare innanzitutto un oggetto hash che definisca le proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="67316-132">To add an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="67316-133">Si noti che per ogni entità è necessario specificare un oggetto **PartitionKey** e un oggetto **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="67316-133">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="67316-134">Si tratta di identificatori univoci dell'entità e sono valori che possono essere interrogati molto più velocemente di altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="67316-134">These are the unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="67316-135">Archiviazione Azure utilizza **PartitionKey** per distribuire automaticamente le entità della tabella su molti nodi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="67316-135">Azure Storage uses **PartitionKey** to automatically distribute the table's entities over many storage nodes.</span></span> <span data-ttu-id="67316-136">Le entità con lo stesso oggetto **PartitionKey** vengono archiviate nello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="67316-136">Entities with the same **PartitionKey** are stored on the same node.</span></span> <span data-ttu-id="67316-137">RowKey **è l'ID univoco dell'entità all'interno della partizione cui appartiene.**</span><span class="sxs-lookup"><span data-stu-id="67316-137">The **RowKey** is the unique ID of the entity within the partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="67316-138">Aggiornare un'entità</span><span class="sxs-lookup"><span data-stu-id="67316-138">Update an entity</span></span>
<span data-ttu-id="67316-139">Esistono vari metodi per aggiornare un'entità esistente:</span><span class="sxs-lookup"><span data-stu-id="67316-139">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="67316-140">**update\_entity():** aggiorna un'entità esistente sostituendola.</span><span class="sxs-lookup"><span data-stu-id="67316-140">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="67316-141">**merge\_entity():** aggiorna un'entità esistente unendovi i nuovi valori delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="67316-141">**merge\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span>
* <span data-ttu-id="67316-142">**insert\_or\_merge\_entity():** aggiorna un'entità esistente sostituendola.</span><span class="sxs-lookup"><span data-stu-id="67316-142">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="67316-143">Se non esiste alcuna entità, ne verrà inserita una nuova:</span><span class="sxs-lookup"><span data-stu-id="67316-143">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="67316-144">**insert\_or\_replace\_entity():** aggiorna un'entità esistente unendovi i nuovi valori delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="67316-144">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into the existing entity.</span></span> <span data-ttu-id="67316-145">Se non esiste alcuna entità, ne verrà inserita una nuova.</span><span class="sxs-lookup"><span data-stu-id="67316-145">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="67316-146">Nell'esempio seguente viene dimostrato l'aggiornamento di un'entità mediante l'uso di **update\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="67316-146">The following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="67316-147">Con **update\_entity()** e **merge\_entity()**, se l'entità che si sta aggiornando non esiste, l'operazione di aggiornamento avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="67316-147">With **update\_entity()** and **merge\_entity()**, if the entity that you are updating doesn't exist then the update operation will fail.</span></span> <span data-ttu-id="67316-148">Se pertanto si desidera archiviare un'entità indipendentemente dal fatto che esista o meno, è necessario usare **insert\_or\_replace\_entity()** oppure **insert\_or\_merge\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="67316-148">Therefore if you wish to store an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="67316-149">Usare i gruppi di entità</span><span class="sxs-lookup"><span data-stu-id="67316-149">Work with groups of entities</span></span>
<span data-ttu-id="67316-150">È talvolta consigliabile inviare più operazioni in un batch per garantire l'elaborazione atomica da parte del server.</span><span class="sxs-lookup"><span data-stu-id="67316-150">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="67316-151">A tale scopo, è necessario prima creare un oggetto **Batch** e quindi usare il metodo **execute\_batch()** su **TableService**.</span><span class="sxs-lookup"><span data-stu-id="67316-151">To accomplish that, you first create a **Batch** object and then use the **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="67316-152">Nell'esempio seguente viene dimostrato l'invio di due entità con RowKey 2 e 3 in un batch:</span><span class="sxs-lookup"><span data-stu-id="67316-152">The following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="67316-153">Si noti che funziona solo per le entità con lo stesso oggetto PartitionKey.</span><span class="sxs-lookup"><span data-stu-id="67316-153">Notice that it only works for entities with the same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="67316-154">Eseguire una query su un'entità</span><span class="sxs-lookup"><span data-stu-id="67316-154">Query for an entity</span></span>
<span data-ttu-id="67316-155">Per eseguire una query su un'entità in una tabella, usare il metodo **get\_entity()** passando il nome tabella e i parametri **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="67316-155">To query an entity in a table, use the **get\_entity()** method, by passing the table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="67316-156">Eseguire query su un set di entità</span><span class="sxs-lookup"><span data-stu-id="67316-156">Query a set of entities</span></span>
<span data-ttu-id="67316-157">Per eseguire query su un set di entità in una tabella, creare un oggetto hash di query e usare il metodo **query\_entities()**.</span><span class="sxs-lookup"><span data-stu-id="67316-157">To query a set of entities in a table, create a query hash object and use the **query\_entities()** method.</span></span> <span data-ttu-id="67316-158">Nell'esempio seguente viene dimostrato l'invio di tutte le entità con lo stesso oggetto **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="67316-158">The following example demonstrates getting all the entities with the same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="67316-159">Se il risultato impostato è troppo grande affinché sia restituito da un'unica query, verrà restituito un token di continuazione per recuperare le pagine successive.</span><span class="sxs-lookup"><span data-stu-id="67316-159">If the result set is too large for a single query to return, a continuation token will be returned which you can use to retrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="67316-160">Eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="67316-160">Query a subset of entity properties</span></span>
<span data-ttu-id="67316-161">Mediante una query su una tabella è possibile recuperare solo alcune proprietà da un'entità.</span><span class="sxs-lookup"><span data-stu-id="67316-161">A query to a table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="67316-162">Questa tecnica, denominata "proiezione", consente di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="67316-162">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="67316-163">Utilizzare la clausola select e passare i nomi delle proprietà da inoltrare al client.</span><span class="sxs-lookup"><span data-stu-id="67316-163">Use the select clause and pass the names of the properties you would like to bring over to the client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="67316-164">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="67316-164">Delete an entity</span></span>
<span data-ttu-id="67316-165">Per eliminare un'entità, usare il metodo **delete\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="67316-165">To delete an entity, use the **delete\_entity()** method.</span></span> <span data-ttu-id="67316-166">È necessario passare il nome della tabella contenente l'entità e i parametri PartitionKey e RowKey dell'entità.</span><span class="sxs-lookup"><span data-stu-id="67316-166">You need to pass in the name of the table which contains the entity, the PartitionKey and RowKey of the entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="67316-167">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="67316-167">Delete a table</span></span>
<span data-ttu-id="67316-168">Per eliminare una tabella, usare il metodo **delete\_table()** e passare il nome della tabella che si desidera eliminare.</span><span class="sxs-lookup"><span data-stu-id="67316-168">To delete a table, use the **delete\_table()** method and pass in the name of the table you want to delete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="67316-169">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67316-169">Next steps</span></span>

* <span data-ttu-id="67316-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma gratuita di Microsoft che consente di rappresentare facilmente dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="67316-170">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="67316-171">[Azure SDK per Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) su GitHub</span><span class="sxs-lookup"><span data-stu-id="67316-171">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

