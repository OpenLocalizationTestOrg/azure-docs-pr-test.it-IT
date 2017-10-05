---
title: 'Esercitazione: Crittografare e decrittografare i BLOB in Archiviazione di Azure con Azure Key Vault | Documentazione Microsoft'
description: Come crittografare e decrittografare un BLOB usando la crittografia lato client per Archiviazione di Microsoft Azure con Azure Key Vault.
services: storage
documentationcenter: 
author: adhurwit
manager: jasonsav
editor: tysonn
ms.assetid: 027e8631-c1bf-48c1-9d9b-f6843e88b583
ms.service: storage
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 01/23/2017
ms.author: adhurwit
ms.openlocfilehash: a2a3a4773d33fe6b8589ad8d9d219acda4d1015e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="0e1f2-103">Esercitazione: Crittografare e decrittografare i BLOB in Archiviazione di Microsoft Azure tramite l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="0e1f2-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="0e1f2-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="0e1f2-104">Introduction</span></span>
<span data-ttu-id="0e1f2-105">Questa esercitazione illustra come usare la crittografia di archiviazione lato client con l'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-105">This tutorial covers how to make use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="0e1f2-106">Illustra come crittografare e decrittografare un BLOB in un'applicazione console mediante queste tecnologie.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-106">It walks you through how to encrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="0e1f2-107">**Tempo previsto per il completamento:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="0e1f2-107">**Estimated time to complete:** 20 minutes</span></span>

<span data-ttu-id="0e1f2-108">Per informazioni generali sull'Insieme di credenziali delle chiavi di Azure, vedere [Cos'è l'Insieme di credenziali delle chiavi di Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="0e1f2-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="0e1f2-109">Per informazioni generali sulla crittografia lato client per Archiviazione di Azure, vedere l'articolo relativo alla [crittografia lato client e all'Insieme di credenziali delle chiavi di Azure per Archiviazione di Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="0e1f2-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e1f2-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0e1f2-110">Prerequisites</span></span>
<span data-ttu-id="0e1f2-111">Per completare l'esercitazione, sono necessari gli elementi seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e1f2-111">To complete this tutorial, you must have the following:</span></span>

* <span data-ttu-id="0e1f2-112">Un account di archiviazione Azure</span><span class="sxs-lookup"><span data-stu-id="0e1f2-112">An Azure Storage account</span></span>
* <span data-ttu-id="0e1f2-113">Visual Studio 2013 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="0e1f2-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="0e1f2-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="0e1f2-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="0e1f2-115">Panoramica della crittografia lato client</span><span class="sxs-lookup"><span data-stu-id="0e1f2-115">Overview of client-side encryption</span></span>
<span data-ttu-id="0e1f2-116">Per una panoramica sulla crittografia lato client per Archiviazione di Azure, vedere l'articolo relativo alla [crittografia lato client e all'Insieme di credenziali delle chiavi di Azure per Archiviazione di Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="0e1f2-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span></span>

<span data-ttu-id="0e1f2-117">Ecco una breve descrizione del funzionamento della crittografia lato client:</span><span class="sxs-lookup"><span data-stu-id="0e1f2-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="0e1f2-118">Azure Storage Client SDK genera una chiave di crittografia del contenuto (CEK) che funziona come chiave simmetrica monouso.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-118">The Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="0e1f2-119">I dati del cliente vengono crittografati con questa chiave CEK.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="0e1f2-120">Viene quindi eseguito il wrapping della chiave CEK mediante la chiave di crittografia della chiave (KEK).</span><span class="sxs-lookup"><span data-stu-id="0e1f2-120">The CEK is then wrapped (encrypted) using the key encryption key (KEK).</span></span> <span data-ttu-id="0e1f2-121">La chiave KEK è identificata con un identificatore di chiave e può essere costituita da una coppia di chiavi asimmetriche o da una chiave simmetrica. Può essere gestita localmente o archiviata nell'insieme di credenziali delle chiavi di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-121">The KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="0e1f2-122">Il client di archiviazione non ha mai accesso alla chiave KEK.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-122">The Storage client itself never has access to the KEK.</span></span> <span data-ttu-id="0e1f2-123">Richiama solo l'algoritmo di wrapping della chiave fornito dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-123">It just invokes the key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="0e1f2-124">I clienti possono scegliere di usare provider personalizzati per il wrapping o la rimozione del wrapping delle chiavi, se lo desiderano.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-124">Customers can choose to use custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="0e1f2-125">I dati crittografati vengono quindi caricati nel servizio Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-125">The encrypted data is then uploaded to the Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="0e1f2-126">Impostare l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="0e1f2-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="0e1f2-127">Per procedere con questa esercitazione, è necessario effettuare le operazioni seguenti, descritte nell'esercitazione [Introduzione all'Insieme di credenziali delle chiavi di Azure](../../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="0e1f2-127">In order to proceed with this tutorial, you need to do the following steps, which are outlined in the tutorial  [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="0e1f2-128">Creare un insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-128">Create a key vault.</span></span>
* <span data-ttu-id="0e1f2-129">Aggiungere una chiave o un segreto all'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-129">Add a key or secret to the key vault.</span></span>
* <span data-ttu-id="0e1f2-130">Registrare un'applicazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="0e1f2-131">Autorizzare l'applicazione a usare la chiave o il segreto.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-131">Authorize the application to use the key or secret.</span></span>

<span data-ttu-id="0e1f2-132">Prendere nota dei valori di ClientID e ClientSecret generati durante la registrazione di un'applicazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-132">Make note of the ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="0e1f2-133">Creare entrambe le chiavi nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-133">Create both keys in the key vault.</span></span> <span data-ttu-id="0e1f2-134">Per il resto dell'esercitazione si presuppone che siano stati usati i nomi seguenti: ContosoKeyVault e TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-134">We assume for the rest of the tutorial that you have used the following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="0e1f2-135">Creare un'applicazione console con pacchetti e AppSettings</span><span class="sxs-lookup"><span data-stu-id="0e1f2-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="0e1f2-136">In Visual Studio creare una nuova applicazione console.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="0e1f2-137">Aggiungere i pacchetti NuGet necessari nella console Gestione pacchetti.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-137">Add necessary nuget packages in the Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is the latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="0e1f2-138">Aggiungere AppSettings al file App.Config.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-138">Add AppSettings to the App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="0e1f2-139">Aggiungere le istruzioni `using` seguenti e assicurarsi di aggiungere al progetto un riferimento a System.Configuration.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-139">Add the following `using` statements and make sure to add a reference to System.Configuration to the project.</span></span>

```csharp
using Microsoft.IdentityModel.Clients.ActiveDirectory;
using System.Configuration;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.Azure.KeyVault;
using System.Threading;        
using System.IO;
```

## <a name="add-a-method-to-get-a-token-to-your-console-application"></a><span data-ttu-id="0e1f2-140">Aggiungere un metodo per ottenere un token per l'applicazione console</span><span class="sxs-lookup"><span data-stu-id="0e1f2-140">Add a method to get a token to your console application</span></span>
<span data-ttu-id="0e1f2-141">Il metodo seguente viene usato dalle classi dell'insieme di credenziali delle chiavi che devono essere autenticate per l'accesso all'insieme di credenziali delle chiavi dell'utente.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-141">The following method is used by Key Vault classes that need to authenticate for access to your key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed to obtain the JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="0e1f2-142">Accedere all'archiviazione e all'insieme di credenziali delle chiavi nel programma</span><span class="sxs-lookup"><span data-stu-id="0e1f2-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="0e1f2-143">Nella funzione Main aggiungere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-143">In the Main function, add the following code.</span></span>

```csharp
// This is standard code to interact with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// The Resolver object is used to interact with Key Vault for Azure Storage.
// This is where the GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="0e1f2-144">Modelli a oggetti dell'insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="0e1f2-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="0e1f2-145">È importante capire che esistono in realtà due modelli a oggetti dell'insieme di credenziali chiave da tenere presenti: uno è basato sull'API REST (spazio dei nomi KeyVault) e l'altro è un'estensione per la crittografia lato client.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-145">It is important to understand that there are actually two Key Vault object models to be aware of: one is based on the REST API (KeyVault namespace) and the other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="0e1f2-146">Il client dell'insieme di credenziali delle chiavi interagisce con l'API REST e interpreta correttamente i segreti e le chiavi Web JSON per i due tipi di oggetti contenuti nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-146">The Key Vault Client interacts with the REST API and understands JSON Web Keys and secrets for the two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="0e1f2-147">Le estensioni dell'insieme di credenziali chiave sono classi che sembrano create appositamente per la crittografia lato client in Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-147">The Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="0e1f2-148">Contengono un'interfaccia per le chiavi, ovvero IKey, e classi basate sul concetto di resolver di chiavi.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-148">They contain an interface for keys (IKey) and classes based on the concept of a Key Resolver.</span></span> <span data-ttu-id="0e1f2-149">Esistono due implementazioni di IKey che è necessario conoscere: RSAKey e SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-149">There are two implementations of IKey that you need to know: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="0e1f2-150">Coincidono con gli oggetti contenuti in un insieme di credenziali chiave, ma a questo punto sono classi indipendenti (pertanto la chiave e il segreto recuperati dal client insieme di credenziali chiave non implementano IKey).</span><span class="sxs-lookup"><span data-stu-id="0e1f2-150">Now they happen to coincide with the things that are contained in a Key Vault, but at this point they are independent classes (so the Key and Secret retrieved by the Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="0e1f2-151">Crittografare un BLOB ed eseguire il caricamento</span><span class="sxs-lookup"><span data-stu-id="0e1f2-151">Encrypt blob and upload</span></span>
<span data-ttu-id="0e1f2-152">Aggiungere il codice seguente per crittografare un BLOB e caricarlo nell'account di Archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-152">Add the following code to encrypt a blob and upload it to your Azure storage account.</span></span> <span data-ttu-id="0e1f2-153">Il metodo **ResolveKeyAsync** usato restituisce un'interfaccia IKey.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-153">The **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve the key that you created previously.
// The IKey that is returned here is an RsaKey.
// Remember that we used the names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use the RSA key to encrypt by setting it in the BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using the UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="0e1f2-154">Di seguito è riportato uno screenshot del [portale di Azure classico](https://manage.windowsazure.com) relativo a un BLOB che è stato crittografato mediante la crittografia lato client con una chiave archiviata nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-154">Following is a screenshot from the [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="0e1f2-155">La proprietà **KeyId** è l'URI della chiave nell'insieme di credenziali delle chiavi che funziona come chiave KEK.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-155">The **KeyId** property is the URI for the key in Key Vault that acts as the KEK.</span></span> <span data-ttu-id="0e1f2-156">La proprietà **EncryptedKey** contiene la versione crittografata della chiave CEK.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-156">The **EncryptedKey** property contains the encrypted version of the CEK.</span></span>

![Screenshot che mostra i metadati BLOB con i metadati di crittografia](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="0e1f2-158">Se si osserva il costruttore BlobEncryptionPolicy, è possibile notare che è in grado di accettare una chiave e/o un resolver.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-158">If you look at the BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="0e1f2-159">Tenere presente che al momento non è possibile usare un resolver per la crittografia perché non supporta attualmente una chiave predefinita.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="0e1f2-160">Decrittografare un BLOB ed eseguire il download</span><span class="sxs-lookup"><span data-stu-id="0e1f2-160">Decrypt blob and download</span></span>
<span data-ttu-id="0e1f2-161">La decrittografia è l'operazione per cui si rivelano utili le classi Resolver.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-161">Decryption is really when using the Resolver classes make sense.</span></span> <span data-ttu-id="0e1f2-162">L'ID della chiave usata per la crittografia è associato al BLOB nei relativi metadati, pertanto non è necessario recuperare la chiave e ricordare l'associazione tra la chiave e il BLOB.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-162">The ID of the key used for encryption is associated with the blob in its metadata, so there is no reason for you to retrieve the key and remember the association between key and blob.</span></span> <span data-ttu-id="0e1f2-163">È sufficiente verificare che la chiave rimanga nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-163">You just have to make sure that the key remains in Key Vault.</span></span>   

<span data-ttu-id="0e1f2-164">La chiave privata di una chiave RSA resta nell'insieme di credenziali delle chiavi. Perché venga eseguita la decrittografia, la chiave crittografata nei metadati del BLOB che contengono la chiave CEK viene pertanto inviata all'insieme di credenziali delle chiavi per la decrittografia.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-164">The private key of an RSA Key remains in Key Vault, so for decryption to occur, the Encrypted Key from the blob metadata that contains the CEK is sent to Key Vault for decryption.</span></span>

<span data-ttu-id="0e1f2-165">Aggiungere quanto segue per decrittografare il BLOB appena caricato.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-165">Add the following to decrypt the blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass the resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="0e1f2-166">Esiste un paio di altri tipi di resolver per semplificare la gestione delle chiavi, ovvero AggregateKeyResolver e CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-166">There are a couple of other kinds of resolvers to make key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="0e1f2-167">Uso dei segreti dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="0e1f2-167">Use Key Vault secrets</span></span>
<span data-ttu-id="0e1f2-168">Per usare un segreto con la crittografia lato client, usare la classe SymmetricKey, dal momento che un segreto è in pratica una chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-168">The way to use a secret with client-side encryption is via the SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="0e1f2-169">Come indicato in precedenza però, un segreto nell'insieme di credenziali delle chiavi non corrisponde esattamente a una classe SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-169">But, as noted above, a secret in Key Vault does not map exactly to a SymmetricKey.</span></span> <span data-ttu-id="0e1f2-170">Tenere presenti le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="0e1f2-170">There are a few things to understand:</span></span>

* <span data-ttu-id="0e1f2-171">La chiave in una classe SymmetricKey deve avere una lunghezza fissa: 128, 192, 256, 384 o 512 bit.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-171">The key in a SymmetricKey has to be a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="0e1f2-172">La chiave in una classe SymmetricKey deve essere con codifica Base64.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-172">The key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="0e1f2-173">Un segreto dell'insieme di credenziali delle chiavi da usare come SymmetricKey deve avere come tipo di contenuto "application/octet-stream" nell'insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-173">A Key Vault secret that will be used as a SymmetricKey needs to have a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="0e1f2-174">Di seguito è riportato un esempio di PowerShell per la creazione di un segreto nell'insieme di credenziali delle chiavi che può essere usato come SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="0e1f2-175">Si noti che il valore hardcoded $key è solo a scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-175">Please note that the hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="0e1f2-176">È possibile generare questa chiave nel codice personale.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-176">In your own code you'll want to generate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     The characters are in the ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute the VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="0e1f2-177">Nell'applicazione console è possibile usare la stessa chiamata descritta precedentemente per recuperare questo segreto come SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-177">In your console application, you can use the same call as before to retrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="0e1f2-178">È tutto.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-178">That's it.</span></span> <span data-ttu-id="0e1f2-179">Buon lavoro.</span><span class="sxs-lookup"><span data-stu-id="0e1f2-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e1f2-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0e1f2-180">Next steps</span></span>
<span data-ttu-id="0e1f2-181">Per altre informazioni sull'uso di Archiviazione di Microsoft Azure con C#, vedere [Libreria client di archiviazione di Microsoft Azure per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e1f2-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="0e1f2-182">Per altre informazioni sull'API REST per i BLOB, vedere [API REST del servizio BLOB](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="0e1f2-182">For more information about the Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="0e1f2-183">Per le informazioni più recenti su Archiviazione di Microsoft Azure, visitare il [blog del relativo team](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="0e1f2-183">For the latest information on Microsoft Azure Storage, go to the [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
