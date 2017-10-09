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
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="3755a-103">Eseguire lo sviluppo per Archiviazione file di Azure con Java</span><span class="sxs-lookup"><span data-stu-id="3755a-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="3755a-104">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="3755a-104">About this tutorial</span></span>
<span data-ttu-id="3755a-105">In questa esercitazione verrà illustrato l'utilizzo di Java toodevelop applicazioni o servizi che utilizzano i File di Azure storage toostore file dati di base di hello.</span><span class="sxs-lookup"><span data-stu-id="3755a-105">This tutorial will demonstrate hello basics of using Java toodevelop applications or services that use Azure File storage toostore file data.</span></span> <span data-ttu-id="3755a-106">In questa esercitazione verrà creata una semplice applicazione console e Mostra come tooperform azioni di base con l'archiviazione di Java e i File di Azure:</span><span class="sxs-lookup"><span data-stu-id="3755a-106">In this tutorial, we will create a simple console application and show how tooperform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="3755a-107">Creare ed eliminare condivisioni file di Azure</span><span class="sxs-lookup"><span data-stu-id="3755a-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="3755a-108">Creare ed eliminare directory</span><span class="sxs-lookup"><span data-stu-id="3755a-108">Create and delete directories</span></span>
* <span data-ttu-id="3755a-109">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="3755a-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="3755a-110">Caricare, scaricare ed eliminare un file</span><span class="sxs-lookup"><span data-stu-id="3755a-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="3755a-111">Poiché la memorizzazione dei File di Azure sono accessibili tramite SMB, è possibile toowrite semplici applicazioni che accedono a hello Azure condivisione File che utilizza le classi dei / o Java standard hello.</span><span class="sxs-lookup"><span data-stu-id="3755a-111">Because Azure File storage may be accessed over SMB, it is possible toowrite simple applications that access hello Azure File share using hello standard Java I/O classes.</span></span> <span data-ttu-id="3755a-112">In questo articolo descrive come le applicazioni che usano toowrite hello Java Azure Storage SDK, che usa hello [API REST di archiviazione di File di Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure archiviazione File.</span><span class="sxs-lookup"><span data-stu-id="3755a-112">This article will describe how toowrite applications that use hello Azure Storage Java SDK, which uses hello [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="3755a-113">Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="3755a-113">Create a Java application</span></span>
<span data-ttu-id="3755a-114">esempi di hello toobuild, sarà necessario hello Java Development Kit (JDK) e [] [Azure Storage SDK per Java] hello.</span><span class="sxs-lookup"><span data-stu-id="3755a-114">toobuild hello samples, you will need hello Java Development Kit (JDK) and hello [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="3755a-115">È inoltre necessario aver creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="3755a-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-toouse-azure-file-storage"></a><span data-ttu-id="3755a-116">Configurare l'archiviazione di File di Azure di toouse applicazione</span><span class="sxs-lookup"><span data-stu-id="3755a-116">Setup your application toouse Azure File storage</span></span>
<span data-ttu-id="3755a-117">hello toouse API di archiviazione di Azure aggiungere hello file Java hello in cui si intende il servizio di archiviazione hello tooaccess dalla cima toohello istruzione seguente.</span><span class="sxs-lookup"><span data-stu-id="3755a-117">toouse hello Azure storage APIs, add hello following statement toohello top of hello Java file where you intend tooaccess hello storage service from.</span></span>

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="3755a-118">Configurare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3755a-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="3755a-119">toouse archiviazione di File di Azure, è necessario tooconnect tooyour account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="3755a-119">toouse Azure File storage, you need tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="3755a-120">Hello primo passaggio potrebbe essere una stringa di connessione che verrà usato tooconfigure tooconnect tooyour account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3755a-120">hello first step would be tooconfigure a connection string which we'll use tooconnect tooyour storage account.</span></span> <span data-ttu-id="3755a-121">È pertanto possibile definire un toodo variabile statica che.</span><span class="sxs-lookup"><span data-stu-id="3755a-121">Let's define a static variable toodo that.</span></span>

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="3755a-122">Sostituire your_storage_account_name e your_storage_account_key con i valori effettivi hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="3755a-122">Replace your_storage_account_name and your_storage_account_key with hello actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a><span data-ttu-id="3755a-123">Connessione tooan account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3755a-123">Connecting tooan Azure storage account</span></span>
<span data-ttu-id="3755a-124">account di archiviazione tooyour tooconnect, è necessario hello toouse **CloudStorageAccount** oggetto, passando un tooits di stringa di connessione **analizzare** metodo.</span><span class="sxs-lookup"><span data-stu-id="3755a-124">tooconnect tooyour storage account, you need toouse hello **CloudStorageAccount** object, passing a connection string tooits **parse** method.</span></span>

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

<span data-ttu-id="3755a-125">**CloudStorageAccount.parse** genera un'InvalidKeyException pertanto sarà necessario tooput è all'interno di un blocco try/catch bloccare.</span><span class="sxs-lookup"><span data-stu-id="3755a-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need tooput it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="3755a-126">Creare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="3755a-126">Create an Azure File share</span></span>
<span data-ttu-id="3755a-127">Tutti i file e directory in Archiviazione file di Azure si trovano in un contenitore denominato **Share**.</span><span class="sxs-lookup"><span data-stu-id="3755a-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="3755a-128">L'account di archiviazione può disporre di tante condivisioni quante sono consentite dalla capacità dell'account.</span><span class="sxs-lookup"><span data-stu-id="3755a-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="3755a-129">condivisione di tooa tooobtain accesso e il relativo contenuto, è necessario toouse un client di archiviazione di File di Azure.</span><span class="sxs-lookup"><span data-stu-id="3755a-129">tooobtain access tooa share and its contents, you need toouse a Azure File storage client.</span></span>

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="3755a-130">Client di archiviazione Azure File hello è quindi possibile ottenere una condivisione di tooa di riferimento.</span><span class="sxs-lookup"><span data-stu-id="3755a-130">Using hello Azure File storage client, you can then obtain a reference tooa share.</span></span>

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="3755a-131">tooactually creare hello condivisione, utilizzare hello **createIfNotExists** metodo dell'oggetto CloudFileShare hello.</span><span class="sxs-lookup"><span data-stu-id="3755a-131">tooactually create hello share, use hello **createIfNotExists** method of hello CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="3755a-132">A questo punto, **condividere** contiene una condivisione di tooa di riferimento denominata **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="3755a-132">At this point, **share** holds a reference tooa share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="3755a-133">Eliminare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="3755a-133">Delete an Azure File share</span></span>
<span data-ttu-id="3755a-134">Eliminazione di una condivisione di viene eseguita dal chiamante hello **deleteIfExists** metodo su un oggetto CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="3755a-134">Deleting a share is done by calling hello **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="3755a-135">Ecco il codice di esempio che esegue tale operazione.</span><span class="sxs-lookup"><span data-stu-id="3755a-135">Here's sample code that does that.</span></span>

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

## <a name="create-a-directory"></a><span data-ttu-id="3755a-136">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="3755a-136">Create a directory</span></span>
<span data-ttu-id="3755a-137">È anche possibile organizzare archiviazione inserendo i file all'interno di sottodirectory, anziché tutti gli elementi nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="3755a-137">You can also organize storage by putting files inside sub-directories instead of having all of them in hello root directory.</span></span> <span data-ttu-id="3755a-138">Archiviazione di File di Azure consente toocreate come consentire più directory come l'account.</span><span class="sxs-lookup"><span data-stu-id="3755a-138">Azure File storage allows you toocreate as much directories as your account will allow.</span></span> <span data-ttu-id="3755a-139">codice Hello seguente verrà creata una sottodirectory denominata **sampledir** nella directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="3755a-139">hello code below will create a sub-directory named **sampledir** under hello root directory.</span></span>

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

## <a name="delete-a-directory"></a><span data-ttu-id="3755a-140">Eliminare una directory</span><span class="sxs-lookup"><span data-stu-id="3755a-140">Delete a directory</span></span>
<span data-ttu-id="3755a-141">Eliminare una directory è un'attività piuttosto semplice, anche se occorre tenere presente che non è possibile eliminare una directory che contiene ancora file o altre directory.</span><span class="sxs-lookup"><span data-stu-id="3755a-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

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

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="3755a-142">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="3755a-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="3755a-143">Ottenere un elenco di file e directory all'interno di una condivisione è facile chiamando **listFilesAndDirectories** in un riferimento CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="3755a-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="3755a-144">metodo Hello restituisce un elenco di oggetti ListFileItem in cui è possibile eseguire l'iterazione.</span><span class="sxs-lookup"><span data-stu-id="3755a-144">hello method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="3755a-145">Ad esempio, hello codice riportato di seguito consente di visualizzare file e directory all'interno della directory radice hello.</span><span class="sxs-lookup"><span data-stu-id="3755a-145">As an example, hello following code will list files and directories inside hello root directory.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="3755a-146">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="3755a-146">Upload a file</span></span>
<span data-ttu-id="3755a-147">Condivisione contiene in hello molto almeno un File di Azure, una directory radice in cui i file possono trovarsi.</span><span class="sxs-lookup"><span data-stu-id="3755a-147">An Azure File share contains at hello very least, a root directory where files can reside.</span></span> <span data-ttu-id="3755a-148">In questa sezione si apprenderà come tooupload un file dall'archiviazione locale su hello radice della directory di una condivisione.</span><span class="sxs-lookup"><span data-stu-id="3755a-148">In this section, you'll learn how tooupload a file from local storage onto hello root directory of a share.</span></span>

<span data-ttu-id="3755a-149">Hello caricando un file è innanzitutto tooobtain una directory toohello di riferimento in cui risiede.</span><span class="sxs-lookup"><span data-stu-id="3755a-149">hello first step in uploading a file is tooobtain a reference toohello directory where it should reside.</span></span> <span data-ttu-id="3755a-150">A tale scopo, chiamata hello **getRootDirectoryReference** metodo dell'oggetto condivisione hello.</span><span class="sxs-lookup"><span data-stu-id="3755a-150">You do this by calling hello **getRootDirectoryReference** method of hello share object.</span></span>

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="3755a-151">Dopo aver creato una directory radice toohello di riferimento della condivisione di hello, è possibile caricare un file nel seguente codice hello.</span><span class="sxs-lookup"><span data-stu-id="3755a-151">Now that you have a reference toohello root directory of hello share, you can upload a file onto it using hello following code.</span></span>

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="3755a-152">Scaricare un file</span><span class="sxs-lookup"><span data-stu-id="3755a-152">Download a file</span></span>
<span data-ttu-id="3755a-153">Uno dei più frequente di operazioni eseguite nel servizio di archiviazione Azure File hello è file toodownload.</span><span class="sxs-lookup"><span data-stu-id="3755a-153">One of hello more frequent operations you will perform against Azure File storage is toodownload files.</span></span> <span data-ttu-id="3755a-154">Nell'esempio seguente di hello, codice hello Scarica samplefile. txt e visualizzarne il contenuto.</span><span class="sxs-lookup"><span data-stu-id="3755a-154">In hello following example, hello code downloads SampleFile.txt and displays its contents.</span></span>

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

## <a name="delete-a-file"></a><span data-ttu-id="3755a-155">Eliminare un file</span><span class="sxs-lookup"><span data-stu-id="3755a-155">Delete a file</span></span>
<span data-ttu-id="3755a-156">Un'altra operazione comunemente eseguita nell'archiviazione file di Azure è l'eliminazione dei file.</span><span class="sxs-lookup"><span data-stu-id="3755a-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="3755a-157">il codice seguente Hello Elimina un file denominato samplefile. txt archiviati all'interno di una directory denominata **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="3755a-157">hello following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="3755a-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3755a-158">Next steps</span></span>
<span data-ttu-id="3755a-159">Se si desidera toolearn ulteriori informazioni sulle altre API di archiviazione Azure, vedere i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="3755a-159">If you would like toolearn more about other Azure storage APIs, follow these links.</span></span>

* [<span data-ttu-id="3755a-160">Centro per sviluppatori Java</span><span class="sxs-lookup"><span data-stu-id="3755a-160">Java Developer Center</span></span>](http://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="3755a-161">Azure Storage SDK per Java</span><span class="sxs-lookup"><span data-stu-id="3755a-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="3755a-162">Azure Storage SDK per Android</span><span class="sxs-lookup"><span data-stu-id="3755a-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="3755a-163">Riferimento all'SDK del client di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3755a-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="3755a-164">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3755a-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="3755a-165">Blog del team di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="3755a-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="3755a-166">Trasferimento dati con l'utilità della riga di comando di AzCopy hello</span><span class="sxs-lookup"><span data-stu-id="3755a-166">Transfer data with hello AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)
