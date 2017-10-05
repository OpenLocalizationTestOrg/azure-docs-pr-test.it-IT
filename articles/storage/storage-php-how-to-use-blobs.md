---
title: Come usare l'archiviazione BLOB (archiviazione di oggetti) da PHP | Microsoft Docs
description: Archiviare i dati non strutturati nel cloud con l'archivio BLOB (archivio di oggetti) di Azure.
documentationcenter: php
services: storage
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 1af56b59-b3f0-4b46-8441-aab463ae088e
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: PHP
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 2c356d7faafa8ef4591087b5b1f949b9374732be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-blob-storage-from-php"></a><span data-ttu-id="341a1-103">Come usare l'archiviazione BLOB da PHP</span><span class="sxs-lookup"><span data-stu-id="341a1-103">How to use blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="341a1-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="341a1-104">Overview</span></span>
<span data-ttu-id="341a1-105">L'archiviazione BLOB di Azure è un servizio che archivia dati non strutturati nel cloud come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="341a1-105">Azure Blob storage is a service that stores unstructured data in the cloud as objects/blobs.</span></span> <span data-ttu-id="341a1-106">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="341a1-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="341a1-107">L'archivio BLOB è anche denominato archivio di oggetti.</span><span class="sxs-lookup"><span data-stu-id="341a1-107">Blob storage is also referred to as object storage.</span></span>

<span data-ttu-id="341a1-108">Questa guida illustra diversi scenari di utilizzo comuni del servizio BLOB di Azure.</span><span class="sxs-lookup"><span data-stu-id="341a1-108">This guide shows you how to perform common scenarios using the Azure blob service.</span></span> <span data-ttu-id="341a1-109">Gli esempi sono scritti in PHP e usano [Azure SDK per PHP][download].</span><span class="sxs-lookup"><span data-stu-id="341a1-109">The samples are written in PHP and use the [Azure SDK for PHP][download].</span></span> <span data-ttu-id="341a1-110">Gli scenari illustrati includono **caricamento**, **visualizzazione in elenchi**, **download** e **eliminazione** di BLOB.</span><span class="sxs-lookup"><span data-stu-id="341a1-110">The scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="341a1-111">Per ulteriori informazioni sui BLOB, vedere la sezione [Passaggi successivi](#next-steps) .</span><span class="sxs-lookup"><span data-stu-id="341a1-111">For more information on blobs, see the [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="341a1-112">Creare un'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="341a1-112">Create a PHP application</span></span>
<span data-ttu-id="341a1-113">Per creare un'applicazione PHP che accede al servizio BLOB di Azure, è sufficiente fare riferimento alle classi in Azure SDK per PHP dall'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="341a1-113">The only requirement for creating a PHP application that accesses the Azure blob service is the referencing of classes in the Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="341a1-114">Per creare l'applicazione, è possibile usare qualsiasi strumento di sviluppo, incluso il Blocco note.</span><span class="sxs-lookup"><span data-stu-id="341a1-114">You can use any development tools to create your application, including Notepad.</span></span>

<span data-ttu-id="341a1-115">In questa guida si useranno le funzionalità del servizio che possono essere chiamate in un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="341a1-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-the-azure-client-libraries"></a><span data-ttu-id="341a1-116">Acquisire le librerie client di Azure</span><span class="sxs-lookup"><span data-stu-id="341a1-116">Get the Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-to-access-the-blob-service"></a><span data-ttu-id="341a1-117">Configurare l'applicazione per l'accesso al servizio BLOB</span><span class="sxs-lookup"><span data-stu-id="341a1-117">Configure your application to access the blob service</span></span>
<span data-ttu-id="341a1-118">Per usare le API del servizio BLOB di Azure, è necessario:</span><span class="sxs-lookup"><span data-stu-id="341a1-118">To use the Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="341a1-119">Fare riferimento al file autoloader mediante l'istruzione [require_once].</span><span class="sxs-lookup"><span data-stu-id="341a1-119">Reference the autoloader file using the [require_once] statement, and</span></span>
2. <span data-ttu-id="341a1-120">Fare riferimento a tutte le eventuali classi utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="341a1-120">Reference any classes you might use.</span></span>

<span data-ttu-id="341a1-121">Nell'esempio seguente viene indicato come includere il file autoloader e fare riferimento alla classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="341a1-121">The following example shows how to include the autoloader file and reference the **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="341a1-122">Gli esempi in questo articolo presuppongono che siano state installate le librerie client PHP per Azure tramite Composer.</span><span class="sxs-lookup"><span data-stu-id="341a1-122">The examples in this article assume you have installed the PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="341a1-123">Se le librerie sono state installate manualmente, sarà necessario fare riferimento al file autoloader `WindowsAzure.php` .</span><span class="sxs-lookup"><span data-stu-id="341a1-123">If you installed the libraries manually, you need to reference the `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="341a1-124">Nei seguenti esempi l'istruzione `require_once` verrà sempre visualizzata, ma si fa riferimento solo alle classi necessarie per eseguire l'esempio.</span><span class="sxs-lookup"><span data-stu-id="341a1-124">In the examples below, the `require_once` statement will be shown always, but only the classes necessary for the example to execute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="341a1-125">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="341a1-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="341a1-126">Per creare un'istanza di un client del servizio BLOB di Azure, è necessario innanzitutto disporre di una stringa di connessione valida.</span><span class="sxs-lookup"><span data-stu-id="341a1-126">To instantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="341a1-127">Il formato della stringa di connessione del servizio BLOB è:</span><span class="sxs-lookup"><span data-stu-id="341a1-127">The format for the blob service connection string is:</span></span>

<span data-ttu-id="341a1-128">Per accedere a un servizio attivo:</span><span class="sxs-lookup"><span data-stu-id="341a1-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="341a1-129">Per accedere alla memoria dell'emulatore:</span><span class="sxs-lookup"><span data-stu-id="341a1-129">For accessing the storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="341a1-130">Per creare un client di servizio di Azure, è necessario usare la classe **ServicesBuilder** .</span><span class="sxs-lookup"><span data-stu-id="341a1-130">To create any Azure service client, you need to use the **ServicesBuilder** class.</span></span> <span data-ttu-id="341a1-131">È possibile:</span><span class="sxs-lookup"><span data-stu-id="341a1-131">You can:</span></span>

* <span data-ttu-id="341a1-132">passare la stringa di connessione direttamente a essa o</span><span class="sxs-lookup"><span data-stu-id="341a1-132">Pass the connection string directly to it or</span></span>
* <span data-ttu-id="341a1-133">utilizzare **CloudConfigurationManager (CCM)** per cercare la stringa di connessione in più origini esterne:</span><span class="sxs-lookup"><span data-stu-id="341a1-133">Use the **CloudConfigurationManager (CCM)** to check multiple external sources for the connection string:</span></span>
  * <span data-ttu-id="341a1-134">per impostazione predefinita viene fornito con il supporto per un'origine esterna - ovvero le variabili ambientali</span><span class="sxs-lookup"><span data-stu-id="341a1-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="341a1-135">è possibile aggiungere nuove origini estendendo la classe **ConnectionStringSource**</span><span class="sxs-lookup"><span data-stu-id="341a1-135">You can add new sources by extending the **ConnectionStringSource** class.</span></span>

<span data-ttu-id="341a1-136">Per gli esempi illustrati in questo articolo, la stringa di connessione verrà passata direttamente.</span><span class="sxs-lookup"><span data-stu-id="341a1-136">For the examples outlined here, the connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="341a1-137">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="341a1-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="341a1-138">Un oggetto **BlobRestProxy** consente di creare un contenitore BLOB con il metodo **createContainer**.</span><span class="sxs-lookup"><span data-stu-id="341a1-138">A **BlobRestProxy** object lets you create a blob container with the **createContainer** method.</span></span> <span data-ttu-id="341a1-139">Quando si crea un contenitore, è possibile impostare le opzioni per il contenitore, anche se tale operazione non è necessaria.</span><span class="sxs-lookup"><span data-stu-id="341a1-139">When creating a container, you can set options on the container, but doing so is not required.</span></span> <span data-ttu-id="341a1-140">(Nell'esempio seguente viene illustrato come impostare l'elenco ACL del contenitore e i metadati del contenitore.)</span><span class="sxs-lookup"><span data-stu-id="341a1-140">(The example below shows how to set the container access control list (ACL) and container metadata.)</span></span>

```php
require_once 'vendor\autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Blob\Models\CreateContainerOptions;
use MicrosoftAzure\Storage\Blob\Models\PublicAccessType;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


// OPTIONAL: Set public access policy and metadata.
// Create container options object.
$createContainerOptions = new CreateContainerOptions();

// Set public access policy. Possible values are
// PublicAccessType::CONTAINER_AND_BLOBS and PublicAccessType::BLOBS_ONLY.
// CONTAINER_AND_BLOBS:
// Specifies full public read access for container and blob data.
// proxys can enumerate blobs within the container via anonymous
// request, but cannot enumerate containers within the storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within the container via
// anonymous request.
// If this value is not specified in the request, container data is
// private to the account owner.
$createContainerOptions->setPublicAccess(PublicAccessType::CONTAINER_AND_BLOBS);

// Set container metadata.
$createContainerOptions->addMetaData("key1", "value1");
$createContainerOptions->addMetaData("key2", "value2");

try    {
    // Create container.
    $blobRestProxy->createContainer("mycontainer", $createContainerOptions);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="341a1-141">Con la chiamata a **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** il contenitore e i dati BLOB diventano accessibili tramite richieste anonime.</span><span class="sxs-lookup"><span data-stu-id="341a1-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes the container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="341a1-142">Con la chiamata a **setPublicAccess(PublicAccessType::BLOBS_ONLY)**, invece, solo i dati BLOB diventano accessibili tramite richieste anonime.</span><span class="sxs-lookup"><span data-stu-id="341a1-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="341a1-143">Per altre informazioni sugli ACL contenitore, vedere [Set container ACL (REST API)][container-acl] (Configurare ACL contenitore - API REST).</span><span class="sxs-lookup"><span data-stu-id="341a1-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="341a1-144">Per altre informazioni sui codici errore del servizio BLOB, vedere [Blob Service Error Codes][error-codes] (Codici errore del servizio BLOB).</span><span class="sxs-lookup"><span data-stu-id="341a1-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="341a1-145">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="341a1-145">Upload a blob into a container</span></span>
<span data-ttu-id="341a1-146">Per caricare un file come BLOB, usare il metodo **BlobRestProxy->createBlockBlob**.</span><span class="sxs-lookup"><span data-stu-id="341a1-146">To upload a file as a blob, use the **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="341a1-147">Questa operazione consentirà di creare il BLOB se non esistente o di sovrascriverlo se esistente.</span><span class="sxs-lookup"><span data-stu-id="341a1-147">This operation creates the blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="341a1-148">Nell'esempio di codice seguente si presuppone che il contenitore sia già stato creato e che usi [fopen][fopen] per aprire il file come flusso.</span><span class="sxs-lookup"><span data-stu-id="341a1-148">The code example below assumes that the container has already been created and uses [fopen][fopen] to open the file as a stream.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


$content = fopen("c:\myfile.txt", "r");
$blob_name = "myblob";

try    {
    //Upload blob
    $blobRestProxy->createBlockBlob("mycontainer", $blob_name, $content);
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="341a1-149">Si noti che l'esempio precedente consente di caricare un BLOB come flusso.</span><span class="sxs-lookup"><span data-stu-id="341a1-149">Note that the previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="341a1-150">Un BLOB può tuttavia essere caricato anche come stringa, ad esempio mediante la funzione [file\_get\_contents][file_get_contents].</span><span class="sxs-lookup"><span data-stu-id="341a1-150">However, a blob can also be uploaded as a string using, for example, the [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="341a1-151">A tale scopo utilizzare l'esempio precedente, modificare `$content = fopen("c:\myfile.txt", "r");` con `$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="341a1-151">To do this using the previous sample, change `$content = fopen("c:\myfile.txt", "r");` to `$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="341a1-152">Elencare i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="341a1-152">List the blobs in a container</span></span>
<span data-ttu-id="341a1-153">Per elencare i BLOB in un contenitore, usare il metodo **BlobRestProxy->listBlobs** con un ciclo **foreach** per eseguire il ciclo nel risultato.</span><span class="sxs-lookup"><span data-stu-id="341a1-153">To list the blobs in a container, use the **BlobRestProxy->listBlobs** method with a **foreach** loop to loop through the result.</span></span> <span data-ttu-id="341a1-154">Il codice seguente mostra il nome di ogni BLOB come output in un contenitore e mostra il relativo URI al browser.</span><span class="sxs-lookup"><span data-stu-id="341a1-154">The following code displays the name of each blob as output in a container and displays its URI to the browser.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // List blobs.
    $blob_list = $blobRestProxy->listBlobs("mycontainer");
    $blobs = $blob_list->getBlobs();

    foreach($blobs as $blob)
    {
        echo $blob->getName().": ".$blob->getUrl()."<br />";
    }
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="download-a-blob"></a><span data-ttu-id="341a1-155">Scaricare un BLOB</span><span class="sxs-lookup"><span data-stu-id="341a1-155">Download a blob</span></span>
<span data-ttu-id="341a1-156">Per scaricare un BLOB, chiamare il metodo **BlobRestProxy->getBlob**, quindi chiamare il metodo **getContentStream** nell'oggetto **GetBlobResult** risultante.</span><span class="sxs-lookup"><span data-stu-id="341a1-156">To download a blob, call the **BlobRestProxy->getBlob** method, then call the **getContentStream** method on the resulting **GetBlobResult** object.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Get blob.
    $blob = $blobRestProxy->getBlob("mycontainer", "myblob");
    fpassthru($blob->getContentStream());
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

<span data-ttu-id="341a1-157">Si noti che con l'esempio precedente si ottiene un BLOB come risorsa di flusso (comportamento predefinito).</span><span class="sxs-lookup"><span data-stu-id="341a1-157">Note that the example above gets a blob as a stream resource (the default behavior).</span></span> <span data-ttu-id="341a1-158">È tuttavia possibile usare la funzione [stream\_get\_contents][stream-get-contents] per convertire il flusso restituito in una stringa.</span><span class="sxs-lookup"><span data-stu-id="341a1-158">However, you can use the [stream\_get\_contents][stream-get-contents] function to convert the returned stream to a string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="341a1-159">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="341a1-159">Delete a blob</span></span>
<span data-ttu-id="341a1-160">Per eliminare un BLOB, passare il nome del contenitore e il nome del BLOB a **BlobRestProxy->deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="341a1-160">To delete a blob, pass the container name and blob name to **BlobRestProxy->deleteBlob**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);


try    {
    // Delete blob.
    $blobRestProxy->deleteBlob("mycontainer", "myblob");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="delete-a-blob-container"></a><span data-ttu-id="341a1-161">Eliminare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="341a1-161">Delete a blob container</span></span>
<span data-ttu-id="341a1-162">Per eliminare un contenere di BLOB, infine, passare il nome del contenitore a **BlobRestProxy->deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="341a1-162">Finally, to delete a blob container, pass the container name to **BlobRestProxy->deleteContainer**.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;
use MicrosoftAzure\Storage\Common\ServiceException;

// Create blob REST proxy.
$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);

try    {
    // Delete container.
    $blobRestProxy->deleteContainer("mycontainer");
}
catch(ServiceException $e){
    // Handle exception based on error codes and messages.
    // Error codes and messages are here:
    // http://msdn.microsoft.com/library/azure/dd179439.aspx
    $code = $e->getCode();
    $error_message = $e->getMessage();
    echo $code.": ".$error_message."<br />";
}
```

## <a name="next-steps"></a><span data-ttu-id="341a1-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="341a1-163">Next steps</span></span>
<span data-ttu-id="341a1-164">A questo punto, dopo aver appreso le nozioni di base del servizio BLOB di Azure, usare i collegamenti seguenti per altre informazioni su attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="341a1-164">Now that you've learned the basics of the Azure blob service, follow these links to learn about more complex storage tasks.</span></span>

* <span data-ttu-id="341a1-165">[Blog del team di Archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="341a1-165">Visit the [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="341a1-166">Vedere l' [esempio PHP relativo al BLOB in blocchi](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="341a1-166">See the [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="341a1-167">Vedere l' [esempio PHP relativo al BLOB di pagine](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="341a1-167">See the [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="341a1-168">Trasferire dati con l'utilità della riga di comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="341a1-168">Transfer data with the AzCopy Command-Line Utility</span></span>](storage-use-azcopy.md)

<span data-ttu-id="341a1-169">Per ulteriori informazioni, vedere anche il [Centro per sviluppatori di PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="341a1-169">For more information, see also the [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
<span data-ttu-id="341a1-170">[require_once]: http://php.net/require_once</span><span class="sxs-lookup"><span data-stu-id="341a1-170">[require_once]: http://php.net/require_once</span></span>
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
