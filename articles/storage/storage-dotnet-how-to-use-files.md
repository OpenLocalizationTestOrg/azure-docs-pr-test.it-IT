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
# <a name="develop-for-azure-file-storage-with-net"></a>Eseguire lo sviluppo per Archiviazione file di Azure con .NET 
> [!NOTE]
> Questo articolo viene illustrato come toomanage archiviazione di File di Azure con il codice .NET. toolearn più sull'archiviazione di File di Azure, vedere hello [tooAzure introduzione archiviazione File](storage-files-introduction.md).
>

[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

## <a name="about-this-tutorial"></a>Informazioni sull'esercitazione
In questa esercitazione verrà illustrato l'utilizzo toodevelop applicazioni o servizi .NET che utilizzano i File di Azure storage toostore file dati di base di hello. In questa esercitazione verrà creata una semplice applicazione console e Mostra come azioni di base tooperform con archiviazione .NET e i File di Azure:

* Ottenere il contenuto di hello di un file
* Impostare la quota hello (dimensione massima) per la condivisione di file hello.
* Creare una firma di accesso condiviso (chiave di firma di accesso condiviso) per un file che utilizza un criterio di accesso condiviso definito nella condivisione di hello.
* Copiare un file con estensione tooanother hello stesso account di archiviazione.
* Copiare un blob tooa file hello stesso account di archiviazione.
* Usare la metrica di archiviazione di Azure per la risoluzione dei problemi

> [!Note]  
> Poiché la memorizzazione dei File di Azure sono accessibili tramite SMB, è possibile toowrite semplici applicazioni che accedono a condivisione di File di Azure hello utilizzando le classi System.IO hello standard per i/o File. In questo articolo descrive come le applicazioni che usano toowrite hello Azure Storage .NET SDK, che usa hello [API REST di archiviazione di File di Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure archiviazione File. 


## <a name="create-hello-console-application-and-obtain-hello-assembly"></a>Creare un'applicazione console hello e ottenere assembly hello
In Visual Studio creare una nuova applicazione console di Windows. Hello alla procedura seguente viene illustrato come toocreate un'applicazione console in Visual Studio 2017, tuttavia, i passaggi di hello sono simili in altre versioni di Visual Studio.

1. Selezionare **File** > **Nuovo** > **Progetto**
2. Selezionare **Installati** > **Modelli** > **Visual C#** > **Desktop classico di Windows**
3. Selezionare **App console (.NET Framework)**
4. Immettere un nome per l'applicazione in hello **nome:** campo
5. Selezionare **OK**.

Tutti gli esempi di codice in questa esercitazione è possibile aggiungere toohello `Main()` metodo dell'applicazione console `Program.cs` file.

È possibile usare Azure Storage Client Library hello in qualsiasi tipo di applicazione .NET, tra cui un'app web o servizio di cloud di Azure e le applicazioni desktop e mobile. Per semplicità, in questa guida si usa un'applicazione console.

## <a name="use-nuget-tooinstall-hello-required-packages"></a>Utilizzare i pacchetti hello necessario tooinstall NuGet
Sono disponibili due pacchetti, è necessario tooreference in toocomplete il progetto in questa esercitazione:

* [Microsoft Azure Storage Client Library per .NET](https://www.nuget.org/packages/WindowsAzure.Storage/): questo pacchetto fornisce l'accesso programmatico toodata risorse nell'account di archiviazione.
* [Libreria Gestione configurazione di Microsoft Azure per .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/): questo pacchetto fornisce una classe per l'analisi di una stringa di connessione in un file di configurazione, indipendentemente dalla posizione in cui viene eseguita l'applicazione.

È possibile utilizzare NuGet tooobtain entrambi i pacchetti. A tale scopo, seguire questa procedura:

1. Fare clic con il pulsante destro del mouse sul progetto in **Esplora soluzioni** e scegliere **Gestisci pacchetti NuGet**.
2. Cercare online "Windowsazure" e fare clic su **installare** tooinstall hello libreria Client di archiviazione e le relative dipendenze.
3. Cercare online "WindowsAzure.ConfigurationManager" e fare clic su **installare** tooinstall hello Azure Configuration Manager.

## <a name="save-your-storage-account-credentials-toohello-appconfig-file"></a>Salvare il file app. config di toohello le credenziali di account di archiviazione
A questo punto salvare le credenziali nel file app.config del progetto. Modifica file app. config hello in modo che venga visualizzato simile toohello di esempio seguente, sostituendo `myaccount` con il nome di account di archiviazione e `mykey` con la chiave di account di archiviazione.

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
> versione più recente di Hello dell'emulatore di archiviazione Azure hello non supporta l'archiviazione di File di Azure. La stringa di connessione deve essere un Account di archiviazione di Azure in hello cloud toowork con l'archiviazione di File di Azure.

## <a name="add-using-directives"></a>Aggiungere le direttive using
Aprire hello `Program.cs` file da Esplora soluzioni e aggiungere il seguente hello utilizzo di top toohello direttive del file hello.

```csharp
using Microsoft.Azure; // Namespace for Azure Configuration Manager
using Microsoft.WindowsAzure.Storage; // Namespace for Storage Client Library
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Azure Blobs
using Microsoft.WindowsAzure.Storage.File; // Namespace for Azure File storage
```

[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

## <a name="access-hello-file-share-programmatically"></a>Condivisione di file hello accesso a livello di codice
Successivamente, aggiungere hello seguente codice toohello `Main()` stringa di connessione hello tooretrieve metodo (dopo il codice hello illustrato in precedenza). Questo codice ottiene un file di riferimento toohello creato in precedenza e restituisce la finestra di console toohello contenuto.

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

Eseguire l'output di hello toosee applicazione console hello.

## <a name="set-hello-maximum-size-for-a-file-share"></a>Impostare dimensioni massime di hello per una condivisione file
A partire dalla versione 5. x di hello Azure Storage Client Library, è possibile impostare set hello quota (o dimensioni massime) per una condivisione di file, in gigabyte. È inoltre possibile verificare la quantità di dati è attualmente archiviati nella condivisione di hello toosee.

Dalla quota hello impostazione per una condivisione, è possibile limitare hello totale dimensioni hello file archiviati nella condivisione di hello. Se hello dimensioni totali dei file nella condivisione di hello superano quota hello impostato nella condivisione di hello, il client verrà tooincrease Impossibile hello dimensioni dei file esistenti o creare nuovi file, a meno che tali file sono vuoti.

esempio di Hello seguente mostra come toocheck hello utilizzo corrente per una condivisione e la modalità tooset hello quota per la condivisione di hello.

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

### <a name="generate-a-shared-access-signature-for-a-file-or-file-share"></a>Generare la firma di accesso condiviso per un file o una condivisione file
A partire dalla versione 5. x di hello Azure Storage Client Library, è possibile generare una firma di accesso condiviso (SAS) per una condivisione file o per un singolo file. È anche possibile creare un criterio di accesso condiviso per un accesso condiviso toomanage di condivisione file firme. È consigliabile creare un criterio di accesso condiviso, in quanto forniscono un mezzo di revoca hello SAS se questa deve essere compromessa.

Hello di esempio seguente viene creato un criterio di accesso condiviso in una condivisione e quindi utilizza che condividono tooprovide hello i vincoli dei criteri per una firma di accesso condiviso in un file hello.

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

Per altre informazioni sulla creazione e sull'uso di firme di accesso condiviso, vedere [Uso delle firme di accesso condiviso](storage-dotnet-shared-access-signature-part-1.md) e [Creare e usare una firma di accesso condiviso con i BLOB di Azure](storage-dotnet-shared-access-signature-part-2.md).

## <a name="copy-files"></a>Copiare i file
A partire dalla versione 5. x di hello Azure Storage Client Library, è possibile copiare un file con estensione tooanother, un blob tooa file o un file di blob tooa. Nelle sezioni successive di hello, viene illustrato come questi tooperform copiare operazioni a livello di codice.

È inoltre possibile utilizzare AzCopy toocopy un file tooanother o toocopy versa di file o viceversa tooa un blob. Vedere [trasferire i dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md).

> [!NOTE]
> Se si copia un file di blob tooa o un blob tooa file, è necessario utilizzare un oggetto di origine hello accesso condiviso (firma) tooauthenticate, anche se si copia all'interno di hello stesso account di archiviazione.
> 
> 

**Copiare un file con estensione tooanother** hello esempio copia un file con estensione tooanother hello stessa condivisione. Poiché questa operazione di copia copia tra file hello stesso account di archiviazione, è possibile utilizzare una copia di hello tooperform autenticazione chiave condivisa.

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

**Copiare un blob tooa file** hello seguente viene creato un file e copia tooa blob all'interno di hello stesso account di archiviazione. esempio Hello crea una firma di accesso condiviso per il file di origine hello, quale servizio hello utilizza file di origine toohello tooauthenticate accesso durante l'operazione di copia hello.

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

È possibile copiare un file di blob tooa hello allo stesso modo. Se l'oggetto di origine hello è un blob, creare un blob di firma di accesso condiviso tooauthenticate accesso toothat durante l'operazione di copia hello.

## <a name="troubleshooting-azure-file-storage-using-metrics"></a>Risoluzione dei problemi di Archiviazione file di Azure con le metriche
Analisi archiviazione di Azure ora supporta le metriche per Archiviazione file di Azure. Grazie ai dati di metrica, è possibile monitorare le richieste e diagnosticare i problemi.


È possibile abilitare la metrica per l'archiviazione di File di Azure da hello [portale Azure](https://portal.azure.com). È inoltre possibile abilitare le metriche a livello di codice dal chiamante hello operazione Set File Service Properties tramite hello API REST o uno dei relativi analoghi in hello libreria Client di archiviazione.


Hello esempio di codice seguente viene illustrato come toouse hello libreria Client di archiviazione per le metriche tooenable .NET per l'archiviazione di File di Azure.

In primo luogo, aggiungere hello seguenti `using` tooyour direttive `Program.cs` file inoltre toothose aggiunto nel passaggio precedente:

```csharp
using Microsoft.WindowsAzure.Storage.File.Protocol;
using Microsoft.WindowsAzure.Storage.Shared.Protocol;
```

Si noti che, mentre i BLOB di Azure, tabelle di Azure e le code di Azure, utilizzare hello condiviso `ServiceProperties` tipo di hello `Microsoft.WindowsAzure.Storage.Shared.Protocol` dello spazio dei nomi, la memorizzazione dei File di Azure Usa il proprio tipo, hello `FileServiceProperties` tipo di hello `Microsoft.WindowsAzure.Storage.File.Protocol` dello spazio dei nomi. Entrambi gli spazi dei nomi devono fare riferimento dal codice, tuttavia, per hello toocompile di codice seguente.

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

Inoltre, è possibile fare riferimento troppo[archiviazione di File di Azure articolo Troubleshooting](storage-troubleshoot-file-connection-problems.md) per informazioni sulla risoluzione end-to-end.

## <a name="next-steps"></a>Passaggi successivi
Vedere i collegamenti seguenti per ulteriori informazioni sull'archiviazione file di Azure.

### <a name="conceptual-articles-and-videos"></a>Articoli concettuali e video
* [Archiviazione di file in Azure: un file system SMB nel cloud senza problemi per Windows e Linux](https://azure.microsoft.com/documentation/videos/azurecon-2015-azure-files-storage-a-frictionless-cloud-smb-file-system-for-windows-and-linux/)
* [Come toouse archiviazione di File di Azure con Linux](storage-how-to-use-files-linux.md)

### <a name="tooling-support-for-file-storage"></a>Supporto degli strumenti per Archiviazione file
* [Uso di Azure PowerShell con Archiviazione di Azure](storage-powershell-guide-full.md)
* [Come toouse AzCopy con archiviazione di Microsoft Azure](storage-use-azcopy.md)
* [Con l'archiviazione di Azure hello CLI di Azure](storage-azure-cli.md#create-and-manage-file-shares)
* [Risoluzione dei problemi di archiviazione file di Azure](https://docs.microsoft.com/azure/storage/storage-troubleshoot-file-connection-problems)

### <a name="reference"></a>Riferimento
* [Informazioni di riferimento sulla libreria client di archiviazione per .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx)
* [Riferimento API REST del servizio File](http://msdn.microsoft.com/library/azure/dn167006.aspx)

### <a name="blog-posts"></a>Post di BLOG
* [Archiviazione file di Azure è attualmente disponibile a livello generale](https://azure.microsoft.com/blog/azure-file-storage-now-generally-available/)
* [Inside Azure File storage (Analisi di Archiviazione file di Azure)](https://azure.microsoft.com/blog/inside-azure-file-storage/)
* [Introduzione al servizio File di Microsoft Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/12/introducing-microsoft-azure-file-service.aspx)
* [Rendere persistenti le connessioni tooMicrosoft archiviazione di File di Azure](http://blogs.msdn.com/b/windowsazurestorage/archive/2014/05/27/persisting-connections-to-microsoft-azure-files.aspx)
