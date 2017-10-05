---
title: Come usare l'archiviazione tabelle di Azure da Node.js | Microsoft Docs
description: Archiviare dati non strutturati nel cloud con il servizio di archiviazione tabelle di Azure, ovvero un archivio dati NoSQL.
services: storage
documentationcenter: nodejs
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: fc2e33d2-c5da-4861-8503-53fdc25750de
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 12/08/2016
ms.author: marsma
ms.openlocfilehash: f004408910aecc380e20f7da54dbd155d179aaa5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-use-azure-table-storage-from-nodejs"></a><span data-ttu-id="95111-103">Come usare l'archiviazione tabelle di Azure da Node.js</span><span class="sxs-lookup"><span data-stu-id="95111-103">How to use Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="95111-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="95111-104">Overview</span></span>
<span data-ttu-id="95111-105">Questo argomento illustra come eseguire scenari comuni usando il servizio tabelle di Azure in un'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="95111-105">This topic shows how to perform common scenarios using the Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="95111-106">Negli esempi di codice illustrati in questo argomento si suppone che sia già stata ottenuta un'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="95111-106">The code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="95111-107">Per informazioni su come creare un'applicazione Node.js in Azure, vedere uno qualsiasi degli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="95111-107">For information about how to create a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="95111-108">Creare un'app Web Node.js nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="95111-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="95111-109">Creazione e distribuzione di un sito Web Node.js in Azure con WebMatrix</span><span class="sxs-lookup"><span data-stu-id="95111-109">Build and deploy a Node.js web app to Azure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="95111-110">[Creare e distribuire un'applicazione Node.js in un servizio cloud di Azure](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (usando Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="95111-110">[Build and deploy a Node.js application to an Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-to-access-azure-storage"></a><span data-ttu-id="95111-111">Configurare l'applicazione per l'accesso all'archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="95111-111">Configure your application to access Azure Storage</span></span>
<span data-ttu-id="95111-112">Per usare Archiviazione di Azure, è necessario disporre di Azure Storage SDK per Node.js, che comprende un set di pratiche librerie che comunicano con i servizi di archiviazione REST.</span><span class="sxs-lookup"><span data-stu-id="95111-112">To use Azure Storage, you need the Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with the storage REST services.</span></span>

### <a name="use-node-package-manager-npm-to-install-the-package"></a><span data-ttu-id="95111-113">Usare Node Package Manager (NPM) per installare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="95111-113">Use Node Package Manager (NPM) to install the package</span></span>
1. <span data-ttu-id="95111-114">Usare un'interfaccia della riga di comando come **PowerShell** (Windows), **Terminale** (Mac) o **Bash** (Unix) e passare alla cartella in cui è stata creata l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="95111-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate to the folder where you created your application.</span></span>
2. <span data-ttu-id="95111-115">Digitare **npm install azure-storage** nella finestra di comando.</span><span class="sxs-lookup"><span data-stu-id="95111-115">Type **npm install azure-storage** in the command window.</span></span> <span data-ttu-id="95111-116">L'output da questo comando sarà simile al seguente esempio:</span><span class="sxs-lookup"><span data-stu-id="95111-116">Output from the command is similar to the following example.</span></span>

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
3. <span data-ttu-id="95111-117">È possibile eseguire manualmente il comando **ls** per verificare che sia stata creata una cartella **node\_modules**.</span><span class="sxs-lookup"><span data-stu-id="95111-117">You can manually run the **ls** command to verify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="95111-118">All'interno di questa cartella si trova il pacchetto **azure-storage** , che contiene le librerie necessarie per accedere all'archiviazione.</span><span class="sxs-lookup"><span data-stu-id="95111-118">Inside that folder you will find the **azure-storage** package, which contains the libraries you need to access storage.</span></span>

### <a name="import-the-package"></a><span data-ttu-id="95111-119">Importare il pacchetto</span><span class="sxs-lookup"><span data-stu-id="95111-119">Import the package</span></span>
<span data-ttu-id="95111-120">Aggiungere il codice seguente all'inizio del file **server.js** nell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="95111-120">Add the following code to the top of the **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="95111-121">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="95111-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="95111-122">I modulo di Azure leggerà le variabili di ambiente AZURE\_STORAGE\_ACCOUNT e AZURE\_STORAGE\_ACCESS\_KEY, o AZURE\_STORAGE\_CONNECTION\_STRING per ottenere le informazioni necessarie per la connessione all'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="95111-122">The azure module will read the environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required to connect to your Azure storage account.</span></span> <span data-ttu-id="95111-123">Se queste variabili di ambiente non sono impostate, sarà necessario specificare le informazioni relative all'account quando si chiama **TableService**.</span><span class="sxs-lookup"><span data-stu-id="95111-123">If these environment variables are not set, you must specify the account information when calling **TableService**.</span></span>

<span data-ttu-id="95111-124">Per un esempio di impostazione delle variabili di ambiente nel [portale di Azure](https://portal.azure.com) per un sito Web di Azure, vedere [App Web Node.js con il servizio tabelle di Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="95111-124">For an example of setting the environment variables in the [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using the Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="95111-125">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="95111-125">Create a table</span></span>
<span data-ttu-id="95111-126">Il codice seguente consente di creare un oggetto **TableService** e di utilizzarlo per creare una nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="95111-126">The following code creates a **TableService** object and uses it to create a new table.</span></span> <span data-ttu-id="95111-127">Aggiungere il codice seguente nella parte superiore di **server.js**.</span><span class="sxs-lookup"><span data-stu-id="95111-127">Add the following near the top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="95111-128">La chiamata a **createTableIfNotExists** crea una nuova tabella con il nome specificato, se non è già presente.</span><span class="sxs-lookup"><span data-stu-id="95111-128">The call to **createTableIfNotExists** will create a new table with the specified name if it does not already exist.</span></span> <span data-ttu-id="95111-129">Nell'esempio seguente viene creata una nuova tabella denominata "mytable" se questa non esiste ancora:</span><span class="sxs-lookup"><span data-stu-id="95111-129">The following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="95111-130">`result.created` sarà `true` se viene creata una nuova tabella e sarà `false` se la tabella è già presente.</span><span class="sxs-lookup"><span data-stu-id="95111-130">The `result.created` will be `true` if a new table is created, and `false` if the table already exists.</span></span> <span data-ttu-id="95111-131">`response` conterrà le informazioni sulla richiesta.</span><span class="sxs-lookup"><span data-stu-id="95111-131">The `response` will contain information about the request.</span></span>

### <a name="filters"></a><span data-ttu-id="95111-132">Filtri</span><span class="sxs-lookup"><span data-stu-id="95111-132">Filters</span></span>
<span data-ttu-id="95111-133">Le operazioni di filtro facoltative possono essere applicate alle operazioni eseguite usando **TableService**.</span><span class="sxs-lookup"><span data-stu-id="95111-133">Optional filtering operations can be applied to operations performed using **TableService**.</span></span> <span data-ttu-id="95111-134">Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con la firma:</span><span class="sxs-lookup"><span data-stu-id="95111-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with the signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="95111-135">Dopo aver eseguito la pre-elaborazione sulle opzioni della richiesta, il metodo deve chiamare "next" passando un callback con la firma seguente:</span><span class="sxs-lookup"><span data-stu-id="95111-135">After doing its preprocessing on the request options, the method needs to call "next", passing a callback with the following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="95111-136">In questo callback, e dopo l'elaborazione di returnObject (la risposta della richiesta al server), il callback deve richiamare "next", se questo esiste, per continuare a elaborare altri filtri oppure semplicemente richiamare finalCallback per concludere la chiamata al servizio.</span><span class="sxs-lookup"><span data-stu-id="95111-136">In this callback, and after processing the returnObject (the response from the request to the server), the callback needs to either invoke next if it exists to continue processing other filters or simply invoke finalCallback otherwise to end the service invocation.</span></span>

<span data-ttu-id="95111-137">In Azure SDK per Node.js sono inclusi due filtri che implementano la logica di ripetizione dei tentativi. Sono **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="95111-137">Two filters that implement retry logic are included with the Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="95111-138">Il codice seguente consente di creare un oggetto **TableService** che usa **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="95111-138">The following creates a **TableService** object that uses the **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-to-a-table"></a><span data-ttu-id="95111-139">Aggiungere un'entità a una tabella</span><span class="sxs-lookup"><span data-stu-id="95111-139">Add an entity to a table</span></span>
<span data-ttu-id="95111-140">Per aggiungere un'entità, creare prima un oggetto che definisca le proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="95111-140">To add an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="95111-141">Tutte le entità devono contenere **PartitionKey** e **RowKey** che sono gli identificatori univoci dell'entità.</span><span class="sxs-lookup"><span data-stu-id="95111-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for the entity.</span></span>

* <span data-ttu-id="95111-142">**PartitionKey** : determina la partizione in cui è archiviata l'entità.</span><span class="sxs-lookup"><span data-stu-id="95111-142">**PartitionKey** - determines the partition that the entity is stored in</span></span>
* <span data-ttu-id="95111-143">**RowKey** : identifica in modo univoco l'entità all'interno della partizione.</span><span class="sxs-lookup"><span data-stu-id="95111-143">**RowKey** - uniquely identifies the entity within the partition</span></span>

<span data-ttu-id="95111-144">Sia **PartitionKey** che **RowKey** devono essere valori stringa.</span><span class="sxs-lookup"><span data-stu-id="95111-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="95111-145">Per altre informazioni, vedere [Informazioni sul modello di dati del servizio tabelle](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="95111-145">For more information, see [Understanding the Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="95111-146">Nell'esempio seguente viene definita un'entità.</span><span class="sxs-lookup"><span data-stu-id="95111-146">The following is an example of defining an entity.</span></span> <span data-ttu-id="95111-147">**dueDate** è definito come tipo di **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="95111-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="95111-148">La specifica del tipo è facoltativa e si presuppone che i tipi non siano specificati.</span><span class="sxs-lookup"><span data-stu-id="95111-148">Specifying the type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="95111-149">Per ogni record è anche presente un campo **Timestamp** , impostato da Azure quando viene inserita o aggiornata un'entità.</span><span class="sxs-lookup"><span data-stu-id="95111-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="95111-150">È anche possibile usare **entityGenerator** per creare le entità.</span><span class="sxs-lookup"><span data-stu-id="95111-150">You can also use the **entityGenerator** to create entities.</span></span> <span data-ttu-id="95111-151">Nell'esempio seguente viene creata la stessa entità Task tramite **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="95111-151">The following example creates the same task entity using the **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out the trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="95111-152">Per aggiungere un'entità alla tabella, passare l'oggetto entità al metodo **insertEntity** .</span><span class="sxs-lookup"><span data-stu-id="95111-152">To add an entity to your table, pass the entity object to the **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="95111-153">Se l'operazione ha esito positivo, `result` conterrà l'[ETag](http://en.wikipedia.org/wiki/HTTP_ETag) del record inserito e `response` conterrà le informazioni sull'operazione.</span><span class="sxs-lookup"><span data-stu-id="95111-153">If the operation is successful, `result` will contain the [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of the inserted record and `response` will contain information about the operation.</span></span>

<span data-ttu-id="95111-154">Esempio di risposta:</span><span class="sxs-lookup"><span data-stu-id="95111-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="95111-155">Per impostazione predefinita, **insertEntity** non restituisce l'entità inserita come parte delle informazioni di `response`.</span><span class="sxs-lookup"><span data-stu-id="95111-155">By default, **insertEntity** does not return the inserted entity as part of the `response` information.</span></span> <span data-ttu-id="95111-156">Se si prevede di eseguire altre operazioni su questa entità o si intende memorizzare le informazioni nella cache, è opportuno che l'entità venga restituita insieme a `result`.</span><span class="sxs-lookup"><span data-stu-id="95111-156">If you plan on performing other operations on this entity, or wish to cache the information, it can be useful to have it returned as part of the `result`.</span></span> <span data-ttu-id="95111-157">A tale scopo, abilitare **echoContent** come segue:</span><span class="sxs-lookup"><span data-stu-id="95111-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="95111-158">Aggiornare un'entità</span><span class="sxs-lookup"><span data-stu-id="95111-158">Update an entity</span></span>
<span data-ttu-id="95111-159">Esistono vari metodi per aggiornare un'entità esistente:</span><span class="sxs-lookup"><span data-stu-id="95111-159">There are multiple methods available to update an existing entity:</span></span>

* <span data-ttu-id="95111-160">**replaceEntity** : aggiorna un'entità esistente sostituendola</span><span class="sxs-lookup"><span data-stu-id="95111-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="95111-161">**mergeEntity** : aggiorna un'entità esistente unendovi i nuovi valori delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="95111-161">**mergeEntity** - updates an existing entity by merging new property values into the existing entity</span></span>
* <span data-ttu-id="95111-162">**insertOrReplaceEntity** : aggiorna un'entità esistente sostituendola.</span><span class="sxs-lookup"><span data-stu-id="95111-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="95111-163">Se non esiste alcuna entità, ne verrà inserita una nuova.</span><span class="sxs-lookup"><span data-stu-id="95111-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="95111-164">**insertOrMergeEntity** : aggiorna un'entità esistente unendovi i nuovi valori delle proprietà.</span><span class="sxs-lookup"><span data-stu-id="95111-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into the existing.</span></span> <span data-ttu-id="95111-165">Se non esiste alcuna entità, ne verrà inserita una nuova.</span><span class="sxs-lookup"><span data-stu-id="95111-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="95111-166">Nell'esempio seguente viene illustrato l'aggiornamento di un'entità mediante **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="95111-166">The following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="95111-167">Per impostazione predefinita, l'aggiornamento di un'entità non comporta la verifica dei dati per controllare se siano stati modificati da altri processi.</span><span class="sxs-lookup"><span data-stu-id="95111-167">By default, updating an entity does not check to see if the data being updated has previously been modified by another process.</span></span> <span data-ttu-id="95111-168">Per supportare gli aggiornamenti simultanei:</span><span class="sxs-lookup"><span data-stu-id="95111-168">To support concurrent updates:</span></span>
>
> 1. <span data-ttu-id="95111-169">Recuperare il valore ETag dell'oggetto da aggiornare.</span><span class="sxs-lookup"><span data-stu-id="95111-169">Get the ETag of the object being updated.</span></span> <span data-ttu-id="95111-170">Questo valore viene restituito insieme a `response` per qualsiasi operazione associata all'entità e può essere recuperato tramite `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="95111-170">This is returned as part of the `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="95111-171">Quando si esegue un'operazione di aggiornamento su un'entità, aggiungere le informazioni ETag precedentemente recuperate alla nuova entità.</span><span class="sxs-lookup"><span data-stu-id="95111-171">When performing an update operation on an entity, add the ETag information previously retrieved to the new entity.</span></span> <span data-ttu-id="95111-172">Ad esempio:</span><span class="sxs-lookup"><span data-stu-id="95111-172">For example:</span></span>
>
>       <span data-ttu-id="95111-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="95111-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="95111-174">Eseguire l'operazione di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="95111-174">Perform the update operation.</span></span> <span data-ttu-id="95111-175">Se l'entità è stata modificata dall'ultimo recupero del valore di ETag, ad esempio da un'altra istanza dell'applicazione, viene restituito un `error` che indica che la condizione di aggiornamento specificata nella richiesta non è stata soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="95111-175">If the entity has been modified since you retrieved the ETag value, such as another instance of your application, an `error` will be returned stating that the update condition specified in the request was not satisfied.</span></span>
>
>

<span data-ttu-id="95111-176">Con **replaceEntity** e **mergeEntity**, se l'entità da aggiornare non esiste, l'operazione di aggiornamento non riesce.</span><span class="sxs-lookup"><span data-stu-id="95111-176">With **replaceEntity** and **mergeEntity**, if the entity that is being updated doesn't exist, then the update operation will fail.</span></span> <span data-ttu-id="95111-177">Se pertanto si desidera archiviare un'entità indipendentemente dal fatto che esista o meno, usare **insertOrReplaceEntity** oppure **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="95111-177">Therefore if you wish to store an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="95111-178">In `result` per le operazioni di aggiornamento riuscite correttamente sarà incluso l' **Etag** dell'entità aggiornata.</span><span class="sxs-lookup"><span data-stu-id="95111-178">The `result` for successful update operations will contain the **Etag** of the updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="95111-179">Usare i gruppi di entità</span><span class="sxs-lookup"><span data-stu-id="95111-179">Work with groups of entities</span></span>
<span data-ttu-id="95111-180">È talvolta consigliabile inviare più operazioni in un batch per garantire l'elaborazione atomica da parte del server.</span><span class="sxs-lookup"><span data-stu-id="95111-180">Sometimes it makes sense to submit multiple operations together in a batch to ensure atomic processing by the server.</span></span> <span data-ttu-id="95111-181">A questo scopo, usare la classe **TableBatch** per creare un batch e quindi usare il metodo **executeBatch** di **TableService** per eseguire le operazioni in batch.</span><span class="sxs-lookup"><span data-stu-id="95111-181">To accomplish that, use the **TableBatch** class to create a batch, and then use the **executeBatch** method of **TableService** to perform the batched operations.</span></span>

 <span data-ttu-id="95111-182">Nell'esempio seguente viene dimostrato l'invio di due entità in un batch:</span><span class="sxs-lookup"><span data-stu-id="95111-182">The following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out the trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash the dishes'},
  dueDate: {'_':new Date(2015, 6, 20)}
};

var batch = new azure.TableBatch();

batch.insertEntity(task1, {echoContent: true});
batch.insertEntity(task2, {echoContent: true});

tableSvc.executeBatch('mytable', batch, function (error, result, response) {
  if(!error) {
    // Batch completed
  }
});
```

<span data-ttu-id="95111-183">Per le operazioni in batch riuscite, `result` conterrà le informazioni relative a ogni operazione del batch.</span><span class="sxs-lookup"><span data-stu-id="95111-183">For successful batch operations, `result` will contain information for each operation in the batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="95111-184">Uso delle operazioni in batch</span><span class="sxs-lookup"><span data-stu-id="95111-184">Work with batched operations</span></span>
<span data-ttu-id="95111-185">Le operazioni aggiunte a un batch possono essere esaminate visualizzando la proprietà `operations` .</span><span class="sxs-lookup"><span data-stu-id="95111-185">Operations added to a batch can be inspected by viewing the `operations` property.</span></span> <span data-ttu-id="95111-186">Per usare le operazioni sono disponibili anche i metodi seguenti:</span><span class="sxs-lookup"><span data-stu-id="95111-186">You can also use the following methods to work with operations:</span></span>

* <span data-ttu-id="95111-187">**clear** : cancella tutte le operazioni da un batch.</span><span class="sxs-lookup"><span data-stu-id="95111-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="95111-188">**getOperations** : recupera un'operazione dal batch.</span><span class="sxs-lookup"><span data-stu-id="95111-188">**getOperations** - gets an operation from the batch</span></span>
* <span data-ttu-id="95111-189">**hasOperations** : restituisce true se il batch contiene operazioni.</span><span class="sxs-lookup"><span data-stu-id="95111-189">**hasOperations** - returns true if the batch contains operations</span></span>
* <span data-ttu-id="95111-190">**removeOperations** : rimuove un'operazione.</span><span class="sxs-lookup"><span data-stu-id="95111-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="95111-191">**size** : restituisce il numero di operazioni nel batch.</span><span class="sxs-lookup"><span data-stu-id="95111-191">**size** - returns the number of operations in the batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="95111-192">Recuperare un'entità in base alla chiave</span><span class="sxs-lookup"><span data-stu-id="95111-192">Retrieve an entity by key</span></span>
<span data-ttu-id="95111-193">Per restituire un'entità specifica in base a **PartitionKey** e **RowKey**, usare il metodo **retrieveEntity**.</span><span class="sxs-lookup"><span data-stu-id="95111-193">To return a specific entity based on the **PartitionKey** and **RowKey**, use the **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains the entity
  }
});
```

<span data-ttu-id="95111-194">Al termine di questa operazione, `result` conterrà l'entità.</span><span class="sxs-lookup"><span data-stu-id="95111-194">Once this operation is complete, `result` will contain the entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="95111-195">Eseguire query su un set di entità</span><span class="sxs-lookup"><span data-stu-id="95111-195">Query a set of entities</span></span>
<span data-ttu-id="95111-196">Per eseguire una query su una tabella, usare l'oggetto **TableQuery** per creare un'espressione di query con queste clausole:</span><span class="sxs-lookup"><span data-stu-id="95111-196">To query a table, use the **TableQuery** object to build up a query expression using the following clauses:</span></span>

* <span data-ttu-id="95111-197">**select** : i campi che la query deve restituire.</span><span class="sxs-lookup"><span data-stu-id="95111-197">**select** - the fields to be returned from the query</span></span>
* <span data-ttu-id="95111-198">**where** : la clausola where.</span><span class="sxs-lookup"><span data-stu-id="95111-198">**where** - the where clause</span></span>

  * <span data-ttu-id="95111-199">**and**: una condizione where`and`.</span><span class="sxs-lookup"><span data-stu-id="95111-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="95111-200">**or**: una condizione where `or`.</span><span class="sxs-lookup"><span data-stu-id="95111-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="95111-201">**top** : il numero di elementi da recuperare.</span><span class="sxs-lookup"><span data-stu-id="95111-201">**top** - the number of items to fetch</span></span>

<span data-ttu-id="95111-202">L'esempio seguente crea una query che restituisce i primi cinque elementi con PartitionKey 'hometasks'.</span><span class="sxs-lookup"><span data-stu-id="95111-202">The following example builds a query that will return the top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="95111-203">Poiché **select** non viene usato, vengono restituiti tutti i campi.</span><span class="sxs-lookup"><span data-stu-id="95111-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="95111-204">Per eseguire la query su una tabella, usare **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="95111-204">To perform the query against a table, use **queryEntities**.</span></span> <span data-ttu-id="95111-205">Nell'esempio seguente viene usata questa query per restituire entità da 'mytable'.</span><span class="sxs-lookup"><span data-stu-id="95111-205">The following example uses this query to return entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="95111-206">Se la query ha esito positivo, `result.entries` conterrà una matrice delle entità che corrispondono alla query.</span><span class="sxs-lookup"><span data-stu-id="95111-206">If successful, `result.entries` will contain an array of entities that match the query.</span></span> <span data-ttu-id="95111-207">Se la query non è in grado di restituire tutte le entità, `result.continuationToken` sarà un valore diverso da -*null* e potrà essere usato come terzo parametro di **queryEntities** per recuperare più risultati.</span><span class="sxs-lookup"><span data-stu-id="95111-207">If the query was unable to return all entities, `result.continuationToken` will be non-*null* and can be used as the third parameter of **queryEntities** to retrieve more results.</span></span> <span data-ttu-id="95111-208">Per la query iniziale, utilizzare *null* per il terzo parametro.</span><span class="sxs-lookup"><span data-stu-id="95111-208">For the initial query, use *null* for the third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="95111-209">Eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="95111-209">Query a subset of entity properties</span></span>
<span data-ttu-id="95111-210">Una query su una tabella può recuperare solo alcuni campi da un'entità.</span><span class="sxs-lookup"><span data-stu-id="95111-210">A query to a table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="95111-211">Questa tecnica permette di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="95111-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="95111-212">Usare la clausola **select** e passare i nomi dei campi da restituire.</span><span class="sxs-lookup"><span data-stu-id="95111-212">Use the **select** clause and pass the names of the fields to be returned.</span></span> <span data-ttu-id="95111-213">Ad esempio, la query seguente restituisce solo i campi **description** e **dueDate**.</span><span class="sxs-lookup"><span data-stu-id="95111-213">For example, the following query will return only the **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="95111-214">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="95111-214">Delete an entity</span></span>
<span data-ttu-id="95111-215">È possibile eliminare un'entità utilizzando le relative chiavi di riga e di partizione.</span><span class="sxs-lookup"><span data-stu-id="95111-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="95111-216">In questo esempio, l'oggetto **task1** contiene i valori **RowKey** e **PartitionKey** dell'entità da eliminare.</span><span class="sxs-lookup"><span data-stu-id="95111-216">In this example, the **task1** object contains the **RowKey** and **PartitionKey** values of the entity to be deleted.</span></span> <span data-ttu-id="95111-217">L'oggetto viene quindi passato al metodo **deleteEntity** .</span><span class="sxs-lookup"><span data-stu-id="95111-217">Then the object is passed to the **deleteEntity** method.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'}
};

tableSvc.deleteEntity('mytable', task, function(error, response){
  if(!error) {
    // Entity deleted
  }
});
```

> [!NOTE]
> <span data-ttu-id="95111-218">Quando si eliminano elementi, è bene valutare l'uso di ETag per assicurarsi che l'elemento non sia stato modificato da un altro processo.</span><span class="sxs-lookup"><span data-stu-id="95111-218">Consider using ETags when deleting items, to ensure that the item hasn't been modified by another process.</span></span> <span data-ttu-id="95111-219">Vedere [Aggiornare un'entità](#update-an-entity) per informazioni sull'uso di ETag.</span><span class="sxs-lookup"><span data-stu-id="95111-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="95111-220">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="95111-220">Delete a table</span></span>
<span data-ttu-id="95111-221">Nell'esempio di codice seguente viene illustrato come eliminare una tabella da un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="95111-221">The following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="95111-222">Se non si è certi dell'esistenza della tabella, usare **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="95111-222">If you are uncertain whether the table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="95111-223">Utilizzare i token di continuazione</span><span class="sxs-lookup"><span data-stu-id="95111-223">Use continuation tokens</span></span>
<span data-ttu-id="95111-224">Quando si esegue una query di tabelle di grandi quantità di risultati, ricercare i token di continuazione.</span><span class="sxs-lookup"><span data-stu-id="95111-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="95111-225">Potrebbero essere disponibili grandi quantità di dati per la query di cui si potrebbe non essere consapevoli se non si compila il riconoscimento della presenza di un token di continuazione.</span><span class="sxs-lookup"><span data-stu-id="95111-225">There may be large amounts of data available for your query that you might not realize if you do not build to recognize when a continuation token is present.</span></span>

<span data-ttu-id="95111-226">L'oggetto results restituito quando si esegue una query sulle entità imposta una proprietà `continuationToken` se è presente un token di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="95111-226">The results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="95111-227">È possibile quindi utilizzarlo quando si esegue una query per continuare a spostarsi tra le entità della partizione e della tabella.</span><span class="sxs-lookup"><span data-stu-id="95111-227">You can then use this when performing a query to continue to move across the partition and table entities.</span></span>

<span data-ttu-id="95111-228">Quando si esegue una query, è possibile specificare un parametro continuationToken tra l'istanza dell'oggetto della query e la funzione di richiamata:</span><span class="sxs-lookup"><span data-stu-id="95111-228">When querying, a continuationToken parameter may be provided between the query object instance and the callback function:</span></span>

```nodejs
var nextContinuationToken = null;
dc.table.queryEntities(tableName,
    query,
    nextContinuationToken,
    function (error, results) {
        if (error) throw error;

        // iterate through results.entries with results

        if (results.continuationToken) {
            nextContinuationToken = results.continuationToken;
        }

    });
```

<span data-ttu-id="95111-229">Se si osserva l'oggetto `continuationToken`, si troveranno proprietà come `nextPartitionKey`, `nextRowKey` e `targetLocation` che possono essere usate per eseguire l'iterazione di tutti i risultati.</span><span class="sxs-lookup"><span data-stu-id="95111-229">If you inspect the `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used to iterate through all the results.</span></span>

<span data-ttu-id="95111-230">È inoltre disponibile un esempio di continuazione all'interno del repository Node.js di Archiviazione di Azure su GitHub.</span><span class="sxs-lookup"><span data-stu-id="95111-230">There is also a continuation sample within the Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="95111-231">Cercare `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="95111-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="95111-232">Usare le firme di accesso condiviso di Azure</span><span class="sxs-lookup"><span data-stu-id="95111-232">Work with shared access signatures</span></span>
<span data-ttu-id="95111-233">Le firme di accesso condiviso rappresentano un modo sicuro per fornire accesso granulare alle tabelle senza specificare il nome o le chiavi dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="95111-233">Shared access signatures (SAS) are a secure way to provide granular access to tables without providing your storage account name or keys.</span></span> <span data-ttu-id="95111-234">Le firme di accesso condiviso vengono spesso usate per fornire accesso limitato ai dati, ad esempio per consentire a un'app per dispositivi mobili di eseguire query sui record.</span><span class="sxs-lookup"><span data-stu-id="95111-234">SAS are often used to provide limited access to your data, such as allowing a mobile app to query records.</span></span>

<span data-ttu-id="95111-235">Un'applicazione attendibile, ad esempio un servizio basato sul cloud, genera una firma di accesso condiviso tramite il metodo **generateSharedAccessSignature** dell'oggetto **TableService** e la fornisce a un'applicazione non attendibile o parzialmente attendibile, ad esempio a un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="95111-235">A trusted application such as a cloud-based service generates a SAS using the **generateSharedAccessSignature** of the **TableService**, and provides it to an untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="95111-236">La firma di accesso condiviso viene generata tramite un criterio che indica le date di inizio e di fine del periodo di validità della firma, nonché il livello di accesso concesso al titolare della firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="95111-236">The SAS is generated using a policy, which describes the start and end dates during which the SAS is valid, as well as the access level granted to the SAS holder.</span></span>

<span data-ttu-id="95111-237">Nell'esempio seguente viene generato un nuovo criterio di accesso condiviso che consentirà al titolare della firma di accesso condiviso di eseguire una query ('r') per la tabella e che scadrà 100 minuti dopo la data di creazione.</span><span class="sxs-lookup"><span data-stu-id="95111-237">The following example generates a new shared access policy that will allow the SAS holder to query ('r') the table, and expires 100 minutes after the time it is created.</span></span>

```nodejs
var startDate = new Date();
var expiryDate = new Date(startDate);
expiryDate.setMinutes(startDate.getMinutes() + 100);
startDate.setMinutes(startDate.getMinutes() - 100);

var sharedAccessPolicy = {
  AccessPolicy: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
};

var tableSAS = tableSvc.generateSharedAccessSignature('mytable', sharedAccessPolicy);
var host = tableSvc.host;
```

<span data-ttu-id="95111-238">Si noti che è necessario fornire anche le informazioni sull'host, in quanto sono necessarie quando il titolare della firma di accesso condiviso tenta di accedere alla tabella.</span><span class="sxs-lookup"><span data-stu-id="95111-238">Note that the host information must be provided also, as it is required when the SAS holder attempts to access the table.</span></span>

<span data-ttu-id="95111-239">L'applicazione client usa quindi la firma di accesso condiviso con il metodo **TableServiceWithSAS** per eseguire operazioni sulla tabella.</span><span class="sxs-lookup"><span data-stu-id="95111-239">The client application then uses the SAS with **TableServiceWithSAS** to perform operations against the table.</span></span> <span data-ttu-id="95111-240">Nell'esempio seguente viene eseguita la connessione alla tabella e viene eseguita una query.</span><span class="sxs-lookup"><span data-stu-id="95111-240">The following example connects to the table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains the entities
  }
});
```

<span data-ttu-id="95111-241">Poiché la firma di accesso condiviso è stata generata con accesso solo query, se si tentasse di inserire, aggiornare o eliminare le entità verrebbe restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="95111-241">Since the SAS was generated with only query access, if an attempt were made to insert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="95111-242">Elenchi di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="95111-242">Access Control Lists</span></span>
<span data-ttu-id="95111-243">Per impostare i criteri di accesso per una firma di accesso condiviso è anche possibile usare un elenco di controllo di accesso.</span><span class="sxs-lookup"><span data-stu-id="95111-243">You can also use an Access Control List (ACL) to set the access policy for a SAS.</span></span> <span data-ttu-id="95111-244">Questa soluzione è utile quando si vuole consentire a più client di accedere alla tabella, impostando tuttavia criteri di accesso diversi per ogni client.</span><span class="sxs-lookup"><span data-stu-id="95111-244">This is useful if you wish to allow multiple clients to access the table, but provide different access policies for each client.</span></span>

<span data-ttu-id="95111-245">Un elenco di controllo di accesso viene implementato usando una matrice di criteri di accesso, con un ID associato a ogni criterio.</span><span class="sxs-lookup"><span data-stu-id="95111-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="95111-246">L'esempio seguente definisce due criteri, uno per 'user1' e uno per 'user2':</span><span class="sxs-lookup"><span data-stu-id="95111-246">The following example defines two policies, one for 'user1' and one for 'user2':</span></span>

```nodejs
var sharedAccessPolicy = {
  user1: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.QUERY,
    Start: startDate,
    Expiry: expiryDate
  },
  user2: {
    Permissions: azure.TableUtilities.SharedAccessPermissions.ADD,
    Start: startDate,
    Expiry: expiryDate
  }
};
```

<span data-ttu-id="95111-247">L'esempio seguente recupera l'elenco di controllo di accesso corrente per la tabella **hometasks** e quindi aggiunge i nuovi criteri tramite **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="95111-247">The following example gets the current ACL for the **hometasks** table, and then adds the new policies using **setTableAcl**.</span></span> <span data-ttu-id="95111-248">Risultato:</span><span class="sxs-lookup"><span data-stu-id="95111-248">This approach allows:</span></span>

```nodejs
var extend = require('extend');
tableSvc.getTableAcl('hometasks', function(error, result, response) {
if(!error){
    var newSignedIdentifiers = extend(true, result.signedIdentifiers, sharedAccessPolicy);
    tableSvc.setTableAcl('hometasks', newSignedIdentifiers, function(error, result, response){
      if(!error){
        // ACL set
      }
    });
  }
});
```

<span data-ttu-id="95111-249">Dopo avere impostato l'elenco di controllo di accesso, è possibile creare una firma di accesso condiviso in base all'ID di un criterio.</span><span class="sxs-lookup"><span data-stu-id="95111-249">Once the ACL has been set, you can then create a SAS based on the ID for a policy.</span></span> <span data-ttu-id="95111-250">Nell'esempio seguente viene creata una nuova firma di accesso condiviso per 'user2':</span><span class="sxs-lookup"><span data-stu-id="95111-250">The following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="95111-251">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="95111-251">Next steps</span></span>
<span data-ttu-id="95111-252">Per altre informazioni, vedere le risorse seguenti:</span><span class="sxs-lookup"><span data-stu-id="95111-252">For more information, see the following resources.</span></span>

* <span data-ttu-id="95111-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma gratuita di Microsoft che consente di rappresentare facilmente dati di Archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="95111-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you to work visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="95111-254">[Azure Storage SDK per Node](https://github.com/Azure/azure-storage-node) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="95111-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="95111-255">Centro per sviluppatori di Node.js</span><span class="sxs-lookup"><span data-stu-id="95111-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="95111-256">Creare e distribuire un'applicazione Node.js in un sito Web di Azure</span><span class="sxs-lookup"><span data-stu-id="95111-256">Create and deploy a Node.js application to an Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)