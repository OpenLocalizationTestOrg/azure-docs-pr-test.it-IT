---
title: aaaHow toouse (archiviazione di oggetti) di archiviazione Blob di Azure da Python | Documenti Microsoft
description: Archiviare dati non strutturati nel cloud hello con archiviazione Blob di Azure (archiviazione di oggetti).
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
ms.openlocfilehash: 8f9ca93e52b030384e28a739d2f1c6b610be094a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-blob-storage-from-python"></a><span data-ttu-id="87318-103">Come toouse archiviazione Blob di Azure da Python</span><span class="sxs-lookup"><span data-stu-id="87318-103">How toouse Azure Blob storage from Python</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="87318-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="87318-104">Overview</span></span>
<span data-ttu-id="87318-105">Archiviazione Blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="87318-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="87318-106">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="87318-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="87318-107">Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.</span><span class="sxs-lookup"><span data-stu-id="87318-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="87318-108">In questo articolo viene illustrato come tooperform scenari comuni di utilizzo dell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="87318-108">This article will show you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="87318-109">esempi di Hello sono scritti in Python e utilizzare hello [Microsoft Azure Storage SDK per Python].</span><span class="sxs-lookup"><span data-stu-id="87318-109">hello samples are written in Python and use hello [Microsoft Azure Storage SDK for Python].</span></span> <span data-ttu-id="87318-110">scenari di Hello trattati includono il caricamento, elenco, il download e l'eliminazione dei BLOB.</span><span class="sxs-lookup"><span data-stu-id="87318-110">hello scenarios covered include uploading, listing, downloading, and deleting blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-container"></a><span data-ttu-id="87318-111">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="87318-111">Create a container</span></span>
<span data-ttu-id="87318-112">In base al tipo di hello del blob desideri toouse, creare un **BlockBlobService**, **AppendBlobService**, o **PageBlobService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="87318-112">Based on hello type of blob you would like toouse, create a **BlockBlobService**, **AppendBlobService**, or **PageBlobService** object.</span></span> <span data-ttu-id="87318-113">codice Hello seguente viene utilizzato un **BlockBlobService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="87318-113">hello following code uses a **BlockBlobService** object.</span></span> <span data-ttu-id="87318-114">Aggiungere il seguente hello superiore hello di qualsiasi file Python in cui si desidera tooprogrammatically accesso Azure archivio Blob in blocchi.</span><span class="sxs-lookup"><span data-stu-id="87318-114">Add hello following near hello top of any Python file in which you wish tooprogrammatically access Azure Block Blob Storage.</span></span>

```python
from azure.storage.blob import BlockBlobService
```

<span data-ttu-id="87318-115">Hello codice seguente viene creata una **BlockBlobService** oggetto utilizzando hello chiave account di archiviazione nome e all'account.</span><span class="sxs-lookup"><span data-stu-id="87318-115">hello following code creates a **BlockBlobService** object using hello storage account name and account key.</span></span>  <span data-ttu-id="87318-116">Sostituire 'myaccount' e 'mykey' con l'account e la chiave da usare.</span><span class="sxs-lookup"><span data-stu-id="87318-116">Replace 'myaccount' and 'mykey' with your account name and key.</span></span>

```python
block_blob_service = BlockBlobService(account_name='myaccount', account_key='mykey')
```

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="87318-117">Nell'esempio di codice seguente di hello, è possibile utilizzare un **BlockBlobService** toocreate hello contenitore di oggetti di se non esiste.</span><span class="sxs-lookup"><span data-stu-id="87318-117">In hello following code example, you can use a **BlockBlobService** object toocreate hello container if it doesn't exist.</span></span>

```python
block_blob_service.create_container('mycontainer')
```

<span data-ttu-id="87318-118">Per impostazione predefinita, hello nuovo contenitore è privato, è necessario specificare la chiave di accesso di archiviazione (come descritto in precedenza) BLOB toodownload da questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="87318-118">By default, hello new container is private, so you must specify your storage access key (as you did earlier) toodownload blobs from this container.</span></span> <span data-ttu-id="87318-119">Se si desidera BLOB hello toomake all'interno di hello contenitore disponibili tooeveryone, è possibile creare il contenitore di hello e passare il livello di accesso pubblico hello utilizzando il seguente codice hello.</span><span class="sxs-lookup"><span data-stu-id="87318-119">If you want toomake hello blobs within hello container available tooeveryone, you can create hello container and pass hello public access level using hello following code.</span></span>

```python
from azure.storage.blob import PublicAccess
block_blob_service.create_container('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="87318-120">In alternativa, è possibile modificare un contenitore dopo aver creato tramite hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="87318-120">Alternatively, you can modify a container after you have created it using hello following code.</span></span>

```python
block_blob_service.set_container_acl('mycontainer', public_access=PublicAccess.Container)
```

<span data-ttu-id="87318-121">Dopo questa modifica, chiunque in Internet hello può visualizzare i BLOB in un contenitore pubblico, ma solo è possibile modificarli o eliminarli.</span><span class="sxs-lookup"><span data-stu-id="87318-121">After this change, anyone on hello Internet can see blobs in a public container, but only you can modify or delete them.</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="87318-122">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="87318-122">Upload a blob into a container</span></span>
<span data-ttu-id="87318-123">toocreate un blob in blocchi e caricare i dati, utilizzare hello **creare\_blob\_da\_percorso**, **creare\_blob\_da\_flusso**, **creare\_blob\_da\_byte** o **creare\_blob\_da\_testo** metodi.</span><span class="sxs-lookup"><span data-stu-id="87318-123">toocreate a block blob and upload data, use hello **create\_blob\_from\_path**, **create\_blob\_from\_stream**, **create\_blob\_from\_bytes** or **create\_blob\_from\_text** methods.</span></span> <span data-ttu-id="87318-124">Sono metodi di alto livello che eseguono hello necessarie suddivisione in blocchi quando hello hello dati superano di 64 MB.</span><span class="sxs-lookup"><span data-stu-id="87318-124">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="87318-125">**creare\_blob\_da\_percorso** caricamenti hello contenuto di un file dal percorso specificato hello, e **creare\_blob\_da\_flusso** caricamenti hello contenuto dal flusso file già aperto.</span><span class="sxs-lookup"><span data-stu-id="87318-125">**create\_blob\_from\_path** uploads hello contents of a file from hello specified path, and **create\_blob\_from\_stream** uploads hello contents from an already opened file/stream.</span></span> <span data-ttu-id="87318-126">**creare\_blob\_da\_byte** carica una matrice di byte, e **creare\_blob\_da\_testo** carica hello specificato il valore di testo utilizzando hello specificato codifica (impostazioni predefinite tooUTF-8).</span><span class="sxs-lookup"><span data-stu-id="87318-126">**create\_blob\_from\_bytes** uploads an array of bytes, and **create\_blob\_from\_text** uploads hello specified text value using hello specified encoding (defaults tooUTF-8).</span></span>

<span data-ttu-id="87318-127">esempio Hello carica il contenuto di hello di hello **sunset.png** file hello **myblob** blob.</span><span class="sxs-lookup"><span data-stu-id="87318-127">hello following example uploads hello contents of hello **sunset.png** file into hello **myblob** blob.</span></span>

```python
from azure.storage.blob import ContentSettings
block_blob_service.create_blob_from_path(
    'mycontainer',
    'myblockblob',
    'sunset.png',
    content_settings=ContentSettings(content_type='image/png')
            )
```

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="87318-128">Elenco di BLOB hello in un contenitore</span><span class="sxs-lookup"><span data-stu-id="87318-128">List hello blobs in a container</span></span>
<span data-ttu-id="87318-129">BLOB di hello toolist in un contenitore, usare hello **elenco\_BLOB** metodo.</span><span class="sxs-lookup"><span data-stu-id="87318-129">toolist hello blobs in a container, use hello **list\_blobs** method.</span></span> <span data-ttu-id="87318-130">Questo metodo restituisce un generatore.</span><span class="sxs-lookup"><span data-stu-id="87318-130">This method returns a generator.</span></span> <span data-ttu-id="87318-131">il codice seguente Hello restituisce hello **nome** di ogni blob in una console toohello contenitore.</span><span class="sxs-lookup"><span data-stu-id="87318-131">hello following code outputs hello **name** of each blob in a container toohello console.</span></span>

```python
generator = block_blob_service.list_blobs('mycontainer')
for blob in generator:
    print(blob.name)
```

## <a name="download-blobs"></a><span data-ttu-id="87318-132">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="87318-132">Download blobs</span></span>
<span data-ttu-id="87318-133">toodownload dei dati da un blob, utilizzare **ottenere\_blob\_a\_percorso**, **ottenere\_blob\_a\_flusso**, **ottenere\_blob\_a\_byte**, o **ottenere\_blob\_a\_testo**.</span><span class="sxs-lookup"><span data-stu-id="87318-133">toodownload data from a blob, use **get\_blob\_to\_path**, **get\_blob\_to\_stream**, **get\_blob\_to\_bytes**, or **get\_blob\_to\_text**.</span></span> <span data-ttu-id="87318-134">Sono metodi di alto livello che eseguono hello necessarie suddivisione in blocchi quando hello hello dati superano di 64 MB.</span><span class="sxs-lookup"><span data-stu-id="87318-134">They are high-level methods that perform hello necessary chunking when hello size of hello data exceeds 64 MB.</span></span>

<span data-ttu-id="87318-135">Hello seguente viene illustrato l'utilizzo **ottenere\_blob\_a\_percorso** contenuto hello toodownload di hello **myblob** blob e di archiviarlo toohello **out sunset.png** file.</span><span class="sxs-lookup"><span data-stu-id="87318-135">hello following example demonstrates using **get\_blob\_to\_path** toodownload hello contents of hello **myblob** blob and store it toohello **out-sunset.png** file.</span></span>

```python
block_blob_service.get_blob_to_path('mycontainer', 'myblockblob', 'out-sunset.png')
```

## <a name="delete-a-blob"></a><span data-ttu-id="87318-136">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="87318-136">Delete a blob</span></span>
<span data-ttu-id="87318-137">Chiamare infine toodelete un blob, **delete_blob**.</span><span class="sxs-lookup"><span data-stu-id="87318-137">Finally, toodelete a blob, call **delete_blob**.</span></span>

```python
block_blob_service.delete_blob('mycontainer', 'myblockblob')
```

## <a name="writing-tooan-append-blob"></a><span data-ttu-id="87318-138">Scrittura tooan aggiungere blob</span><span class="sxs-lookup"><span data-stu-id="87318-138">Writing tooan append blob</span></span>
<span data-ttu-id="87318-139">Un blob di accodamento è ottimizzato per le operazioni di accodamento, ad esempio la registrazione.</span><span class="sxs-lookup"><span data-stu-id="87318-139">An append blob is optimized for append operations, such as logging.</span></span> <span data-ttu-id="87318-140">Come un blob in blocchi, un blob di aggiunta è costituito da blocchi, ma quando si aggiunge un nuovo blob in blocchi tooan accodamento, è sempre aggiunte toohello fine del blob hello.</span><span class="sxs-lookup"><span data-stu-id="87318-140">Like a block blob, an append blob is comprised of blocks, but when you add a new block tooan append blob, it is always appended toohello end of hello blob.</span></span> <span data-ttu-id="87318-141">È possibile aggiornare o eliminare un blocco esistente in un blob di Accodamento.</span><span class="sxs-lookup"><span data-stu-id="87318-141">You cannot update or delete an existing block in an append blob.</span></span> <span data-ttu-id="87318-142">ID blocco Hello per un blob di aggiunta non vengono esposte come se fossero per un blob in blocchi.</span><span class="sxs-lookup"><span data-stu-id="87318-142">hello block IDs for an append blob are not exposed as they are for a block blob.</span></span>

<span data-ttu-id="87318-143">Ogni blocco di un blob di aggiunta può avere dimensioni diverse, backup tooa massimo 4 MB, e un blob di aggiunta può includere un massimo di 50.000 blocchi.</span><span class="sxs-lookup"><span data-stu-id="87318-143">Each block in an append blob can be a different size, up tooa maximum of 4 MB, and an append blob can include a maximum of 50,000 blocks.</span></span> <span data-ttu-id="87318-144">dimensione massima di Hello di un blob di aggiunta è pertanto leggermente superiore a 195 GB (4 MB X 50.000 blocchi).</span><span class="sxs-lookup"><span data-stu-id="87318-144">hello maximum size of an append blob is therefore slightly more than 195 GB (4 MB X 50,000 blocks).</span></span>

<span data-ttu-id="87318-145">esempio Hello seguente crea un nuovo blob di aggiunta e accoda tooit alcuni dati, simulazione di un'operazione di registrazione semplice.</span><span class="sxs-lookup"><span data-stu-id="87318-145">hello example below creates a new append blob and appends some data tooit, simulating a simple logging operation.</span></span>

```python
from azure.storage.blob import AppendBlobService
append_blob_service = AppendBlobService(account_name='myaccount', account_key='mykey')

# hello same containers can hold all types of blobs
append_blob_service.create_container('mycontainer')

# Append blobs must be created before they are appended to
append_blob_service.create_blob('mycontainer', 'myappendblob')
append_blob_service.append_blob_from_text('mycontainer', 'myappendblob', u'Hello, world!')

append_blob = append_blob_service.get_blob_to_text('mycontainer', 'myappendblob')
```

## <a name="next-steps"></a><span data-ttu-id="87318-146">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87318-146">Next steps</span></span>
<span data-ttu-id="87318-147">Ora che si è appreso i concetti di base di hello dell'archiviazione Blob, seguire questi ulteriori toolearn di collegamenti.</span><span class="sxs-lookup"><span data-stu-id="87318-147">Now that you've learned hello basics of Blob storage, follow these links toolearn more.</span></span>

* [<span data-ttu-id="87318-148">Centro per sviluppatori Python</span><span class="sxs-lookup"><span data-stu-id="87318-148">Python Developer Center</span></span>](https://azure.microsoft.com/develop/python/)
* [<span data-ttu-id="87318-149">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="87318-149">Azure Storage Services REST API</span></span>](http://msdn.microsoft.com/library/azure/dd179355)
* <span data-ttu-id="87318-150">[Blog del team di Archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="87318-150">[Azure Storage Team Blog]</span></span>
* <span data-ttu-id="87318-151">[Microsoft Azure Storage SDK per Python]</span><span class="sxs-lookup"><span data-stu-id="87318-151">[Microsoft Azure Storage SDK for Python]</span></span>

[Blog del team di Archiviazione di Azure]: http://blogs.msdn.com/b/windowsazurestorage/
[Microsoft Azure Storage SDK per Python]: https://github.com/Azure/azure-storage-python
