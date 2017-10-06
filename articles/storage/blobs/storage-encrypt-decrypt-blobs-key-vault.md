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
# <a name="tutorial-encrypt-and-decrypt-blobs-in-microsoft-azure-storage-using-azure-key-vault"></a>Esercitazione: Crittografare e decrittografare i BLOB in Archiviazione di Microsoft Azure tramite l'insieme di credenziali delle chiavi di Azure
## <a name="introduction"></a>Introduzione
Questa esercitazione sono trattati come toomake utilizzare di crittografia di archiviazione lato client con l'insieme di credenziali chiave di Azure. Illustra come tooencrypt e la decrittografia di un blob in un'applicazione console tramite tali tecnologie.

**Toocomplete tempo stimato:** 20 minuti

Per informazioni generali sull'Insieme di credenziali delle chiavi di Azure, vedere [Cos'è l'Insieme di credenziali delle chiavi di Azure?](../../key-vault/key-vault-whatis.md)

Per informazioni generali sulla crittografia lato client per Archiviazione di Azure, vedere l'articolo relativo alla [crittografia lato client e all'Insieme di credenziali delle chiavi di Azure per Archiviazione di Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json).

## <a name="prerequisites"></a>Prerequisiti
toocomplete questa esercitazione, è necessario disporre di hello seguenti:

* Un account di archiviazione Azure
* Visual Studio 2013 o versioni successive
* Azure PowerShell

## <a name="overview-of-client-side-encryption"></a>Panoramica della crittografia lato client
Per una panoramica sulla crittografia lato client per Archiviazione di Azure, vedere l'articolo relativo alla [crittografia lato client e all'Insieme di credenziali delle chiavi di Azure per Archiviazione di Microsoft Azure](../common/storage-client-side-encryption.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

Ecco una breve descrizione del funzionamento della crittografia lato client:

1. Hello Azure Storage client SDK genera una chiave di crittografia del contenuto (CEK), che è una chiave simmetrica con un utilizzo.
2. I dati del cliente vengono crittografati con questa chiave CEK.
3. Hello CEK viene eseguito il wrapping (crittografata) con chiave di crittografia della chiave hello (CHIAVI). Hello KEK è identificato da un identificatore di chiave e può essere una coppia di chiavi asimmetriche o di una chiave simmetrica e possono essere gestito in locale o memorizzato nell'insieme di credenziali chiave di Azure. client di archiviazione Hello stesso non ha mai accesso toohello KEK. Richiama solo l'algoritmo di wrapping delle chiavi hello fornito dall'insieme di credenziali chiave. I clienti possono scegliere toouse provider personalizzati per la chiave di ritorno a capo/annullamento del wrapping se desiderano.
4. Hello dati crittografati viene quindi caricato toohello servizio di archiviazione di Azure.

## <a name="set-up-your-azure-key-vault"></a>Impostare l'insieme di credenziali delle chiavi di Azure
In ordine tooproceed in questa esercitazione, è necessario hello toodo alla procedura seguente, che sono descritte nell'esercitazione hello [introduzione insieme credenziali chiavi Azure](../../key-vault/key-vault-get-started.md):

* Creare un insieme di credenziali delle chiavi.
* Aggiungere una chiave o un insieme di credenziali chiave segreta toohello.
* Registrare un'applicazione con Azure Active Directory.
* Autorizzare hello applicazione toouse hello chiave o il segreto.

Assicurarsi di annotare hello ClientID e ClientSecret che sono stati generati durante la registrazione di un'applicazione con Azure Active Directory.

Creare entrambe le chiavi nell'insieme di credenziali chiave hello. Per rest hello di esercitazione hello si presuppone che si usa hello seguenti nomi: ContosoKeyVault e TestRSAKey1.

## <a name="create-a-console-application-with-packages-and-appsettings"></a>Creare un'applicazione console con pacchetti e AppSettings
In Visual Studio creare una nuova applicazione console.

Aggiungere pacchetti nuget necessari nella Console di gestione pacchetti hello.

```
Install-Package WindowsAzure.Storage

// This is hello latest stable release for ADAL.
Install-Package Microsoft.IdentityModel.Clients.ActiveDirectory -Version 2.16.204221202

Install-Package Microsoft.Azure.KeyVault
Install-Package Microsoft.Azure.KeyVault.Extensions
```

Aggiungere AppSettings toohello app. config.

```xml
<appSettings>
    <add key="accountName" value="myaccount"/>
    <add key="accountKey" value="theaccountkey"/>
    <add key="clientId" value="theclientid"/>
    <add key="clientSecret" value="theclientsecret"/>
    <add key="container" value="stuff"/>
</appSettings>
```

Aggiungere il seguente hello `using` tooadd che crea un progetto di riferimento tooSystem.Configuration toohello e istruzioni.

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

## <a name="add-a-method-tooget-a-token-tooyour-console-application"></a>Aggiungere un tooget metodo un'applicazione console tooyour token
metodo seguente Hello viene utilizzato dalle classi di insieme di credenziali chiave che è necessario per l'insieme di credenziali chiave di accesso tooyour tooauthenticate.

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

## <a name="access-storage-and-key-vault-in-your-program"></a>Accedere all'archiviazione e all'insieme di credenziali delle chiavi nel programma
Nella funzione Main hello, aggiungere hello seguente codice.

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
> Modelli a oggetti dell'insieme di credenziali chiave
> 
> È importante che esistono effettivamente due oggetti insieme di credenziali chiave toounderstand modelli toobe comunicata: una si basa sull'API REST (spazio dei nomi KeyVault) hello e altri hello è un'estensione per la crittografia lato client.
> 
> Chiave dell'insieme di credenziali Client Hello interagisce con hello API REST e riconosce i segreti hello due tipi di elementi contenuti nell'insieme di credenziali chiave e le chiavi Web JSON.
> 
> le estensioni di insieme di credenziali chiave di Hello sono classi che sembrano create appositamente per la crittografia lato client in archiviazione di Azure. Contengono un'interfaccia per le chiavi (IKey) e le classi basate sul concetto di hello di un Resolver di chiave. Esistono due implementazioni di che è necessario tooknow IKey: RSAKey e SymmetricKey. Ora che si verifichino toocoincide con operazioni hello contenuti in un insieme di credenziali chiave, ma a questo punto sono classi indipendenti (in modo che non implementano IKey hello chiave e il segreto recuperato da hello chiave dell'insieme di credenziali Client).
> 
> 

## <a name="encrypt-blob-and-upload"></a>Crittografare un BLOB ed eseguire il caricamento
Aggiungere seguente hello tooencrypt un blob del codice e caricarlo tooyour account di archiviazione Azure. Hello **ResolveKeyAsync** metodo che viene utilizzato un IKey viene restituito.

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

Di seguito è riportata una schermata da hello [portale di Azure classico](https://manage.windowsazure.com) per un blob che è stato crittografato con la crittografia lato client con una chiave archiviata nell'insieme di credenziali chiave. Hello **KeyId** proprietà è hello URI per la chiave di hello nell'insieme di credenziali chiave che funge da hello KEK. Hello **EncryptedKey** proprietà contiene la versione di crittografato hello di hello CEK.

![Screenshot che mostra i metadati BLOB con i metadati di crittografia](./media/storage-encrypt-decrypt-blobs-key-vault/blobmetadata.png)

> [!NOTE]
> Se si osserva il costruttore di BlobEncryptionPolicy hello, si noterà che può accettare una chiave e/o un sistema di risoluzione. Tenere presente che al momento non è possibile usare un resolver per la crittografia perché non supporta attualmente una chiave predefinita.
> 
> 

## <a name="decrypt-blob-and-download"></a>Decrittografare un BLOB ed eseguire il download
La decrittografia è piuttosto semplice quando utilizzando hello Resolver classi ha senso. Hello ID della chiave di hello utilizzata per la crittografia è associata a blob hello nei relativi metadati, pertanto non c'è alcun motivo per si tooretrieve hello chiave e ricordare associazione hello tra chiave e del blob. È sufficiente toomake che tale chiave hello rimane nell'insieme di credenziali chiave.   

chiave privata di Hello del rimane impostato su una chiave RSA nell'insieme di credenziali chiave, pertanto, per la decrittografia toooccur, hello il chiave crittografata dai metadati del blob hello contenente hello CEK viene inviato tooKey insieme di credenziali per la decrittografia.

Aggiungere hello seguenti blob hello toodecrypt appena caricato.

```csharp
// In this case, we will not pass a key and only pass hello resolver because
// this policy will only be used for downloading / decrypting.
BlobEncryptionPolicy policy = new BlobEncryptionPolicy(null, cloudResolver);
BlobRequestOptions options = new BlobRequestOptions() { EncryptionPolicy = policy };

using (var np = File.Open(@"C:\data\MyFileDecrypted.txt", FileMode.Create))
    blob.DownloadToStream(np, null, options, null);
```

> [!NOTE]
> Esistono un paio di altri tipi di gestione delle chiavi toomake resolver più semplice, tra cui: AggregateKeyResolver e CachingKeyResolver.
> 
> 

## <a name="use-key-vault-secrets"></a>Uso dei segreti dell'insieme di credenziali delle chiavi
Hello modo toouse una chiave privata con la crittografia lato client è tramite la classe SymmetricKey hello perché una chiave privata è essenzialmente una chiave simmetrica. Tuttavia, come indicato in precedenza, un segreto nell'insieme di credenziali chiave non è mappato esattamente tooa SymmetricKey. Esistono alcuni aspetti toounderstand:

* chiave di Hello in un SymmetricKey ha toobe una lunghezza fissa: 128, 192, 256, 384 e 512 bit.
* chiave di Hello in un SymmetricKey deve essere con codificata Base64.
* Un segreto dell'insieme di credenziali chiave che verrà utilizzato come un SymmetricKey deve toohave un tipo di contenuto di "application/octet-stream" nell'insieme di credenziali chiave.

Di seguito è riportato un esempio di PowerShell per la creazione di un segreto nell'insieme di credenziali delle chiavi che può essere usato come SymmetricKey.
Si noti che il valore di hello rigido codificato, $key, a solo scopo dimostrativo. Nel codice si toogenerate questa chiave.

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

Nell'applicazione console, è possibile utilizzare hello stesso come prima di chiamare tooretrieve questo segreto come un SymmetricKey.

```csharp
SymmetricKey sec = (SymmetricKey) cloudResolver.ResolveKeyAsync(
    "https://contosokeyvault.vault.azure.net/secrets/TestSecret2/",
    CancellationToken.None).GetAwaiter().GetResult();
```
È tutto. Buon lavoro.

## <a name="next-steps"></a>Passaggi successivi
Per altre informazioni sull'uso di Archiviazione di Microsoft Azure con C#, vedere [Libreria client di archiviazione di Microsoft Azure per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Per ulteriori informazioni su hello API REST di Blob, vedere [API REST del servizio Blob](https://msdn.microsoft.com/library/azure/dd135733.aspx).

Per informazioni più recenti di hello in archiviazione di Microsoft Azure, visitare toohello [blog del Team di archiviazione di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/).
