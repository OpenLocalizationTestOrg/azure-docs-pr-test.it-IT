---
title: Eseguire lo sviluppo per Archiviazione file di Azure con .NET | Microsoft Docs
description: Informazioni su come sviluppare applicazioni e servizi .NET che usano Archiviazione file di Azure per archiviare i dati dei file.
services: storage
documentationcenter: .net
author: RenaShahMSFT
manager: aungoo
editor: tysonn
ms.assetid: 6a889ee1-1e60-46ec-a592-ae854f9fb8b6
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 05/27/2017
ms.author: renash
ms.openlocfilehash: 7b94e70619324bb8dc8e7f8306f00f06e7476c1f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="67ba1-103">Eseguire lo sviluppo per Archiviazione file di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="67ba1-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="67ba1-104">Questo articolo illustra come gestire Archiviazione file di Azure con .NET.</span><span class="sxs-lookup"><span data-stu-id="67ba1-104">This article shows how to manage Azure File storage with .NET code.</span></span> <span data-ttu-id="67ba1-105">Per altre informazioni su Archiviazione file di Azure, vedere l'[introduzione ad Archiviazione file di Azure](storage-files-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="67ba1-105">To learn more about Azure File storage, please see the [Introduction to Azure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="67ba1-106">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="67ba1-106">About this tutorial</span></span>
<span data-ttu-id="67ba1-107">Questa esercitazione illustra le nozioni base per l'uso di .NET per sviluppare applicazioni o servizi che usano Archiviazione file di Azure per archiviare i dati dei file.</span><span class="sxs-lookup"><span data-stu-id="67ba1-107">This tutorial will demonstrate the basics of using .NET to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="67ba1-108">In questa esercitazione verrà creata una semplice applicazione console e verrà mostrato come eseguire le azioni di base con .NET e Archiviazione file di Azure:</span><span class="sxs-lookup"><span data-stu-id="67ba1-108">In this tutorial, we will create a simple console application and show how to perform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="67ba1-109">Ottenere il contenuto di un file</span><span class="sxs-lookup"><span data-stu-id="67ba1-109">Get the contents of a file</span></span>
* <span data-ttu-id="67ba1-110">Impostare la quota (dimensione massima) per la condivisione file.</span><span class="sxs-lookup"><span data-stu-id="67ba1-110">Set the quota (maximum size) for the file share.</span></span>
* <span data-ttu-id="67ba1-111">Creare una firma di accesso condiviso (chiave di firma di accesso condiviso) per un file che usa un criterio di accesso condiviso definito nella condivisione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on the share.</span></span>
* <span data-ttu-id="67ba1-112">Copiare un file in un altro file nello stesso account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-112">Copy a file to another file in the same storage account.</span></span>
* <span data-ttu-id="67ba1-113">Copiare un file in un BLOB nello stesso account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-113">Copy a file to a blob in the same storage account.</span></span>
* <span data-ttu-id="67ba1-114">Usare la metrica di archiviazione di Azure per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="67ba1-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="67ba1-115">Poiché Archiviazione file di Azure è accessibile tramite SMB, è possibile scrivere semplici applicazioni che accedono alla condivisione file di Azure usando le classi standard System.IO per l'I/O file.</span><span class="sxs-lookup"><span data-stu-id="67ba1-115">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard System.IO classes for File I/O.</span></span> <span data-ttu-id="67ba1-116">Questo articolo descrive come scrivere applicazioni che usano Azure Storage .NET SDK, che usa l'[API REST di archiviazione file Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) per comunicare con Archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="67ba1-116">This article will describe how to write applications that use the Azure Storage .NET SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span> 


## <a name="create-the-console-application-and-obtain-the-assembly"></a><span data-ttu-id="67ba1-117">Creare l'applicazione console e ottenere l'assembly</span><span class="sxs-lookup"><span data-stu-id="67ba1-117">Create the console application and obtain the assembly</span></span>
<span data-ttu-id="67ba1-118">In Visual Studio creare una nuova applicazione console di Windows.</span><span class="sxs-lookup"><span data-stu-id="67ba1-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="67ba1-119">La procedura seguente illustra come creare un'applicazione console in Visual Studio 2017, ma i passaggi sono simili anche per le altre versioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="67ba1-119">The following steps show you how to create a console application in Visual Studio 2017, however, the steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="67ba1-120">Selezionare **File** > **Nuovo** > **Progetto**</span><span class="sxs-lookup"><span data-stu-id="67ba1-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="67ba1-121">Selezionare **Installati** > **Modelli** > **Visual C#** > **Desktop classico di Windows**</span><span class="sxs-lookup"><span data-stu-id="67ba1-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="67ba1-122">Selezionare **App console (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="67ba1-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="67ba1-123">Immettere un nome per l'applicazione nel campo **Nome**</span><span class="sxs-lookup"><span data-stu-id="67ba1-123">Enter a name for your application in the **Name:** field</span></span>
5. <span data-ttu-id="67ba1-124">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="67ba1-124">Select **OK**</span></span>

<span data-ttu-id="67ba1-125">Tutti gli esempi di codice in questa esercitazione possono essere aggiunti al metodo `Main()` del file `Program.cs` dell'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="67ba1-125">All code examples in this tutorial can be added to the `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="67ba1-126">È possibile usare la libreria client di archiviazione di Azure in qualsiasi tipo di applicazione .NET, ad esempio un servizio cloud o un'app Web di Azure e applicazioni desktop e per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="67ba1-126">You can use the Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="67ba1-127">Per semplicità, in questa guida si usa un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="67ba1-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-to-install-the-required-packages"></a><span data-ttu-id="67ba1-128">Usare NuGet per installare i pacchetti necessari</span><span class="sxs-lookup"><span data-stu-id="67ba1-128">Use NuGet to install the required packages</span></span>
<span data-ttu-id="67ba1-129">Per completare questa esercitazione, è necessario fare riferimento a due pacchetti nel progetto:</span><span class="sxs-lookup"><span data-stu-id="67ba1-129">There are two packages you need to reference in your project to complete this tutorial:</span></span>

* <span data-ttu-id="67ba1-130">[Libreria client di archiviazione di Microsoft Azure per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): questo pacchetto fornisce l'accesso a livello di codice alle risorse dati nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access to data resources in your storage account.</span></span>
* <span data-ttu-id="67ba1-131">[Libreria Gestione configurazione di Microsoft Azure per .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): questo pacchetto fornisce una classe per l'analisi di una stringa di connessione in un file di configurazione, indipendentemente dalla posizione in cui viene eseguita l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="67ba1-132">Per ottenere entrambi i pacchetti, è possibile usare NuGet.</span><span class="sxs-lookup"><span data-stu-id="67ba1-132">You can use NuGet to obtain both packages.</span></span> <span data-ttu-id="67ba1-133">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="67ba1-133">Follow these steps:</span></span>

1. <span data-ttu-id="67ba1-134">Fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="67ba1-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="67ba1-135">Cercare online "WindowsAzure.Storage" e fare clic su **Installa** per installare il pacchetto della libreria client di archiviazione e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="67ba1-135">Search online for "WindowsAzure.Storage" and click **Install** to install the Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="67ba1-136">Cercare online "WindowsAzure.ConfigurationManager" e fare clic su **Installa** per installare Gestione configurazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="67ba1-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** to install the Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-to-the-appconfig-file"></a><span data-ttu-id="67ba1-137">Salvare le credenziali dell'account di archiviazione nel file app.config</span><span class="sxs-lookup"><span data-stu-id="67ba1-137">Save your storage account credentials to the app.config file</span></span>
<span data-ttu-id="67ba1-138">A questo punto salvare le credenziali nel file app.config del progetto.</span><span class="sxs-lookup"><span data-stu-id="67ba1-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="67ba1-139">Modificare il file app.config in modo che assomigli all'esempio seguente, sostituendo `myaccount` con il nome dell'account di archiviazione e `mykey` con la chiave dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-139">Edit the app.config file so that it appears similar to the following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

```xml
<?xml version="1.0" encoding="utf-8" ?>
<configuration>
    <startup>
        <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5" />
    </startup>
    <appSettings>
        <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=StorageAccountKeyEndingIn==" />
    </appSettings>
</configuration>
```

> [!NOTE]
> L'ultima versione dell'emulatore di archiviazione di Azure non supporta Archiviazione file di Azure. <span data-ttu-id="67ba1-141">La stringa di connessione deve indirizzare a un account di archiviazione di Azure nel cloud per poter usare Archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="67ba1-141">Your connection string must target an Azure Storage Account in the cloud to work with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="67ba1-142">Aggiungere le direttive using</span><span class="sxs-lookup"><span data-stu-id="67ba1-142">Add using directives</span></span>
<span data-ttu-id="67ba1-143">Aprire il file `Program.cs` da Esplora soluzioni e aggiungere le direttive using seguenti all'inizio del file.</span><span class="sxs-lookup"><span data-stu-id="67ba1-143">Open the `Program.cs` file from Solution Explorer, and add the following using directives to the top of the file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-the-file-share-programmatically"></a><span data-ttu-id="67ba1-144">Accedere alla condivisione file a livello di programmazione</span><span class="sxs-lookup"><span data-stu-id="67ba1-144">Access the file share programmatically</span></span>
<span data-ttu-id="67ba1-145">A questo punto aggiungere il codice seguente al metodo `Main()`, dopo il codice indicato sopra, per recuperare la stringa di connessione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-145">Next, add the following code to the `Main()` method (after the code shown above) to retrieve the connection string.</span></span> <span data-ttu-id="67ba1-146">Questo codice ottiene un riferimento al file creato in precedenza e genera i contenuti nella finestra della console.</span><span class="sxs-lookup"><span data-stu-id="67ba1-146">This code gets a reference to the file we created earlier and outputs its contents to the console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the file exists.
        if (file.Exists())
        {
            // Write the contents of the file to the console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="67ba1-147">Eseguire l'applicazione console per visualizzare l'output.</span><span class="sxs-lookup"><span data-stu-id="67ba1-147">Run the console application to see the output.</span></span>

## <a name="set-the-maximum-size-for-a-file-share"></a><span data-ttu-id="67ba1-148">Impostare la dimensione massima per una condivisione file</span><span class="sxs-lookup"><span data-stu-id="67ba1-148">Set the maximum size for a file share</span></span>
<span data-ttu-id="67ba1-149">A partire dalla versione 5.x della libreria del client di archiviazione di Azure, è possibile impostare la quota (o dimensione massima) per una condivisione file, in gigabyte.</span><span class="sxs-lookup"><span data-stu-id="67ba1-149">Beginning with version 5.x of the Azure Storage Client Library, you can set set the quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="67ba1-150">È anche possibile controllare la quantità di dati archiviata attualmente nella condivisione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-150">You can also check to see how much data is currently stored on the share.</span></span>

<span data-ttu-id="67ba1-151">Impostando la quota per una condivisione, è possibile limitare la dimensione totale dei file archiviati nella condivisione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-151">By setting the quota for a share, you can limit the total size of the files stored on the share.</span></span> <span data-ttu-id="67ba1-152">Se la dimensione totale dei file nella condivisione supera la quota impostata per la condivisione, i client non saranno in grado di aumentare le dimensioni dei file esistenti o creare nuovi file, a meno che tali file non siano vuoti.</span><span class="sxs-lookup"><span data-stu-id="67ba1-152">If the total size of files on the share exceeds the quota set on the share, then clients will be unable to increase the size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="67ba1-153">L'esempio seguente illustra come controllare l'uso corrente per una condivisione e come impostare la quota per la condivisione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-153">The example below shows how to check the current usage for a share and how to set the quota for the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Check current usage stats for the share.
    // Note that the ShareStats object is part of the protocol layer for the File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify the maximum size of the share, in GB.
    // This line sets the quota to be 10 GB greater than the current usage of the share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check the quota for the share. Call FetchAttributes() to populate the share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="67ba1-154">Generare la firma di accesso condiviso per un file o una condivisione file</span><span class="sxs-lookup"><span data-stu-id="67ba1-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="67ba1-155">A partire dalla versione 5.x della Libreria del client di archiviazione di Azure, è possibile generare una firma di accesso condiviso (SAS) per una condivisione file o per un singolo file.</span><span class="sxs-lookup"><span data-stu-id="67ba1-155">Beginning with version 5.x of the Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="67ba1-156">È inoltre possibile creare un criterio di accesso condiviso in una condivisione file per gestire le firme di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="67ba1-156">You can also create a shared access policy on a file share to manage shared access signatures.</span></span> <span data-ttu-id="67ba1-157">È consigliabile creare un criterio di accesso condiviso, in quanto fornisce un modo per revocare la firma SAS se necessario.</span><span class="sxs-lookup"><span data-stu-id="67ba1-157">Creating a shared access policy is recommended, as it provides a means of revoking the SAS if it should be compromised.</span></span>

<span data-ttu-id="67ba1-158">Nell'esempio seguente viene creato un criterio di accesso condiviso in una condivisione e quindi viene usato tale criterio per fornire i vincoli per una firma di accesso condiviso su un file della condivisione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-158">The following example creates a shared access policy on a share, and then uses that policy to provide the constraints for a SAS on a file in the share.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for the share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add the shared access policy to the share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in the share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from the SAS, and write some text to the file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="67ba1-159">Per altre informazioni sulla creazione e sull'uso di firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) e [Creare e usare una firma di accesso condiviso con i BLOB di Azure](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="67ba1-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json) and [Create and use a SAS with Azure Blobs](../blobs/storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="67ba1-160">Copiare i file</span><span class="sxs-lookup"><span data-stu-id="67ba1-160">Copy files</span></span>
<span data-ttu-id="67ba1-161">A partire dalla versione 5.x della libreria del client di archiviazione di Azure, è possibile copiare un file in un altro file, un file in un BLOB o un BLOB in un file.</span><span class="sxs-lookup"><span data-stu-id="67ba1-161">Beginning with version 5.x of the Azure Storage Client Library, you can copy a file to another file, a file to a blob, or a blob to a file.</span></span> <span data-ttu-id="67ba1-162">Le sezioni seguenti illustrano come eseguire queste operazioni di copia a livello di programmazione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-162">In the next sections, we demonstrate how to perform these copy operations programmatically.</span></span>

<span data-ttu-id="67ba1-163">È inoltre possibile utilizzare AzCopy per copiare un file in un altro o per copiare un blob in un file o viceversa.</span><span class="sxs-lookup"><span data-stu-id="67ba1-163">You can also use AzCopy to copy one file to another or to copy a blob to a file or vice versa.</span></span> <span data-ttu-id="67ba1-164">Vedere [Trasferire dati con l'utilità della riga di comando AzCopy](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="67ba1-164">See [Transfer data with the AzCopy Command-Line Utility](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json).</span></span>

> [!NOTE]
> <span data-ttu-id="67ba1-165">Se si copia un BLOB in un file o un file in un BLOB, è necessario utilizzare una firma di accesso condiviso (SAS) per autenticare l'oggetto di origine, anche se si copia nello stesso account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-165">If you are copying a blob to a file, or a file to a blob, you must use a shared access signature (SAS) to authenticate the source object, even if you are copying within the same storage account.</span></span>
> 
> 

<span data-ttu-id="67ba1-166">**Copiare un file in un altro file** Nell'esempio seguente viene copiato un file in un altro file nella stessa condivisione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-166">**Copy a file to another file** The following example copies a file to another file in the same share.</span></span> <span data-ttu-id="67ba1-167">Poiché questa operazione esegue la copia tra file nello stesso account di archiviazione, è possibile utilizzare l'autenticazione chiave condivisa per eseguire la copia.</span><span class="sxs-lookup"><span data-stu-id="67ba1-167">Because this copy operation copies between files in the same storage account, you can use Shared Key authentication to perform the copy.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference to the file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that the share exists.
if (share.Exists())
{
    // Get a reference to the root directory for the share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference to the directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that the directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference to the file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that the source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference to the destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start the copy operation.
            destFile.StartCopy(sourceFile);

            // Write the contents of the destination file to the console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="67ba1-168">**Copiare un file in un BLOB** Nell'esempio seguente viene creato un file che viene copiato in un BLOB nello stesso account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-168">**Copy a file to a blob** The following example creates a file and copies it to a blob within the same storage account.</span></span> <span data-ttu-id="67ba1-169">Nell'esempio viene creata una firma di accesso condiviso per il file di origine, che il servizio utilizza per autenticare l'accesso al file di origine durante l'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="67ba1-169">The example creates a SAS for the source file, which the service uses to authenticate access to the source file during the copy operation.</span></span>

```csharp
// Parse the connection string for the storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access to Azure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in the root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in the root directory.");

// Get a reference to the blob to which the file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for the file that's valid for 24 hours.
// Note that when you are copying a file to a blob, or a blob to a file, you must use a SAS
// to authenticate access to the source object, even if you are copying within the same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for the source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct the URI to the source file, including the SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy the file to the blob.
destBlob.StartCopy(fileSasUri);

// Write the contents of the file to the console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="67ba1-170">È possibile copiare un BLOB in un file nello stesso modo.</span><span class="sxs-lookup"><span data-stu-id="67ba1-170">You can copy a blob to a file in the same way.</span></span> <span data-ttu-id="67ba1-171">Se l'oggetto di origine è un BLOB, creare una firma di accesso condiviso per consentire l'accesso al BLOB durante l'operazione di copia.</span><span class="sxs-lookup"><span data-stu-id="67ba1-171">If the source object is a blob, then create a SAS to authenticate access to that blob during the copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="67ba1-172">Risoluzione dei problemi di Archiviazione file di Azure con le metriche</span><span class="sxs-lookup"><span data-stu-id="67ba1-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="67ba1-173">Analisi archiviazione di Azure ora supporta le metriche per Archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="67ba1-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="67ba1-174">Grazie ai dati di metrica, è possibile monitorare le richieste e diagnosticare i problemi.</span><span class="sxs-lookup"><span data-stu-id="67ba1-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="67ba1-175">È possibile abilitare le metriche per Archiviazione file di Azure dal [portale di Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="67ba1-175">You can enable metrics for Azure File storage from the [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="67ba1-176">È anche possibile abilitare le metriche a livello ci codice chiamando l'operazione Set File Service Properties tramite l'API REST o una delle soluzioni analoghe disponibili nella libreria client di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="67ba1-176">You can also enable metrics programmatically by calling the Set File Service Properties operation via the REST API, or one of its analogues in the Storage Client Library.</span></span>


<span data-ttu-id="67ba1-177">L'esempio di codice seguente mostra come usare la libreria client di archiviazione per .NET per abilitare le metriche per Archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="67ba1-177">The following code example shows how to use the Storage Client Library for .NET to enable metrics for Azure File storage.</span></span>

<span data-ttu-id="67ba1-178">Aggiungere prima le direttive `using` seguenti al file `Program.cs`, oltre a quelle aggiunte sopra:</span><span class="sxs-lookup"><span data-stu-id="67ba1-178">First, add the following `using` directives to your `Program.cs` file, in addition to those you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="67ba1-179">Si noti che, anche se i BLOB di Azure, le tabelle di Azure e le code di Azure usano il tipo `ServiceProperties` condiviso nello spazio dei nomi `Microsoft.WindowsAzure.Storage.Shared.Protocol`, Archiviazione file di Azure usa il proprio tipo, ovvero il tipo `FileServiceProperties` nello spazio dei nomi `Microsoft.WindowsAzure.Storage.File.Protocol`.</span><span class="sxs-lookup"><span data-stu-id="67ba1-179">Note that while Azure Blobs, Azure Table, and Azure Queues use the shared `ServiceProperties` type in the `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, the `FileServiceProperties` type in the `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="67ba1-180">È tuttavia necessario fare riferimento a entrambi gli spazi dei nomi dal proprio codice, per poter compilare il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="67ba1-180">Both namespaces must be referenced from your code, however, for the following code to compile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create the File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that the File service currently uses its own service properties type,
// available in the Microsoft.WindowsAzure.Storage.File.Protocol namespace.
fileClient.SetServiceProperties(new FileServiceProperties()
{
    // Set hour metrics
    HourMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 14,
        Version = "1.0"
    },
    // Set minute metrics
    MinuteMetrics = new MetricsProperties()
    {
        MetricsLevel = MetricsLevel.ServiceAndApi,
        RetentionDays = 7,
        Version = "1.0"
    }
});

// Read the metrics properties we just set.
FileServiceProperties serviceProperties = fileClient.GetServiceProperties();
Console.WriteLine("Hour metrics:");
Console.WriteLine(serviceProperties.HourMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.HourMetrics.RetentionDays);
Console.WriteLine(serviceProperties.HourMetrics.Version);
Console.WriteLine();
Console.WriteLine("Minute metrics:");
Console.WriteLine(serviceProperties.MinuteMetrics.MetricsLevel);
Console.WriteLine(serviceProperties.MinuteMetrics.RetentionDays);
Console.WriteLine(serviceProperties.MinuteMetrics.Version);
```

<span data-ttu-id="67ba1-181">È anche possibile vedere l'articolo sulla [risoluzione dei problemi di Archiviazione file di Azure](storage-troubleshoot-windows-file-connection-problems.md) per indicazioni sulla risoluzione dei problemi end-to-end.</span><span class="sxs-lookup"><span data-stu-id="67ba1-181">Also, you can refer to [Azure File storage Troubleshooting Article](storage-troubleshoot-windows-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67ba1-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="67ba1-182">Next steps</span></span>
<span data-ttu-id="67ba1-183">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="67ba1-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="67ba1-184">Articoli concettuali e video</span><span class="sxs-lookup"><span data-stu-id="67ba1-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="67ba1-185">Archiviazione di file in Azure: un file system SMB nel cloud senza problemi per Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="67ba1-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="67ba1-186">Come usare Archiviazione file di Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="67ba1-186">How to use Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="67ba1-187">Supporto degli strumenti per Archiviazione file</span><span class="sxs-lookup"><span data-stu-id="67ba1-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="67ba1-188">Come usare AzCopy con Archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="67ba1-188">How to use AzCopy with Microsoft Azure Storage</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json)
* [<span data-ttu-id="67ba1-189">Utilizzo dell'interfaccia della riga di comando di Azure con archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="67ba1-189">Using the Azure CLI with Azure Storage</span></span>](../common/storage-azure-cli.md?toc=%2fazure%2fstorage%2ffiles%2ftoc.json#create-and-manage-file-shares)
* [<span data-ttu-id="67ba1-190">Risoluzione dei problemi di archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="67ba1-190">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="67ba1-191">Riferimento</span><span class="sxs-lookup"><span data-stu-id="67ba1-191">Reference</span></span>
* [<span data-ttu-id="67ba1-192">Informazioni di riferimento sulla libreria client di archiviazione per .NET</span><span class="sxs-lookup"><span data-stu-id="67ba1-192">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="67ba1-193">Riferimento API REST del servizio File</span><span class="sxs-lookup"><span data-stu-id="67ba1-193">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="67ba1-194">Post di BLOG</span><span class="sxs-lookup"><span data-stu-id="67ba1-194">Blog posts</span></span>
* [<span data-ttu-id="67ba1-195">Archiviazione file di Azure è attualmente disponibile a livello generale</span><span class="sxs-lookup"><span data-stu-id="67ba1-195">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="67ba1-196">Inside Azure File storage (Analisi di Archiviazione file di Azure)</span><span class="sxs-lookup"><span data-stu-id="67ba1-196">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="67ba1-197">Introduzione al servizio File di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="67ba1-197">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="67ba1-198">Persisting connections to Microsoft Azure File storage (Impostazione della persistenza delle connessioni ad Archiviazione file di Microsoft Azure)</span><span class="sxs-lookup"><span data-stu-id="67ba1-198">Persisting connections to Microsoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)