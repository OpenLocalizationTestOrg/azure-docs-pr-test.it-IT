---
title: aaaCreate e usare una firma di accesso condiviso (SAS) di archiviazione Blob di Azure | Documenti Microsoft
description: Questa esercitazione viene illustrato come toocreate condiviso firme di accesso per l'utilizzo con archiviazione Blob e come tooconsume usarle nelle applicazioni client.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 491e0b3c-76d4-4149-9a80-bbbd683b1f3e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 32004d7d29a190a7ed7234513428c3c156b833b7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="98c8c-103">Firme di accesso condiviso, parte 2: creare e usare una firma di accesso condiviso con l'archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="98c8c-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="98c8c-104">[parte 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) di questa esercitazione è stata fornita una descrizione dettagliata delle firme di accesso condiviso e sono state illustrate le procedure consigliate per utilizzarle.</span><span class="sxs-lookup"><span data-stu-id="98c8c-104">[Part 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="98c8c-105">Parte 2 viene mostrato come toogenerate, quindi utilizzare l'accesso condiviso firme con archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="98c8c-105">Part 2 shows you how toogenerate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="98c8c-106">esempi di Hello vengono scritti in c# e usano hello Azure Storage Client Library per .NET.</span><span class="sxs-lookup"><span data-stu-id="98c8c-106">hello examples are written in C# and use hello Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="98c8c-107">esempi di Hello in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="98c8c-107">hello examples in this tutorial:</span></span>

* <span data-ttu-id="98c8c-108">Generare una firma di accesso condiviso per un contenitore</span><span class="sxs-lookup"><span data-stu-id="98c8c-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="98c8c-109">Generare una firma di accesso condiviso per un BLOB</span><span class="sxs-lookup"><span data-stu-id="98c8c-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="98c8c-110">Creare un accesso archiviati firme toomanage criteri sulle risorse di un contenitore</span><span class="sxs-lookup"><span data-stu-id="98c8c-110">Create a stored access policy toomanage signatures on a container's resources</span></span>
* <span data-ttu-id="98c8c-111">Verificare le firme di accesso condiviso hello in un'applicazione client</span><span class="sxs-lookup"><span data-stu-id="98c8c-111">Test hello shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="98c8c-112">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="98c8c-112">About this tutorial</span></span>
<span data-ttu-id="98c8c-113">In questa esercitazione vengono create due applicazioni console che illustrano la creazione e l'uso delle firme di accesso condiviso per contenitori e BLOB:</span><span class="sxs-lookup"><span data-stu-id="98c8c-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="98c8c-114">**Applicazione 1**: hello applicazione di gestione.</span><span class="sxs-lookup"><span data-stu-id="98c8c-114">**Application 1**: hello management application.</span></span> <span data-ttu-id="98c8c-115">Genera una firma di accesso condiviso per un contenitore e un BLOB.</span><span class="sxs-lookup"><span data-stu-id="98c8c-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="98c8c-116">Include una chiave di accesso di account di archiviazione hello nel codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="98c8c-116">Includes hello storage account access key in source code.</span></span>

<span data-ttu-id="98c8c-117">**Applicazione 2**: hello applicazione client.</span><span class="sxs-lookup"><span data-stu-id="98c8c-117">**Application 2**: hello client application.</span></span> <span data-ttu-id="98c8c-118">Accede alle risorse blob e contenitore utilizza le firme di accesso condiviso hello create con un'applicazione hello prima.</span><span class="sxs-lookup"><span data-stu-id="98c8c-118">Accesses container and blob resources using hello shared access signatures created with hello first application.</span></span> <span data-ttu-id="98c8c-119">Contenitore firme di accesso condiviso di utilizza solo hello tooaccess e delle risorse blob - caso *non* includono una chiave di accesso di account di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="98c8c-119">Uses only hello shared access signatures tooaccess container and blob resources--it does *not* include hello storage account access key.</span></span>

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a><span data-ttu-id="98c8c-120">Parte 1: Creare un accesso condiviso toogenerate all'applicazione console firme</span><span class="sxs-lookup"><span data-stu-id="98c8c-120">Part 1: Create a console application toogenerate shared access signatures</span></span>
<span data-ttu-id="98c8c-121">In primo luogo, verificare di aver hello Azure Storage Client Library per .NET sia installato.</span><span class="sxs-lookup"><span data-stu-id="98c8c-121">First, ensure that you have hello Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="98c8c-122">È possibile installare hello [pacchetto NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "pacchetto NuGet") contenenti hello assembly aggiornate per la libreria client hello.</span><span class="sxs-lookup"><span data-stu-id="98c8c-122">You can install hello [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing hello most up-to-date assemblies for hello client library.</span></span> <span data-ttu-id="98c8c-123">Si tratta di hello metodo per assicurarsi di disporre di correzioni più recenti hello consigliato.</span><span class="sxs-lookup"><span data-stu-id="98c8c-123">This is hello recommended method for ensuring that you have hello most recent fixes.</span></span> <span data-ttu-id="98c8c-124">È inoltre possibile scaricare la libreria client di hello come parte di una versione più recente di hello di hello [Azure SDK per .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="98c8c-124">You can also download hello client library as part of hello most recent version of hello [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="98c8c-125">In Visual Studio creare una nuova applicazione console Windows e assegnare ad essa il nome **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="98c8c-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="98c8c-126">Aggiungere riferimenti troppo[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [Windowsazure](https://www.nuget.org/packages/WindowsAzure.Storage/) utilizzando uno degli approcci seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="98c8c-126">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of hello following approaches:</span></span>

* <span data-ttu-id="98c8c-127">Hello utilizzare [Gestione pacchetti NuGet](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="98c8c-127">Use hello [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="98c8c-128">Selezionare **Progetto** > **Gestisci pacchetti NuGet**, eseguire la ricerca online per ogni pacchetto (Microsoft.WindowsAzure.ConfigurationManager e WindowsAzure.Storage) e installarli.</span><span class="sxs-lookup"><span data-stu-id="98c8c-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="98c8c-129">In alternativa, individuare gli assembly nell'installazione di hello Azure SDK e aggiungere riferimenti toothem:</span><span class="sxs-lookup"><span data-stu-id="98c8c-129">Alternatively, locate these assemblies in your installation of hello Azure SDK and add references toothem:</span></span>
  * <span data-ttu-id="98c8c-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="98c8c-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="98c8c-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="98c8c-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="98c8c-132">Nella parte superiore di hello del file Program.cs hello, aggiungere hello **utilizzando** direttive:</span><span class="sxs-lookup"><span data-stu-id="98c8c-132">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="98c8c-133">Modificare il file app. config hello in modo che contenga un'impostazione di configurazione con una stringa di connessione che punta tooyour account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="98c8c-133">Edit hello app.config file so that it contains a configuration setting with a connection string that points tooyour storage account.</span></span> <span data-ttu-id="98c8c-134">File app. config dovrebbe essere simile toothis uno:</span><span class="sxs-lookup"><span data-stu-id="98c8c-134">Your app.config file should look similar toothis one:</span></span>

```xml
<configuration>
  <startup>
    <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5.2" />
  </startup>
  <appSettings>
    <add key="StorageConnectionString" value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey"/>
  </appSettings>
</configuration>
```

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="98c8c-135">Generare l'URI di una firma di accesso condiviso per un contenitore</span><span class="sxs-lookup"><span data-stu-id="98c8c-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="98c8c-136">toobegin con, aggiungiamo un toogenerate metodo una firma di accesso condiviso in un nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="98c8c-136">toobegin with, we add a method toogenerate a shared access signature on a new container.</span></span> <span data-ttu-id="98c8c-137">In questo caso, la firma hello non è associata a un criterio di accesso archiviati, in modo che esercita hello informazioni hello URI che indica le autorizzazioni di hello e l'ora di scadenza concede.</span><span class="sxs-lookup"><span data-stu-id="98c8c-137">In this case, hello signature is not associated with a stored access policy, so it carries on hello URI hello information indicating its expiry time and hello permissions it grants.</span></span>

<span data-ttu-id="98c8c-138">Innanzitutto, aggiungere codice toohello **Main ()** tooauthenticate metodo accedere tooyour account di archiviazione e creare un nuovo contenitore:</span><span class="sxs-lookup"><span data-stu-id="98c8c-138">First, add code toohello **Main()** method tooauthenticate access tooyour storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls toohello methods created below here...

    //Require user input before closing hello console window.
    Console.ReadLine();
}
```

<span data-ttu-id="98c8c-139">Successivamente, aggiungere un metodo che genera l'errore di firma di accesso condiviso hello contenitore hello e restituisce l'URI di firma hello:</span><span class="sxs-lookup"><span data-stu-id="98c8c-139">Next, add a method that generates hello shared access signature for hello container and returns hello signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set hello expiry time and permissions for hello container.
    //In this case no start time is specified, so hello shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello container, setting hello constraints directly on hello signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="98c8c-140">Aggiungere hello seguendo le linee nella parte inferiore di hello di hello **Main ()** (metodo), prima di chiamare troppo di hello**Console.ReadLine()**, toocall **GetContainerSasUri()** e scrivere hello finestra di console toohello URI di firma:</span><span class="sxs-lookup"><span data-stu-id="98c8c-140">Add hello following lines at hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, toocall **GetContainerSasUri()** and write hello signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="98c8c-141">Compilare ed eseguire toooutput firma di accesso condiviso hello URI per il nuovo contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="98c8c-141">Compile and run toooutput hello shared access signature URI for hello new container.</span></span> <span data-ttu-id="98c8c-142">Hello URI sarà simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="98c8c-142">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="98c8c-143">Dopo aver eseguito codice hello, firma di accesso condiviso hello creato per il contenitore di hello sarà valido per hello 24 ore successive.</span><span class="sxs-lookup"><span data-stu-id="98c8c-143">Once you have run hello code, hello shared access signature you created for hello container will be valid for hello next 24 hours.</span></span> <span data-ttu-id="98c8c-144">firma Hello concede a un client BLOB toolist autorizzazione in un contenitore hello e toowrite nuovo contenitore toohello di BLOB.</span><span class="sxs-lookup"><span data-stu-id="98c8c-144">hello signature grants a client permission toolist blobs in hello container and toowrite new blobs toohello container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="98c8c-145">Generare l'URI di una firma di accesso condiviso per un BLOB</span><span class="sxs-lookup"><span data-stu-id="98c8c-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="98c8c-146">È quindi scrivere toocreate codice simile di un nuovo blob all'interno del contenitore di hello e generare una firma di accesso condiviso per tale.</span><span class="sxs-lookup"><span data-stu-id="98c8c-146">Next, we write similar code toocreate a new blob within hello container and generate a shared access signature for it.</span></span> <span data-ttu-id="98c8c-147">Questa firma di accesso condiviso non è associata a un criterio di accesso archiviati, in modo da includere l'ora di inizio hello, ora di scadenza e le informazioni sulle autorizzazioni in hello URI.</span><span class="sxs-lookup"><span data-stu-id="98c8c-147">This shared access signature is not associated with a stored access policy, so it includes hello start time, expiry time, and permission information in hello URI.</span></span>

<span data-ttu-id="98c8c-148">Aggiungere un nuovo metodo che crea un nuovo blob e scrive alcuni tooit di testo, quindi genera una firma di accesso condiviso e restituisce l'URI di firma hello:</span><span class="sxs-lookup"><span data-stu-id="98c8c-148">Add a new method that creates a new blob and writes some text tooit, then generates a shared access signature and returns hello signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set hello expiry time and permissions for hello blob.
    //In this case, hello start time is specified as a few minutes in hello past, toomitigate clock skew.
    //hello shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate hello shared access signature on hello blob, setting hello constraints directly on hello signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="98c8c-149">Nella parte inferiore di hello di hello **Main ()** metodo, aggiungere hello seguenti righe toocall **GetBlobSasUri()**, prima di chiamare troppo di hello**Console.ReadLine()**e scrivere hello condiviso finestra console toohello URI firma di accesso:</span><span class="sxs-lookup"><span data-stu-id="98c8c-149">At hello bottom of hello **Main()** method, add hello following lines toocall **GetBlobSasUri()**, before hello call too**Console.ReadLine()**, and write hello shared access signature URI toohello console window:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="98c8c-150">Compilare ed eseguire toooutput hello firma di accesso condiviso URI blob nuovo hello.</span><span class="sxs-lookup"><span data-stu-id="98c8c-150">Compile and run toooutput hello shared access signature URI for hello new blob.</span></span> <span data-ttu-id="98c8c-151">Hello URI sarà simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="98c8c-151">hello URI will be similar toohello following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a><span data-ttu-id="98c8c-152">Creare un criterio di accesso archiviati nel contenitore di hello</span><span class="sxs-lookup"><span data-stu-id="98c8c-152">Create a stored access policy on hello container</span></span>
<span data-ttu-id="98c8c-153">A questo punto creare criteri di accesso archiviati nel contenitore di hello, che verrà definiti i vincoli di hello per le firme di accesso condiviso sono associati.</span><span class="sxs-lookup"><span data-stu-id="98c8c-153">Now let's create a stored access policy on hello container, which will define hello constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="98c8c-154">Negli esempi precedenti hello, è specificato l'ora di inizio hello (implicito o esplicito), l'ora di scadenza hello e autorizzazioni hello hello condiviso URI stessa firma di accesso.</span><span class="sxs-lookup"><span data-stu-id="98c8c-154">In hello previous examples, we specified hello start time (implicitly or explicitly), hello expiry time, and hello permissions on hello shared access signature URI itself.</span></span> <span data-ttu-id="98c8c-155">In hello seguono esempi, si specifica questi criteri di accesso archiviato hello e non la firma di accesso condiviso hello.</span><span class="sxs-lookup"><span data-stu-id="98c8c-155">In hello following examples, we specify these on hello stored access policy, not on hello shared access signature.</span></span> <span data-ttu-id="98c8c-156">Questa impostazione consente a questi vincoli senza riemettere hello condiviso toochange accedere firma.</span><span class="sxs-lookup"><span data-stu-id="98c8c-156">Doing so enables us toochange these constraints without reissuing hello shared access signature.</span></span>

<span data-ttu-id="98c8c-157">È possibile toohave uno o più vincoli hello sulla firma di accesso condiviso hello e resto hello ai criteri di accesso archiviato hello.</span><span class="sxs-lookup"><span data-stu-id="98c8c-157">It's possible toohave one or more of hello constraints on hello shared access signature, and hello remainder on hello stored access policy.</span></span> <span data-ttu-id="98c8c-158">Tuttavia, è possibile specificare solo ora di inizio hello, ora di scadenza e le autorizzazioni in una posizione o hello altri.</span><span class="sxs-lookup"><span data-stu-id="98c8c-158">However, you can only specify hello start time, expiry time, and permissions in one place or hello other.</span></span> <span data-ttu-id="98c8c-159">È ad esempio, non è possibile specificare autorizzazioni per la firma di accesso condiviso hello e specificarli anche ai criteri di accesso archiviato hello.</span><span class="sxs-lookup"><span data-stu-id="98c8c-159">For example, you can't specify permissions on hello shared access signature and also specify them on hello stored access policy.</span></span>

<span data-ttu-id="98c8c-160">Quando si aggiunge un contenitore di tooa criteri di accesso archiviati, è necessario ottenere le autorizzazioni esistenti del contenitore di hello, aggiungere il nuovo criterio di accesso hello e quindi impostare le autorizzazioni del contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="98c8c-160">When you add a stored access policy tooa container, you must get hello container's existing permissions, add hello new access policy, and then set hello container's permissions.</span></span>

<span data-ttu-id="98c8c-161">Aggiungere un nuovo metodo che crea un nuovo criterio di accesso archiviati in un contenitore e restituisce il nome di hello del criterio di hello:</span><span class="sxs-lookup"><span data-stu-id="98c8c-161">Add a new method that creates a new stored access policy on a container and returns hello name of hello policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get hello container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add hello new policy toohello container's permissions, and set hello container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="98c8c-162">Nella parte inferiore di hello di hello **Main ()** (metodo), prima di chiamare troppo di hello**Console.ReadLine()**, aggiungere hello seguendo le linee toofirst deselezionare eventuali criteri di accesso esistente e quindi chiamare hello  **CreateSharedAccessPolicy()** metodo:</span><span class="sxs-lookup"><span data-stu-id="98c8c-162">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toofirst clear any existing access policies, and then call hello **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on hello container, which may be optionally used tooprovide constraints for
//shared access signatures on hello container and hello blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="98c8c-163">Quando si cancella i criteri di accesso hello in un contenitore, è innanzitutto necessario ottenere le autorizzazioni esistenti del contenitore hello quindi autorizzazioni crittografato hello, quindi impostare le autorizzazioni di hello nuovamente.</span><span class="sxs-lookup"><span data-stu-id="98c8c-163">When you clear hello access policies on a container, you must first get hello container's existing permissions, then clear hello permissions, then set hello permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a><span data-ttu-id="98c8c-164">Generare una firma di accesso condiviso URI nel contenitore hello che utilizza un criterio di accesso</span><span class="sxs-lookup"><span data-stu-id="98c8c-164">Generate a shared access signature URI on hello container that uses an access policy</span></span>
<span data-ttu-id="98c8c-165">Successivamente, abbiamo creato un'altra firma di accesso condiviso per il contenitore hello creati in precedenza, ma questa volta Associamo firma hello con i criteri di accesso archiviato hello creata nell'esempio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="98c8c-165">Next, we create another shared access signature for hello container that we created earlier, but this time we associate hello signature with hello stored access policy we created in hello previous example.</span></span>

<span data-ttu-id="98c8c-166">Aggiungere un nuovo toogenerate metodo un'altra firma di accesso condiviso per il contenitore di hello:</span><span class="sxs-lookup"><span data-stu-id="98c8c-166">Add a new method toogenerate another shared access signature for hello container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate hello shared access signature on hello container. In this case, all of hello constraints for the
    //shared access signature are specified on hello stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="98c8c-167">Nella parte inferiore di hello di hello **Main ()** (metodo), prima di chiamare troppo di hello**Console.ReadLine()**, aggiungere hello seguente hello toocall righe **GetContainerSasUriWithPolicy** (metodo) :</span><span class="sxs-lookup"><span data-stu-id="98c8c-167">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a><span data-ttu-id="98c8c-168">Generare un URI firma di accesso condiviso in hello Blob che utilizza un criterio di accesso</span><span class="sxs-lookup"><span data-stu-id="98c8c-168">Generate a Shared Access Signature URI on hello Blob That Uses an Access Policy</span></span>
<span data-ttu-id="98c8c-169">Infine, aggiungiamo un simile toocreate metodo un altro blob e generare una firma di accesso condiviso associata a un criterio di accesso archiviati.</span><span class="sxs-lookup"><span data-stu-id="98c8c-169">Finally, we add a similar method toocreate another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="98c8c-170">Aggiungere un nuovo toocreate metodo un blob e generare una firma di accesso condiviso:</span><span class="sxs-lookup"><span data-stu-id="98c8c-170">Add a new method toocreate a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference tooa blob within hello container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text toohello blob. If hello blob does not yet exist, it will be created.
    //If hello blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible tooclients via a shared access signature. " +
    "A stored access policy defines hello constraints for hello signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate hello shared access signature on hello blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return hello URI string for hello container, including hello SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="98c8c-171">Nella parte inferiore di hello di hello **Main ()** (metodo), prima di chiamare troppo di hello**Console.ReadLine()**, aggiungere hello seguente hello toocall righe **GetBlobSasUriWithPolicy** metodo:</span><span class="sxs-lookup"><span data-stu-id="98c8c-171">At hello bottom of hello **Main()** method, before hello call too**Console.ReadLine()**, add hello following lines toocall hello **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="98c8c-172">Hello **Main ()** metodo dovrebbe essere simile al seguente nella sua interezza.</span><span class="sxs-lookup"><span data-stu-id="98c8c-172">hello **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="98c8c-173">Eseguire firma di accesso condiviso hello toowrite finestra della console toohello URI, quindi copiare e incollarli in un file di testo per l'utilizzo nella seconda parte di hello di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="98c8c-173">Run it toowrite hello shared access signature URIs toohello console window, then copy and paste them into a text file for use in hello second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse hello connection string and return a reference toohello storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create hello blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference tooa container toouse for hello sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for hello container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on hello container, which may be optionally used tooprovide constraints for
    //shared access signatures on hello container and hello blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="98c8c-174">Quando si esegue un'applicazione console GenerateSharedAccessSignatures hello, verrà visualizzato il seguente toohello simili di output.</span><span class="sxs-lookup"><span data-stu-id="98c8c-174">When you run hello GenerateSharedAccessSignatures console application, you'll see output similar toohello following.</span></span> <span data-ttu-id="98c8c-175">Queste sono le firme di accesso condiviso hello che è utilizzare nella parte 2 dell'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="98c8c-175">These are hello shared access signatures you use in Part 2 of hello tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a><span data-ttu-id="98c8c-176">Parte 2: Creare un accesso da console applicazione tootest hello condiviso firme</span><span class="sxs-lookup"><span data-stu-id="98c8c-176">Part 2: Create a console application tootest hello shared access signatures</span></span>
<span data-ttu-id="98c8c-177">hello tootest condivisi firme di accesso create negli esempi precedenti hello, viene creata una seconda applicazione console che utilizza le operazioni di hello firme tooperform nel contenitore hello e su un blob.</span><span class="sxs-lookup"><span data-stu-id="98c8c-177">tootest hello shared access signatures created in hello previous examples, we create a second console application that uses hello signatures tooperform operations on hello container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="98c8c-178">Se più di 24 ore sono stati superati poiché è completato hello prima parte dell'esercitazione hello, firme di hello generato non saranno valide.</span><span class="sxs-lookup"><span data-stu-id="98c8c-178">If more than 24 hours have passed since you completed hello first part of hello tutorial, hello signatures you generated will no longer be valid.</span></span> <span data-ttu-id="98c8c-179">In questo caso, eseguire il codice hello in toogenerate applicazione console prima di hello firme di accesso condiviso aggiornata per l'utilizzo nella seconda parte di hello dell'esercitazione hello.</span><span class="sxs-lookup"><span data-stu-id="98c8c-179">In this case, you should run hello code in hello first console application toogenerate fresh shared access signatures for use in hello second part of hello tutorial.</span></span>
>

<span data-ttu-id="98c8c-180">In Visual Studio creare una nuova applicazione console Windows e assegnare ad essa il nome **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="98c8c-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="98c8c-181">Aggiungere riferimenti troppo[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [Windowsazure](https://www.nuget.org/packages/WindowsAzure.Storage/), come in precedenza.</span><span class="sxs-lookup"><span data-stu-id="98c8c-181">Add references too[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="98c8c-182">Nella parte superiore di hello del file Program.cs hello, aggiungere hello **utilizzando** direttive:</span><span class="sxs-lookup"><span data-stu-id="98c8c-182">At hello top of hello Program.cs file, add hello following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="98c8c-183">Nel corpo di hello di hello **Main ()** (metodo), aggiungere hello seguendo le costanti di stringa, la modifica è stato generato nella parte 1 dell'esercitazione hello le firme di accesso toohello condiviso i relativi valori.</span><span class="sxs-lookup"><span data-stu-id="98c8c-183">In hello body of hello **Main()** method, add hello following string constants, changing their values toohello shared access signatures you generated in part 1 of hello tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="98c8c-184">Aggiungere un contenitore della tootry metodo le operazioni utilizzando una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="98c8c-184">Add a method tootry container operations using a shared access signature</span></span>
<span data-ttu-id="98c8c-185">Successivamente, è aggiungere un metodo che esegue il test utilizzando una firma di accesso condiviso per il contenitore di hello alcune operazioni di contenitore.</span><span class="sxs-lookup"><span data-stu-id="98c8c-185">Next, we add a method that tests some container operations using a shared access signature for hello container.</span></span> <span data-ttu-id="98c8c-186">firma di accesso condiviso Hello è tooreturn usato un contenitore toohello riferimento, l'autenticazione contenitore toohello accesso in base alla firma hello da solo.</span><span class="sxs-lookup"><span data-stu-id="98c8c-186">hello shared access signature is used tooreturn a reference toohello container, authenticating access toohello container based on hello signature alone.</span></span>

<span data-ttu-id="98c8c-187">Aggiungere hello tooProgram.cs metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="98c8c-187">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with hello SAS provided.

    //Return a reference toohello container using hello SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list toostore blob URIs returned by a listing operation on hello container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob toohello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello container. ";
        blob.UploadText(blobContent);

        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //List operation: List hello blobs in hello container.
    try
    {
        foreach (ICloudBlob blob in container.ListBlobs())
        {
            blobList.Add(blob);
        }
        Console.WriteLine("List operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("List operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Get a reference tooone of hello blobs in hello container and read it.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        MemoryStream msRead = new MemoryStream();
        msRead.Position = 0;
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            Console.WriteLine(msRead.Length);
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
    Console.WriteLine();

    //Delete operation: Delete a blob in hello container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference(blobList[0].Name);
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="98c8c-188">Hello aggiornamento **Main ()** metodo toocall **UseContainerSAS()** con entrambi hello condiviso firme di accesso creato nel contenitore hello:</span><span class="sxs-lookup"><span data-stu-id="98c8c-188">Update hello **Main()** method toocall **UseContainerSAS()** with both of hello shared access signatures you created on hello container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="98c8c-189">Aggiungere operazioni di blob tootry un metodo utilizzando una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="98c8c-189">Add a method tootry blob operations using a shared access signature</span></span>
<span data-ttu-id="98c8c-190">Infine, è aggiungere un metodo che esegue il test utilizzando una firma di accesso condiviso nel blob hello alcune operazioni di blob.</span><span class="sxs-lookup"><span data-stu-id="98c8c-190">Finally, we add a method that tests some blob operations using a shared access signature on hello blob.</span></span> <span data-ttu-id="98c8c-191">In questo caso, viene usato il costruttore hello **CloudBlockBlob(String)**, passando nella firma di accesso condiviso hello, tooreturn un blob toohello di riferimento.</span><span class="sxs-lookup"><span data-stu-id="98c8c-191">In this case, we use hello constructor **CloudBlockBlob(String)**, passing in hello shared access signature, tooreturn a reference toohello blob.</span></span> <span data-ttu-id="98c8c-192">Nessun altro tipo di autenticazione è obbligatoria. è basato sulla firma hello da solo.</span><span class="sxs-lookup"><span data-stu-id="98c8c-192">No other authentication is required; it's based on hello signature alone.</span></span>

<span data-ttu-id="98c8c-193">Aggiungere hello tooProgram.cs metodo seguente:</span><span class="sxs-lookup"><span data-stu-id="98c8c-193">Add hello following method tooProgram.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using hello SAS provided.

    //Return a reference toohello blob using hello SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob toohello container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions toohello blob. ";
        MemoryStream msWrite = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
        msWrite.Position = 0;
        using (msWrite)
        {
            blob.UploadFromStream(msWrite);
        }
        Console.WriteLine("Write operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Write operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Read operation: Read hello contents of hello blob.
    try
    {
        MemoryStream msRead = new MemoryStream();
        using (msRead)
        {
            blob.DownloadToStream(msRead);
            msRead.Position = 0;
            using (StreamReader reader = new StreamReader(msRead, true))
            {
                string line;
                while ((line = reader.ReadLine()) != null)
                {
                    Console.WriteLine(line);
                }
            }
        }
        Console.WriteLine("Read operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Read operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }

    //Delete operation: Delete hello blob.
    try
    {
        blob.Delete();
        Console.WriteLine("Delete operation succeeded for SAS " + sas);
        Console.WriteLine();
    }
    catch (StorageException e)
    {
        Console.WriteLine("Delete operation failed for SAS " + sas);
        Console.WriteLine("Additional error information: " + e.Message);
        Console.WriteLine();
    }
}
```

<span data-ttu-id="98c8c-194">Hello aggiornamento **Main ()** metodo toocall **UseBlobSAS()** con entrambi hello condiviso firme di accesso creato nel blob hello:</span><span class="sxs-lookup"><span data-stu-id="98c8c-194">Update hello **Main()** method toocall **UseBlobSAS()** with both of hello shared access signatures that you created on hello blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call hello test methods with hello shared access signatures created on hello container, with and without hello access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call hello test methods with hello shared access signatures created on hello blob, with and without hello access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="98c8c-195">Eseguire un'applicazione console hello e osservare toosee di output di hello quali operazioni sono consentite per le firme.</span><span class="sxs-lookup"><span data-stu-id="98c8c-195">Run hello console application and observe hello output toosee which operations are permitted for which signatures.</span></span> <span data-ttu-id="98c8c-196">output di Hello nella finestra di console hello avrà un aspetto simile toohello seguenti:</span><span class="sxs-lookup"><span data-stu-id="98c8c-196">hello output in hello console window will look similar toohello following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="98c8c-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="98c8c-197">Next Steps</span></span>

* [<span data-ttu-id="98c8c-198">Firme di accesso condiviso, parte 1: Hello informazioni modello di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="98c8c-198">Shared Access Signatures, Part 1: Understanding hello SAS Model</span></span>](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [<span data-ttu-id="98c8c-199">Gestire BLOB e accesso in lettura anonimo toocontainers</span><span class="sxs-lookup"><span data-stu-id="98c8c-199">Manage anonymous read access toocontainers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="98c8c-200">Delega dell'accesso con una firma di accesso condiviso (API REST)</span><span class="sxs-lookup"><span data-stu-id="98c8c-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="98c8c-201">Introduzione alla firma di accesso condiviso per tabelle e code</span><span class="sxs-lookup"><span data-stu-id="98c8c-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
