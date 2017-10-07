---
title: aaaHow toouse archiviazione Blob di Azure (archiviazione di oggetti) da Java | Documenti Microsoft
description: Archiviare dati non strutturati nel cloud hello con archiviazione Blob di Azure (archiviazione di oggetti).
services: storage
documentationcenter: java
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 2e223b38-92de-4c2f-9254-346374545d32
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: java
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 6dd6efdf688161c32b9d73a65fa7f3a98f2fad74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-java"></a>Come toouse archiviazione Blob da Java
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a>Panoramica
Archiviazione Blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB. Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione. Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.

In questo articolo verrà illustrato come gli scenari comuni di tooperform utilizzando hello archiviazione Blob di Microsoft Azure. esempi di Hello sono scritti in Java e usano hello [Azure Storage SDK per Java][Azure Storage SDK for Java]. Hello scenari trattati includono **caricamento**, **elenco**, **download**, e **eliminazione** BLOB. Per ulteriori informazioni sui blob, vedere hello [passaggi successivi](#Next-Steps) sezione.

> [!NOTE]
> per gli sviluppatori che usano il servizio di archiviazione di Azure in dispositivi Android, è disponibile un SDK specifico. Per ulteriori informazioni, vedere hello [Azure Storage SDK per Android][Azure Storage SDK for Android].
>
>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a>Creare un'applicazione Java
In questo articolo, si useranno le funzionalità di archiviazione che possono essere eseguite in un'applicazione Java in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in Azure.

toodo in tal caso, sarà necessario tooinstall hello Java Development Kit (JDK) e creare un account di archiviazione di Azure nella sottoscrizione di Azure. Dopo aver eseguito questa operazione, sarà necessario tooverify che il sistema di sviluppo soddisfi i requisiti minimi di hello e le dipendenze sono elencate in hello [Azure Storage SDK per Java] [ Azure Storage SDK for Java] repository in GitHub. Se il sistema soddisfi tali requisiti, è possibile seguire le istruzioni di hello per scaricare e installare le librerie di archiviazione di Azure hello for Java nel sistema da quel repository. Dopo aver completato queste attività, sarà in grado di toocreate un'applicazione Java che utilizza esempi hello in questo articolo.

## <a name="configure-your-application-tooaccess-blob-storage"></a>Configurare l'archiviazione Blob di tooaccess applicazione
Aggiungere hello dopo l'inizio di toohello di istruzioni di importazione del file di Java hello in cui si desidera toouse hello API di archiviazione Azure tooaccess BLOB.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a>Configurare una stringa di connessione di archiviazione di Azure
Un client di archiviazione di Azure Usa un endpoint di toostore stringa di connessione archiviazione e le credenziali per l'accesso a servizi di gestione dati. Quando si esegue un'applicazione client, è necessario fornire una stringa di connessione di archiviazione hello in hello seguente formato, utilizzando nome hello dell'account di archiviazione e chiave di accesso primaria per l'account di archiviazione hello elencati in hello hello [il portale di Azure](https://portal.azure.com)per hello *AccountName* e *AccountKey* valori. Hello esempio seguente viene illustrato come dichiarare una stringa di connessione hello toohold campo statico.

```java
// Define hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

In un'applicazione in esecuzione all'interno di un ruolo in Microsoft Azure, questa stringa può essere archiviata nel file di configurazione del servizio hello *ServiceConfiguration. cscfg*ed è possibile accedervi con una chiamata toohello  **RoleEnvironment.getConfigurationSettings** metodo. esempio Hello Ottiene la stringa di connessione hello da un **impostazione** elemento denominato *StorageConnectionString* nel file di configurazione del servizio hello.

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

Hello negli esempi seguenti si presuppongono che si usa uno di questi due metodi tooget hello stringa di connessione.

## <a name="create-a-container"></a>Creare un contenitore
Gli oggetti **CloudBlobClient** consentono di ottenere oggetti di riferimento per contenitori e BLOB. Hello codice seguente viene creata una **CloudBlobClient** oggetto.

> [!NOTE]
> Esistono altri modi toocreate **CloudStorageAccount** oggetti; per ulteriori informazioni, vedere **CloudStorageAccount** in hello [Azure Storage Client SDK riferimento].
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Hello utilizzare **CloudBlobClient** tooget un contenitore toohello riferimento desiderato toouse dell'oggetto. È possibile creare il contenitore di hello se non esiste con hello **createIfNotExists** (metodo), che in caso contrario restituirà contenitore esistente hello. Per impostazione predefinita, hello nuovo contenitore è privato, è necessario specificare la chiave di accesso di archiviazione (come descritto in precedenza) BLOB toodownload da questo contenitore.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference tooa container.
    // hello container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create hello container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a>Facoltativo: configurare un contenitore per l'accesso pubblico
Le autorizzazioni di un contenitore sono configurate per l'accesso privato per impostazione predefinita, ma è possibile configurare facilmente autorizzazioni tooallow pubbliche di sola lettura e di accesso un contenitore per tutti gli utenti su Internet hello:

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in hello permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set hello permissions on hello container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
tooupload un blob tooa file, ottenere un riferimento a un contenitore e usarlo tooget un riferimento di blob. Dopo aver creato un riferimento di blob, è possibile caricare qualsiasi flusso tramite una chiamata di caricamento sul riferimento blob hello. Se non esiste o sovrascrivere il file in caso affermativo, questa operazione creerà blob hello. Hello nell'esempio di codice seguente viene illustrata questa situazione e si presuppone che il contenitore hello è già stato creato.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define hello path tooa local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite hello "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="list-hello-blobs-in-a-container"></a>Elenco di BLOB hello in un contenitore
come è avvenuto tooupload un blob del BLOB di hello toolist in un contenitore, innanzitutto ottenere un riferimento di contenitore. È possibile utilizzare del contenitore hello **listBlobs** metodo con un **per** ciclo. Hello codice riportato di seguito genera hello Uri di ogni blob in una console toohello contenitore.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within hello container and output hello URI tooeach of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

Notare che è possibile assegnare il nome ai BLOB con le informazioni sul percorso nel nome. Consente di creare una struttura di directory virtuale che è possibile organizzare e attraversare come un file system tradizionale. Si noti che la struttura di directory hello virtuale solo - hello solo le risorse disponibili nell'archiviazione Blob sono contenitori e BLOB. Libreria client hello offre tuttavia un **CloudBlobDirectory** oggetto directory virtuale di toorefer tooa e semplificare il processo di hello dell'utilizzo di BLOB sono organizzati in questo modo.

È ad esempio possibile disporre di un contenitore denominato "photos", in cui sono stati caricati i BLOB denominati "rootphoto1", "2010/photo1", "2010/photo2" e "2011/photo1". Questa modifica produrrebbe hello directory virtuali all'interno del contenitore "foto" hello "2011" e "2010". Quando si chiama **listBlobs** nel contenitore "foto" hello, hello insieme restituito conterrà **CloudBlobDirectory** e **CloudBlob** gli oggetti che rappresentano hello Directory e i BLOB contenuti al livello superiore di hello. In questo caso oltre alle directory "2010" e "2011", verrà restituita anche la foto "rootphoto1". È possibile utilizzare hello **instanceof** operatore toodistinguish questi oggetti.

Facoltativamente, è possibile passare parametri toohello **listBlobs** metodo con hello **useFlatBlobListing** parametro impostato tootrue. In questo modo verranno restituiti tutti i BLOB indipendentemente dalla directory. Per ulteriori informazioni, vedere **cloudblobcontainer. Listblobs** in hello [Azure Storage Client SDK riferimento].

## <a name="download-a-blob"></a>Scaricare un BLOB
BLOB toodownload, seguire hello stessi passaggi per il caricamento di un blob in ordine tooget un riferimento di blob. In hello caricamento di esempio, il caricamento è stato chiamato sull'oggetto blob hello. Nell'esempio seguente di hello, chiamare download tootransfer hello blob contenuto tooa oggetto flusso, ad esempio un **FileOutputStream** che è possibile utilizzare un file locale tooa toopersist hello blob.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in hello container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If hello item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download hello item and save it tooa file with hello same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a>Eliminare un BLOB
toodelete un blob, ottenere un blob di riferimento e chiamare **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference tooa blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete hello blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a>Eliminare un contenitore BLOB
Infine, toodelete un contenitore blob, ottenere un blob di riferimento del contenitore e chiamare **deleteIfExists**.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference tooa previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete hello blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output hello stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso i concetti di base di hello dell'archiviazione Blob, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.

* [Azure Storage SDK per Java][Azure Storage SDK for Java]
* [Azure Storage Client SDK riferimento][Azure Storage Client SDK riferimento]
* [API REST di Archiviazione di Azure][Azure Storage REST API]
* [Blog del team di Archiviazione di Azure][Azure Storage Team Blog]

Per ulteriori informazioni, vedere anche hello [Centro per sviluppatori Java](/develop/java/).

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Azure Storage Client SDK riferimento]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
