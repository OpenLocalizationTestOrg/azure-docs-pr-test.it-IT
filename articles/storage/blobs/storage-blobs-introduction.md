---
title: Introduzione all'archiviazione BLOB di Azure | Microsoft Docs
description: Introduzione all'archiviazione BLOB di Azure
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
ms.openlocfilehash: 051f1b37eab254d4ab4f806166ac8d0b8cab944d
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-blob-storage"></a><span data-ttu-id="d1e36-103">Introduzione all'archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="d1e36-103">Introduction to Blob storage</span></span>

<span data-ttu-id="d1e36-104">Archivio BLOB di Azure è un servizio per l'archiviazione di grandi quantità di dati oggetto non strutturati, ad esempio dati di testo o binari, a cui è possibile accedere da qualsiasi parte del mondo tramite HTTP o HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d1e36-104">Azure Blob storage is a service for storing large amounts of unstructured object data, such as text or binary data, that can be accessed from anywhere in the world via HTTP or HTTPS.</span></span> <span data-ttu-id="d1e36-105">L'archiviazione BLOB può essere usata per esporre dati pubblicamente a livello mondiale o archiviare privatamente i dati delle applicazioni.</span><span class="sxs-lookup"><span data-stu-id="d1e36-105">You can use Blob storage to expose data publicly to the world, or to store application data privately.</span></span>

<span data-ttu-id="d1e36-106">Quelli di seguito sono gli impieghi più comuni dell'archiviazione BLOB:</span><span class="sxs-lookup"><span data-stu-id="d1e36-106">Common uses of Blob storage include:</span></span>

* <span data-ttu-id="d1e36-107">Invio di immagini o documenti direttamente in un browser</span><span class="sxs-lookup"><span data-stu-id="d1e36-107">Serving images or documents directly to a browser</span></span>
* <span data-ttu-id="d1e36-108">Archiviazione di file per l'accesso distribuito</span><span class="sxs-lookup"><span data-stu-id="d1e36-108">Storing files for distributed access</span></span>
* <span data-ttu-id="d1e36-109">Flussi audio e video</span><span class="sxs-lookup"><span data-stu-id="d1e36-109">Streaming video and audio</span></span>
* <span data-ttu-id="d1e36-110">Archiviazione di dati per backup e ripristino, ripristino di emergenza e archiviazione</span><span class="sxs-lookup"><span data-stu-id="d1e36-110">Storing data for backup and restore, disaster recovery, and archiving</span></span>
* <span data-ttu-id="d1e36-111">Archiviazione di dati a scopo di analisi da parte di un servizio locale o ospitato in Azure</span><span class="sxs-lookup"><span data-stu-id="d1e36-111">Storing data for analysis by an on-premises or Azure-hosted service</span></span>

## <a name="blob-service-concepts"></a><span data-ttu-id="d1e36-112">Concetti del servizio BLOB</span><span class="sxs-lookup"><span data-stu-id="d1e36-112">Blob service concepts</span></span>

<span data-ttu-id="d1e36-113">Il servizio BLOB è composto dai componenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="d1e36-113">The Blob service contains the following components:</span></span>

![Architettura BLOB](./media/storage-blobs-introduction/blob1.png)

* <span data-ttu-id="d1e36-115">**Account di archiviazione:** l'accesso ad Archiviazione di Azure viene eseguito esclusivamente tramite un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d1e36-115">**Storage Account:** All access to Azure Storage is done through a storage account.</span></span> <span data-ttu-id="d1e36-116">Questo può essere un **account di archiviazione di uso generico** o un **account di archiviazione BLOB**, specializzato per l'archiviazione di oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="d1e36-116">This storage account can be a **General-purpose storage account** or a **Blob storage account** that is specialized for storing objects/blobs.</span></span> <span data-ttu-id="d1e36-117">Per altre informazioni, vedere [Informazioni sugli account di archiviazione di Azure](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="d1e36-117">See [About Azure storage accounts](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) for more information.</span></span>

* <span data-ttu-id="d1e36-118">**Contenitore:** un contenitore è un raggruppamento di un set di BLOB.</span><span class="sxs-lookup"><span data-stu-id="d1e36-118">**Container:** A container provides a grouping of a set of blobs.</span></span> <span data-ttu-id="d1e36-119">Tutti i BLOB devono trovarsi in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="d1e36-119">All blobs must be in a container.</span></span> <span data-ttu-id="d1e36-120">In un account può esistere un numero illimitato di contenitori.</span><span class="sxs-lookup"><span data-stu-id="d1e36-120">An account can contain an unlimited number of containers.</span></span> <span data-ttu-id="d1e36-121">In un contenitore può essere archiviato un numero illimitato di BLOB.</span><span class="sxs-lookup"><span data-stu-id="d1e36-121">A container can store an unlimited number of blobs.</span></span> <span data-ttu-id="d1e36-122">Il nome del contenitore deve essere in lettere minuscole.</span><span class="sxs-lookup"><span data-stu-id="d1e36-122">Note that the container name must be lowercase.</span></span>

* <span data-ttu-id="d1e36-123">**BLOB:** file di qualsiasi tipo e dimensione.</span><span class="sxs-lookup"><span data-stu-id="d1e36-123">**Blob:** A file of any type and size.</span></span> <span data-ttu-id="d1e36-124">Archiviazione di Azure offre tre tipi di BLOB: i BLOB in blocchi, i BLOB di pagine e i BLOB di accodamento.</span><span class="sxs-lookup"><span data-stu-id="d1e36-124">Azure Storage offers three types of blobs: block blobs, page blobs, and append blobs.</span></span>
  
    <span data-ttu-id="d1e36-125">*BLOB in blocchi* sono ideali per l'archiviazione di file di testo o file binari, ad esempio i documenti e i file multimediali.</span><span class="sxs-lookup"><span data-stu-id="d1e36-125">*Block blobs* are ideal for storing text or binary files, such as documents and media files.</span></span> <span data-ttu-id="d1e36-126">*BLOB di accodamento* sono simili ai BLOB in blocchi in quanto sono costituiti da blocchi, ma sono ottimizzati per le operazioni di accodamento, in modo che siano utili per gli scenari di registrazione.</span><span class="sxs-lookup"><span data-stu-id="d1e36-126">*Append blobs* are similar to block blobs in that they are made up of blocks, but they are optimized for append operations, so they are useful for logging scenarios.</span></span> <span data-ttu-id="d1e36-127">Un singolo BLOB in blocchi può contenere fino a 50.000 blocchi da al massimo 100 MB ognuno, per una dimensione totale leggermente superiore a 4,75 TB (100 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="d1e36-127">A single block blob can contain up to 50,000 blocks of up to 100 MB each, for a total size of slightly more than 4.75 TB (100 MB X 50,000).</span></span> <span data-ttu-id="d1e36-128">Un singolo BLOB di accodamento può contenere fino a 50.000 blocchi da al massimo 4 MB ognuno, per una dimensione totale leggermente superiore a 195 GB (4 MB X 50.000).</span><span class="sxs-lookup"><span data-stu-id="d1e36-128">A single append blob can contain up to 50,000 blocks of up to 4 MB each, for a total size of slightly more than 195 GB (4 MB X 50,000).</span></span>
  
    <span data-ttu-id="d1e36-129">*BLOB di pagine* possono avere un dimensione di al massimo 1 TB e sono più efficienti per operazioni di lettura/scrittura frequenti.</span><span class="sxs-lookup"><span data-stu-id="d1e36-129">*Page blobs* can be up to 1 TB in size, and are more efficient for frequent read/write operations.</span></span> <span data-ttu-id="d1e36-130">Le macchine virtuali di Azure usano BLOB di pagine come dischi di dati e del sistema operativo.</span><span class="sxs-lookup"><span data-stu-id="d1e36-130">Azure Virtual Machines uses page blobs as OS and data disks.</span></span>
  
    <span data-ttu-id="d1e36-131">Per informazioni sulla denominazione di contenitori e BLOB, vedere l'articolo relativo alla [denominazione e riferimento a contenitori, BLOB e metadati](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span><span class="sxs-lookup"><span data-stu-id="d1e36-131">For details about naming containers and blobs, see [Naming and Referencing Containers, Blobs, and Metadata](/rest/api/storageservices/Naming-and-Referencing-Containers--Blobs--and-Metadata).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d1e36-132">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d1e36-132">Next steps</span></span>

* [<span data-ttu-id="d1e36-133">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="d1e36-133">Create a storage account</span></span>](../common/storage-create-storage-account.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="d1e36-134">Introduzione all'archivio BLOB di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="d1e36-134">Getting started with Blob storage using .NET</span></span>](storage-dotnet-how-to-use-blobs.md)