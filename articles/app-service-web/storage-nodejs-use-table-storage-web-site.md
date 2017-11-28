---
title: app web aaaNode.js utilizzando hello del servizio tabelle di Azure
description: "Questa esercitazione viene illustrato come toouse hello Azure Table service toostore dati da un'applicazione Node.js che è ospitato in App Web di servizio App di Azure."
tags: azure-portal
services: app-service\web, storage
documentationcenter: nodejs
author: TomArcher
manager: routlaw
editor: 
ms.assetid: 029e6f46-f586-4309-adbf-71c7b8d537d4
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: article
ms.date: 08/17/2016
ms.author: tarcher
ms.openlocfilehash: f6e08335b4c7f62f7b3994287edd586860cb7135
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="nodejs-web-app-using-hello-azure-table-service"></a><span data-ttu-id="2df6c-103">App web Node. js utilizzando hello del servizio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="2df6c-103">Node.js web app using hello Azure Table Service</span></span>
## <a name="overview"></a><span data-ttu-id="2df6c-104">Panoramica</span><span class="sxs-lookup"><span data-stu-id="2df6c-104">Overview</span></span>
<span data-ttu-id="2df6c-105">Questa esercitazione viene illustrato come servizio tabelle toouse forniti da Gestione dati di Azure toostore e accedere ai dati da un [nodo] applicazione ospitata in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) App Web.</span><span class="sxs-lookup"><span data-stu-id="2df6c-105">This tutorial shows you how toouse Table service provided by Azure Data Management toostore and access data from a [node] application hosted in [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) Web Apps.</span></span> <span data-ttu-id="2df6c-106">In questa esercitazione si presuppone che l'utente abbia già utilizzato l'applicazione Node e [Git].</span><span class="sxs-lookup"><span data-stu-id="2df6c-106">This tutorial assumes that you have some prior experience using node and [Git].</span></span>

<span data-ttu-id="2df6c-107">Si acquisiranno le nozioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="2df6c-107">You will learn:</span></span>

* <span data-ttu-id="2df6c-108">Come toouse npm (gestione di pacchetti di nodi) tooinstall hello i moduli del nodo</span><span class="sxs-lookup"><span data-stu-id="2df6c-108">How toouse npm (node package manager) tooinstall hello node modules</span></span>
* <span data-ttu-id="2df6c-109">Come toowork con hello servizio tabelle di Azure</span><span class="sxs-lookup"><span data-stu-id="2df6c-109">How toowork with hello Azure Table service</span></span>
* <span data-ttu-id="2df6c-110">Come un'app web toouse hello toocreate CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="2df6c-110">How toouse hello Azure CLI toocreate a web app.</span></span>

<span data-ttu-id="2df6c-111">In questa esercitazione verrà creata una semplice applicazione di "elenco attività" basata su Web che consente di creare, recuperare e completare le attività.</span><span class="sxs-lookup"><span data-stu-id="2df6c-111">By following this tutorial, you will build a simple web-based "to-do list" application that allows creating, retrieving and completing tasks.</span></span> <span data-ttu-id="2df6c-112">attività Hello vengono archiviate nel servizio tabelle hello.</span><span class="sxs-lookup"><span data-stu-id="2df6c-112">hello tasks are stored in hello Table service.</span></span>

<span data-ttu-id="2df6c-113">Di seguito è riportata un'applicazione hello completata:</span><span class="sxs-lookup"><span data-stu-id="2df6c-113">Here is hello completed application:</span></span>

![Pagina Web con un elenco di attività vuoto][node-table-finished]

> [!NOTE]
> <span data-ttu-id="2df6c-115">Se si desidera tooget avviato con il servizio App di Azure prima di effettuare l'iscrizione per un account Azure, andare troppo[tenta di servizio App](https://azure.microsoft.com/try/app-service/), in cui è possibile creare subito un'app web di breve durata starter nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="2df6c-115">If you want tooget started with Azure App Service before signing up for an Azure account, go too[Try App Service](https://azure.microsoft.com/try/app-service/), where you can immediately create a short-lived starter web app in App Service.</span></span> <span data-ttu-id="2df6c-116">Non è necessario fornire una carta di credito né impegnarsi in alcun modo.</span><span class="sxs-lookup"><span data-stu-id="2df6c-116">No credit cards required; no commitments.</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="2df6c-117">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="2df6c-117">Prerequisites</span></span>
<span data-ttu-id="2df6c-118">Prima di seguire le istruzioni di hello in questo articolo, assicurarsi di aver installato quanto segue hello:</span><span class="sxs-lookup"><span data-stu-id="2df6c-118">Before following hello instructions in this article, ensure that you have hello following installed:</span></span>

* <span data-ttu-id="2df6c-119">[nodo] 0.10.24 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="2df6c-119">[node] version 0.10.24 or higher</span></span>
* <span data-ttu-id="2df6c-120">[Git]</span><span class="sxs-lookup"><span data-stu-id="2df6c-120">[Git]</span></span>

[!INCLUDE [create-account-and-websites-note](../../includes/create-account-and-websites-note.md)]

## <a name="create-a-storage-account"></a><span data-ttu-id="2df6c-121">Creare un account di archiviazione</span><span class="sxs-lookup"><span data-stu-id="2df6c-121">Create a storage account</span></span>
<span data-ttu-id="2df6c-122">Creare un account di archiviazione di Azure</span><span class="sxs-lookup"><span data-stu-id="2df6c-122">Create an Azure storage account.</span></span> <span data-ttu-id="2df6c-123">app Hello utilizzerà questa attività da svolgere hello toostore di account.</span><span class="sxs-lookup"><span data-stu-id="2df6c-123">hello app will use this account toostore hello to-do items.</span></span>

1. <span data-ttu-id="2df6c-124">Accedere al hello [portale Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2df6c-124">Log into hello [Azure Portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="2df6c-125">Fare clic su hello **New** sull'icona nella parte inferiore di hello sinistra del portale hello, quindi fare clic su **dati e archiviazione** > **archiviazione**.</span><span class="sxs-lookup"><span data-stu-id="2df6c-125">Click hello **New** icon on hello bottom left of hello portal, then click **Data + Storage** > **Storage**.</span></span> <span data-ttu-id="2df6c-126">Assegnare un nome univoco di account di archiviazione hello e creare un nuovo [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) relativo.</span><span class="sxs-lookup"><span data-stu-id="2df6c-126">Give hello storage account a unique name and create a new [resource group](../azure-resource-manager/resource-group-overview.md) for it.</span></span>
   
      ![Pulsante Nuovo](./media/storage-nodejs-use-table-storage-web-site/configure-storage.png)
   
    <span data-ttu-id="2df6c-128">Quando è stato creato l'account di archiviazione hello, hello **notifiche** pulsante farà lampeggiare una verde **esito positivo** ed è aperto il pannello dell'account di archiviazione hello gruppo tooshow appartiene toohello nuova risorsa creato.</span><span class="sxs-lookup"><span data-stu-id="2df6c-128">When hello storage account has been created, hello **Notifications** button will flash a green **SUCCESS** and hello storage account's blade is open tooshow that it belongs toohello new resource group you created.</span></span>
3. <span data-ttu-id="2df6c-129">Nel pannello hello account di archiviazione, fare clic su **impostazioni** > **chiavi**.</span><span class="sxs-lookup"><span data-stu-id="2df6c-129">In hello storage account's blade, click **Settings** > **Keys**.</span></span> <span data-ttu-id="2df6c-130">Copiare negli Appunti toohello chiave di accesso primaria hello.</span><span class="sxs-lookup"><span data-stu-id="2df6c-130">Copy hello primary access key toohello clipboard.</span></span>
   
    ![Chiave di accesso][portal-storage-access-keys]

## <a name="install-modules-and-generate-scaffolding"></a><span data-ttu-id="2df6c-132">Installazione dei moduli e generazione dello scaffolding</span><span class="sxs-lookup"><span data-stu-id="2df6c-132">Install modules and generate scaffolding</span></span>
<span data-ttu-id="2df6c-133">In questa sezione verrà di creare una nuova applicazione di nodo e utilizzare i pacchetti di npm tooadd modulo.</span><span class="sxs-lookup"><span data-stu-id="2df6c-133">In this section you will create a new Node application and use npm tooadd module packages.</span></span> <span data-ttu-id="2df6c-134">Per questa applicazione si utilizzerà hello [Express] e [Azure] moduli.</span><span class="sxs-lookup"><span data-stu-id="2df6c-134">For this application you will use hello [Express] and [Azure] modules.</span></span> <span data-ttu-id="2df6c-135">modulo Express Hello fornisce un framework di Model View Controller per nodo, mentre hello moduli di Azure fornisce servizio di integrazione applicativa toohello tabella.</span><span class="sxs-lookup"><span data-stu-id="2df6c-135">hello Express module provides a Model View Controller framework for node, while hello Azure modules provides connectivity toohello Table service.</span></span>

### <a name="install-express-and-generate-scaffolding"></a><span data-ttu-id="2df6c-136">Installare Express e generare lo scaffolding</span><span class="sxs-lookup"><span data-stu-id="2df6c-136">Install express and generate scaffolding</span></span>
1. <span data-ttu-id="2df6c-137">Dalla riga di comando hello, creare una nuova directory denominata **tasklist** e commutatore toothat directory.</span><span class="sxs-lookup"><span data-stu-id="2df6c-137">From hello command line, create a new directory named **tasklist** and switch toothat directory.</span></span>  
2. <span data-ttu-id="2df6c-138">Immettere hello seguente tooinstall hello Express il modulo.</span><span class="sxs-lookup"><span data-stu-id="2df6c-138">Enter hello following command tooinstall hello Express module.</span></span>
   
        npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="2df6c-139">A seconda del sistema operativo hello, potrebbe essere necessario tooput 'sudo' prima del comando hello:</span><span class="sxs-lookup"><span data-stu-id="2df6c-139">Depending on hello operating system, you may need tooput 'sudo' before hello command:</span></span>
   
        sudo npm install express-generator@4.2.0 -g
   
    <span data-ttu-id="2df6c-140">output di Hello visualizzato è simile toohello esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-140">hello output appears similar toohello following example:</span></span>
   
        express-generator@4.2.0 /usr/local/lib/node_modules/express-generator
        ├── mkdirp@0.3.5
        └── commander@1.3.2 (keypress@0.1.0)
   
   > [!NOTE]
   > <span data-ttu-id="2df6c-141">Hello '-g' parametro Installa modulo hello a livello globale.</span><span class="sxs-lookup"><span data-stu-id="2df6c-141">hello '-g' parameter installs hello module globally.</span></span> <span data-ttu-id="2df6c-142">In questo modo, è possibile utilizzare **express** lo scaffolding di app web toogenerate senza tootype in informazioni aggiuntive sul percorso.</span><span class="sxs-lookup"><span data-stu-id="2df6c-142">That way, we can use **express** toogenerate web app scaffolding without having tootype in additional path information.</span></span>
   > 
   > 
3. <span data-ttu-id="2df6c-143">lo scaffolding di hello toocreate per un'applicazione hello, immettere hello **express** comando:</span><span class="sxs-lookup"><span data-stu-id="2df6c-143">toocreate hello scaffolding for hello application, enter hello **express** command:</span></span>
   
        express
   
    <span data-ttu-id="2df6c-144">output di Hello di questo comando viene visualizzato toohello simile esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-144">hello output of this command appears similar toohello following example:</span></span>
   
           create : .
           create : ./package.json
           create : ./app.js
           create : ./public
           create : ./public/images
           create : ./routes
           create : ./routes/index.js
           create : ./routes/users.js
           create : ./public/stylesheets
           create : ./public/stylesheets/style.css
           create : ./views
           create : ./views/index.jade
           create : ./views/layout.jade
           create : ./views/error.jade
           create : ./public/javascripts
           create : ./bin
           create : ./bin/www
   
           install dependencies:
             $ cd . && npm install
   
           run hello app:
             $ DEBUG=my-application ./bin/www
   
    <span data-ttu-id="2df6c-145">Sono disponibili diverse nuove directory e file hello **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="2df6c-145">You now have several new directories and files in hello **tasklist** directory.</span></span>

### <a name="install-additional-modules"></a><span data-ttu-id="2df6c-146">Installare moduli aggiuntivi</span><span class="sxs-lookup"><span data-stu-id="2df6c-146">Install additional modules</span></span>
<span data-ttu-id="2df6c-147">Uno dei hello file che **express** crea è **package. JSON**.</span><span class="sxs-lookup"><span data-stu-id="2df6c-147">One of hello files that **express** creates is **package.json**.</span></span> <span data-ttu-id="2df6c-148">Questo file contiene un elenco di dipendenze del modulo.</span><span class="sxs-lookup"><span data-stu-id="2df6c-148">This file contains a list of module dependencies.</span></span> <span data-ttu-id="2df6c-149">In un secondo momento, quando si distribuisce tooApp applicazione hello App Web del servizio, questo file determina i moduli necessari toobe installato in Azure.</span><span class="sxs-lookup"><span data-stu-id="2df6c-149">Later, when you deploy hello application tooApp Service Web Apps, this file determines which modules need toobe installed on Azure.</span></span>

<span data-ttu-id="2df6c-150">Hello della riga di comando, digitare hello seguenti moduli di hello tooinstall comando descritti in hello **package. JSON** file.</span><span class="sxs-lookup"><span data-stu-id="2df6c-150">From hello command-line, enter hello following command tooinstall hello modules described in hello **package.json** file.</span></span> <span data-ttu-id="2df6c-151">Potrebbe essere necessario toouse 'sudo'.</span><span class="sxs-lookup"><span data-stu-id="2df6c-151">You may need toouse 'sudo'.</span></span>

    npm install

<span data-ttu-id="2df6c-152">output di Hello di questo comando viene visualizzato toohello simile esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-152">hello output of this command appears similar toohello following example:</span></span>

    debug@0.7.4 node_modules\debug

    cookie-parser@1.0.1 node_modules\cookie-parser
    ├── cookie-signature@1.0.3
    └── cookie@0.1.0

    [...]


<span data-ttu-id="2df6c-153">Quindi, immettere hello successivo comando tooinstall hello [azure], [nodo uuid], [nconf] e [async] moduli:</span><span class="sxs-lookup"><span data-stu-id="2df6c-153">Next, enter hello following command tooinstall hello [azure], [node-uuid], [nconf] and [async] modules:</span></span>

    npm install azure-storage node-uuid async nconf --save

<span data-ttu-id="2df6c-154">Hello **-Salva** flag aggiunge voci per toohello questi moduli **package. JSON** file.</span><span class="sxs-lookup"><span data-stu-id="2df6c-154">hello **--save** flag adds entries for these modules toohello **package.json** file.</span></span>

<span data-ttu-id="2df6c-155">output di Hello di questo comando viene visualizzato toohello simile esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-155">hello output of this command appears similar toohello following example:</span></span>

    async@0.9.0 node_modules\async

    node-uuid@1.4.1 node_modules\node-uuid

    nconf@0.6.9 node_modules\nconf
    ├── ini@1.2.1
    ├── async@0.2.9
    └── optimist@0.6.0 (wordwrap@0.0.2, minimist@0.0.10)

    [...]


## <a name="create-hello-application"></a><span data-ttu-id="2df6c-156">Creare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="2df6c-156">Create hello application</span></span>
<span data-ttu-id="2df6c-157">Si è un'applicazione hello toobuild pronto.</span><span class="sxs-lookup"><span data-stu-id="2df6c-157">Now we're ready toobuild hello application.</span></span>

### <a name="create-a-model"></a><span data-ttu-id="2df6c-158">Creare il modello</span><span class="sxs-lookup"><span data-stu-id="2df6c-158">Create a model</span></span>
<span data-ttu-id="2df6c-159">Oggetto *modello* è un oggetto che rappresenta i dati di hello nell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-159">A *model* is an object that represents hello data in your application.</span></span> <span data-ttu-id="2df6c-160">Per un'applicazione hello, modello solo hello è un oggetto attività, che rappresenta un elemento nell'elenco attività hello.</span><span class="sxs-lookup"><span data-stu-id="2df6c-160">For hello application, hello only model is a task object, which represents an item in hello to-do list.</span></span> <span data-ttu-id="2df6c-161">Attività saranno necessario hello seguenti campi:</span><span class="sxs-lookup"><span data-stu-id="2df6c-161">Tasks will have hello following fields:</span></span>

* <span data-ttu-id="2df6c-162">PartitionKey</span><span class="sxs-lookup"><span data-stu-id="2df6c-162">PartitionKey</span></span>
* <span data-ttu-id="2df6c-163">RowKey</span><span class="sxs-lookup"><span data-stu-id="2df6c-163">RowKey</span></span>
* <span data-ttu-id="2df6c-164">name (string)</span><span class="sxs-lookup"><span data-stu-id="2df6c-164">name (string)</span></span>
* <span data-ttu-id="2df6c-165">category (string)</span><span class="sxs-lookup"><span data-stu-id="2df6c-165">category (string)</span></span>
* <span data-ttu-id="2df6c-166">completed (Boolean)</span><span class="sxs-lookup"><span data-stu-id="2df6c-166">completed (Boolean)</span></span>

<span data-ttu-id="2df6c-167">**PartitionKey** e **RowKey** vengono utilizzati dal servizio tabelle hello come chiavi della tabella.</span><span class="sxs-lookup"><span data-stu-id="2df6c-167">**PartitionKey** and **RowKey** are used by hello Table Service as table keys.</span></span> <span data-ttu-id="2df6c-168">Per ulteriori informazioni, vedere [modello di dati del servizio tabelle hello comprensione](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span><span class="sxs-lookup"><span data-stu-id="2df6c-168">For more information, see [Understanding hello Table Service data model](https://msdn.microsoft.com/library/azure/dd179338.aspx).</span></span>

1. <span data-ttu-id="2df6c-169">In hello **tasklist** directory, creare una nuova directory denominata **modelli**.</span><span class="sxs-lookup"><span data-stu-id="2df6c-169">In hello **tasklist** directory, create a new directory named **models**.</span></span>
2. <span data-ttu-id="2df6c-170">In hello **modelli** directory, creare un nuovo file denominato **task.js**.</span><span class="sxs-lookup"><span data-stu-id="2df6c-170">In hello **models** directory, create a new file named **task.js**.</span></span> <span data-ttu-id="2df6c-171">Questo file contiene il modello di hello per le operazioni di hello create dall'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-171">This file will contain hello model for hello tasks created by your application.</span></span>
3. <span data-ttu-id="2df6c-172">All'inizio di hello di hello **task.js** file, aggiungere hello tooreference richiesto dalle librerie di codice seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-172">At hello beginning of hello **task.js** file, add hello following code tooreference required libraries:</span></span>
   
        var azure = require('azure-storage');
          var uuid = require('node-uuid');
        var entityGen = azure.TableUtilities.entityGenerator;
4. <span data-ttu-id="2df6c-173">Aggiungere seguente hello toodefine del codice e di esportare l'oggetto attività hello.</span><span class="sxs-lookup"><span data-stu-id="2df6c-173">Add hello following code toodefine and export hello Task object.</span></span> <span data-ttu-id="2df6c-174">Questo oggetto è responsabile per la connessione toohello tabella.</span><span class="sxs-lookup"><span data-stu-id="2df6c-174">This object is responsible for connecting toohello table.</span></span>
   
          module.exports = Task;
   
        function Task(storageClient, tableName, partitionKey) {
          this.storageClient = storageClient;
          this.tableName = tableName;
          this.partitionKey = partitionKey;
          this.storageClient.createTableIfNotExists(tableName, function tableCreated(error) {
            if(error) {
              throw error;
            }
          });
        };
5. <span data-ttu-id="2df6c-175">Aggiungere hello seguito metodi aggiuntivi di codice toodefine nell'oggetto attività hello, che consentono le interazioni con i dati archiviati nella tabella hello:</span><span class="sxs-lookup"><span data-stu-id="2df6c-175">Add hello following code toodefine additional methods on hello Task object, which allow interactions with data stored in hello table:</span></span>
   
        Task.prototype = {
          find: function(query, callback) {
            self = this;
            self.storageClient.queryEntities(this.tableName, query, null, function entitiesQueried(error, result) {
              if(error) {
                callback(error);
              } else {
                callback(null, result.entries);
              }
            });
          },
   
          addItem: function(item, callback) {
            self = this;
            // use entityGenerator tooset types
            // NOTE: RowKey must be a string type, even though
            // it contains a GUID in this example.
            var itemDescriptor = {
              PartitionKey: entityGen.String(self.partitionKey),
              RowKey: entityGen.String(uuid()),
              name: entityGen.String(item.name),
              category: entityGen.String(item.category),
              completed: entityGen.Boolean(false)
            };
            self.storageClient.insertEntity(self.tableName, itemDescriptor, function entityInserted(error) {
              if(error){  
                callback(error);
              }
              callback(null);
            });
          },
   
          updateItem: function(rKey, callback) {
            self = this;
            self.storageClient.retrieveEntity(self.tableName, self.partitionKey, rKey, function entityQueried(error, entity) {
              if(error) {
                callback(error);
              }
              entity.completed._ = true;
              self.storageClient.updateEntity(self.tableName, entity, function entityUpdated(error) {
                if(error) {
                  callback(error);
                }
                callback(null);
              });
            });
          }
        }
6. <span data-ttu-id="2df6c-176">Salvare e chiudere hello **task.js** file.</span><span class="sxs-lookup"><span data-stu-id="2df6c-176">Save and close hello **task.js** file.</span></span>

### <a name="create-a-controller"></a><span data-ttu-id="2df6c-177">Creare un controller</span><span class="sxs-lookup"><span data-stu-id="2df6c-177">Create a controller</span></span>
<span data-ttu-id="2df6c-178">Oggetto *controller* gestisce le richieste HTTP ed esegue il rendering di risposta hello HTML.</span><span class="sxs-lookup"><span data-stu-id="2df6c-178">A *controller* handles HTTP requests and renders hello HTML response.</span></span>

1. <span data-ttu-id="2df6c-179">In hello **tasklist/route** directory, creare un nuovo file denominato **tasklist.js** e aprirlo in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="2df6c-179">In hello **tasklist/routes** directory, create a new file named **tasklist.js** and open it in a text editor.</span></span>
2. <span data-ttu-id="2df6c-180">Aggiungere hello seguente codice troppo**tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="2df6c-180">Add hello following code too**tasklist.js**.</span></span> <span data-ttu-id="2df6c-181">Viene caricato hello async moduli di azure e, che vengono usati da **tasklist.js**.</span><span class="sxs-lookup"><span data-stu-id="2df6c-181">This loads hello azure and async modules, which are used by **tasklist.js**.</span></span> <span data-ttu-id="2df6c-182">Definisce inoltre hello **TaskList** funzione, che viene passata un'istanza di hello **attività** dell'oggetto definita in precedenza:</span><span class="sxs-lookup"><span data-stu-id="2df6c-182">This also defines hello **TaskList** function, which is passed an instance of hello **Task** object we defined earlier:</span></span>
   
        var azure = require('azure-storage');
        var async = require('async');
   
        module.exports = TaskList;
3. <span data-ttu-id="2df6c-183">Definire un oggetto **TaskList** .</span><span class="sxs-lookup"><span data-stu-id="2df6c-183">Define a **TaskList** object.</span></span>
   
        function TaskList(task) {
          this.task = task;
        }
4. <span data-ttu-id="2df6c-184">Aggiungere i seguenti metodi troppo hello**TaskList**:</span><span class="sxs-lookup"><span data-stu-id="2df6c-184">Add hello following methods too**TaskList**:</span></span>
   
        TaskList.prototype = {
          showTasks: function(req, res) {
            self = this;
            var query = new azure.TableQuery()
              .where('completed eq ?', false);
            self.task.find(query, function itemsFound(error, items) {
              res.render('index',{title: 'My ToDo List ', tasks: items});
            });
          },
   
          addTask: function(req,res) {
            var self = this;
            var item = req.body.item;
            self.task.addItem(item, function itemAdded(error) {
              if(error) {
                throw error;
              }
              res.redirect('/');
            });
          },
   
          completeTask: function(req,res) {
            var self = this;
            var completedTasks = Object.keys(req.body);
            async.forEach(completedTasks, function taskIterator(completedTask, callback) {
              self.task.updateItem(completedTask, function itemsUpdated(error) {
                if(error){
                  callback(error);
                } else {
                  callback(null);
                }
              });
            }, function goHome(error){
              if(error) {
                throw error;
              } else {
               res.redirect('/');
              }
            });
          }
        }

### <a name="modify-appjs"></a><span data-ttu-id="2df6c-185">Modificare il file app.js</span><span class="sxs-lookup"><span data-stu-id="2df6c-185">Modify app.js</span></span>
1. <span data-ttu-id="2df6c-186">Da hello **tasklist** hello directory, aprire **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="2df6c-186">From hello **tasklist** directory, open hello **app.js** file.</span></span> <span data-ttu-id="2df6c-187">Questo file è stato creato in precedenza eseguendo hello **express** comando.</span><span class="sxs-lookup"><span data-stu-id="2df6c-187">This file was created earlier by running hello **express** command.</span></span>
2. <span data-ttu-id="2df6c-188">Inizio hello del file hello, aggiungere hello seguente modulo hello azure tooload, nome della tabella hello set, chiave di partizione e le credenziali di archiviazione hello set utilizzate in questo esempio:</span><span class="sxs-lookup"><span data-stu-id="2df6c-188">At hello beginning of hello file, add hello following tooload hello azure module, set hello table name, partition key, and set hello storage credentials used by this example:</span></span>
   
        var azure = require('azure-storage');
        var nconf = require('nconf');
        nconf.env()
             .file({ file: 'config.json', search: true });
        var tableName = nconf.get("TABLE_NAME");
        var partitionKey = nconf.get("PARTITION_KEY");
        var accountName = nconf.get("STORAGE_NAME");
        var accountKey = nconf.get("STORAGE_KEY");
   
   > [!NOTE]
   > <span data-ttu-id="2df6c-189">nconf caricherà i valori di configurazione hello da variabili di ambiente o hello **config. JSON** file, verrà creata in un secondo momento.</span><span class="sxs-lookup"><span data-stu-id="2df6c-189">nconf will load hello configuration values from either environment variables or hello **config.json** file, which we will create later.</span></span>
   > 
   > 
3. <span data-ttu-id="2df6c-190">Nel file app.js hello, scorrere verso il basso toowhere vedrai hello la seguente riga:</span><span class="sxs-lookup"><span data-stu-id="2df6c-190">In hello app.js file, scroll down toowhere you see hello following line:</span></span>
   
        app.use('/', routes);
        app.use('/users', users);
   
    <span data-ttu-id="2df6c-191">Sostituire hello sopra righe con codice hello riportato di seguito.</span><span class="sxs-lookup"><span data-stu-id="2df6c-191">Replace hello above lines with hello code shown below.</span></span> <span data-ttu-id="2df6c-192">Inizializza un'istanza di <strong>attività</strong> con un account di archiviazione tooyour di connessione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-192">This will initialize an instance of <strong>Task</strong> with a connection tooyour storage account.</span></span> <span data-ttu-id="2df6c-193">Questo argomento viene passato toohello <strong>TaskList</strong>, che verrà utilizzato toocommunicate con hello del servizio tabelle:</span><span class="sxs-lookup"><span data-stu-id="2df6c-193">This is passed toohello <strong>TaskList</strong>, which will use it toocommunicate with hello Table service:</span></span>
   
        var TaskList = require('./routes/tasklist');
        var Task = require('./models/task');
        var task = new Task(azure.createTableService(accountName, accountKey), tableName, partitionKey);
        var taskList = new TaskList(task);
   
        app.get('/', taskList.showTasks.bind(taskList));
        app.post('/addtask', taskList.addTask.bind(taskList));
        app.post('/completetask', taskList.completeTask.bind(taskList));
4. <span data-ttu-id="2df6c-194">Salvare hello **app.js** file.</span><span class="sxs-lookup"><span data-stu-id="2df6c-194">Save hello **app.js** file.</span></span>

### <a name="modify-hello-index-view"></a><span data-ttu-id="2df6c-195">Modifica visualizzazione dell'indice hello</span><span class="sxs-lookup"><span data-stu-id="2df6c-195">Modify hello index view</span></span>
1. <span data-ttu-id="2df6c-196">Aprire hello **tasklist/views/index.jade** file in un editor di testo.</span><span class="sxs-lookup"><span data-stu-id="2df6c-196">Open hello **tasklist/views/index.jade** file in a text editor.</span></span>
2. <span data-ttu-id="2df6c-197">Sostituire hello l'intero contenuto del file hello con hello seguente codice.</span><span class="sxs-lookup"><span data-stu-id="2df6c-197">Replace hello entire contents of hello file with hello following code.</span></span> <span data-ttu-id="2df6c-198">Ciò consente di definire una visualizzazione delle attività esistenti e includere un modulo per aggiungere nuove attività e contrassegnare quelle esistenti come completate.</span><span class="sxs-lookup"><span data-stu-id="2df6c-198">This defines a view that displays existing tasks and includes a form for adding new tasks and marking existing ones as completed.</span></span>
   
        extends layout
   
        block content
          h1= title
          br
   
          form(action="/completetask", method="post")
            table.table.table-striped.table-bordered
              tr
                td Name
                td Category
                td Date
                td Complete
              if (typeof tasks === "undefined")
                tr
                  td
              else
                each task in tasks
                  tr
                    td #{task.name._}
                    td #{task.category._}
                    - var day   = task.Timestamp._.getDate();
                    - var month = task.Timestamp._.getMonth() + 1;
                    - var year  = task.Timestamp._.getFullYear();
                    td #{month + "/" + day + "/" + year}
                    td
                      input(type="checkbox", name="#{task.RowKey._}", value="#{!task.completed._}", checked=task.completed._)
            button.btn(type="submit") Update tasks
          hr
          form.well(action="/addtask", method="post")
            label Item Name:
            input(name="item[name]", type="textbox")
            label Item Category:
            input(name="item[category]", type="textbox")
            br
            button.btn(type="submit") Add item
3. <span data-ttu-id="2df6c-199">Salvare e chiudere il file **index.jade** .</span><span class="sxs-lookup"><span data-stu-id="2df6c-199">Save and close **index.jade** file.</span></span>

### <a name="modify-hello-global-layout"></a><span data-ttu-id="2df6c-200">Modifica layout globale hello</span><span class="sxs-lookup"><span data-stu-id="2df6c-200">Modify hello global layout</span></span>
<span data-ttu-id="2df6c-201">Hello **layout.jade** file hello **viste** directory è un modello generale per altri **.jade** file.</span><span class="sxs-lookup"><span data-stu-id="2df6c-201">hello **layout.jade** file in hello **views** directory is a global template for other **.jade** files.</span></span> <span data-ttu-id="2df6c-202">In questo passaggio è necessario modificarlo toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), che è un toolkit che rende facile toodesign un'app web di aspetto interessante.</span><span class="sxs-lookup"><span data-stu-id="2df6c-202">In this step you will modify it toouse [Twitter Bootstrap](https://github.com/twbs/bootstrap), which is a toolkit that makes it easy toodesign a nice looking web app.</span></span>

<span data-ttu-id="2df6c-203">Scaricare ed estrarre file hello per [Twitter Bootstrap](http://getbootstrap.com/).</span><span class="sxs-lookup"><span data-stu-id="2df6c-203">Download and extract hello files for [Twitter Bootstrap](http://getbootstrap.com/).</span></span> <span data-ttu-id="2df6c-204">Hello copia **bootstrap.min.css** file hello Bootstrap **css** hello nella cartella **pubblico/fogli di stile** directory dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-204">Copy hello **bootstrap.min.css** file from hello Bootstrap **css** folder into hello **public/stylesheets** directory of your application.</span></span>

<span data-ttu-id="2df6c-205">Da hello **viste** cartella, aprire **layout.jade** e sostituire tutto il contenuto di hello con hello seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-205">From hello **views** folder, open **layout.jade** and replace hello entire contents with hello following:</span></span>

    doctype html
    html
      head
        title= title
        link(rel='stylesheet', href='/stylesheets/bootstrap.min.css')
        link(rel='stylesheet', href='/stylesheets/style.css')
      body.app
        nav.navbar.navbar-default
          div.navbar-header
          a.navbar-brand(href='/') My Tasks
        block content

### <a name="create-a-config-file"></a><span data-ttu-id="2df6c-206">Creare un file config</span><span class="sxs-lookup"><span data-stu-id="2df6c-206">Create a config file</span></span>
<span data-ttu-id="2df6c-207">toorun hello app localmente, si saranno inserire le credenziali di archiviazione di Azure in un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-207">toorun hello app locally, we'll put Azure Storage credentials into a config file.</span></span> <span data-ttu-id="2df6c-208">Creare un file denominato **config. JSON* * con hello JSON seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-208">Create a file named **config.json* *with hello following JSON:</span></span>

    {
        "STORAGE_NAME": "<storage account name>",
        "STORAGE_KEY": "<storage access key>",
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="2df6c-209">Sostituire **nome account di archiviazione** con nome hello dell'archiviazione hello account creato in precedenza e sostituire **chiave di accesso di archiviazione** con la chiave di accesso primaria hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-209">Replace **storage account name** with hello name of hello storage account you created earlier, and replace **storage access key** with hello primary access key for your storage account.</span></span> <span data-ttu-id="2df6c-210">ad esempio:</span><span class="sxs-lookup"><span data-stu-id="2df6c-210">For example:</span></span>

    {
        "STORAGE_NAME": "nodejsappstorage",
        "STORAGE_KEY": "KG0oDd..."
        "PARTITION_KEY": "mytasks",
        "TABLE_NAME": "tasks"
    }

<span data-ttu-id="2df6c-211">Salvare il file *livello di una directory superiore* di hello **tasklist** directory, simile al seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-211">Save this file *one directory level higher* than hello **tasklist** directory, like this:</span></span>

    parent/
      |-- config.json
      |-- tasklist/

<span data-ttu-id="2df6c-212">motivo di Hello per eseguire questa operazione è tooavoid controllare il file di configurazione hello nel controllo del codice sorgente, in cui potrebbe non pubblico.</span><span class="sxs-lookup"><span data-stu-id="2df6c-212">hello reason for doing this is tooavoid checking hello config file into source control, where it might become public.</span></span> <span data-ttu-id="2df6c-213">Quando si distribuisce hello app tooAzure, si utilizzerà le variabili di ambiente invece di un file di configurazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-213">When we deploy hello app tooAzure, we will use environment variables instead of a config file.</span></span>

## <a name="run-hello-application-locally"></a><span data-ttu-id="2df6c-214">Eseguire un'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="2df6c-214">Run hello application locally</span></span>
<span data-ttu-id="2df6c-215">un'applicazione hello tootest sul computer locale, eseguire hello alla procedura seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-215">tootest hello application on your local machine, perform hello following steps:</span></span>

1. <span data-ttu-id="2df6c-216">Hello della riga di comando, modificare le directory toohello **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="2df6c-216">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="2df6c-217">Utilizzare hello successivo comando toolaunch un'applicazione hello in locale:</span><span class="sxs-lookup"><span data-stu-id="2df6c-217">Use hello following command toolaunch hello application locally:</span></span>
   
        npm start
3. <span data-ttu-id="2df6c-218">Aprire un web browser e passare toohttp://127.0.0.1:3000.</span><span class="sxs-lookup"><span data-stu-id="2df6c-218">Open a web browser and navigate toohttp://127.0.0.1:3000.</span></span>
   
    <span data-ttu-id="2df6c-219">Viene visualizzato un toohello simile a pagina web seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="2df6c-219">A web page similar toohello following example appears.</span></span>
   
    ![Pagina Web con un elenco di attività vuoto][node-table-finished]
4. <span data-ttu-id="2df6c-221">toocreate un nuovo elemento di attività, immettere un nome e una categoria e fare clic su **Aggiungi elemento**.</span><span class="sxs-lookup"><span data-stu-id="2df6c-221">toocreate a new to-do item, enter a name and category and click **Add Item**.</span></span> 
5. <span data-ttu-id="2df6c-222">un'attività come il controllo completo, toomark **completa** e fare clic su **Aggiorna attività**.</span><span class="sxs-lookup"><span data-stu-id="2df6c-222">toomark a task as complete, check **Complete** and click **Update Tasks**.</span></span>
   
    ![Un'immagine di hello nuovo elemento hello elenco di attività][node-table-list-items]

<span data-ttu-id="2df6c-224">Anche se un'applicazione hello è in esecuzione in locale, l'archiviazione dati hello in hello del servizio tabelle di Azure.</span><span class="sxs-lookup"><span data-stu-id="2df6c-224">Even though hello application is running locally, it is storing hello data in hello Azure Table service.</span></span>

## <a name="deploy-your-application-tooazure"></a><span data-ttu-id="2df6c-225">Distribuire l'applicazione tooAzure</span><span class="sxs-lookup"><span data-stu-id="2df6c-225">Deploy your application tooAzure</span></span>
<span data-ttu-id="2df6c-226">passaggi Hello in questa sezione utilizzano gli strumenti da riga di comando di Azure di hello toocreate una nuova app web nel servizio App e quindi usare Git toodeploy l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-226">hello steps in this section use hello Azure command-line tools toocreate a new web app in App Service, and then use Git toodeploy your application.</span></span> <span data-ttu-id="2df6c-227">tooperform questi passaggi, è necessario disporre di una sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2df6c-227">tooperform these steps you must have an Azure subscription.</span></span>

> [!NOTE]
> <span data-ttu-id="2df6c-228">Questi passaggi possono essere eseguiti anche utilizzando hello [portale Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="2df6c-228">These steps can also be performed by using hello [Azure Portal](https://portal.azure.com/).</span></span> <span data-ttu-id="2df6c-229">Vedere [Creazione e distribuzione di un'app Web Node.js nel Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="2df6c-229">See [Build and deploy a Node.js web app in Azure App Service].</span></span>
> 
> <span data-ttu-id="2df6c-230">Se si tratta di hello prima app web che è stato creato, è necessario utilizzare hello Azure Portal toodeploy questa applicazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-230">If this is hello first web app you have created, you must use hello Azure Portal toodeploy this application.</span></span>
> 
> 

<span data-ttu-id="2df6c-231">tooget avviato, installare hello [CLI di Azure] immettendo hello comando seguente dalla riga di comando hello:</span><span class="sxs-lookup"><span data-stu-id="2df6c-231">tooget started, install hello [Azure CLI] by entering hello following command from hello command line:</span></span>

    npm install azure-cli -g

### <a name="import-publishing-settings"></a><span data-ttu-id="2df6c-232">Importare le impostazioni di pubblicazione</span><span class="sxs-lookup"><span data-stu-id="2df6c-232">Import publishing settings</span></span>
<span data-ttu-id="2df6c-233">In questo passaggio verrà scaricato un file contenente informazioni sulla sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-233">In this step, you will download a file containing information about your subscription.</span></span>

1. <span data-ttu-id="2df6c-234">Immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-234">Enter hello following command:</span></span>
   
        azure login
   
    <span data-ttu-id="2df6c-235">Questo comando viene avviato un browser e si sposta toohello pagina di download.</span><span class="sxs-lookup"><span data-stu-id="2df6c-235">This command launches a browser and navigates toohello download page.</span></span> <span data-ttu-id="2df6c-236">Se richiesto, accedere con l'account hello associati alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2df6c-236">If prompted, log in with hello account associated with your Azure subscription.</span></span>
   
    <!-- ![hello download page][download-publishing-settings] -->
   
    <span data-ttu-id="2df6c-237">download del file Hello inizia automaticamente. in caso contrario, è possibile fare clic su collegamento hello all'inizio di hello hello toomanually download hello del file della pagina.</span><span class="sxs-lookup"><span data-stu-id="2df6c-237">hello file download begins automatically; if it does not, you can click hello link at hello beginning of hello page toomanually download hello file.</span></span> <span data-ttu-id="2df6c-238">Salvare hello file e Nota hello percorso del file.</span><span class="sxs-lookup"><span data-stu-id="2df6c-238">Save hello file and note hello file path.</span></span>
2. <span data-ttu-id="2df6c-239">Immettere hello impostazioni hello tooimport del comando seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-239">Enter hello following command tooimport hello settings:</span></span>
   
        azure account import <path-to-file>
   
    <span data-ttu-id="2df6c-240">Specificare hello percorso e il nome della pubblicazione di file di impostazioni che è stato scaricato nel passaggio precedente hello hello.</span><span class="sxs-lookup"><span data-stu-id="2df6c-240">Specify hello path and file name of hello publishing settings file you downloaded in hello previous step.</span></span>
3. <span data-ttu-id="2df6c-241">Dopo l'importano delle impostazioni di hello, hello di eliminare i file di impostazioni di pubblicazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-241">After hello settings are imported, delete hello publish settings file.</span></span> <span data-ttu-id="2df6c-242">Non è più necessario e contiene informazioni riservate relative alla sottoscrizione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2df6c-242">It is no longer needed, and contains sensitive information regarding your Azure subscription.</span></span>

### <a name="create-an-app-service-web-app"></a><span data-ttu-id="2df6c-243">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="2df6c-243">Create an App Service web app</span></span>
1. <span data-ttu-id="2df6c-244">Hello della riga di comando, modificare le directory toohello **tasklist** directory.</span><span class="sxs-lookup"><span data-stu-id="2df6c-244">From hello command-line, change directories toohello **tasklist** directory.</span></span>
2. <span data-ttu-id="2df6c-245">Utilizzare hello successivo comando toocreate una nuova app web.</span><span class="sxs-lookup"><span data-stu-id="2df6c-245">Use hello following command toocreate a new web app.</span></span>
   
        azure site create --git
   
    <span data-ttu-id="2df6c-246">Verrà richiesto per la posizione e nome dell'applicazione web hello.</span><span class="sxs-lookup"><span data-stu-id="2df6c-246">You will be prompted for hello web app name and location.</span></span> <span data-ttu-id="2df6c-247">Fornire un nome univoco e selezionare hello stessa località geografica dell'account di archiviazione di Azure.</span><span class="sxs-lookup"><span data-stu-id="2df6c-247">Provide a unique name and select hello same geographical location as your Azure Storage account.</span></span>
   
    <span data-ttu-id="2df6c-248">Hello `--git` parametro crea un repository Git in Azure per questa app web.</span><span class="sxs-lookup"><span data-stu-id="2df6c-248">hello `--git` parameter creates a Git repository on Azure for this web app.</span></span> <span data-ttu-id="2df6c-249">Inizializza un repository Git nella directory corrente hello anche se non esiste e aggiunge un [Git remoto] denominato 'azure', che è usato toopublish hello applicazione tooAzure.</span><span class="sxs-lookup"><span data-stu-id="2df6c-249">It also initializes a Git repository in hello current directory if none exists, and adds a [Git remote] named 'azure', which is used toopublish hello application tooAzure.</span></span> <span data-ttu-id="2df6c-250">Infine, viene creato un **Web. config** file che contiene le impostazioni utilizzate dalle applicazioni di Azure toohost nodo.</span><span class="sxs-lookup"><span data-stu-id="2df6c-250">Finally, it creates a **web.config** file, which contains settings used by Azure toohost node applications.</span></span> <span data-ttu-id="2df6c-251">Se si omette hello `--git` parametro ma hello directory contiene un repository Git, comando hello verrà comunque creati remoto hello 'azure'.</span><span class="sxs-lookup"><span data-stu-id="2df6c-251">If you omit hello `--git` parameter but hello directory contains a Git repository, hello command will still create hello 'azure' remote.</span></span>
   
    <span data-ttu-id="2df6c-252">Al termine di questo comando, verrà visualizzato il seguente toohello simili di output.</span><span class="sxs-lookup"><span data-stu-id="2df6c-252">Once this command has completed, you will see output similar toohello following.</span></span> <span data-ttu-id="2df6c-253">Si noti che hello riga che inizia con **sito Web creato in** contiene hello URL per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="2df6c-253">Note that hello line beginning with **Website created at** contains hello URL for hello web app.</span></span>
   
        info:   Executing command site create
        help:   Need a site name
        Name: TableTasklist
        info:   Using location southcentraluswebspace
        info:   Executing `git init`
        info:   Creating default .gitignore file
        info:   Creating a new web site
        info:   Created web site at  tabletasklist.azurewebsites.net
        info:   Initializing repository
        info:   Repository initialized
        info:   Executing `git remote add azure https://username@tabletasklist.azurewebsites.net/TableTasklist.git`
        info:   site create command OK
   
   > [!NOTE]
   > <span data-ttu-id="2df6c-254">Se si tratta di hello prima applicazione del servizio web app per la sottoscrizione, sarà toouse istruzioni riportate hello Azure Portal toocreate hello web app.</span><span class="sxs-lookup"><span data-stu-id="2df6c-254">If this is hello first App Service web app for your subscription, you will be instructed toouse hello Azure Portal toocreate hello web app.</span></span> <span data-ttu-id="2df6c-255">Per ulteriori informazioni, vedere [Creazione e distribuzione di un'app Web Node.js nel Azure App Service].</span><span class="sxs-lookup"><span data-stu-id="2df6c-255">For more information, see [Build and deploy a Node.js web app in Azure App Service].</span></span>
   > 
   > 

### <a name="set-environment-variables"></a><span data-ttu-id="2df6c-256">Impostare le variabili di ambiente</span><span class="sxs-lookup"><span data-stu-id="2df6c-256">Set environment variables</span></span>
<span data-ttu-id="2df6c-257">In questo passaggio si aggiungeranno configurazione dell'ambiente variabili tooyour web app in Azure.</span><span class="sxs-lookup"><span data-stu-id="2df6c-257">In this step, you will add environment variables tooyour web app configuration on Azure.</span></span>
<span data-ttu-id="2df6c-258">Dalla riga di comando hello, immettere il seguente hello:</span><span class="sxs-lookup"><span data-stu-id="2df6c-258">From hello command line, enter hello following:</span></span>

    azure site appsetting add
        STORAGE_NAME=<storage account name>;STORAGE_KEY=<storage access key>;PARTITION_KEY=mytasks;TABLE_NAME=tasks


<span data-ttu-id="2df6c-259">Sostituire  **<storage account name>**  con nome hello dell'archiviazione hello account creato in precedenza e sostituire  **<storage access key>**  con la chiave di accesso primaria hello dell'account di archiviazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-259">Replace **<storage account name>** with hello name of hello storage account you created earlier, and replace **<storage access key>** with hello primary access key for your storage account.</span></span> <span data-ttu-id="2df6c-260">(Utilizzare hello stesso valori come file config. JSON hello creato in precedenza).</span><span class="sxs-lookup"><span data-stu-id="2df6c-260">(Use hello same values as hello config.json file that you created earlier.)</span></span>

<span data-ttu-id="2df6c-261">In alternativa, è possibile impostare le variabili di ambiente in hello [portale Azure](https://portal.azure.com/):</span><span class="sxs-lookup"><span data-stu-id="2df6c-261">Alternatively, you can set environment variables in hello [Azure Portal](https://portal.azure.com/):</span></span>

1. <span data-ttu-id="2df6c-262">Aprire il pannello dell'app web hello facendo **Sfoglia** > **App Web** > nome dell'app web.</span><span class="sxs-lookup"><span data-stu-id="2df6c-262">Open hello web app's blade by clicking **Browse** > **Web Apps** > your web app name.</span></span>
2. <span data-ttu-id="2df6c-263">Nel pannello dell'app Web fare clic su **Tutte le impostazioni** > **Impostazioni dell'applicazione**.</span><span class="sxs-lookup"><span data-stu-id="2df6c-263">In your web app's blade, click **All Settings** > **Application Settings**.</span></span>
   
     <!-- ![Top Menu](./media/storage-nodejs-use-table-storage-web-site/PollsCommonWebSiteTopMenu.png) -->
3. <span data-ttu-id="2df6c-264">Scorrere verso il basso toohello **impostazioni App** sezione e aggiungere coppie chiave/valore hello.</span><span class="sxs-lookup"><span data-stu-id="2df6c-264">Scroll down toohello **App settings** section and add hello key/value pairs.</span></span>
   
     ![Impostazioni app](./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png)
4. <span data-ttu-id="2df6c-266">Fare clic su **SAVE**.</span><span class="sxs-lookup"><span data-stu-id="2df6c-266">Click **SAVE**.</span></span>

### <a name="publish-hello-application"></a><span data-ttu-id="2df6c-267">Pubblicare un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="2df6c-267">Publish hello application</span></span>
<span data-ttu-id="2df6c-268">app hello toopublish, eseguire il commit tooGit i file di codice hello e quindi push tooazure o master.</span><span class="sxs-lookup"><span data-stu-id="2df6c-268">toopublish hello app, commit hello code files tooGit and then push tooazure/master.</span></span>

1. <span data-ttu-id="2df6c-269">Impostare le credenziali di distribuzione</span><span class="sxs-lookup"><span data-stu-id="2df6c-269">Set your deployment credentials.</span></span>
   
        azure site deployment user set <name> <password>
2. <span data-ttu-id="2df6c-270">Aggiungere ed effettuare il commit dei file dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-270">Add and commit your application files.</span></span>
   
        git add .
        git commit -m "adding files"
3. <span data-ttu-id="2df6c-271">Push hello commit toohello App del servizio web app:</span><span class="sxs-lookup"><span data-stu-id="2df6c-271">Push hello commit toohello App Service web app:</span></span>
   
        git push azure master
   
    <span data-ttu-id="2df6c-272">Utilizzare **master** come ramo di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="2df6c-272">Use **master** as hello target branch.</span></span> <span data-ttu-id="2df6c-273">Alla fine di hello della distribuzione di hello, viene visualizzato un toohello simile istruzione esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="2df6c-273">At hello end of hello deployment, you see a statement similar toohello following example:</span></span>
   
        toohttps://username@tabletasklist.azurewebsites.net/TableTasklist.git
          * [new branch]      master -> master
4. <span data-ttu-id="2df6c-274">Una volta completata l'operazione di push hello, individuare l'URL dell'app web toohello restituito in precedenza da hello `azure create site` comando tooview l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="2df6c-274">Once hello push operation has completed, browse toohello web app URL returned previously by hello `azure create site` command tooview your application.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2df6c-275">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2df6c-275">Next steps</span></span>
<span data-ttu-id="2df6c-276">Mentre hello in questo articolo viene descritta la utilizzando le informazioni di toostore di hello del servizio tabelle, è inoltre possibile utilizzare [MongoDB](https://mlab.com/azure/).</span><span class="sxs-lookup"><span data-stu-id="2df6c-276">While hello steps in this article describe using hello Table Service toostore information, you can also use [MongoDB](https://mlab.com/azure/).</span></span> 

## <a name="additional-resources"></a><span data-ttu-id="2df6c-277">Risorse aggiuntive</span><span class="sxs-lookup"><span data-stu-id="2df6c-277">Additional resources</span></span>
<span data-ttu-id="2df6c-278">[CLI di Azure]</span><span class="sxs-lookup"><span data-stu-id="2df6c-278">[Azure CLI]</span></span>

## <a name="whats-changed"></a><span data-ttu-id="2df6c-279">Modifiche apportate</span><span class="sxs-lookup"><span data-stu-id="2df6c-279">What's changed</span></span>
* <span data-ttu-id="2df6c-280">Per una Guida toohello modifica da siti Web tooApp servizio vedere: [relativo impatto sui servizi di Azure esistente e servizio App di Azure](http://go.microsoft.com/fwlink/?LinkId=529714)</span><span class="sxs-lookup"><span data-stu-id="2df6c-280">For a guide toohello change from Websites tooApp Service see: [Azure App Service and Its Impact on Existing Azure Services](http://go.microsoft.com/fwlink/?LinkId=529714)</span></span>

<!-- URLs -->

[Creazione e distribuzione di un'app Web Node.js nel Azure App Service]: app-service-web-get-started-nodejs.md
[Azure Developer Center]: /develop/nodejs/

[nodo]: http://nodejs.org
[Git]: http://git-scm.com
[Express]: http://expressjs.com
[for free]: http://windowsazure.com
[Git remoto]: http://git-scm.com/docs/git-remote

[CLI di Azure]:../cli-install-nodejs.md

[azure]: https://github.com/Azure/azure-sdk-for-node
[nodo uuid]: https://www.npmjs.com/package/node-uuid
[nconf]: https://www.npmjs.com/package/nconf
[async]: https://www.npmjs.com/package/async

[Azure Portal]: https://portal.azure.com

[Create and deploy a Node.js application tooan Azure Web Site]: app-service-web-get-started-nodejs.md

<!-- Image References -->

[node-table-finished]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_empty.png
[node-table-list-items]: ./media/storage-nodejs-use-table-storage-web-site/table_todo_list.png
[download-publishing-settings]: ./media/storage-nodejs-use-table-storage-web-site/azure-account-download-cli.png
[portal-storage-access-keys]: ./media/storage-nodejs-use-table-storage-web-site/manage-access-keys.png
[app-settings]: ./media/storage-nodejs-use-table-storage-web-site/storage-tasks-appsettings.png
