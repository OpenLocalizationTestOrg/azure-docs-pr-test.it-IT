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
ms.openlocfilehash: 331405e583c17c4f71acacdc0078b2bc71efbef0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-php"></a>Toouse come blob di archiviazione da PHP
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-try-azure-tools-queues](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Panoramica
Archiviazione Blob di Azure è un servizio che archivia i dati non strutturati nel cloud hello come oggetti/BLOB. Archivio BLOB può archiviare qualsiasi tipo di dati di testo o binari, ad esempio un documento, un file multimediale o un programma di installazione di un'applicazione. Archiviazione BLOB è anche archiviazione di oggetti di cui viene fatto riferimento tooas.

Questa guida viene illustrato come gli scenari comuni di tooperform utilizzando hello Azure servizio blob. esempi di Hello sono scritti in PHP e utilizzare hello [Azure SDK per PHP][download]. Hello scenari trattati includono **caricamento**, **elenco**, **download**, e **eliminazione** BLOB. Per ulteriori informazioni sui blob, vedere hello [passaggi successivi](#next-steps) sezione.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-php-application"></a>Creare un'applicazione PHP
Hello solo requisito per la creazione di un'applicazione PHP che accede al servizio blob di Azure hello è hello che fanno riferimento a delle classi in hello Azure SDK per PHP all'interno del codice. È possibile utilizzare qualsiasi toocreate di strumenti di sviluppo dell'applicazione, inclusi il blocco note.

In questa guida si useranno le funzionalità del servizio che possono essere chiamate in un'applicazione PHP in locale o nel codice in esecuzione in un ruolo Web, in un ruolo di lavoro o in un sito Web di Azure.

## <a name="get-hello-azure-client-libraries"></a>Recuperare le librerie Client di hello Azure
[!INCLUDE [get-client-libraries](../../includes/get-client-libraries.md)]

## <a name="configure-your-application-tooaccess-hello-blob-service"></a>Configurare il servizio di applicazione tooaccess hello blob
toouse hello Azure API del servizio blob, è necessario:

1. File di riferimento autoloader hello utilizzando hello [require_once] istruzione, e
2. Fare riferimento a tutte le eventuali classi utilizzabili.

Hello esempio seguente viene illustrato come tooinclude hello hello di file e riferimento autoloader **ServicesBuilder** classe.

> [!NOTE]
> esempi di Hello in questo articolo presuppongono installate le librerie Client di PHP per Azure tramite Composer hello. Se le librerie di hello è stato installato manualmente, è necessario tooreference hello `WindowsAzure.php` autoloader file.
>
>

```php
require_once 'vendor/autoload.php';
use WindowsAzure\Common\ServicesBuilder;
```

Negli esempi di hello riportato di seguito, hello `require_once` istruzione verrà sempre visualizzata, ma solo hello classi necessarie per tooexecute esempio hello viene fatto riferimento.

## <a name="set-up-an-azure-storage-connection"></a>Configurare una connessione di archiviazione di Azure
tooinstantiate un client del servizio blob di Azure, è innanzitutto necessario una stringa di connessione valido. formato stringa di connessione del servizio blob hello Hello è:

Per accedere a un servizio attivo:

```php
DefaultEndpointsProtocol=[http|https];AccountName=[yourAccount];AccountKey=[yourKey]
```

Per l'accesso a emulatore di archiviazione hello:

```php
UseDevelopmentStorage=true
```

toocreate qualsiasi client del servizio di Azure, è necessario hello toouse **ServicesBuilder** classe. È possibile:

* Passare la connessione hello stringa direttamente tooit o
* Hello utilizzare **CloudConfigurationManager (CCM)** toocheck origini dati esterne di più origini per la stringa di connessione hello:
  * per impostazione predefinita viene fornito con il supporto per un'origine esterna - ovvero le variabili ambientali
  * È possibile aggiungere nuove origini estendendo hello **ConnectionStringSource** classe.

Per esempi di hello descritti di seguito, la stringa di connessione hello verrà passata direttamente.

```php
require_once 'vendor/autoload.php';

use WindowsAzure\Common\ServicesBuilder;

$blobRestProxy = ServicesBuilder::getInstance()->createBlobService($connectionString);
```

## <a name="create-a-container"></a>Creare un contenitore
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Oggetto **BlobRestProxy** oggetto consente di creare un contenitore blob con hello **createContainer** metodo. Quando si crea un contenitore, è possibile impostare opzioni di contenitore hello, ma non è necessario. (esempio di hello seguente mostra come contenitore hello tooset accesso (ACL) di elenco di controllo e i metadati del contenitore).

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

La chiamata **setPublicAccess (PublicAccessType::CONTAINER\_AND\_BLOB)** rende hello dati blob e contenitore accessibili tramite richieste anonime. Con la chiamata a **setPublicAccess(PublicAccessType::BLOBS_ONLY)**, invece, solo i dati BLOB diventano accessibili tramite richieste anonime. Per altre informazioni sugli ACL contenitore, vedere [Set container ACL (REST API)][container-acl] (Configurare ACL contenitore - API REST).

Per altre informazioni sui codici errore del servizio BLOB, vedere [Blob Service Error Codes][error-codes] (Codici errore del servizio BLOB).

## <a name="upload-a-blob-into-a-container"></a>Caricare un BLOB in un contenitore
un file come un blob, utilizzare hello tooupload **BlobRestProxy -> createBlockBlob** metodo. Se non esiste o lo sovrascrive in caso affermativo, questa operazione crea blob hello. Hello esempio di codice seguente presuppone che tale contenitore hello è già stato creato e Usa [fopen] [ fopen] file hello tooopen come flusso.

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

Si noti che hello precedente esempio carica un blob come un flusso. Tuttavia, un blob può essere caricato anche sotto forma di stringa, ad esempio, tramite hello [file\_ottenere\_contenuto] [ file_get_contents] (funzione). toodo questo hello precedente esempio, impostare `$content = fopen("c:\myfile.txt", "r");` troppo`$content = file_get_contents("c:\myfile.txt");`.

## <a name="list-hello-blobs-in-a-container"></a>Elenco di BLOB hello in un contenitore
BLOB di hello toolist in un contenitore, usare hello **BlobRestProxy -> listBlobs** metodo con un **foreach** ciclo tooloop attraverso il risultato di hello. Hello codice riportato di seguito Visualizza nome hello di ciascun blob come output in un contenitore e il browser toohello URI.

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

## <a name="download-a-blob"></a>Scaricare un BLOB
toodownload un blob, chiamata hello **BlobRestProxy -> getBlob** (metodo), quindi chiamata hello **getContentStream** metodo hello risultante **GetBlobResult** oggetto.

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

Si noti che esempio hello precedente Ottiene un blob come una risorsa di flusso (comportamento predefinito di hello). Tuttavia, è possibile utilizzare hello [flusso\_ottenere\_contenuto] [ stream-get-contents] hello tooconvert funzione ha restituito una stringa tooa di flusso.

## <a name="delete-a-blob"></a>Eliminare un BLOB
toodelete un blob, passare il nome di contenitore hello e il nome di blob troppo**BlobRestProxy -> deleteBlob**.

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

## <a name="delete-a-blob-container"></a>Eliminare un contenitore BLOB
Infine, toodelete un contenitore blob, passare il nome di contenitore hello troppo**BlobRestProxy -> deleteContainer**.

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

## <a name="next-steps"></a>Passaggi successivi
Ora che si è appreso i concetti di base di hello di hello servizio blob di Azure, seguire questi toolearn collegamenti sulle attività di archiviazione più complesse.

* Visitare hello [blog del team di archiviazione di Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* Vedere hello [esempio blob di blocco PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/BlockBlobExample.php).
* Vedere hello [esempio blob di pagina PHP](https://github.com/WindowsAzure/azure-sdk-for-php-samples/blob/master/storage/PageBlobExample.php).
* [Trasferimento dati con l'utilità della riga di comando di AzCopy hello](storage-use-azcopy.md)

Per ulteriori informazioni, vedere anche hello [Centro sviluppatori PHP](/develop/php/).

[download]: http://go.microsoft.com/fwlink/?LinkID=252473
[container-acl]: http://msdn.microsoft.com/library/azure/dd179391.aspx
[error-codes]: http://msdn.microsoft.com/library/azure/dd179439.aspx
[file_get_contents]: http://php.net/file_get_contents
[require_once]: http://php.net/require_once
[fopen]: http://www.php.net/fopen
[stream-get-contents]: http://www.php.net/stream_get_contents
