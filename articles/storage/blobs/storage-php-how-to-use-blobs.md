---
title: aaaHow toouse blob archiviazione (oggetto) da PHP | Documenti Microsoft
description: Archiviare dati non strutturati nel cloud hello con archiviazione Blob di Azure (archiviazione di oggetti).
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
ms.openlocfilehash: 2e77415519b38007652e3ea372da531b3a97c5d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a><span data-ttu-id="42655-103">Toouse come blob di archiviazione da PHP</span><span class="sxs-lookup"><span data-stu-id="42655-103">How toouse blob storage from PHP</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a><span data-ttu-id="42655-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="42655-104">Overview</span></span>
<span data-ttu-id="42655-105">Archiviazione Blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB.</span><span class="sxs-lookup"><span data-stu-id="42655-105">Azure Blob storage is a service that stores unstructured data in hello cloud as objects/blobs.</span></span> <span data-ttu-id="42655-106">Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione.</span><span class="sxs-lookup"><span data-stu-id="42655-106">Blob storage can store any type of text or binary data, such as a document, media file, or application installer.</span></span> <span data-ttu-id="42655-107">Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.</span><span class="sxs-lookup"><span data-stu-id="42655-107">Blob storage is also referred tooas object storage.</span></span>

<span data-ttu-id="42655-108">Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello Azure servizio blob.</span><span class="sxs-lookup"><span data-stu-id="42655-108">This guide shows you how tooperform common scenarios using hello Azure blob service.</span></span> <span data-ttu-id="42655-109">esempi di Hello sono scritti in PHP e utilizzare hello [Azure SDK per PHP][download].</span><span class="sxs-lookup"><span data-stu-id="42655-109">hello samples are written in PHP and use hello [Azure SDK for PHP][download].</span></span> <span data-ttu-id="42655-110">Hello scenari trattati includono **caricamento**, **elenco**, **download**, e **eliminazione** BLOB.</span><span class="sxs-lookup"><span data-stu-id="42655-110">hello scenarios covered include **uploading**, **listing**, **downloading**, and **deleting** blobs.</span></span> <span data-ttu-id="42655-111">Per ulteriori informazioni sui blob, vedere hello [passaggi successivi](#next-steps) sezione.</span><span class="sxs-lookup"><span data-stu-id="42655-111">For more information on blobs, see hello [Next steps](#next-steps) section.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a><span data-ttu-id="42655-112">Creare un'applicazione PHP</span><span class="sxs-lookup"><span data-stu-id="42655-112">Create a PHP application</span></span>
<span data-ttu-id="42655-113">Hello solo requisito per la creazione di un'applicazione PHP che accede al servizio blob di Azure hello è hello che fanno riferimento a delle classi in hello Azure SDK per PHP all'interno del codice.</span><span class="sxs-lookup"><span data-stu-id="42655-113">hello only requirement for creating a PHP application that accesses hello Azure blob service is hello referencing of classes in hello Azure SDK for PHP from within your code.</span></span> <span data-ttu-id="42655-114">È possibile utilizzare qualsiasi toocreate di strumenti di sviluppo dell'applicazione, inclusi il blocco note.</span><span class="sxs-lookup"><span data-stu-id="42655-114">You can use any development tools toocreate your application, including Notepad.</span></span>

<span data-ttu-id="42655-115">In questa guida si useranno le funzionalità del servizio che possono essere chiamate in un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="42655-115">In this guide, you use service features, which can be called within a PHP application locally or in code running within an Azure web role, worker role, or website.</span></span>

## <a name="get-hello-azure-client-libraries"></a><span data-ttu-id="42655-116">Recuperare le librerie Client di hello Azure</span><span class="sxs-lookup"><span data-stu-id="42655-116">Get hello Azure Client Libraries</span></span>
[!INCLUDE [get-client-libraries](../../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a><span data-ttu-id="42655-117">Configurare il servizio di applicazione tooaccess hello blob</span><span class="sxs-lookup"><span data-stu-id="42655-117">Configure your application tooaccess hello blob service</span></span>
<span data-ttu-id="42655-118">toouse hello Azure API del servizio blob, è necessario:</span><span class="sxs-lookup"><span data-stu-id="42655-118">toouse hello Azure blob service APIs, you need to:</span></span>

1. <span data-ttu-id="42655-119">File di riferimento autoloader hello utilizzando hello [require_once] istruzione, e</span><span class="sxs-lookup"><span data-stu-id="42655-119">Reference hello autoloader file using hello [require_once] statement, and</span></span>
2. <span data-ttu-id="42655-120">Fare riferimento a tutte le eventuali classi utilizzabili.</span><span class="sxs-lookup"><span data-stu-id="42655-120">Reference any classes you might use.</span></span>

<span data-ttu-id="42655-121">Hello esempio seguente viene illustrato come tooinclude hello hello di file e riferimento autoloader **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="42655-121">hello following example shows how tooinclude hello autoloader file and reference hello **ServicesBuilder** class.</span></span>

> [!NOTE]
> <span data-ttu-id="42655-122">esempi di Hello in questo articolo presuppongono installate le librerie Client di PHP per Azure tramite Composer hello.</span><span class="sxs-lookup"><span data-stu-id="42655-122">hello examples in this article assume you have installed hello PHP Client Libraries for Azure via Composer.</span></span> <span data-ttu-id="42655-123">Se le librerie di hello è stato installato manualmente, è necessario tooreference hello `WindowsAzure.php` autoloader file.</span><span class="sxs-lookup"><span data-stu-id="42655-123">If you installed hello libraries manually, you need tooreference hello `WindowsAzure.php` autoloader file.</span></span>
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

<span data-ttu-id="42655-124">Negli esempi di hello riportato di seguito, hello `require_once` istruzione verrà sempre visualizzata, ma solo hello classi necessarie per tooexecute esempio hello viene fatto riferimento.</span><span class="sxs-lookup"><span data-stu-id="42655-124">In hello examples below, hello `require_once` statement will be shown always, but only hello classes necessary for hello example tooexecute are referenced.</span></span>

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="42655-125">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="42655-125">Set up an Azure storage connection</span></span>
<span data-ttu-id="42655-126">tooinstantiate un client del servizio blob di Azure, è innanzitutto necessario una stringa di connessione valido.</span><span class="sxs-lookup"><span data-stu-id="42655-126">tooinstantiate an Azure blob service client, you must first have a valid connection string.</span></span> <span data-ttu-id="42655-127">formato stringa di connessione del servizio blob hello Hello è:</span><span class="sxs-lookup"><span data-stu-id="42655-127">hello format for hello blob service connection string is:</span></span>

<span data-ttu-id="42655-128">Per accedere a un servizio attivo:</span><span class="sxs-lookup"><span data-stu-id="42655-128">For accessing a live service:</span></span>

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

<span data-ttu-id="42655-129">Per l'accesso a emulatore di archiviazione hello:</span><span class="sxs-lookup"><span data-stu-id="42655-129">For accessing hello storage emulator:</span></span>

```php
UseDevelopmentStorage=true
```

<span data-ttu-id="42655-130">toocreate qualsiasi client del servizio di Azure, è necessario hello toouse **ServicesBuilder** classe.</span><span class="sxs-lookup"><span data-stu-id="42655-130">toocreate any Azure service client, you need toouse hello **ServicesBuilder** class.</span></span> <span data-ttu-id="42655-131">È possibile:</span><span class="sxs-lookup"><span data-stu-id="42655-131">You can:</span></span>

* <span data-ttu-id="42655-132">Passare la connessione hello stringa direttamente tooit o</span><span class="sxs-lookup"><span data-stu-id="42655-132">Pass hello connection string directly tooit or</span></span>
* <span data-ttu-id="42655-133">Hello utilizzare **CloudConfigurationManager (CCM)** toocheck origini dati esterne di più origini per la stringa di connessione hello:</span><span class="sxs-lookup"><span data-stu-id="42655-133">Use hello **CloudConfigurationManager (CCM)** toocheck multiple external sources for hello connection string:</span></span>
  * <span data-ttu-id="42655-134">per impostazione predefinita viene fornito con il supporto per un'origine esterna - ovvero le variabili ambientali</span><span class="sxs-lookup"><span data-stu-id="42655-134">By default, it comes with support for one external source - environmental variables.</span></span>
  * <span data-ttu-id="42655-135">È possibile aggiungere nuove origini estendendo hello **ConnectionStringSource** classe.</span><span class="sxs-lookup"><span data-stu-id="42655-135">You can add new sources by extending hello **ConnectionStringSource** class.</span></span>

<span data-ttu-id="42655-136">Per esempi di hello descritti di seguito, la stringa di connessione hello verrà passata direttamente.</span><span class="sxs-lookup"><span data-stu-id="42655-136">For hello examples outlined here, hello connection string will be passed directly.</span></span>

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a><span data-ttu-id="42655-137">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="42655-137">Create a container</span></span>
[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="42655-138">Oggetto **BlobRestProxy** oggetto consente di creare un contenitore blob con hello **createContainer** metodo.</span><span class="sxs-lookup"><span data-stu-id="42655-138">A **BlobRestProxy** object lets you create a blob container with hello **createContainer** method.</span></span> <span data-ttu-id="42655-139">Quando si crea un contenitore, è possibile impostare opzioni di contenitore hello, ma non è necessario.</span><span class="sxs-lookup"><span data-stu-id="42655-139">When creating a container, you can set options on hello container, but doing so is not required.</span></span> <span data-ttu-id="42655-140">(esempio di hello seguente mostra come contenitore hello tooset accesso (ACL) di elenco di controllo e i metadati del contenitore).</span><span class="sxs-lookup"><span data-stu-id="42655-140">(hello example below shows how tooset hello container access control list (ACL) and container metadata.)</span></span>

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
// proxys can enumerate blobs within hello container via anonymous
// request, but cannot enumerate containers within hello storage account.
//
// BLOBS_ONLY:
// Specifies public read access for blobs. Blob data within this
// container can be read via anonymous request, but container data is not
// available. proxys cannot enumerate blobs within hello container via
// anonymous request.
// If this value is not specified in hello request, container data is
// private toohello account owner.
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

<span data-ttu-id="42655-141">La chiamata **setPublicAccess (PublicAccessType::CONTAINER\_AND\_BLOB)** rende hello dati blob e contenitore accessibili tramite richieste anonime.</span><span class="sxs-lookup"><span data-stu-id="42655-141">Calling **setPublicAccess(PublicAccessType::CONTAINER\_AND\_BLOBS)** makes hello container and blob data accessible via anonymous requests.</span></span> <span data-ttu-id="42655-142">Con la chiamata a **setPublicAccess(PublicAccessType::BLOBS_ONLY)**, invece, solo i dati BLOB diventano accessibili tramite richieste anonime.</span><span class="sxs-lookup"><span data-stu-id="42655-142">Calling **setPublicAccess(PublicAccessType::BLOBS_ONLY)** makes only blob data accessible via anonymous requests.</span></span> <span data-ttu-id="42655-143">Per altre informazioni sugli ACL contenitore, vedere [Set container ACL (REST API)][container-acl] (Configurare ACL contenitore - API REST).</span><span class="sxs-lookup"><span data-stu-id="42655-143">For more information about container ACLs, see [Set container ACL (REST API)][container-acl].</span></span>

<span data-ttu-id="42655-144">Per altre informazioni sui codici errore del servizio BLOB, vedere [Blob Service Error Codes][error-codes] (Codici errore del servizio BLOB).</span><span class="sxs-lookup"><span data-stu-id="42655-144">For more information about Blob service error codes, see [Blob Service Error Codes][error-codes].</span></span>

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="42655-145">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="42655-145">Upload a blob into a container</span></span>
<span data-ttu-id="42655-146">un file come un blob, utilizzare hello tooupload **BlobRestProxy -> createBlockBlob** metodo.</span><span class="sxs-lookup"><span data-stu-id="42655-146">tooupload a file as a blob, use hello **BlobRestProxy->createBlockBlob** method.</span></span> <span data-ttu-id="42655-147">Se non esiste o lo sovrascrive in caso affermativo, questa operazione crea blob hello.</span><span class="sxs-lookup"><span data-stu-id="42655-147">This operation creates hello blob if it doesn't exist, or overwrites it if it does.</span></span> <span data-ttu-id="42655-148">Hello esempio di codice seguente presuppone che tale contenitore hello è già stato creato e Usa [fopen] [ fopen] file hello tooopen come flusso.</span><span class="sxs-lookup"><span data-stu-id="42655-148">hello code example below assumes that hello container has already been created and uses [fopen][fopen] tooopen hello file as a stream.</span></span>

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

<span data-ttu-id="42655-149">Si noti che hello precedente esempio carica un blob come un flusso.</span><span class="sxs-lookup"><span data-stu-id="42655-149">Note that hello previous sample uploads a blob as a stream.</span></span> <span data-ttu-id="42655-150">Tuttavia, un blob può essere caricato anche sotto forma di stringa, ad esempio, tramite hello [file\_ottenere\_contenuto] [ file_get_contents] (funzione).</span><span class="sxs-lookup"><span data-stu-id="42655-150">However, a blob can also be uploaded as a string using, for example, hello [file\_get\_contents][file_get_contents] function.</span></span> <span data-ttu-id="42655-151">toodo questo hello precedente esempio, impostare `$content = fopen("c:\myfile.txt", "r");` troppo`$content = file_get_contents("c:\myfile.txt");`.</span><span class="sxs-lookup"><span data-stu-id="42655-151">toodo this using hello previous sample, change `$content = fopen("c:\myfile.txt", "r");` too`$content = file_get_contents("c:\myfile.txt");`.</span></span>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="42655-152">Elenco di BLOB hello in un contenitore</span><span class="sxs-lookup"><span data-stu-id="42655-152">List hello blobs in a container</span></span>
<span data-ttu-id="42655-153">BLOB di hello toolist in un contenitore, usare hello **BlobRestProxy -> listBlobs** metodo con un **foreach** ciclo tooloop attraverso il risultato di hello.</span><span class="sxs-lookup"><span data-stu-id="42655-153">toolist hello blobs in a container, use hello **BlobRestProxy->listBlobs** method with a **foreach** loop tooloop through hello result.</span></span> <span data-ttu-id="42655-154">Hello codice riportato di seguito Visualizza nome hello di ciascun blob come output in un contenitore e il browser toohello URI.</span><span class="sxs-lookup"><span data-stu-id="42655-154">hello following code displays hello name of each blob as output in a container and displays its URI toohello browser.</span></span>

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

## <a name="download-a-blob"></a><span data-ttu-id="42655-155">Scaricare un BLOB</span><span class="sxs-lookup"><span data-stu-id="42655-155">Download a blob</span></span>
<span data-ttu-id="42655-156">toodownload un blob, chiamata hello **BlobRestProxy -> getBlob** (metodo), quindi chiamata hello **getContentStream** metodo hello risultante **GetBlobResult** oggetto.</span><span class="sxs-lookup"><span data-stu-id="42655-156">toodownload a blob, call hello **BlobRestProxy->getBlob** method, then call hello **getContentStream** method on hello resulting **GetBlobResult** object.</span></span>

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

<span data-ttu-id="42655-157">Si noti che esempio hello precedente Ottiene un blob come una risorsa di flusso (comportamento predefinito di hello).</span><span class="sxs-lookup"><span data-stu-id="42655-157">Note that hello example above gets a blob as a stream resource (hello default behavior).</span></span> <span data-ttu-id="42655-158">Tuttavia, è possibile utilizzare hello [flusso\_ottenere\_contenuto] [ stream-get-contents] hello tooconvert funzione ha restituito una stringa tooa di flusso.</span><span class="sxs-lookup"><span data-stu-id="42655-158">However, you can use hello [stream\_get\_contents][stream-get-contents] function tooconvert hello returned stream tooa string.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="42655-159">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="42655-159">Delete a blob</span></span>
<span data-ttu-id="42655-160">toodelete un blob, passare il nome di contenitore hello e il nome di blob troppo**BlobRestProxy -> deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="42655-160">toodelete a blob, pass hello container name and blob name too**BlobRestProxy->deleteBlob**.</span></span>

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

## <a name="delete-a-blob-container"></a><span data-ttu-id="42655-161">Eliminare un contenitore BLOB</span><span class="sxs-lookup"><span data-stu-id="42655-161">Delete a blob container</span></span>
<span data-ttu-id="42655-162">Infine, toodelete un contenitore blob, passare il nome di contenitore hello troppo**BlobRestProxy -> deleteContainer**.</span><span class="sxs-lookup"><span data-stu-id="42655-162">Finally, toodelete a blob container, pass hello container name too**BlobRestProxy->deleteContainer**.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="42655-163">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="42655-163">Next steps</span></span>
<span data-ttu-id="42655-164">Ora che si è appreso i concetti di base di hello di hello servizio blob di Azure, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.</span><span class="sxs-lookup"><span data-stu-id="42655-164">Now that you've learned hello basics of hello Azure blob service, follow these links toolearn about more complex storage tasks.</span></span>

* <span data-ttu-id="42655-165">Visitare hello [blog del team di archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)</span><span class="sxs-lookup"><span data-stu-id="42655-165">Visit hello [Azure Storage team blog](http://blogs.msdn.com/b/windowsazurestorage/)</span></span>
* <span data-ttu-id="42655-166">Vedere hello [esempio blob di blocco PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="42655-166">See hello [PHP block blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).</span></span>
* <span data-ttu-id="42655-167">Vedere hello [esempio blob di pagina PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span><span class="sxs-lookup"><span data-stu-id="42655-167">See hello [PHP page blob example](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).</span></span>
* [<span data-ttu-id="42655-168">Trasferimento dati con l'utilità della riga di comando di AzCopy hello</span><span class="sxs-lookup"><span data-stu-id="42655-168">Transfer data with hello AzCopy Command-Line Utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

<span data-ttu-id="42655-169">Per ulteriori informazioni, vedere anche hello [Centro sviluppatori PHP](/develop/php/).</span><span class="sxs-lookup"><span data-stu-id="42655-169">For more information, see also hello [PHP Developer Center](/develop/php/).</span></span>

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
