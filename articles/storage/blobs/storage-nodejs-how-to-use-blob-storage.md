---
title: aaaHow toouse archiviazione Blob da Node.js | Documenti Microsoft
description: Archiviare dati non strutturati nel cloud hello con archiviazione Blob di Azure (archiviazione di oggetti).
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
ms.openlocfilehash: 572e7fc9f7b19ff01720a7cadd495c809ed49fb2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blob-storage-from-nodejs"></a><span data-ttu-id="b1307-103">Come toouse archiviazione Blob da Node.js</span><span class="sxs-lookup"><span data-stu-id="b1307-103">How toouse Blob storage from Node.js</span></span>
[!INCLUDE [storage-selector-blob-include](../../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-all](../../../includes/storage-check-out-samples-all.md)]

## <a name="overview"></a><span data-ttu-id="b1307-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="b1307-104">Overview</span></span>
<span data-ttu-id="b1307-105">In questo articolo illustra come tooperform scenari comuni di utilizzo dell'archiviazione Blob.</span><span class="sxs-lookup"><span data-stu-id="b1307-105">This article shows you how tooperform common scenarios using Blob storage.</span></span> <span data-ttu-id="b1307-106">esempi di Hello vengono scritti tramite hello API Node.js.</span><span class="sxs-lookup"><span data-stu-id="b1307-106">hello samples are written via hello Node.js API.</span></span> <span data-ttu-id="b1307-107">scenari di Hello trattati includono come tooupload, elenco, scaricare ed eliminare i BLOB.</span><span class="sxs-lookup"><span data-stu-id="b1307-107">hello scenarios covered include how tooupload, list, download, and delete blobs.</span></span>

[!INCLUDE [storage-blob-concepts-include](../../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../../includes/storage-create-account-include.md)]

## <a name="create-a-nodejs-application"></a><span data-ttu-id="b1307-108">Creare un'applicazione Node.js</span><span class="sxs-lookup"><span data-stu-id="b1307-108">Create a Node.js application</span></span>
<span data-ttu-id="b1307-109">Per istruzioni su come toocreate un'applicazione Node.js, vedere [creare un'app web Node.js in Azure App Service], [compilare e distribuire un tooan di applicazione del servizio Cloud di Azure Node.js](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) : utilizzo di Windows PowerShell, o [compilare e distribuire un tooAzure di app web Node. js utilizzando WebMatrix](https://www.microsoft.com/web/webmatrix/).</span><span class="sxs-lookup"><span data-stu-id="b1307-109">For instructions on how toocreate a Node.js application, see [Create a Node.js web app in Azure App Service], [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) -- using Windows PowerShell, or [Build and deploy a Node.js web app tooAzure using Web Matrix](https://www.microsoft.com/web/webmatrix/).</span></span>

## <a name="configure-your-application-tooaccess-storage"></a><span data-ttu-id="b1307-110">Configurare l'archiviazione tooaccess applicazione</span><span class="sxs-lookup"><span data-stu-id="b1307-110">Configure your application tooaccess storage</span></span>
<span data-ttu-id="b1307-111">toouse archiviazione di Azure, è necessario hello Azure Storage SDK per Node.js, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="b1307-111">toouse Azure storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooobtain-hello-package"></a><span data-ttu-id="b1307-112">Utilizzare un pacchetto di hello tooobtain nodo Package Manager (NPM)</span><span class="sxs-lookup"><span data-stu-id="b1307-112">Use Node Package Manager (NPM) tooobtain hello package</span></span>
1. <span data-ttu-id="b1307-113">Utilizzare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix), toonavigate toohello cartella in cui è stato creato l'esempio applicazione.</span><span class="sxs-lookup"><span data-stu-id="b1307-113">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), toonavigate toohello folder where you created your sample application.</span></span>
2. <span data-ttu-id="b1307-114">Tipo **npm installare archiviazione di azure** nella finestra di comando hello.</span><span class="sxs-lookup"><span data-stu-id="b1307-114">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="b1307-115">Output del comando hello è simile toohello esempio di codice seguente.</span><span class="sxs-lookup"><span data-stu-id="b1307-115">Output from hello command is similar toohello following code example.</span></span>

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
3. <span data-ttu-id="b1307-116">È possibile eseguire manualmente hello **ls** comando tooverify che un **nodo\_moduli** cartella è stata creata.</span><span class="sxs-lookup"><span data-stu-id="b1307-116">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="b1307-117">All'interno di tale cartella, trovare hello **archiviazione di azure** pacchetto che contiene le librerie di hello che è necessario un archivio tooaccess.</span><span class="sxs-lookup"><span data-stu-id="b1307-117">Inside that folder, find hello **azure-storage** package, which contains hello libraries that you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="b1307-118">Importa pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="b1307-118">Import hello package</span></span>
<span data-ttu-id="b1307-119">Utilizzando blocco note o un altro editor di testo, aggiungere hello seguente toohello cima hello **server.js** file dell'applicazione hello in cui si intende toouse archiviazione:</span><span class="sxs-lookup"><span data-stu-id="b1307-119">Using Notepad or another text editor, add hello following toohello top of hello **server.js** file of hello application where you intend toouse storage:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="b1307-120">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="b1307-120">Set up an Azure Storage connection</span></span>
<span data-ttu-id="b1307-121">Hello modulo Azure verrà lette le variabili di ambiente hello `AZURE_STORAGE_ACCOUNT` e `AZURE_STORAGE_ACCESS_KEY`, o `AZURE_STORAGE_CONNECTION_STRING`, per le informazioni necessarie tooconnect tooyour account di archiviazione Azure.</span><span class="sxs-lookup"><span data-stu-id="b1307-121">hello Azure module will read hello environment variables `AZURE_STORAGE_ACCOUNT` and `AZURE_STORAGE_ACCESS_KEY`, or `AZURE_STORAGE_CONNECTION_STRING`, for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="b1307-122">Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello quando si chiama **createBlobService**.</span><span class="sxs-lookup"><span data-stu-id="b1307-122">If these environment variables are not set, you must specify hello account information when calling **createBlobService**.</span></span>

<span data-ttu-id="b1307-123">Per un esempio di impostazione delle variabili di ambiente hello in hello [portale di Azure](https://portal.azure.com) per un'app web di Azure, vedere [app web Node. js utilizzando hello del servizio tabelle di Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="b1307-123">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure web app, see [Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="b1307-124">Creare un contenitore</span><span class="sxs-lookup"><span data-stu-id="b1307-124">Create a container</span></span>
<span data-ttu-id="b1307-125">Hello **BlobService** oggetto consente di collaborare con i contenitori e BLOB.</span><span class="sxs-lookup"><span data-stu-id="b1307-125">hello **BlobService** object lets you work with containers and blobs.</span></span> <span data-ttu-id="b1307-126">Hello codice seguente viene creata una **BlobService** oggetto.</span><span class="sxs-lookup"><span data-stu-id="b1307-126">hello following code creates a **BlobService** object.</span></span> <span data-ttu-id="b1307-127">Aggiungere il seguente hello parte superiore di hello di **server.js**:</span><span class="sxs-lookup"><span data-stu-id="b1307-127">Add hello following near hello top of **server.js**:</span></span>

```nodejs
var blobSvc = azure.createBlobService();
```

> [!NOTE]
> <span data-ttu-id="b1307-128">È possibile accedere in modo anonimo un blob utilizzando **createBlobServiceAnonymous** e fornendo l'indirizzo host hello.</span><span class="sxs-lookup"><span data-stu-id="b1307-128">You can access a blob anonymously by using **createBlobServiceAnonymous** and providing hello host address.</span></span> <span data-ttu-id="b1307-129">Ad esempio, usare `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span><span class="sxs-lookup"><span data-stu-id="b1307-129">For example, use `var blobSvc = azure.createBlobServiceAnonymous('https://myblob.blob.core.windows.net/');`.</span></span>
>
>

[!INCLUDE [storage-container-naming-rules-include](../../../includes/storage-container-naming-rules-include.md)]

<span data-ttu-id="b1307-130">Utilizzare un nuovo contenitore, toocreate **createContainerIfNotExists**.</span><span class="sxs-lookup"><span data-stu-id="b1307-130">toocreate a new container, use **createContainerIfNotExists**.</span></span> <span data-ttu-id="b1307-131">Hello esempio di codice seguente crea un nuovo contenitore denominato 'mycontainer':</span><span class="sxs-lookup"><span data-stu-id="b1307-131">hello following code example creates a new container named 'mycontainer':</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', function(error, result, response){
    if(!error){
      // Container exists and is private
    }
});
```

<span data-ttu-id="b1307-132">Se il contenitore di hello appena creato, `result.created` è true.</span><span class="sxs-lookup"><span data-stu-id="b1307-132">If hello container is newly created, `result.created` is true.</span></span> <span data-ttu-id="b1307-133">Se il contenitore di hello esiste già, `result.created` è false.</span><span class="sxs-lookup"><span data-stu-id="b1307-133">If hello container already exists, `result.created` is false.</span></span> <span data-ttu-id="b1307-134">`response`contiene informazioni sull'operazione di hello, incluse le informazioni di hello ETag per il contenitore di hello.</span><span class="sxs-lookup"><span data-stu-id="b1307-134">`response` contains information about hello operation, including hello ETag information for hello container.</span></span>

### <a name="container-security"></a><span data-ttu-id="b1307-135">Sicurezza del contenitore</span><span class="sxs-lookup"><span data-stu-id="b1307-135">Container security</span></span>
<span data-ttu-id="b1307-136">Per impostazione predefinita, i nuovi contenitori sono privati e non è possibile accedervi in modo anonimo.</span><span class="sxs-lookup"><span data-stu-id="b1307-136">By default, new containers are private and cannot be accessed anonymously.</span></span> <span data-ttu-id="b1307-137">contenitore di hello toomake pubblico in modo che sia possibile accedervi in modo anonimo, è possibile impostare il livello di accesso del contenitore hello troppo**blob** o **contenitore**.</span><span class="sxs-lookup"><span data-stu-id="b1307-137">toomake hello container public so that you can access it anonymously, you can set hello container's access level too**blob** or **container**.</span></span>

* <span data-ttu-id="b1307-138">**BLOB** -consente l'accesso in lettura anonimo tooblob contenuto e i metadati all'interno del contenitore, ma non toocontainer metadati, ad esempio l'elenco di tutti i BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="b1307-138">**blob** - allows anonymous read access tooblob content and metadata within this container, but not toocontainer metadata such as listing all blobs within a container</span></span>
* <span data-ttu-id="b1307-139">**contenitore** -consente l'accesso in lettura anonimo tooblob contenuto e i metadati, nonché i metadati del contenitore</span><span class="sxs-lookup"><span data-stu-id="b1307-139">**container** - allows anonymous read access tooblob content and metadata as well as container metadata</span></span>

<span data-ttu-id="b1307-140">Hello esempio di codice riportato di seguito viene illustrato il livello di accesso hello impostazione troppo**blob**:</span><span class="sxs-lookup"><span data-stu-id="b1307-140">hello following code example demonstrates setting hello access level too**blob**:</span></span>

```nodejs
blobSvc.createContainerIfNotExists('mycontainer', {publicAccessLevel : 'blob'}, function(error, result, response){
    if(!error){
      // Container exists and allows
      // anonymous read access tooblob
      // content and metadata within this container
    }
});
```

<span data-ttu-id="b1307-141">In alternativa, è possibile modificare il livello di accesso hello di un contenitore utilizzando **setContainerAcl** toospecify il livello di accesso hello.</span><span class="sxs-lookup"><span data-stu-id="b1307-141">Alternatively, you can modify hello access level of a container by using **setContainerAcl** toospecify hello access level.</span></span> <span data-ttu-id="b1307-142">esempio modifiche hello accesso livello toocontainer di codice seguente di Hello:</span><span class="sxs-lookup"><span data-stu-id="b1307-142">hello following code example changes hello access level toocontainer:</span></span>

```nodejs
blobSvc.setContainerAcl('mycontainer', null /* signedIdentifiers */, {publicAccessLevel : 'container'} /* publicAccessLevel*/, function(error, result, response){
  if(!error){
    // Container access level set too'container'
  }
});
```

<span data-ttu-id="b1307-143">risultato Hello contiene informazioni sull'operazione di hello, tra cui hello corrente **ETag** per contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="b1307-143">hello result contains information about hello operation, including hello current **ETag** for hello container.</span></span>

### <a name="filters"></a><span data-ttu-id="b1307-144">Filtri</span><span class="sxs-lookup"><span data-stu-id="b1307-144">Filters</span></span>
<span data-ttu-id="b1307-145">È possibile applicare facoltativo il filtraggio operazioni toooperations eseguita mediante **BlobService**.</span><span class="sxs-lookup"><span data-stu-id="b1307-145">You can apply optional filtering operations toooperations performed using **BlobService**.</span></span> <span data-ttu-id="b1307-146">Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con firma hello:</span><span class="sxs-lookup"><span data-stu-id="b1307-146">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="b1307-147">Dopo aver eseguito il pre-elaborazione sulle opzioni di richiesta di hello, metodo hello deve toocall "Avanti", il passaggio di un callback con hello seguente firma:</span><span class="sxs-lookup"><span data-stu-id="b1307-147">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="b1307-148">In questo callback e dopo l'elaborazione di hello returnObject (risposta hello dal server di hello richiesta toohello), il callback di hello richiede tooeither richiamare successivamente se esiste l'elaborazione di altri filtri toocontinue o semplicemente richiamare servizio hello di finalCallback tooend chiamata.</span><span class="sxs-lookup"><span data-stu-id="b1307-148">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback tooend hello service invocation.</span></span>

<span data-ttu-id="b1307-149">Due filtri, che implementano la logica di ripetizione sono inclusi in Azure SDK per Node.js, hello **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="b1307-149">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="b1307-150">Hello seguito creato un **BlobService** oggetto che utilizza hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="b1307-150">hello following creates a **BlobService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var blobSvc = azure.createBlobService().withFilter(retryOperations);
```

## <a name="upload-a-blob-into-a-container"></a><span data-ttu-id="b1307-151">Caricare un BLOB in un contenitore</span><span class="sxs-lookup"><span data-stu-id="b1307-151">Upload a blob into a container</span></span>
<span data-ttu-id="b1307-152">Esistono tre tipi di BLOB: BLOB in blocchi, BLOB di pagine e BLOB di accodamento.</span><span class="sxs-lookup"><span data-stu-id="b1307-152">There are three types of blobs: block blobs, page blobs and append blobs.</span></span> <span data-ttu-id="b1307-153">I BLOB in blocchi è toomore in modo efficiente caricare i dati di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="b1307-153">Block blobs allow you toomore efficiently upload large data.</span></span> <span data-ttu-id="b1307-154">I BLOB di accodamento sono ottimizzati per le operazioni di accodamento.</span><span class="sxs-lookup"><span data-stu-id="b1307-154">Append blobs are optimized for append operations.</span></span> <span data-ttu-id="b1307-155">I BLOB di pagine sono ottimizzati per le operazioni di lettura/scrittura.</span><span class="sxs-lookup"><span data-stu-id="b1307-155">Page blobs are optimized for read/write operations.</span></span> <span data-ttu-id="b1307-156">Per altre informazioni, vedere [Informazioni sui BLOB in blocchi, sui BLOB di aggiunta e sui BLOB di pagine](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span><span class="sxs-lookup"><span data-stu-id="b1307-156">For more information, see [Understanding Block Blobs, Append Blobs, and Page Blobs](http://msdn.microsoft.com/library/azure/ee691964.aspx).</span></span>

### <a name="block-blobs"></a><span data-ttu-id="b1307-157">BLOB in blocchi</span><span class="sxs-lookup"><span data-stu-id="b1307-157">Block blobs</span></span>
<span data-ttu-id="b1307-158">blob in blocchi tooa dati tooupload, utilizzare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1307-158">tooupload data tooa block blob, use hello following:</span></span>

* <span data-ttu-id="b1307-159">**createBlockBlobFromLocalFile** : crea un nuovo blob in blocchi e carica il contenuto di hello di un file</span><span class="sxs-lookup"><span data-stu-id="b1307-159">**createBlockBlobFromLocalFile** - creates a new block blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="b1307-160">**createBlockBlobFromStream** : crea un nuovo blob in blocchi e carica il contenuto di hello di un flusso</span><span class="sxs-lookup"><span data-stu-id="b1307-160">**createBlockBlobFromStream** - creates a new block blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="b1307-161">**createBlockBlobFromText** : crea un nuovo blob in blocchi e carica il contenuto di hello di una stringa</span><span class="sxs-lookup"><span data-stu-id="b1307-161">**createBlockBlobFromText** - creates a new block blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="b1307-162">**createWriteStreamToBlockBlob** -fornisce un blob in blocchi tooa flusso scrittura</span><span class="sxs-lookup"><span data-stu-id="b1307-162">**createWriteStreamToBlockBlob** - provides a write stream tooa block blob</span></span>

<span data-ttu-id="b1307-163">esempio di codice seguente Hello carica il contenuto di hello di hello **test.txt** file **myblob**.</span><span class="sxs-lookup"><span data-stu-id="b1307-163">hello following code example uploads hello contents of hello **test.txt** file into **myblob**.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="b1307-164">Hello `result` restituito da questi metodi contiene informazioni sull'operazione di hello, ad esempio hello **ETag** del blob hello.</span><span class="sxs-lookup"><span data-stu-id="b1307-164">hello `result` returned by these methods contains information on hello operation, such as hello **ETag** of hello blob.</span></span>

### <a name="append-blobs"></a><span data-ttu-id="b1307-165">BLOB di accodamento</span><span class="sxs-lookup"><span data-stu-id="b1307-165">Append blobs</span></span>
<span data-ttu-id="b1307-166">tooupload dati tooa nuovo blob di accodamento, utilizzare hello seguente:</span><span class="sxs-lookup"><span data-stu-id="b1307-166">tooupload data tooa new append blob, use hello following:</span></span>

* <span data-ttu-id="b1307-167">**createAppendBlobFromLocalFile** : crea un nuovo blob di aggiunta e carica il contenuto di hello di un file</span><span class="sxs-lookup"><span data-stu-id="b1307-167">**createAppendBlobFromLocalFile** - creates a new append blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="b1307-168">**createAppendBlobFromStream** : crea un nuovo blob di aggiunta e carica il contenuto di hello di un flusso</span><span class="sxs-lookup"><span data-stu-id="b1307-168">**createAppendBlobFromStream** - creates a new append blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="b1307-169">**createAppendBlobFromText** : crea un nuovo blob di aggiunta e carica il contenuto di hello di una stringa</span><span class="sxs-lookup"><span data-stu-id="b1307-169">**createAppendBlobFromText** - creates a new append blob and uploads hello contents of a string</span></span>
* <span data-ttu-id="b1307-170">**createWriteStreamToNewAppendBlob** : crea un nuovo blob di aggiunta e quindi fornisce un tooit toowrite flusso</span><span class="sxs-lookup"><span data-stu-id="b1307-170">**createWriteStreamToNewAppendBlob** - creates a new append blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="b1307-171">esempio di codice seguente Hello carica il contenuto di hello di hello **test.txt** file **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="b1307-171">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.createAppendBlobFromLocalFile('mycontainer', 'myappendblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="b1307-172">tooappend un tooan blocco esistente aggiungere blob, utilizzare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1307-172">tooappend a block tooan existing append blob, use hello following:</span></span>

* <span data-ttu-id="b1307-173">**appendFromLocalFile** -accodare hello contenuto di un file tooan esistente aggiungere blob</span><span class="sxs-lookup"><span data-stu-id="b1307-173">**appendFromLocalFile** - append hello contents of a file tooan existing append blob</span></span>
* <span data-ttu-id="b1307-174">**appendFromStream** -accodare hello contenuto di un flusso tooan esistente aggiungere blob</span><span class="sxs-lookup"><span data-stu-id="b1307-174">**appendFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="b1307-175">**appendFromText** -aggiungere contenuto hello di tooan una stringa esistente aggiungere blob</span><span class="sxs-lookup"><span data-stu-id="b1307-175">**appendFromText** - append hello contents of a string tooan existing append blob</span></span>
* <span data-ttu-id="b1307-176">**appendBlockFromStream** -accodare hello contenuto di un flusso tooan esistente aggiungere blob</span><span class="sxs-lookup"><span data-stu-id="b1307-176">**appendBlockFromStream** - append hello contents of a stream tooan existing append blob</span></span>
* <span data-ttu-id="b1307-177">**appendBlockFromText** -aggiungere contenuto hello di tooan una stringa esistente aggiungere blob</span><span class="sxs-lookup"><span data-stu-id="b1307-177">**appendBlockFromText** - append hello contents of a string tooan existing append blob</span></span>

> [!NOTE]
> <span data-ttu-id="b1307-178">appendFromXXX API eseguirà alcune chiamate non necessari server di convalida lato client toofail tooavoid veloce.</span><span class="sxs-lookup"><span data-stu-id="b1307-178">appendFromXXX APIs will do some client-side validation toofail fast tooavoid unnecessary server calls.</span></span> <span data-ttu-id="b1307-179">contrariamente alle API appendBlockFromXXX.</span><span class="sxs-lookup"><span data-stu-id="b1307-179">appendBlockFromXXX won't.</span></span>
>
>

<span data-ttu-id="b1307-180">esempio di codice seguente Hello carica il contenuto di hello di hello **test.txt** file **myappendblob**.</span><span class="sxs-lookup"><span data-stu-id="b1307-180">hello following code example uploads hello contents of hello **test.txt** file into **myappendblob**.</span></span>

```nodejs
blobSvc.appendFromText('mycontainer', 'myappendblob', 'text toobe appended', function(error, result, response){
  if(!error){
    // text appended
  }
});
```

### <a name="page-blobs"></a><span data-ttu-id="b1307-181">BLOB di pagine</span><span class="sxs-lookup"><span data-stu-id="b1307-181">Page blobs</span></span>
<span data-ttu-id="b1307-182">blob di pagine tooa dati tooupload, utilizzare hello seguenti:</span><span class="sxs-lookup"><span data-stu-id="b1307-182">tooupload data tooa page blob, use hello following:</span></span>

* <span data-ttu-id="b1307-183">**createPageBlob** : crea un nuovo BLOB di pagine con una lunghezza specifica</span><span class="sxs-lookup"><span data-stu-id="b1307-183">**createPageBlob** - creates a new page blob of a specific length</span></span>
* <span data-ttu-id="b1307-184">**createPageBlobFromLocalFile** : crea un nuovo blob di pagine e carica il contenuto di hello di un file</span><span class="sxs-lookup"><span data-stu-id="b1307-184">**createPageBlobFromLocalFile** - creates a new page blob and uploads hello contents of a file</span></span>
* <span data-ttu-id="b1307-185">**createPageBlobFromStream** : crea un nuovo blob di pagine e carica il contenuto di hello di un flusso</span><span class="sxs-lookup"><span data-stu-id="b1307-185">**createPageBlobFromStream** - creates a new page blob and uploads hello contents of a stream</span></span>
* <span data-ttu-id="b1307-186">**createWriteStreamToExistingPageBlob** -fornisce un blob di pagine esistente scrittura flusso tooan</span><span class="sxs-lookup"><span data-stu-id="b1307-186">**createWriteStreamToExistingPageBlob** - provides a write stream tooan existing page blob</span></span>
* <span data-ttu-id="b1307-187">**createWriteStreamToNewPageBlob** : crea un nuovo blob di pagine e quindi fornisce un tooit toowrite flusso</span><span class="sxs-lookup"><span data-stu-id="b1307-187">**createWriteStreamToNewPageBlob** - creates a new page blob and then provides a stream toowrite tooit</span></span>

<span data-ttu-id="b1307-188">esempio di codice seguente Hello carica il contenuto di hello di hello **test.txt** file **mypageblob**.</span><span class="sxs-lookup"><span data-stu-id="b1307-188">hello following code example uploads hello contents of hello **test.txt** file into **mypageblob**.</span></span>

```nodejs
blobSvc.createPageBlobFromLocalFile('mycontainer', 'mypageblob', 'test.txt', function(error, result, response){
  if(!error){
    // file uploaded
  }
});
```

> [!NOTE]
> <span data-ttu-id="b1307-189">I BLOB di pagine sono costituiti da "pagine" da 512 byte.</span><span class="sxs-lookup"><span data-stu-id="b1307-189">Page blobs consist of 512-byte 'pages'.</span></span> <span data-ttu-id="b1307-190">Quando si caricano dati con una dimensione che non corrisponde a un multiplo di 512, viene visualizzato un errore.</span><span class="sxs-lookup"><span data-stu-id="b1307-190">You will receive an error when uploading data with a size that is not a multiple of 512.</span></span>
>
>

## <a name="list-hello-blobs-in-a-container"></a><span data-ttu-id="b1307-191">Elenco di BLOB hello in un contenitore</span><span class="sxs-lookup"><span data-stu-id="b1307-191">List hello blobs in a container</span></span>
<span data-ttu-id="b1307-192">BLOB di hello toolist in un contenitore, usare hello **listBlobsSegmented** metodo.</span><span class="sxs-lookup"><span data-stu-id="b1307-192">toolist hello blobs in a container, use hello **listBlobsSegmented** method.</span></span> <span data-ttu-id="b1307-193">Se si desidera tooreturn BLOB con un prefisso specifico, utilizzare **listBlobsSegmentedWithPrefix**.</span><span class="sxs-lookup"><span data-stu-id="b1307-193">If you'd like tooreturn blobs with a specific prefix, use **listBlobsSegmentedWithPrefix**.</span></span>

```nodejs
blobSvc.listBlobsSegmented('mycontainer', null, function(error, result, response){
  if(!error){
      // result.entries contains hello entries
      // If not all blobs were returned, result.continuationToken has hello continuation token.
  }
});
```

<span data-ttu-id="b1307-194">Hello `result` contiene un `entries` raccolta, ovvero una matrice di oggetti che descrivono ogni blob.</span><span class="sxs-lookup"><span data-stu-id="b1307-194">hello `result` contains an `entries` collection, which is an array of objects that describe each blob.</span></span> <span data-ttu-id="b1307-195">Se non è possibile restituire tutti i BLOB, hello `result` fornisce inoltre un `continuationToken`, che è possibile utilizzare come hello secondo parametro tooretrieve ulteriori voci.</span><span class="sxs-lookup"><span data-stu-id="b1307-195">If all blobs cannot be returned, hello `result` also provides a `continuationToken`, which you may use as hello second parameter tooretrieve additional entries.</span></span>

## <a name="download-blobs"></a><span data-ttu-id="b1307-196">Scaricare BLOB</span><span class="sxs-lookup"><span data-stu-id="b1307-196">Download blobs</span></span>
<span data-ttu-id="b1307-197">dati toodownload da un blob, utilizzare l'esempio hello:</span><span class="sxs-lookup"><span data-stu-id="b1307-197">toodownload data from a blob, use hello following:</span></span>

* <span data-ttu-id="b1307-198">**getBlobToLocalFile** -scrive hello blob contenuto toofile</span><span class="sxs-lookup"><span data-stu-id="b1307-198">**getBlobToLocalFile** - writes hello blob contents toofile</span></span>
* <span data-ttu-id="b1307-199">**getBlobToStream** -scrive hello blob contenuto tooa flusso</span><span class="sxs-lookup"><span data-stu-id="b1307-199">**getBlobToStream** - writes hello blob contents tooa stream</span></span>
* <span data-ttu-id="b1307-200">**getBlobToText** -scrive il contenuto di blob hello tooa stringa</span><span class="sxs-lookup"><span data-stu-id="b1307-200">**getBlobToText** - writes hello blob contents tooa string</span></span>
* <span data-ttu-id="b1307-201">**createReadStream** -fornisce un tooread flusso dal blob hello</span><span class="sxs-lookup"><span data-stu-id="b1307-201">**createReadStream** - provides a stream tooread from hello blob</span></span>

<span data-ttu-id="b1307-202">Hello esempio di codice seguente viene illustrato come utilizzare **getBlobToStream** contenuto hello toodownload di hello **myblob** blob e di archiviarlo toohello **txt** file utilizzando un flusso:</span><span class="sxs-lookup"><span data-stu-id="b1307-202">hello following code example demonstrates using **getBlobToStream** toodownload hello contents of hello **myblob** blob and store it toohello **output.txt** file by using a stream:</span></span>

```nodejs
var fs = require('fs');
blobSvc.getBlobToStream('mycontainer', 'myblob', fs.createWriteStream('output.txt'), function(error, result, response){
  if(!error){
    // blob retrieved
  }
});
```

<span data-ttu-id="b1307-203">Hello `result` contiene informazioni sui blob di hello, tra cui **ETag** informazioni.</span><span class="sxs-lookup"><span data-stu-id="b1307-203">hello `result` contains information about hello blob, including **ETag** information.</span></span>

## <a name="delete-a-blob"></a><span data-ttu-id="b1307-204">Eliminare un BLOB</span><span class="sxs-lookup"><span data-stu-id="b1307-204">Delete a blob</span></span>
<span data-ttu-id="b1307-205">Chiamare infine toodelete un blob, **deleteBlob**.</span><span class="sxs-lookup"><span data-stu-id="b1307-205">Finally, toodelete a blob, call **deleteBlob**.</span></span> <span data-ttu-id="b1307-206">Hello eliminazioni hello blob denominato di esempio di codice seguente **myblob**.</span><span class="sxs-lookup"><span data-stu-id="b1307-206">hello following code example deletes hello blob named **myblob**.</span></span>

```nodejs
blobSvc.deleteBlob(containerName, 'myblob', function(error, response){
  if(!error){
    // Blob has been deleted
  }
});
```

## <a name="concurrent-access"></a><span data-ttu-id="b1307-207">Accesso simultaneo</span><span class="sxs-lookup"><span data-stu-id="b1307-207">Concurrent access</span></span>
<span data-ttu-id="b1307-208">blob di tooa toosupport accesso simultaneo da più client o più istanze di processo, è possibile utilizzare **eTag** o **lease**.</span><span class="sxs-lookup"><span data-stu-id="b1307-208">toosupport concurrent access tooa blob from multiple clients or multiple process instances, you can use **ETags** or **leases**.</span></span>

* <span data-ttu-id="b1307-209">**ETag** -fornisce un modo toodetect che hello blob o contenitore è stato modificato da un altro processo</span><span class="sxs-lookup"><span data-stu-id="b1307-209">**Etag** - provides a way toodetect that hello blob or container has been modified by another process</span></span>
* <span data-ttu-id="b1307-210">**Lease** : fornisce una scrittura esclusivo, rinnovabile, tooobtain modo o eliminare il blob tooa di accesso per un periodo di tempo</span><span class="sxs-lookup"><span data-stu-id="b1307-210">**Lease** - provides a way tooobtain exclusive, renewable, write or delete access tooa blob for a period of time</span></span>

### <a name="etag"></a><span data-ttu-id="b1307-211">ETag</span><span class="sxs-lookup"><span data-stu-id="b1307-211">ETag</span></span>
<span data-ttu-id="b1307-212">Se è necessario tooallow più client o istanze toowrite toohello Blob di pagine o blocchi del Blob contemporaneamente, utilizzare ETag.</span><span class="sxs-lookup"><span data-stu-id="b1307-212">Use ETags if you need tooallow multiple clients or instances toowrite toohello block Blob or page Blob simultaneously.</span></span> <span data-ttu-id="b1307-213">Hello ETag consente toodetermine se hello contenitore o blob è stato modificato dopo la lettura di inizialmente o creato, che consente di sovrascrivere le modifiche a commit da un altro client o processo tooavoid.</span><span class="sxs-lookup"><span data-stu-id="b1307-213">hello ETag allows you toodetermine if hello container or blob was modified since you initially read or created it, which allows you tooavoid overwriting changes committed by another client or process.</span></span>

<span data-ttu-id="b1307-214">È possibile impostare le condizioni di ETag utilizzando hello facoltativo `options.accessConditions` parametro.</span><span class="sxs-lookup"><span data-stu-id="b1307-214">You can set ETag conditions by using hello optional `options.accessConditions` parameter.</span></span> <span data-ttu-id="b1307-215">Hello esempio di codice seguente solo carica hello **test.txt** contenuti file se il blob hello esiste già e contiene il valore di ETag hello `etagToMatch`.</span><span class="sxs-lookup"><span data-stu-id="b1307-215">hello following code example only uploads hello **test.txt** file if hello blob already exists and has hello ETag value contained by `etagToMatch`.</span></span>

```nodejs
blobSvc.createBlockBlobFromLocalFile('mycontainer', 'myblob', 'test.txt', { accessConditions: { EtagMatch: etagToMatch} }, function(error, result, response){
    if(!error){
    // file uploaded
  }
});
```

<span data-ttu-id="b1307-216">Quando si utilizzano valori eTag, modello generale di hello è:</span><span class="sxs-lookup"><span data-stu-id="b1307-216">When you're using ETags, hello general pattern is:</span></span>

1. <span data-ttu-id="b1307-217">Ottenere hello ETag come risultato di hello di creazione un elenco operazione get.</span><span class="sxs-lookup"><span data-stu-id="b1307-217">Obtain hello ETag as hello result of a create, list, or get operation.</span></span>
2. <span data-ttu-id="b1307-218">Eseguire un'azione, il controllo che non è stato modificato il valore ETag hello.</span><span class="sxs-lookup"><span data-stu-id="b1307-218">Perform an action, checking that hello ETag value has not been modified.</span></span>

<span data-ttu-id="b1307-219">Se è stato modificato il valore di hello, ciò indica che un altro client o un'istanza modificato hello blob o contenitore perché è stato ottenuto il valore di ETag hello.</span><span class="sxs-lookup"><span data-stu-id="b1307-219">If hello value was modified, this indicates that another client or instance modified hello blob or container since you obtained hello ETag value.</span></span>

### <a name="lease"></a><span data-ttu-id="b1307-220">Lease</span><span class="sxs-lookup"><span data-stu-id="b1307-220">Lease</span></span>
<span data-ttu-id="b1307-221">È possibile acquisire un nuovo lease utilizzando hello **acquireLease** metodo, specificando hello blob o il contenitore che si desidera tooobtain un lease in.</span><span class="sxs-lookup"><span data-stu-id="b1307-221">You can acquire a new lease by using hello **acquireLease** method, specifying hello blob or container that you wish tooobtain a lease on.</span></span> <span data-ttu-id="b1307-222">Ad esempio, hello seguente codice acquisisce un lease su **myblob**.</span><span class="sxs-lookup"><span data-stu-id="b1307-222">For example, hello following code acquires a lease on **myblob**.</span></span>

```nodejs
blobSvc.acquireLease('mycontainer', 'myblob', function(error, result, response){
  if(!error) {
    console.log('leaseId: ' + result.id);
  }
});
```

<span data-ttu-id="b1307-223">Operazioni successive su **myblob** deve fornire hello `options.leaseId` parametro.</span><span class="sxs-lookup"><span data-stu-id="b1307-223">Subsequent operations on **myblob** must provide hello `options.leaseId` parameter.</span></span> <span data-ttu-id="b1307-224">come viene restituito l'ID lease di Hello `result.id` da **acquireLease**.</span><span class="sxs-lookup"><span data-stu-id="b1307-224">hello lease ID is returned as `result.id` from **acquireLease**.</span></span>

> [!NOTE]
> <span data-ttu-id="b1307-225">Per impostazione predefinita, la durata del lease hello è infinita.</span><span class="sxs-lookup"><span data-stu-id="b1307-225">By default, hello lease duration is infinite.</span></span> <span data-ttu-id="b1307-226">È possibile specificare una durata non infinito (compreso tra 15 e 60 secondi), fornendo hello `options.leaseDuration` parametro.</span><span class="sxs-lookup"><span data-stu-id="b1307-226">You can specify a non-infinite duration (between 15 and 60 seconds) by providing hello `options.leaseDuration` parameter.</span></span>
>
>

<span data-ttu-id="b1307-227">Utilizzare tooremove un lease, **releaseLease**.</span><span class="sxs-lookup"><span data-stu-id="b1307-227">tooremove a lease, use **releaseLease**.</span></span> <span data-ttu-id="b1307-228">toobreak un lease, ma impedire ad altri utenti di ottenere un nuovo lease finché la durata originale hello è scaduto, utilizzare **breakLease**.</span><span class="sxs-lookup"><span data-stu-id="b1307-228">toobreak a lease, but prevent others from obtaining a new lease until hello original duration has expired, use **breakLease**.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="b1307-229">Usare le firme di accesso condiviso di Azure</span><span class="sxs-lookup"><span data-stu-id="b1307-229">Work with shared access signatures</span></span>
<span data-ttu-id="b1307-230">Firme di accesso condiviso (SAS) sono un tooblobs di accesso granulare tooprovide in modo sicuro e contenitori senza fornire il nome account di archiviazione o chiavi.</span><span class="sxs-lookup"><span data-stu-id="b1307-230">Shared access signatures (SAS) are a secure way tooprovide granular access tooblobs and containers without providing your storage account name or keys.</span></span> <span data-ttu-id="b1307-231">Firme di accesso condiviso sono spesso i dati tooyour di accesso utilizzato tooprovide limitate, ad esempio per consentire a un'app mobile tooaccess BLOB.</span><span class="sxs-lookup"><span data-stu-id="b1307-231">Shared access signatures are often used tooprovide limited access tooyour data, such as allowing a mobile app tooaccess blobs.</span></span>

> [!NOTE]
> <span data-ttu-id="b1307-232">Mentre è inoltre possibile consentire l'accesso anonimo tooblobs, firme di accesso condiviso consentono di tooprovide più controllato l'accesso, come è necessario generare hello SAS.</span><span class="sxs-lookup"><span data-stu-id="b1307-232">While you can also allow anonymous access tooblobs, shared access signatures allow you tooprovide more controlled access, as you must generate hello SAS.</span></span>
>
>

<span data-ttu-id="b1307-233">Un'applicazione attendibile, ad esempio un servizio basato su cloud genera firme di accesso condiviso utilizzando hello **generateSharedAccessSignature** di hello **BlobService**e fornisce tooan non attendibili o applicazione con attendibilità parziale, ad esempio un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="b1307-233">A trusted application such as a cloud-based service generates shared access signatures using hello **generateSharedAccessSignature** of hello **BlobService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="b1307-234">Le firme generate utilizzando un criterio, che descrive l'avvio di hello di accesso condiviso e la data di fine durante cui hello firme di accesso condiviso sono valide, nonché hello accedere titolare livello di firme di accesso condiviso toohello concesso.</span><span class="sxs-lookup"><span data-stu-id="b1307-234">Shared access signatures are generated using a policy, which describes hello start and end dates during which hello shared access signatures are valid, as well as hello access level granted toohello shared access signatures holder.</span></span>

<span data-ttu-id="b1307-235">esempio di codice seguente Hello genera un nuovo criterio di accesso condiviso che consente di hello condiviso accesso firme titolare tooperform operazioni di lettura nel hello **myblob** blob e scade 100 minuti dopo il tempo di hello viene creato.</span><span class="sxs-lookup"><span data-stu-id="b1307-235">hello following code example generates a new shared access policy that allows hello shared access signatures holder tooperform read operations on hello **myblob** blob, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="b1307-236">Si noti che le informazioni sull'host hello deve essere fornito, come richiesto quando titolare firme di accesso condiviso hello tenta anche contenitore hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="b1307-236">Note that hello host information must be provided also, as it is required when hello shared access signatures holder attempts tooaccess hello container.</span></span>

<span data-ttu-id="b1307-237">quindi l'applicazione client Hello utilizza le firme di accesso condiviso con **BlobServiceWithSAS** tooperform operazioni blob hello.</span><span class="sxs-lookup"><span data-stu-id="b1307-237">hello client application then uses shared access signatures with **BlobServiceWithSAS** tooperform operations against hello blob.</span></span> <span data-ttu-id="b1307-238">Hello seguente ottiene informazioni sul **myblob**.</span><span class="sxs-lookup"><span data-stu-id="b1307-238">hello following gets information about **myblob**.</span></span>

```nodejs
var sharedBlobSvc = azure.createBlobServiceWithSas(host, blobSAS);
sharedBlobSvc.getBlobProperties('mycontainer', 'myblob', function (error, result, response) {
  if(!error) {
    // retrieved info
  }
});
```

<span data-ttu-id="b1307-239">Poiché le firme di accesso condiviso hello generate con accesso in sola lettura, se viene effettuato un tentativo di blob hello toomodify, verrà restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="b1307-239">Since hello shared access signatures were generated with read-only access, if an attempt is made toomodify hello blob, an error will be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="b1307-240">Elenchi di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="b1307-240">Access control lists</span></span>
<span data-ttu-id="b1307-241">È anche possibile utilizzare criteri di accesso di accesso controllo elenco (ACL) tooset hello di SAS.</span><span class="sxs-lookup"><span data-stu-id="b1307-241">You can also use an access control list (ACL) tooset hello access policy for SAS.</span></span> <span data-ttu-id="b1307-242">Ciò è utile se si desidera tooallow più client tooaccess un contenitore ma forniscono criteri di accesso diversi per ogni client.</span><span class="sxs-lookup"><span data-stu-id="b1307-242">This is useful if you wish tooallow multiple clients tooaccess a container but provide different access policies for each client.</span></span>

<span data-ttu-id="b1307-243">Un elenco di controllo di accesso viene implementato usando una matrice di criteri di accesso, con un ID associato a ogni criterio.</span><span class="sxs-lookup"><span data-stu-id="b1307-243">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="b1307-244">Hello esempio di codice seguente definisce due criteri, uno per "user1" e uno per 'Utente2':</span><span class="sxs-lookup"><span data-stu-id="b1307-244">hello following code example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="b1307-245">Hello seguente ottiene di esempio di codice hello gli ACL per **mycontainer**e quindi aggiunge nuovi criteri hello utilizzando **setBlobAcl**.</span><span class="sxs-lookup"><span data-stu-id="b1307-245">hello following code example gets hello current ACL for **mycontainer**, and then adds hello new policies using **setBlobAcl**.</span></span> <span data-ttu-id="b1307-246">Risultato:</span><span class="sxs-lookup"><span data-stu-id="b1307-246">This approach allows:</span></span>

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

<span data-ttu-id="b1307-247">Una volta hello che ACL viene impostato, è possibile quindi creare le firme di accesso condiviso in base all'ID di hello per un criterio.</span><span class="sxs-lookup"><span data-stu-id="b1307-247">Once hello ACL is set, you can then create shared access signatures based on hello ID for a policy.</span></span> <span data-ttu-id="b1307-248">esempio di codice seguente Hello crea nuove firme di accesso condiviso per 'Utente2':</span><span class="sxs-lookup"><span data-stu-id="b1307-248">hello following code example creates new shared access signatures for 'user2':</span></span>

```nodejs
blobSAS = blobSvc.generateSharedAccessSignature('mycontainer', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="b1307-249">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b1307-249">Next steps</span></span>
<span data-ttu-id="b1307-250">Per ulteriori informazioni, vedere hello seguenti risorse.</span><span class="sxs-lookup"><span data-stu-id="b1307-250">For more information, see hello following resources.</span></span>

* <span data-ttu-id="b1307-251">[Riferimento per le API di Azure Storage SDK per Node][Riferimento per le API di Azure Storage SDK per Node]</span><span class="sxs-lookup"><span data-stu-id="b1307-251">[Azure Storage SDK for Node API Reference][Azure Storage SDK for Node API Reference]</span></span>
* <span data-ttu-id="b1307-252">[Blog del team di Archiviazione di Azure][Blog del team di Archiviazione di Azure]</span><span class="sxs-lookup"><span data-stu-id="b1307-252">[Azure Storage Team Blog][Azure Storage Team Blog]</span></span>
* <span data-ttu-id="b1307-253">Repository di [Azure Storage SDK per Node][Azure Storage SDK for Node] su GitHub</span><span class="sxs-lookup"><span data-stu-id="b1307-253">[Azure Storage SDK for Node][Azure Storage SDK for Node] repository on GitHub</span></span>
* [<span data-ttu-id="b1307-254">Centro per sviluppatori di Node. js</span><span class="sxs-lookup"><span data-stu-id="b1307-254">Node.js Developer Center</span></span>](https://azure.microsoft.com/develop/nodejs/)
* [<span data-ttu-id="b1307-255">Trasferimento dati con hello utilità della riga di comando AzCopy</span><span class="sxs-lookup"><span data-stu-id="b1307-255">Transfer data with hello AzCopy command-line utility</span></span>](../common/storage-use-azcopy.md?toc=%2fazure%2fstorage%2fblobs%2ftoc.json)

[Azure Storage SDK for Node]: https://github.com/Azure/azure-storage-node

<span data-ttu-id="b1307-256">[App web Node. js utilizzando hello del servizio tabelle di Azure](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span><span class="sxs-lookup"><span data-stu-id="b1307-256">[Node.js web app using hello Azure Table Service](../../app-service-web/storage-nodejs-use-table-storage-web-site.md)  </span></span>  
<span data-ttu-id="b1307-257">[Compilare e distribuire un tooAzure di app web Node. js utilizzando WebMatrix]: https://www.microsoft.com/web/webmatrix/</span><span class="sxs-lookup"><span data-stu-id="b1307-257">[Build and deploy a Node.js web app tooAzure using Web Matrix]: https://www.microsoft.com/web/webmatrix/</span></span>  
<span data-ttu-id="b1307-258">[Utilizzando hello REST API]: [portale] http://msdn.microsoft.com/library/azure/hh264518.aspx: https://portal.azure.com [compilare e distribuire un tooan di applicazione del servizio Cloud di Azure Node.js](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Blog del Team di archiviazione di Azure]: http:// [Azure Storage SDK per nodo di riferimento all'API] blogs.msdn.com/b/windowsazurestorage/: http://dl.windowsazure.com/nodestoragedocs/index.html</span><span class="sxs-lookup"><span data-stu-id="b1307-258">[Using hello REST API]: http://msdn.microsoft.com/library/azure/hh264518.aspx [Azure portal]: https://portal.azure.com [Build and deploy a Node.js application tooan Azure Cloud Service](../../cloud-services/cloud-services-nodejs-develop-deploy-app.md) [Azure Storage Team Blog]: http://blogs.msdn.com/b/windowsazurestorage/ [Azure Storage SDK for Node API Reference]: http://dl.windowsazure.com/nodestoragedocs/index.html</span></span>
