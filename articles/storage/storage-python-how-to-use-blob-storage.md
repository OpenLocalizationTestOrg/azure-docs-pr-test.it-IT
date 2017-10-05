---
title: Come usare l'archiviazione BLOB di Azure (archiviazione degli oggetti) da Python | Microsoft Docs
description: Archiviare i dati non strutturati nel cloud con l'archivio BLOB (archivio di oggetti) di Azure.
services: storage
documentationcenter: python
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 0348e360-b24d-41fa-bb12-b8f18990d8bc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: article
ms.date: 2/24/2017
ms.author: marsma
ms.openlocfilehash: 968814db9496fd410162d482191592c8a56101f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-blob-storage-from-python"></a><span data-ttu-id="09d2a-103">Come usare l'archiviazione BLOB di Azure da Python</span><span class="sxs-lookup"><span data-stu-id="09d2a-103">How to use Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="09d2a-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="09d2a-104">Overview</span></span>
<span data-ttu-id="09d2a-105">L'archiviazione BLOB di Azure è un servizio che archivia dati non strutturati nel cloud come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="09d2a-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="09d2a-106">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="09d2a-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="09d2a-107">L'archivio BLOB è anche denominato archivio di oggetti.</span><span class="sxs-lookup"><span data-stu-id="09d2a-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="09d2a-108">In questo articolo verranno illustrati diversi scenari comuni di uso del servizio di archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="09d2a-108">This article will show you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="09d2a-109">Gli esempi sono scritti in Python e usano [Microsoft Azure Storage SDK per Python].</span><span class="sxs-lookup"><span data-stu-id="09d2a-109">The samples are written in Python and use the [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="09d2a-110">Gli scenari presentati includono caricamento, visualizzazione in elenchi, download ed eliminazione di BLOB.</span><span class="sxs-lookup"><span data-stu-id="09d2a-110">The scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="09d2a-111">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="09d2a-111">Create a container</span></span>
<span data-ttu-id="09d2a-112">In base al tipo di BLOB che si vuole usare, creare un oggetto **BlockBlobService**, **AppendBlobService** o **PageBlobService**.</span><span class="sxs-lookup"><span data-stu-id="09d2a-112">Based on the type of blob you would like to use, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="09d2a-113">Il codice seguente usa un oggetto **BlockBlobService** .</span><span class="sxs-lookup"><span data-stu-id="09d2a-113">The following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="09d2a-114">Aggiungere il codice seguente vicino all'inizio del file Python da cui si desidera accedere all'archiviazione di BLOB in blocchi di Azure a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="09d2a-114">Add the following near the top of any Python file in which you wish to programmatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="09d2a-115">Il codice seguente crea un oggetto **BlockBlobService** usando il nome e la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="09d2a-115">The following code creates a **BlockBlobService** object using the storage account name and account key.</span></span>  <span data-ttu-id="09d2a-116">Sostituire 'myaccount' e 'mykey' con l'account e la chiave da usare.</span><span class="sxs-lookup"><span data-stu-id="09d2a-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="09d2a-117">Nell'esempio di codice seguente è possibile usare un oggetto **BlockBlobService** per creare il contenitore, se non esiste.</span><span class="sxs-lookup"><span data-stu-id="09d2a-117">In the following code example, you can use a **BlockBlobService** object to create the container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="09d2a-118">Per impostazione predefinita, il nuovo contenitore è privato ed è necessario specificare la chiave di accesso alle risorse di archiviazione, come già fatto in precedenza, per scaricare BLOB da questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="09d2a-118">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span> <span data-ttu-id="09d2a-119">Se si vuole che i BLOB all'interno del contenitore siano disponibili a tutti, è possibile creare il contenitore e passare il livello di accesso pubblico usando il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="09d2a-119">If you want to make the blobs within the container available to everyone, you can create the container and pass the public access level using the following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="09d2a-120">In alternativa è possibile modificare un contenitore dopo averlo creato usando il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="09d2a-120">Alternatively, you can modify a container after you have created it using the following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="09d2a-121">Dopo questa modifica, i BLOB in un contenitore pubblico saranno visibili a tutti gli utenti di Internet, tuttavia solo l'utente che li ha creati sarà in grado di modificarli o eliminarli.</span><span class="sxs-lookup"><span data-stu-id="09d2a-121">After this change, anyone on the Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="09d2a-122">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="09d2a-122">Upload a blob into a container</span></span>
<span data-ttu-id="09d2a-123">Per creare un BLOB in blocchi e caricare i dati, usare i metodi **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** o **create\_blob\_from\_text**.</span><span class="sxs-lookup"><span data-stu-id="09d2a-123">To create a block blob and upload data, use the **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="09d2a-124">Questi sono metodi di carattere generale che eseguono il blocco dei dati necessario quando le dimensioni superano i 64 MB.</span><span class="sxs-lookup"><span data-stu-id="09d2a-124">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="09d2a-125">**create\_blob\_from\_path** carica i contenuti di un file dal percorso specificato, mentre **create\_blob\_from\_stream** carica i contenuti da un file/flusso già aperto.</span><span class="sxs-lookup"><span data-stu-id="09d2a-125">**create\_blob\_from\_path** uploads the contents of a file from the specified path, and **create\_blob\_from\_stream** uploads the contents from an already opened file/stream.</span></span> <span data-ttu-id="09d2a-126">**create\_blob\_from\_bytes** carica un array di byte, mentre **create\_blob\_from\_text** carica il valore di testo specificato usando la codifica specificata (l'impostazione predefinita è UTF-8).</span><span class="sxs-lookup"><span data-stu-id="09d2a-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads the specified text value using the specified encoding (defaults to UTF-8).</span></span>

<span data-ttu-id="09d2a-127">Nell'esempio seguente viene caricato il contenuto del file **sunset.png** nel BLOB **myblob**.</span><span class="sxs-lookup"><span data-stu-id="09d2a-127">The following example uploads the contents of the **sunset.png** file into the **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="09d2a-128">Elencare i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="09d2a-128">List the blobs in a container</span></span>
<span data-ttu-id="09d2a-129">Per elencare i BLOB in un contenitore, usare il metodo **list\_blobs**.</span><span class="sxs-lookup"><span data-stu-id="09d2a-129">To list the blobs in a container, use the **list\_blobs** method.</span></span> <span data-ttu-id="09d2a-130">Questo metodo restituisce un generatore.</span><span class="sxs-lookup"><span data-stu-id="09d2a-130">This method returns a generator.</span></span> <span data-ttu-id="09d2a-131">Il codice seguente consente di inviare alla console il valore **name** di ogni BLOB in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="09d2a-131">The following code outputs the **name** of each blob in a container to the console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="09d2a-132">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="09d2a-132">Download blobs</span></span>
<span data-ttu-id="09d2a-133">Per scaricare i dati da un BLOB, usare **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes** o **get\_blob\_to\_text**.</span><span class="sxs-lookup"><span data-stu-id="09d2a-133">To download data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="09d2a-134">Questi sono metodi di carattere generale che eseguono il blocco dei dati necessario quando le dimensioni superano i 64 MB.</span><span class="sxs-lookup"><span data-stu-id="09d2a-134">They are high-level methods that perform the necessary chunking when the size of the data exceeds 64 MB.</span></span>

<span data-ttu-id="09d2a-135">Nell'esempio seguente viene illustrato l'uso di **get\_blob\_to\_path** per scaricare il contenuto del BLOB **myblob** e archiviarlo nel file **out-sunset.png**.</span><span class="sxs-lookup"><span data-stu-id="09d2a-135">The following example demonstrates using **get\_blob\_to\_path** to download the contents of the **myblob** blob and store it to the **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="09d2a-136">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="09d2a-136">Delete a blob</span></span>
<span data-ttu-id="09d2a-137">Per eliminare un BLOB, infine, chiamare **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="09d2a-137">Finally, to delete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-to-an-append-blob"></a><span data-ttu-id="09d2a-138">Scrittura in un blob di Accodamento</span><span class="sxs-lookup"><span data-stu-id="09d2a-138">Writing to an append blob</span></span>
<span data-ttu-id="09d2a-139">Un blob di accodamento è ottimizzato per le operazioni di accodamento, ad esempio la registrazione.</span><span class="sxs-lookup"><span data-stu-id="09d2a-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="09d2a-140">Come un blob in blocchi, un blob di accodamento è costituito da blocchi, ma quando si aggiunge un nuovo blocco in un blob di accodamento, viene aggiunto sempre alla fine del blob.</span><span class="sxs-lookup"><span data-stu-id="09d2a-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block to an append blob, it is always appended to the end of the blob.</span></span> <span data-ttu-id="09d2a-141">È possibile aggiornare o eliminare un blocco esistente in un blob di Accodamento.</span><span class="sxs-lookup"><span data-stu-id="09d2a-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="09d2a-142">L'ID di blocco per un blob di accodamento non vengono esposte come in un blob in blocchi.</span><span class="sxs-lookup"><span data-stu-id="09d2a-142">The block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="09d2a-143">Ogni blocco di un blob di accodamento può avere dimensioni diverse, con un massimo di 4 MB e un blob di accodamento può includere un massimo di 50.000 blocchi.</span><span class="sxs-lookup"><span data-stu-id="09d2a-143">Each block in an append blob can be a different size, up to a maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="09d2a-144">La dimensione massima di un blob di accodamento è pertanto leggermente superiore a 195 GB (4 MB X 50.000 blocchi).</span><span class="sxs-lookup"><span data-stu-id="09d2a-144">The maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="09d2a-145">Nell'esempio seguente si crea un nuovo blob di accodamento e vi si aggiungono alcuni dati, per simulare un'operazione di registrazione semplice.</span><span class="sxs-lookup"><span data-stu-id="09d2a-145">The example below creates a new append blob and appends some data to it, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# The same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="09d2a-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="09d2a-146">Next steps</span></span>
<span data-ttu-id="09d2a-147">A questo punto, dopo avere appreso le nozioni di base dell'archivio BLOB, visitare i collegamenti seguenti per altre informazioni.</span><span class="sxs-lookup"><span data-stu-id="09d2a-147">Now that you've learned the basics of Blob storage, follow these links to learn more.</span></span>

* [<span data-ttu-id="09d2a-148">Centro per sviluppatori di Python</span><span class="sxs-lookup"><span data-stu-id="09d2a-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="09d2a-149">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="09d2a-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="09d2a-150">[Blog del team di Archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="09d2a-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="09d2a-151">[Microsoft Azure Storage SDK per Python]</span><span class="sxs-lookup"><span data-stu-id="09d2a-151">[Microsoft Azure Storage SDK for Python]</span></span>

<span data-ttu-id="09d2a-152">[Blog del team di Archiviazione di Azure]: http://blogs.msdn.com/b/windowsazurestorage/</span><span class="sxs-lookup"><span data-stu-id="09d2a-152">[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/</span></span>
<span data-ttu-id="09d2a-153">[Microsoft Azure Storage SDK per Python]: https://github.com/Azure/azure-storage-python</span><span class="sxs-lookup"><span data-stu-id="09d2a-153">[Microsoft Azure Storage SDK for Python]: https://github.com/Azure/azure-storage-python</span></span>
