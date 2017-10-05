---
title: Trasferire i dati con la libreria per lo spostamento dei dati di Archiviazione di Microsoft Azure | Microsoft Docs
description: Usare la libreria per lo spostamento dei dati per spostare o copiare dati da o verso il contenuto di BLOB e file. Copiare i dati in archiviazione di Azure da file locali o copiare i dati all'interno o tra account di archiviazione. Migrare facilmente i dati in archiviazione di Azure.
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
ms.openlocfilehash: 2ba94e4dd931b6d385101c7dadccfa3583b5296e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="transfer-data-with-the-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="d55ec-105">Trasferire i dati con la libreria per lo spostamento dei dati di Archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="d55ec-105">Transfer Data with the Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="d55ec-106">Panoramica</span><span class="sxs-lookup"><span data-stu-id="d55ec-106">Overview</span></span>
<span data-ttu-id="d55ec-107">La libreria per lo spostamento dei dati di Archiviazione di Microsoft Azure è una libreria open source multi-piattaforma progettata per prestazioni elevate di caricamento, download e copia di file e BLOB di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d55ec-107">The Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="d55ec-108">Questa libreria è il principale framework di spostamento dei dati alla base di [AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="d55ec-108">This library is the core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="d55ec-109">La libreria per lo spostamento dei dati offre metodi pratici che non sono disponibili nella tradizionale [libreria client di Archiviazione di Azure per .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="d55ec-109">The Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="d55ec-110">È possibile ad esempio impostare il numero di operazioni parallele, tener traccia dello stato del trasferimento, riprendere facilmente un trasferimento annullato e molto altro ancora.</span><span class="sxs-lookup"><span data-stu-id="d55ec-110">This includes the ability to set the number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="d55ec-111">La libreria usa inoltre .NET Core, utile quando si creano app .NET per Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="d55ec-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="d55ec-112">Per altre informazioni su .NET Core, consultare la [documentazione di .NET Core](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="d55ec-112">To learn more about .NET Core, refer to the [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="d55ec-113">La libreria è compatibile anche con le app .NET Framework tradizionali per Windows.</span><span class="sxs-lookup"><span data-stu-id="d55ec-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="d55ec-114">In questo documento viene spiegato come creare un'applicazione console di .NET Core da eseguire su Windows, Linux e macOS e vengono dimostrati gli scenari seguenti:</span><span class="sxs-lookup"><span data-stu-id="d55ec-114">This document demonstrates how to create a .NET Core console application that that runs on Windows, Linux, and macOS and performs the following scenarios:</span></span>

- <span data-ttu-id="d55ec-115">Caricare file e directory nell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="d55ec-115">Upload files and directories to Blob Storage.</span></span>
- <span data-ttu-id="d55ec-116">Definire il numero di operazioni parallele durante il trasferimento dati.</span><span class="sxs-lookup"><span data-stu-id="d55ec-116">Define the number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="d55ec-117">Monitorare lo stato del trasferimento dati.</span><span class="sxs-lookup"><span data-stu-id="d55ec-117">Track data transfer progress.</span></span>
- <span data-ttu-id="d55ec-118">Riprendere un trasferimento dati annullato.</span><span class="sxs-lookup"><span data-stu-id="d55ec-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="d55ec-119">Copiare file dall'URL all'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="d55ec-119">Copy file from URL to Blob Storage.</span></span> 
- <span data-ttu-id="d55ec-120">Copiare da archivio BLOB ad archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="d55ec-120">Copy from Blob Storage to Blob Storage.</span></span>

<span data-ttu-id="d55ec-121">**Che cosa occorre:**</span><span class="sxs-lookup"><span data-stu-id="d55ec-121">**What you need:**</span></span>

* [<span data-ttu-id="d55ec-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d55ec-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="d55ec-123">Un [account di archiviazione di Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="d55ec-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="d55ec-124">Questa guida presuppone che si abbia già familiarità con [Archiviazione di Azure](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="d55ec-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="d55ec-125">In caso contrario, potrà essere utile leggere la documentazione [Introduzione ad Archiviazione di Azure](storage-introduction.md) .</span><span class="sxs-lookup"><span data-stu-id="d55ec-125">If not, reading the [Introduction to Azure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="d55ec-126">Ancora più importante, per iniziare a usare la libreria per lo spostamento dei dati è necessario [creare un account di archiviazione](storage-create-storage-account.md#create-a-storage-account).</span><span class="sxs-lookup"><span data-stu-id="d55ec-126">Most importantly, you need to [create a Storage account](storage-create-storage-account.md#create-a-storage-account) to start using the Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="d55ec-127">Configurazione</span><span class="sxs-lookup"><span data-stu-id="d55ec-127">Setup</span></span>  

1. <span data-ttu-id="d55ec-128">Consultare la [guida all'installazione di .NET Core](https://www.microsoft.com/net/core) per installare .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d55ec-128">Visit the [.NET Core Installation Guide](https://www.microsoft.com/net/core) to install .NET Core.</span></span> <span data-ttu-id="d55ec-129">Quando si seleziona l'ambiente, scegliere l'opzione della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="d55ec-129">When selecting your environment, choose the command-line option.</span></span> 
2. <span data-ttu-id="d55ec-130">Dalla riga di comando creare una directory per il progetto.</span><span class="sxs-lookup"><span data-stu-id="d55ec-130">From the command line, create a directory for your project.</span></span> <span data-ttu-id="d55ec-131">Passare a questa directory, quindi digitare `dotnet new` per creare un progetto console C#.</span><span class="sxs-lookup"><span data-stu-id="d55ec-131">Navigate into this directory, then type `dotnet new` to create a C# console project.</span></span>
3. <span data-ttu-id="d55ec-132">Aprire la directory in Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d55ec-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="d55ec-133">Questo passaggio può essere eseguito rapidamente tramite la riga di comando digitando `code .`.</span><span class="sxs-lookup"><span data-stu-id="d55ec-133">This step can be quickly done via the command line by typing `code .`.</span></span>  
4. <span data-ttu-id="d55ec-134">Installare l'[estensione C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) dal marketplace di Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d55ec-134">Install the [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from the Visual Studio Code Marketplace.</span></span> <span data-ttu-id="d55ec-135">Riavviare Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="d55ec-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="d55ec-136">A questo punto compariranno due prompt.</span><span class="sxs-lookup"><span data-stu-id="d55ec-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="d55ec-137">Un prompt permette di aggiungere le "risorse necessarie per compilare ed eseguire il debug".</span><span class="sxs-lookup"><span data-stu-id="d55ec-137">One is for adding "required assets to build and debug."</span></span> <span data-ttu-id="d55ec-138">Fare clic su "Sì".</span><span class="sxs-lookup"><span data-stu-id="d55ec-138">Click "yes."</span></span> <span data-ttu-id="d55ec-139">L'altro prompt consente di ripristinare le dipendenze non risolte.</span><span class="sxs-lookup"><span data-stu-id="d55ec-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="d55ec-140">Fare clic su "Ripristina".</span><span class="sxs-lookup"><span data-stu-id="d55ec-140">Click "restore."</span></span>
6. <span data-ttu-id="d55ec-141">A questo punto l'applicazione dovrebbe contenere un file `launch.json` nella directory `.vscode`.</span><span class="sxs-lookup"><span data-stu-id="d55ec-141">Your application should now contain a `launch.json` file under the `.vscode` directory.</span></span> <span data-ttu-id="d55ec-142">In questo file modificare il valore di `externalConsole` in `true`.</span><span class="sxs-lookup"><span data-stu-id="d55ec-142">In this file, change the `externalConsole` value to `true`.</span></span>
7. <span data-ttu-id="d55ec-143">Visual Studio Code consente di eseguire il debug delle applicazioni di .NET Core.</span><span class="sxs-lookup"><span data-stu-id="d55ec-143">Visual Studio Code allows you to debug .NET Core applications.</span></span> <span data-ttu-id="d55ec-144">Premere `F5` per eseguire l'applicazione e verificare che l'installazione funzioni.</span><span class="sxs-lookup"><span data-stu-id="d55ec-144">Hit `F5` to run your application and verify that your setup is working.</span></span> <span data-ttu-id="d55ec-145">Dovrebbe essere visualizzato "Hello World!"</span><span class="sxs-lookup"><span data-stu-id="d55ec-145">You should see "Hello World!"</span></span> <span data-ttu-id="d55ec-146">sulla console.</span><span class="sxs-lookup"><span data-stu-id="d55ec-146">printed to the console.</span></span> 

## <a name="add-data-movement-library-to-your-project"></a><span data-ttu-id="d55ec-147">Aggiungere la libreria per lo spostamento dei dati al progetto</span><span class="sxs-lookup"><span data-stu-id="d55ec-147">Add Data Movement Library to your project</span></span>

1. <span data-ttu-id="d55ec-148">Aggiungere la versione più recente della libreria per lo spostamento dei dati alla sezione `dependencies` del file `project.json`.</span><span class="sxs-lookup"><span data-stu-id="d55ec-148">Add the latest version of the Data Movement Library to the `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="d55ec-149">Al momento della redazione di questo documento, la versione è `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="d55ec-149">At the time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="d55ec-150">Aggiungere `"portable-net45+win8"` alla sezione `imports` .</span><span class="sxs-lookup"><span data-stu-id="d55ec-150">Add `"portable-net45+win8"` to the `imports` section.</span></span> 
3. <span data-ttu-id="d55ec-151">Per ripristinare il progetto dovrebbe essere visualizzato un prompt dei comandi.</span><span class="sxs-lookup"><span data-stu-id="d55ec-151">A prompt should display to restore your project.</span></span> <span data-ttu-id="d55ec-152">Fare clic sul pulsante "ripristina".</span><span class="sxs-lookup"><span data-stu-id="d55ec-152">Click the "restore" button.</span></span> <span data-ttu-id="d55ec-153">È inoltre possibile ripristinare il progetto dalla riga di comando digitando il comando `dotnet restore` nella radice della directory del progetto.</span><span class="sxs-lookup"><span data-stu-id="d55ec-153">You can also restore your project from the command line by typing the command `dotnet restore` in the root of your project directory.</span></span>

<span data-ttu-id="d55ec-154">Modificare `project.json`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-154">Modify `project.json`:</span></span>

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

## <a name="set-up-the-skeleton-of-your-application"></a><span data-ttu-id="d55ec-155">Configurare lo scheletro dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="d55ec-155">Set up the skeleton of your application</span></span>
<span data-ttu-id="d55ec-156">La prima cosa da fare è impostare il codice "scheletro" dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d55ec-156">The first thing we do is set up the "skeleton" code of our application.</span></span> <span data-ttu-id="d55ec-157">Questo codice richiede un nome e una chiave dell'account di archiviazione, che usa per creare un oggetto `CloudStorageAccount`.</span><span class="sxs-lookup"><span data-stu-id="d55ec-157">This code prompts us for a Storage account name and account key and uses those credentials to create a `CloudStorageAccount` object.</span></span> <span data-ttu-id="d55ec-158">Questo oggetto viene usato per interagire con l'account di archiviazione in tutti gli scenari di trasferimento.</span><span class="sxs-lookup"><span data-stu-id="d55ec-158">This object is used to interact with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="d55ec-159">Il codice consente inoltre di scegliere il tipo di operazione di trasferimento desiderata.</span><span class="sxs-lookup"><span data-stu-id="d55ec-159">The code also prompts us to choose the type of transfer operation we would like to execute.</span></span> 

<span data-ttu-id="d55ec-160">Modificare `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-160">Modify `Program.cs`:</span></span>

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
            Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

## <a name="transfer-local-file-to-azure-blob"></a><span data-ttu-id="d55ec-161">Trasferire il file locale in BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d55ec-161">Transfer local file to Azure Blob</span></span>
<span data-ttu-id="d55ec-162">Aggiungere i metodi `GetSourcePath` e `GetBlob` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-162">Add the methods `GetSourcePath` and `GetBlob` to `Program.cs`:</span></span>

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

<span data-ttu-id="d55ec-163">Modificare il metodo `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-163">Modify the `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="d55ec-164">Questo codice richiede il percorso di un file locale, il nome di un contenitore nuovo o esistente e il nome di un nuovo BLOB.</span><span class="sxs-lookup"><span data-stu-id="d55ec-164">This code prompts us for the path to a local file, the name of a new or existing container, and the name of a new blob.</span></span> <span data-ttu-id="d55ec-165">Il metodo `TransferManager.UploadAsync` esegue il caricamento usando queste informazioni.</span><span class="sxs-lookup"><span data-stu-id="d55ec-165">The `TransferManager.UploadAsync` method performs the upload using this information.</span></span> 

<span data-ttu-id="d55ec-166">Premere `F5` per eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d55ec-166">Hit `F5` to run your application.</span></span> <span data-ttu-id="d55ec-167">È possibile verificare l'avvenuto caricamento visualizzando l'account di archiviazione con [Esplora archivi di Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="d55ec-167">You can verify that the upload occurred by viewing your Storage account with the [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="d55ec-168">Impostare il numero di operazioni parallele</span><span class="sxs-lookup"><span data-stu-id="d55ec-168">Set number of parallel operations</span></span>
<span data-ttu-id="d55ec-169">Un'ottima funzionalità offerta dalla libreria per lo spostamento dei dati è la possibilità di impostare il numero di operazioni parallele per aumentare la velocità effettiva del trasferimento dati.</span><span class="sxs-lookup"><span data-stu-id="d55ec-169">A great feature offered by the Data Movement Library is the ability to set the number of parallel operations to increase the data transfer throughput.</span></span> <span data-ttu-id="d55ec-170">Per impostazione predefinita, la libreria per lo spostamento dei dati imposta il numero di operazioni parallele su 8 * il numero di core nel computer in uso.</span><span class="sxs-lookup"><span data-stu-id="d55ec-170">By default, the Data Movement Library sets the number of parallel operations to 8 * the number of cores on your machine.</span></span> 

<span data-ttu-id="d55ec-171">Tenere presente che un numero elevato di operazioni parallele in un ambiente con larghezza di banda ridotta potrebbe sovraccaricare la connessione di rete e impedire il corretto completamento delle operazioni.</span><span class="sxs-lookup"><span data-stu-id="d55ec-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm the network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="d55ec-172">È necessario fare qualche prova con questa impostazione per determinare la soluzione migliore in base alla larghezza di banda di rete disponibile.</span><span class="sxs-lookup"><span data-stu-id="d55ec-172">You'll need to experiment with this setting to determine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="d55ec-173">Aggiungere il codice che consente di impostare il numero di operazioni parallele.</span><span class="sxs-lookup"><span data-stu-id="d55ec-173">Let's add some code that allows us to set the number of parallel operations.</span></span> <span data-ttu-id="d55ec-174">Aggiungere anche il codice che imposta il tempo per completare il trasferimento.</span><span class="sxs-lookup"><span data-stu-id="d55ec-174">Let's also add code that times how long it takes for the transfer to complete.</span></span>

<span data-ttu-id="d55ec-175">Aggiungere un metodo `SetNumberOfParallelOperations` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-175">Add a `SetNumberOfParallelOperations` method to `Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like to use?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="d55ec-176">Modificare il metodo `ExecuteChoice` in modo che usi `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-176">Modify the `ExecuteChoice` method to use `SetNumberOfParallelOperations`:</span></span>

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like to execute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
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

<span data-ttu-id="d55ec-177">Modificare il metodo `TransferLocalFileToAzureBlob` in modo che usi un timer:</span><span class="sxs-lookup"><span data-stu-id="d55ec-177">Modify the `TransferLocalFileToAzureBlob` method to use a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="d55ec-178">Monitorare lo stato del trasferimento dati</span><span class="sxs-lookup"><span data-stu-id="d55ec-178">Track transfer progress</span></span>
<span data-ttu-id="d55ec-179">È molto utile conoscere il tempo impiegato per trasferire i dati.</span><span class="sxs-lookup"><span data-stu-id="d55ec-179">Knowing how long it took for our data to transfer is great.</span></span> <span data-ttu-id="d55ec-180">Tuttavia, la possibilità di visualizzare lo stato del trasferimento *durante* l'operazione è ancora più utile.</span><span class="sxs-lookup"><span data-stu-id="d55ec-180">However, being able to see the progress of our transfer *during* the transfer operation would be even better.</span></span> <span data-ttu-id="d55ec-181">Per realizzare questo scenario, è necessario creare un oggetto `TransferContext`.</span><span class="sxs-lookup"><span data-stu-id="d55ec-181">To achieve this scenario, we need to create a `TransferContext` object.</span></span> <span data-ttu-id="d55ec-182">L'oggetto `TransferContext` è disponibile in due forme: `SingleTransferContext` e `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="d55ec-182">The `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="d55ec-183">La prima serve per il trasferimento di un singolo file (ovvero l'operazione attualmente in corso) mentre la seconda serve per il trasferimento di una directory di file (operazione che avverrà successivamente).</span><span class="sxs-lookup"><span data-stu-id="d55ec-183">The former is for transferring a single file (which is what we're doing now) and the latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="d55ec-184">Aggiungere i metodi `GetSingleTransferContext` e `GetDirectoryTransferContext` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-184">Add the methods `GetSingleTransferContext` and `GetDirectoryTransferContext` to `Program.cs`:</span></span> 

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

<span data-ttu-id="d55ec-185">Modificare il metodo `TransferLocalFileToAzureBlob` in modo che usi `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-185">Modify the `TransferLocalFileToAzureBlob` method to use `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="d55ec-186">Riprendere un trasferimento annullato</span><span class="sxs-lookup"><span data-stu-id="d55ec-186">Resume a canceled transfer</span></span>
<span data-ttu-id="d55ec-187">Un'altra funzionalità utile offerta dalla libreria per lo spostamento dei dati è la possibilità di riprendere un trasferimento annullato.</span><span class="sxs-lookup"><span data-stu-id="d55ec-187">Another convenient feature offered by the Data Movement Library is the ability to resume a canceled transfer.</span></span> <span data-ttu-id="d55ec-188">Aggiungere un codice che consente di annullare temporaneamente il trasferimento digitando `c`, quindi riprendere il trasferimento dopo 3 secondi.</span><span class="sxs-lookup"><span data-stu-id="d55ec-188">Let's add some code that allows us to temporarily cancel the transfer by typing `c`, and then resume the transfer 3 seconds later.</span></span>

<span data-ttu-id="d55ec-189">Modificare `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="d55ec-190">Fino a questo momento il valore `checkpoint` è sempre rimasto impostato su `null`.</span><span class="sxs-lookup"><span data-stu-id="d55ec-190">Up until now, our `checkpoint` value has always been set to `null`.</span></span> <span data-ttu-id="d55ec-191">A questo punto, se si annulla il trasferimento, viene recuperato l'ultimo checkpoint dell'operazione, che viene poi usato come nuovo checkpoint nel trasferimento.</span><span class="sxs-lookup"><span data-stu-id="d55ec-191">Now, if we cancel the transfer, we retrieve the last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-to-azure-blob-directory"></a><span data-ttu-id="d55ec-192">Trasferire la directory locale nella directory BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d55ec-192">Transfer local directory to Azure Blob directory</span></span>
<span data-ttu-id="d55ec-193">Una potenziale forte limitazione si avrebbe se la libreria per lo spostamento dei dati potesse trasferire un solo file per volta.</span><span class="sxs-lookup"><span data-stu-id="d55ec-193">It would be disappointing if the Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="d55ec-194">Per fortuna però non è così.</span><span class="sxs-lookup"><span data-stu-id="d55ec-194">Luckily, this is not the case.</span></span> <span data-ttu-id="d55ec-195">La libreria per lo spostamento dei dati offre la possibilità di trasferire una directory di file e tutte le relative sottodirectory.</span><span class="sxs-lookup"><span data-stu-id="d55ec-195">The Data Movement Library provides the ability to transfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="d55ec-196">Aggiungere un codice che consente questa operazione.</span><span class="sxs-lookup"><span data-stu-id="d55ec-196">Let's add some code that allows us to do just that.</span></span>

<span data-ttu-id="d55ec-197">Per prima cosa, aggiungere il metodo `GetBlobDirectory` a `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-197">First, add the method `GetBlobDirectory` to `Program.cs`:</span></span>

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

<span data-ttu-id="d55ec-198">Poi modificare `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="d55ec-199">Esistono alcune differenze tra questo metodo e il metodo di caricamento di un singolo file.</span><span class="sxs-lookup"><span data-stu-id="d55ec-199">There are a few differences between this method and the method for uploading a single file.</span></span> <span data-ttu-id="d55ec-200">Attualmente sono in uso `TransferManager.UploadDirectoryAsync` e il metodo `getDirectoryTransferContext` creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="d55ec-200">We're now using `TransferManager.UploadDirectoryAsync` and the `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="d55ec-201">Ora è disponibile anche un valore `options` per l'operazione di caricamento, che consente di indicare la volontà di includere le sottodirectory nel caricamento.</span><span class="sxs-lookup"><span data-stu-id="d55ec-201">In addition, we now provide an `options` value to our upload operation, which allows us to indicate that we want to include subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-to-azure-blob"></a><span data-ttu-id="d55ec-202">Copiare i file dall'URL a un BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d55ec-202">Copy file from URL to Azure Blob</span></span>
<span data-ttu-id="d55ec-203">A questo punto, aggiungere un codice che consente di copiare un file da un URL a un BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d55ec-203">Now, let's add code that allows us to copy a file from a URL to an Azure Blob.</span></span> 

<span data-ttu-id="d55ec-204">Modificare `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-204">Modify `TransferUrlToAzureBlob`:</span></span>

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="d55ec-205">Un importante caso in cui viene usata questa funzionalità è quando è necessario spostare i dati da un altro servizio cloud (ad esempio AWS) ad Azure.</span><span class="sxs-lookup"><span data-stu-id="d55ec-205">One important use case for this feature is when you need to move data from another cloud service (e.g. AWS) to Azure.</span></span> <span data-ttu-id="d55ec-206">Se si dispone di un URL che consente di accedere alla risorsa, è possibile spostarla facilmente nei BLOB di Azure tramite il metodo `TransferManager.CopyAsync`.</span><span class="sxs-lookup"><span data-stu-id="d55ec-206">As long as you have a URL that gives you access to the resource, you can easily move that resource into Azure Blobs by using the `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="d55ec-207">Questo metodo introduce anche un nuovo parametro booleano.</span><span class="sxs-lookup"><span data-stu-id="d55ec-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="d55ec-208">L'impostazione di questo parametro su `true` indica che si desidera eseguire una copia asincrona sul lato server.</span><span class="sxs-lookup"><span data-stu-id="d55ec-208">Setting this parameter to `true` indicates that we want to do an asynchronous server-side copy.</span></span> <span data-ttu-id="d55ec-209">L'impostazione di questo parametro su `false` indica una copia sincrona, ovvero la risorsa viene prima scaricata sul computer locale e poi caricata sul BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d55ec-209">Setting this parameter to `false` indicates a synchronous copy - meaning the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="d55ec-210">La copia sincrona tuttavia è attualmente disponibile solo per la copia da una risorsa di archiviazione di Azure a un'altra.</span><span class="sxs-lookup"><span data-stu-id="d55ec-210">However, synchronous copy is currently only available for copying from one Azure Storage resource to another.</span></span> 

## <a name="transfer-azure-blob-to-azure-blob"></a><span data-ttu-id="d55ec-211">Trasferire da un BLOB di Azure a un altro BLOB di Azure</span><span class="sxs-lookup"><span data-stu-id="d55ec-211">Transfer Azure Blob to Azure Blob</span></span>
<span data-ttu-id="d55ec-212">Un'altra funzionalità esclusiva della libreria per lo spostamento dei dati è la possibilità di copiare da una risorsa di archiviazione di Azure a un'altra.</span><span class="sxs-lookup"><span data-stu-id="d55ec-212">Another feature that's uniquely provided by the Data Movement Library is the ability to copy from one Azure Storage resource to another.</span></span> 

<span data-ttu-id="d55ec-213">Modificare `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="d55ec-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' to temporarily cancel your transfer...\n");

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

<span data-ttu-id="d55ec-214">In questo esempio il parametro booleano in `TransferManager.CopyAsync` viene impostato su `false` per indicare che si desidera eseguire una copia sincrona.</span><span class="sxs-lookup"><span data-stu-id="d55ec-214">In this example, we set the boolean parameter in `TransferManager.CopyAsync` to `false` to indicate that we want to do a synchronous copy.</span></span> <span data-ttu-id="d55ec-215">Ciò significa che la risorsa viene prima scaricata sul computer locale e successivamente caricata sul BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="d55ec-215">This means that the resource is downloaded to our local machine first, then uploaded to Azure Blob.</span></span> <span data-ttu-id="d55ec-216">L'opzione di copia sincrona è un ottimo modo per assicurarsi che l'operazione di copia avvenga a velocità costante.</span><span class="sxs-lookup"><span data-stu-id="d55ec-216">The synchronous copy option is a great way to ensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="d55ec-217">Al contrario, la velocità di una copia asincrona sul lato server dipende dalla larghezza di banda di rete disponibile sul server, che può variare.</span><span class="sxs-lookup"><span data-stu-id="d55ec-217">In contrast, the speed of an asynchronous server-side copy is dependent on the available network bandwidth on the server, which can fluctuate.</span></span> <span data-ttu-id="d55ec-218">La copia sincrona, tuttavia, può generare costi aggiuntivi in uscita rispetto alla copia asincrona.</span><span class="sxs-lookup"><span data-stu-id="d55ec-218">However, synchronous copy may generate additional egress cost compared to asynchronous copy.</span></span> <span data-ttu-id="d55ec-219">Per evitare costi in uscita, si consiglia quindi di usare la copia sincrona in una macchina virtuale di Azure che si trova nella stessa area dell'account di archiviazione di origine.</span><span class="sxs-lookup"><span data-stu-id="d55ec-219">The recommended approach is to use synchronous copy in an Azure VM that is in the same region as your source storage account to avoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="d55ec-220">Conclusione</span><span class="sxs-lookup"><span data-stu-id="d55ec-220">Conclusion</span></span>
<span data-ttu-id="d55ec-221">L'applicazione per lo spostamento dei dati ora è completa.</span><span class="sxs-lookup"><span data-stu-id="d55ec-221">Our data movement application is now complete.</span></span> <span data-ttu-id="d55ec-222">[L'esempio di codice completo è disponibile su GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="d55ec-222">[The full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="d55ec-223">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d55ec-223">Next steps</span></span>
<span data-ttu-id="d55ec-224">In questa guida introduttiva è stata creata un'applicazione in grado di interagire con Archiviazione di Azure e che può essere eseguita su Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="d55ec-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="d55ec-225">Questa guida introduttiva ha trattato principalmente dell'archivio BLOB.</span><span class="sxs-lookup"><span data-stu-id="d55ec-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="d55ec-226">Tuttavia, queste stesse conoscenze si possono applicare all'archiviazione file.</span><span class="sxs-lookup"><span data-stu-id="d55ec-226">However, this same knowledge can be applied to File Storage.</span></span> <span data-ttu-id="d55ec-227">Per altre informazioni, consultare la [documentazione di riferimento sulla libreria per lo spostamento dei dati di Archiviazione di Azure](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="d55ec-227">To learn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




