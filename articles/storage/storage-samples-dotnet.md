---
title: esempi di archiviazione aaaAzure usando .NET | Documenti Microsoft
description: Visualizzare, scaricare ed eseguire codici di esempio e applicazioni per l'Archiviazione di Azure. Individuare l'introduzione di esempi per BLOB, code, tabelle e file, utilizzando le librerie client di archiviazione .NET hello.
services: storage
documentationcenter: na
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage
ms.date: 01/12/2017
ms.author: seguler
ms.openlocfilehash: 9a7055645b0f0658b850f024b8b19ab19840330e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="0ee0f-104">Esempi di Archiviazione di Azure che usano .NET</span><span class="sxs-lookup"><span data-stu-id="0ee0f-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="0ee0f-105">Indice degli esempi .NET</span><span class="sxs-lookup"><span data-stu-id="0ee0f-105">.NET sample index</span></span>

<span data-ttu-id="0ee0f-106">Hello nella tabella seguente viene fornita una panoramica di esempi del repository e hello scenari analizzate in ogni esempio.</span><span class="sxs-lookup"><span data-stu-id="0ee0f-106">hello following table provides an overview of our samples repository and hello scenarios covered in each sample.</span></span> <span data-ttu-id="0ee0f-107">Fare clic su hello collegamenti tooview hello corrispondente codice di esempio in GitHub.</span><span class="sxs-lookup"><span data-stu-id="0ee0f-107">Click on hello links tooview hello corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="0ee0f-108">Endpoint</span><span class="sxs-lookup"><span data-stu-id="0ee0f-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="0ee0f-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="0ee0f-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="0ee0f-110">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="0ee0f-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="0ee0f-111"><b>BLOB</b></span><span class="sxs-lookup"><span data-stu-id="0ee0f-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="0ee0f-112">Append Blob</span><span class="sxs-lookup"><span data-stu-id="0ee0f-112">Append Blob</span></span></td> 
<td><span data-ttu-id="0ee0f-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a> (Esempio di metodo CloudBlobContainer.GetAppendBlobReference)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-114">BLOB in blocchi</span><span class="sxs-lookup"><span data-stu-id="0ee0f-114">Block Blob</span></span></td>
<td><span data-ttu-id="0ee0f-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-116">Crittografia lato client</span><span class="sxs-lookup"><span data-stu-id="0ee0f-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="0ee0f-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a> (Esempi di crittografia dei BLOB)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-118">Copia di BLOB</span><span class="sxs-lookup"><span data-stu-id="0ee0f-118">Copy Blob</span></span></td>
<td><span data-ttu-id="0ee0f-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-120">Creazione contenitore</span><span class="sxs-lookup"><span data-stu-id="0ee0f-120">Create Container</span></span></td>
<td><span data-ttu-id="0ee0f-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-122">Eliminazione BLOB</span><span class="sxs-lookup"><span data-stu-id="0ee0f-122">Delete Blob</span></span></td>
<td><span data-ttu-id="0ee0f-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-124">Eliminazione contenitore</span><span class="sxs-lookup"><span data-stu-id="0ee0f-124">Delete Container</span></span></td>
<td><span data-ttu-id="0ee0f-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-126">Metadati/proprietà/statistiche BLOB</span><span class="sxs-lookup"><span data-stu-id="0ee0f-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="0ee0f-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-128">ACL/metadati/proprietà contenitore</span><span class="sxs-lookup"><span data-stu-id="0ee0f-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="0ee0f-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-130">Ottenere intervalli di pagine</span><span class="sxs-lookup"><span data-stu-id="0ee0f-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="0ee0f-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-132">BLOB/contenitore di lease</span><span class="sxs-lookup"><span data-stu-id="0ee0f-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="0ee0f-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-134">Elenco BLOB/contenitore</span><span class="sxs-lookup"><span data-stu-id="0ee0f-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="0ee0f-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-136">BLOB di pagine</span><span class="sxs-lookup"><span data-stu-id="0ee0f-136">Page Blob</span></span></td>
<td><span data-ttu-id="0ee0f-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="0ee0f-138">SAS</span><span class="sxs-lookup"><span data-stu-id="0ee0f-138">SAS</span></span></td>
<td><span data-ttu-id="0ee0f-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="0ee0f-140">Proprietà del servizio</span><span class="sxs-lookup"><span data-stu-id="0ee0f-140">Service Properties</span></span></td>
<td><span data-ttu-id="0ee0f-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="0ee0f-142">Snapshot di BLOB</span><span class="sxs-lookup"><span data-stu-id="0ee0f-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="0ee0f-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup dei dischi delle macchine virtuali di Azure con snapshot incrementali</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="0ee0f-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="0ee0f-144"><b>File</b></span></span></td>
<td><span data-ttu-id="0ee0f-145">Creazione condivisioni/directory/file</span><span class="sxs-lookup"><span data-stu-id="0ee0f-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="0ee0f-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="0ee0f-147">Eliminazione condivisioni/directory/file</span><span class="sxs-lookup"><span data-stu-id="0ee0f-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="0ee0f-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-149">Proprietà/metadati di directory</span><span class="sxs-lookup"><span data-stu-id="0ee0f-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="0ee0f-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-151">Download di file</span><span class="sxs-lookup"><span data-stu-id="0ee0f-151">Download Files</span></span></td> 
<td><span data-ttu-id="0ee0f-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-153">Proprietà/metadati/metriche di file</span><span class="sxs-lookup"><span data-stu-id="0ee0f-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="0ee0f-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-155">Proprietà del servizio file</span><span class="sxs-lookup"><span data-stu-id="0ee0f-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="0ee0f-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-157">Elenco di directory e file</span><span class="sxs-lookup"><span data-stu-id="0ee0f-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="0ee0f-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="0ee0f-159">Elenco di condivisioni</span><span class="sxs-lookup"><span data-stu-id="0ee0f-159">List Shares</span></span></td> 
<td><span data-ttu-id="0ee0f-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="0ee0f-161">Condivisione di proprietà/metadati/statistiche</span><span class="sxs-lookup"><span data-stu-id="0ee0f-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="0ee0f-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="0ee0f-163"><b>Coda</b></span><span class="sxs-lookup"><span data-stu-id="0ee0f-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="0ee0f-164">Aggiunta di un messaggio</span><span class="sxs-lookup"><span data-stu-id="0ee0f-164">Add Message</span></span></td> 
<td><span data-ttu-id="0ee0f-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-166">Crittografia lato client</span><span class="sxs-lookup"><span data-stu-id="0ee0f-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="0ee0f-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a> (Crittografia lato client della coda di Archiviazione di Azure .NET)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-168">Creazione di code</span><span class="sxs-lookup"><span data-stu-id="0ee0f-168">Create Queues</span></span></td> 
<td><span data-ttu-id="0ee0f-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-170">Eliminazione di messaggio/coda</span><span class="sxs-lookup"><span data-stu-id="0ee0f-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="0ee0f-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-172">Visualizzazione di messaggio</span><span class="sxs-lookup"><span data-stu-id="0ee0f-172">Peek Message</span></span></td> 
<td><span data-ttu-id="0ee0f-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-174">ACL/metadati/statistiche di coda</span><span class="sxs-lookup"><span data-stu-id="0ee0f-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="0ee0f-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-176">Proprietà del servizio di accodamento</span><span class="sxs-lookup"><span data-stu-id="0ee0f-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="0ee0f-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-178">Aggiornamento messaggio</span><span class="sxs-lookup"><span data-stu-id="0ee0f-178">Update Message</span></span></td> 
<td><span data-ttu-id="0ee0f-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="0ee0f-180"><b>Tabella</b></span><span class="sxs-lookup"><span data-stu-id="0ee0f-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="0ee0f-181">Creazione di tabella</span><span class="sxs-lookup"><span data-stu-id="0ee0f-181">Create Table</span></span></td> 
<td><span data-ttu-id="0ee0f-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestione della concorrenza con l'archiviazione di Azure - Applicazione di esempio</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-183">Eliminazione entità/tabella</span><span class="sxs-lookup"><span data-stu-id="0ee0f-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="0ee0f-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introduzione all'archiviazione tabelle di Azure con .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-185">Inserimento/unione/sostituzione di entità</span><span class="sxs-lookup"><span data-stu-id="0ee0f-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="0ee0f-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestione della concorrenza con l'archiviazione di Azure - Applicazione di esempio</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-187">Query su entità</span><span class="sxs-lookup"><span data-stu-id="0ee0f-187">Query Entities</span></span></td> 
<td><span data-ttu-id="0ee0f-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introduzione all'archiviazione tabelle di Azure con .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-189">Query su tabelle</span><span class="sxs-lookup"><span data-stu-id="0ee0f-189">Query Tables</span></span></td> 
<td><span data-ttu-id="0ee0f-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introduzione all'archiviazione tabelle di Azure con .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-191">ACL/proprietà di tabella</span><span class="sxs-lookup"><span data-stu-id="0ee0f-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="0ee0f-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Introduzione all'archiviazione tabelle di Azure con .NET</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="0ee0f-193">Aggiornamento di entità</span><span class="sxs-lookup"><span data-stu-id="0ee0f-193">Update Entity</span></span></td> 
<td><span data-ttu-id="0ee0f-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestione della concorrenza con l'archiviazione di Azure - Applicazione di esempio</a></span><span class="sxs-lookup"><span data-stu-id="0ee0f-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="0ee0f-195">Libreria di esempi di codice per Azure</span><span class="sxs-lookup"><span data-stu-id="0ee0f-195">Azure Code Samples library</span></span>

<span data-ttu-id="0ee0f-196">libreria di esempio completo di hello tooview, andare toohello [esempi di codice di Azure](https://azure.microsoft.com/resources/samples/?service=storage) libreria che sono inclusi esempi per l'archiviazione di Azure che è possibile scaricare ed eseguire in locale.</span><span class="sxs-lookup"><span data-stu-id="0ee0f-196">tooview hello complete sample library, go toohello [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="0ee0f-197">Libreria di esempio di codice Hello fornisce il codice di esempio in formato zip.</span><span class="sxs-lookup"><span data-stu-id="0ee0f-197">hello Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="0ee0f-198">In alternativa, è possibile esplorare e clonare il repository GitHub hello per ogni esempio.</span><span class="sxs-lookup"><span data-stu-id="0ee0f-198">Alternatively, you can browse and clone hello GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="0ee0f-199">Guide introduttive</span><span class="sxs-lookup"><span data-stu-id="0ee0f-199">Getting started guides</span></span>

<span data-ttu-id="0ee0f-200">Estrarre hello seguenti guide se si sta cercando di istruzioni su come tooinstall e iniziare a utilizzare hello le librerie Client di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0ee0f-200">Check out hello following guides if you are looking for instructions on how tooinstall and get started with hello Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="0ee0f-201">Getting Started with Azure Blob Service in .NET</span><span class="sxs-lookup"><span data-stu-id="0ee0f-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="0ee0f-202">Getting Started with Azure Queue Service in .NET</span><span class="sxs-lookup"><span data-stu-id="0ee0f-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="0ee0f-203">Getting Started with Azure Table Service in .NET</span><span class="sxs-lookup"><span data-stu-id="0ee0f-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="0ee0f-204">Getting Started with Azure File Service in .NET</span><span class="sxs-lookup"><span data-stu-id="0ee0f-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="0ee0f-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0ee0f-205">Next steps</span></span>

<span data-ttu-id="0ee0f-206">Per informazioni su esempi con altri linguaggi:</span><span class="sxs-lookup"><span data-stu-id="0ee0f-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="0ee0f-207">Java: [Esempi di Archiviazione di Azure con Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="0ee0f-208">Tutti gli altri linguaggi: [Esempi di archiviazione di Azure](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="0ee0f-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
