---
title: aaaDevelop per l'archiviazione di File di Azure con .NET | Documenti Microsoft
description: Informazioni su come toodevelop .NET applicazioni e servizi che utilizzano i File di Azure storage toostore dati dei file.
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
ms.openlocfilehash: aa8f84f1c93249055370e2a2cb33d7118b972be1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-net"></a><span data-ttu-id="c791a-103">Eseguire lo sviluppo per Archiviazione file di Azure con .NET</span><span class="sxs-lookup"><span data-stu-id="c791a-103">Develop for Azure File storage with .NET</span></span> 
> [!NOTE]
> <span data-ttu-id="c791a-104">Questo articolo viene illustrato come toomanage archiviazione di File di Azure con il codice .NET.</span><span class="sxs-lookup"><span data-stu-id="c791a-104">This article shows how toomanage Azure File storage with .NET code.</span></span> <span data-ttu-id="c791a-105">toolearn più sull'archiviazione di File di Azure, vedere hello [tooAzure introduzione archiviazione File](storage-files-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c791a-105">toolearn more about Azure File storage, please see hello [Introduction tooAzure File storage](storage-files-introduction.md).</span></span>
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="c791a-106">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="c791a-106">About this tutorial</span></span>
<span data-ttu-id="c791a-107">In questa esercitazione verrà illustrato l'utilizzo toodevelop applicazioni o servizi .NET che utilizzano i File di Azure storage toostore file dati di base di hello.</span><span class="sxs-lookup"><span data-stu-id="c791a-107">This tutorial will demonstrate hello basics of using .NET toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="c791a-108">In questa esercitazione verrà creata una semplice applicazione console e Mostra come azioni di base tooperform con archiviazione .NET e i File di Azure:</span><span class="sxs-lookup"><span data-stu-id="c791a-108">In this tutorial, we will create a simple console application and show how tooperform basic actions with .NET and Azure File storage:</span></span>

* <span data-ttu-id="c791a-109">Ottenere il contenuto di hello di un file</span><span class="sxs-lookup"><span data-stu-id="c791a-109">Get hello contents of a file</span></span>
* <span data-ttu-id="c791a-110">Impostare la quota hello (dimensione massima) per la condivisione di file hello.</span><span class="sxs-lookup"><span data-stu-id="c791a-110">Set hello quota (maximum size) for hello file share.</span></span>
* <span data-ttu-id="c791a-111">Creare una firma di accesso condiviso (chiave di firma di accesso condiviso) per un file che utilizza un criterio di accesso condiviso definito nella condivisione di hello.</span><span class="sxs-lookup"><span data-stu-id="c791a-111">Create a shared access signature (SAS key) for a file that uses a shared access policy defined on hello share.</span></span>
* <span data-ttu-id="c791a-112">Copiare un file con estensione tooanother hello stesso account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c791a-112">Copy a file tooanother file in hello same storage account.</span></span>
* <span data-ttu-id="c791a-113">Copiare un blob tooa file hello stesso account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c791a-113">Copy a file tooa blob in hello same storage account.</span></span>
* <span data-ttu-id="c791a-114">Usare la metrica di archiviazione di Azure per la risoluzione dei problemi</span><span class="sxs-lookup"><span data-stu-id="c791a-114">Use Azure Storage Metrics for troubleshooting</span></span>

> [!Note]  
> <span data-ttu-id="c791a-115">Poiché la memorizzazione dei File di Azure sono accessibili tramite SMB, è possibile toowrite semplici applicazioni che accedono a condivisione di File di Azure hello utilizzando le classi System.IO hello standard per i/o File.</span><span class="sxs-lookup"><span data-stu-id="c791a-115">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard System.IO classes for File I/O.</span></span> <span data-ttu-id="c791a-116">In questo articolo descrive come le applicazioni che usano toowrite hello Azure Storage .NET SDK, che usa hello [API REST di archiviazione di File di Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure archiviazione File.</span><span class="sxs-lookup"><span data-stu-id="c791a-116">This article will describe how toowrite applications that use hello Azure Storage .NET SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span> 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a><span data-ttu-id="c791a-117">Creare un'applicazione console hello e ottenere assembly hello</span><span class="sxs-lookup"><span data-stu-id="c791a-117">Create hello console application and obtain hello assembly</span></span>
<span data-ttu-id="c791a-118">In Visual Studio creare una nuova applicazione console di Windows.</span><span class="sxs-lookup"><span data-stu-id="c791a-118">In Visual Studio, create a new Windows console application.</span></span> <span data-ttu-id="c791a-119">Hello alla procedura seguente viene illustrato come toocreate un'applicazione console in Visual Studio 2017, tuttavia, i passaggi di hello sono simili in altre versioni di Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="c791a-119">hello following steps show you how toocreate a console application in Visual Studio 2017, however, hello steps are similar in other versions of Visual Studio.</span></span>

1. <span data-ttu-id="c791a-120">Selezionare **File** > **Nuovo** > **Progetto**</span><span class="sxs-lookup"><span data-stu-id="c791a-120">Select **File** > **New** > **Project**</span></span>
2. <span data-ttu-id="c791a-121">Selezionare **Installati** > **Modelli** > **Visual C#** > **Desktop classico di Windows**</span><span class="sxs-lookup"><span data-stu-id="c791a-121">Select **Installed** > **Templates** > **Visual C#** > **Windows Classic Desktop**</span></span>
3. <span data-ttu-id="c791a-122">Selezionare **App console (.NET Framework)**</span><span class="sxs-lookup"><span data-stu-id="c791a-122">Select **Console App (.NET Framework)**</span></span>
4. <span data-ttu-id="c791a-123">Immettere un nome per l'applicazione in hello **nome:** campo</span><span class="sxs-lookup"><span data-stu-id="c791a-123">Enter a name for your application in hello **Name:** field</span></span>
5. <span data-ttu-id="c791a-124">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="c791a-124">Select **OK**</span></span>

<span data-ttu-id="c791a-125">Tutti gli esempi di codice in questa esercitazione è possibile aggiungere toohello `Main()` metodo dell'applicazione console `Program.cs` file.</span><span class="sxs-lookup"><span data-stu-id="c791a-125">All code examples in this tutorial can be added toohello `Main()` method of your console application's `Program.cs` file.</span></span>

<span data-ttu-id="c791a-126">È possibile usare Azure Storage Client Library hello in qualsiasi tipo di applicazione .NET, tra cui un'app web o servizio di cloud di Azure e le applicazioni desktop e mobile.</span><span class="sxs-lookup"><span data-stu-id="c791a-126">You can use hello Azure Storage Client Library in any type of .NET application, including an Azure cloud service or web app, and desktop and mobile applications.</span></span> <span data-ttu-id="c791a-127">Per semplicità, in questa guida si usa un'applicazione console.</span><span class="sxs-lookup"><span data-stu-id="c791a-127">In this guide, we use a console application for simplicity.</span></span>

## <a name="use-nuget-tooinstall-hello-required-packages"></a><span data-ttu-id="c791a-128">Utilizzare i pacchetti hello necessario tooinstall NuGet</span><span class="sxs-lookup"><span data-stu-id="c791a-128">Use NuGet tooinstall hello required packages</span></span>
<span data-ttu-id="c791a-129">Sono disponibili due pacchetti, è necessario tooreference in toocomplete il progetto in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="c791a-129">There are two packages you need tooreference in your project toocomplete this tutorial:</span></span>

* <span data-ttu-id="c791a-130">[Microsoft Azure Storage Client Library per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): questo pacchetto fornisce l'accesso programmatico toodata risorse nell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c791a-130">[Microsoft Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): This package provides programmatic access toodata resources in your storage account.</span></span>
* <span data-ttu-id="c791a-131">[Libreria Gestione configurazione di Microsoft Azure per .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): questo pacchetto fornisce una classe per l'analisi di una stringa di connessione in un file di configurazione, indipendentemente dalla posizione in cui viene eseguita l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="c791a-131">[Microsoft Azure Configuration Manager library for .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): This package provides a class for parsing a connection string in a configuration file, regardless of where your application is running.</span></span>

<span data-ttu-id="c791a-132">È possibile utilizzare NuGet tooobtain entrambi i pacchetti.</span><span class="sxs-lookup"><span data-stu-id="c791a-132">You can use NuGet tooobtain both packages.</span></span> <span data-ttu-id="c791a-133">A tale scopo, seguire questa procedura:</span><span class="sxs-lookup"><span data-stu-id="c791a-133">Follow these steps:</span></span>

1. <span data-ttu-id="c791a-134">Fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere **Gestisci pacchetti NuGet**.</span><span class="sxs-lookup"><span data-stu-id="c791a-134">Right-click your project in **Solution Explorer** and choose **Manage NuGet Packages**.</span></span>
2. <span data-ttu-id="c791a-135">Cercare online "Windowsazure" e fare clic su **installare** tooinstall hello libreria Client di archiviazione e le relative dipendenze.</span><span class="sxs-lookup"><span data-stu-id="c791a-135">Search online for "WindowsAzure.Storage" and click **Install** tooinstall hello Storage Client Library and its dependencies.</span></span>
3. <span data-ttu-id="c791a-136">Cercare online "WindowsAzure.ConfigurationManager" e fare clic su **installare** tooinstall hello Azure Configuration Manager.</span><span class="sxs-lookup"><span data-stu-id="c791a-136">Search online for "WindowsAzure.ConfigurationManager" and click **Install** tooinstall hello Azure Configuration Manager.</span></span>

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a><span data-ttu-id="c791a-137">Salvare il file app. config di toohello le credenziali di account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="c791a-137">Save your storage account credentials toohello app.config file</span></span>
<span data-ttu-id="c791a-138">A questo punto salvare le credenziali nel file app.config del progetto.</span><span class="sxs-lookup"><span data-stu-id="c791a-138">Next, save your credentials in your project's app.config file.</span></span> <span data-ttu-id="c791a-139">Modifica file app. config hello in modo che venga visualizzato simile toohello di esempio seguente, sostituendo `myaccount` con il nome di account di archiviazione e `mykey` con la chiave di account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c791a-139">Edit hello app.config file so that it appears similar toohello following example, replacing `myaccount` with your storage account name, and `mykey` with your storage account key.</span></span>

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
> versione più recente di Hello dell'emulatore di archiviazione Azure hello non supporta l'archiviazione di File di Azure. <span data-ttu-id="c791a-141">La stringa di connessione deve essere un Account di archiviazione di Azure in hello cloud toowork con l'archiviazione di File di Azure.</span><span class="sxs-lookup"><span data-stu-id="c791a-141">Your connection string must target an Azure Storage Account in hello cloud toowork with Azure File storage.</span></span>

## <a name="add-using-directives"></a><span data-ttu-id="c791a-142">Aggiungere le direttive using</span><span class="sxs-lookup"><span data-stu-id="c791a-142">Add using directives</span></span>
<span data-ttu-id="c791a-143">Aprire hello `Program.cs` file da Esplora soluzioni e aggiungere il seguente hello utilizzo di top toohello direttive del file hello.</span><span class="sxs-lookup"><span data-stu-id="c791a-143">Open hello `Program.cs` file from Solution Explorer, and add hello following using directives toohello top of hello file.</span></span>

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a><span data-ttu-id="c791a-144">Condivisione di file hello accesso a livello di codice</span><span class="sxs-lookup"><span data-stu-id="c791a-144">Access hello file share programmatically</span></span>
<span data-ttu-id="c791a-145">Successivamente, aggiungere hello seguente codice toohello `Main()` stringa di connessione hello tooretrieve metodo (dopo il codice hello illustrato in precedenza).</span><span class="sxs-lookup"><span data-stu-id="c791a-145">Next, add hello following code toohello `Main()` method (after hello code shown above) tooretrieve hello connection string.</span></span> <span data-ttu-id="c791a-146">Questo codice ottiene un file di riferimento toohello creato in precedenza e restituisce la finestra di console toohello contenuto.</span><span class="sxs-lookup"><span data-stu-id="c791a-146">This code gets a reference toohello file we created earlier and outputs its contents toohello console window.</span></span>

```csharp
// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile file = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello file exists.
        if (file.Exists())
        {
            // Write hello contents of hello file toohello console window.
            Console.WriteLine(file.DownloadTextAsync().Result);
        }
    }
}
```

<span data-ttu-id="c791a-147">Eseguire l'output di hello toosee applicazione console hello.</span><span class="sxs-lookup"><span data-stu-id="c791a-147">Run hello console application toosee hello output.</span></span>

## <a name="set-hello-maximum-size-for-a-file-share"></a><span data-ttu-id="c791a-148">Impostare dimensioni massime di hello per una condivisione file</span><span class="sxs-lookup"><span data-stu-id="c791a-148">Set hello maximum size for a file share</span></span>
<span data-ttu-id="c791a-149">A partire dalla versione 5. x di hello Azure Storage Client Library, è possibile impostare set hello quota (o dimensioni massime) per una condivisione di file, in gigabyte.</span><span class="sxs-lookup"><span data-stu-id="c791a-149">Beginning with version 5.x of hello Azure Storage Client Library, you can set set hello quota (or maximum size) for a file share, in gigabytes.</span></span> <span data-ttu-id="c791a-150">È inoltre possibile verificare la quantità di dati è attualmente archiviati nella condivisione di hello toosee.</span><span class="sxs-lookup"><span data-stu-id="c791a-150">You can also check toosee how much data is currently stored on hello share.</span></span>

<span data-ttu-id="c791a-151">Dalla quota hello impostazione per una condivisione, è possibile limitare hello totale dimensioni hello file archiviati nella condivisione di hello.</span><span class="sxs-lookup"><span data-stu-id="c791a-151">By setting hello quota for a share, you can limit hello total size of hello files stored on hello share.</span></span> <span data-ttu-id="c791a-152">Se hello dimensioni totali dei file nella condivisione di hello superano quota hello impostato nella condivisione di hello, il client verrà tooincrease Impossibile hello dimensioni dei file esistenti o creare nuovi file, a meno che tali file sono vuoti.</span><span class="sxs-lookup"><span data-stu-id="c791a-152">If hello total size of files on hello share exceeds hello quota set on hello share, then clients will be unable tooincrease hello size of existing files or create new files, unless those files are empty.</span></span>

<span data-ttu-id="c791a-153">esempio di Hello seguente mostra come toocheck hello utilizzo corrente per una condivisione e la modalità tooset hello quota per la condivisione di hello.</span><span class="sxs-lookup"><span data-stu-id="c791a-153">hello example below shows how toocheck hello current usage for a share and how tooset hello quota for hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Check current usage stats for hello share.
    // Note that hello ShareStats object is part of hello protocol layer for hello File service.
    Microsoft.WindowsAzure.Storage.File.Protocol.ShareStats stats = share.GetStats();
    Console.WriteLine("Current share usage: {0} GB", stats.Usage.ToString());

    // Specify hello maximum size of hello share, in GB.
    // This line sets hello quota toobe 10 GB greater than hello current usage of hello share.
    share.Properties.Quota = 10 + stats.Usage;
    share.SetProperties();

    // Now check hello quota for hello share. Call FetchAttributes() toopopulate hello share's properties.
    share.FetchAttributes();
    Console.WriteLine("Current share quota: {0} GB", share.Properties.Quota);
}
```

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a><span data-ttu-id="c791a-154">Generare la firma di accesso condiviso per un file o una condivisione file</span><span class="sxs-lookup"><span data-stu-id="c791a-154">Generate a shared access signature for a file or file share</span></span>
<span data-ttu-id="c791a-155">A partire dalla versione 5. x di hello Azure Storage Client Library, è possibile generare una firma di accesso condiviso (SAS) per una condivisione file o per un singolo file.</span><span class="sxs-lookup"><span data-stu-id="c791a-155">Beginning with version 5.x of hello Azure Storage Client Library, you can generate a shared access signature (SAS) for a file share or for an individual file.</span></span> <span data-ttu-id="c791a-156">È anche possibile creare un criterio di accesso condiviso per un accesso condiviso toomanage di condivisione file firme.</span><span class="sxs-lookup"><span data-stu-id="c791a-156">You can also create a shared access policy on a file share toomanage shared access signatures.</span></span> <span data-ttu-id="c791a-157">È consigliabile creare un criterio di accesso condiviso, in quanto forniscono un mezzo di revoca hello SAS se questa deve essere compromessa.</span><span class="sxs-lookup"><span data-stu-id="c791a-157">Creating a shared access policy is recommended, as it provides a means of revoking hello SAS if it should be compromised.</span></span>

<span data-ttu-id="c791a-158">Hello di esempio seguente viene creato un criterio di accesso condiviso in una condivisione e quindi utilizza che condividono tooprovide hello i vincoli dei criteri per una firma di accesso condiviso in un file hello.</span><span class="sxs-lookup"><span data-stu-id="c791a-158">hello following example creates a shared access policy on a share, and then uses that policy tooprovide hello constraints for a SAS on a file in hello share.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    string policyName = "sampleSharePolicy" + DateTime.UtcNow.Ticks;

    // Create a new shared access policy and define its constraints.
    SharedAccessFilePolicy sharedPolicy = new SharedAccessFilePolicy()
        {
            SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24),
            Permissions = SharedAccessFilePermissions.Read | SharedAccessFilePermissions.Write
        };

    // Get existing permissions for hello share.
    FileSharePermissions permissions = share.GetPermissions();

    // Add hello shared access policy toohello share's policies. Note that each policy must have a unique name.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    share.SetPermissions(permissions);

    // Generate a SAS for a file in hello share and associate this access policy with it.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");
    CloudFile file = sampleDir.GetFileReference("Log1.txt");
    string sasToken = file.GetSharedAccessSignature(null, policyName);
    Uri fileSasUri = new Uri(file.StorageUri.PrimaryUri.ToString() + sasToken);

    // Create a new CloudFile object from hello SAS, and write some text toohello file.
    CloudFile fileSas = new CloudFile(fileSasUri);
    fileSas.UploadText("This write operation is authenticated via SAS.");
    Console.WriteLine(fileSas.DownloadText());
}
```

<span data-ttu-id="c791a-159">Per altre informazioni sulla creazione e sull'uso di firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](storage-dotnet-shared-access-signature-part-1.md) e [Creare e usare una firma di accesso condiviso con i BLOB di Azure](storage-dotnet-shared-access-signature-part-2.md).</span><span class="sxs-lookup"><span data-stu-id="c791a-159">For more information about creating and using shared access signatures, see [Using Shared Access Signatures (SAS)](storage-dotnet-shared-access-signature-part-1.md) and [Create and use a SAS with Azure Blobs](storage-dotnet-shared-access-signature-part-2.md).</span></span>

## <a name="copy-files"></a><span data-ttu-id="c791a-160">Copiare i file</span><span class="sxs-lookup"><span data-stu-id="c791a-160">Copy files</span></span>
<span data-ttu-id="c791a-161">A partire dalla versione 5. x di hello Azure Storage Client Library, è possibile copiare un file con estensione tooanother, un blob tooa file o un file di blob tooa.</span><span class="sxs-lookup"><span data-stu-id="c791a-161">Beginning with version 5.x of hello Azure Storage Client Library, you can copy a file tooanother file, a file tooa blob, or a blob tooa file.</span></span> <span data-ttu-id="c791a-162">Nelle sezioni successive di hello, viene illustrato come questi tooperform copiare operazioni a livello di codice.</span><span class="sxs-lookup"><span data-stu-id="c791a-162">In hello next sections, we demonstrate how tooperform these copy operations programmatically.</span></span>

<span data-ttu-id="c791a-163">È inoltre possibile utilizzare AzCopy toocopy un file tooanother o toocopy versa di file o viceversa tooa un blob.</span><span class="sxs-lookup"><span data-stu-id="c791a-163">You can also use AzCopy toocopy one file tooanother or toocopy a blob tooa file or vice versa.</span></span> <span data-ttu-id="c791a-164">Vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="c791a-164">See [Transfer data with hello AzCopy Command-Line Utility](storage-use-azcopy.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c791a-165">Se si copia un file di blob tooa o un blob tooa file, è necessario utilizzare un oggetto di origine hello accesso condiviso (firma) tooauthenticate, anche se si copia all'interno di hello stesso account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c791a-165">If you are copying a blob tooa file, or a file tooa blob, you must use a shared access signature (SAS) tooauthenticate hello source object, even if you are copying within hello same storage account.</span></span>
> 
> 

<span data-ttu-id="c791a-166">**Copiare un file con estensione tooanother** hello esempio copia un file con estensione tooanother hello stessa condivisione.</span><span class="sxs-lookup"><span data-stu-id="c791a-166">**Copy a file tooanother file** hello following example copies a file tooanother file in hello same share.</span></span> <span data-ttu-id="c791a-167">Poiché questa operazione di copia copia tra file hello stesso account di archiviazione, è possibile utilizzare una copia di hello tooperform autenticazione chiave condivisa.</span><span class="sxs-lookup"><span data-stu-id="c791a-167">Because this copy operation copies between files in hello same storage account, you can use Shared Key authentication tooperform hello copy.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Get a reference toohello file share we created previously.
CloudFileShare share = fileClient.GetShareReference("logs");

// Ensure that hello share exists.
if (share.Exists())
{
    // Get a reference toohello root directory for hello share.
    CloudFileDirectory rootDir = share.GetRootDirectoryReference();

    // Get a reference toohello directory we created previously.
    CloudFileDirectory sampleDir = rootDir.GetDirectoryReference("CustomLogs");

    // Ensure that hello directory exists.
    if (sampleDir.Exists())
    {
        // Get a reference toohello file we created previously.
        CloudFile sourceFile = sampleDir.GetFileReference("Log1.txt");

        // Ensure that hello source file exists.
        if (sourceFile.Exists())
        {
            // Get a reference toohello destination file.
            CloudFile destFile = sampleDir.GetFileReference("Log1Copy.txt");

            // Start hello copy operation.
            destFile.StartCopy(sourceFile);

            // Write hello contents of hello destination file toohello console window.
            Console.WriteLine(destFile.DownloadText());
        }
    }
}
```

<span data-ttu-id="c791a-168">**Copiare un blob tooa file** hello seguente viene creato un file e copia tooa blob all'interno di hello stesso account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c791a-168">**Copy a file tooa blob** hello following example creates a file and copies it tooa blob within hello same storage account.</span></span> <span data-ttu-id="c791a-169">esempio Hello crea una firma di accesso condiviso per il file di origine hello, quale servizio hello utilizza file di origine toohello tooauthenticate accesso durante l'operazione di copia hello.</span><span class="sxs-lookup"><span data-stu-id="c791a-169">hello example creates a SAS for hello source file, which hello service uses tooauthenticate access toohello source file during hello copy operation.</span></span>

```csharp
// Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create a CloudFileClient object for credentialed access tooAzure File storage.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Create a new file share, if it does not already exist.
CloudFileShare share = fileClient.GetShareReference("sample-share");
share.CreateIfNotExists();

// Create a new file in hello root directory.
CloudFile sourceFile = share.GetRootDirectoryReference().GetFileReference("sample-file.txt");
sourceFile.UploadText("A sample file in hello root directory.");

// Get a reference toohello blob toowhich hello file will be copied.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference("sample-container");
container.CreateIfNotExists();
CloudBlockBlob destBlob = container.GetBlockBlobReference("sample-blob.txt");

// Create a SAS for hello file that's valid for 24 hours.
// Note that when you are copying a file tooa blob, or a blob tooa file, you must use a SAS
// tooauthenticate access toohello source object, even if you are copying within hello same
// storage account.
string fileSas = sourceFile.GetSharedAccessSignature(new SharedAccessFilePolicy()
{
    // Only read permissions are required for hello source file.
    Permissions = SharedAccessFilePermissions.Read,
    SharedAccessExpiryTime = DateTime.UtcNow.AddHours(24)
});

// Construct hello URI toohello source file, including hello SAS token.
Uri fileSasUri = new Uri(sourceFile.StorageUri.PrimaryUri.ToString() + fileSas);

// Copy hello file toohello blob.
destBlob.StartCopy(fileSasUri);

// Write hello contents of hello file toohello console window.
Console.WriteLine("Source file contents: {0}", sourceFile.DownloadText());
Console.WriteLine("Destination blob contents: {0}", destBlob.DownloadText());
```

<span data-ttu-id="c791a-170">È possibile copiare un file di blob tooa hello allo stesso modo.</span><span class="sxs-lookup"><span data-stu-id="c791a-170">You can copy a blob tooa file in hello same way.</span></span> <span data-ttu-id="c791a-171">Se l'oggetto di origine hello è un blob, creare un blob di firma di accesso condiviso tooauthenticate accesso toothat durante l'operazione di copia hello.</span><span class="sxs-lookup"><span data-stu-id="c791a-171">If hello source object is a blob, then create a SAS tooauthenticate access toothat blob during hello copy operation.</span></span>

## <a name="troubleshooting-azure-file-storage-using-metrics"></a><span data-ttu-id="c791a-172">Risoluzione dei problemi di Archiviazione file di Azure con le metriche</span><span class="sxs-lookup"><span data-stu-id="c791a-172">Troubleshooting Azure File storage using metrics</span></span>
<span data-ttu-id="c791a-173">Analisi archiviazione di Azure ora supporta le metriche per Archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="c791a-173">Azure Storage Analytics now supports metrics for Azure File storage.</span></span> <span data-ttu-id="c791a-174">Grazie ai dati di metrica, è possibile monitorare le richieste e diagnosticare i problemi.</span><span class="sxs-lookup"><span data-stu-id="c791a-174">With metrics data, you can trace requests and diagnose issues.</span></span>


<span data-ttu-id="c791a-175">È possibile abilitare la metrica per l'archiviazione di File di Azure da hello [portale Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="c791a-175">You can enable metrics for Azure File storage from hello [Azure Portal](https://portal.azure.com).</span></span> <span data-ttu-id="c791a-176">È inoltre possibile abilitare le metriche a livello di codice dal chiamante hello operazione Set File Service Properties tramite hello API REST o uno dei relativi analoghi in hello libreria Client di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="c791a-176">You can also enable metrics programmatically by calling hello Set File Service Properties operation via hello REST API, or one of its analogues in hello Storage Client Library.</span></span>


<span data-ttu-id="c791a-177">Hello esempio di codice seguente viene illustrato come toouse hello libreria Client di archiviazione per le metriche tooenable .NET per l'archiviazione di File di Azure.</span><span class="sxs-lookup"><span data-stu-id="c791a-177">hello following code example shows how toouse hello Storage Client Library for .NET tooenable metrics for Azure File storage.</span></span>

<span data-ttu-id="c791a-178">In primo luogo, aggiungere hello seguenti `using` tooyour direttive `Program.cs` file inoltre toothose aggiunto nel passaggio precedente:</span><span class="sxs-lookup"><span data-stu-id="c791a-178">First, add hello following `using` directives tooyour `Program.cs` file, in addition toothose you added above:</span></span>

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

<span data-ttu-id="c791a-179">Si noti che, mentre i BLOB di Azure, tabelle di Azure e le code di Azure, utilizzare hello condiviso `ServiceProperties` tipo di hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` dello spazio dei nomi, la memorizzazione dei File di Azure Usa il proprio tipo, hello `FileServiceProperties` tipo di hello `Microsoft.WindowsAzure.Storage.File.Protocol` dello spazio dei nomi.</span><span class="sxs-lookup"><span data-stu-id="c791a-179">Note that while Azure Blobs, Azure Table, and Azure Queues use hello shared `ServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` namespace, Azure File storage uses its own type, hello `FileServiceProperties` type in hello `Microsoft.WindowsAzure.Storage.File.Protocol` namespace.</span></span> <span data-ttu-id="c791a-180">Entrambi gli spazi dei nomi devono fare riferimento dal codice, tuttavia, per hello toocompile di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="c791a-180">Both namespaces must be referenced from your code, however, for hello following code toocompile.</span></span>

```csharp
// Parse your storage connection string from your application's configuration file.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));
// Create hello File service client.
CloudFileClient fileClient = storageAccount.CreateCloudFileClient();

// Set metrics properties for File service.
// Note that hello File service currently uses its own service properties type,
// available in hello Microsoft.WindowsAzure.Storage.File.Protocol namespace.
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

// Read hello metrics properties we just set.
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

<span data-ttu-id="c791a-181">Inoltre, è possibile fare riferimento troppo[archiviazione di File di Azure articolo Troubleshooting](storage-troubleshoot-file-connection-problems.md) per informazioni sulla risoluzione end-to-end.</span><span class="sxs-lookup"><span data-stu-id="c791a-181">Also, you can refer too[Azure File storage Troubleshooting Article](storage-troubleshoot-file-connection-problems.md) for end-to-end troubleshooting guidance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c791a-182">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c791a-182">Next steps</span></span>
<span data-ttu-id="c791a-183">Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="c791a-183">See these links for more information about Azure File storage.</span></span>

### <a name="conceptual-articles-and-videos"></a><span data-ttu-id="c791a-184">Articoli concettuali e video</span><span class="sxs-lookup"><span data-stu-id="c791a-184">Conceptual articles and videos</span></span>
* [<span data-ttu-id="c791a-185">Archiviazione di file in Azure: un file system SMB nel cloud senza problemi per Windows e Linux</span><span class="sxs-lookup"><span data-stu-id="c791a-185">Azure File storage: a frictionless cloud SMB file system for Windows and Linux</span></span>](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [<span data-ttu-id="c791a-186">Come toouse archiviazione di File di Azure con Linux</span><span class="sxs-lookup"><span data-stu-id="c791a-186">How toouse Azure File storage with Linux</span></span>](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a><span data-ttu-id="c791a-187">Supporto degli strumenti per Archiviazione file</span><span class="sxs-lookup"><span data-stu-id="c791a-187">Tooling support for File storage</span></span>
* [<span data-ttu-id="c791a-188">Uso di Azure PowerShell con Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="c791a-188">Using Azure PowerShell with Azure Storage</span></span>](storage-powershell-guide-full.md)
* [<span data-ttu-id="c791a-189">Come toouse AzCopy con archiviazione di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c791a-189">How toouse AzCopy with Microsoft Azure Storage</span></span>](storage-use-azcopy.md)
* [<span data-ttu-id="c791a-190">Con l'archiviazione di Azure hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="c791a-190">Using hello Azure CLI with Azure Storage</span></span>](storage-azure-cli.md#create-and-manage-file-shares)
* [<span data-ttu-id="c791a-191">Risoluzione dei problemi di archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="c791a-191">Troubleshooting Azure File storage problems</span></span>](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a><span data-ttu-id="c791a-192">Riferimento</span><span class="sxs-lookup"><span data-stu-id="c791a-192">Reference</span></span>
* [<span data-ttu-id="c791a-193">Informazioni di riferimento sulla libreria client di archiviazione per .NET</span><span class="sxs-lookup"><span data-stu-id="c791a-193">Storage Client Library for .NET reference</span></span>](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [<span data-ttu-id="c791a-194">Riferimento API REST del servizio File</span><span class="sxs-lookup"><span data-stu-id="c791a-194">File Service REST API reference</span></span>](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a><span data-ttu-id="c791a-195">Post di BLOG</span><span class="sxs-lookup"><span data-stu-id="c791a-195">Blog posts</span></span>
* [<span data-ttu-id="c791a-196">Archiviazione file di Azure è attualmente disponibile a livello generale</span><span class="sxs-lookup"><span data-stu-id="c791a-196">Azure File storage is now generally available</span></span>](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [<span data-ttu-id="c791a-197">Inside Azure File storage (Analisi di Archiviazione file di Azure)</span><span class="sxs-lookup"><span data-stu-id="c791a-197">Inside Azure File storage</span></span>](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [<span data-ttu-id="c791a-198">Introduzione al servizio File di Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c791a-198">Introducing Microsoft Azure File Service</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [<span data-ttu-id="c791a-199">Rendere persistenti le connessioni tooMicrosoft archiviazione di File di Azure</span><span class="sxs-lookup"><span data-stu-id="c791a-199">Persisting connections tooMicrosoft Azure File storage</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
