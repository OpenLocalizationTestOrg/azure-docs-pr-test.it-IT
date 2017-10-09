---
title: aaaDevelop per l'archiviazione di File di Azure con Java | Documenti Microsoft
description: Informazioni su come applicazioni Java toodevelop e servizi che usano File di Azure storage toostore dati dei file.
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a>Eseguire lo sviluppo per Archiviazione file di Azure con Java
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>Informazioni sull'esercitazione
In questa esercitazione verrà illustrato l'utilizzo di Java toodevelop applicazioni o servizi che utilizzano i File di Azure storage toostore file dati di base di hello. In questa esercitazione verrà creata una semplice applicazione console e Mostra come tooperform azioni di base con l'archiviazione di Java e i File di Azure:

* Creare ed eliminare condivisioni file di Azure
* Creare ed eliminare directory
* Enumerare file e directory in una condivisione file di Azure
* Caricare, scaricare ed eliminare un file

> [!Note]  
> Poiché la memorizzazione dei File di Azure sono accessibili tramite SMB, è possibile toowrite semplici applicazioni che accedono a hello Azure condivisione File che utilizza le classi dei / o Java standard hello. In questo articolo descrive come le applicazioni che usano toowrite hello Java Azure Storage SDK, che usa hello [API REST di archiviazione di File di Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure archiviazione File.

## <a name="create-a-java-application"></a>Creare un'applicazione Java
esempi di hello toobuild, sarà necessario hello Java Development Kit (JDK) e [] [Azure Storage SDK per Java] hello. È inoltre necessario aver creato un account di archiviazione di Azure.

## <a name="setup-your-application-toouse-azure-file-storage"></a>Configurare l'archiviazione di File di Azure di toouse applicazione
hello toouse API di archiviazione di Azure aggiungere hello file Java hello in cui si intende il servizio di archiviazione hello tooaccess dalla cima toohello istruzione seguente.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Configurare una stringa di connessione di archiviazione di Azure
toouse archiviazione di File di Azure, è necessario tooconnect tooyour account di archiviazione Azure. Hello primo passaggio potrebbe essere una stringa di connessione che verrà usato tooconfigure tooconnect tooyour account di archiviazione. È pertanto possibile definire un toodo variabile statica che.

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Sostituire your_storage_account_name e your_storage_account_key con i valori effettivi hello dell'account di archiviazione.
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a>Connessione tooan account di archiviazione di Azure
account di archiviazione tooyour tooconnect, è necessario hello toouse **CloudStorageAccount** oggetto, passando un tooits di stringa di connessione **analizzare** metodo.

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

**CloudStorageAccount.parse** genera un'InvalidKeyException pertanto sarà necessario tooput è all'interno di un blocco try/catch bloccare.

## <a name="create-an-azure-file-share"></a>Creare una condivisione file di Azure
Tutti i file e directory in Archiviazione file di Azure si trovano in un contenitore denominato **Share**. L'account di archiviazione può disporre di tante condivisioni quante sono consentite dalla capacità dell'account. condivisione di tooa tooobtain accesso e il relativo contenuto, è necessario toouse un client di archiviazione di File di Azure.

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

Client di archiviazione Azure File hello è quindi possibile ottenere una condivisione di tooa di riferimento.

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

tooactually creare hello condivisione, utilizzare hello **createIfNotExists** metodo dell'oggetto CloudFileShare hello.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

A questo punto, **condividere** contiene una condivisione di tooa di riferimento denominata **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Eliminare una condivisione file di Azure
Eliminazione di una condivisione di viene eseguita dal chiamante hello **deleteIfExists** metodo su un oggetto CloudFileShare. Ecco il codice di esempio che esegue tale operazione.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a>Creare una directory
È anche possibile organizzare archiviazione inserendo i file all'interno di sottodirectory, anziché tutti gli elementi nella directory radice hello. Archiviazione di File di Azure consente toocreate come consentire più directory come l'account. codice Hello seguente verrà creata una sottodirectory denominata **sampledir** nella directory radice hello.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a>Eliminare una directory
Eliminare una directory è un'attività piuttosto semplice, anche se occorre tenere presente che non è possibile eliminare una directory che contiene ancora file o altre directory.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerare file e directory in una condivisione file di Azure
Ottenere un elenco di file e directory all'interno di una condivisione è facile chiamando **listFilesAndDirectories** in un riferimento CloudFileDirectory. metodo Hello restituisce un elenco di oggetti ListFileItem in cui è possibile eseguire l'iterazione. Ad esempio, hello codice riportato di seguito consente di visualizzare file e directory all'interno della directory radice hello.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Caricare un file
Condivisione contiene in hello molto almeno un File di Azure, una directory radice in cui i file possono trovarsi. In questa sezione si apprenderà come tooupload un file dall'archiviazione locale su hello radice della directory di una condivisione.

Hello caricando un file è innanzitutto tooobtain una directory toohello di riferimento in cui risiede. A tale scopo, chiamata hello **getRootDirectoryReference** metodo dell'oggetto condivisione hello.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Dopo aver creato una directory radice toohello di riferimento della condivisione di hello, è possibile caricare un file nel seguente codice hello.

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Scaricare un file
Uno dei più frequente di operazioni eseguite nel servizio di archiviazione Azure File hello è file toodownload. Nell'esempio seguente di hello, codice hello Scarica samplefile. txt e visualizzarne il contenuto.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a>Eliminare un file
Un'altra operazione comunemente eseguita nell'archiviazione file di Azure è l'eliminazione dei file. il codice seguente Hello Elimina un file denominato samplefile. txt archiviati all'interno di una directory denominata **sampledir**.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a>Passaggi successivi
Se si desidera toolearn ulteriori informazioni sulle altre API di archiviazione Azure, vedere i collegamenti seguenti.

* [Centro per sviluppatori Java](http://azure.microsoft.com/develop/java/)
* [Azure Storage SDK per Java](https://github.com/azure/azure-storage-java)
* [Azure Storage SDK per Android](https://github.com/azure/azure-storage-android)
* [Riferimento all'SDK del client di archiviazione di Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API REST dei servizi di archiviazione di Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Trasferimento dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md)
