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
# <a name="shared-access-signatures-part-2-create-and-use-a-sas-with-blob-storage"></a>Firme di accesso condiviso, parte 2: creare e usare una firma di accesso condiviso con l'archiviazione BLOB

[parte 1](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json) di questa esercitazione è stata fornita una descrizione dettagliata delle firme di accesso condiviso e sono state illustrate le procedure consigliate per utilizzarle. Parte 2 viene mostrato come toogenerate, quindi utilizzare l'accesso condiviso firme con archiviazione Blob. esempi di Hello vengono scritti in c# e usano hello Azure Storage Client Library per .NET. esempi di Hello in questa esercitazione:

* Generare una firma di accesso condiviso per un contenitore
* Generare una firma di accesso condiviso per un BLOB
* Creare un accesso archiviati firme toomanage criteri sulle risorse di un contenitore
* Verificare le firme di accesso condiviso hello in un'applicazione client

## <a name="about-this-tutorial"></a>Informazioni sull'esercitazione
In questa esercitazione vengono create due applicazioni console che illustrano la creazione e l'uso delle firme di accesso condiviso per contenitori e BLOB:

**Applicazione 1**: hello applicazione di gestione. Genera una firma di accesso condiviso per un contenitore e un BLOB. Include una chiave di accesso di account di archiviazione hello nel codice sorgente.

**Applicazione 2**: hello applicazione client. Accede alle risorse blob e contenitore utilizza le firme di accesso condiviso hello create con un'applicazione hello prima. Contenitore firme di accesso condiviso di utilizza solo hello tooaccess e delle risorse blob - caso *non* includono una chiave di accesso di account di archiviazione hello.

## <a name="part-1-create-a-console-application-toogenerate-shared-access-signatures"></a>Parte 1: Creare un accesso condiviso toogenerate all'applicazione console firme
In primo luogo, verificare di aver hello Azure Storage Client Library per .NET sia installato. È possibile installare hello [pacchetto NuGet](http://nuget.org/packages/WindowsAzure.Storage/ "pacchetto NuGet") contenenti hello assembly aggiornate per la libreria client hello. Si tratta di hello metodo per assicurarsi di disporre di correzioni più recenti hello consigliato. È inoltre possibile scaricare la libreria client di hello come parte di una versione più recente di hello di hello [Azure SDK per .NET](https://azure.microsoft.com/downloads/).

In Visual Studio creare una nuova applicazione console Windows e assegnare ad essa il nome **GenerateSharedAccessSignatures**. Aggiungere riferimenti troppo[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [Windowsazure](https://www.nuget.org/packages/WindowsAzure.Storage/) utilizzando uno degli approcci seguenti hello:

* Hello utilizzare [Gestione pacchetti NuGet](https://docs.nuget.org/consume/installing-nuget) in Visual Studio. Selezionare **Progetto** > **Gestisci pacchetti NuGet**, eseguire la ricerca online per ogni pacchetto (Microsoft.WindowsAzure.ConfigurationManager e WindowsAzure.Storage) e installarli.
* In alternativa, individuare gli assembly nell'installazione di hello Azure SDK e aggiungere riferimenti toothem:
  * Microsoft.WindowsAzure.Configuration.dll
  * Microsoft.WindowsAzure.Storage.dll

Nella parte superiore di hello del file Program.cs hello, aggiungere hello **utilizzando** direttive:

```csharp
using System.IO;
using Microsoft.Azure;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Modificare il file app. config hello in modo che contenga un'impostazione di configurazione con una stringa di connessione che punta tooyour account di archiviazione. File app. config dovrebbe essere simile toothis uno:

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

### <a name="generate-a-shared-access-signature-uri-for-a-container"></a>Generare l'URI di una firma di accesso condiviso per un contenitore
toobegin con, aggiungiamo un toogenerate metodo una firma di accesso condiviso in un nuovo contenitore. In questo caso, la firma hello non è associata a un criterio di accesso archiviati, in modo che esercita hello informazioni hello URI che indica le autorizzazioni di hello e l'ora di scadenza concede.

Innanzitutto, aggiungere codice toohello **Main ()** tooauthenticate metodo accedere tooyour account di archiviazione e creare un nuovo contenitore:

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

Successivamente, aggiungere un metodo che genera l'errore di firma di accesso condiviso hello contenitore hello e restituisce l'URI di firma hello:

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

Aggiungere hello seguendo le linee nella parte inferiore di hello di hello **Main ()** (metodo), prima di chiamare troppo di hello**Console.ReadLine()**, toocall **GetContainerSasUri()** e scrivere hello finestra di console toohello URI di firma:

```csharp
//Generate a SAS URI for hello container, without a stored access policy.
Console.WriteLine("Container SAS URI: " + GetContainerSasUri(container));
Console.WriteLine();
```

Compilare ed eseguire toooutput firma di accesso condiviso hello URI per il nuovo contenitore di hello. Hello URI sarà simile toohello seguenti:

```
https://storageaccount.blob.core.windows.net/sascontainer?sv=2012-02-12&se=2013-04-13T00%3A12%3A08Z&sr=c&sp=wl&sig=t%2BbzU9%2B7ry4okULN9S0wst%2F8MCUhTjrHyV9rDNLSe8g%3D
```

Dopo aver eseguito codice hello, firma di accesso condiviso hello creato per il contenitore di hello sarà valido per hello 24 ore successive. firma Hello concede a un client BLOB toolist autorizzazione in un contenitore hello e toowrite nuovo contenitore toohello di BLOB.

### <a name="generate-a-shared-access-signature-uri-for-a-blob"></a>Generare l'URI di una firma di accesso condiviso per un BLOB
È quindi scrivere toocreate codice simile di un nuovo blob all'interno del contenitore di hello e generare una firma di accesso condiviso per tale. Questa firma di accesso condiviso non è associata a un criterio di accesso archiviati, in modo da includere l'ora di inizio hello, ora di scadenza e le informazioni sulle autorizzazioni in hello URI.

Aggiungere un nuovo metodo che crea un nuovo blob e scrive alcuni tooit di testo, quindi genera una firma di accesso condiviso e restituisce l'URI di firma hello:

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

Nella parte inferiore di hello di hello **Main ()** metodo, aggiungere hello seguenti righe toocall **GetBlobSasUri()**, prima di chiamare troppo di hello**Console.ReadLine()**e scrivere hello condiviso finestra console toohello URI firma di accesso:

```csharp
//Generate a SAS URI for a blob within hello container, without a stored access policy.
Console.WriteLine("Blob SAS URI: " + GetBlobSasUri(container));
Console.WriteLine();
```

Compilare ed eseguire toooutput hello firma di accesso condiviso URI blob nuovo hello. Hello URI sarà simile toohello seguenti:

```
https://storageaccount.blob.core.windows.net/sascontainer/sasblob.txt?sv=2012-02-12&st=2013-04-12T23%3A37%3A08Z&se=2013-04-13T00%3A12%3A08Z&sr=b&sp=rw&sig=dF2064yHtc8RusQLvkQFPItYdeOz3zR8zHsDMBi4S30%3D
```

### <a name="create-a-stored-access-policy-on-hello-container"></a>Creare un criterio di accesso archiviati nel contenitore di hello
A questo punto creare criteri di accesso archiviati nel contenitore di hello, che verrà definiti i vincoli di hello per le firme di accesso condiviso sono associati.

Negli esempi precedenti hello, è specificato l'ora di inizio hello (implicito o esplicito), l'ora di scadenza hello e autorizzazioni hello hello condiviso URI stessa firma di accesso. In hello seguono esempi, si specifica questi criteri di accesso archiviato hello e non la firma di accesso condiviso hello. Questa impostazione consente a questi vincoli senza riemettere hello condiviso toochange accedere firma.

È possibile toohave uno o più vincoli hello sulla firma di accesso condiviso hello e resto hello ai criteri di accesso archiviato hello. Tuttavia, è possibile specificare solo ora di inizio hello, ora di scadenza e le autorizzazioni in una posizione o hello altri. È ad esempio, non è possibile specificare autorizzazioni per la firma di accesso condiviso hello e specificarli anche ai criteri di accesso archiviato hello.

Quando si aggiunge un contenitore di tooa criteri di accesso archiviati, è necessario ottenere le autorizzazioni esistenti del contenitore di hello, aggiungere il nuovo criterio di accesso hello e quindi impostare le autorizzazioni del contenitore hello.

Aggiungere un nuovo metodo che crea un nuovo criterio di accesso archiviati in un contenitore e restituisce il nome di hello del criterio di hello:

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

Nella parte inferiore di hello di hello **Main ()** (metodo), prima di chiamare troppo di hello**Console.ReadLine()**, aggiungere hello seguendo le linee toofirst deselezionare eventuali criteri di accesso esistente e quindi chiamare hello  **CreateSharedAccessPolicy()** metodo:

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

Quando si cancella i criteri di accesso hello in un contenitore, è innanzitutto necessario ottenere le autorizzazioni esistenti del contenitore hello quindi autorizzazioni crittografato hello, quindi impostare le autorizzazioni di hello nuovamente.

### <a name="generate-a-shared-access-signature-uri-on-hello-container-that-uses-an-access-policy"></a>Generare una firma di accesso condiviso URI nel contenitore hello che utilizza un criterio di accesso
Successivamente, abbiamo creato un'altra firma di accesso condiviso per il contenitore hello creati in precedenza, ma questa volta Associamo firma hello con i criteri di accesso archiviato hello creata nell'esempio precedente hello.

Aggiungere un nuovo toogenerate metodo un'altra firma di accesso condiviso per il contenitore di hello:

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

Nella parte inferiore di hello di hello **Main ()** (metodo), prima di chiamare troppo di hello**Console.ReadLine()**, aggiungere hello seguente hello toocall righe **GetContainerSasUriWithPolicy** (metodo) :

```csharp
//Generate a SAS URI for hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Container SAS URI using stored access policy: " + GetContainerSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

### <a name="generate-a-shared-access-signature-uri-on-hello-blob-that-uses-an-access-policy"></a>Generare un URI firma di accesso condiviso in hello Blob che utilizza un criterio di accesso
Infine, aggiungiamo un simile toocreate metodo un altro blob e generare una firma di accesso condiviso associata a un criterio di accesso archiviati.

Aggiungere un nuovo toocreate metodo un blob e generare una firma di accesso condiviso:

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

Nella parte inferiore di hello di hello **Main ()** (metodo), prima di chiamare troppo di hello**Console.ReadLine()**, aggiungere hello seguente hello toocall righe **GetBlobSasUriWithPolicy** metodo:

```csharp
//Generate a SAS URI for a blob within hello container, using a stored access policy tooset constraints on hello SAS.
Console.WriteLine("Blob SAS URI using stored access policy: " + GetBlobSasUriWithPolicy(container, sharedAccessPolicyName));
Console.WriteLine();
```

Hello **Main ()** metodo dovrebbe essere simile al seguente nella sua interezza. Eseguire firma di accesso condiviso hello toowrite finestra della console toohello URI, quindi copiare e incollarli in un file di testo per l'utilizzo nella seconda parte di hello di questa esercitazione.

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

Quando si esegue un'applicazione console GenerateSharedAccessSignatures hello, verrà visualizzato il seguente toohello simili di output. Queste sono le firme di accesso condiviso hello che è utilizzare nella parte 2 dell'esercitazione hello.

```
Container SAS URI: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=pFlEZD%2F6sJTNLxD%2FQ26Hh85j%2FzYPxZav6mP1KJwnvJE%3D&se=2017-05-16T16%3A16%3A47Z&sp=wl

Blob SAS URI: https://storagesample.blob.core.windows.net/sascontainer/sasblob.txt?sv=2016-05-31&sr=b&sig=%2FiBWAZbXESzCMvRcm7JwJBK0gT0BtPSWEq4pRwmlBRI%3D&st=2017-05-15T16%3A11%3A48Z&se=2017-05-16T16%3A16%3A48Z&sp=rw

Container SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&si=tutorialpolicy&sig=aMb6rKDvvpfiGVsZI2rCmyUra6ZPpq%2BZ%2FLyTgAeec%2Bk%3D

Blob SAS URI using stored access policy: https://storagesample.blob.core.windows.net/sascontainer/sasblobpolicy.txt?sv=2016-05-31&sr=b&si=tutorialpolicy&sig=%2FkTWkT23SS45%2FoF4bK2mqXkN%2BPKs%2FyHuzkfQ4GFoZVU%3D
```

## <a name="part-2-create-a-console-application-tootest-hello-shared-access-signatures"></a>Parte 2: Creare un accesso da console applicazione tootest hello condiviso firme
hello tootest condivisi firme di accesso create negli esempi precedenti hello, viene creata una seconda applicazione console che utilizza le operazioni di hello firme tooperform nel contenitore hello e su un blob.

> [!NOTE]
> Se più di 24 ore sono stati superati poiché è completato hello prima parte dell'esercitazione hello, firme di hello generato non saranno valide. In questo caso, eseguire il codice hello in toogenerate applicazione console prima di hello firme di accesso condiviso aggiornata per l'utilizzo nella seconda parte di hello dell'esercitazione hello.
>

In Visual Studio creare una nuova applicazione console Windows e assegnare ad essa il nome **ConsumeSharedAccessSignatures**. Aggiungere riferimenti troppo[Microsoft.WindowsAzure.ConfigurationManager](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager) e [Windowsazure](https://www.nuget.org/packages/WindowsAzure.Storage/), come in precedenza.

Nella parte superiore di hello del file Program.cs hello, aggiungere hello **utilizzando** direttive:

```csharp
using System.IO;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

Nel corpo di hello di hello **Main ()** (metodo), aggiungere hello seguendo le costanti di stringa, la modifica è stato generato nella parte 1 dell'esercitazione hello le firme di accesso toohello condiviso i relativi valori.

```csharp
static void Main(string[] args)
{
    const string containerSAS = "<your container SAS>";
    const string blobSAS = "<your blob SAS>";
    const string containerSASWithAccessPolicy = "<your container SAS with access policy>";
    const string blobSASWithAccessPolicy = "<your blob SAS with access policy>";
}
```

### <a name="add-a-method-tootry-container-operations-using-a-shared-access-signature"></a>Aggiungere un contenitore della tootry metodo le operazioni utilizzando una firma di accesso condiviso
Successivamente, è aggiungere un metodo che esegue il test utilizzando una firma di accesso condiviso per il contenitore di hello alcune operazioni di contenitore. firma di accesso condiviso Hello è tooreturn usato un contenitore toohello riferimento, l'autenticazione contenitore toohello accesso in base alla firma hello da solo.

Aggiungere hello tooProgram.cs metodo seguente:

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

Hello aggiornamento **Main ()** metodo toocall **UseContainerSAS()** con entrambi hello condiviso firme di accesso creato nel contenitore hello:

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

### <a name="add-a-method-tootry-blob-operations-using-a-shared-access-signature"></a>Aggiungere operazioni di blob tootry un metodo utilizzando una firma di accesso condiviso
Infine, è aggiungere un metodo che esegue il test utilizzando una firma di accesso condiviso nel blob hello alcune operazioni di blob. In questo caso, viene usato il costruttore hello **CloudBlockBlob(String)**, passando nella firma di accesso condiviso hello, tooreturn un blob toohello di riferimento. Nessun altro tipo di autenticazione è obbligatoria. è basato sulla firma hello da solo.

Aggiungere hello tooProgram.cs metodo seguente:

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

Hello aggiornamento **Main ()** metodo toocall **UseBlobSAS()** con entrambi hello condiviso firme di accesso creato nel blob hello:

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

Eseguire un'applicazione console hello e osservare toosee di output di hello quali operazioni sono consentite per le firme. output di Hello nella finestra di console hello avrà un aspetto simile toohello seguenti:

```
Write operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

List operation succeeded for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl

Read operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

Delete operation failed for SAS https://storagesample.blob.core.windows.net/sascontainer?sv=2016-05-31&sr=c&sig=32EaQGuFyDMb3yOAey3wq%2B%2FLwgPQxAgSo7UhzLdyIDU%3D&se=2017-05-16T15%3A41%3A20Z&sp=wl
Additional error information: hello remote server returned an error: (403) Forbidden.

...
```

## <a name="next-steps"></a>Passaggi successivi

* [Firme di accesso condiviso, parte 1: Hello informazioni modello di firma di accesso condiviso](../common/storage-dotnet-shared-access-signature-part-1.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)
* [Gestire BLOB e accesso in lettura anonimo toocontainers](storage-manage-access-to-resources.md)
* [Delega dell'accesso con una firma di accesso condiviso (API REST)](http://msdn.microsoft.com/library/azure/ee395415.aspx)
* [Introduzione alla firma di accesso condiviso per tabelle e code](http://blogs.msdn.com/b/windowsazurestorage/archive/2012/06/12/introducing-table-sas-shared-access-signature-queue-sas-and-update-to-blob-sas.aspx)
