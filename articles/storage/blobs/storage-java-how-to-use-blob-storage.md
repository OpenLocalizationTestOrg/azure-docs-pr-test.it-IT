---
title: Come usare l'archiviazione BLOB di Azure (archiviazione di oggetti) da Java | Microsoft Docs
description: Archiviare i dati non strutturati nel cloud con l'archivio BLOB (archivio di oggetti) di Azure.
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
ms.openlocfilehash: e4de1bc57adf668f383d1fbaf4a721a61576d2a0
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-use-blob-storage-from-java"></a><span data-ttu-id="d0921-103">Come usare l'archiviazione BLOB da Java</span><span class="sxs-lookup"><span data-stu-id="d0921-103">How to use Blob storage from Java</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../../includes/storage-check-out-samples-java.md)]

## <a name="overview"></a><span data-ttu-id="d0921-104">Overview</span><span class="sxs-lookup"><span data-stu-id="d0921-104">Overview</span></span>
<span data-ttu-id="d0921-105">L'archiviazione BLOB di Azure è un servizio che archivia dati non strutturati nel cloud come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="d0921-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="d0921-106">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d0921-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="d0921-107">L'archivio BLOB è anche denominato archivio di oggetti.</span><span class="sxs-lookup"><span data-stu-id="d0921-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="d0921-108">Questa guida illustra i diversi scenari comuni di utilizzo del servizio di archiviazione BLOB di Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="d0921-108">This article will show you how to perform common scenarios using the Microsoft Azure Blob storage.</span></span> <span data-ttu-id="d0921-109">Gli esempi sono scritti in Java e usano [Azure Storage SDK per Java][Azure Storage SDK for Java].</span><span class="sxs-lookup"><span data-stu-id="d0921-109">The samples are written in Java and use the [Azure Storage SDK for Java][Azure Storage SDK for Java].</span></span> <span data-ttu-id="d0921-110">Gli scenari illustrati includono **caricamento**, **visualizzazione in elenchi**, **download** e **eliminazione** di BLOB.</span><span class="sxs-lookup"><span data-stu-id="d0921-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="d0921-111">Per ulteriori informazioni sui BLOB, vedere la sezione [Passaggi successivi](#Next-Steps) .</span><span class="sxs-lookup"><span data-stu-id="d0921-111">For more information on blobs, see the [Next Steps](#Next-Steps) section.</span></span>

> [!NOTE]
> <span data-ttu-id="d0921-112">per gli sviluppatori che usano il servizio di archiviazione di Azure in dispositivi Android, è disponibile un SDK specifico.</span><span class="sxs-lookup"><span data-stu-id="d0921-112">An SDK is available for developers who are using Azure Storage on Android devices.</span></span> <span data-ttu-id="d0921-113">Per altre informazioni, vedere [Azure Storage SDK per Android][Azure Storage SDK for Android].</span><span class="sxs-lookup"><span data-stu-id="d0921-113">For more information, see the [Azure Storage SDK for Android][Azure Storage SDK for Android].</span></span>
>
>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-java-application"></a><span data-ttu-id="d0921-114">Creare un'applicazione Java</span><span class="sxs-lookup"><span data-stu-id="d0921-114">Create a Java application</span></span>
<span data-ttu-id="d0921-115">In questo articolo, si useranno le funzionalità di archiviazione che possono essere eseguite in un'applicazione Java in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in Azure.</span><span class="sxs-lookup"><span data-stu-id="d0921-115">In this article, you will use storage features which can be run within a Java application locally, or in code running within a web role or worker role in Azure.</span></span>

<span data-ttu-id="d0921-116">A questo scopo, è necessario installare Java Development Kit (JDK) e creare un account di archiviazione di Azure nella sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="d0921-116">To do so, you will need to install the Java Development Kit (JDK) and create an Azure Storage account in your Azure subscription.</span></span> <span data-ttu-id="d0921-117">Dopo avere eseguito questa operazione, sarà necessario verificare che il sistema di sviluppo in uso soddisfi i requisiti minimi e le dipendenze elencate nel repository [Azure Storage SDK per Java][Azure Storage SDK for Java] su GitHub.</span><span class="sxs-lookup"><span data-stu-id="d0921-117">Once you have done so, you will need to verify that your development system meets the minimum requirements and dependencies which are listed in the [Azure Storage SDK for Java][Azure Storage SDK for Java] repository on GitHub.</span></span> <span data-ttu-id="d0921-118">Se il sistema soddisfa i requisiti, è possibile seguire le istruzioni per scaricare e installare le librerie di archiviazione di Azure per Java nel sistema dall'archivio indicato.</span><span class="sxs-lookup"><span data-stu-id="d0921-118">If your system meets those requirements, you can follow the instructions for downloading and installing the Azure Storage Libraries for Java on your system from that repository.</span></span> <span data-ttu-id="d0921-119">Dopo avere completato queste attività, sarà possibile creare un'applicazione Java che usa gli esempi illustrati in questo articolo.</span><span class="sxs-lookup"><span data-stu-id="d0921-119">Once you have completed those tasks, you will be able to create a Java application which uses the examples in this article.</span></span>

## <a name="configure-your-application-to-access-blob-storage"></a><span data-ttu-id="d0921-120">Configurazione dell'applicazione per l'accesso all'archiviazione BLOB</span><span class="sxs-lookup"><span data-stu-id="d0921-120">Configure your application to access Blob storage</span></span>
<span data-ttu-id="d0921-121">Aggiungere le istruzioni import seguenti all'inizio del file Java in cui si desidera usare le API di archiviazione di Azure per accedere ai BLOB:</span><span class="sxs-lookup"><span data-stu-id="d0921-121">Add the following import statements to the top of the Java file where you want to use the Azure Storage APIs to access blobs.</span></span>

```java
// Include the following imports to use blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.blob.*;
```

## <a name="set-up-an-azure-storage-connection-string"></a><span data-ttu-id="d0921-122">Configurare una stringa di connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="d0921-122">Set up an Azure Storage connection string</span></span>
<span data-ttu-id="d0921-123">I client di archiviazione di Azure usano le stringhe di connessione di archiviazione per archiviare endpoint e credenziali per l'accesso ai servizi di gestione dati.</span><span class="sxs-lookup"><span data-stu-id="d0921-123">An Azure Storage client uses a storage connection string to store endpoints and credentials for accessing data management services.</span></span> <span data-ttu-id="d0921-124">Quando si esegue un'applicazione client, è necessario specificare la stringa di connessione di archiviazione nel formato seguente, usando il nome dell'account di archiviazione e la chiave di accesso primaria relativa all'account di archiviazione riportata nel [portale di Azure](https://portal.azure.com) per i valori *AccountName* e *AccountKey*.</span><span class="sxs-lookup"><span data-stu-id="d0921-124">When running in a client application, you must provide the storage connection string in the following format, using the name of your storage account and the Primary access key for the storage account listed in the [Azure portal](https://portal.azure.com) for the *AccountName* and *AccountKey* values.</span></span> <span data-ttu-id="d0921-125">In questo esempio viene illustrato come dichiarare un campo statico per memorizzare la stringa di connessione:</span><span class="sxs-lookup"><span data-stu-id="d0921-125">The following example shows how you can declare a static field to hold the connection string.</span></span>

```java
// Define the connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key";
```

<span data-ttu-id="d0921-126">In un'applicazione in esecuzione in un ruolo di Microsoft Azure, questa stringa può essere archiviata nel file di configurazione del servizio *ServiceConfiguration.cscfg*ed è accessibile con una chiamata al metodo **RoleEnvironment.getConfigurationSettings** .</span><span class="sxs-lookup"><span data-stu-id="d0921-126">In an application running within a role in Microsoft Azure, this string can be stored in the service configuration file, *ServiceConfiguration.cscfg*, and can be accessed with a call to the **RoleEnvironment.getConfigurationSettings** method.</span></span> <span data-ttu-id="d0921-127">Nell'esempio seguente viene recuperata la stringa di connessione da un elemento **Setting** denominato *StorageConnectionString* nel file di configurazione del servizio.</span><span class="sxs-lookup"><span data-stu-id="d0921-127">The following example gets the connection string from a **Setting** element named *StorageConnectionString* in the service configuration file.</span></span>

```java
// Retrieve storage account from connection-string.
String storageConnectionString =
    RoleEnvironment.getConfigurationSettings().get("StorageConnectionString");
```

<span data-ttu-id="d0921-128">Gli esempi seguenti presumono che sia stato usato uno di questi due metodi per ottenere la stringa di connessione di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="d0921-128">The following samples assume that you have used one of these two methods to get the storage connection string.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="d0921-129">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="d0921-129">Create a container</span></span>
<span data-ttu-id="d0921-130">Gli oggetti **CloudBlobClient** consentono di ottenere oggetti di riferimento per contenitori e BLOB.</span><span class="sxs-lookup"><span data-stu-id="d0921-130">A **CloudBlobClient** object lets you get reference objects for containers and blobs.</span></span> <span data-ttu-id="d0921-131">Il codice seguente consente di creare un oggetto **CloudBlobClient** .</span><span class="sxs-lookup"><span data-stu-id="d0921-131">The following code creates a **CloudBlobClient** object.</span></span>

> [!NOTE]
> <span data-ttu-id="d0921-132">Esistono altri modi per creare oggetti **CloudStorageAccount**. Per altre informazioni, vedere **CloudStorageAccount** nel [Riferimento all'SDK del client di Archiviazione di Azure].</span><span class="sxs-lookup"><span data-stu-id="d0921-132">There are additional ways to create **CloudStorageAccount** objects; for more information, see **CloudStorageAccount** in the [Azure Storage Client SDK Reference].</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="d0921-133">Utilizzare l'oggetto **CloudBlobClient** per ottenere un riferimento al contenitore da utilizzare.</span><span class="sxs-lookup"><span data-stu-id="d0921-133">Use the **CloudBlobClient** object to get a reference to the container you want to use.</span></span> <span data-ttu-id="d0921-134">È possibile creare un contenitore, se non esiste, con il metodo **createIfNotExists** , che in caso contrario restituirà il contenitore esistente.</span><span class="sxs-lookup"><span data-stu-id="d0921-134">You can create the container if it doesn't exist with the **createIfNotExists** method, which will otherwise return the existing container.</span></span> <span data-ttu-id="d0921-135">Per impostazione predefinita, il nuovo contenitore è privato ed è necessario specificare la chiave di accesso alle risorse di archiviazione, come già fatto in precedenza, per scaricare BLOB da questo contenitore.</span><span class="sxs-lookup"><span data-stu-id="d0921-135">By default, the new container is private, so you must specify your storage access key (as you did earlier) to download blobs from this container.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Get a reference to a container.
    // The container name must be lower case
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Create the container if it does not exist.
    container.createIfNotExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

### <a name="optional-configure-a-container-for-public-access"></a><span data-ttu-id="d0921-136">Facoltativo: configurare un contenitore per l'accesso pubblico</span><span class="sxs-lookup"><span data-stu-id="d0921-136">Optional: Configure a container for public access</span></span>
<span data-ttu-id="d0921-137">Per impostazione predefinita autorizzazioni di un contenitore sono configurate per l'accesso privato, ma è possibile configurare le autorizzazioni di un contenitore per consentire l'accesso pubblico di sola lettura per tutti gli utenti in Internet:</span><span class="sxs-lookup"><span data-stu-id="d0921-137">A container's permissions are configured for private access by default, but you can easily configure a container's permissions to allow public, read-only access for all users on the Internet:</span></span>

```java
// Create a permissions object.
BlobContainerPermissions containerPermissions = new BlobContainerPermissions();

// Include public access in the permissions object.
containerPermissions.setPublicAccess(BlobContainerPublicAccessType.CONTAINER);

// Set the permissions on the container.
container.uploadPermissions(containerPermissions);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="d0921-138">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="d0921-138">Upload a blob into a container</span></span>
<span data-ttu-id="d0921-139">Per caricare un file in un BLOB, ottenere un riferimento a un contenitore e utilizzarlo per ottenere un riferimento a un BLOB.</span><span class="sxs-lookup"><span data-stu-id="d0921-139">To upload a file to a blob, get a container reference and use it to get a blob reference.</span></span> <span data-ttu-id="d0921-140">Dopo aver ottenuto un riferimento al BLOB, sarà possibile caricarvi qualsiasi flusso di dati chiamando upload sul riferimento al BLOB.</span><span class="sxs-lookup"><span data-stu-id="d0921-140">Once you have a blob reference, you can upload any stream by calling upload on the blob reference.</span></span> <span data-ttu-id="d0921-141">Questa operazione consentirà di creare il BLOB se non esistente o di sovrascriverlo se esistente.</span><span class="sxs-lookup"><span data-stu-id="d0921-141">This operation will create the blob if it doesn't exist, or overwrite it if it does.</span></span> <span data-ttu-id="d0921-142">Nel codice seguente viene illustrato come effettuare questa operazione presupponendo che il contenitore sia già stato creato.</span><span class="sxs-lookup"><span data-stu-id="d0921-142">The following code sample shows this, and assumes that the container has already been created.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Define the path to a local file.
    final String filePath = "C:\\myimages\\myimage.jpg";

    // Create or overwrite the "myimage.jpg" blob with contents from a local file.
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");
    File source = new File(filePath);
    blob.upload(new FileInputStream(source), source.length());
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="d0921-143">Elencare i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="d0921-143">List the blobs in a container</span></span>
<span data-ttu-id="d0921-144">Per elencare i BLOB in un contenitore, ottenere prima un riferimento al contenitore, come previsto per caricare un BLOB.</span><span class="sxs-lookup"><span data-stu-id="d0921-144">To list the blobs in a container, first get a container reference like you did to upload a blob.</span></span> <span data-ttu-id="d0921-145">È possibile usare il metodo **listBlobs** del contenitore con un ciclo **for**.</span><span class="sxs-lookup"><span data-stu-id="d0921-145">You can use the container's **listBlobs** method with a **for** loop.</span></span> <span data-ttu-id="d0921-146">Il codice seguente consente di inviare alla console l'URI di ogni BLOB in un contenitore.</span><span class="sxs-lookup"><span data-stu-id="d0921-146">The following code outputs the Uri of each blob in a container to the console.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop over blobs within the container and output the URI to each of them.
    for (ListBlobItem blobItem : container.listBlobs()) {
        System.out.println(blobItem.getUri());
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

<span data-ttu-id="d0921-147">Notare che è possibile assegnare il nome ai BLOB con le informazioni sul percorso nel nome.</span><span class="sxs-lookup"><span data-stu-id="d0921-147">Note that you can name blobs with path information in their names.</span></span> <span data-ttu-id="d0921-148">Consente di creare una struttura di directory virtuale che è possibile organizzare e attraversare come un file system tradizionale.</span><span class="sxs-lookup"><span data-stu-id="d0921-148">This creates a virtual directory structure that you can organize and traverse as you would a traditional file system.</span></span> <span data-ttu-id="d0921-149">Si noti che la struttura di directory è solo virtuale, le uniche risorse disponibili nell'archiviazione BLOB sono i contenitori e i BLOB.</span><span class="sxs-lookup"><span data-stu-id="d0921-149">Note that the directory structure is virtual only - the only resources available in Blob storage are containers and blobs.</span></span> <span data-ttu-id="d0921-150">Tuttavia, la libreria client offre un oggetto **CloudBlobDirectory** per fare riferimento a una directory virtuale e semplificare il processo di utilizzo dei BLOB organizzati in questo modo.</span><span class="sxs-lookup"><span data-stu-id="d0921-150">However, the client library offers a **CloudBlobDirectory** object to refer to a virtual directory and simplify the process of working with blobs that are organized in this way.</span></span>

<span data-ttu-id="d0921-151">È ad esempio possibile disporre di un contenitore denominato "photos", in cui sono stati caricati i BLOB denominati "rootphoto1", "2010/photo1", "2010/photo2" e "2011/photo1".</span><span class="sxs-lookup"><span data-stu-id="d0921-151">For example, you could have a container named "photos", in which you might upload blobs named "rootphoto1", "2010/photo1", "2010/photo2", and "2011/photo1".</span></span> <span data-ttu-id="d0921-152">Questa situazione implica in genere la creazione delle directory virtuali "2010" e "2011" nel contenitore "photos".</span><span class="sxs-lookup"><span data-stu-id="d0921-152">This would create the virtual directories "2010" and "2011" within the "photos" container.</span></span> <span data-ttu-id="d0921-153">Quando si chiama **listBlobs** sul contenitore "photos", la raccolta restituita conterrà gli oggetti **CloudBlobDirectory** e **CloudBlob** che rappresentano le directory e i BLOB contenuti al primo livello.</span><span class="sxs-lookup"><span data-stu-id="d0921-153">When you call **listBlobs** on the "photos" container, the collection returned will contain **CloudBlobDirectory** and **CloudBlob** objects representing the directories and blobs contained at the top level.</span></span> <span data-ttu-id="d0921-154">In questo caso oltre alle directory "2010" e "2011", verrà restituita anche la foto "rootphoto1".</span><span class="sxs-lookup"><span data-stu-id="d0921-154">In this case, directories "2010" and "2011", as well as photo "rootphoto1" would be returned.</span></span> <span data-ttu-id="d0921-155">È possibile utilizzare l'operatore **instanceof** per distinguere questi oggetti.</span><span class="sxs-lookup"><span data-stu-id="d0921-155">You can use the **instanceof** operator to distinguish these objects.</span></span>

<span data-ttu-id="d0921-156">Facoltativamente, è possibile passare parametri al metodo **listBlobs** con il parametro **useFlatBlobListing** impostato su True.</span><span class="sxs-lookup"><span data-stu-id="d0921-156">Optionally, you can pass in parameters to the **listBlobs** method with the **useFlatBlobListing** parameter set to true.</span></span> <span data-ttu-id="d0921-157">In questo modo verranno restituiti tutti i BLOB indipendentemente dalla directory.</span><span class="sxs-lookup"><span data-stu-id="d0921-157">This will result in every blob being returned, regardless of directory.</span></span> <span data-ttu-id="d0921-158">Per altre informazioni, vedere **CloudBlobContainer.listBlobs** nel [Riferimento all'SDK del client di Archiviazione di Azure].</span><span class="sxs-lookup"><span data-stu-id="d0921-158">For more information, see **CloudBlobContainer.listBlobs** in the [Azure Storage Client SDK Reference].</span></span>

## <a name="download-a-blob"></a><span data-ttu-id="d0921-159">Scaricare un BLOB</span><span class="sxs-lookup"><span data-stu-id="d0921-159">Download a blob</span></span>
<span data-ttu-id="d0921-160">Per scaricare i BLOB, eseguire la stessa procedura illustrata per caricarli al fine di ottenere un riferimento al BLOB.</span><span class="sxs-lookup"><span data-stu-id="d0921-160">To download blobs, follow the same steps as you did for uploading a blob in order to get a blob reference.</span></span> <span data-ttu-id="d0921-161">Nell'esempio di caricamento è stato chiamato upload sull'oggetto BLOB.</span><span class="sxs-lookup"><span data-stu-id="d0921-161">In the uploading example, you called upload on the blob object.</span></span> <span data-ttu-id="d0921-162">Nell'esempio seguente verrà chiamato download per trasferire il contenuto del BLOB in un oggetto stream, come **FileOutputStream** , che è possibile utilizzare per mantenere il BLOB in un file locale.</span><span class="sxs-lookup"><span data-stu-id="d0921-162">In the following example, call download to transfer the blob contents to a stream object such as a **FileOutputStream** that you can use to persist the blob to a local file.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Loop through each blob item in the container.
    for (ListBlobItem blobItem : container.listBlobs()) {
        // If the item is a blob, not a virtual directory.
        if (blobItem instanceof CloudBlob) {
            // Download the item and save it to a file with the same name.
            CloudBlob blob = (CloudBlob) blobItem;
            blob.download(new FileOutputStream("C:\\mydownloads\\" + blob.getName()));
        }
    }
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob"></a><span data-ttu-id="d0921-163">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="d0921-163">Delete a blob</span></span>
<span data-ttu-id="d0921-164">Per eliminare un BLOB, ottenere il riferimento al BLOB e chiamare **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="d0921-164">To delete a blob, get a blob reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Retrieve reference to a blob named "myimage.jpg".
    CloudBlockBlob blob = container.getBlockBlobReference("myimage.jpg");

    // Delete the blob.
    blob.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="d0921-165">Eliminare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="d0921-165">Delete a blob container</span></span>
<span data-ttu-id="d0921-166">Infine, per eliminare un contenitore BLOB, ottenere un riferimento al contenitore BLOB e richiamare **deleteIfExists**.</span><span class="sxs-lookup"><span data-stu-id="d0921-166">Finally, to delete a blob container, get a blob container reference, and call **deleteIfExists**.</span></span>

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create the blob client.
    CloudBlobClient blobClient = storageAccount.createCloudBlobClient();

    // Retrieve reference to a previously created container.
    CloudBlobContainer container = blobClient.getContainerReference("mycontainer");

    // Delete the blob container.
    container.deleteIfExists();
}
catch (Exception e)
{
    // Output the stack trace.
    e.printStackTrace();
}
```

## <a name="next-steps"></a><span data-ttu-id="d0921-167">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d0921-167">Next steps</span></span>
<span data-ttu-id="d0921-168">A questo punto, dopo aver appreso le nozioni di base dell'archiviazione BLOB, visitare i collegamenti seguenti per altre informazioni sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="d0921-168">Now that you've learned the basics of Blob storage, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="d0921-169">[Azure Storage SDK per Java][Azure Storage SDK for Java]</span><span class="sxs-lookup"><span data-stu-id="d0921-169">[Azure Storage SDK for Java][Azure Storage SDK for Java]</span></span>
* <span data-ttu-id="d0921-170">[Riferimento all'SDK del client di Archiviazione di Azure][Riferimento all'SDK del client di Archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="d0921-170">[Azure Storage Client SDK Reference][Azure Storage Client SDK Reference]</span></span>
* <span data-ttu-id="d0921-171">[API REST di Archiviazione di Azure][Azure Storage REST API]</span><span class="sxs-lookup"><span data-stu-id="d0921-171">[Azure Storage REST API][Azure Storage REST API]</span></span>
* <span data-ttu-id="d0921-172">[Blog del team di Archiviazione di Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="d0921-172">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>

<span data-ttu-id="d0921-173">Per altre informazioni, vedere anche [Azure for Java developers](/java/azure) (Azure per sviluppatori Java).</span><span class="sxs-lookup"><span data-stu-id="d0921-173">For more information, see also [Azure for Java developers](/java/azure).</span></span>

[Azure SDK for Java]: http://go.microsoft.com/fwlink/?LinkID=525671
[Azure Storage SDK for Java]: https://github.com/azure/azure-storage-java
[Azure Storage SDK for Android]: https://github.com/azure/azure-storage-android
[Riferimento all'SDK del client di Archiviazione di Azure]: http://dl.windowsazure.com/storage/javadoc/
[Azure Storage REST API]: https://msdn.microsoft.com/library/azure/dd179355.aspx
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
