---
title: Creare e usare una firma di accesso condiviso (SAS) con Archiviazione BLOB di Azure | Microsoft Docs
description: Questa esercitazione illustra come creare firme di accesso condiviso da usare con l'archiviazione BLOB e come usarle nelle applicazioni client.
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
ms.openlocfilehash: ba78dd2bbcc68ffffeba59b1623891126baf656f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a><span data-ttu-id="5915b-103">Firme di accesso condiviso, parte 2: creare e usare una firma di accesso condiviso con l'archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="5915b-103">Shared Access Signatures, Part 2: Create and use a SAS with Blob storage</span></span>

<span data-ttu-id="5915b-104">[parte 1](storage-dotnet-shared-access-signature-part-1.md) di questa esercitazione è stata fornita una descrizione dettagliata delle firme di accesso condiviso e sono state illustrate le procedure consigliate per utilizzarle.</span><span class="sxs-lookup"><span data-stu-id="5915b-104">[Part 1](storage-dotnet-shared-access-signature-part-1.md) of this tutorial explored shared access signatures (SAS) and explained best practices for using them.</span></span> <span data-ttu-id="5915b-105">La parte 2 illustra come generare e poi usare le firme di accesso condiviso con l'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="5915b-105">Part 2 shows you how to generate and then use shared access signatures with Blob storage.</span></span> <span data-ttu-id="5915b-106">Negli esempi, scritti in C#, viene utilizzata la libreria client di archiviazione di Azure per .NET.</span><span class="sxs-lookup"><span data-stu-id="5915b-106">The examples are written in C# and use the Azure Storage Client Library for .NET.</span></span> <span data-ttu-id="5915b-107">Gli esempi inclusi in questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="5915b-107">The examples in this tutorial:</span></span>

* <span data-ttu-id="5915b-108">Generare una firma di accesso condiviso per un contenitore</span><span class="sxs-lookup"><span data-stu-id="5915b-108">Generate a shared access signature on a container</span></span>
* <span data-ttu-id="5915b-109">Generare una firma di accesso condiviso per un BLOB</span><span class="sxs-lookup"><span data-stu-id="5915b-109">Generate a shared access signature on a blob</span></span>
* <span data-ttu-id="5915b-110">Creare criteri di accesso archiviati per gestire le firme per le risorse di un contenitore</span><span class="sxs-lookup"><span data-stu-id="5915b-110">Create a stored access policy to manage signatures on a container's resources</span></span>
* <span data-ttu-id="5915b-111">Testare le firme di accesso condiviso in un'applicazione client</span><span class="sxs-lookup"><span data-stu-id="5915b-111">Test the shared access signatures in a client application</span></span>

## <a name="about-this-tutorial"></a><span data-ttu-id="5915b-112">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="5915b-112">About this tutorial</span></span>
<span data-ttu-id="5915b-113">In questa esercitazione vengono create due applicazioni console che illustrano la creazione e l'uso delle firme di accesso condiviso per contenitori e BLOB:</span><span class="sxs-lookup"><span data-stu-id="5915b-113">In this tutorial, we create two console applications that demonstrate creating and using shared access signatures for containers and blobs:</span></span>

<span data-ttu-id="5915b-114">**Applicazione 1**: applicazione di gestione.</span><span class="sxs-lookup"><span data-stu-id="5915b-114">**Application 1**: The management application.</span></span> <span data-ttu-id="5915b-115">Genera una firma di accesso condiviso per un contenitore e un BLOB.</span><span class="sxs-lookup"><span data-stu-id="5915b-115">Generates a shared access signature for a container and a blob.</span></span> <span data-ttu-id="5915b-116">Include la chiave di accesso dell'account di archiviazione nel codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="5915b-116">Includes the storage account access key in source code.</span></span>

<span data-ttu-id="5915b-117">**Applicazione 2**: applicazione client.</span><span class="sxs-lookup"><span data-stu-id="5915b-117">**Application 2**: The client application.</span></span> <span data-ttu-id="5915b-118">Accede alle risorse di contenitore e BLOB usando le firme di accesso condiviso create con la prima applicazione.</span><span class="sxs-lookup"><span data-stu-id="5915b-118">Accesses container and blob resources using the shared access signatures created with the first application.</span></span> <span data-ttu-id="5915b-119">Usa solo le firme di accesso condiviso per accedere alle risorse di contenitore e BLOB. *Non* include la chiave di accesso dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5915b-119">Uses only the shared access signatures to access container and blob resources--it does *not* include the storage account access key.</span></span>

## <a name="part-1-create-a-console-application-to-generate-shared-access-signatures"></a><span data-ttu-id="5915b-120">Parte 1: creare un'applicazione console per generare firme di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="5915b-120">Part 1: Create a console application to generate shared access signatures</span></span>
<span data-ttu-id="5915b-121">In primo luogo verificare che la libreria client di archiviazione di Azure per .NET sia installata.</span><span class="sxs-lookup"><span data-stu-id="5915b-121">First, ensure that you have the Azure Storage Client Library for .NET installed.</span></span> <span data-ttu-id="5915b-122">È possibile installare il [pacchetto NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "pacchetto NuGet") contenente gli assembly più aggiornati per la libreria client.</span><span class="sxs-lookup"><span data-stu-id="5915b-122">You can install the [NuGet package](http://nuget.org/packages/WindowsAzure.Storage/ "NuGet package") containing the most up-to-date assemblies for the client library.</span></span> <span data-ttu-id="5915b-123">Questo è il metodo consigliato per verificare se si dispone delle correzioni più recenti.</span><span class="sxs-lookup"><span data-stu-id="5915b-123">This is the recommended method for ensuring that you have the most recent fixes.</span></span> <span data-ttu-id="5915b-124">È anche possibile scaricare la libreria client inclusa nella versione più recente di [Azure SDK per .NET](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="5915b-124">You can also download the client library as part of the most recent version of the [Azure SDK for .NET](https://azure.microsoft.com/downloads/).</span></span>

<span data-ttu-id="5915b-125">In Visual Studio creare una nuova applicazione console Windows e assegnare ad essa il nome **GenerateSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="5915b-125">In Visual Studio, create a new Windows console application and name it **GenerateSharedAccessSignatures**.</span></span> <span data-ttu-id="5915b-126">Aggiungere i riferimenti a [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) usando uno degli approcci seguenti:</span><span class="sxs-lookup"><span data-stu-id="5915b-126">Add references to [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/) by using one of the following approaches:</span></span>

* <span data-ttu-id="5915b-127">Usare la [Gestione pacchetti NuGet](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="5915b-127">Use the [NuGet package manager](https://docs.nuget.org/consume/installing-nuget) in Visual Studio.</span></span> <span data-ttu-id="5915b-128">Selezionare **Progetto** > **Gestisci pacchetti NuGet**, eseguire la ricerca online per ogni pacchetto (Microsoft.WindowsAzure.ConfigurationManager e WindowsAzure.Storage) e installarli.</span><span class="sxs-lookup"><span data-stu-id="5915b-128">Select **Project** > **Manage NuGet Packages**, search online for each package (Microsoft.WindowsAzure.ConfigurationManager and WindowsAzure.Storage) and install them.</span></span>
* <span data-ttu-id="5915b-129">In alternativa, individuare gli assembly nell'installazione di Azure SDK e aggiungervi i riferimenti:</span><span class="sxs-lookup"><span data-stu-id="5915b-129">Alternatively, locate these assemblies in your installation of the Azure SDK and add references to them:</span></span>
  * <span data-ttu-id="5915b-130">Microsoft.WindowsAzure.Configuration.dll</span><span class="sxs-lookup"><span data-stu-id="5915b-130">Microsoft.WindowsAzure.Configuration.dll</span></span>
  * <span data-ttu-id="5915b-131">Microsoft.WindowsAzure.Storage.dll</span><span class="sxs-lookup"><span data-stu-id="5915b-131">Microsoft.WindowsAzure.Storage.dll</span></span>

<span data-ttu-id="5915b-132">All'inizio del file Program.cs aggiungere le direttive **Using** seguenti:</span><span class="sxs-lookup"><span data-stu-id="5915b-132">At the top of the Program.cs file, add the following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="5915b-133">Modificare il file app.config in modo che contenga un'impostazione di configurazione con una stringa di connessione che punta all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="5915b-133">Edit the app.config file so that it contains a configuration setting with a connection string that points to your storage account.</span></span> <span data-ttu-id="5915b-134">Il file app.config dovrebbe essere simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5915b-134">Your app.config file should look similar to this one:</span></span>

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a><span data-ttu-id="5915b-135">Generare l'URI di una firma di accesso condiviso per un contenitore</span><span class="sxs-lookup"><span data-stu-id="5915b-135">Generate a shared access signature URI for a container</span></span>
<span data-ttu-id="5915b-136">Per iniziare, viene aggiunto un metodo per generare una firma di accesso condiviso per un nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="5915b-136">To begin with, we add a method to generate a shared access signature on a new container.</span></span> <span data-ttu-id="5915b-137">In questo caso la firma non è associata a criteri di accesso archiviati, pertanto include nell'URI le informazioni relative alla scadenza e alle autorizzazioni concesse.</span><span class="sxs-lookup"><span data-stu-id="5915b-137">In this case, the signature is not associated with a stored access policy, so it carries on the URI the information indicating its expiry time and the permissions it grants.</span></span>

<span data-ttu-id="5915b-138">In primo luogo, aggiungere al metodo **Main()** il codice per autenticare l'accesso all'account di archiviazione e creare un nuovo contenitore:</span><span class="sxs-lookup"><span data-stu-id="5915b-138">First, add code to the **Main()** method to authenticate access to your storage account and create a new container:</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Insert calls to the methods created below here...

    //Require user input before closing the console window.
    Console.ReadLine();
}
```

<span data-ttu-id="5915b-139">Aggiungere quindi un metodo che genera la firma di accesso condiviso per il contenitore e restituisce l'URI della firma:</span><span class="sxs-lookup"><span data-stu-id="5915b-139">Next, add a method that generates the shared access signature for the container and returns the signature URI:</span></span>

```csharp
static string GetContainerSasUri(CloudBlobContainer container)
{
    //Set the expiry time and permissions for the container.
    //In this case no start time is specified, so the shared access signature becomes valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Write;

    //Generate the shared access signature on the container, setting the constraints directly on the signature.
    string sasContainerToken = container.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="5915b-140">Aggiungere le righe seguenti alla fine del metodo **Main()**, prima della chiamata a **Console.ReadLine()**, per chiamare **GetContainerSasUri()** e scrivere l'URI della firma nella finestra della console:</span><span class="sxs-lookup"><span data-stu-id="5915b-140">Add the following lines at the bottom of the **Main()** method, before the call to **Console.ReadLine()**, to call **GetContainerSasUri()** and write the signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for the container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="5915b-141">Compilare ed eseguire nell'output l'URI della firma di accesso condiviso per il nuovo contenitore.</span><span class="sxs-lookup"><span data-stu-id="5915b-141">Compile and run to output the shared access signature URI for the new container.</span></span> <span data-ttu-id="5915b-142">L'URI sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5915b-142">The URI will be similar to the following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

<span data-ttu-id="5915b-143">Dopo avere eseguito il codice, la firma di accesso condiviso creata per il contenitore rimarrà valida per le 24 ore successive.</span><span class="sxs-lookup"><span data-stu-id="5915b-143">Once you have run the code, the shared access signature you created for the container will be valid for the next 24 hours.</span></span> <span data-ttu-id="5915b-144">La firma concede l'autorizzazione per elencare i BLOB e scrivere nuovi BLOB nel contenitore.</span><span class="sxs-lookup"><span data-stu-id="5915b-144">The signature grants a client permission to list blobs in the container and to write new blobs to the container.</span></span>

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a><span data-ttu-id="5915b-145">Generare l'URI di una firma di accesso condiviso per un BLOB</span><span class="sxs-lookup"><span data-stu-id="5915b-145">Generate a shared access signature URI for a blob</span></span>
<span data-ttu-id="5915b-146">A questo punto viene scritto codice simile per creare un nuovo BLOB all'interno del contenitore e per generarvi una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5915b-146">Next, we write similar code to create a new blob within the container and generate a shared access signature for it.</span></span> <span data-ttu-id="5915b-147">Tale firma non è associata a criteri di accesso archiviati, pertanto include nell'URI le informazioni relative all'ora di inizio, alla scadenza e alle autorizzazioni.</span><span class="sxs-lookup"><span data-stu-id="5915b-147">This shared access signature is not associated with a stored access policy, so it includes the start time, expiry time, and permission information in the URI.</span></span>

<span data-ttu-id="5915b-148">Aggiungere un nuovo metodo che crea un nuovo BLOB e vi scrive del testo, quindi genera una firma di accesso condiviso e restituisce l'URI della firma:</span><span class="sxs-lookup"><span data-stu-id="5915b-148">Add a new method that creates a new blob and writes some text to it, then generates a shared access signature and returns the signature URI:</span></span>

```csharp
static string GetBlobSasUri(CloudBlobContainer container)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblob.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a shared access signature (SAS).";
    blob.UploadText(blobContent);

    //Set the expiry time and permissions for the blob.
    //In this case, the start time is specified as a few minutes in the past, to mitigate clock skew.
    //The shared access signature will be valid immediately.
    SharedAccessBlobPolicy sasConstraints = new SharedAccessBlobPolicy();
    sasConstraints.SharedAccessStartTime = DateTimeOffset.UtcNow.AddMinutes(-5);
    sasConstraints.SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24);
    sasConstraints.Permissions = SharedAccessBlobPermissions.Read | SharedAccessBlobPermissions.Write;

    //Generate the shared access signature on the blob, setting the constraints directly on the signature.
    string sasBlobToken = blob.GetSharedAccessSignature(sasConstraints);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="5915b-149">Alla fine del metodo **Main()**, prima della chiamata a **Console.ReadLine()**, aggiungere le righe seguenti per chiamare **GetBlobSasUri()** e scrivere l'URI della firma di accesso condiviso nella finestra della console:</span><span class="sxs-lookup"><span data-stu-id="5915b-149">At the bottom of the **Main()** method, add the following lines to call **GetBlobSasUri()**, before the call to **Console.ReadLine()**, and write the shared access signature URI to the console window:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

<span data-ttu-id="5915b-150">Compilare ed eseguire nell'output l'URI della firma di accesso condiviso per il nuovo BLOB.</span><span class="sxs-lookup"><span data-stu-id="5915b-150">Compile and run to output the shared access signature URI for the new blob.</span></span> <span data-ttu-id="5915b-151">L'URI sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5915b-151">The URI will be similar to the following:</span></span>

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-the-container"></a><span data-ttu-id="5915b-152">Creare criteri di accesso archiviati per il contenitore</span><span class="sxs-lookup"><span data-stu-id="5915b-152">Create a stored access policy on the container</span></span>
<span data-ttu-id="5915b-153">A questo punto verranno creati criteri di accesso archiviati per il contenitore che consentiranno di definire i vincoli per le eventuali firme di accesso condiviso ad essi associate.</span><span class="sxs-lookup"><span data-stu-id="5915b-153">Now let's create a stored access policy on the container, which will define the constraints for any shared access signatures that are associated with it.</span></span>

<span data-ttu-id="5915b-154">Negli esempi precedenti l'ora di inizio (implicitamente o esplicitamente), la scadenza e le autorizzazioni sono state specificate nell'URI stesso della firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5915b-154">In the previous examples, we specified the start time (implicitly or explicitly), the expiry time, and the permissions on the shared access signature URI itself.</span></span> <span data-ttu-id="5915b-155">Negli esempi seguenti questi parametri vengono specificati nei criteri di accesso archiviati, non nella firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5915b-155">In the following examples, we specify these on the stored access policy, not on the shared access signature.</span></span> <span data-ttu-id="5915b-156">In tal modo sarà possibile modificare questi vincoli senza creare nuovamente la firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5915b-156">Doing so enables us to change these constraints without reissuing the shared access signature.</span></span>

<span data-ttu-id="5915b-157">È possibile specificare uno o più vincoli nella firma di accesso condiviso e quelli rimanenti nei criteri di accesso archiviati.</span><span class="sxs-lookup"><span data-stu-id="5915b-157">It's possible to have one or more of the constraints on the shared access signature, and the remainder on the stored access policy.</span></span> <span data-ttu-id="5915b-158">Tuttavia, non è possibile specificare l'ora di inizio, la scadenza e le autorizzazioni in entrambe le posizioni.</span><span class="sxs-lookup"><span data-stu-id="5915b-158">However, you can only specify the start time, expiry time, and permissions in one place or the other.</span></span> <span data-ttu-id="5915b-159">Ad esempio, non è possibile specificare le autorizzazioni nella firma di accesso condiviso e specificarli anche nei criteri di accesso archiviati.</span><span class="sxs-lookup"><span data-stu-id="5915b-159">For example, you can't specify permissions on the shared access signature and also specify them on the stored access policy.</span></span>

<span data-ttu-id="5915b-160">Quando si aggiunge un criterio di accesso archiviato a un contenitore, è necessario ottenere le autorizzazioni del contenitore esistente, aggiungere il nuovo criterio di accesso e quindi impostare le autorizzazioni del contenitore.</span><span class="sxs-lookup"><span data-stu-id="5915b-160">When you add a stored access policy to a container, you must get the container's existing permissions, add the new access policy, and then set the container's permissions.</span></span>

<span data-ttu-id="5915b-161">Aggiungere un nuovo metodo che crea nuovi criteri di accesso archiviati su un contenitore e restituisce il nome dei criteri:</span><span class="sxs-lookup"><span data-stu-id="5915b-161">Add a new method that creates a new stored access policy on a container and returns the name of the policy:</span></span>

```csharp
static void CreateSharedAccessPolicy(CloudBlobClient blobClient, CloudBlobContainer container,
    string policyName)
{
    //Get the container's existing permissions.
    BlobContainerPermissions permissions = container.GetPermissions();

    //Create a new shared access policy and define its constraints.
    SharedAccessBlobPolicy sharedPolicy = new SharedAccessBlobPolicy()
    {
        SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddHours(24),
        Permissions = SharedAccessBlobPermissions.Write | SharedAccessBlobPermissions.List | SharedAccessBlobPermissions.Read
    };

    //Add the new policy to the container's permissions, and set the container's permissions.
    permissions.SharedAccessPolicies.Add(policyName, sharedPolicy);
    container.SetPermissions(permissions);
}
```

<span data-ttu-id="5915b-162">Alla fine del metodo **Main()**, prima della chiamata a **Console.ReadLine()**, aggiungere le righe seguenti per cancellare prima di tutto eventuali criteri di accesso esistenti e quindi per chiamare il metodo **CreateSharedAccessPolicy()**:</span><span class="sxs-lookup"><span data-stu-id="5915b-162">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to first clear any existing access policies, and then call the **CreateSharedAccessPolicy()** method:</span></span>

```csharp
//Clear any existing access policies on container.
BlobContainerPermissions perms = container.GetPermissions();
perms.SharedAccessPolicies.Clear();
container.SetPermissions(perms);

//Create a new access policy on the container, which may be optionally used to provide constraints for
//shared access signatures on the container and the blob.
string sharedAccessPolicyName = "tutorialpolicy";
CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);
```

<span data-ttu-id="5915b-163">Quando si cancella un criterio di accesso in un contenitore, è necessario prima ottenere le autorizzazioni del contenitore esistente, quindi cancellare le autorizzazioni e infine reimpostarle.</span><span class="sxs-lookup"><span data-stu-id="5915b-163">When you clear the access policies on a container, you must first get the container's existing permissions, then clear the permissions, then set the permissions again.</span></span>

### <a name="generate-a-shared-access-signature-uri-on-the-container-that-uses-an-access-policy"></a><span data-ttu-id="5915b-164">Generare l'URI di una firma di accesso condiviso per un contenitore che usa criteri di accesso</span><span class="sxs-lookup"><span data-stu-id="5915b-164">Generate a shared access signature URI on the container that uses an access policy</span></span>
<span data-ttu-id="5915b-165">Viene quindi creata un'altra firma di accesso condiviso per il contenitore creato in precedenza, ma questa volta la firma viene associata ai criteri di accesso archiviati creati nell'esempio precedente.</span><span class="sxs-lookup"><span data-stu-id="5915b-165">Next, we create another shared access signature for the container that we created earlier, but this time we associate the signature with the stored access policy we created in the previous example.</span></span>

<span data-ttu-id="5915b-166">Aggiungere un nuovo metodo per generare un'altra firma di accesso condiviso per il contenitore:</span><span class="sxs-lookup"><span data-stu-id="5915b-166">Add a new method to generate another shared access signature for the container:</span></span>

```csharp
static string GetContainerSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Generate the shared access signature on the container. In this case, all of the constraints for the
    //shared access signature are specified on the stored access policy.
    string sasContainerToken = container.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return container.Uri + sasContainerToken;
}
```

<span data-ttu-id="5915b-167">Alla fine del metodo **Main()**, prima della chiamata a **Console.ReadLine()**, aggiungere le righe seguenti per chiamare il metodo **GetContainerSasUriWithPolicy**:</span><span class="sxs-lookup"><span data-stu-id="5915b-167">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetContainerSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-the-blob-that-uses-an-access-policy"></a><span data-ttu-id="5915b-168">Generazione dell'URI di una firma di accesso condiviso per un BLOB che utilizza criteri di accesso</span><span class="sxs-lookup"><span data-stu-id="5915b-168">Generate a Shared Access Signature URI on the Blob That Uses an Access Policy</span></span>
<span data-ttu-id="5915b-169">Viene infine aggiunto un metodo simile per creare un altro BLOB e generare una firma di accesso condiviso associata a criteri di accesso archiviati.</span><span class="sxs-lookup"><span data-stu-id="5915b-169">Finally, we add a similar method to create another blob and generate a shared access signature that's associated with a stored access policy.</span></span>

<span data-ttu-id="5915b-170">Aggiungere un nuovo metodo per creare un BLOB e generare una firma di accesso condiviso:</span><span class="sxs-lookup"><span data-stu-id="5915b-170">Add a new method to create a blob and generate a shared access signature:</span></span>

```csharp
static string GetBlobSasUriWithPolicy(CloudBlobContainer container, string policyName)
{
    //Get a reference to a blob within the container.
    CloudBlockBlob blob = container.GetBlockBlobReference("sasblobpolicy.txt");

    //Upload text to the blob. If the blob does not yet exist, it will be created.
    //If the blob does exist, its existing content will be overwritten.
    string blobContent = "This blob will be accessible to clients via a shared access signature. " +
    "A stored access policy defines the constraints for the signature.";
    MemoryStream ms = new MemoryStream(Encoding.UTF8.GetBytes(blobContent));
    ms.Position = 0;
    using (ms)
    {
        blob.UploadFromStream(ms);
    }

    //Generate the shared access signature on the blob.
    string sasBlobToken = blob.GetSharedAccessSignature(null, policyName);

    //Return the URI string for the container, including the SAS token.
    return blob.Uri + sasBlobToken;
}
```

<span data-ttu-id="5915b-171">Alla fine del metodo **Main()**, prima della chiamata a **Console.ReadLine()**, aggiungere le righe seguenti per chiamare il metodo **GetBlobSasUriWithPolicy**:</span><span class="sxs-lookup"><span data-stu-id="5915b-171">At the bottom of the **Main()** method, before the call to **Console.ReadLine()**, add the following lines to call the **GetBlobSasUriWithPolicy** method:</span></span>

```csharp
//Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

<span data-ttu-id="5915b-172">L'intero metodo **Main()** dovrebbe ora essere simile al seguente.</span><span class="sxs-lookup"><span data-stu-id="5915b-172">The **Main()** method should now look like this in its entirety.</span></span> <span data-ttu-id="5915b-173">Eseguirlo per scrivere gli URI delle firme di accesso condiviso nella finestra della console, quindi copiarli e incollarli in un file di testo per utilizzarli nella seconda parte dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5915b-173">Run it to write the shared access signature URIs to the console window, then copy and paste them into a text file for use in the second part of this tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    //Parse the connection string and return a reference to the storage account.
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(CloudConfigurationManager.GetSetting("StorageConnectionString"));

    //Create the blob client object.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    //Get a reference to a container to use for the sample code, and create it if it does not exist.
    CloudBlobContainer container = blobClient.GetContainerReference("sascontainer");
    container.CreateIfNotExists();

    //Generate a SAS URI for the container, without a stored access policy.
    Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, without a stored access policy.
    Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
    Console.WriteLine();

    //Clear any existing access policies on container.
    BlobContainerPermissions perms = container.GetPermissions();
    perms.SharedAccessPolicies.Clear();
    container.SetPermissions(perms);

    //Create a new access policy on the container, which may be optionally used to provide constraints for
    //shared access signatures on the container and the blob.
    string sharedAccessPolicyName = "tutorialpolicy";
    CreateSharedAccessPolicy(blobClient, container, sharedAccessPolicyName);

    //Generate a SAS URI for the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    //Generate a SAS URI for a blob within the container, using a stored access policy to set constraints on the SAS.
    Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
    Console.WriteLine();

    Console.ReadLine();
}
```

<span data-ttu-id="5915b-174">Quando si esegue l'applicazione console GenerateSharedAccessSignatures, l'output sarà simile a quello seguente.</span><span class="sxs-lookup"><span data-stu-id="5915b-174">When you run the GenerateSharedAccessSignatures console application, you'll see output similar to the following.</span></span> <span data-ttu-id="5915b-175">Queste sono le firme di accesso condiviso usate nella parte 2 dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5915b-175">These are the shared access signatures you use in Part 2 of the tutorial.</span></span>

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-to-test-the-shared-access-signatures"></a><span data-ttu-id="5915b-176">Parte 2: creare un'applicazione console per testare le firme di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="5915b-176">Part 2: Create a console application to test the shared access signatures</span></span>
<span data-ttu-id="5915b-177">Per testare le firme di accesso condiviso create negli esempi precedenti, viene creata una seconda applicazione console che usa le firme per eseguire operazioni sul contenitore e su un BLOB.</span><span class="sxs-lookup"><span data-stu-id="5915b-177">To test the shared access signatures created in the previous examples, we create a second console application that uses the signatures to perform operations on the container and on a blob.</span></span>

> [!NOTE]
> <span data-ttu-id="5915b-178">Se sono passate più di 24 ore da quando è stata completata la prima parte dell'esercitazione, le firme generate non saranno più valide.</span><span class="sxs-lookup"><span data-stu-id="5915b-178">If more than 24 hours have passed since you completed the first part of the tutorial, the signatures you generated will no longer be valid.</span></span> <span data-ttu-id="5915b-179">In questo caso, è necessario eseguire il codice nella prima applicazione console per generare nuove firme di accesso condiviso da usare nella seconda parte dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5915b-179">In this case, you should run the code in the first console application to generate fresh shared access signatures for use in the second part of the tutorial.</span></span>
>

<span data-ttu-id="5915b-180">In Visual Studio creare una nuova applicazione console Windows e assegnare ad essa il nome **ConsumeSharedAccessSignatures**.</span><span class="sxs-lookup"><span data-stu-id="5915b-180">In Visual Studio, create a new Windows console application and name it **ConsumeSharedAccessSignatures**.</span></span> <span data-ttu-id="5915b-181">Aggiungere i riferimenti a [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), come è già stato fatto in precedenza.</span><span class="sxs-lookup"><span data-stu-id="5915b-181">Add references to [Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) and [WindowsAzure.Storage](https://www.nuget.org/packages/WindowsAzure.Storage/), as you did previously.</span></span>

<span data-ttu-id="5915b-182">All'inizio del file Program.cs aggiungere le direttive **Using** seguenti:</span><span class="sxs-lookup"><span data-stu-id="5915b-182">At the top of the Program.cs file, add the following **using** directives:</span></span>

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="5915b-183">Nel corpo del metodo **Main()** aggiungere le seguenti costanti di stringa, modificando i valori in base alle firme di accesso condiviso generate nella parte 1 dell'esercitazione.</span><span class="sxs-lookup"><span data-stu-id="5915b-183">In the body of the **Main()** method, add the following string constants, changing their values to the shared access signatures you generated in part 1 of the tutorial.</span></span>

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-to-try-container-operations-using-a-shared-access-signature"></a><span data-ttu-id="5915b-184">Aggiungere un metodo per testare le operazioni su contenitore con una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="5915b-184">Add a method to try container operations using a shared access signature</span></span>
<span data-ttu-id="5915b-185">Viene ora aggiunto un metodo per testare alcune operazioni sul contenitore con una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5915b-185">Next, we add a method that tests some container operations using a shared access signature for the container.</span></span> <span data-ttu-id="5915b-186">La firma di accesso condiviso viene usata per restituire un riferimento al contenitore, autenticando l'accesso al contenitore sulla base della sola firma.</span><span class="sxs-lookup"><span data-stu-id="5915b-186">The shared access signature is used to return a reference to the container, authenticating access to the container based on the signature alone.</span></span>

<span data-ttu-id="5915b-187">Aggiungere il metodo seguente a Program.cs:</span><span class="sxs-lookup"><span data-stu-id="5915b-187">Add the following method to Program.cs:</span></span>

```csharp
static void UseContainerSAS(string sas)
{
    //Try performing container operations with the SAS provided.

    //Return a reference to the container using the SAS URI.
    CloudBlobContainer container = new CloudBlobContainer(new Uri(sas));

    //Create a list to store blob URIs returned by a listing operation on the container.
    List<ICloudBlob> blobList = new List<ICloudBlob>();

    //Write operation: write a new blob to the container.
    try
    {
        CloudBlockBlob blob = container.GetBlockBlobReference("blobCreatedViaSAS.txt");
        string blobContent = "This blob was created with a shared access signature granting write permissions to the container. ";
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

    //List operation: List the blobs in the container.
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

    //Read operation: Get a reference to one of the blobs in the container and read it.
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

    //Delete operation: Delete a blob in the container.
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

<span data-ttu-id="5915b-188">Aggiornare il metodo **Main()** in modo che chiami **UseContainerSAS()** con entrambe le firme di accesso condiviso create per il contenitore:</span><span class="sxs-lookup"><span data-stu-id="5915b-188">Update the **Main()** method to call **UseContainerSAS()** with both of the shared access signatures you created on the container:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    Console.ReadLine();
}
```

### <a name="add-a-method-to-try-blob-operations-using-a-shared-access-signature"></a><span data-ttu-id="5915b-189">Aggiungere un metodo per testare le operazioni su BLOB con una firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="5915b-189">Add a method to try blob operations using a shared access signature</span></span>
<span data-ttu-id="5915b-190">Viene infine aggiunto un metodo per testare alcune operazioni sul BLOB con una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="5915b-190">Finally, we add a method that tests some blob operations using a shared access signature on the blob.</span></span> <span data-ttu-id="5915b-191">In questo caso viene usato il costruttore **CloudBlockBlob(String)**, passando nella firma di accesso condiviso, per restituire un riferimento al BLOB.</span><span class="sxs-lookup"><span data-stu-id="5915b-191">In this case, we use the constructor **CloudBlockBlob(String)**, passing in the shared access signature, to return a reference to the blob.</span></span> <span data-ttu-id="5915b-192">Non è richiesto un altro tipo di autenticazione; è basato esclusivamente sulla firma.</span><span class="sxs-lookup"><span data-stu-id="5915b-192">No other authentication is required; it's based on the signature alone.</span></span>

<span data-ttu-id="5915b-193">Aggiungere il metodo seguente a Program.cs:</span><span class="sxs-lookup"><span data-stu-id="5915b-193">Add the following method to Program.cs:</span></span>

```csharp
static void UseBlobSAS(string sas)
{
    //Try performing blob operations using the SAS provided.

    //Return a reference to the blob using the SAS URI.
    CloudBlockBlob blob = new CloudBlockBlob(new Uri(sas));

    //Write operation: Write a new blob to the container.
    try
    {
        string blobContent = "This blob was created with a shared access signature granting write permissions to the blob. ";
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

    //Read operation: Read the contents of the blob.
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

    //Delete operation: Delete the blob.
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

<span data-ttu-id="5915b-194">Aggiornare il metodo **Main()** in modo che chiami **UseBlobSAS()** con entrambe le firme di accesso condiviso create nel BLOB:</span><span class="sxs-lookup"><span data-stu-id="5915b-194">Update the **Main()** method to call **UseBlobSAS()** with both of the shared access signatures that you created on the blob:</span></span>

```csharp
static void Main(string[] args)
{
    string containerSAS = "<your container SAS>";
    string blobSAS = "<your blob SAS>";
    string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    string blobSASWithAccessPolicy = "<your blob SAS with access policy>";

    //Call the test methods with the shared access signatures created on the container, with and without the access policy.
    UseContainerSAS(containerSAS);
    UseContainerSAS(containerSASWithAccessPolicy);

    //Call the test methods with the shared access signatures created on the blob, with and without the access policy.
    UseBlobSAS(blobSAS);
    UseBlobSAS(blobSASWithAccessPolicy);

    Console.ReadLine();
}
```

<span data-ttu-id="5915b-195">Eseguire l'applicazione console e osservare l'output per verificare le operazioni consentite in base alle firme.</span><span class="sxs-lookup"><span data-stu-id="5915b-195">Run the console application and observe the output to see which operations are permitted for which signatures.</span></span> <span data-ttu-id="5915b-196">L'output nella finestra della console sarà simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="5915b-196">The output in the console window will look similar to the following:</span></span>

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: The remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: The remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a><span data-ttu-id="5915b-197">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5915b-197">Next Steps</span></span>

* [<span data-ttu-id="5915b-198">Firme di accesso condiviso, parte 1: informazioni sul modello di firma di accesso condiviso</span><span class="sxs-lookup"><span data-stu-id="5915b-198">Shared Access Signatures, Part 1: Understanding the SAS Model</span></span>](storage-dotnet-shared-access-signature-part-1.md)
* [<span data-ttu-id="5915b-199">Gestire l'accesso in lettura anonimo a contenitori e BLOB</span><span class="sxs-lookup"><span data-stu-id="5915b-199">Manage anonymous read access to containers and blobs</span></span>](storage-manage-access-to-resources.md)
* [<span data-ttu-id="5915b-200">Delega dell'accesso con una firma di accesso condiviso (API REST)</span><span class="sxs-lookup"><span data-stu-id="5915b-200">Delegating access with a shared access signature (REST API)</span></span>](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [<span data-ttu-id="5915b-201">Introduzione alla firma di accesso condiviso per tabelle e code</span><span class="sxs-lookup"><span data-stu-id="5915b-201">Introducing Table and Queue SAS</span></span>](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
