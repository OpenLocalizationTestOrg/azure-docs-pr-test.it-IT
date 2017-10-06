---
title: aaaIntroduction tooAzure nell'archiviazione Blob | Documenti Microsoft
description: Introduzione tooAzure nell'archiviazione Blob
services: storage
documentationcenter: 
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: robinsh
ms.openlocfilehash: 3431f826ae51d42dbced084ee60f9ff70a8168d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-tooblob-storage"></a><span data-ttu-id="c544c-103">Archiviazione tooBlob introduzione</span><span class="sxs-lookup"><span data-stu-id="c544c-103">Introduction tooBlob storage</span></span>

<span data-ttu-id="c544c-104">Archiviazione Blob di Azure è un servizio per l'archiviazione di grandi quantità di dati dell'oggetto non strutturati, ad esempio dati di testo o binario, che è possibile accedere da qualsiasi in HelloWorld tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="c544c-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in hello world via HTTP or HTTPS.</span></span> <span data-ttu-id="c544c-105">È possibile utilizzare dati tooexpose di archiviazione Blob pubblicamente toohello world o dati dell'applicazione toostore privatamente.</span><span class="sxs-lookup"><span data-stu-id="c544c-105">You can use Blob storage tooexpose data publicly toohello world, or toostore application data privately.</span></span>

<span data-ttu-id="c544c-106">Quelli di seguito sono gli impieghi più comuni dell'archiviazione BLOB:</span><span class="sxs-lookup"><span data-stu-id="c544c-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="c544c-107">Servizio immagini o documenti direttamente browser tooa</span><span class="sxs-lookup"><span data-stu-id="c544c-107">Serving images or documents directly tooa browser</span></span>
* <span data-ttu-id="c544c-108">Archiviazione di file per l'accesso distribuito</span><span class="sxs-lookup"><span data-stu-id="c544c-108">Storing files for distributed access</span></span>
* <span data-ttu-id="c544c-109">Flussi audio e video</span><span class="sxs-lookup"><span data-stu-id="c544c-109">Streaming video and audio</span></span>
* <span data-ttu-id="c544c-110">Archiviazione di dati per backup e ripristino, ripristino di emergenza e archiviazione</span><span class="sxs-lookup"><span data-stu-id="c544c-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="c544c-111">Archiviazione di dati a scopo di analisi da parte di un servizio locale o ospitato in Azure</span><span class="sxs-lookup"><span data-stu-id="c544c-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="c544c-112">Concetti del servizio BLOB</span><span class="sxs-lookup"><span data-stu-id="c544c-112">Blob service concepts</span></span>

<span data-ttu-id="c544c-113">servizio Blob Hello contiene hello seguenti componenti:</span><span class="sxs-lookup"><span data-stu-id="c544c-113">hello Blob service contains hello following components:</span></span>

![Architettura BLOB](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="c544c-115">**Account di archiviazione:** tutti gli accessi tooAzure archiviazione viene eseguita tramite un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c544c-115">**Storage Account:** All access tooAzure Storage is done through a storage account.</span></span> <span data-ttu-id="c544c-116">Questo può essere un **account di archiviazione di uso generico** o un **account di archiviazione BLOB**, specializzato per l'archiviazione di oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="c544c-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="c544c-117">Per altre informazioni, vedere [Informazioni sugli account di archiviazione di Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="c544c-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="c544c-118">**Contenitore:** un contenitore è un raggruppamento di un set di BLOB.</span><span class="sxs-lookup"><span data-stu-id="c544c-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="c544c-119">Tutti i BLOB devono trovarsi in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="c544c-119">All blobs must be in a container.</span></span> <span data-ttu-id="c544c-120">In un account può esistere un numero illimitato di contenitori.</span><span class="sxs-lookup"><span data-stu-id="c544c-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="c544c-121">In un contenitore può essere archiviato un numero illimitato di BLOB.</span><span class="sxs-lookup"><span data-stu-id="c544c-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="c544c-122">Si noti che il nome del contenitore hello deve essere minuscole.</span><span class="sxs-lookup"><span data-stu-id="c544c-122">Note that hello container name must be lowercase.</span></span>

* <span data-ttu-id="c544c-123">**BLOB:** file di qualsiasi tipo e dimensione.</span><span class="sxs-lookup"><span data-stu-id="c544c-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="c544c-124">Archiviazione di Azure offre tre tipi di BLOB: i BLOB in blocchi, i BLOB di pagine e i BLOB di accodamento.</span><span class="sxs-lookup"><span data-stu-id="c544c-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="c544c-125">*BLOB in blocchi* sono ideali per l'archiviazione di file di testo o file binari, ad esempio i documenti e i file multimediali.</span><span class="sxs-lookup"><span data-stu-id="c544c-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="c544c-126">*BLOB di aggiunta* sono BLOB tooblock simili in quanto essi sono costituiti da blocchi, ma vengono ottimizzati per le operazioni di accodamento, in modo che siano utili per gli scenari di registrazione.</span><span class="sxs-lookup"><span data-stu-id="c544c-126">*Append blobs* are similar tooblock blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="c544c-127">Un blob in blocchi singolo può contenere un massimo di too50, i blocchi 000 di too100 MB, per una dimensione totale di leggermente superiore a 4,75 TB (100 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="c544c-127">A single block blob can contain up too50,000 blocks of up too100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="c544c-128">Un blob di aggiunta singolo può contenere un massimo di too50, i blocchi 000 di too4 MB, per una dimensione totale leggermente superiore 195 GB (4 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="c544c-128">A single append blob can contain up too50,000 blocks of up too4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="c544c-129">*BLOB di pagine* può essere backup too1 TB in dimensioni e sono più efficienti per le operazioni frequenti in lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="c544c-129">*Page blobs* can be up too1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="c544c-130">Le macchine virtuali di Azure usano BLOB di pagine come dischi di dati e del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="c544c-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="c544c-131">Per informazioni sulla denominazione di contenitori e BLOB, vedere l'articolo relativo alla [denominazione e riferimento a contenitori, BLOB e metadati](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="c544c-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c544c-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c544c-132">Next steps</span></span>

* [<span data-ttu-id="c544c-133">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="c544c-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="c544c-134">Introduzione all'archivio BLOB di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="c544c-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)