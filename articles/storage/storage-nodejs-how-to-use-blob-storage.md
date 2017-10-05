---
title: Come usare l'archiviazione BLOB da Node.js | Microsoft Docs
description: Archiviare i dati non strutturati nel cloud con l'archivio BLOB (archivio di oggetti) di Azure.
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 8b0df222-1ca8-4967-8248-6d6d720947b8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: 38c3fd3cd271c3f9d60c44fff17715062b4979ae
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-use-blob-storage-from-nodejs"></a><span data-ttu-id="15daa-103">Come usare l'archiviazione BLOB da Node.js</span><span class="sxs-lookup"><span data-stu-id="15daa-103">How to use Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="15daa-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="15daa-104">Overview</span></span>
<span data-ttu-id="15daa-105">Questo articolo illustra scenari comuni relativi all'uso dell'archiviazione BLOB.</span><span class="sxs-lookup"><span data-stu-id="15daa-105">This article shows you how to perform common scenarios using Blob storage.</span></span> <span data-ttu-id="15daa-106">Gli esempi sono scritti usando l'API Node.js.</span><span class="sxs-lookup"><span data-stu-id="15daa-106">The samples are written via the Node.js API.</span></span> <span data-ttu-id="15daa-107">Gli scenari presentati illustrano come caricare, elencare, scaricare ed eliminare i BLOB.</span><span class="sxs-lookup"><span data-stu-id="15daa-107">The scenarios covered include how to upload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="15daa-108">Creare un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="15daa-108">Create a Node.js application</span></span>
<span data-ttu-id="15daa-109">Per istruzioni su come creare un'applicazione Node.js, vedere [Creare un'app Web Node.js nel servizio app di Azure], [Creazione e distribuzione di un'applicazione Node.js a un servizio cloud di Azure] -- con Windows PowerShell, o [Creazione e distribuzione di un sito Web Node.js in Azure con WebMatrix].</span><span class="sxs-lookup"><span data-stu-id="15daa-109">For instructions on how to create a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application to an Azure Cloud Service] -- using Windows PowerShell, or [Build and deploy a Node.js web app to Azure using Web Matrix].</span></span>

## <a name="configure-your-application-to-access-storage"></a><span data-ttu-id="15daa-110">Configurare l'applicazione per l'accesso all'archiviazione</span><span class="sxs-lookup"><span data-stu-id="15daa-110">Configure your application to access storage</span></span>
<span data-ttu-id="15daa-111">Per usare Archiviazione di Azure, è necessario disporre di Azure Storage SDK per Node.js, che comprende un set di pratiche librerie che comunicano con i servizi di archiviazione REST.</span><span class="sxs-lookup"><span data-stu-id="15daa-111">To use Azure storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-obtain-the-package"></a><span data-ttu-id="15daa-112">Usare Node Package Manager (NPM) per ottenere il pacchetto</span><span class="sxs-lookup"><span data-stu-id="15daa-112">Use Node Package Manager (NPM) to obtain the package</span></span>
1. <span data-ttu-id="15daa-113">Usare un'interfaccia della riga di comando come **PowerShell** (Windows), **Terminal** (Mac) o **Bash** (Unix) per spostarsi nella cartella in cui è stata creata l'applicazione di esempio.</span><span class="sxs-lookup"><span data-stu-id="15daa-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), to navigate to the folder where you created your sample application.</span></span>
2. <span data-ttu-id="15daa-114">Digitare **npm install azure-storage** nella finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="15daa-114">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="15daa-115">L'output da questo comando sarà simile all'esempio di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="15daa-115">Output from the command is similar to the following code example.</span></span>

        azure-storage@0.5.0 node_modules\azure-storage
        +-- extend@1.2.1
        +-- xmlbuilder@0.4.3
        +-- mime@1.2.11
        +-- node-uuid@1.4.3
        +-- validator@3.22.2
        +-- underscore@1.4.4
        +-- readable-stream@1.0.33 (string_decoder@0.10.31, isarray@0.0.1, inherits@2.0.1, core-util-is@1.0.1)
        +-- xml2js@0.2.7 (sax@0.5.2)
        +-- request@2.57.0 (caseless@0.10.0, aws-sign2@0.5.0, forever-agent@0.6.1, stringstream@0.0.4, oauth-sign@0.8.0, tunnel-agent@0.4.1, isstream@0.1.2, json-stringify-safe@5.0.1, bl@0.9.4, combined-stream@1.0.5, qs@3.1.0, mime-types@2.0.14, form-data@0.2.0, http-signature@0.11.0, tough-cookie@2.0.0, hawk@2.3.1, har-validator@1.8.0)
3. <span data-ttu-id="15daa-116">È possibile eseguire manualmente il comando **ls** per verificare che sia stata creata una cartella **node\_modules**.</span><span class="sxs-lookup"><span data-stu-id="15daa-116">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="15daa-117">All'interno di tale cartella trovare il pacchetto **azure-storage** , che contiene le librerie necessarie per accedere all'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="15daa-117">Inside that folder, find the **azure-storage** package, which contains the libraries that you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="15daa-118">Importare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="15daa-118">Import the package</span></span>
<span data-ttu-id="15daa-119">Usando il Blocco note o un altro editor di testo, aggiungere quanto segue alla parte superiore del file **server.js** dell'applicazione in cui si intende usare l'archiviazione:</span><span class="sxs-lookup"><span data-stu-id="15daa-119">Using Notepad or another text editor, add the following to the top of the **server.js** file of the application where you intend to use storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="15daa-120">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="15daa-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="15daa-121">Il modulo di Azure leggerà le variabili di ambiente `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY` o `AZURE_STORAGE_CONNECTION_STRING` per ottenere le informazioni necessarie per la connessione all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="15daa-121">The Azure module will read the environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="15daa-122">Se queste variabili di ambiente non sono impostate, sarà necessario specificare le informazioni relative all'account quando si chiama **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="15daa-122">If these environment variables are not set, you must specify the account information when calling **createBlobService**.</span></span>

<span data-ttu-id="15daa-123">Per un esempio di impostazione delle variabili di ambiente nel [portale di Azure](https://portal.azure.com) per un'app Web di Azure, vedere [App Web Node.js con il servizio tabelle di Azure].</span><span class="sxs-lookup"><span data-stu-id="15daa-123">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using the Azure Table Service].</span></span>

## <a name="create-a-container"></a><span data-ttu-id="15daa-124">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="15daa-124">Create a container</span></span>
<span data-ttu-id="15daa-125">L'oggetto **BlobService** consente di lavorare con contenitori e BLOB.</span><span class="sxs-lookup"><span data-stu-id="15daa-125">The **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="15daa-126">Il codice seguente consente di creare un oggetto **BlobService** .</span><span class="sxs-lookup"><span data-stu-id="15daa-126">The following code creates a **BlobService** object.</span></span> <span data-ttu-id="15daa-127">Aggiungere il codice seguente nella parte superiore di **server.js**:</span><span class="sxs-lookup"><span data-stu-id="15daa-127">Add the following near the top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="15daa-128">È possibile accedere a un BLOB in modo anonimo usando **createBlobServiceAnonymous** e specificando l'indirizzo host.</span><span class="sxs-lookup"><span data-stu-id="15daa-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing the host address.</span></span> <span data-ttu-id="15daa-129">Ad esempio, usare `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="15daa-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="15daa-130">Per creare un nuovo contenitore, usare **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="15daa-130">To create a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="15daa-131">L'esempio di codice seguente crea un nuovo contenitore denominato "mycontainer":</span><span class="sxs-lookup"><span data-stu-id="15daa-131">The following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="15daa-132">Se il contenitore viene creato, `result.created` è true.</span><span class="sxs-lookup"><span data-stu-id="15daa-132">If the container is newly created, `result.created` is true.</span></span> <span data-ttu-id="15daa-133">Se il contenitore esiste già, `result.created` è false.</span><span class="sxs-lookup"><span data-stu-id="15daa-133">If the container already exists, `result.created` is false.</span></span> <span data-ttu-id="15daa-134">`response` contiene informazioni sull'operazione, incluse le informazioni sull'ETag per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="15daa-134">`response` contains information about the operation, including the ETag information for the container.</span></span>

### <a name="container-security"></a><span data-ttu-id="15daa-135">Sicurezza del contenitore</span><span class="sxs-lookup"><span data-stu-id="15daa-135">Container security</span></span>
<span data-ttu-id="15daa-136">Per impostazione predefinita, i nuovi contenitori sono privati e non è possibile accedervi in modo anonimo.</span><span class="sxs-lookup"><span data-stu-id="15daa-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="15daa-137">Per rendere pubblico il contenitore affinché sia accessibile in modo anonimo, è possibile impostarne il livello di accesso su **blob** o **container**.</span><span class="sxs-lookup"><span data-stu-id="15daa-137">To make the container public so that you can access it anonymously, you can set the container's access level to **blob** or **container**.</span></span>

* <span data-ttu-id="15daa-138">**blob** consente l'accesso anonimo in lettura al contenuto e ai metadati del BLOB all'interno di quel contenitore, ma non ai metadati del contenitore, ad esempio l'elenco di tutti i BLOB all'interno di un contenitore.</span><span class="sxs-lookup"><span data-stu-id="15daa-138">**blob** - allows anonymous read access to blob content and metadata within this container, but not to container metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="15daa-139">**container** consente l'accesso anonimo in lettura al contenuto e ai metadati del BLOB, nonché ai metadati del contenitore.</span><span class="sxs-lookup"><span data-stu-id="15daa-139">**container** - allows anonymous read access to blob content and metadata as well as container metadata</span></span>

<span data-ttu-id="15daa-140">L'esempio di codice seguente illustra l'impostazione del livello di accesso su **blob**:</span><span class="sxs-lookup"><span data-stu-id="15daa-140">The following code example demonstrates setting the access level to **blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access to blob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="15daa-141">In alternativa, è possibile modificare il livello di accesso di un contenitore usando **setContainerAcl** per specificare il livello di accesso.</span><span class="sxs-lookup"><span data-stu-id="15daa-141">Alternatively, you can modify the access level of a container by using **setContainerAcl** to specify the access level.</span></span> <span data-ttu-id="15daa-142">L'esempio di codice seguente illustra la modifica del livello di accesso al contenitore:</span><span class="sxs-lookup"><span data-stu-id="15daa-142">The following code example changes the access level to container:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set to 'container'
  }
});
```

<span data-ttu-id="15daa-143">Il risultato contiene informazioni sull'operazione, incluso l' **ETag** corrente per il contenitore.</span><span class="sxs-lookup"><span data-stu-id="15daa-143">The result contains information about the operation, including the current **ETag** for the container.</span></span>

### <a name="filters"></a><span data-ttu-id="15daa-144">Filtri</span><span class="sxs-lookup"><span data-stu-id="15daa-144">Filters</span></span>
<span data-ttu-id="15daa-145">È possibile applicare operazioni di filtro facoltative alle operazioni eseguite usando **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="15daa-145">You can apply optional filtering operations to operations performed using **BlobService**.</span></span> <span data-ttu-id="15daa-146">Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con la firma:</span><span class="sxs-lookup"><span data-stu-id="15daa-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="15daa-147">Dopo aver eseguito la pre-elaborazione sulle opzioni della richiesta, il metodo deve chiamare "next" passando un callback con la firma seguente:</span><span class="sxs-lookup"><span data-stu-id="15daa-147">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="15daa-148">In questo callback, e dopo l'elaborazione del returnObject (la risposta della richiesta al server), il callback deve richiamare "next", se questo esiste, per continuare a elaborare altri filtri oppure semplicemente richiamare finalCallback per concludere la chiamata al servizio.</span><span class="sxs-lookup"><span data-stu-id="15daa-148">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback to end the service invocation.</span></span>

<span data-ttu-id="15daa-149">In Azure SDK per Node.js sono inclusi due filtri che implementano la logica di ripetizione dei tentativi. Sono **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="15daa-149">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="15daa-150">Il codice seguente consente di creare un oggetto **BlobService** che usa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="15daa-150">The following creates a **BlobService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="15daa-151">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="15daa-151">Upload a blob into a container</span></span>
<span data-ttu-id="15daa-152">Esistono tre tipi di BLOB: BLOB in blocchi, BLOB di pagine e BLOB di accodamento.</span><span class="sxs-lookup"><span data-stu-id="15daa-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="15daa-153">I BLOB in blocchi consentono di caricare in modo più efficiente dati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="15daa-153">Block blobs allow you to more efficiently upload large data.</span></span> <span data-ttu-id="15daa-154">I BLOB di accodamento sono ottimizzati per le operazioni di accodamento.</span><span class="sxs-lookup"><span data-stu-id="15daa-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="15daa-155">I BLOB di pagine sono ottimizzati per le operazioni di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="15daa-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="15daa-156">Per altre informazioni, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="15daa-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="15daa-157">BLOB in blocchi</span><span class="sxs-lookup"><span data-stu-id="15daa-157">Block blobs</span></span>
<span data-ttu-id="15daa-158">Per caricare i dati in un BLOB in blocchi, usare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="15daa-158">To upload data to a block blob, use the following:</span></span>

* <span data-ttu-id="15daa-159">**createBlockBlobFromLocalFile** : crea un nuovo BLOB in blocchi e carica il contenuto di un file</span><span class="sxs-lookup"><span data-stu-id="15daa-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads the contents of a file</span></span>
* <span data-ttu-id="15daa-160">**createBlockBlobFromStream** : crea un nuovo BLOB in blocchi e carica il contenuto di un flusso</span><span class="sxs-lookup"><span data-stu-id="15daa-160">**createBlockBlobFromStream** - creates a new block blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="15daa-161">**createBlockBlobFromText** : crea un nuovo BLOB in blocchi e carica il contenuti di una stringa</span><span class="sxs-lookup"><span data-stu-id="15daa-161">**createBlockBlobFromText** - creates a new block blob and uploads the contents of a string</span></span>
* <span data-ttu-id="15daa-162">**createWriteStreamToBlockBlob** : fornisce un flusso di scrittura a un BLOB in blocchi</span><span class="sxs-lookup"><span data-stu-id="15daa-162">**createWriteStreamToBlockBlob** - provides a write stream to a block blob</span></span>

<span data-ttu-id="15daa-163">L'esempio di codice seguente carica il contenuto del file **test.txt** nel BLOB **myblob**.</span><span class="sxs-lookup"><span data-stu-id="15daa-163">The following code example uploads the contents of the **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="15daa-164">L'oggetto `result` restituito da questi metodi contiene informazioni sull'operazione, ad esempio l' **ETag** del BLOB.</span><span class="sxs-lookup"><span data-stu-id="15daa-164">The `result` returned by these methods contains information on the operation, such as the **ETag** of the blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="15daa-165">BLOB di accodamento</span><span class="sxs-lookup"><span data-stu-id="15daa-165">Append blobs</span></span>
<span data-ttu-id="15daa-166">Per caricare i dati in un nuovo BLOB di accodamento, usare le API seguenti:</span><span class="sxs-lookup"><span data-stu-id="15daa-166">To upload data to a new append blob, use the following:</span></span>

* <span data-ttu-id="15daa-167">**createAppendBlobFromLocalFile** : crea un nuovo BLOB di accodamento e carica i contenuti di un file</span><span class="sxs-lookup"><span data-stu-id="15daa-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads the contents of a file</span></span>
* <span data-ttu-id="15daa-168">**createAppendBlobFromStream** : crea un nuovo BLOB di accodamento e carica i contenuti di un flusso</span><span class="sxs-lookup"><span data-stu-id="15daa-168">**createAppendBlobFromStream** - creates a new append blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="15daa-169">**createAppendBlobFromText** : crea un nuovo BLOB di accodamento e carica i contenuti di una stringa</span><span class="sxs-lookup"><span data-stu-id="15daa-169">**createAppendBlobFromText** - creates a new append blob and uploads the contents of a string</span></span>
* <span data-ttu-id="15daa-170">**createWriteStreamToNewAppendBlob** : crea un nuovo BLOB di accodamento e quindi fornisce un flusso per la scrittura nel BLOB stesso</span><span class="sxs-lookup"><span data-stu-id="15daa-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream to write to it</span></span>

<span data-ttu-id="15daa-171">L'esempio di codice seguente carica il contenuto del file **test.txt** nel BLOB **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="15daa-171">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="15daa-172">Per accodare un blocco a un blob di accodamento esistente, usare quanto segue:</span><span class="sxs-lookup"><span data-stu-id="15daa-172">To append a block to an existing append blob, use the following:</span></span>

* <span data-ttu-id="15daa-173">**appendFromLocalFile** : consente di accodare i contenuti di un file a un BLOB di accodamento esistente</span><span class="sxs-lookup"><span data-stu-id="15daa-173">**appendFromLocalFile** - append the contents of a file to an existing append blob</span></span>
* <span data-ttu-id="15daa-174">**appendFromStream** : consente di accodare i contenuti di un flusso a un BLOB di accodamento esistente</span><span class="sxs-lookup"><span data-stu-id="15daa-174">**appendFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="15daa-175">**appendFromText** : consente di accodare i contenuti di una stringa a un BLOB di accodamento esistente</span><span class="sxs-lookup"><span data-stu-id="15daa-175">**appendFromText** - append the contents of a string to an existing append blob</span></span>
* <span data-ttu-id="15daa-176">**appendBlockFromStream** : consente di accodare i contenuti di un flusso a un BLOB di accodamento esistente</span><span class="sxs-lookup"><span data-stu-id="15daa-176">**appendBlockFromStream** - append the contents of a stream to an existing append blob</span></span>
* <span data-ttu-id="15daa-177">**appendBlockFromText** : consente di accodare i contenuti di una stringa a un BLOB di accodamento esistente</span><span class="sxs-lookup"><span data-stu-id="15daa-177">**appendBlockFromText** - append the contents of a string to an existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="15daa-178">Le API appendFromXXX consentono di eseguire rapidamente alcune convalide sul lato client per evitare chiamate al server non necessarie,</span><span class="sxs-lookup"><span data-stu-id="15daa-178">appendFromXXX APIs will do some client-side validation to fail fast to avoid unnecessary server calls.</span></span> <span data-ttu-id="15daa-179">contrariamente alle API appendBlockFromXXX.</span><span class="sxs-lookup"><span data-stu-id="15daa-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="15daa-180">L'esempio di codice seguente carica il contenuto del file **test.txt** nel BLOB **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="15daa-180">The following code example uploads the contents of the **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text to be appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="15daa-181">BLOB di pagine</span><span class="sxs-lookup"><span data-stu-id="15daa-181">Page blobs</span></span>
<span data-ttu-id="15daa-182">Per caricare i dati in un BLOB di pagine, usare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="15daa-182">To upload data to a page blob, use the following:</span></span>

* <span data-ttu-id="15daa-183">**createPageBlob** : crea un nuovo BLOB di pagine con una lunghezza specifica</span><span class="sxs-lookup"><span data-stu-id="15daa-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="15daa-184">**createPageBlobFromLocalFile** : crea un nuovo BLOB di pagine e carica i contenuti di un file</span><span class="sxs-lookup"><span data-stu-id="15daa-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads the contents of a file</span></span>
* <span data-ttu-id="15daa-185">**createPageBlobFromStream** : crea un nuovo BLOB di pagine e carica i contenuti di un flusso</span><span class="sxs-lookup"><span data-stu-id="15daa-185">**createPageBlobFromStream** - creates a new page blob and uploads the contents of a stream</span></span>
* <span data-ttu-id="15daa-186">**createWriteStreamToExistingPageBlob** : fornisce un flusso di scrittura a un BLOB di pagine esistente</span><span class="sxs-lookup"><span data-stu-id="15daa-186">**createWriteStreamToExistingPageBlob** - provides a write stream to an existing page blob</span></span>
* <span data-ttu-id="15daa-187">**createWriteStreamToNewPageBlob** : crea un nuovo BLOB di pagine e quindi fornisce un flusso per la scrittura nel BLOB stesso</span><span class="sxs-lookup"><span data-stu-id="15daa-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream to write to it</span></span>

<span data-ttu-id="15daa-188">L'esempio di codice seguente carica il contenuto del file **test.txt** nel BLOB **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="15daa-188">The following code example uploads the contents of the **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="15daa-189">I BLOB di pagine sono costituiti da "pagine" da 512 byte.</span><span class="sxs-lookup"><span data-stu-id="15daa-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="15daa-190">Quando si caricano dati con una dimensione che non corrisponde a un multiplo di 512, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="15daa-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-the-blobs-in-a-container"></a><span data-ttu-id="15daa-191">Elencare i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="15daa-191">List the blobs in a container</span></span>
<span data-ttu-id="15daa-192">Per elencare i BLOB all'interno di un contenitore, usare il metodo **listBlobsSegmented** .</span><span class="sxs-lookup"><span data-stu-id="15daa-192">To list the blobs in a container, use the **listBlobsSegmented** method.</span></span> <span data-ttu-id="15daa-193">Per fare in modo che vengano restituiti i BLOB con un prefisso specifico, usare il metodo **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="15daa-193">If you'd like to return blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains the entries
      // If not all blobs were returned, result.continuationToken has the continuation token.
  }
});
```

<span data-ttu-id="15daa-194">`result` contiene una raccolta di `entries`, ovvero una matrice di oggetti che descrivono ogni BLOB.</span><span class="sxs-lookup"><span data-stu-id="15daa-194">The `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="15daa-195">Se non vengono restituiti tutti i BLOB, `result` fornisce anche un `continuationToken`, che può essere usato come secondo parametro per recuperare voci aggiuntive.</span><span class="sxs-lookup"><span data-stu-id="15daa-195">If all blobs cannot be returned, the `result` also provides a `continuationToken`, which you may use as the second parameter to retrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="15daa-196">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="15daa-196">Download blobs</span></span>
<span data-ttu-id="15daa-197">Per scaricare i dati da un BLOB, usare le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="15daa-197">To download data from a blob, use the following:</span></span>

* <span data-ttu-id="15daa-198">**getBlobToLocalFile** - scrive i contenuti del BLOB in un file.</span><span class="sxs-lookup"><span data-stu-id="15daa-198">**getBlobToLocalFile** - writes the blob contents to file</span></span>
* <span data-ttu-id="15daa-199">**getBlobToStream** : scrive il contenuto del BLOB in un flusso</span><span class="sxs-lookup"><span data-stu-id="15daa-199">**getBlobToStream** - writes the blob contents to a stream</span></span>
* <span data-ttu-id="15daa-200">**getBlobToText** : scrive il contenuto del BLOB in una stringa</span><span class="sxs-lookup"><span data-stu-id="15daa-200">**getBlobToText** - writes the blob contents to a string</span></span>
* <span data-ttu-id="15daa-201">**createReadStream** : fornisce un flusso per la lettura dal BLOB.</span><span class="sxs-lookup"><span data-stu-id="15daa-201">**createReadStream** - provides a stream to read from the blob</span></span>

<span data-ttu-id="15daa-202">L'esempio di codice seguente illustra l'uso di **getBlobToStream** per scaricare il contenuto del BLOB **myblob** e archiviarlo nel file **output.txt** usando un flusso:</span><span class="sxs-lookup"><span data-stu-id="15daa-202">The following code example demonstrates using **getBlobToStream** to download the contents of the **myblob** blob and store it to the **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="15daa-203">`result` contiene informazioni sul BLOB, incluse le informazioni sull' **ETag** .</span><span class="sxs-lookup"><span data-stu-id="15daa-203">The `result` contains information about the blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="15daa-204">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="15daa-204">Delete a blob</span></span>
<span data-ttu-id="15daa-205">Per eliminare un BLOB, infine, chiamare **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="15daa-205">Finally, to delete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="15daa-206">L'esempio di codice seguente elimina il BLOB denominato **myblob**.</span><span class="sxs-lookup"><span data-stu-id="15daa-206">The following code example deletes the blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="15daa-207">Accesso simultaneo</span><span class="sxs-lookup"><span data-stu-id="15daa-207">Concurrent access</span></span>
<span data-ttu-id="15daa-208">Per supportare l'accesso simultaneo a un BLOB da più client o da più istanze di processo, è possibile usare gli **ETag** o **lease**.</span><span class="sxs-lookup"><span data-stu-id="15daa-208">To support concurrent access to a blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="15daa-209">**Etag** : fornisce un modo per rilevare le eventuali modifiche apportate al BLOB o contenitore da un altro processo</span><span class="sxs-lookup"><span data-stu-id="15daa-209">**Etag** - provides a way to detect that the blob or container has been modified by another process</span></span>
* <span data-ttu-id="15daa-210">**Lease** : consente di ottenere accesso esclusivo, rinnovabile, in scrittura o eliminazione a un BLOB per un periodo di tempo</span><span class="sxs-lookup"><span data-stu-id="15daa-210">**Lease** - provides a way to obtain exclusive, renewable, write or delete access to a blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="15daa-211">ETag</span><span class="sxs-lookup"><span data-stu-id="15daa-211">ETag</span></span>
<span data-ttu-id="15daa-212">Usare gli ETag se è necessario consentire a più client o istanze di scrivere simultaneamente nel BLOB in blocchi o nel BLOB di pagine.</span><span class="sxs-lookup"><span data-stu-id="15daa-212">Use ETags if you need to allow multiple clients or instances to write to the block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="15daa-213">L'ETag consente di determinare se il contenitore o il BLOB è stato modificato dalla data di creazione o dell'ultima lettura per evitare di sovrascrivere le modifiche già sottoposte a commit da un altro client o processo.</span><span class="sxs-lookup"><span data-stu-id="15daa-213">The ETag allows you to determine if the container or blob was modified since you initially read or created it, which allows you to avoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="15daa-214">È possibile impostare le condizioni degli ETag usando il parametro `options.accessConditions` facoltativo.</span><span class="sxs-lookup"><span data-stu-id="15daa-214">You can set ETag conditions by using the optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="15daa-215">L'esempio di codice seguente carica il file **test.txt** solo se il BLOB è già presente e include il valore di ETag contenuto in `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="15daa-215">The following code example only uploads the **test.txt** file if the blob already exists and has the ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="15daa-216">Il modello generale per l'uso degli ETag è il seguente:</span><span class="sxs-lookup"><span data-stu-id="15daa-216">When you're using ETags, the general pattern is:</span></span>

1. <span data-ttu-id="15daa-217">Ottenere l'ETag in seguito a un'operazione create, list o get.</span><span class="sxs-lookup"><span data-stu-id="15daa-217">Obtain the ETag as the result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="15daa-218">Eseguire un'azione verificando che il valore ETag non sia stato modificato.</span><span class="sxs-lookup"><span data-stu-id="15daa-218">Perform an action, checking that the ETag value has not been modified.</span></span>

<span data-ttu-id="15daa-219">Se il valore è stato modificato, significa che un altro client o un'altra istanza ha modificato il BLOB o il contenitore in un momento successivo a quello in cui è stato ottenuto il valore ETag.</span><span class="sxs-lookup"><span data-stu-id="15daa-219">If the value was modified, this indicates that another client or instance modified the blob or container since you obtained the ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="15daa-220">Lease</span><span class="sxs-lookup"><span data-stu-id="15daa-220">Lease</span></span>
<span data-ttu-id="15daa-221">È possibile acquisire un nuovo lease usando il metodo **acquireLease** e specificando il BLOB o il contenitore per il quale si vuole ottenere il lease.</span><span class="sxs-lookup"><span data-stu-id="15daa-221">You can acquire a new lease by using the **acquireLease** method, specifying the blob or container that you wish to obtain a lease on.</span></span> <span data-ttu-id="15daa-222">Il codice seguente ad esempio acquisisce un lease sul BLOB **myblob**.</span><span class="sxs-lookup"><span data-stu-id="15daa-222">For example, the following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="15daa-223">Le operazioni successive sul BLOB **myblob** devono fornire il parametro `options.leaseId`.</span><span class="sxs-lookup"><span data-stu-id="15daa-223">Subsequent operations on **myblob** must provide the `options.leaseId` parameter.</span></span> <span data-ttu-id="15daa-224">L'ID del lease viene restituito come `result.id` da **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="15daa-224">The lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="15daa-225">Per impostazione predefinita, la durata del lease è infinita.</span><span class="sxs-lookup"><span data-stu-id="15daa-225">By default, the lease duration is infinite.</span></span> <span data-ttu-id="15daa-226">Per definire una durata non infinita (compresa tra 15 e 60 secondi), specificare il parametro `options.leaseDuration` .</span><span class="sxs-lookup"><span data-stu-id="15daa-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing the `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="15daa-227">Per rimuovere un lease, usare il metodo **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="15daa-227">To remove a lease, use **releaseLease**.</span></span> <span data-ttu-id="15daa-228">Per interrompere un lease e impedire ad altri di ottenere un nuovo lease fintanto che la durata originale non scade, usare il metodo **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="15daa-228">To break a lease, but prevent others from obtaining a new lease until the original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="15daa-229">Usare le firme di accesso condiviso di Azure</span><span class="sxs-lookup"><span data-stu-id="15daa-229">Work with shared access signatures</span></span>
<span data-ttu-id="15daa-230">Le firme di accesso condiviso rappresentano un modo sicuro per fornire accesso granulare a BLOB e contenitori senza specificare il nome o le chiavi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="15daa-230">Shared access signatures (SAS) are a secure way to provide granular access to blobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="15daa-231">Tali firme vengono spesso usate per fornire accesso limitato ai dati, ad esempio per consentire a un'app per dispositivi mobili di accedere ai BLOB.</span><span class="sxs-lookup"><span data-stu-id="15daa-231">Shared access signatures are often used to provide limited access to your data, such as allowing a mobile app to access blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="15daa-232">Benché sia anche possibile consentire l'accesso anonimo ai BLOB, le firme di accesso condiviso garantiscono un accesso più controllato, in quanto devono essere generate.</span><span class="sxs-lookup"><span data-stu-id="15daa-232">While you can also allow anonymous access to blobs, shared access signatures allow you to provide more controlled access, as you must generate the SAS.</span></span>
>
>

<span data-ttu-id="15daa-233">Un'applicazione attendibile, ad esempio un servizio basato sul cloud, genera una firma di accesso condiviso tramite il metodo **generateSharedAccessSignature** dell'oggetto **BlobService** e la fornisce a un'applicazione non attendibile o parzialmente attendibile, ad esempio a un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="15daa-233">A trusted application such as a cloud-based service generates shared access signatures using the **generateSharedAccessSignature** of the **BlobService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="15daa-234">La firma di accesso condiviso viene generata tramite un criterio che indica le date di inizio e di fine del periodo di validità della firma, nonché il livello di accesso concesso al titolare della firma.</span><span class="sxs-lookup"><span data-stu-id="15daa-234">Shared access signatures are generated using a policy, which describes the start and end dates during which the shared access signatures are valid, as well as the access level granted to the shared access signatures holder.</span></span>

<span data-ttu-id="15daa-235">L'esempio di codice seguente genera un nuovo criterio di accesso condiviso che consente al titolare della firma di accesso condiviso di eseguire operazioni di lettura nel BLOB **myblob** e che scadrà 100 minuti dopo la data di creazione.</span><span class="sxs-lookup"><span data-stu-id="15daa-235">The following code example generates a new shared access policy that allows the shared access signatures holder to perform read operations on the **myblob** blob, and expires 100 minutes after the time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
};

var blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', 'myblob', sharedAccessPolicy);
var host = blobSvc.host;
```

<span data-ttu-id="15daa-236">Si noti che devono essere fornite anche le informazioni sull'host, in quanto sono necessarie quando il titolare della firma di accesso condiviso tenta di accedere al contenitore.</span><span class="sxs-lookup"><span data-stu-id="15daa-236">Note that the host information must be provided also, as it is required when the shared access signatures holder attempts to access the container.</span></span>

<span data-ttu-id="15daa-237">L'applicazione client usa quindi la firma di accesso condiviso con **BlobServiceWithSAS** per eseguire operazioni sul BLOB.</span><span class="sxs-lookup"><span data-stu-id="15daa-237">The client application then uses shared access signatures with **BlobServiceWithSAS** to perform operations against the blob.</span></span> <span data-ttu-id="15daa-238">L'operazione seguente consente di recuperare informazioni sul BLOB **myblob**.</span><span class="sxs-lookup"><span data-stu-id="15daa-238">The following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="15daa-239">Poiché la firma di accesso condiviso è stata generata con l'accesso in sola lettura, verrà restituito un errore se viene eseguito un tentativo di modificare il BLOB.</span><span class="sxs-lookup"><span data-stu-id="15daa-239">Since the shared access signatures were generated with read-only access, if an attempt is made to modify the blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="15daa-240">Elenchi di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="15daa-240">Access control lists</span></span>
<span data-ttu-id="15daa-241">Per impostare i criteri di accesso per una firma di accesso condiviso, è anche possibile usare un elenco di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="15daa-241">You can also use an access control list (ACL) to set the access policy for SAS.</span></span> <span data-ttu-id="15daa-242">Questa soluzione è utile quando si desidera consentire a più client di accedere a un contenitore, impostando tuttavia criteri di accesso diversi per ogni client.</span><span class="sxs-lookup"><span data-stu-id="15daa-242">This is useful if you wish to allow multiple clients to access a container but provide different access policies for each client.</span></span>

<span data-ttu-id="15daa-243">Un elenco di controllo di accesso viene implementato usando una matrice di criteri di accesso, con un ID associato a ogni criterio.</span><span class="sxs-lookup"><span data-stu-id="15daa-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="15daa-244">L'esempio di codice seguente definisce due criteri, uno per 'user1' e uno per 'user2':</span><span class="sxs-lookup"><span data-stu-id="15daa-244">The following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.READ,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.BlobUtilities.SharedAccessPermissions.WRITE,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="15daa-245">L'esempio di codice seguente recupera l'elenco di controllo di accesso corrente per **mycontainer** e quindi aggiunge i nuovi criteri tramite **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="15daa-245">The following code example gets the current ACL for **mycontainer**, and then adds the new policies using **setBlobAcl**.</span></span> <span data-ttu-id="15daa-246">Risultato:</span><span class="sxs-lookup"><span data-stu-id="15daa-246">This approach allows:</span></span>

```nodejs
var extend = require('extend');
blobSvc.getBlobAcl('mycontainer', function(error, result, response) {
  if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    blobSvc.setBlobAcl('mycontainer', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="15daa-247">Dopo aver impostato l'elenco di controllo di accesso, è possibile creare una firma di accesso condiviso in base all'ID di un criterio.</span><span class="sxs-lookup"><span data-stu-id="15daa-247">Once the ACL is set, you can then create shared access signatures based on the ID for a policy.</span></span> <span data-ttu-id="15daa-248">L'esempio di codice seguente crea una nuova firma di accesso condiviso per 'user2':</span><span class="sxs-lookup"><span data-stu-id="15daa-248">The following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="15daa-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="15daa-249">Next steps</span></span>
<span data-ttu-id="15daa-250">Per altre informazioni, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="15daa-250">For more information, see the following resources.</span></span>

* <span data-ttu-id="15daa-251">[Riferimento per le API di Azure Storage SDK per Node][Azure Storage SDK for Node API Reference]</span><span class="sxs-lookup"><span data-stu-id="15daa-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="15daa-252">[Blog del team di Archiviazione di Azure][Azure Storage Team Blog]</span><span class="sxs-lookup"><span data-stu-id="15daa-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="15daa-253">Repository di [Azure Storage SDK per Node][Azure Storage SDK for Node] su GitHub</span><span class="sxs-lookup"><span data-stu-id="15daa-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="15daa-254">Centro per sviluppatori di Node. js</span><span class="sxs-lookup"><span data-stu-id="15daa-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="15daa-255">Trasferire dati con l'utilità della riga di comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="15daa-255">Transfer data with the AzCopy command-line utility</span></span>](storage-use-azcopy.md)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="15daa-256">[Creare un'app Web Node.js nel servizio app di Azure]: ../app-service-web/app-service-web-get-started-nodejs.md</span><span class="sxs-lookup"><span data-stu-id="15daa-256">[Create a Node.js web app in Azure App Service]: ../app-service-web/app-service-web-get-started-nodejs.md</span></span>
<span data-ttu-id="15daa-257">[App Web Node.js con il servizio tabelle di Azure]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span><span class="sxs-lookup"><span data-stu-id="15daa-257">[Node.js web app using the Azure Table Service]: ../app-service-web/storage-nodejs-use-table-storage-web-site.md</span></span>
<span data-ttu-id="15daa-258">[Creazione e distribuzione di un sito Web Node.js in Azure con WebMatrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span><span class="sxs-lookup"><span data-stu-id="15daa-258">[Build and deploy a Node.js web app to Azure using Web Matrix]: ../app-service-web/web-sites-nodejs-use-webmatrix.md</span></span>
[Using the REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx
[Azure portal]: https://portal.azure.com
<span data-ttu-id="15daa-259">[Creazione e distribuzione di un'applicazione Node.js a un servizio cloud di Azure]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span><span class="sxs-lookup"><span data-stu-id="15daa-259">[Build and deploy a Node.js application to an Azure Cloud Service]: ../cloud-services/cloud-services-nodejs-develop-deploy-app.md</span></span>
[Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/
[Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html
