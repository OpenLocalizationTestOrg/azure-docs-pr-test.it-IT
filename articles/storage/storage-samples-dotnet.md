---
title: Esempi di Archiviazione di Azure che usano .NET | Microsoft Docs
description: Visualizzare, scaricare ed eseguire codici di esempio e applicazioni per l'Archiviazione di Azure. Individuare esempi introduttivi per BLOB, code, tabelle e file usando le librerie client di archiviazione .NET.
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
ms.openlocfilehash: d2b6b3d9483f230ad25ae47255a4f28c1a67e064
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="azure-storage-samples-using-net"></a><span data-ttu-id="700a6-104">Esempi di Archiviazione di Azure che usano .NET</span><span class="sxs-lookup"><span data-stu-id="700a6-104">Azure Storage samples using .NET</span></span>

## <a name="net-sample-index"></a><span data-ttu-id="700a6-105">Indice degli esempi .NET</span><span class="sxs-lookup"><span data-stu-id="700a6-105">.NET sample index</span></span>

<span data-ttu-id="700a6-106">La tabella seguente fornisce una panoramica del repository di esempi e degli scenari presentati in ogni esempio.</span><span class="sxs-lookup"><span data-stu-id="700a6-106">The following table provides an overview of our samples repository and the scenarios covered in each sample.</span></span> <span data-ttu-id="700a6-107">Fare clic sui collegamenti per visualizzare il codice di esempio corrispondente in GitHub.</span><span class="sxs-lookup"><span data-stu-id="700a6-107">Click on the links to view the corresponding sample code in GitHub.</span></span>

<table style="font-size:90%"><thead><tr><th style="font-size:110%"><span data-ttu-id="700a6-108">Endpoint</span><span class="sxs-lookup"><span data-stu-id="700a6-108">Endpoint</span></span></th><th style="font-size:110%"><span data-ttu-id="700a6-109">Scenario</span><span class="sxs-lookup"><span data-stu-id="700a6-109">Scenario</span></span></th><th style="font-size:110%"><span data-ttu-id="700a6-110">Codice di esempio</span><span class="sxs-lookup"><span data-stu-id="700a6-110">Sample Code</span></span></th></tr></thead><tbody> 
<tr> 
<td rowspan="16"><span data-ttu-id="700a6-111"><b>BLOB</b></span><span class="sxs-lookup"><span data-stu-id="700a6-111"><b>Blob</b></span></span></td>
<td><span data-ttu-id="700a6-112">Append Blob</span><span class="sxs-lookup"><span data-stu-id="700a6-112">Append Blob</span></span></td> 
<td><span data-ttu-id="700a6-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a> (Esempio di metodo CloudBlobContainer.GetAppendBlobReference)</span><span class="sxs-lookup"><span data-stu-id="700a6-113"><a href="https://msdn.microsoft.com/en-us/library/microsoft.windowsazure.storage.blob.cloudblobcontainer.getappendblobreference.aspx">CloudBlobContainer.GetAppendBlobReference Method Example</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-114">BLOB in blocchi</span><span class="sxs-lookup"><span data-stu-id="700a6-114">Block Blob</span></span></td>
<td><span data-ttu-id="700a6-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span><span class="sxs-lookup"><span data-stu-id="700a6-115"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="700a6-116">Crittografia lato client</span><span class="sxs-lookup"><span data-stu-id="700a6-116">Client-Side Encryption</span></span></td>
<td><span data-ttu-id="700a6-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a> (Esempi di crittografia dei BLOB)</span><span class="sxs-lookup"><span data-stu-id="700a6-117"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/BlobGettingStarted/Program.cs">Blob Encryption Samples</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="700a6-118">Copia di BLOB</span><span class="sxs-lookup"><span data-stu-id="700a6-118">Copy Blob</span></span></td>
<td><span data-ttu-id="700a6-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="700a6-119"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="700a6-120">Creazione contenitore</span><span class="sxs-lookup"><span data-stu-id="700a6-120">Create Container</span></span></td>
<td><span data-ttu-id="700a6-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span><span class="sxs-lookup"><span data-stu-id="700a6-121"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="700a6-122">Eliminazione BLOB</span><span class="sxs-lookup"><span data-stu-id="700a6-122">Delete Blob</span></span></td>
<td><span data-ttu-id="700a6-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span><span class="sxs-lookup"><span data-stu-id="700a6-123"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="700a6-124">Eliminazione contenitore</span><span class="sxs-lookup"><span data-stu-id="700a6-124">Delete Container</span></span></td>
<td><span data-ttu-id="700a6-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="700a6-125"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="700a6-126">Metadati/proprietà/statistiche BLOB</span><span class="sxs-lookup"><span data-stu-id="700a6-126">Blob Metadata/Properties/Stats</span></span></td>
<td><span data-ttu-id="700a6-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="700a6-127"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="700a6-128">ACL/metadati/proprietà contenitore</span><span class="sxs-lookup"><span data-stu-id="700a6-128">Container ACL/Metadata/Properties</span></span></td>
<td><span data-ttu-id="700a6-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span><span class="sxs-lookup"><span data-stu-id="700a6-129"><a href="https://github.com/Azure-Samples/storage-blobs-dotnet-webapp/blob/master/WebApp-Storage-DotNet/Controllers/HomeController.cs">Azure Blob Storage Photo Gallery Web Application</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="700a6-130">Ottenere intervalli di pagine</span><span class="sxs-lookup"><span data-stu-id="700a6-130">Get Page Ranges</span></span></td>
<td><span data-ttu-id="700a6-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="700a6-131"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="700a6-132">BLOB/contenitore di lease</span><span class="sxs-lookup"><span data-stu-id="700a6-132">Lease Blob/Container</span></span></td>
<td><span data-ttu-id="700a6-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="700a6-133"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="700a6-134">Elenco BLOB/contenitore</span><span class="sxs-lookup"><span data-stu-id="700a6-134">List Blob/Container</span></span></td>
<td><span data-ttu-id="700a6-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="700a6-135"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr> 
<tr> 
<td><span data-ttu-id="700a6-136">BLOB di pagine</span><span class="sxs-lookup"><span data-stu-id="700a6-136">Page Blob</span></span></td>
<td><span data-ttu-id="700a6-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="700a6-137"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/GettingStarted.cs">Getting Started with Blobs</a></span></span></td>
</tr>
<tr> 
<td><span data-ttu-id="700a6-138">SAS</span><span class="sxs-lookup"><span data-stu-id="700a6-138">SAS</span></span></td>
<td><span data-ttu-id="700a6-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="700a6-139"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>   
<tr> 
<td><span data-ttu-id="700a6-140">Proprietà del servizio</span><span class="sxs-lookup"><span data-stu-id="700a6-140">Service Properties</span></span></td>
<td><span data-ttu-id="700a6-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a> (Introduzione ai BLOB)</span><span class="sxs-lookup"><span data-stu-id="700a6-141"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-getting-started/blob/master/BlobStorage/Advanced.cs">Getting Started with Blobs</a></span></span></td>
</tr>           
<tr> 
<td><span data-ttu-id="700a6-142">Snapshot di BLOB</span><span class="sxs-lookup"><span data-stu-id="700a6-142">Snapshot Blob</span></span></td>
<td><span data-ttu-id="700a6-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup dei dischi delle macchine virtuali di Azure con snapshot incrementali</a></span><span class="sxs-lookup"><span data-stu-id="700a6-143"><a href="https://github.com/Azure-Samples/storage-blob-dotnet-back-up-with-incremental-snapshots/blob/master/Program.cs">Backup Azure Virtual Machine Disks with Incremental Snapshots</a></span></span></td>
</tr> 
<tr> 
<td rowspan="9"><span data-ttu-id="700a6-144"><b>File</b></span><span class="sxs-lookup"><span data-stu-id="700a6-144"><b>File</b></span></span></td>
<td><span data-ttu-id="700a6-145">Creazione condivisioni/directory/file</span><span class="sxs-lookup"><span data-stu-id="700a6-145">Create Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="700a6-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="700a6-146"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="700a6-147">Eliminazione condivisioni/directory/file</span><span class="sxs-lookup"><span data-stu-id="700a6-147">Delete Shares/Directories/Files</span></span></td> 
<td><span data-ttu-id="700a6-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-148"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/master/FileStorage/GettingStarted.cs">Getting Started with Azure File Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-149">Proprietà/metadati di directory</span><span class="sxs-lookup"><span data-stu-id="700a6-149">Directory Properties/Metadata</span></span></td> 
<td><span data-ttu-id="700a6-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="700a6-150"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-151">Download di file</span><span class="sxs-lookup"><span data-stu-id="700a6-151">Download Files</span></span></td> 
<td><span data-ttu-id="700a6-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="700a6-152"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-153">Proprietà/metadati/metriche di file</span><span class="sxs-lookup"><span data-stu-id="700a6-153">File Properties/Metadata/Metrics</span></span></td> 
<td><span data-ttu-id="700a6-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="700a6-154"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-155">Proprietà del servizio file</span><span class="sxs-lookup"><span data-stu-id="700a6-155">File Service Properties</span></span></td> 
<td><span data-ttu-id="700a6-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="700a6-156"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-157">Elenco di directory e file</span><span class="sxs-lookup"><span data-stu-id="700a6-157">List Directories and Files</span></span></td> 
<td><span data-ttu-id="700a6-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="700a6-158"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/VisualStudioQuickStarts/DataFileStorage/Program.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="700a6-159">Elenco di condivisioni</span><span class="sxs-lookup"><span data-stu-id="700a6-159">List Shares</span></span></td> 
<td><span data-ttu-id="700a6-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="700a6-160"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td><span data-ttu-id="700a6-161">Condivisione di proprietà/metadati/statistiche</span><span class="sxs-lookup"><span data-stu-id="700a6-161">Share Properties/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="700a6-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a> (Esempio di archiviazione file .NET in Archiviazione di Azure)</span><span class="sxs-lookup"><span data-stu-id="700a6-162"><a href="https://github.com/Azure-Samples/storage-file-dotnet-getting-started/blob/9f12304b2f5f5472a1c87c1e21be4af5661ac043/FileStorage/Advanced.cs">Azure Storage .NET File Storage Sample</a></span></span></td> 
</tr>
<tr> 
<td rowspan="8"><span data-ttu-id="700a6-163"><b>Coda</b></span><span class="sxs-lookup"><span data-stu-id="700a6-163"><b>Queue</b></span></span></td>
<td><span data-ttu-id="700a6-164">Aggiunta di un messaggio</span><span class="sxs-lookup"><span data-stu-id="700a6-164">Add Message</span></span></td> 
<td><span data-ttu-id="700a6-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-165"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-166">Crittografia lato client</span><span class="sxs-lookup"><span data-stu-id="700a6-166">Client-Side Encryption</span></span></td> 
<td><span data-ttu-id="700a6-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a> (Crittografia lato client della coda di Archiviazione di Azure .NET)</span><span class="sxs-lookup"><span data-stu-id="700a6-167"><a href="https://github.com/Azure/azure-storage-net/blob/master/Samples/GettingStarted/EncryptionSamples/QueueGettingStarted/Program.cs">Azure Storage .NET Queue Client-Side Encryption</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-168">Creazione di code</span><span class="sxs-lookup"><span data-stu-id="700a6-168">Create Queues</span></span></td> 
<td><span data-ttu-id="700a6-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-169"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-170">Eliminazione di messaggio/coda</span><span class="sxs-lookup"><span data-stu-id="700a6-170">Delete Message/Queue</span></span></td> 
<td><span data-ttu-id="700a6-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-171"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-172">Visualizzazione di messaggio</span><span class="sxs-lookup"><span data-stu-id="700a6-172">Peek Message</span></span></td> 
<td><span data-ttu-id="700a6-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-173"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-174">ACL/metadati/statistiche di coda</span><span class="sxs-lookup"><span data-stu-id="700a6-174">Queue ACL/Metadata/Stats</span></span></td> 
<td><span data-ttu-id="700a6-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-175"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-176">Proprietà del servizio di accodamento</span><span class="sxs-lookup"><span data-stu-id="700a6-176">Queue Service Properties</span></span></td> 
<td><span data-ttu-id="700a6-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-177"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/Advanced.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-178">Aggiornamento messaggio</span><span class="sxs-lookup"><span data-stu-id="700a6-178">Update Message</span></span></td> 
<td><span data-ttu-id="700a6-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-179"><a href="https://github.com/Azure-Samples/storage-queue-dotnet-getting-started/blob/master/QueueStorage/GettingStarted.cs">Getting Started with Azure Queue Service in .NET</a></span></span></td> 
</tr> 
<tr> 
<td rowspan="7"><span data-ttu-id="700a6-180"><b>Tabella</b></span><span class="sxs-lookup"><span data-stu-id="700a6-180"><b>Table</b></span></span></td>
<td><span data-ttu-id="700a6-181">Creazione di tabella</span><span class="sxs-lookup"><span data-stu-id="700a6-181">Create Table</span></span></td> 
<td><span data-ttu-id="700a6-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestione della concorrenza con l'archiviazione di Azure - Applicazione di esempio</a></span><span class="sxs-lookup"><span data-stu-id="700a6-182"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-183">Eliminazione entità/tabella</span><span class="sxs-lookup"><span data-stu-id="700a6-183">Delete Entity/Table</span></span></td> 
<td><span data-ttu-id="700a6-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introduzione all'archiviazione tabelle di Azure con .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-184"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-185">Inserimento/unione/sostituzione di entità</span><span class="sxs-lookup"><span data-stu-id="700a6-185">Insert/Merge/Replace Entity</span></span></td> 
<td><span data-ttu-id="700a6-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestione della concorrenza con l'archiviazione di Azure - Applicazione di esempio</a></span><span class="sxs-lookup"><span data-stu-id="700a6-186"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-187">Query su entità</span><span class="sxs-lookup"><span data-stu-id="700a6-187">Query Entities</span></span></td> 
<td><span data-ttu-id="700a6-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introduzione all'archiviazione tabelle di Azure con .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-188"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-189">Query su tabelle</span><span class="sxs-lookup"><span data-stu-id="700a6-189">Query Tables</span></span></td> 
<td><span data-ttu-id="700a6-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Introduzione all'archiviazione tabelle di Azure con .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-190"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/BasicSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-191">ACL/proprietà di tabella</span><span class="sxs-lookup"><span data-stu-id="700a6-191">Table ACL/Properties</span></span></td> 
<td><span data-ttu-id="700a6-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Introduzione all'archiviazione tabelle di Azure con .NET</a></span><span class="sxs-lookup"><span data-stu-id="700a6-192"><a href="https://github.com/Azure-Samples/storage-table-dotnet-getting-started/blob/master/TableStorage/AdvancedSamples.cs">Getting Started with Azure Table Storage in .NET</a></span></span></td> 
</tr> 
<tr> 
<td><span data-ttu-id="700a6-193">Aggiornamento di entità</span><span class="sxs-lookup"><span data-stu-id="700a6-193">Update Entity</span></span></td> 
<td><span data-ttu-id="700a6-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Gestione della concorrenza con l'archiviazione di Azure - Applicazione di esempio</a></span><span class="sxs-lookup"><span data-stu-id="700a6-194"><a href="https://code.msdn.microsoft.com/Managing-Concurrency-using-56018114/sourcecode?fileId=123913&pathId=50196262">Managing Concurrency using Azure Storage - Sample Application</a></span></span></td> 
</tr> 
</tbody> 
</table>
<br/>

## <a name="azure-code-samples-library"></a><span data-ttu-id="700a6-195">Libreria di esempi di codice per Azure</span><span class="sxs-lookup"><span data-stu-id="700a6-195">Azure Code Samples library</span></span>

<span data-ttu-id="700a6-196">Per visualizzare la libreria completa, accedere alla libreria [Esempi di codice di Azure](https://azure.microsoft.com/resources/samples/?service=storage), nella quale sono disponibili esempi per Archiviazione di Azure scaricabili ed eseguibili in locale.</span><span class="sxs-lookup"><span data-stu-id="700a6-196">To view the complete sample library, go to the [Azure Code Samples](https://azure.microsoft.com/resources/samples/?service=storage) library, which includes samples for Azure Storage that you can download and run locally.</span></span> <span data-ttu-id="700a6-197">La libreria degli esempi di codice fornisce il codice di esempio in formato .zip.</span><span class="sxs-lookup"><span data-stu-id="700a6-197">The Code Sample Library provides sample code in .zip format.</span></span> <span data-ttu-id="700a6-198">In alternativa, è possibile esplorare e clonare l'archivio GitHub per ogni esempio.</span><span class="sxs-lookup"><span data-stu-id="700a6-198">Alternatively, you can browse and clone the GitHub repository for each sample.</span></span>

[!INCLUDE [storage-dotnet-samples-include](../../includes/storage-dotnet-samples-include.md)]

## <a name="getting-started-guides"></a><span data-ttu-id="700a6-199">Guide introduttive</span><span class="sxs-lookup"><span data-stu-id="700a6-199">Getting started guides</span></span>

<span data-ttu-id="700a6-200">Per istruzioni su come installare e iniziare a utilizzare le librerie client di Archiviazione di Azure, consultare le seguenti guide.</span><span class="sxs-lookup"><span data-stu-id="700a6-200">Check out the following guides if you are looking for instructions on how to install and get started with the Azure Storage Client Libraries.</span></span>

* [<span data-ttu-id="700a6-201">Getting Started with Azure Blob Service in .NET</span><span class="sxs-lookup"><span data-stu-id="700a6-201">Getting Started with Azure Blob Service in .NET</span></span>](storage-dotnet-how-to-use-blobs.md)
* [<span data-ttu-id="700a6-202">Getting Started with Azure Queue Service in .NET</span><span class="sxs-lookup"><span data-stu-id="700a6-202">Getting Started with Azure Queue Service in .NET</span></span>](storage-dotnet-how-to-use-queues.md)
* [<span data-ttu-id="700a6-203">Getting Started with Azure Table Service in .NET</span><span class="sxs-lookup"><span data-stu-id="700a6-203">Getting Started with Azure Table Service in .NET</span></span>](storage-dotnet-how-to-use-tables.md)
* [<span data-ttu-id="700a6-204">Getting Started with Azure File Service in .NET</span><span class="sxs-lookup"><span data-stu-id="700a6-204">Getting Started with Azure File Service in .NET</span></span>](storage-dotnet-how-to-use-files.md)

## <a name="next-steps"></a><span data-ttu-id="700a6-205">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="700a6-205">Next steps</span></span>

<span data-ttu-id="700a6-206">Per informazioni su esempi con altri linguaggi:</span><span class="sxs-lookup"><span data-stu-id="700a6-206">For information on samples for other languages:</span></span>

* <span data-ttu-id="700a6-207">Java: [Esempi di Archiviazione di Azure con Java](storage-samples-java.md)</span><span class="sxs-lookup"><span data-stu-id="700a6-207">Java: [Azure Storage samples using Java](storage-samples-java.md)</span></span>
* <span data-ttu-id="700a6-208">Tutti gli altri linguaggi: [Esempi di archiviazione di Azure](storage-samples.md)</span><span class="sxs-lookup"><span data-stu-id="700a6-208">All other languages: [Azure Storage samples](storage-samples.md)</span></span>
