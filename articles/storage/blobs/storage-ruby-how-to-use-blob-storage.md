---
title: Come usare l'archiviazione BLOB (archiviazione di oggetti) da Ruby | Microsoft Docs
description: Archiviare i dati non strutturati nel cloud con l'archivio BLOB (archivio di oggetti) di Azure.
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
ms.openlocfilehash: d27cf1594d6a31a746ca85b5c3184f8a5dbbaa54
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-ruby"></a><span data-ttu-id="cb4f6-103">Come usare l'archiviazione BLOB da Ruby</span><span class="sxs-lookup"><span data-stu-id="cb4f6-103">How to use Blob storage from Ruby</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="cb4f6-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="cb4f6-104">Overview</span></span>
<span data-ttu-id="cb4f6-105">L'archiviazione BLOB di Azure è un servizio che archivia dati non strutturati nel cloud come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="cb4f6-106">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="cb4f6-107">L'archivio BLOB è anche denominato archivio di oggetti.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="cb4f6-108">Questa guida illustra scenari comuni relativi all'uso dell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-108">This guide will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="cb4f6-109">Gli esempi sono scritti utilizzando l'API Ruby.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-109">The samples are written using the Ruby API.</span></span> <span data-ttu-id="cb4f6-110">Gli scenari presentati includono **caricamento, visualizzazione in elenchi, download** ed **eliminazione** di BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-110">The scenarios covered include **uploading, listing, downloading,** and **deleting** blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-ruby-application"></a><span data-ttu-id="cb4f6-111">Creare un'applicazione Ruby</span><span class="sxs-lookup"><span data-stu-id="cb4f6-111">Create a Ruby application</span></span>
<span data-ttu-id="cb4f6-112">Creare un'applicazione Ruby.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-112">Create a Ruby application.</span></span> <span data-ttu-id="cb4f6-113">Per istruzioni, vedere l'articolo relativo all'[applicazione Web Ruby on Rails in una VM di Azure](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md).</span><span class="sxs-lookup"><span data-stu-id="cb4f6-113">For instructions, see [Ruby on Rails Web application on an Azure VM](../../virtual-machines/linux/classic/virtual-machines-linux-classic-ruby-rails-web-app.md)</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="cb4f6-114">Configurare l'applicazione per l'accesso all'archiviazione</span><span class="sxs-lookup"><span data-stu-id="cb4f6-114">Configure your application to access Storage</span></span>
<span data-ttu-id="cb4f6-115">Per usare l'archiviazione di Azure, è necessario scaricare e usare il pacchetto Ruby Azure, che comprende un set di pratiche librerie che comunicano con i servizi di archiviazione REST.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-115">To use Azure Storage, you need to download and use the Ruby azure package, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-rubygems-to-obtain-the-package"></a><span data-ttu-id="cb4f6-116">Utilizzare RubyGems per ottenere il pacchetto</span><span class="sxs-lookup"><span data-stu-id="cb4f6-116">Use RubyGems to obtain the package</span></span>
1. <span data-ttu-id="cb4f6-117">Usare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix).</span><span class="sxs-lookup"><span data-stu-id="cb4f6-117">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix).</span></span>
2. <span data-ttu-id="cb4f6-118">Digitare "gem install azure" nella finestra di comando per installare la gemma e le dipendenze.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-118">Type "gem install azure" in the command window to install the gem and dependencies.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="cb4f6-119">Importare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="cb4f6-119">Import the package</span></span>
<span data-ttu-id="cb4f6-120">Usando l'editor di testo preferito aggiungere quanto segue alla parte superiore del file Ruby dove si intende usare l'archiviazione:</span><span class="sxs-lookup"><span data-stu-id="cb4f6-120">Using your favorite text editor, add the following to the top of the Ruby file where you intend to use storage:</span></span>

```ruby
require "azure"
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="cb4f6-121">Configurare una connessione di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="cb4f6-121">Set up an Azure Storage Connection</span></span>
<span data-ttu-id="cb4f6-122">Il modulo di Azure leggerà le variabili di ambiente **AZURE\_STORAGE\_ACCOUNT** e **AZURE\_STORAGE\_ACCESS_KEY** per ottenere le informazioni necessarie per la connessione all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-122">The azure module will read the environment variables **AZURE\_STORAGE\_ACCOUNT** and **AZURE\_STORAGE\_ACCESS_KEY** for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="cb4f6-123">Se queste variabili di ambiente non sono impostate, sarà necessario specificare le informazioni relative all'account prima di usare **Azure::BLOB::BlobService** con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="cb4f6-123">If these environment variables are not set, you must specify the account information before using **Azure::Blob::BlobService** with the following code:</span></span>

```ruby
Azure.config.storage_account_name = "<your azure storage account>"
Azure.config.storage_access_key = "<your azure storage access key>"
```

<span data-ttu-id="cb4f6-124">Per ottenere questi valori da un account di archiviazione classico o di Resource Manager nel portale di Azure:</span><span class="sxs-lookup"><span data-stu-id="cb4f6-124">To obtain these values from a classic or Resource Manager storage account in the Azure portal:</span></span>

1. <span data-ttu-id="cb4f6-125">Accedere al [Portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="cb4f6-125">Log in to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="cb4f6-126">Passare all'account di archiviazione che si desidera utilizzare.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-126">Navigate to the storage account you want to use.</span></span>
3. <span data-ttu-id="cb4f6-127">Nel pannello Impostazioni a destra fare clic su **Chiavi di accesso**.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-127">In the Settings blade on the right, click **Access Keys**.</span></span>
4. <span data-ttu-id="cb4f6-128">Nel pannello Chiavi di accesso visualizzato notare la chiave di accesso 1 e la chiave di accesso 2.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-128">In the Access keys blade that appears, you'll see the access key 1 and access key 2.</span></span> <span data-ttu-id="cb4f6-129">È possibile usare una di queste indifferentemente.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-129">You can use either of these.</span></span>
5. <span data-ttu-id="cb4f6-130">Fare clic sull'icona Copia per copiare la chiave negli Appunti.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-130">Click the copy icon to copy the key to the clipboard.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="cb4f6-131">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="cb4f6-131">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="cb4f6-132">L'oggetto **Azure::BLOB::BlobService** consente di lavorare con contenitori e BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-132">The **Azure::Blob::BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="cb4f6-133">Per creare un contenitore, usare il metodo **create\_container()**.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-133">To create a container, use the **create\_container()** method.</span></span>

<span data-ttu-id="cb4f6-134">L'esempio di codice seguente crea un contenitore o stampa l'eventuale errore.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-134">The following code example creates a container or prints the error if there is any.</span></span>

```ruby
azure_blob_service = Azure::Blob::BlobService.new
begin
    container = azure_blob_service.create_container("test-container")
rescue
    puts $!
end
```

<span data-ttu-id="cb4f6-135">Se si desidera rendere pubblici i file nel contenitore è possibile impostare le autorizzazioni del contenitore.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-135">If you want to make the files in the container public, you can set the container's permissions.</span></span>

<span data-ttu-id="cb4f6-136">È possibile modificare solo la chiamata <strong>create\_container()</strong> per passare l'opzione **:public\_access\_level**:</span><span class="sxs-lookup"><span data-stu-id="cb4f6-136">You can just modify the <strong>create\_container()</strong> call to pass the **:public\_access\_level** option:</span></span>

```ruby
container = azure_blob_service.create_container("test-container",
    :public_access_level => "<public access level>")
```

<span data-ttu-id="cb4f6-137">I valori validi per l'opzione **:public\_access\_level** sono:</span><span class="sxs-lookup"><span data-stu-id="cb4f6-137">Valid values for the **:public\_access\_level** option are:</span></span>

* <span data-ttu-id="cb4f6-138">**blob:** specifica l'accesso in lettura pubblico per i BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-138">**blob:** Specifies public read access for blobs.</span></span> <span data-ttu-id="cb4f6-139">I dati BLOB all'interno di questo contenitore possono essere letti tramite richiesta anonima, ma i dati del contenitore non sono disponibili.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-139">Blob data within this container can be read via anonymous request, but container data is not available.</span></span> <span data-ttu-id="cb4f6-140">I client non possono enumerare i BLOB all'interno del contenitore tramite richiesta anonima.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-140">Clients cannot enumerate blobs within the container via anonymous request.</span></span>
* <span data-ttu-id="cb4f6-141">**container:** specifica l'accesso in lettura pubblico completo per i dati di contenitori e BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-141">**container:** Specifies full public read access for container and blob data.</span></span> <span data-ttu-id="cb4f6-142">I client possono enumerare i BLOB all'interno del contenitore tramite richiesta anonima, ma non sono in grado di enumerare i contenitori all'interno dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-142">Clients can enumerate blobs within the container via anonymous request, but cannot enumerate containers within the storage account.</span></span>

<span data-ttu-id="cb4f6-143">In alternativa, è possibile modificare il livello di accesso di un contenitore usando il metodo **set\_container\_acl()** per specificare il livello di accesso pubblico.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-143">Alternatively, you can modify the public access level of a container by using **set\_container\_acl()** method to specify the public access level.</span></span>

<span data-ttu-id="cb4f6-144">Nell'esempio di codice seguente viene modificato il livello di accesso pubblico al **contenitore**:</span><span class="sxs-lookup"><span data-stu-id="cb4f6-144">The following code example changes the public access level to **container**:</span></span>

```ruby
azure_blob_service.set_container_acl('test-container', "container")
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="cb4f6-145">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="cb4f6-145">Upload a blob into a container</span></span>
<span data-ttu-id="cb4f6-146">Per caricare contenuto in un BLOB, usare il metodo **create\_block\_blob()** per crearne uno, usando un file o una stringa come contenuto del BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-146">To upload content to a blob, use the **create\_block\_blob()** method to create the blob, use a file or string as the content of the blob.</span></span>

<span data-ttu-id="cb4f6-147">Il codice seguente consentirà di caricare il file **test.png** come nuovo BLOB denominato "image-blob" nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-147">The following code uploads the file **test.png** as a new blob named "image-blob" in the container.</span></span>

```ruby
content = File.open("test.png", "rb") { |file| file.read }
blob = azure_blob_service.create_block_blob(container.name,
    "image-blob", content)
puts blob.name
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="cb4f6-148">Elencare i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="cb4f6-148">List the blobs in a container</span></span>
<span data-ttu-id="cb4f6-149">Per elencare i contenitori, usare il metodo **list_containers()**.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-149">To list the containers, use **list_containers()** method.</span></span>
<span data-ttu-id="cb4f6-150">Per elencare i BLOB all'interno di un contenitore, usare il metodo **list\_blobs()**.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-150">To list the blobs within a container, use **list\_blobs()** method.</span></span>

<span data-ttu-id="cb4f6-151">L'output sarà costituito dagli URL di tutti i BLOB in tutti i contenitori relativi all'account.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-151">This outputs the urls of all the blobs in all the containers for the account.</span></span>

```ruby
containers = azure_blob_service.list_containers()
containers.each do |container|
    blobs = azure_blob_service.list_blobs(container.name)
    blobs.each do |blob|
    puts blob.name
    end
end
```

## <a name="download-blobs"></a><span data-ttu-id="cb4f6-152">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="cb4f6-152">Download blobs</span></span>
<span data-ttu-id="cb4f6-153">Per scaricare i BLOB, usare il metodo **get\_blob()** per recuperare il contenuto.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-153">To download blobs, use the **get\_blob()** method to retrieve the contents.</span></span>

<span data-ttu-id="cb4f6-154">Nell'esempio seguente viene illustrato l'uso di **get\_blob()** per scaricare il contenuto di "image-blob" e scriverlo in un file locale.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-154">The following code example demonstrates using **get\_blob()** to download the contents of "image-blob" and write it to a local file.</span></span>

```ruby
blob, content = azure_blob_service.get_blob(container.name,"image-blob")
File.open("download.png","wb") {|f| f.write(content)}
```

## <a name="delete-a-blob"></a><span data-ttu-id="cb4f6-155">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="cb4f6-155">Delete a Blob</span></span>
<span data-ttu-id="cb4f6-156">Per eliminare un BLOB, infine, usare il metodo **delete\_blob()**.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-156">Finally, to delete a blob, use the **delete\_blob()** method.</span></span> <span data-ttu-id="cb4f6-157">Nell'esempio seguente viene illustrato come eliminare un BLOB.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-157">The following code example demonstrates how to delete a blob.</span></span>

```ruby
azure_blob_service.delete_blob(container.name, "image-blob")
```

## <a name="next-steps"></a><span data-ttu-id="cb4f6-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="cb4f6-158">Next steps</span></span>
<span data-ttu-id="cb4f6-159">Seguire i collegamenti seguenti per ulteriori informazioni sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="cb4f6-159">To learn about more complex storage tasks, follow these links:</span></span>

* [<span data-ttu-id="cb4f6-160">Blog del team di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="cb4f6-160">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* <span data-ttu-id="cb4f6-161">[Azure SDK per Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) su GitHub</span><span class="sxs-lookup"><span data-stu-id="cb4f6-161">[Azure SDK for Ruby](https://github.com/WindowsAzure/azure-sdk-for-ruby) repository on GitHub</span></span>
* [<span data-ttu-id="cb4f6-162">Trasferire dati con l'utilità della riga di comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="cb4f6-162">Transfer data with the AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

