---
title: 'Esercitazione: Crittografare e decrittografare i BLOB in Archiviazione di Azure con Azure Key Vault | Documentazione Microsoft'
description: Come tooencrypt e la decrittografia di un blob mediante la crittografia lato client per l'archiviazione di Microsoft Azure insieme di credenziali chiave di Azure.
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
ms.openlocfilehash: e387dd419a51b5b1df62d10ead97268e8295ff56
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a><span data-ttu-id="7f8de-103">Esercitazione: Crittografare e decrittografare i BLOB in Archiviazione di Microsoft Azure tramite l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="7f8de-103">Tutorial: Encrypt and decrypt blobs in Microsoft Azure Storage using Azure Key Vault</span></span>
## <a name="introduction"></a><span data-ttu-id="7f8de-104">Introduzione</span><span class="sxs-lookup"><span data-stu-id="7f8de-104">Introduction</span></span>
<span data-ttu-id="7f8de-105">Questa esercitazione sono trattati come toomake utilizzare di crittografia di archiviazione lato client con l'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f8de-105">This tutorial covers how toomake use of client-side storage encryption with Azure Key Vault.</span></span> <span data-ttu-id="7f8de-106">Illustra come tooencrypt e la decrittografia di un blob in un'applicazione console tramite tali tecnologie.</span><span class="sxs-lookup"><span data-stu-id="7f8de-106">It walks you through how tooencrypt and decrypt a blob in a console application using these technologies.</span></span>

<span data-ttu-id="7f8de-107">**Toocomplete tempo stimato:** 20 minuti</span><span class="sxs-lookup"><span data-stu-id="7f8de-107">**Estimated time toocomplete:** 20 minutes</span></span>

<span data-ttu-id="7f8de-108">Per informazioni generali sull'Insieme di credenziali delle chiavi di Azure, vedere [Cos'è l'Insieme di credenziali delle chiavi di Azure?](../../key-vault/key-vault-whatis.md)</span><span class="sxs-lookup"><span data-stu-id="7f8de-108">For overview information about Azure Key Vault, see [What is Azure Key Vault?](../../key-vault/key-vault-whatis.md).</span></span>

<span data-ttu-id="7f8de-109">Per informazioni generali sulla crittografia lato client per Archiviazione di Azure, vedere l'articolo relativo alla [crittografia lato client e all'Insieme di credenziali delle chiavi di Azure per Archiviazione di Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7f8de-109">For overview information about client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7f8de-110">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7f8de-110">Prerequisites</span></span>
<span data-ttu-id="7f8de-111">toocomplete questa esercitazione, è necessario disporre di hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="7f8de-111">toocomplete this tutorial, you must have hello following:</span></span>

* <span data-ttu-id="7f8de-112">Un account di archiviazione Azure</span><span class="sxs-lookup"><span data-stu-id="7f8de-112">An Azure Storage account</span></span>
* <span data-ttu-id="7f8de-113">Visual Studio 2013 o versioni successive</span><span class="sxs-lookup"><span data-stu-id="7f8de-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="7f8de-114">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7f8de-114">Azure PowerShell</span></span>

## <a name="overview-of-client-side-encryption"></a><span data-ttu-id="7f8de-115">Panoramica della crittografia lato client</span><span class="sxs-lookup"><span data-stu-id="7f8de-115">Overview of client-side encryption</span></span>
<span data-ttu-id="7f8de-116">Per una panoramica sulla crittografia lato client per Archiviazione di Azure, vedere l'articolo relativo alla [crittografia lato client e all'Insieme di credenziali delle chiavi di Azure per Archiviazione di Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span><span class="sxs-lookup"><span data-stu-id="7f8de-116">For an overview of client-side encryption for Azure Storage, see [Client-Side Encryption and Azure Key Vault for Microsoft Azure Storage](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)</span></span>

<span data-ttu-id="7f8de-117">Ecco una breve descrizione del funzionamento della crittografia lato client:</span><span class="sxs-lookup"><span data-stu-id="7f8de-117">Here is a brief description of how client side encryption works:</span></span>

1. <span data-ttu-id="7f8de-118">Hello Azure Storage client SDK genera una chiave di crittografia del contenuto (CEK), che è una chiave simmetrica con un utilizzo.</span><span class="sxs-lookup"><span data-stu-id="7f8de-118">hello Azure Storage client SDK generates a content encryption key (CEK), which is a one-time-use symmetric key.</span></span>
2. <span data-ttu-id="7f8de-119">I dati del cliente vengono crittografati con questa chiave CEK.</span><span class="sxs-lookup"><span data-stu-id="7f8de-119">Customer data is encrypted using this CEK.</span></span>
3. <span data-ttu-id="7f8de-120">Hello CEK viene eseguito il wrapping (crittografata) con chiave di crittografia della chiave hello (CHIAVI).</span><span class="sxs-lookup"><span data-stu-id="7f8de-120">hello CEK is then wrapped (encrypted) using hello key encryption key (KEK).</span></span> <span data-ttu-id="7f8de-121">Hello KEK è identificato da un identificatore di chiave e può essere una coppia di chiavi asimmetriche o di una chiave simmetrica e possono essere gestito in locale o memorizzato nell'insieme di credenziali chiave di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f8de-121">hello KEK is identified by a key identifier and can be an asymmetric key pair or a symmetric key and can be managed locally or stored in Azure Key Vault.</span></span> <span data-ttu-id="7f8de-122">client di archiviazione Hello stesso non ha mai accesso toohello KEK.</span><span class="sxs-lookup"><span data-stu-id="7f8de-122">hello Storage client itself never has access toohello KEK.</span></span> <span data-ttu-id="7f8de-123">Richiama solo l'algoritmo di wrapping delle chiavi hello fornito dall'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="7f8de-123">It just invokes hello key wrapping algorithm that is provided by Key Vault.</span></span> <span data-ttu-id="7f8de-124">I clienti possono scegliere toouse provider personalizzati per la chiave di ritorno a capo/annullamento del wrapping se desiderano.</span><span class="sxs-lookup"><span data-stu-id="7f8de-124">Customers can choose toouse custom providers for key wrapping/unwrapping if they want.</span></span>
4. <span data-ttu-id="7f8de-125">Hello dati crittografati viene quindi caricato toohello servizio di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f8de-125">hello encrypted data is then uploaded toohello Azure Storage service.</span></span>

## <a name="set-up-your-azure-key-vault"></a><span data-ttu-id="7f8de-126">Impostare l'insieme di credenziali delle chiavi di Azure</span><span class="sxs-lookup"><span data-stu-id="7f8de-126">Set up your Azure Key Vault</span></span>
<span data-ttu-id="7f8de-127">In ordine tooproceed in questa esercitazione, è necessario hello toodo alla procedura seguente, che sono descritte nell'esercitazione hello [introduzione insieme credenziali chiavi Azure](../../key-vault/key-vault-get-started.md):</span><span class="sxs-lookup"><span data-stu-id="7f8de-127">In order tooproceed with this tutorial, you need toodo hello following steps, which are outlined in hello tutorial  [Get started with Azure Key Vault](../../key-vault/key-vault-get-started.md):</span></span>

* <span data-ttu-id="7f8de-128">Creare un insieme di credenziali delle chiavi.</span><span class="sxs-lookup"><span data-stu-id="7f8de-128">Create a key vault.</span></span>
* <span data-ttu-id="7f8de-129">Aggiungere una chiave o un insieme di credenziali chiave segreta toohello.</span><span class="sxs-lookup"><span data-stu-id="7f8de-129">Add a key or secret toohello key vault.</span></span>
* <span data-ttu-id="7f8de-130">Registrare un'applicazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7f8de-130">Register an application with Azure Active Directory.</span></span>
* <span data-ttu-id="7f8de-131">Autorizzare hello applicazione toouse hello chiave o il segreto.</span><span class="sxs-lookup"><span data-stu-id="7f8de-131">Authorize hello application toouse hello key or secret.</span></span>

<span data-ttu-id="7f8de-132">Assicurarsi di annotare hello ClientID e ClientSecret che sono stati generati durante la registrazione di un'applicazione con Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="7f8de-132">Make note of hello ClientID and ClientSecret that were generated when registering an application with Azure Active Directory.</span></span>

<span data-ttu-id="7f8de-133">Creare entrambe le chiavi nell'insieme di credenziali chiave hello.</span><span class="sxs-lookup"><span data-stu-id="7f8de-133">Create both keys in hello key vault.</span></span> <span data-ttu-id="7f8de-134">Per rest hello di esercitazione hello si presuppone che si usa hello seguenti nomi: ContosoKeyVault e TestRSAKey1.</span><span class="sxs-lookup"><span data-stu-id="7f8de-134">We assume for hello rest of hello tutorial that you have used hello following names: ContosoKeyVault and TestRSAKey1.</span></span>

## <a name="create-a-console-application-with-packages-and-appsettings"></a><span data-ttu-id="7f8de-135">Creare un'applicazione console con pacchetti e AppSettings</span><span class="sxs-lookup"><span data-stu-id="7f8de-135">Create a console application with packages and AppSettings</span></span>
<span data-ttu-id="7f8de-136">In Visual Studio creare una nuova applicazione console.</span><span class="sxs-lookup"><span data-stu-id="7f8de-136">In Visual Studio, create a new console application.</span></span>

<span data-ttu-id="7f8de-137">Aggiungere pacchetti nuget necessari nella Console di gestione pacchetti hello.</span><span class="sxs-lookup"><span data-stu-id="7f8de-137">Add necessary nuget packages in hello Package Manager Console.</span></span>

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

<span data-ttu-id="7f8de-138">Aggiungere AppSettings toohello app. config.</span><span class="sxs-lookup"><span data-stu-id="7f8de-138">Add AppSettings toohello App.Config.</span></span>

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

<span data-ttu-id="7f8de-139">Aggiungere il seguente hello `using` tooadd che crea un progetto di riferimento tooSystem.Configuration toohello e istruzioni.</span><span class="sxs-lookup"><span data-stu-id="7f8de-139">Add hello following `using` statements and make sure tooadd a reference tooSystem.Configuration toohello project.</span></span>

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a><span data-ttu-id="7f8de-140">Aggiungere un tooget metodo un'applicazione console tooyour token</span><span class="sxs-lookup"><span data-stu-id="7f8de-140">Add a method tooget a token tooyour console application</span></span>
<span data-ttu-id="7f8de-141">metodo seguente Hello viene utilizzato dalle classi di insieme di credenziali chiave che è necessario per l'insieme di credenziali chiave di accesso tooyour tooauthenticate.</span><span class="sxs-lookup"><span data-stu-id="7f8de-141">hello following method is used by Key Vault classes that need tooauthenticate for access tooyour key vault.</span></span>

```csharp
private async static Task<string> GetToken(string authority, string resource, string scope)
{
    var authContext = new AuthenticationContext(authority);
    ClientCredential clientCred = new ClientCredential(
        ConfigurationManager.AppSettings["clientId"],
        ConfigurationManager.AppSettings["clientSecret"]);
    AuthenticationResult result = await authContext.AcquireTokenAsync(resource, clientCred);

    if (result == null)
        throw new InvalidOperationException("Failed tooobtain hello JWT token");

    return result.AccessToken;
}
```

## <a name="access-storage-and-key-vault-in-your-program"></a><span data-ttu-id="7f8de-142">Accedere all'archiviazione e all'insieme di credenziali delle chiavi nel programma</span><span class="sxs-lookup"><span data-stu-id="7f8de-142">Access Storage and Key Vault in your program</span></span>
<span data-ttu-id="7f8de-143">Nella funzione Main hello, aggiungere hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="7f8de-143">In hello Main function, add hello following code.</span></span>

```csharp
// This is standard code toointeract with Blob storage.
StorageCredentials creds = new StorageCredentials(
    ConfigurationManager.AppSettings["accountName"],
       ConfigurationManager.AppSettings["accountKey"]);
CloudStorageAccount account = new CloudStorageAccount(creds, useHttps: true);
CloudBlobClient client = account.CreateCloudBlobClient();
CloudBlobContainer contain = client.GetContainerReference(ConfigurationManager.AppSettings["container"]);
contain.CreateIfNotExists();

// hello Resolver object is used toointeract with Key Vault for Azure Storage.
// This is where hello GetToken method from above is used.
KeyVaultKeyResolver cloudResolver = new KeyVaultKeyResolver(GetToken);
```

> [!NOTE]
> <span data-ttu-id="7f8de-144">Modelli a oggetti dell'insieme di credenziali chiave</span><span class="sxs-lookup"><span data-stu-id="7f8de-144">Key Vault Object Models</span></span>
> 
> <span data-ttu-id="7f8de-145">È importante che esistono effettivamente due oggetti insieme di credenziali chiave toounderstand modelli toobe comunicata: una si basa sull'API REST (spazio dei nomi KeyVault) hello e altri hello è un'estensione per la crittografia lato client.</span><span class="sxs-lookup"><span data-stu-id="7f8de-145">It is important toounderstand that there are actually two Key Vault object models toobe aware of: one is based on hello REST API (KeyVault namespace) and hello other is an extension for client-side encryption.</span></span>
> 
> <span data-ttu-id="7f8de-146">Chiave dell'insieme di credenziali Client Hello interagisce con hello API REST e riconosce i segreti hello due tipi di elementi contenuti nell'insieme di credenziali chiave e le chiavi Web JSON.</span><span class="sxs-lookup"><span data-stu-id="7f8de-146">hello Key Vault Client interacts with hello REST API and understands JSON Web Keys and secrets for hello two kinds of things that are contained in Key Vault.</span></span>
> 
> <span data-ttu-id="7f8de-147">le estensioni di insieme di credenziali chiave di Hello sono classi che sembrano create appositamente per la crittografia lato client in archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="7f8de-147">hello Key Vault Extensions are classes that seem specifically created for client-side encryption in Azure Storage.</span></span> <span data-ttu-id="7f8de-148">Contengono un'interfaccia per le chiavi (IKey) e le classi basate sul concetto di hello di un Resolver di chiave.</span><span class="sxs-lookup"><span data-stu-id="7f8de-148">They contain an interface for keys (IKey) and classes based on hello concept of a Key Resolver.</span></span> <span data-ttu-id="7f8de-149">Esistono due implementazioni di che è necessario tooknow IKey: RSAKey e SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="7f8de-149">There are two implementations of IKey that you need tooknow: RSAKey and SymmetricKey.</span></span> <span data-ttu-id="7f8de-150">Ora che si verifichino toocoincide con operazioni hello contenuti in un insieme di credenziali chiave, ma a questo punto sono classi indipendenti (in modo che non implementano IKey hello chiave e il segreto recuperato da hello chiave dell'insieme di credenziali Client).</span><span class="sxs-lookup"><span data-stu-id="7f8de-150">Now they happen toocoincide with hello things that are contained in a Key Vault, but at this point they are independent classes (so hello Key and Secret retrieved by hello Key Vault Client do not implement IKey).</span></span>
> 
> 

## <a name="encrypt-blob-and-upload"></a><span data-ttu-id="7f8de-151">Crittografare un BLOB ed eseguire il caricamento</span><span class="sxs-lookup"><span data-stu-id="7f8de-151">Encrypt blob and upload</span></span>
<span data-ttu-id="7f8de-152">Aggiungere seguente hello tooencrypt un blob del codice e caricarlo tooyour account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="7f8de-152">Add hello following code tooencrypt a blob and upload it tooyour Azure storage account.</span></span> <span data-ttu-id="7f8de-153">Hello **ResolveKeyAsync** metodo che viene utilizzato un IKey viene restituito.</span><span class="sxs-lookup"><span data-stu-id="7f8de-153">hello **ResolveKeyAsync** method that is used returns an IKey.</span></span>

```csharp
// Retrieve hello key that you created previously.
// hello IKey that is returned here is an RsaKey.
// Remember that we used hello names contosokeyvault and testrsakey1.
var rsa = cloudResolver.ResolveKeyAsync("https://contosokeyvault.vault.azure.net/keys/TestRSAKey1", CancellationToken.None).GetAwaiter().GetResult();

// Now you simply use hello RSA key tooencrypt by setting it in hello BlobEncryptionPolicy.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(rsa, null);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

// Reference a block blob.
CloudBlockBlob blob = contain.GetBlockBlobReference("MyFile.txt");

// Upload using hello UploadFromStream method.
using (var stream = System.IO.File.OpenRead(@"C:\data\MyFile.txt"))
    blob.UploadFromStream(stream, stream.Length, null, options, null);
```

<span data-ttu-id="7f8de-154">Di seguito è riportata una schermata da hello [portale di Azure classico](https://manage.windowsazure.com) per un blob che è stato crittografato con la crittografia lato client con una chiave archiviata nell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="7f8de-154">Following is a screenshot from hello [Azure Classic Portal](https://manage.windowsazure.com) for a blob that has been encrypted by using client-side encryption with a key stored in Key Vault.</span></span> <span data-ttu-id="7f8de-155">Hello **KeyId** proprietà è hello URI per la chiave di hello nell'insieme di credenziali chiave che funge da hello KEK.</span><span class="sxs-lookup"><span data-stu-id="7f8de-155">hello **KeyId** property is hello URI for hello key in Key Vault that acts as hello KEK.</span></span> <span data-ttu-id="7f8de-156">Hello **EncryptedKey** proprietà contiene la versione di crittografato hello di hello CEK.</span><span class="sxs-lookup"><span data-stu-id="7f8de-156">hello **EncryptedKey** property contains hello encrypted version of hello CEK.</span></span>

![Screenshot che mostra i metadati BLOB con i metadati di crittografia](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> <span data-ttu-id="7f8de-158">Se si osserva il costruttore di BlobEncryptionPolicy hello, si noterà che può accettare una chiave e/o un sistema di risoluzione.</span><span class="sxs-lookup"><span data-stu-id="7f8de-158">If you look at hello BlobEncryptionPolicy constructor, you will see that it can accept a key and/or a resolver.</span></span> <span data-ttu-id="7f8de-159">Tenere presente che al momento non è possibile usare un resolver per la crittografia perché non supporta attualmente una chiave predefinita.</span><span class="sxs-lookup"><span data-stu-id="7f8de-159">Be aware that right now you cannot use a resolver for encryption because it does not currently support a default key.</span></span>
> 
> 

## <a name="decrypt-blob-and-download"></a><span data-ttu-id="7f8de-160">Decrittografare un BLOB ed eseguire il download</span><span class="sxs-lookup"><span data-stu-id="7f8de-160">Decrypt blob and download</span></span>
<span data-ttu-id="7f8de-161">La decrittografia è piuttosto semplice quando utilizzando hello Resolver classi ha senso.</span><span class="sxs-lookup"><span data-stu-id="7f8de-161">Decryption is really when using hello Resolver classes make sense.</span></span> <span data-ttu-id="7f8de-162">Hello ID della chiave di hello utilizzata per la crittografia è associata a blob hello nei relativi metadati, pertanto non c'è alcun motivo per si tooretrieve hello chiave e ricordare associazione hello tra chiave e del blob.</span><span class="sxs-lookup"><span data-stu-id="7f8de-162">hello ID of hello key used for encryption is associated with hello blob in its metadata, so there is no reason for you tooretrieve hello key and remember hello association between key and blob.</span></span> <span data-ttu-id="7f8de-163">È sufficiente toomake che tale chiave hello rimane nell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="7f8de-163">You just have toomake sure that hello key remains in Key Vault.</span></span>   

<span data-ttu-id="7f8de-164">chiave privata di Hello del rimane impostato su una chiave RSA nell'insieme di credenziali chiave, pertanto, per la decrittografia toooccur, hello il chiave crittografata dai metadati del blob hello contenente hello CEK viene inviato tooKey insieme di credenziali per la decrittografia.</span><span class="sxs-lookup"><span data-stu-id="7f8de-164">hello private key of an RSA Key remains in Key Vault, so for decryption toooccur, hello Encrypted Key from hello blob metadata that contains hello CEK is sent tooKey Vault for decryption.</span></span>

<span data-ttu-id="7f8de-165">Aggiungere hello seguenti blob hello toodecrypt appena caricato.</span><span class="sxs-lookup"><span data-stu-id="7f8de-165">Add hello following toodecrypt hello blob that you just uploaded.</span></span>

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> <span data-ttu-id="7f8de-166">Esistono un paio di altri tipi di gestione delle chiavi toomake resolver più semplice, tra cui: AggregateKeyResolver e CachingKeyResolver.</span><span class="sxs-lookup"><span data-stu-id="7f8de-166">There are a couple of other kinds of resolvers toomake key management easier, including: AggregateKeyResolver and CachingKeyResolver.</span></span>
> 
> 

## <a name="use-key-vault-secrets"></a><span data-ttu-id="7f8de-167">Uso dei segreti dell'insieme di credenziali delle chiavi</span><span class="sxs-lookup"><span data-stu-id="7f8de-167">Use Key Vault secrets</span></span>
<span data-ttu-id="7f8de-168">Hello modo toouse una chiave privata con la crittografia lato client è tramite la classe SymmetricKey hello perché una chiave privata è essenzialmente una chiave simmetrica.</span><span class="sxs-lookup"><span data-stu-id="7f8de-168">hello way toouse a secret with client-side encryption is via hello SymmetricKey class because a secret is essentially a symmetric key.</span></span> <span data-ttu-id="7f8de-169">Tuttavia, come indicato in precedenza, un segreto nell'insieme di credenziali chiave non è mappato esattamente tooa SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="7f8de-169">But, as noted above, a secret in Key Vault does not map exactly tooa SymmetricKey.</span></span> <span data-ttu-id="7f8de-170">Esistono alcuni aspetti toounderstand:</span><span class="sxs-lookup"><span data-stu-id="7f8de-170">There are a few things toounderstand:</span></span>

* <span data-ttu-id="7f8de-171">chiave di Hello in un SymmetricKey ha toobe una lunghezza fissa: 128, 192, 256, 384 e 512 bit.</span><span class="sxs-lookup"><span data-stu-id="7f8de-171">hello key in a SymmetricKey has toobe a fixed length: 128, 192, 256, 384, or 512 bits.</span></span>
* <span data-ttu-id="7f8de-172">chiave di Hello in un SymmetricKey deve essere con codificata Base64.</span><span class="sxs-lookup"><span data-stu-id="7f8de-172">hello key in a SymmetricKey should be Base64 encoded.</span></span>
* <span data-ttu-id="7f8de-173">Un segreto dell'insieme di credenziali chiave che verrà utilizzato come un SymmetricKey deve toohave un tipo di contenuto di "application/octet-stream" nell'insieme di credenziali chiave.</span><span class="sxs-lookup"><span data-stu-id="7f8de-173">A Key Vault secret that will be used as a SymmetricKey needs toohave a Content Type of "application/octet-stream" in Key Vault.</span></span>

<span data-ttu-id="7f8de-174">Di seguito è riportato un esempio di PowerShell per la creazione di un segreto nell'insieme di credenziali delle chiavi che può essere usato come SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="7f8de-174">Here is an example in PowerShell of creating a secret in Key Vault that can be used as a SymmetricKey.</span></span>
<span data-ttu-id="7f8de-175">Si noti che il valore di hello rigido codificato, $key, a solo scopo dimostrativo.</span><span class="sxs-lookup"><span data-stu-id="7f8de-175">Please note that hello hard coded value, $key, is for demonstration purpose only.</span></span> <span data-ttu-id="7f8de-176">Nel codice si toogenerate questa chiave.</span><span class="sxs-lookup"><span data-stu-id="7f8de-176">In your own code you'll want toogenerate this key.</span></span>

```csharp
// Here we are making a 128-bit key so we have 16 characters.
//     hello characters are in hello ASCII range of UTF8 so they are
//    each 1 byte. 16 x 8 = 128.
$key = "qwertyuiopasdfgh"
$b = [System.Text.Encoding]::UTF8.GetBytes($key)
$enc = [System.Convert]::ToBase64String($b)
$secretvalue = ConvertTo-SecureString $enc -AsPlainText -Force

// Substitute hello VaultName and Name in this command.
$secret = Set-AzureKeyVaultSecret -VaultName 'ContoseKeyVault' -Name 'TestSecret2' -SecretValue $secretvalue -ContentType "application/octet-stream"
```

<span data-ttu-id="7f8de-177">Nell'applicazione console, è possibile utilizzare hello stesso come prima di chiamare tooretrieve questo segreto come un SymmetricKey.</span><span class="sxs-lookup"><span data-stu-id="7f8de-177">In your console application, you can use hello same call as before tooretrieve this secret as a SymmetricKey.</span></span>

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
<span data-ttu-id="7f8de-178">È tutto.</span><span class="sxs-lookup"><span data-stu-id="7f8de-178">That's it.</span></span> <span data-ttu-id="7f8de-179">Buon lavoro.</span><span class="sxs-lookup"><span data-stu-id="7f8de-179">Enjoy!</span></span>

## <a name="next-steps"></a><span data-ttu-id="7f8de-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7f8de-180">Next steps</span></span>
<span data-ttu-id="7f8de-181">Per altre informazioni sull'uso di Archiviazione di Microsoft Azure con C#, vedere [Libreria client di archiviazione di Microsoft Azure per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f8de-181">For more information about using Microsoft Azure Storage with C#, see [Microsoft Azure Storage Client Library for .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).</span></span>

<span data-ttu-id="7f8de-182">Per ulteriori informazioni su hello API REST di Blob, vedere [API REST del servizio Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span><span class="sxs-lookup"><span data-stu-id="7f8de-182">For more information about hello Blob REST API, see [Blob Service REST API](https://msdn.microsoft.com/library/azure/dd135733.aspx).</span></span>

<span data-ttu-id="7f8de-183">Per informazioni più recenti di hello in archiviazione di Microsoft Azure, visitare toohello [blog del Team di archiviazione di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).</span><span class="sxs-lookup"><span data-stu-id="7f8de-183">For hello latest information on Microsoft Azure Storage, go toohello [Microsoft Azure Storage Team Blog](http://blogs.msdn.com/b/windowsazurestorage/).</span></span>
