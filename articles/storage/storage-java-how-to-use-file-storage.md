---
title: Eseguire lo sviluppo per Archiviazione file di Azure con Java | Microsoft Docs
description: Informazioni su come sviluppare applicazioni e servizi Java che usano Archiviazione file di Azure per archiviare i dati dei file.
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
ms.openlocfilehash: 16924599e49990265e07f7a58613756d93c46942
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a><span data-ttu-id="710a3-103">Eseguire lo sviluppo per Archiviazione file di Azure con Java</span><span class="sxs-lookup"><span data-stu-id="710a3-103">Develop for Azure File storage with Java</span></span>
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a><span data-ttu-id="710a3-104">Informazioni sull'esercitazione</span><span class="sxs-lookup"><span data-stu-id="710a3-104">About this tutorial</span></span>
<span data-ttu-id="710a3-105">Questa esercitazione illustra le nozioni di base per l'uso di Java per sviluppare applicazioni o servizi che usano Archiviazione file di Azure per archiviare i dati dei file.</span><span class="sxs-lookup"><span data-stu-id="710a3-105">This tutorial will demonstrate the basics of using Java to develop applications or services that use Azure File storage to store file data.</span></span> <span data-ttu-id="710a3-106">In questa esercitazione verrà creata una semplice applicazione console e verrà mostrato come eseguire le azioni di base con Java e Archiviazione file di Azure:</span><span class="sxs-lookup"><span data-stu-id="710a3-106">In this tutorial, we will create a simple console application and show how to perform basic actions with Java and Azure File storage:</span></span>

* <span data-ttu-id="710a3-107">Creare ed eliminare condivisioni file di Azure</span><span class="sxs-lookup"><span data-stu-id="710a3-107">Create and delete Azure File shares</span></span>
* <span data-ttu-id="710a3-108">Creare ed eliminare directory</span><span class="sxs-lookup"><span data-stu-id="710a3-108">Create and delete directories</span></span>
* <span data-ttu-id="710a3-109">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="710a3-109">Enumerate files and directories in an Azure File share</span></span>
* <span data-ttu-id="710a3-110">Caricare, scaricare ed eliminare un file</span><span class="sxs-lookup"><span data-stu-id="710a3-110">Upload, download, and delete a file</span></span>

> [!Note]  
> <span data-ttu-id="710a3-111">Poiché Archiviazione file di Azure è accessibile tramite SMB, è possibile scrivere semplici applicazioni che accedono alla condivisione file di Azure usando le classi standard I/O di Java.</span><span class="sxs-lookup"><span data-stu-id="710a3-111">Because Azure File storage may be accessed over SMB, it is possible to write simple applications that access the Azure File share using the standard Java I/O classes.</span></span> <span data-ttu-id="710a3-112">Questo articolo descrive come scrivere applicazioni che usano Azure Storage Java SDK, che usa l'[API REST di archiviazione file Azure](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) per comunicare con Archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="710a3-112">This article will describe how to write applications that use the Azure Storage Java SDK, which uses the [Azure File storage REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) to talk to Azure File storage.</span></span>

## <a name="create-a-java-application"></a><span data-ttu-id="710a3-113">Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="710a3-113">Create a Java application</span></span>
<span data-ttu-id="710a3-114">Per compilare gli esempi, saranno necessari il Java Development Kit (JDK) e [Azure Storage SDK per Java][].</span><span class="sxs-lookup"><span data-stu-id="710a3-114">To build the samples, you will need the Java Development Kit (JDK) and the [Azure Storage SDK for Java][].</span></span> <span data-ttu-id="710a3-115">È inoltre necessario aver creato un account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="710a3-115">You should also have created an Azure storage account.</span></span>

## <a name="setup-your-application-to-use-azure-file-storage"></a><span data-ttu-id="710a3-116">Configurare l'applicazione per usare Archiviazione file di Azure</span><span class="sxs-lookup"><span data-stu-id="710a3-116">Setup your application to use Azure File storage</span></span>
<span data-ttu-id="710a3-117">Per utilizzare le API di archiviazione di Azure, aggiungere le seguenti istruzioni all'inizio del file Java da cui si desidera accedere al servizio di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="710a3-117">To use the Azure storage APIs, add the following statement to the top of the Java file where you intend to access the storage service from.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a><span data-ttu-id="710a3-118">Configurare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="710a3-118">Setup an Azure storage connection string</span></span>
<span data-ttu-id="710a3-119">Per usare Archiviazione file di Azure, è necessario connettersi all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="710a3-119">To use Azure File storage, you need to connect to your Azure storage account.</span></span> <span data-ttu-id="710a3-120">Il primo passaggio consisterà nel configurare una stringa di connessione che verrà utilizzata per connettersi all'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="710a3-120">The first step would be to configure a connection string which we'll use to connect to your storage account.</span></span> <span data-ttu-id="710a3-121">È importante definire una variabile statica a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="710a3-121">Let's define a static variable to do that.</span></span>

```java
// Configure the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> <span data-ttu-id="710a3-122">Sostituire your_storage_account_name e your_storage_account_key con i valori effettivi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="710a3-122">Replace your_storage_account_name and your_storage_account_key with the actual values for your storage account.</span></span>
> 
> 

## <a name="connecting-to-an-azure-storage-account"></a><span data-ttu-id="710a3-123">Connessione a un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="710a3-123">Connecting to an Azure storage account</span></span>
<span data-ttu-id="710a3-124">Per connettersi all'account di archiviazione, è necessario usare l'oggetto **CloudStorageAccount**, passando una stringa di connessione al relativo metodo **parse**.</span><span class="sxs-lookup"><span data-stu-id="710a3-124">To connect to your storage account, you need to use the **CloudStorageAccount** object, passing a connection string to its **parse** method.</span></span>

```java
// Use the CloudStorageAccount object to connect to your storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle the exception
}
```

<span data-ttu-id="710a3-125">**CloudStorageAccount.parse** genera un'eccezione InvalidKeyException, sarà quindi necessario inserirlo in un blocco Try-Catch.</span><span class="sxs-lookup"><span data-stu-id="710a3-125">**CloudStorageAccount.parse** throws an InvalidKeyException so you'll need to put it inside a try/catch block.</span></span>

## <a name="create-an-azure-file-share"></a><span data-ttu-id="710a3-126">Creare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="710a3-126">Create an Azure File share</span></span>
<span data-ttu-id="710a3-127">Tutti i file e directory in Archiviazione file di Azure si trovano in un contenitore denominato **Share**.</span><span class="sxs-lookup"><span data-stu-id="710a3-127">All files and directories in Azure File storage reside in a container called a **Share**.</span></span> <span data-ttu-id="710a3-128">L'account di archiviazione può disporre di tante condivisioni quante sono consentite dalla capacità dell'account.</span><span class="sxs-lookup"><span data-stu-id="710a3-128">Your storage account can have as much shares as your account capacity allows.</span></span> <span data-ttu-id="710a3-129">Per ottenere accesso a una condivisione e ai suoi contenuti, è necessario usare un client per Archiviazione file di Azure.</span><span class="sxs-lookup"><span data-stu-id="710a3-129">To obtain access to a share and its contents, you need to use a Azure File storage client.</span></span>

```java
// Create the Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

<span data-ttu-id="710a3-130">Tale client consente di ottenere un riferimento a una condivisione.</span><span class="sxs-lookup"><span data-stu-id="710a3-130">Using the Azure File storage client, you can then obtain a reference to a share.</span></span>

```java
// Get a reference to the file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

<span data-ttu-id="710a3-131">Per creare effettivamente la condivisione, utilizzare il metodo **createIfNotExists** dell'oggetto CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="710a3-131">To actually create the share, use the **createIfNotExists** method of the CloudFileShare object.</span></span>

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

<span data-ttu-id="710a3-132">A questo punto, **share** contiene un riferimento a una condivisione denominata **sampleshare**.</span><span class="sxs-lookup"><span data-stu-id="710a3-132">At this point, **share** holds a reference to a share named **sampleshare**.</span></span>

## <a name="delete-an-azure-file-share"></a><span data-ttu-id="710a3-133">Eliminare una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="710a3-133">Delete an Azure File share</span></span>
<span data-ttu-id="710a3-134">L'eliminazione di una condivisione viene eseguita chiamando il metodo **deleteIfExists** in un oggetto CloudFileShare.</span><span class="sxs-lookup"><span data-stu-id="710a3-134">Deleting a share is done by calling the **deleteIfExists** method on a CloudFileShare object.</span></span> <span data-ttu-id="710a3-135">Ecco il codice di esempio che esegue tale operazione.</span><span class="sxs-lookup"><span data-stu-id="710a3-135">Here's sample code that does that.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference to the file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a><span data-ttu-id="710a3-136">Creare una directory</span><span class="sxs-lookup"><span data-stu-id="710a3-136">Create a directory</span></span>
<span data-ttu-id="710a3-137">È inoltre possibile organizzare l'archiviazione inserendo i file all'interno di sottodirectory anziché inserirli tutti nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="710a3-137">You can also organize storage by putting files inside sub-directories instead of having all of them in the root directory.</span></span> <span data-ttu-id="710a3-138">Archiviazione file di Azure consente di creare tutte le directory consentite dall'account.</span><span class="sxs-lookup"><span data-stu-id="710a3-138">Azure File storage allows you to create as much directories as your account will allow.</span></span> <span data-ttu-id="710a3-139">Il codice riportato di seguito creerà una sottodirectory denominata **sampledir** nella directory radice.</span><span class="sxs-lookup"><span data-stu-id="710a3-139">The code below will create a sub-directory named **sampledir** under the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a><span data-ttu-id="710a3-140">Eliminare una directory</span><span class="sxs-lookup"><span data-stu-id="710a3-140">Delete a directory</span></span>
<span data-ttu-id="710a3-141">Eliminare una directory è un'attività piuttosto semplice, anche se occorre tenere presente che non è possibile eliminare una directory che contiene ancora file o altre directory.</span><span class="sxs-lookup"><span data-stu-id="710a3-141">Deleting a directory is a fairly simple task, although it should be noted that you cannot delete a directory that still contains files or other directories.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory you want to delete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete the directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a><span data-ttu-id="710a3-142">Enumerare file e directory in una condivisione file di Azure</span><span class="sxs-lookup"><span data-stu-id="710a3-142">Enumerate files and directories in an Azure File share</span></span>
<span data-ttu-id="710a3-143">Ottenere un elenco di file e directory all'interno di una condivisione è facile chiamando **listFilesAndDirectories** in un riferimento CloudFileDirectory.</span><span class="sxs-lookup"><span data-stu-id="710a3-143">Obtaining a list of files and directories within a share is easily done by calling **listFilesAndDirectories** on a CloudFileDirectory reference.</span></span> <span data-ttu-id="710a3-144">Il metodo restituisce un elenco di oggetti ListFileItem che è possibile scorrere.</span><span class="sxs-lookup"><span data-stu-id="710a3-144">The method returns a list of ListFileItem objects which you can iterate on.</span></span> <span data-ttu-id="710a3-145">Ad esempio, il seguente codice elencherà i file e le directory all'interno della directory radice.</span><span class="sxs-lookup"><span data-stu-id="710a3-145">As an example, the following code will list files and directories inside the root directory.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a><span data-ttu-id="710a3-146">Caricare un file</span><span class="sxs-lookup"><span data-stu-id="710a3-146">Upload a file</span></span>
<span data-ttu-id="710a3-147">Una condivisione file di Azure contiene almeno una directory radice in cui possono risiedere i file.</span><span class="sxs-lookup"><span data-stu-id="710a3-147">An Azure File share contains at the very least, a root directory where files can reside.</span></span> <span data-ttu-id="710a3-148">In questa sezione verrà illustrato come caricare un file dall'archiviazione locale nella directory radice di una condivisione.</span><span class="sxs-lookup"><span data-stu-id="710a3-148">In this section, you'll learn how to upload a file from local storage onto the root directory of a share.</span></span>

<span data-ttu-id="710a3-149">Il primo passaggio del caricamento di un file consiste nell'ottenere un riferimento alla directory in cui risiederà.</span><span class="sxs-lookup"><span data-stu-id="710a3-149">The first step in uploading a file is to obtain a reference to the directory where it should reside.</span></span> <span data-ttu-id="710a3-150">È possibile eseguire questa operazione chiamando il metodo **getRootDirectoryReference** dell'oggetto condivisione.</span><span class="sxs-lookup"><span data-stu-id="710a3-150">You do this by calling the **getRootDirectoryReference** method of the share object.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

<span data-ttu-id="710a3-151">Ora che si dispone di un riferimento alla directory radice della condivisione, è possibile caricarvi un file mediante il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="710a3-151">Now that you have a reference to the root directory of the share, you can upload a file onto it using the following code.</span></span>

```java
        // Define the path to a local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a><span data-ttu-id="710a3-152">Scaricare un file</span><span class="sxs-lookup"><span data-stu-id="710a3-152">Download a file</span></span>
<span data-ttu-id="710a3-153">Una delle operazioni più frequenti che verranno eseguite in Archiviazione file di Azure consiste nello scaricare i file.</span><span class="sxs-lookup"><span data-stu-id="710a3-153">One of the more frequent operations you will perform against Azure File storage is to download files.</span></span> <span data-ttu-id="710a3-154">Nell'esempio seguente, il codice scarica SampleFile.txt e ne visualizza il contenuto.</span><span class="sxs-lookup"><span data-stu-id="710a3-154">In the following example, the code downloads SampleFile.txt and displays its contents.</span></span>

```java
//Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference to the directory that contains the file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference to the file you want to download
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write the contents of the file to the console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a><span data-ttu-id="710a3-155">Eliminare un file</span><span class="sxs-lookup"><span data-stu-id="710a3-155">Delete a file</span></span>
<span data-ttu-id="710a3-156">Un'altra operazione comune è l'eliminazione dei file.</span><span class="sxs-lookup"><span data-stu-id="710a3-156">Another common Azure File storage operation is file deletion.</span></span> <span data-ttu-id="710a3-157">Il codice seguente elimina un file denominato SampleFile.txt memorizzato all'interno di una directory denominata **sampledir**.</span><span class="sxs-lookup"><span data-stu-id="710a3-157">The following code deletes a file named SampleFile.txt stored inside a directory named **sampledir**.</span></span>

```java
// Get a reference to the root directory for the share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference to the directory where the file to be deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a><span data-ttu-id="710a3-158">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="710a3-158">Next steps</span></span>
<span data-ttu-id="710a3-159">Per ulteriori informazioni su altre API di archiviazione di Azure, seguire i collegamenti seguenti.</span><span class="sxs-lookup"><span data-stu-id="710a3-159">If you would like to learn more about other Azure storage APIs, follow these links.</span></span>

* [<span data-ttu-id="710a3-160">Centro per sviluppatori Java</span><span class="sxs-lookup"><span data-stu-id="710a3-160">Java Developer Center</span></span>](http://azure.microsoft.com/develop/java/)
* [<span data-ttu-id="710a3-161">Azure Storage SDK per Java</span><span class="sxs-lookup"><span data-stu-id="710a3-161">Azure Storage SDK for Java</span></span>](https://github.com/azure/azure-storage-java)
* [<span data-ttu-id="710a3-162">Azure Storage SDK per Android</span><span class="sxs-lookup"><span data-stu-id="710a3-162">Azure Storage SDK for Android</span></span>](https://github.com/azure/azure-storage-android)
* [<span data-ttu-id="710a3-163">Riferimento all'SDK del client di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="710a3-163">Azure Storage Client SDK Reference</span></span>](http://dl.windowsazure.com/storage/javadoc/)
* [<span data-ttu-id="710a3-164">API REST dei servizi di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="710a3-164">Azure Storage Services REST API</span></span>](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [<span data-ttu-id="710a3-165">Blog del team di Archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="710a3-165">Azure Storage Team Blog</span></span>](http://blogs.msdn.com/b/windowsazurestorage/)
* [<span data-ttu-id="710a3-166">Trasferire dati con l'utilità della riga di comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="710a3-166">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)