---
title: aaaHow toouse archiviazione tabelle di Azure da Node.js | Documenti Microsoft
description: Archiviare dati strutturati in un cloud di hello tramite l'archiviazione tabelle di Azure, un archivio dati NoSQL.
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
ms.openlocfilehash: 990a71337b806d759d0277a7691712346db7b355
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-azure-table-storage-from-nodejs"></a><span data-ttu-id="17fa8-103">Come toouse archiviazione tabelle di Azure da Node.js</span><span class="sxs-lookup"><span data-stu-id="17fa8-103">How toouse Azure Table storage from Node.js</span></span>
[!INCLUDE [storage-selector-table-include](../../includes/storage-selector-table-include.md)]
[!INCLUDE [storage-table-cosmos-db-langsoon-tip-include](../../includes/storage-table-cosmos-db-langsoon-tip-include.md)]

## <a name="overview"></a><span data-ttu-id="17fa8-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="17fa8-104">Overview</span></span>
<span data-ttu-id="17fa8-105">Questo argomento viene illustrato come gli scenari comuni di tooperform utilizzando hello tabelle di Azure del servizio in un'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="17fa8-105">This topic shows how tooperform common scenarios using hello Azure Table service in a Node.js application.</span></span>

<span data-ttu-id="17fa8-106">esempi di codice Hello in questo argomento si presume che un'applicazione Node.js.</span><span class="sxs-lookup"><span data-stu-id="17fa8-106">hello code examples in this topic assume you already have a Node.js application.</span></span> <span data-ttu-id="17fa8-107">Per informazioni su come toocreate un'applicazione Node.js in Azure, vedere uno degli argomenti seguenti:</span><span class="sxs-lookup"><span data-stu-id="17fa8-107">For information about how toocreate a Node.js application in Azure, see any of these topics:</span></span>

* [<span data-ttu-id="17fa8-108">Creare un'app Web Node.js nel servizio app di Azure</span><span class="sxs-lookup"><span data-stu-id="17fa8-108">Create a Node.js web app in Azure App Service</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
* [<span data-ttu-id="17fa8-109">Compilare e distribuire un tooAzure di app web Node. js con WebMatrix</span><span class="sxs-lookup"><span data-stu-id="17fa8-109">Build and deploy a Node.js web app tooAzure using WebMatrix</span></span>](../app-service-web/web-sites-nodejs-use-webmatrix.md)
* <span data-ttu-id="17fa8-110">[Compilare e distribuire un tooan di applicazione del servizio Cloud di Azure Node.js](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (tramite Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="17fa8-110">[Build and deploy a Node.js application tooan Azure Cloud Service](../cloud-services/cloud-services-nodejs-develop-deploy-app.md) (using Windows PowerShell)</span></span>

[!INCLUDE [storage-table-concepts-include](../../includes/storage-table-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

## <a name="configure-your-application-tooaccess-azure-storage"></a><span data-ttu-id="17fa8-111">Configurare l'archiviazione di Azure di tooaccess applicazione</span><span class="sxs-lookup"><span data-stu-id="17fa8-111">Configure your application tooaccess Azure Storage</span></span>
<span data-ttu-id="17fa8-112">toouse archiviazione di Azure, è necessario hello Azure Storage SDK per Node.js, che include un set di librerie di praticità che comunicano con servizi REST di archiviazione hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-112">toouse Azure Storage, you need hello Azure Storage SDK for Node.js, which includes a set of convenience libraries that communicate with hello storage REST services.</span></span>

### <a name="use-node-package-manager-npm-tooinstall-hello-package"></a><span data-ttu-id="17fa8-113">Utilizzare un pacchetto di hello tooinstall nodo Package Manager (NPM)</span><span class="sxs-lookup"><span data-stu-id="17fa8-113">Use Node Package Manager (NPM) tooinstall hello package</span></span>
1. <span data-ttu-id="17fa8-114">Utilizzare un'interfaccia della riga di comando, ad esempio **PowerShell** (Windows), **Terminal** (Mac), o **Bash** (Unix) e passare toohello cartella in cui viene creata l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="17fa8-114">Use a command-line interface such as **PowerShell** (Windows), **Terminal** (Mac), or **Bash** (Unix), and navigate toohello folder where you created your application.</span></span>
2. <span data-ttu-id="17fa8-115">Tipo **npm installare archiviazione di azure** nella finestra di comando hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-115">Type **npm install azure-storage** in hello command window.</span></span> <span data-ttu-id="17fa8-116">Output del comando hello è simile toohello esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="17fa8-116">Output from hello command is similar toohello following example.</span></span>

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
3. <span data-ttu-id="17fa8-117">È possibile eseguire manualmente hello **ls** comando tooverify che un **nodo\_moduli** cartella è stata creata.</span><span class="sxs-lookup"><span data-stu-id="17fa8-117">You can manually run hello **ls** command tooverify that a **node\_modules** folder was created.</span></span> <span data-ttu-id="17fa8-118">Questa cartella si troverà hello **archiviazione di azure** pacchetto che contiene le librerie di hello tooaccess archiviazione necessarie.</span><span class="sxs-lookup"><span data-stu-id="17fa8-118">Inside that folder you will find hello **azure-storage** package, which contains hello libraries you need tooaccess storage.</span></span>

### <a name="import-hello-package"></a><span data-ttu-id="17fa8-119">Importa pacchetto di hello</span><span class="sxs-lookup"><span data-stu-id="17fa8-119">Import hello package</span></span>
<span data-ttu-id="17fa8-120">Aggiungere i seguenti hello cima toohello codice hello **server.js** file dell'applicazione:</span><span class="sxs-lookup"><span data-stu-id="17fa8-120">Add hello following code toohello top of hello **server.js** file in your application:</span></span>

```nodejs
var azure = require('azure-storage');
```

## <a name="set-up-an-azure-storage-connection"></a><span data-ttu-id="17fa8-121">Configurare una connessione di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="17fa8-121">Set up an Azure Storage connection</span></span>
<span data-ttu-id="17fa8-122">modulo Hello azure verrà lette le variabili di ambiente hello AZURE\_archiviazione\_ACCOUNT e AZURE\_archiviazione\_accesso\_chiave o AZURE\_archiviazione\_connessione \_Stringa per le informazioni necessarie tooconnect tooyour account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="17fa8-122">hello azure module will read hello environment variables AZURE\_STORAGE\_ACCOUNT and AZURE\_STORAGE\_ACCESS\_KEY, or AZURE\_STORAGE\_CONNECTION\_STRING for information required tooconnect tooyour Azure storage account.</span></span> <span data-ttu-id="17fa8-123">Se non vengono impostate queste variabili di ambiente, è necessario specificare le informazioni sull'account hello quando si chiama **TableService**.</span><span class="sxs-lookup"><span data-stu-id="17fa8-123">If these environment variables are not set, you must specify hello account information when calling **TableService**.</span></span>

<span data-ttu-id="17fa8-124">Per un esempio di impostazione delle variabili di ambiente hello in hello [portale di Azure](https://portal.azure.com) per un sito Web di Azure, vedere [app web Node. js utilizzando hello del servizio tabelle di Azure](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span><span class="sxs-lookup"><span data-stu-id="17fa8-124">For an example of setting hello environment variables in hello [Azure portal](https://portal.azure.com) for an Azure Website, see [Node.js web app using hello Azure Table Service](../app-service-web/storage-nodejs-use-table-storage-web-site.md).</span></span>

## <a name="create-a-table"></a><span data-ttu-id="17fa8-125">Creare una tabella</span><span class="sxs-lookup"><span data-stu-id="17fa8-125">Create a table</span></span>
<span data-ttu-id="17fa8-126">Hello codice seguente viene creata una **TableService** dell'oggetto e lo usa toocreate una nuova tabella.</span><span class="sxs-lookup"><span data-stu-id="17fa8-126">hello following code creates a **TableService** object and uses it toocreate a new table.</span></span> <span data-ttu-id="17fa8-127">Aggiungere il seguente hello parte superiore di hello di **server.js**.</span><span class="sxs-lookup"><span data-stu-id="17fa8-127">Add hello following near hello top of **server.js**.</span></span>

```nodejs
var tableSvc = azure.createTableService();
```

<span data-ttu-id="17fa8-128">Hello chiamata troppo**createTableIfNotExists** creerà una nuova tabella con il nome specificato hello se non esiste già.</span><span class="sxs-lookup"><span data-stu-id="17fa8-128">hello call too**createTableIfNotExists** will create a new table with hello specified name if it does not already exist.</span></span> <span data-ttu-id="17fa8-129">Hello esempio seguente viene creata una nuova tabella denominata "mytable" Se non esiste già:</span><span class="sxs-lookup"><span data-stu-id="17fa8-129">hello following example creates a new table named 'mytable' if it does not already exist:</span></span>

```nodejs
tableSvc.createTableIfNotExists('mytable', function(error, result, response){
  if(!error){
    // Table exists or created
  }
});
```

<span data-ttu-id="17fa8-130">Hello `result.created` sarà `true` se viene creata una nuova tabella, e `false` hello tabella esiste già.</span><span class="sxs-lookup"><span data-stu-id="17fa8-130">hello `result.created` will be `true` if a new table is created, and `false` if hello table already exists.</span></span> <span data-ttu-id="17fa8-131">Hello `response` contengono informazioni sulla richiesta di hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-131">hello `response` will contain information about hello request.</span></span>

### <a name="filters"></a><span data-ttu-id="17fa8-132">Filtri</span><span class="sxs-lookup"><span data-stu-id="17fa8-132">Filters</span></span>
<span data-ttu-id="17fa8-133">Operazioni di filtro facoltative possono essere applicato toooperations eseguita utilizzando **TableService**.</span><span class="sxs-lookup"><span data-stu-id="17fa8-133">Optional filtering operations can be applied toooperations performed using **TableService**.</span></span> <span data-ttu-id="17fa8-134">Le operazioni di filtro possono includere la registrazione, la ripetizione automatica dei tentativi e così via. I filtri sono oggetti che implementano un metodo con firma hello:</span><span class="sxs-lookup"><span data-stu-id="17fa8-134">Filtering operations can include logging, automatically retrying, etc. Filters are objects that implement a method with hello signature:</span></span>

```nodejs
function handle (requestOptions, next)
```

<span data-ttu-id="17fa8-135">Dopo aver eseguito il pre-elaborazione sulle opzioni di richiesta di hello, metodo hello deve toocall "Avanti", il passaggio di un callback con hello seguente firma:</span><span class="sxs-lookup"><span data-stu-id="17fa8-135">After doing its preprocessing on hello request options, hello method needs toocall "next", passing a callback with hello following signature:</span></span>

```nodejs
function (returnObject, finalCallback, next)
```

<span data-ttu-id="17fa8-136">In questo callback e dopo l'elaborazione di hello returnObject (risposta hello dal server di hello richiesta toohello), il callback di hello richiede tooeither richiamare successivamente se esiste l'elaborazione di altri filtri toocontinue o semplicemente richiamare finalCallback hello tooend in caso contrario chiamata del servizio.</span><span class="sxs-lookup"><span data-stu-id="17fa8-136">In this callback, and after processing hello returnObject (hello response from hello request toohello server), hello callback needs tooeither invoke next if it exists toocontinue processing other filters or simply invoke finalCallback otherwise tooend hello service invocation.</span></span>

<span data-ttu-id="17fa8-137">Due filtri, che implementano la logica di ripetizione sono inclusi in Azure SDK per Node.js, hello **ExponentialRetryPolicyFilter** e **LinearRetryPolicyFilter**.</span><span class="sxs-lookup"><span data-stu-id="17fa8-137">Two filters that implement retry logic are included with hello Azure SDK for Node.js, **ExponentialRetryPolicyFilter** and **LinearRetryPolicyFilter**.</span></span> <span data-ttu-id="17fa8-138">Hello seguito creato un **TableService** oggetto che utilizza hello **ExponentialRetryPolicyFilter**:</span><span class="sxs-lookup"><span data-stu-id="17fa8-138">hello following creates a **TableService** object that uses hello **ExponentialRetryPolicyFilter**:</span></span>

```nodejs
var retryOperations = new azure.ExponentialRetryPolicyFilter();
var tableSvc = azure.createTableService().withFilter(retryOperations);
```

## <a name="add-an-entity-tooa-table"></a><span data-ttu-id="17fa8-139">Aggiungere una tabella tooa entità</span><span class="sxs-lookup"><span data-stu-id="17fa8-139">Add an entity tooa table</span></span>
<span data-ttu-id="17fa8-140">tooadd un'entità, creare innanzitutto un oggetto che definisce le proprietà dell'entità.</span><span class="sxs-lookup"><span data-stu-id="17fa8-140">tooadd an entity, first create an object that defines your entity properties.</span></span> <span data-ttu-id="17fa8-141">Tutte le entità devono contenere un **PartitionKey** e **RowKey**, che sono identificatori univoci per l'entità hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-141">All entities must contain a **PartitionKey** and **RowKey**, which are unique identifiers for hello entity.</span></span>

* <span data-ttu-id="17fa8-142">**PartitionKey** -determina partizione hello archiviati in entità hello</span><span class="sxs-lookup"><span data-stu-id="17fa8-142">**PartitionKey** - determines hello partition that hello entity is stored in</span></span>
* <span data-ttu-id="17fa8-143">**RowKey** : in modo univoco identifica hello entità all'interno della partizione hello</span><span class="sxs-lookup"><span data-stu-id="17fa8-143">**RowKey** - uniquely identifies hello entity within hello partition</span></span>

<span data-ttu-id="17fa8-144">Sia **PartitionKey** che **RowKey** devono essere valori stringa.</span><span class="sxs-lookup"><span data-stu-id="17fa8-144">Both **PartitionKey** and **RowKey** must be string values.</span></span> <span data-ttu-id="17fa8-145">Per ulteriori informazioni, vedere [hello comprensione modello di dati del servizio tabelle](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="17fa8-145">For more information, see [Understanding hello Table Service Data Model](http://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

<span data-ttu-id="17fa8-146">Hello Ecco un esempio di definizione di un'entità.</span><span class="sxs-lookup"><span data-stu-id="17fa8-146">hello following is an example of defining an entity.</span></span> <span data-ttu-id="17fa8-147">**dueDate** è definito come tipo di **Edm.DateTime**.</span><span class="sxs-lookup"><span data-stu-id="17fa8-147">Note that **dueDate** is defined as a type of **Edm.DateTime**.</span></span> <span data-ttu-id="17fa8-148">Specifica il tipo hello è facoltativo e tipi verranno dedotto se non specificati.</span><span class="sxs-lookup"><span data-stu-id="17fa8-148">Specifying hello type is optional, and types will be inferred if not specified.</span></span>

```nodejs
var task = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20), '$':'Edm.DateTime'}
};
```

> [!NOTE]
> <span data-ttu-id="17fa8-149">Per ogni record è anche presente un campo **Timestamp** , impostato da Azure quando viene inserita o aggiornata un'entità.</span><span class="sxs-lookup"><span data-stu-id="17fa8-149">There is also a **Timestamp** field for each record, which is set by Azure when an entity is inserted or updated.</span></span>
>
>

<span data-ttu-id="17fa8-150">È inoltre possibile utilizzare hello **entityGenerator** toocreate entità.</span><span class="sxs-lookup"><span data-stu-id="17fa8-150">You can also use hello **entityGenerator** toocreate entities.</span></span> <span data-ttu-id="17fa8-151">esempio Hello crea hello stessa entità di attività utilizzando hello **entityGenerator**.</span><span class="sxs-lookup"><span data-stu-id="17fa8-151">hello following example creates hello same task entity using hello **entityGenerator**.</span></span>

```nodejs
var entGen = azure.TableUtilities.entityGenerator;
var task = {
  PartitionKey: entGen.String('hometasks'),
  RowKey: entGen.String('1'),
  description: entGen.String('take out hello trash'),
  dueDate: entGen.DateTime(new Date(Date.UTC(2015, 6, 20))),
};
```

<span data-ttu-id="17fa8-152">una tabella, tooyour entità tooadd passare hello entità oggetto toohello **insertEntity** metodo.</span><span class="sxs-lookup"><span data-stu-id="17fa8-152">tooadd an entity tooyour table, pass hello entity object toohello **insertEntity** method.</span></span>

```nodejs
tableSvc.insertEntity('mytable',task, function (error, result, response) {
  if(!error){
    // Entity inserted
  }
});
```

<span data-ttu-id="17fa8-153">Se ha esito positivo, operazione hello `result` conterrà hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) di hello inserire record e `response` conterrà informazioni sull'operazione hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-153">If hello operation is successful, `result` will contain hello [ETag](http://en.wikipedia.org/wiki/HTTP_ETag) of hello inserted record and `response` will contain information about hello operation.</span></span>

<span data-ttu-id="17fa8-154">Esempio di risposta:</span><span class="sxs-lookup"><span data-stu-id="17fa8-154">Example response:</span></span>

```nodejs
{ '.metadata': { etag: 'W/"datetime\'2015-02-25T01%3A22%3A22.5Z\'"' } }
```

> [!NOTE]
> <span data-ttu-id="17fa8-155">Per impostazione predefinita, **insertEntity** non restituisce entità hello inserito come parte di hello `response` informazioni.</span><span class="sxs-lookup"><span data-stu-id="17fa8-155">By default, **insertEntity** does not return hello inserted entity as part of hello `response` information.</span></span> <span data-ttu-id="17fa8-156">Se si prevede di eseguire altre operazioni su questa entità o si desiderano informazioni hello toocache, può essere utile toohave restituita come parte di hello `result`.</span><span class="sxs-lookup"><span data-stu-id="17fa8-156">If you plan on performing other operations on this entity, or wish toocache hello information, it can be useful toohave it returned as part of hello `result`.</span></span> <span data-ttu-id="17fa8-157">A tale scopo, abilitare **echoContent** come segue:</span><span class="sxs-lookup"><span data-stu-id="17fa8-157">You can do this by enabling **echoContent** as follows:</span></span>
>
> `tableSvc.insertEntity('mytable', task, {echoContent: true}, function (error, result, response) {...}`
>
>

## <a name="update-an-entity"></a><span data-ttu-id="17fa8-158">Aggiornare un'entità</span><span class="sxs-lookup"><span data-stu-id="17fa8-158">Update an entity</span></span>
<span data-ttu-id="17fa8-159">Esistono più tooupdate disponibili di metodi un'entità esistente:</span><span class="sxs-lookup"><span data-stu-id="17fa8-159">There are multiple methods available tooupdate an existing entity:</span></span>

* <span data-ttu-id="17fa8-160">**replaceEntity** : aggiorna un'entità esistente sostituendola</span><span class="sxs-lookup"><span data-stu-id="17fa8-160">**replaceEntity** - updates an existing entity by replacing it</span></span>
* <span data-ttu-id="17fa8-161">**mergeEntity** -aggiorna un'entità esistente unendo nuovi valori della proprietà di entità esistente hello</span><span class="sxs-lookup"><span data-stu-id="17fa8-161">**mergeEntity** - updates an existing entity by merging new property values into hello existing entity</span></span>
* <span data-ttu-id="17fa8-162">**insertOrReplaceEntity** : aggiorna un'entità esistente sostituendola.</span><span class="sxs-lookup"><span data-stu-id="17fa8-162">**insertOrReplaceEntity** - updates an existing entity by replacing it.</span></span> <span data-ttu-id="17fa8-163">Se non esiste alcuna entità, ne verrà inserita una nuova.</span><span class="sxs-lookup"><span data-stu-id="17fa8-163">If no entity exists, a new one will be inserted</span></span>
* <span data-ttu-id="17fa8-164">**insertOrMergeEntity** -aggiorna un'entità esistente mediante l'unione di nuovi valori della proprietà in hello esistente.</span><span class="sxs-lookup"><span data-stu-id="17fa8-164">**insertOrMergeEntity** - updates an existing entity by merging new property values into hello existing.</span></span> <span data-ttu-id="17fa8-165">Se non esiste alcuna entità, ne verrà inserita una nuova.</span><span class="sxs-lookup"><span data-stu-id="17fa8-165">If no entity exists, a new one will be inserted</span></span>

<span data-ttu-id="17fa8-166">Hello esempio seguente viene illustrato l'aggiornamento di un'entità mediante **replaceEntity**:</span><span class="sxs-lookup"><span data-stu-id="17fa8-166">hello following example demonstrates updating an entity using **replaceEntity**:</span></span>

```nodejs
tableSvc.replaceEntity('mytable', updatedTask, function(error, result, response){
  if(!error) {
    // Entity updated
  }
});
```

> [!NOTE]
> <span data-ttu-id="17fa8-167">Per impostazione predefinita, l'aggiornamento di un'entità non verifica toosee se i dati di hello in corso l'aggiornamento sono stati modificati in precedenza da un altro processo.</span><span class="sxs-lookup"><span data-stu-id="17fa8-167">By default, updating an entity does not check toosee if hello data being updated has previously been modified by another process.</span></span> <span data-ttu-id="17fa8-168">toosupport aggiornamenti simultanei:</span><span class="sxs-lookup"><span data-stu-id="17fa8-168">toosupport concurrent updates:</span></span>
>
> 1. <span data-ttu-id="17fa8-169">Ottenere hello ETag dell'oggetto hello in corso l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="17fa8-169">Get hello ETag of hello object being updated.</span></span> <span data-ttu-id="17fa8-170">Viene restituito come parte di hello `response` per qualsiasi operazione associati all'entità e possono essere recuperati tramite `response['.metadata'].etag`.</span><span class="sxs-lookup"><span data-stu-id="17fa8-170">This is returned as part of hello `response` for any entity-related operation and can be retrieved through `response['.metadata'].etag`.</span></span>
> 2. <span data-ttu-id="17fa8-171">Quando si esegue un'operazione di aggiornamento su un'entità, aggiungere le informazioni di ETag hello precedentemente recuperati toohello nuova entità.</span><span class="sxs-lookup"><span data-stu-id="17fa8-171">When performing an update operation on an entity, add hello ETag information previously retrieved toohello new entity.</span></span> <span data-ttu-id="17fa8-172">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="17fa8-172">For example:</span></span>
>
>       <span data-ttu-id="17fa8-173">entity2['.metadata'].etag = currentEtag;</span><span class="sxs-lookup"><span data-stu-id="17fa8-173">entity2['.metadata'].etag = currentEtag;</span></span>
> 3. <span data-ttu-id="17fa8-174">Eseguire l'operazione di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-174">Perform hello update operation.</span></span> <span data-ttu-id="17fa8-175">Se l'entità di hello è stata modificata poiché è stato recuperato valore ETag hello, ad esempio un'altra istanza dell'applicazione, un `error` verranno restituite che informa che condizione aggiornamento hello specificato nella richiesta di hello non è stata soddisfatta.</span><span class="sxs-lookup"><span data-stu-id="17fa8-175">If hello entity has been modified since you retrieved hello ETag value, such as another instance of your application, an `error` will be returned stating that hello update condition specified in hello request was not satisfied.</span></span>
>
>

<span data-ttu-id="17fa8-176">Con **replaceEntity** e **mergeEntity**, se l'entità hello in corso di aggiornamento non esiste, l'operazione di aggiornamento hello avrà esito negativo.</span><span class="sxs-lookup"><span data-stu-id="17fa8-176">With **replaceEntity** and **mergeEntity**, if hello entity that is being updated doesn't exist, then hello update operation will fail.</span></span> <span data-ttu-id="17fa8-177">Pertanto se si desidera toostore un'entità indipendentemente dal fatto se esiste già, utilizzare **insertOrReplaceEntity** o **insertOrMergeEntity**.</span><span class="sxs-lookup"><span data-stu-id="17fa8-177">Therefore if you wish toostore an entity regardless of whether it already exists, use **insertOrReplaceEntity** or **insertOrMergeEntity**.</span></span>

<span data-ttu-id="17fa8-178">Hello `result` per l'aggiornamento ha esito positivo operazioni conterrà hello **Etag** di hello aggiornato l'entità.</span><span class="sxs-lookup"><span data-stu-id="17fa8-178">hello `result` for successful update operations will contain hello **Etag** of hello updated entity.</span></span>

## <a name="work-with-groups-of-entities"></a><span data-ttu-id="17fa8-179">Usare i gruppi di entità</span><span class="sxs-lookup"><span data-stu-id="17fa8-179">Work with groups of entities</span></span>
<span data-ttu-id="17fa8-180">A volte risulta più toosubmit senso più operazioni contemporaneamente in un batch tooensure atomica elaborazione dal server hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-180">Sometimes it makes sense toosubmit multiple operations together in a batch tooensure atomic processing by hello server.</span></span> <span data-ttu-id="17fa8-181">tooaccomplish utilizzati, hello **TableBatch** classe toocreate un batch e quindi utilizzare hello **executeBatch** metodo **TableService** tooperform hello operazioni in batch.</span><span class="sxs-lookup"><span data-stu-id="17fa8-181">tooaccomplish that, use hello **TableBatch** class toocreate a batch, and then use hello **executeBatch** method of **TableService** tooperform hello batched operations.</span></span>

 <span data-ttu-id="17fa8-182">Hello di esempio seguente viene illustrato l'invio di due entità in un batch:</span><span class="sxs-lookup"><span data-stu-id="17fa8-182">hello following example demonstrates submitting two entities in a batch:</span></span>

```nodejs
var task1 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '1'},
  description: {'_':'Take out hello trash'},
  dueDate: {'_':new Date(2015, 6, 20)}
};
var task2 = {
  PartitionKey: {'_':'hometasks'},
  RowKey: {'_': '2'},
  description: {'_':'Wash hello dishes'},
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

<span data-ttu-id="17fa8-183">Per le operazioni batch ha esito positivo, `result` conterrà informazioni per ogni operazione nel batch hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-183">For successful batch operations, `result` will contain information for each operation in hello batch.</span></span>

### <a name="work-with-batched-operations"></a><span data-ttu-id="17fa8-184">Uso delle operazioni in batch</span><span class="sxs-lookup"><span data-stu-id="17fa8-184">Work with batched operations</span></span>
<span data-ttu-id="17fa8-185">Aggiungere le operazioni batch tooa può essere controllato da visualizzazione hello `operations` proprietà.</span><span class="sxs-lookup"><span data-stu-id="17fa8-185">Operations added tooa batch can be inspected by viewing hello `operations` property.</span></span> <span data-ttu-id="17fa8-186">È inoltre possibile utilizzare hello toowork metodi con le operazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="17fa8-186">You can also use hello following methods toowork with operations:</span></span>

* <span data-ttu-id="17fa8-187">**clear** : cancella tutte le operazioni da un batch.</span><span class="sxs-lookup"><span data-stu-id="17fa8-187">**clear** - clears all operations from a batch</span></span>
* <span data-ttu-id="17fa8-188">**getOperations** -Ottiene un'operazione batch hello</span><span class="sxs-lookup"><span data-stu-id="17fa8-188">**getOperations** - gets an operation from hello batch</span></span>
* <span data-ttu-id="17fa8-189">**hasOperations** -restituisce true se il batch hello contiene operazioni</span><span class="sxs-lookup"><span data-stu-id="17fa8-189">**hasOperations** - returns true if hello batch contains operations</span></span>
* <span data-ttu-id="17fa8-190">**removeOperations** : rimuove un'operazione.</span><span class="sxs-lookup"><span data-stu-id="17fa8-190">**removeOperations** - removes an operation</span></span>
* <span data-ttu-id="17fa8-191">**dimensioni** -restituisce hello numero di operazioni in batch hello</span><span class="sxs-lookup"><span data-stu-id="17fa8-191">**size** - returns hello number of operations in hello batch</span></span>

## <a name="retrieve-an-entity-by-key"></a><span data-ttu-id="17fa8-192">Recuperare un'entità in base alla chiave</span><span class="sxs-lookup"><span data-stu-id="17fa8-192">Retrieve an entity by key</span></span>
<span data-ttu-id="17fa8-193">un'entità specifica in base a hello tooreturn **PartitionKey** e **RowKey**, utilizzare hello **retrieveEntity** metodo.</span><span class="sxs-lookup"><span data-stu-id="17fa8-193">tooreturn a specific entity based on hello **PartitionKey** and **RowKey**, use hello **retrieveEntity** method.</span></span>

```nodejs
tableSvc.retrieveEntity('mytable', 'hometasks', '1', function(error, result, response){
  if(!error){
    // result contains hello entity
  }
});
```

<span data-ttu-id="17fa8-194">Dopo aver completata questa operazione `result` conterrà entità hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-194">Once this operation is complete, `result` will contain hello entity.</span></span>

## <a name="query-a-set-of-entities"></a><span data-ttu-id="17fa8-195">Eseguire query su un set di entità</span><span class="sxs-lookup"><span data-stu-id="17fa8-195">Query a set of entities</span></span>
<span data-ttu-id="17fa8-196">tooquery una tabella, utilizzare hello **TableQuery** oggetto toobuild di un'espressione di query utilizzando hello clausole seguenti:</span><span class="sxs-lookup"><span data-stu-id="17fa8-196">tooquery a table, use hello **TableQuery** object toobuild up a query expression using hello following clauses:</span></span>

* <span data-ttu-id="17fa8-197">**Selezionare** -hello campi toobe restituito dalla query hello</span><span class="sxs-lookup"><span data-stu-id="17fa8-197">**select** - hello fields toobe returned from hello query</span></span>
* <span data-ttu-id="17fa8-198">**dove** : hello dove clausola</span><span class="sxs-lookup"><span data-stu-id="17fa8-198">**where** - hello where clause</span></span>

  * <span data-ttu-id="17fa8-199">**and**: una condizione where`and`.</span><span class="sxs-lookup"><span data-stu-id="17fa8-199">**and** - an `and` where condition</span></span>
  * <span data-ttu-id="17fa8-200">**or**: una condizione where `or`.</span><span class="sxs-lookup"><span data-stu-id="17fa8-200">**or** - an `or` where condition</span></span>
* <span data-ttu-id="17fa8-201">**inizio** -numero di elementi toofetch hello</span><span class="sxs-lookup"><span data-stu-id="17fa8-201">**top** - hello number of items toofetch</span></span>

<span data-ttu-id="17fa8-202">Hello esempio seguente viene compilata una query che verrà restituiti hello primi cinque elementi con un PartitionKey di 'hometasks'.</span><span class="sxs-lookup"><span data-stu-id="17fa8-202">hello following example builds a query that will return hello top five items with a PartitionKey of 'hometasks'.</span></span>

```nodejs
var query = new azure.TableQuery()
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

<span data-ttu-id="17fa8-203">Poiché **select** non viene usato, vengono restituiti tutti i campi.</span><span class="sxs-lookup"><span data-stu-id="17fa8-203">Since **select** is not used, all fields will be returned.</span></span> <span data-ttu-id="17fa8-204">una tabella, utilizzare query hello tooperform **queryEntities**.</span><span class="sxs-lookup"><span data-stu-id="17fa8-204">tooperform hello query against a table, use **queryEntities**.</span></span> <span data-ttu-id="17fa8-205">Hello seguente viene utilizzata questa entità tooreturn query da "mytable".</span><span class="sxs-lookup"><span data-stu-id="17fa8-205">hello following example uses this query tooreturn entities from 'mytable'.</span></span>

```nodejs
tableSvc.queryEntities('mytable',query, null, function(error, result, response) {
  if(!error) {
    // query was successful
  }
});
```

<span data-ttu-id="17fa8-206">Se ha esito positivo, `result.entries` conterrà una matrice di entità che soddisfano la query hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-206">If successful, `result.entries` will contain an array of entities that match hello query.</span></span> <span data-ttu-id="17fa8-207">Se non è possibile tooreturn query hello tutte le entità, `result.continuationToken` sarà non*null* e può essere utilizzato come terzo parametro del hello **queryEntities** tooretrieve altri risultati.</span><span class="sxs-lookup"><span data-stu-id="17fa8-207">If hello query was unable tooreturn all entities, `result.continuationToken` will be non-*null* and can be used as hello third parameter of **queryEntities** tooretrieve more results.</span></span> <span data-ttu-id="17fa8-208">Per le query iniziale hello, utilizzare *null* per terzo parametro hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-208">For hello initial query, use *null* for hello third parameter.</span></span>

### <a name="query-a-subset-of-entity-properties"></a><span data-ttu-id="17fa8-209">Eseguire query su un subset di proprietà di entità</span><span class="sxs-lookup"><span data-stu-id="17fa8-209">Query a subset of entity properties</span></span>
<span data-ttu-id="17fa8-210">Una tabella di tooa query è possibile recuperare un numero ridotto di campi da un'entità.</span><span class="sxs-lookup"><span data-stu-id="17fa8-210">A query tooa table can retrieve just a few fields from an entity.</span></span>
<span data-ttu-id="17fa8-211">Questa tecnica permette di ridurre la larghezza di banda e di migliorare le prestazioni della query, in particolare per entità di grandi dimensioni.</span><span class="sxs-lookup"><span data-stu-id="17fa8-211">This reduces bandwidth and can improve query performance, especially for large entities.</span></span> <span data-ttu-id="17fa8-212">Hello utilizzare **selezionare** clausola e passare i nomi di hello campi toobe hello restituiti.</span><span class="sxs-lookup"><span data-stu-id="17fa8-212">Use hello **select** clause and pass hello names of hello fields toobe returned.</span></span> <span data-ttu-id="17fa8-213">Ad esempio, hello query seguente restituirà solo hello **descrizione** e **dueDate** campi.</span><span class="sxs-lookup"><span data-stu-id="17fa8-213">For example, hello following query will return only hello **description** and **dueDate** fields.</span></span>

```nodejs
var query = new azure.TableQuery()
  .select(['description', 'dueDate'])
  .top(5)
  .where('PartitionKey eq ?', 'hometasks');
```

## <a name="delete-an-entity"></a><span data-ttu-id="17fa8-214">Eliminare un'entità</span><span class="sxs-lookup"><span data-stu-id="17fa8-214">Delete an entity</span></span>
<span data-ttu-id="17fa8-215">È possibile eliminare un'entità utilizzando le relative chiavi di riga e di partizione.</span><span class="sxs-lookup"><span data-stu-id="17fa8-215">You can delete an entity using its partition and row keys.</span></span> <span data-ttu-id="17fa8-216">In questo esempio hello **Attività1** oggetto contiene hello **RowKey** e **PartitionKey** valori di hello entità toobe eliminato.</span><span class="sxs-lookup"><span data-stu-id="17fa8-216">In this example, hello **task1** object contains hello **RowKey** and **PartitionKey** values of hello entity toobe deleted.</span></span> <span data-ttu-id="17fa8-217">L'oggetto hello è passato toohello **deleteEntity** metodo.</span><span class="sxs-lookup"><span data-stu-id="17fa8-217">Then hello object is passed toohello **deleteEntity** method.</span></span>

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
> <span data-ttu-id="17fa8-218">È consigliabile utilizzare valori eTag durante l'eliminazione di elementi, tooensure che hello elemento non è stato modificato da un altro processo.</span><span class="sxs-lookup"><span data-stu-id="17fa8-218">Consider using ETags when deleting items, tooensure that hello item hasn't been modified by another process.</span></span> <span data-ttu-id="17fa8-219">Vedere [Aggiornare un'entità](#update-an-entity) per informazioni sull'uso di ETag.</span><span class="sxs-lookup"><span data-stu-id="17fa8-219">See [Update an entity](#update-an-entity) for information on using ETags.</span></span>
>
>

## <a name="delete-a-table"></a><span data-ttu-id="17fa8-220">Eliminare una tabella</span><span class="sxs-lookup"><span data-stu-id="17fa8-220">Delete a table</span></span>
<span data-ttu-id="17fa8-221">Hello di codice seguente elimina una tabella da un account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="17fa8-221">hello following code deletes a table from a storage account.</span></span>

```nodejs
tableSvc.deleteTable('mytable', function(error, response){
    if(!error){
        // Table deleted
    }
});
```

<span data-ttu-id="17fa8-222">Se non si è certi se la tabella hello esiste, utilizzare **deleteTableIfExists**.</span><span class="sxs-lookup"><span data-stu-id="17fa8-222">If you are uncertain whether hello table exists, use **deleteTableIfExists**.</span></span>

## <a name="use-continuation-tokens"></a><span data-ttu-id="17fa8-223">Utilizzare i token di continuazione</span><span class="sxs-lookup"><span data-stu-id="17fa8-223">Use continuation tokens</span></span>
<span data-ttu-id="17fa8-224">Quando si esegue una query di tabelle di grandi quantità di risultati, ricercare i token di continuazione.</span><span class="sxs-lookup"><span data-stu-id="17fa8-224">When you are querying tables for large amounts of results, look for continuation tokens.</span></span> <span data-ttu-id="17fa8-225">Potrebbero essere disponibili per la query che si potrebbero non essere consapevoli se toorecognize non compilato quando è presente un token di continuazione grandi quantità di dati.</span><span class="sxs-lookup"><span data-stu-id="17fa8-225">There may be large amounts of data available for your query that you might not realize if you do not build toorecognize when a continuation token is present.</span></span>

<span data-ttu-id="17fa8-226">risultati Hello restituiti durante l'esecuzione di query su set di entità dell'oggetto un `continuationToken` proprietà quando è presente un token di questo tipo.</span><span class="sxs-lookup"><span data-stu-id="17fa8-226">hello results object returned during querying entities sets a `continuationToken` property when such a token is present.</span></span> <span data-ttu-id="17fa8-227">È quindi possibile utilizzare questo durante l'esecuzione di un toomove toocontinue query tra le entità di partizione e la tabella hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-227">You can then use this when performing a query toocontinue toomove across hello partition and table entities.</span></span>

<span data-ttu-id="17fa8-228">Quando si eseguono query, è possibile specificare un parametro continuationToken tra l'istanza dell'oggetto query hello e funzione di callback hello:</span><span class="sxs-lookup"><span data-stu-id="17fa8-228">When querying, a continuationToken parameter may be provided between hello query object instance and hello callback function:</span></span>

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

<span data-ttu-id="17fa8-229">Se si analizza hello `continuationToken` oggetto, sono disponibili le proprietà, ad esempio `nextPartitionKey`, `nextRowKey` e `targetLocation`, che può essere utilizzato tooiterate tramite tutti i risultati di hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-229">If you inspect hello `continuationToken` object, you will find properties such as `nextPartitionKey`, `nextRowKey` and `targetLocation`, which can be used tooiterate through all hello results.</span></span>

<span data-ttu-id="17fa8-230">È inoltre disponibile un esempio di continuazione in repository di hello Azure Storage Node.js su GitHub.</span><span class="sxs-lookup"><span data-stu-id="17fa8-230">There is also a continuation sample within hello Azure Storage Node.js repo on GitHub.</span></span> <span data-ttu-id="17fa8-231">Cercare `examples/samples/continuationsample.js`.</span><span class="sxs-lookup"><span data-stu-id="17fa8-231">Look for `examples/samples/continuationsample.js`.</span></span>

## <a name="work-with-shared-access-signatures"></a><span data-ttu-id="17fa8-232">Usare le firme di accesso condiviso di Azure</span><span class="sxs-lookup"><span data-stu-id="17fa8-232">Work with shared access signatures</span></span>
<span data-ttu-id="17fa8-233">Firme di accesso condiviso (SAS) sono un tootables di accesso granulare tooprovide in modo sicuro senza fornire il nome account di archiviazione o chiavi.</span><span class="sxs-lookup"><span data-stu-id="17fa8-233">Shared access signatures (SAS) are a secure way tooprovide granular access tootables without providing your storage account name or keys.</span></span> <span data-ttu-id="17fa8-234">Firma di accesso condiviso è spesso i dati tooyour di accesso utilizzato tooprovide limitate, ad esempio per consentire a un'app mobile tooquery record.</span><span class="sxs-lookup"><span data-stu-id="17fa8-234">SAS are often used tooprovide limited access tooyour data, such as allowing a mobile app tooquery records.</span></span>

<span data-ttu-id="17fa8-235">Un'applicazione attendibile, ad esempio un servizio basato su cloud genera una firma di accesso condiviso utilizzando hello **generateSharedAccessSignature** di hello **TableService**e fornisce tooan applicazione non attendibile o semi-trusted ad esempio un'app per dispositivi mobili.</span><span class="sxs-lookup"><span data-stu-id="17fa8-235">A trusted application such as a cloud-based service generates a SAS using hello **generateSharedAccessSignature** of hello **TableService**, and provides it tooan untrusted or semi-trusted application such as a mobile app.</span></span> <span data-ttu-id="17fa8-236">Hello firma di accesso condiviso viene generato utilizzando un criterio, che descrive l'avvio di hello e fine in cui hello firma di accesso condiviso è valido, nonché hello titolare SAS toohello concesso livello di accesso.</span><span class="sxs-lookup"><span data-stu-id="17fa8-236">hello SAS is generated using a policy, which describes hello start and end dates during which hello SAS is valid, as well as hello access level granted toohello SAS holder.</span></span>

<span data-ttu-id="17fa8-237">Hello esempio seguente genera un nuovo criterio di accesso condiviso che consentirà di hello tabella hello SAS titolare tooquery ("r") e scade 100 minuti dopo il tempo di hello che viene creato.</span><span class="sxs-lookup"><span data-stu-id="17fa8-237">hello following example generates a new shared access policy that will allow hello SAS holder tooquery ('r') hello table, and expires 100 minutes after hello time it is created.</span></span>

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

<span data-ttu-id="17fa8-238">Si noti che le informazioni sull'host hello deve essere fornito, come richiesto quando titolare SAS hello tenta anche tabella hello tooaccess.</span><span class="sxs-lookup"><span data-stu-id="17fa8-238">Note that hello host information must be provided also, as it is required when hello SAS holder attempts tooaccess hello table.</span></span>

<span data-ttu-id="17fa8-239">Hello applicazione client, quindi Usa hello SAS con **TableServiceWithSAS** tooperform operazioni sulla tabella hello.</span><span class="sxs-lookup"><span data-stu-id="17fa8-239">hello client application then uses hello SAS with **TableServiceWithSAS** tooperform operations against hello table.</span></span> <span data-ttu-id="17fa8-240">Hello di esempio seguente si connette toohello tabella ed esegue una query.</span><span class="sxs-lookup"><span data-stu-id="17fa8-240">hello following example connects toohello table and performs a query.</span></span>

```nodejs
var sharedTableService = azure.createTableServiceWithSas(host, tableSAS);
var query = azure.TableQuery()
  .where('PartitionKey eq ?', 'hometasks');

sharedTableService.queryEntities(query, null, function(error, result, response) {
  if(!error) {
    // result contains hello entities
  }
});
```

<span data-ttu-id="17fa8-241">Poiché hello firma di accesso condiviso è stato generato con il solo accesso query, se un tentativo sono stato apportato tooinsert, aggiornare o eliminare le entità, verrà restituito un errore.</span><span class="sxs-lookup"><span data-stu-id="17fa8-241">Since hello SAS was generated with only query access, if an attempt were made tooinsert, update, or delete entities, an error would be returned.</span></span>

### <a name="access-control-lists"></a><span data-ttu-id="17fa8-242">Elenchi di controllo di accesso</span><span class="sxs-lookup"><span data-stu-id="17fa8-242">Access Control Lists</span></span>
<span data-ttu-id="17fa8-243">È inoltre possibile utilizzare un criterio di accesso hello tooset elenco di controllo di accesso (ACL) per una firma di accesso condiviso.</span><span class="sxs-lookup"><span data-stu-id="17fa8-243">You can also use an Access Control List (ACL) tooset hello access policy for a SAS.</span></span> <span data-ttu-id="17fa8-244">Ciò è utile se si desiderano tooallow più tabelle di hello tooaccess client, ma forniscono criteri di accesso diversi per ogni client.</span><span class="sxs-lookup"><span data-stu-id="17fa8-244">This is useful if you wish tooallow multiple clients tooaccess hello table, but provide different access policies for each client.</span></span>

<span data-ttu-id="17fa8-245">Un elenco di controllo di accesso viene implementato usando una matrice di criteri di accesso, con un ID associato a ogni criterio.</span><span class="sxs-lookup"><span data-stu-id="17fa8-245">An ACL is implemented using an array of access policies, with an ID associated with each policy.</span></span> <span data-ttu-id="17fa8-246">Hello di esempio seguente definisce due criteri, uno per "user1" e uno per 'Utente2':</span><span class="sxs-lookup"><span data-stu-id="17fa8-246">hello following example defines two policies, one for 'user1' and one for 'user2':</span></span>

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

<span data-ttu-id="17fa8-247">Hello seguente esempio ottiene hello gli ACL per hello **hometasks** tabella e quindi aggiunge nuovi criteri hello utilizzando **setTableAcl**.</span><span class="sxs-lookup"><span data-stu-id="17fa8-247">hello following example gets hello current ACL for hello **hometasks** table, and then adds hello new policies using **setTableAcl**.</span></span> <span data-ttu-id="17fa8-248">Risultato:</span><span class="sxs-lookup"><span data-stu-id="17fa8-248">This approach allows:</span></span>

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

<span data-ttu-id="17fa8-249">Una volta hello che ACL è stato impostato, è quindi possibile creare una firma di accesso condiviso in base all'ID di hello per un criterio.</span><span class="sxs-lookup"><span data-stu-id="17fa8-249">Once hello ACL has been set, you can then create a SAS based on hello ID for a policy.</span></span> <span data-ttu-id="17fa8-250">Hello di esempio seguente crea una nuova firma di accesso condiviso per 'Utente2':</span><span class="sxs-lookup"><span data-stu-id="17fa8-250">hello following example creates a new SAS for 'user2':</span></span>

```nodejs
tableSAS = tableSvc.generateSharedAccessSignature('hometasks', { Id: 'user2' });
```

## <a name="next-steps"></a><span data-ttu-id="17fa8-251">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="17fa8-251">Next steps</span></span>
<span data-ttu-id="17fa8-252">Per ulteriori informazioni, vedere hello seguenti risorse.</span><span class="sxs-lookup"><span data-stu-id="17fa8-252">For more information, see hello following resources.</span></span>

* <span data-ttu-id="17fa8-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) è un'app autonoma, disponibile da Microsoft che consente di toowork visivamente i dati di archiviazione di Azure in Windows, macOS e Linux.</span><span class="sxs-lookup"><span data-stu-id="17fa8-253">[Microsoft Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer.md) is a free, standalone app from Microsoft that enables you toowork visually with Azure Storage data on Windows, macOS, and Linux.</span></span>
* <span data-ttu-id="17fa8-254">[Azure Storage SDK per Node](https://github.com/Azure/azure-storage-node) su GitHub.</span><span class="sxs-lookup"><span data-stu-id="17fa8-254">[Azure Storage SDK for Node](https://github.com/Azure/azure-storage-node) repository on GitHub.</span></span>
* [<span data-ttu-id="17fa8-255">Centro per sviluppatori di Node. js</span><span class="sxs-lookup"><span data-stu-id="17fa8-255">Node.js Developer Center</span></span>](/develop/nodejs/)
* [<span data-ttu-id="17fa8-256">Creare e distribuire un tooan applicazione Node.js sito Web di Azure</span><span class="sxs-lookup"><span data-stu-id="17fa8-256">Create and deploy a Node.js application tooan Azure website</span></span>](../app-service-web/app-service-web-get-started-nodejs.md)
