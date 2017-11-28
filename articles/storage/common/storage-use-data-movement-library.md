---
title: aaaTransfer dati con hello libreria lo spostamento dei dati di archiviazione di Microsoft Azure | Documenti Microsoft
description: Utilizzare hello raccolta lo spostamento dei dati toomove o copia dati tooor dal contenuto di blob e file. Copiare i dati tooAzure archiviazione da file locali, o copiare dati in o tra gli account di archiviazione. Migrare facilmente l'archiviazione di tooAzure di dati.
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 9aec6cb171f794cc6ca432938ce499079e7dfdec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="d0bdf-105">Trasferimento dati con hello libreria lo spostamento dei dati di archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d0bdf-105">Transfer Data with hello Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="d0bdf-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d0bdf-106">Overview</span></span>
<span data-ttu-id="d0bdf-107">Hello libreria lo spostamento dei dati di archiviazione di Microsoft Azure è una libreria di multipiattaforma open source che è progettata per prestazioni elevate di caricamento, download e la copia di BLOB di archiviazione di Azure e i file.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-107">hello Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="d0bdf-108">Questa libreria è hello dati lo spostamento dei framework di base che alimenta [AzCopy](../storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-108">This library is hello core data movement framework that powers [AzCopy](../storage-use-azcopy.md).</span></span> <span data-ttu-id="d0bdf-109">Hello raccolta lo spostamento dei dati fornisce pratici metodi che non sono disponibili i tradizionali [.NET Azure Storage Client Library](../blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-109">hello Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](../blobs/storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="d0bdf-110">Ciò include hello possibilità tooset hello numero di operazioni parallele, tenere traccia dell'avanzamento di trasferimento, riprendere facilmente un trasferimento annullato e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-110">This includes hello ability tooset hello number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="d0bdf-111">La libreria usa inoltre .NET Core, utile quando si creano app .NET per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="d0bdf-112">toolearn ulteriori informazioni su .NET Core, vedere toohello [documentazione di .NET Core](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-112">toolearn more about .NET Core, refer toohello [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="d0bdf-113">La libreria è compatibile anche con le app .NET Framework tradizionali per Windows.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="d0bdf-114">Questo documento viene illustrato come un .NET Core toocreate console applicazione che viene eseguito in Windows, Linux e macOS che esegue hello seguenti scenari:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-114">This document demonstrates how toocreate a .NET Core console application that that runs on Windows, Linux, and macOS and performs hello following scenarios:</span></span>

- <span data-ttu-id="d0bdf-115">Caricare file e directory tooBlob archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-115">Upload files and directories tooBlob Storage.</span></span>
- <span data-ttu-id="d0bdf-116">Definire il numero di hello di operazioni parallele durante il trasferimento dei dati.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-116">Define hello number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="d0bdf-117">Monitorare lo stato del trasferimento dati.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-117">Track data transfer progress.</span></span>
- <span data-ttu-id="d0bdf-118">Riprendere un trasferimento dati annullato.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="d0bdf-119">Copia del file da URL tooBlob archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-119">Copy file from URL tooBlob Storage.</span></span> 
- <span data-ttu-id="d0bdf-120">Copiare da archiviazione Blob tooBlob archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-120">Copy from Blob Storage tooBlob Storage.</span></span>

<span data-ttu-id="d0bdf-121">**Che cosa occorre:**</span><span class="sxs-lookup"><span data-stu-id="d0bdf-121">**What you need:**</span></span>

* [<span data-ttu-id="d0bdf-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d0bdf-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="d0bdf-123">Un [account di archiviazione di Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="d0bdf-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="d0bdf-124">Questa guida presuppone che si abbia già familiarità con [Archiviazione di Azure](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="d0bdf-125">Se durante la lettura, non hello [tooAzure introduzione archiviazione](storage-introduction.md) documentazione è utile.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-125">If not, reading hello [Introduction tooAzure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="d0bdf-126">In particolare, è necessario troppo[creare un account di archiviazione](storage-create-storage-account.md#create-a-storage-account) toostart utilizzando hello raccolta lo spostamento dei dati.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-126">Most importantly, you need too[create a Storage account](storage-create-storage-account.md#create-a-storage-account) toostart using hello Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="d0bdf-127">Configurazione</span><span class="sxs-lookup"><span data-stu-id="d0bdf-127">Setup</span></span>  

1. <span data-ttu-id="d0bdf-128">Visitare hello [Guida all'installazione di .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-128">Visit hello [.NET Core Installation Guide](https://www.microsoft.com/net/core) tooinstall .NET Core.</span></span> <span data-ttu-id="d0bdf-129">Quando si seleziona l'ambiente, scegliere l'opzione della riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-129">When selecting your environment, choose hello command-line option.</span></span> 
2. <span data-ttu-id="d0bdf-130">Dalla riga di comando hello, creare una directory per il progetto.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-130">From hello command line, create a directory for your project.</span></span> <span data-ttu-id="d0bdf-131">Spostarsi in questa directory, quindi digitare `dotnet new` progetto console c# toocreate.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-131">Navigate into this directory, then type `dotnet new` toocreate a C# console project.</span></span>
3. <span data-ttu-id="d0bdf-132">Aprire la directory in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="d0bdf-133">Questo passaggio può essere completato rapidamente tramite la riga di comando hello digitando `code .`.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-133">This step can be quickly done via hello command line by typing `code .`.</span></span>  
4. <span data-ttu-id="d0bdf-134">Installare hello [c# estensione](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) da Visual Studio Marketplace di codice hello.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-134">Install hello [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from hello Visual Studio Code Marketplace.</span></span> <span data-ttu-id="d0bdf-135">Riavviare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="d0bdf-136">A questo punto compariranno due prompt.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="d0bdf-137">Uno viene utilizzata per aggiungere "toobuild asset necessari e debug".</span><span class="sxs-lookup"><span data-stu-id="d0bdf-137">One is for adding "required assets toobuild and debug."</span></span> <span data-ttu-id="d0bdf-138">Fare clic su "Sì".</span><span class="sxs-lookup"><span data-stu-id="d0bdf-138">Click "yes."</span></span> <span data-ttu-id="d0bdf-139">L'altro prompt consente di ripristinare le dipendenze non risolte.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="d0bdf-140">Fare clic su "Ripristina".</span><span class="sxs-lookup"><span data-stu-id="d0bdf-140">Click "restore."</span></span>
6. <span data-ttu-id="d0bdf-141">L'applicazione dovrebbe contenere un `launch.json` file hello `.vscode` directory.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-141">Your application should now contain a `launch.json` file under hello `.vscode` directory.</span></span> <span data-ttu-id="d0bdf-142">In questo file, modificare hello `externalConsole` valore troppo`true`.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-142">In this file, change hello `externalConsole` value too`true`.</span></span>
7. <span data-ttu-id="d0bdf-143">Codice di Visual Studio consente di applicazioni .NET Core toodebug.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-143">Visual Studio Code allows you toodebug .NET Core applications.</span></span> <span data-ttu-id="d0bdf-144">Riscontri `F5` toorun l'applicazione e verificare il funzionamento del programma di installazione.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-144">Hit `F5` toorun your application and verify that your setup is working.</span></span> <span data-ttu-id="d0bdf-145">Dovrebbe essere visualizzato "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="d0bdf-145">You should see "Hello World!"</span></span> <span data-ttu-id="d0bdf-146">console toohello stampato.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-146">printed toohello console.</span></span> 

## <a name="add-data-movement-library-tooyour-project"></a><span data-ttu-id="d0bdf-147">Aggiungi progetto tooyour raccolta lo spostamento dei dati</span><span class="sxs-lookup"><span data-stu-id="d0bdf-147">Add Data Movement Library tooyour project</span></span>

1. <span data-ttu-id="d0bdf-148">Aggiungere hello la versione più recente di hello raccolta lo spostamento dei dati toohello `dependencies` sezione il `project.json` file.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-148">Add hello latest version of hello Data Movement Library toohello `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="d0bdf-149">Al momento della scrittura hello sarebbe questa versione`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="d0bdf-149">At hello time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="d0bdf-150">Aggiungere `"portable-net45+win8"` toohello `imports` sezione.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-150">Add `"portable-net45+win8"` toohello `imports` section.</span></span> 
3. <span data-ttu-id="d0bdf-151">Una richiesta deve essere visualizzato toorestore il progetto.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-151">A prompt should display toorestore your project.</span></span> <span data-ttu-id="d0bdf-152">Fare clic su pulsante "Ripristina" hello.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-152">Click hello "restore" button.</span></span> <span data-ttu-id="d0bdf-153">È inoltre possibile ripristinare il progetto dalla riga di comando hello digitando il comando hello `dotnet restore` in hello directory radice del progetto.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-153">You can also restore your project from hello command line by typing hello command `dotnet restore` in hello root of your project directory.</span></span>

<span data-ttu-id="d0bdf-154">Modificare `project.json`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-154">Modify `project.json`:</span></span>

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a><span data-ttu-id="d0bdf-155">Impostare scheletro hello dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d0bdf-155">Set up hello skeleton of your application</span></span>
<span data-ttu-id="d0bdf-156">Innanzitutto, è necessario Hello è impostato il codice di "scheletro" hello dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-156">hello first thing we do is set up hello "skeleton" code of our application.</span></span> <span data-ttu-id="d0bdf-157">Questo codice richiede la chiave account e nome di un account di archiviazione e utilizza tali toocreate credenziali un `CloudStorageAccount` oggetto.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-157">This code prompts us for a Storage account name and account key and uses those credentials toocreate a `CloudStorageAccount` object.</span></span> <span data-ttu-id="d0bdf-158">Questo oggetto è toointeract utilizzato con l'account di archiviazione in tutti gli scenari di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-158">This object is used toointeract with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="d0bdf-159">codice Hello richiede inoltre ci tipo hello toochoose dell'operazione di trasferimento desideriamo tooexecute.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-159">hello code also prompts us toochoose hello type of transfer operation we would like tooexecute.</span></span> 

<span data-ttu-id="d0bdf-160">Modificare `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-160">Modify `Program.cs`:</span></span>

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a><span data-ttu-id="d0bdf-161">Trasferimento file locale tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="d0bdf-161">Transfer local file tooAzure Blob</span></span>
<span data-ttu-id="d0bdf-162">Aggiungere metodi hello `GetSourcePath` e `GetBlob` troppo`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-162">Add hello methods `GetSourcePath` and `GetBlob` too`Program.cs`:</span></span>

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

<span data-ttu-id="d0bdf-163">Modificare hello `TransferLocalFileToAzureBlob` metodo:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-163">Modify hello `TransferLocalFileToAzureBlob` method:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="d0bdf-164">Questo codice richiede ci hello percorso tooa locale file, nome hello di un contenitore di nuovo o esistente e il nome di hello di un nuovo blob.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-164">This code prompts us for hello path tooa local file, hello name of a new or existing container, and hello name of a new blob.</span></span> <span data-ttu-id="d0bdf-165">Hello `TransferManager.UploadAsync` metodo esegue il caricamento di hello utilizzando le informazioni.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-165">hello `TransferManager.UploadAsync` method performs hello upload using this information.</span></span> 

<span data-ttu-id="d0bdf-166">Riscontri `F5` toorun l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-166">Hit `F5` toorun your application.</span></span> <span data-ttu-id="d0bdf-167">Per verificare se si è verificato durante il caricamento di hello visualizzando l'account di archiviazione con hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-167">You can verify that hello upload occurred by viewing your Storage account with hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="d0bdf-168">Impostare il numero di operazioni parallele</span><span class="sxs-lookup"><span data-stu-id="d0bdf-168">Set number of parallel operations</span></span>
<span data-ttu-id="d0bdf-169">Un'ottima funzionalità offerte da hello che raccolta lo spostamento dei dati sono hello possibilità tooset hello di velocità effettiva di trasferimento dei dati di operazioni parallele tooincrease hello.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-169">A great feature offered by hello Data Movement Library is hello ability tooset hello number of parallel operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="d0bdf-170">Per impostazione predefinita, hello raccolta lo spostamento dei dati imposta il numero di hello di operazioni parallele too8 * hello numero di core nel computer.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-170">By default, hello Data Movement Library sets hello number of parallel operations too8 * hello number of cores on your machine.</span></span> 

<span data-ttu-id="d0bdf-171">Tenere presente che molte operazioni parallele in un ambiente di larghezza di banda bassa possono sovraccaricare la connessione di rete hello ed effettivamente impedire completamente il completamento delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm hello network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="d0bdf-172">È necessario tooexperiment con questa impostazione di toodetermine ciò che funziona meglio in base la larghezza di banda di rete disponibile.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-172">You'll need tooexperiment with this setting toodetermine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="d0bdf-173">Aggiungere codice che consente di elaborare il numero hello tooset delle operazioni parallele.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-173">Let's add some code that allows us tooset hello number of parallel operations.</span></span> <span data-ttu-id="d0bdf-174">Aggiungere anche il codice che verifica il tempo necessario per toocomplete trasferimento hello.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-174">Let's also add code that times how long it takes for hello transfer toocomplete.</span></span>

<span data-ttu-id="d0bdf-175">Aggiungere un `SetNumberOfParallelOperations` metodo troppo`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-175">Add a `SetNumberOfParallelOperations` method too`Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="d0bdf-176">Modificare hello `ExecuteChoice` toouse metodo `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-176">Modify hello `ExecuteChoice` method toouse `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

<span data-ttu-id="d0bdf-177">Modificare hello `TransferLocalFileToAzureBlob` toouse metodo timer:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-177">Modify hello `TransferLocalFileToAzureBlob` method toouse a timer:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a><span data-ttu-id="d0bdf-178">Monitorare lo stato del trasferimento dati</span><span class="sxs-lookup"><span data-stu-id="d0bdf-178">Track transfer progress</span></span>
<span data-ttu-id="d0bdf-179">Conoscere il tempo impiegato per il nostro tootransfer dati è molto utile.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-179">Knowing how long it took for our data tootransfer is great.</span></span> <span data-ttu-id="d0bdf-180">Tuttavia, in corso hello toosee in grado del trasferimento *durante* operazione di trasferimento hello sarebbe ancora migliore.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-180">However, being able toosee hello progress of our transfer *during* hello transfer operation would be even better.</span></span> <span data-ttu-id="d0bdf-181">tooachieve questo scenario, è necessario toocreate un `TransferContext` oggetto.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-181">tooachieve this scenario, we need toocreate a `TransferContext` object.</span></span> <span data-ttu-id="d0bdf-182">Hello `TransferContext` oggetto sono disponibili in due forme: `SingleTransferContext` e `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-182">hello `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="d0bdf-183">Hello precedente è per il trasferimento di un singolo file (ovvero stiamo ora) e hello quest'ultimo è per il trasferimento di una directory di file (che si aggiungono più avanti).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-183">hello former is for transferring a single file (which is what we're doing now) and hello latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="d0bdf-184">Aggiungere metodi hello `GetSingleTransferContext` e `GetDirectoryTransferContext` troppo`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-184">Add hello methods `GetSingleTransferContext` and `GetDirectoryTransferContext` too`Program.cs`:</span></span> 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

<span data-ttu-id="d0bdf-185">Modificare hello `TransferLocalFileToAzureBlob` toouse metodo `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-185">Modify hello `TransferLocalFileToAzureBlob` method toouse `GetSingleTransferContext`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="d0bdf-186">Riprendere un trasferimento annullato</span><span class="sxs-lookup"><span data-stu-id="d0bdf-186">Resume a canceled transfer</span></span>
<span data-ttu-id="d0bdf-187">Un'altra caratteristica interessante offerta hello raccolta lo spostamento dei dati è hello possibilità tooresume un trasferimento annullato.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-187">Another convenient feature offered by hello Data Movement Library is hello ability tooresume a canceled transfer.</span></span> <span data-ttu-id="d0bdf-188">Aggiungere codice che consente il trasferimento di hello Annulla tootemporarily digitando `c`e quindi riprendere il trasferimento di hello 3 secondi in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-188">Let's add some code that allows us tootemporarily cancel hello transfer by typing `c`, and then resume hello transfer 3 seconds later.</span></span>

<span data-ttu-id="d0bdf-189">Modificare `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="d0bdf-190">Fino a questo punto, il nostro `checkpoint` valore è sempre stato impostato troppo`null`.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-190">Up until now, our `checkpoint` value has always been set too`null`.</span></span> <span data-ttu-id="d0bdf-191">A questo punto, se si annulla il trasferimento di hello, è recuperare l'ultimo checkpoint di hello del nostro trasferimento, quindi utilizzare questo nuovo checkpoint in questo contesto di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-191">Now, if we cancel hello transfer, we retrieve hello last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-tooazure-blob-directory"></a><span data-ttu-id="d0bdf-192">Trasferimento della directory Blob tooAzure directory locale</span><span class="sxs-lookup"><span data-stu-id="d0bdf-192">Transfer local directory tooAzure Blob directory</span></span>
<span data-ttu-id="d0bdf-193">Sarebbe deludente se hello raccolta lo spostamento dei dati può trasferire un solo file alla volta.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-193">It would be disappointing if hello Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="d0bdf-194">Fortunatamente, non è in questo caso hello.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-194">Luckily, this is not hello case.</span></span> <span data-ttu-id="d0bdf-195">Hello raccolta lo spostamento dei dati fornisce hello possibilità tootransfer una directory di file e tutte le relative sottodirectory.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-195">hello Data Movement Library provides hello ability tootransfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="d0bdf-196">Aggiungere codice che consente di elaborare toodo proprio questo.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-196">Let's add some code that allows us toodo just that.</span></span>

<span data-ttu-id="d0bdf-197">Innanzitutto, aggiungere il metodo hello `GetBlobDirectory` troppo`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-197">First, add hello method `GetBlobDirectory` too`Program.cs`:</span></span>

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

<span data-ttu-id="d0bdf-198">Poi modificare `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="d0bdf-199">Esistono alcune differenze tra questo metodo e il metodo hello per il caricamento di un singolo file.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-199">There are a few differences between this method and hello method for uploading a single file.</span></span> <span data-ttu-id="d0bdf-200">Ora utilizziamo `TransferManager.UploadDirectoryAsync` hello e `getDirectoryTransferContext` metodo creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-200">We're now using `TransferManager.UploadDirectoryAsync` and hello `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="d0bdf-201">Inoltre, sono disponibili un `options` valore tooour operazione di caricamento, che consente tooindicate che si vuole che le sottodirectory tooinclude nella funzione di caricamento.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-201">In addition, we now provide an `options` value tooour upload operation, which allows us tooindicate that we want tooinclude subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-tooazure-blob"></a><span data-ttu-id="d0bdf-202">Copia del file da tooAzure URL Blob</span><span class="sxs-lookup"><span data-stu-id="d0bdf-202">Copy file from URL tooAzure Blob</span></span>
<span data-ttu-id="d0bdf-203">A questo punto, aggiungere codice che consente di elaborare un file da un Blob di Azure di tooan URL toocopy.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-203">Now, let's add code that allows us toocopy a file from a URL tooan Azure Blob.</span></span> 

<span data-ttu-id="d0bdf-204">Modificare `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="d0bdf-205">Un importante questa funzionalità viene usata quando è necessario toomove dati da un altro cloud service (ad esempio AWS) tooAzure.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-205">One important use case for this feature is when you need toomove data from another cloud service (e.g. AWS) tooAzure.</span></span> <span data-ttu-id="d0bdf-206">Se si dispone di un URL che fornisce l'accesso toohello risorse, è possibile spostare facilmente tale risorsa nel BLOB di Azure tramite hello `TransferManager.CopyAsync` metodo.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-206">As long as you have a URL that gives you access toohello resource, you can easily move that resource into Azure Blobs by using hello `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="d0bdf-207">Questo metodo introduce anche un nuovo parametro booleano.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="d0bdf-208">Impostando questo parametro troppo`true` indica che si desidera copia toodo un ambiente asincrono sul lato server.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-208">Setting this parameter too`true` indicates that we want toodo an asynchronous server-side copy.</span></span> <span data-ttu-id="d0bdf-209">Impostando questo parametro troppo`false` indica una copia sincrona, vale a dire risorse hello sono computer locale tooour scaricati in primo luogo, quindi caricato tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-209">Setting this parameter too`false` indicates a synchronous copy - meaning hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="d0bdf-210">Tuttavia, la copia sincrona è attualmente disponibile solo per la copia da un tooanother di risorse di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-210">However, synchronous copy is currently only available for copying from one Azure Storage resource tooanother.</span></span> 

## <a name="transfer-azure-blob-tooazure-blob"></a><span data-ttu-id="d0bdf-211">Trasferimento Blob di Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="d0bdf-211">Transfer Azure Blob tooAzure Blob</span></span>
<span data-ttu-id="d0bdf-212">Un'altra funzionalità fornita in modo univoco da hello raccolta lo spostamento dei dati è hello possibilità toocopy da uno tooanother di risorse di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-212">Another feature that's uniquely provided by hello Data Movement Library is hello ability toocopy from one Azure Storage resource tooanother.</span></span> 

<span data-ttu-id="d0bdf-213">Modificare `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="d0bdf-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

<span data-ttu-id="d0bdf-214">In questo esempio viene impostato parametro booleano hello in `TransferManager.CopyAsync` troppo`false` tooindicate che toodo una copia sincrona.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-214">In this example, we set hello boolean parameter in `TransferManager.CopyAsync` too`false` tooindicate that we want toodo a synchronous copy.</span></span> <span data-ttu-id="d0bdf-215">Ciò significa che risorse hello sono computer locale tooour scaricato, quindi caricato tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-215">This means that hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="d0bdf-216">l'opzione copia sincrono Hello è tooensure un ottimo modo che l'operazione di copia ha una velocità coerenza.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-216">hello synchronous copy option is a great way tooensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="d0bdf-217">Al contrario, la velocità di hello di una copia lato server asincrona è dipendente da hello disponibile larghezza di banda sul server hello, che possono variare.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-217">In contrast, hello speed of an asynchronous server-side copy is dependent on hello available network bandwidth on hello server, which can fluctuate.</span></span> <span data-ttu-id="d0bdf-218">Tuttavia, copia sincrona può generare uscita ulteriori costi rispetto tooasynchronous copia.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-218">However, synchronous copy may generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="d0bdf-219">Hello approccio migliore consiste toouse copia sincrona in una macchina virtuale di Azure in hello stessa area del costo di uscita origine tooavoid account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-219">hello recommended approach is toouse synchronous copy in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d0bdf-220">Conclusioni</span><span class="sxs-lookup"><span data-stu-id="d0bdf-220">Conclusion</span></span>
<span data-ttu-id="d0bdf-221">L'applicazione per lo spostamento dei dati ora è completa.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-221">Our data movement application is now complete.</span></span> <span data-ttu-id="d0bdf-222">[Nell'esempio di codice completo Hello è disponibile in GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-222">[hello full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d0bdf-223">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0bdf-223">Next steps</span></span>
<span data-ttu-id="d0bdf-224">In questa guida introduttiva è stata creata un'applicazione in grado di interagire con Archiviazione di Azure e che può essere eseguita su Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="d0bdf-225">Questa guida introduttiva ha trattato principalmente dell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="d0bdf-226">Tuttavia, questa conoscenza stesso può essere applicato tooFile archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d0bdf-226">However, this same knowledge can be applied tooFile Storage.</span></span> <span data-ttu-id="d0bdf-227">toolearn, estrarre [la documentazione di riferimento libreria lo spostamento dei dati di archiviazione Azure](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="d0bdf-227">toolearn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../../includes/storage-try-azure-tools-blobs.md)]




