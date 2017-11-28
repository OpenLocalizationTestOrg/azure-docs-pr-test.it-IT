---
title: aaaHow toouse archiviazione tabelle di Azure da Ruby | Documenti Microsoft
description: Archiviare dati strutturati in un cloud di hello tramite l'archiviazione tabelle di Azure, un archivio dati NoSQL.
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: 
ms.assetid: 047cd9ff-17d3-4c15-9284-1b5cc61a3224
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 9c77ff9f384a776c9bc075b60b351685c61acc36
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-ruby"></a><span data-ttu-id="ba429-103">Come toouse archiviazione tabelle di Azure da Ruby</span><span class="sxs-lookup"><span data-stu-id="ba429-103">How toouse Azure Table Storage from Ruby</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="ba429-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="ba429-104">Overview</span></span>
<span data-ttu-id="ba429-105">Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello del servizio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="ba429-105">This guide shows you how tooperform common scenarios using hello Azure Table service.</span></span> <span data-ttu-id="ba429-106">esempi di Hello vengono scritti utilizzando hello API Ruby.</span><span class="sxs-lookup"><span data-stu-id="ba429-106">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="ba429-107">Hello scenari trattati includono **creazione e l'eliminazione di una tabella, inserimento e una query sulle entità in una tabella**.</span><span class="sxs-lookup"><span data-stu-id="ba429-107">hello scenarios covered include **creating and deleting a table, inserting and querying entities in a table**.</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="ba429-108">Creare un'applicazione Ruby</span><span class="sxs-lookup"><span data-stu-id="ba429-108">Create a Ruby application</span></span>
<span data-ttu-id="ba429-109">Per istruzioni toocreate un'applicazione Ruby, vedere [Ruby in un'applicazione Web di guide in una macchina virtuale Azure](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="ba429-109">For instructions how toocreate a Ruby application, see [Ruby on Rails Web application on an Azure VM](../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="ba429-110">Configurare l'archiviazione di tooaccess di applicazione</span><span class="sxs-lookup"><span data-stu-id="ba429-110">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="ba429-111">toouse archiviazione di Azure, è necessario toodownload e utilizzare hello Ruby pacchetto azure che include un set di librerie di praticità che comunicano con servizi di archiviazione REST hello.</span><span class="sxs-lookup"><span data-stu-id="ba429-111">toouse Azure Storage, you need toodownload and use hello Ruby azure package which includes a set of convenience libraries that communicate with hello Storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="ba429-112">Utilizzare un pacchetto di hello tooobtain RubyGems</span><span class="sxs-lookup"><span data-stu-id="ba429-112">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="ba429-113">Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="ba429-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="ba429-114">Tipo **azure installazione indicatore** indicatore di hello comando finestra tooinstall hello e delle dipendenze.</span><span class="sxs-lookup"><span data-stu-id="ba429-114">Type **gem install azure** in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="ba429-115">Importa pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="ba429-115">Import hello package</span></span>
<span data-ttu-id="ba429-116">Utilizzare un editor di testo, aggiungere hello toohello cima hello Ruby file in cui si intende toouse archiviazione seguente:</span><span class="sxs-lookup"><span data-stu-id="ba429-116">Use your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse Storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="ba429-117">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="ba429-117">Set up an Azure Storage connection</span></span>
<span data-ttu-id="ba429-118">Hello modulo azure verrà lette le variabili di ambiente hello **AZURE\_archiviazione\_ACCOUNT** e **AZURE\_archiviazione\_accesso\_chiave**per le informazioni necessarie tooconnect tooyour account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="ba429-118">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS\_KEY** for information required tooconnect tooyour Azure Storage account.</span></span> <span data-ttu-id="ba429-119">Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello prima di utilizzare **Azure::TableService** con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="ba429-119">If these environment variables are not set, you must specify hello account information before using **Azure::TableService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="ba429-120">tooobtain questi valori da un classico o Gestione risorse di archiviazione di account nel portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="ba429-120">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="ba429-121">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ba429-121">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="ba429-122">Passare l'account di archiviazione toohello da toouse.</span><span class="sxs-lookup"><span data-stu-id="ba429-122">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="ba429-123">Nel pannello delle impostazioni hello in hello destra, fare clic su **chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="ba429-123">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="ba429-124">Nel pannello chiavi accesso hello che viene visualizzato, si noterà la chiave di accesso hello 1 e 2 di chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="ba429-124">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="ba429-125">È possibile usare una di queste indifferentemente.</span><span class="sxs-lookup"><span data-stu-id="ba429-125">You can use either of these.</span></span>
5. <span data-ttu-id="ba429-126">Fare clic su hello Copia icona toocopy hello toohello chiave Appunti.</span><span class="sxs-lookup"><span data-stu-id="ba429-126">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

<span data-ttu-id="ba429-127">tooobtain questi valori da un'archiviazione classico account nel portale di Azure classico hello:</span><span class="sxs-lookup"><span data-stu-id="ba429-127">tooobtain these values from a classic storage account in hello classic Azure portal:</span></span>

1. <span data-ttu-id="ba429-128">Accedi toohello [portale di Azure classico](https://manage.windowsazure.com).</span><span class="sxs-lookup"><span data-stu-id="ba429-128">Log in toohello [Azure classic portal](https://manage.windowsazure.com).</span></span>
2. <span data-ttu-id="ba429-129">Passare l'account di archiviazione toohello da toouse.</span><span class="sxs-lookup"><span data-stu-id="ba429-129">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="ba429-130">Fare clic su **GESTISCI CHIAVI di accesso** nella parte inferiore di hello del riquadro di spostamento hello.</span><span class="sxs-lookup"><span data-stu-id="ba429-130">Click **MANAGE ACCESS KEYS** at hello bottom of hello navigation pane.</span></span>
4. <span data-ttu-id="ba429-131">Nella finestra di dialogo popup hello, si noterà nome account di archiviazione hello, chiave di accesso primaria e chiave di accesso secondaria.</span><span class="sxs-lookup"><span data-stu-id="ba429-131">In hello pop-up dialog, you'll see hello storage account name, primary access key and secondary access key.</span></span> <span data-ttu-id="ba429-132">Per la chiave di accesso, è possibile utilizzare hello primario o quello secondario hello.</span><span class="sxs-lookup"><span data-stu-id="ba429-132">For access key, you can use either hello primary one or hello secondary one.</span></span>
5. <span data-ttu-id="ba429-133">Fare clic su hello Copia icona toocopy hello toohello chiave Appunti.</span><span class="sxs-lookup"><span data-stu-id="ba429-133">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-table"></a><span data-ttu-id="ba429-134">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="ba429-134">Create a table</span></span>
<span data-ttu-id="ba429-135">Hello **Azure::TableService** oggetto consente di utilizzare tabelle ed entità.</span><span class="sxs-lookup"><span data-stu-id="ba429-135">hello **Azure::TableService** object lets you work with tables and entities.</span></span> <span data-ttu-id="ba429-136">toocreate una tabella, utilizzare hello **creare\_table()** metodo.</span><span class="sxs-lookup"><span data-stu-id="ba429-136">toocreate a table, use hello **create\_table()** method.</span></span> <span data-ttu-id="ba429-137">esempio Hello crea una tabella o stampa hello errore eventuale.</span><span class="sxs-lookup"><span data-stu-id="ba429-137">hello following example creates a table or prints hello error if there is any.</span></span>

```ruby
azure_table_service = Azure::TableService.new
begin
    azure_table_service.create_table("testtable")
rescue
    puts $!
end
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="ba429-138">Aggiungere una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="ba429-138">Add an entity tooa table</span></span>
<span data-ttu-id="ba429-139">tooadd un'entità, creare innanzitutto un oggetto hash che definisce le proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="ba429-139">tooadd an entity, first create a hash object that defines your entity properties.</span></span> <span data-ttu-id="ba429-140">Si noti che per ogni entità è necessario specificare un oggetto **PartitionKey** e un oggetto **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="ba429-140">Note that for every entity you must specify a **PartitionKey** and **RowKey**.</span></span> <span data-ttu-id="ba429-141">Questi sono identificatori univoci delle entità di hello e sono valori che è possono eseguire una query più velocemente rispetto alle altre proprietà.</span><span class="sxs-lookup"><span data-stu-id="ba429-141">These are hello unique identifiers of your entities, and are values that can be queried much faster than your other properties.</span></span> <span data-ttu-id="ba429-142">Archiviazione di Azure Usa **PartitionKey** tooautomatically distribuire entità della tabella hello su molti nodi di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="ba429-142">Azure Storage uses **PartitionKey** tooautomatically distribute hello table's entities over many storage nodes.</span></span> <span data-ttu-id="ba429-143">Le entità con hello stesso **PartitionKey** vengono archiviati in hello stesso nodo.</span><span class="sxs-lookup"><span data-stu-id="ba429-143">Entities with hello same **PartitionKey** are stored on hello same node.</span></span> <span data-ttu-id="ba429-144">Hello **RowKey** hello ID univoco dell'entità hello all'interno della partizione hello a cui appartiene.</span><span class="sxs-lookup"><span data-stu-id="ba429-144">hello **RowKey** is hello unique ID of hello entity within hello partition it belongs to.</span></span>

```ruby
entity = { "content" => "test entity",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.insert_entity("testtable", entity)
```

## <a name="update-an-entity"></a><span data-ttu-id="ba429-145">Aggiornare un'entità</span><span class="sxs-lookup"><span data-stu-id="ba429-145">Update an entity</span></span>
<span data-ttu-id="ba429-146">Esistono più tooupdate disponibili di metodi un'entità esistente:</span><span class="sxs-lookup"><span data-stu-id="ba429-146">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="ba429-147">**update\_entity():** aggiorna un'entità esistente sostituendola.</span><span class="sxs-lookup"><span data-stu-id="ba429-147">**update\_entity():** Update an existing entity by replacing it.</span></span>
* <span data-ttu-id="ba429-148">**unione\_entity():** aggiorna un'entità esistente unendo nuovi valori della proprietà di entità esistente hello.</span><span class="sxs-lookup"><span data-stu-id="ba429-148">**merge\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span>
* <span data-ttu-id="ba429-149">**insert\_or\_merge\_entity():** aggiorna un'entità esistente sostituendola.</span><span class="sxs-lookup"><span data-stu-id="ba429-149">**insert\_or\_merge\_entity():** Updates an existing entity by replacing it.</span></span> <span data-ttu-id="ba429-150">Se non esiste alcuna entità, ne verrà inserita una nuova:</span><span class="sxs-lookup"><span data-stu-id="ba429-150">If no entity exists, a new one will be inserted:</span></span>
* <span data-ttu-id="ba429-151">**Inserisci\_o\_sostituire\_entity():** aggiorna un'entità esistente unendo nuovi valori della proprietà di entità esistente hello.</span><span class="sxs-lookup"><span data-stu-id="ba429-151">**insert\_or\_replace\_entity():** Updates an existing entity by merging new property values into hello existing entity.</span></span> <span data-ttu-id="ba429-152">Se non esiste alcuna entità, ne verrà inserita una nuova.</span><span class="sxs-lookup"><span data-stu-id="ba429-152">If no entity exists, a new one will be inserted.</span></span>

<span data-ttu-id="ba429-153">Hello esempio seguente viene illustrato l'aggiornamento di un'entità mediante **aggiornare\_entity()**:</span><span class="sxs-lookup"><span data-stu-id="ba429-153">hello following example demonstrates updating an entity using **update\_entity()**:</span></span>

```ruby
entity = { "content" => "test entity with updated content",
    :PartitionKey => "test-partition-key", :RowKey => "1" }
azure_table_service.update_entity("testtable", entity)
```

<span data-ttu-id="ba429-154">Con **aggiornare\_entity()** e **unione\_entity()**, se non esiste entità hello che si sta aggiornando l'operazione di aggiornamento hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="ba429-154">With **update\_entity()** and **merge\_entity()**, if hello entity that you are updating doesn't exist then hello update operation will fail.</span></span> <span data-ttu-id="ba429-155">Pertanto se si desidera toostore un'entità indipendentemente dal fatto se esiste già, è invece necessario utilizzare **inserire\_o\_sostituire\_entity()** o **inserire\_o \_unione\_entity()**.</span><span class="sxs-lookup"><span data-stu-id="ba429-155">Therefore if you wish toostore an entity regardless of whether it already exists, you should instead use **insert\_or\_replace\_entity()** or **insert\_or\_merge\_entity()**.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="ba429-156">Usare i gruppi di entità</span><span class="sxs-lookup"><span data-stu-id="ba429-156">Work with groups of entities</span></span>
<span data-ttu-id="ba429-157">A volte risulta più toosubmit senso più operazioni contemporaneamente in un batch tooensure atomica elaborazione dal server hello.</span><span class="sxs-lookup"><span data-stu-id="ba429-157">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="ba429-158">tooaccomplish, creare innanzitutto un **Batch** oggetto, quindi utilizzare hello **eseguire\_batch()** metodo **TableService**.</span><span class="sxs-lookup"><span data-stu-id="ba429-158">tooaccomplish that, you first create a **Batch** object and then use hello **execute\_batch()** method on **TableService**.</span></span> <span data-ttu-id="ba429-159">Hello esempio seguente viene illustrato l'invio di due entità con RowKey 2 e 3 in un batch.</span><span class="sxs-lookup"><span data-stu-id="ba429-159">hello following example demonstrates submitting two entities with RowKey 2 and 3 in a batch.</span></span> <span data-ttu-id="ba429-160">Si noti che solo funziona per le entità con hello PartitionKey stesso.</span><span class="sxs-lookup"><span data-stu-id="ba429-160">Notice that it only works for entities with hello same PartitionKey.</span></span>

```ruby
azure_table_service = Azure::TableService.new
batch = Azure::Storage::Table::Batch.new("testtable",
    "test-partition-key") do
    insert "2", { "content" => "new content 2" }
    insert "3", { "content" => "new content 3" }
end
results = azure_table_service.execute_batch(batch)
```

## <a name="query-for-an-entity"></a><span data-ttu-id="ba429-161">Eseguire una query su un'entità</span><span class="sxs-lookup"><span data-stu-id="ba429-161">Query for an entity</span></span>
<span data-ttu-id="ba429-162">un'entità in una tabella, utilizzare hello tooquery **ottenere\_entity()** (metodo), passando il nome di tabella hello **PartitionKey** e **RowKey**.</span><span class="sxs-lookup"><span data-stu-id="ba429-162">tooquery an entity in a table, use hello **get\_entity()** method, by passing hello table name, **PartitionKey** and **RowKey**.</span></span>

```ruby
result = azure_table_service.get_entity("testtable", "test-partition-key",
    "1")
```

## <a name="query-a-set-of-entities"></a><span data-ttu-id="ba429-163">Eseguire query su un set di entità</span><span class="sxs-lookup"><span data-stu-id="ba429-163">Query a set of entities</span></span>
<span data-ttu-id="ba429-164">tooquery un set di entità in una tabella, creare un oggetto hash di query e utilizzare hello **query\_entities()** metodo.</span><span class="sxs-lookup"><span data-stu-id="ba429-164">tooquery a set of entities in a table, create a query hash object and use hello **query\_entities()** method.</span></span> <span data-ttu-id="ba429-165">Hello esempio seguente viene illustrato come ottenere tutte le entità di hello con hello stesso **PartitionKey**:</span><span class="sxs-lookup"><span data-stu-id="ba429-165">hello following example demonstrates getting all hello entities with hello same **PartitionKey**:</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'" }
result, token = azure_table_service.query_entities("testtable", query)
```

> [!NOTE]
> <span data-ttu-id="ba429-166">Se il set di risultati hello è troppo grande per tooreturn una singola query, un token di continuazione verrà restituito che è possibile utilizzare le pagine successive tooretrieve.</span><span class="sxs-lookup"><span data-stu-id="ba429-166">If hello result set is too large for a single query tooreturn, a continuation token will be returned which you can use tooretrieve subsequent pages.</span></span>
>
>

## <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="ba429-167">Eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="ba429-167">Query a subset of entity properties</span></span>
<span data-ttu-id="ba429-168">Una tabella di tooa query è possibile recuperare solo alcune proprietà di un'entità.</span><span class="sxs-lookup"><span data-stu-id="ba429-168">A query tooa table can retrieve just a few properties from an entity.</span></span> <span data-ttu-id="ba429-169">Questa tecnica, denominata "proiezione", consente di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="ba429-169">This technique, called "projection", reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="ba429-170">Clausola select hello di utilizzo e i nomi di hello passaggio di hello proprietà toobring su toohello client.</span><span class="sxs-lookup"><span data-stu-id="ba429-170">Use hello select clause and pass hello names of hello properties you would like toobring over toohello client.</span></span>

```ruby
query = { :filter => "PartitionKey eq 'test-partition-key'",
    :select => ["content"] }
result, token = azure_table_service.query_entities("testtable", query)
```

## <a name="delete-an-entity"></a><span data-ttu-id="ba429-171">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="ba429-171">Delete an entity</span></span>
<span data-ttu-id="ba429-172">toodelete un'entità, utilizzare hello **eliminare\_entity()** metodo.</span><span class="sxs-lookup"><span data-stu-id="ba429-172">toodelete an entity, use hello **delete\_entity()** method.</span></span> <span data-ttu-id="ba429-173">È necessario toopass nel nome hello della tabella hello che contiene entità hello, hello PartitionKey e RowKey di hello entità.</span><span class="sxs-lookup"><span data-stu-id="ba429-173">You need toopass in hello name of hello table which contains hello entity, hello PartitionKey and RowKey of hello entity.</span></span>

```ruby
azure_table_service.delete_entity("testtable", "test-partition-key", "1")
```

## <a name="delete-a-table"></a><span data-ttu-id="ba429-174">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="ba429-174">Delete a table</span></span>
<span data-ttu-id="ba429-175">toodelete una tabella, utilizzare hello **eliminare\_table()** (metodo) e passare il nome di hello di hello tabella desiderata toodelete.</span><span class="sxs-lookup"><span data-stu-id="ba429-175">toodelete a table, use hello **delete\_table()** method and pass in hello name of hello table you want toodelete.</span></span>

```ruby
azure_table_service.delete_table("testtable")
```

## <a name="next-steps"></a><span data-ttu-id="ba429-176">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ba429-176">Next steps</span></span>

* <span data-ttu-id="ba429-177">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="ba429-177">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="ba429-178">[Azure SDK per Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) su GitHub</span><span class="sxs-lookup"><span data-stu-id="ba429-178">[Azure SDK for Ruby](http://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>

