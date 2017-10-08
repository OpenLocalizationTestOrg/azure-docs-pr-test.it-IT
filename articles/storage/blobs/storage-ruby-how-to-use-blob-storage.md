---
title: aaaHow toouse Blob archiviazione (oggetto) da Ruby | Documenti Microsoft
description: Archiviare dati non strutturati nel cloud hello con archiviazione Blob di Azure (archiviazione di oggetti).
services: storage
documentationcenter: ruby
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: e2fe4c45-27b0-4d15-b3fb-e7eb574db717
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: ruby
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 776e7d788e69d4960f8dde0b783513f6b39b7a47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-ruby"></a><span data-ttu-id="1b15e-103">Come toouse archiviazione Blob da Ruby</span><span class="sxs-lookup"><span data-stu-id="1b15e-103">How toouse Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="1b15e-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="1b15e-104">Overview</span></span>
<span data-ttu-id="1b15e-105">Archiviazione Blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="1b15e-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="1b15e-106">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="1b15e-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="1b15e-107">Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.</span><span class="sxs-lookup"><span data-stu-id="1b15e-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="1b15e-108">Questa guida viene illustrato come tooperform scenari comuni di utilizzo dell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="1b15e-108">This guide will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="1b15e-109">esempi di Hello vengono scritti utilizzando hello API Ruby.</span><span class="sxs-lookup"><span data-stu-id="1b15e-109">hello samples are written using hello Ruby API.</span></span> <span data-ttu-id="1b15e-110">Hello scenari trattati includono **caricamento, visualizzazione di elenchi, download,** e **eliminazione** BLOB.</span><span class="sxs-lookup"><span data-stu-id="1b15e-110">hello scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="1b15e-111">Creare un'applicazione Ruby</span><span class="sxs-lookup"><span data-stu-id="1b15e-111">Create a Ruby application</span></span>
<span data-ttu-id="1b15e-112">Creare un'applicazione Ruby.</span><span class="sxs-lookup"><span data-stu-id="1b15e-112">Create a Ruby application.</span></span> <span data-ttu-id="1b15e-113">Per istruzioni, vedere l'articolo relativo all'[applicazione Web Ruby on Rails in una VM di Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="1b15e-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="1b15e-114">Configurare l'archiviazione di tooaccess di applicazione</span><span class="sxs-lookup"><span data-stu-id="1b15e-114">Configure your application tooaccess Storage</span></span>
<span data-ttu-id="1b15e-115">toouse archiviazione di Azure, è necessario toodownload e utilizzare hello Ruby pacchetto di azure, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b15e-115">toouse Azure Storage, you need toodownload and use hello Ruby azure package, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-rubygems-tooobtain-hello-package"></a><span data-ttu-id="1b15e-116">Utilizzare un pacchetto di hello tooobtain RubyGems</span><span class="sxs-lookup"><span data-stu-id="1b15e-116">Use RubyGems tooobtain hello package</span></span>
1. <span data-ttu-id="1b15e-117">Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="1b15e-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="1b15e-118">Digitare "indicatore installa azure" dipendenze e l'indicatore di hello comando finestra tooinstall hello.</span><span class="sxs-lookup"><span data-stu-id="1b15e-118">Type "gem install azure" in hello command window tooinstall hello gem and dependencies.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="1b15e-119">Importa pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="1b15e-119">Import hello package</span></span>
<span data-ttu-id="1b15e-120">Utilizzando un editor di testo, aggiungere hello toohello cima hello Ruby file in cui si intende toouse archiviazione seguente:</span><span class="sxs-lookup"><span data-stu-id="1b15e-120">Using your favorite text editor, add hello following toohello top of hello Ruby file where you intend toouse storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="1b15e-121">Configurare una connessione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1b15e-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="1b15e-122">modulo Hello azure verrà lette le variabili di ambiente hello **AZURE\_archiviazione\_ACCOUNT** e **AZURE\_archiviazione\_ACCESS_KEY** per le informazioni richieste tooconnect tooyour account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="1b15e-122">hello azure module will read hello environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="1b15e-123">Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello prima di utilizzare **Azure::Blob::BlobService** con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="1b15e-123">If these environment variables are not set, you must specify hello account information before using **Azure::Blob::BlobService** with hello following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="1b15e-124">tooobtain questi valori da un classico o Gestione risorse di archiviazione di account nel portale di Azure hello:</span><span class="sxs-lookup"><span data-stu-id="1b15e-124">tooobtain these values from a classic or Resource Manager storage account in hello Azure portal:</span></span>

1. <span data-ttu-id="1b15e-125">Accedi toohello [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="1b15e-125">Log in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="1b15e-126">Passare l'account di archiviazione toohello da toouse.</span><span class="sxs-lookup"><span data-stu-id="1b15e-126">Navigate toohello storage account you want toouse.</span></span>
3. <span data-ttu-id="1b15e-127">Nel pannello delle impostazioni hello in hello destra, fare clic su **chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="1b15e-127">In hello Settings blade on hello right, click **Access Keys**.</span></span>
4. <span data-ttu-id="1b15e-128">Nel pannello chiavi accesso hello che viene visualizzato, si noterà la chiave di accesso hello 1 e 2 di chiave di accesso.</span><span class="sxs-lookup"><span data-stu-id="1b15e-128">In hello Access keys blade that appears, you'll see hello access key 1 and access key 2.</span></span> <span data-ttu-id="1b15e-129">È possibile usare una di queste indifferentemente.</span><span class="sxs-lookup"><span data-stu-id="1b15e-129">You can use either of these.</span></span>
5. <span data-ttu-id="1b15e-130">Fare clic su hello Copia icona toocopy hello toohello chiave Appunti.</span><span class="sxs-lookup"><span data-stu-id="1b15e-130">Click hello copy icon toocopy hello key toohello clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="1b15e-131">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="1b15e-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="1b15e-132">Hello **Azure::Blob::BlobService** oggetto consente di collaborare con i contenitori e BLOB.</span><span class="sxs-lookup"><span data-stu-id="1b15e-132">hello **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="1b15e-133">toocreate un contenitore, utilizzare hello **creare\_container()** metodo.</span><span class="sxs-lookup"><span data-stu-id="1b15e-133">toocreate a container, use hello **create\_container()** method.</span></span>

<span data-ttu-id="1b15e-134">Hello esempio di codice seguente crea un contenitore o Visualizza errore hello eventuale.</span><span class="sxs-lookup"><span data-stu-id="1b15e-134">hello following code example creates a container or prints hello error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="1b15e-135">Se si desidera file hello toomake nel contenitore hello pubblico, è possibile impostare le autorizzazioni del contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="1b15e-135">If you want toomake hello files in hello container public, you can set hello container's permissions.</span></span>

<span data-ttu-id="1b15e-136">È possibile modificare solo hello <strong>creare\_container()</strong> chiamata toopass hello **: pubblica\_accesso\_livello** opzione:</span><span class="sxs-lookup"><span data-stu-id="1b15e-136">You can just modify hello <strong>create\_container()</strong> call toopass hello **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="1b15e-137">I valori validi per hello **: pubblica\_accesso\_livello** opzione sono:</span><span class="sxs-lookup"><span data-stu-id="1b15e-137">Valid values for hello **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="1b15e-138">**blob:** specifica l'accesso in lettura pubblico per i BLOB.</span><span class="sxs-lookup"><span data-stu-id="1b15e-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="1b15e-139">I dati BLOB all'interno di questo contenitore possono essere letti tramite richiesta anonima, ma i dati del contenitore non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="1b15e-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="1b15e-140">I client non è possibile enumerare i BLOB all'interno del contenitore di hello tramite una richiesta anonima.</span><span class="sxs-lookup"><span data-stu-id="1b15e-140">Clients cannot enumerate blobs within hello container via anonymous request.</span></span>
* <span data-ttu-id="1b15e-141">**container:** specifica l'accesso in lettura pubblico completo per i dati di contenitori e BLOB.</span><span class="sxs-lookup"><span data-stu-id="1b15e-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="1b15e-142">I client possono enumerare i BLOB all'interno del contenitore di hello tramite una richiesta anonima, ma non è possibile enumerare i contenitori nell'account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="1b15e-142">Clients can enumerate blobs within hello container via anonymous request, but cannot enumerate containers within hello storage account.</span></span>

<span data-ttu-id="1b15e-143">In alternativa, è possibile modificare il livello di accesso pubblico hello di un contenitore utilizzando **impostare\_contenitore\_acl()** a livello di metodo toospecify hello accesso pubblico.</span><span class="sxs-lookup"><span data-stu-id="1b15e-143">Alternatively, you can modify hello public access level of a container by using **set\_container\_acl()** method toospecify hello public access level.</span></span>

<span data-ttu-id="1b15e-144">Hello modifiche hello livello di accesso pubblico troppo di esempio di codice seguente**contenitore**:</span><span class="sxs-lookup"><span data-stu-id="1b15e-144">hello following code example changes hello public access level too**container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="1b15e-145">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="1b15e-145">Upload a blob into a container</span></span>
<span data-ttu-id="1b15e-146">blob tooa contenuto tooupload, utilizzare hello **creare\_blocco\_blob()** blob hello toocreate di metodo, utilizzare un file o stringa come contenuto di hello del blob hello.</span><span class="sxs-lookup"><span data-stu-id="1b15e-146">tooupload content tooa blob, use hello **create\_block\_blob()** method toocreate hello blob, use a file or string as hello content of hello blob.</span></span>

<span data-ttu-id="1b15e-147">esempio di codice Hello Carica file hello **test.png** come un nuovo blob denominato "image-" blob nel contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="1b15e-147">hello following code uploads hello file **test.png** as a new blob named "image-blob" in hello container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="1b15e-148">Elenco di BLOB hello in un contenitore</span><span class="sxs-lookup"><span data-stu-id="1b15e-148">List hello blobs in a container</span></span>
<span data-ttu-id="1b15e-149">utilizzare contenitori hello toolist **list_containers()** metodo.</span><span class="sxs-lookup"><span data-stu-id="1b15e-149">toolist hello containers, use **list_containers()** method.</span></span>
<span data-ttu-id="1b15e-150">toolist hello BLOB all'interno di un contenitore, usare **elenco\_blobs()** metodo.</span><span class="sxs-lookup"><span data-stu-id="1b15e-150">toolist hello blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="1b15e-151">Restituisce gli URL di hello di tutti i BLOB hello in tutti i contenitori di hello per conto di hello.</span><span class="sxs-lookup"><span data-stu-id="1b15e-151">This outputs hello urls of all hello blobs in all hello containers for hello account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="1b15e-152">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="1b15e-152">Download blobs</span></span>
<span data-ttu-id="1b15e-153">BLOB toodownload, utilizzare hello **ottenere\_blob()** contenuto hello tooretrieve di metodo.</span><span class="sxs-lookup"><span data-stu-id="1b15e-153">toodownload blobs, use hello **get\_blob()** method tooretrieve hello contents.</span></span>

<span data-ttu-id="1b15e-154">Hello esempio di codice seguente viene illustrato come utilizzare **ottenere\_blob()** toodownload contenuto di "immagine blob" hello e scriverlo tooa file locale.</span><span class="sxs-lookup"><span data-stu-id="1b15e-154">hello following code example demonstrates using **get\_blob()** toodownload hello contents of "image-blob" and write it tooa local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="1b15e-155">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="1b15e-155">Delete a Blob</span></span>
<span data-ttu-id="1b15e-156">Infine, toodelete un blob, utilizzare hello **eliminare\_blob()** metodo.</span><span class="sxs-lookup"><span data-stu-id="1b15e-156">Finally, toodelete a blob, use hello **delete\_blob()** method.</span></span> <span data-ttu-id="1b15e-157">Hello esempio di codice riportato di seguito viene illustrato come toodelete un blob.</span><span class="sxs-lookup"><span data-stu-id="1b15e-157">hello following code example demonstrates how toodelete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="1b15e-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="1b15e-158">Next steps</span></span>
<span data-ttu-id="1b15e-159">toolearn sulle attività di archiviazione più complesse, vedere i collegamenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="1b15e-159">toolearn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="1b15e-160">Blog del team di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="1b15e-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="1b15e-161">[Azure SDK per Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) su GitHub</span><span class="sxs-lookup"><span data-stu-id="1b15e-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="1b15e-162">Trasferimento dati con l'utilità della riga di comando di AzCopy hello</span><span class="sxs-lookup"><span data-stu-id="1b15e-162">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

