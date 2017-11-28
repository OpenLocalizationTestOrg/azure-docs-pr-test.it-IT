---
title: aaaGet introduttiva hello rete CDN di Azure SDK per Node.js | Documenti Microsoft
description: Informazioni su come toomanage di applicazioni Node.js toowrite rete CDN di Azure.
services: cdn
documentationcenter: nodejs
author: zhangmanling
manager: erikre
editor: 
ms.assetid: c4bb6a61-de3d-4f0c-9dca-202554c43dfa
ms.service: cdn
ms.workload: tbd
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: mazha
ms.openlocfilehash: 6c805e5fb8e0b471e8b248cb2f4b29efd6c85940
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="7529d-103">Introduzione allo sviluppo della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="7529d-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7529d-104">Node.JS</span><span class="sxs-lookup"><span data-stu-id="7529d-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="7529d-105">.NET</span><span class="sxs-lookup"><span data-stu-id="7529d-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="7529d-106">È possibile utilizzare hello [SDK della rete CDN di Azure per Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creazione e la gestione dei profili di rete CDN e gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="7529d-106">You can use hello [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="7529d-107">In questa esercitazione vengono illustrati la creazione di hello di una semplice applicazione console Node.js che vengono illustrate diverse operazioni disponibili hello.</span><span class="sxs-lookup"><span data-stu-id="7529d-107">This tutorial walks through hello creation of a simple Node.js console application that demonstrates several of hello available operations.</span></span>  <span data-ttu-id="7529d-108">In questa esercitazione è non è adatto toodescribe tutti gli aspetti di hello rete CDN di Azure SDK per Node.js in dettaglio.</span><span class="sxs-lookup"><span data-stu-id="7529d-108">This tutorial is not intended toodescribe all aspects of hello Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="7529d-109">toocomplete questa esercitazione, dovrebbe già disporre [Node.js](http://www.nodejs.org) **4.x.x** o versione successiva installato e configurato.</span><span class="sxs-lookup"><span data-stu-id="7529d-109">toocomplete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="7529d-110">È possibile utilizzare qualsiasi editor di testo cui toocreate l'applicazione di Node.js.</span><span class="sxs-lookup"><span data-stu-id="7529d-110">You can use any text editor you want toocreate your Node.js application.</span></span>  <span data-ttu-id="7529d-111">toowrite questa esercitazione, utilizzato [codice di Visual Studio](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="7529d-111">toowrite this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="7529d-112">Hello [progetto completato questa esercitazione](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) è disponibile per il download su MSDN.</span><span class="sxs-lookup"><span data-stu-id="7529d-112">hello [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="7529d-113">Creare il progetto e aggiungere le dipendenze NPM</span><span class="sxs-lookup"><span data-stu-id="7529d-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="7529d-114">Ora che è stato creato un gruppo di risorse per i profili di rete CDN e specificati i profili di rete CDN di Azure AD applicazione autorizzazione toomanage e gli endpoint all'interno del gruppo, è possibile iniziare a creare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7529d-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission toomanage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="7529d-115">Creare una cartella toostore l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="7529d-115">Create a folder toostore your application.</span></span>  <span data-ttu-id="7529d-116">Da una console con gli strumenti di Node.js hello nel percorso corrente, impostare la nuova cartella di percorso toothis corrente e inizializzare il progetto tramite l'esecuzione:</span><span class="sxs-lookup"><span data-stu-id="7529d-116">From a console with hello Node.js tools in your current path, set your current location toothis new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="7529d-117">Sarà quindi visualizzata una serie di domande tooinitialize il progetto.</span><span class="sxs-lookup"><span data-stu-id="7529d-117">You will then be presented a series of questions tooinitialize your project.</span></span>  <span data-ttu-id="7529d-118">Come **punto di ingresso**questa esercitazione usa *app.js*.</span><span class="sxs-lookup"><span data-stu-id="7529d-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="7529d-119">È possibile visualizzare le altre scelte in hello di esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="7529d-119">You can see my other choices in hello following example.</span></span>

![Output NPM iniziale](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="7529d-121">A questo punto il progetto viene inizializzato con un file *packages.json* .</span><span class="sxs-lookup"><span data-stu-id="7529d-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="7529d-122">Il progetto verrà toouse alcune librerie di Azure contenuti nei pacchetti NPM.</span><span class="sxs-lookup"><span data-stu-id="7529d-122">Our project is going toouse some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="7529d-123">Utilizzeremo hello Runtime Client di Azure per Node.js (ms-rest azure) e hello libreria Client della rete CDN di Azure per Node.js (azure-arm cd).</span><span class="sxs-lookup"><span data-stu-id="7529d-123">We'll use hello Azure Client Runtime for Node.js (ms-rest-azure) and hello Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="7529d-124">Aggiungere tali progetti toohello come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="7529d-124">Let's add those toohello project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="7529d-125">Dopo aver hello pacchetti vengono eseguiti l'installazione, hello *package. JSON* file dovrebbe essere simile toothis esempio (i numeri di versione potrebbero):</span><span class="sxs-lookup"><span data-stu-id="7529d-125">After hello packages are done installing, hello *package.json* file should look similar toothis example (version numbers may differ):</span></span>

``` json
{
  "name": "cdn_node",
  "version": "1.0.0",
  "description": "Azure CDN Node.js tutorial project",
  "main": "app.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "author": "Cam Soper",
  "license": "MIT",
  "dependencies": {
    "azure-arm-cdn": "^0.2.1",
    "ms-rest-azure": "^1.14.4"
  }
}
```

<span data-ttu-id="7529d-126">Infine, tramite l'editor di testo, creare un file di testo vuoto e salvarlo nella radice hello la cartella di progetto come *app.js*.</span><span class="sxs-lookup"><span data-stu-id="7529d-126">Finally, using your text editor, create a blank text file and save it in hello root of our project folder as *app.js*.</span></span>  <span data-ttu-id="7529d-127">Si è ora pronto toobegin la scrittura di codice.</span><span class="sxs-lookup"><span data-stu-id="7529d-127">We're now ready toobegin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="7529d-128">Istruzioni require, costanti, autenticazione e struttura</span><span class="sxs-lookup"><span data-stu-id="7529d-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="7529d-129">Con *app.js* aprire l'editor, possiamo procedere alla struttura di base di questo programma scritto hello.</span><span class="sxs-lookup"><span data-stu-id="7529d-129">With *app.js* open in our editor, let's get hello basic structure of our program written.</span></span>

1. <span data-ttu-id="7529d-130">Aggiungere hello "richiede" per i pacchetti NPM nella parte superiore di hello con seguenti hello:</span><span class="sxs-lookup"><span data-stu-id="7529d-130">Add hello "requires" for our NPM packages at hello top with hello following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="7529d-131">È necessario toodefine alcune costanti che utilizzeranno i metodi.</span><span class="sxs-lookup"><span data-stu-id="7529d-131">We need toodefine some constants our methods will use.</span></span>  <span data-ttu-id="7529d-132">Aggiungere il seguente hello.</span><span class="sxs-lookup"><span data-stu-id="7529d-132">Add hello following.</span></span>  <span data-ttu-id="7529d-133">Essere tooreplace che segnaposto hello, tra cui hello  **&lt;angolari&gt;**, con valori personalizzati in base alle esigenze.</span><span class="sxs-lookup"><span data-stu-id="7529d-133">Be sure tooreplace hello placeholders, including hello **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
    ``` javascript
    //Tenant app constants
    const clientId = "<YOUR CLIENT ID>";
    const clientSecret = "<YOUR CLIENT AUTHENTICATION KEY>"; //Only for service principals
    const tenantId = "<YOUR TENANT ID>";
   
    //Application constants
    const subscriptionId = "<YOUR SUBSCRIPTION ID>";
    const resourceGroupName = "CdnConsoleTutorial";
    const resourceLocation = "<YOUR PREFERRED AZURE LOCATION, SUCH AS Central US>";
    ```
3. <span data-ttu-id="7529d-134">Viene successivamente, creare un'istanza client di gestione della rete CDN hello e assegnarle il tipo di credenziali.</span><span class="sxs-lookup"><span data-stu-id="7529d-134">Next, we'll instantiate hello CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="7529d-135">Se si usa l'autenticazione del singolo utente, queste due righe di codice avranno un aspetto leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="7529d-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="7529d-136">Usare questo esempio di codice solo se si sceglie l'autenticazione utente toohave anziché un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="7529d-136">Only use this code sample if you are choosing toohave individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="7529d-137">Essere tooguard attenzione le credenziali utente e le mantiene segreta.</span><span class="sxs-lookup"><span data-stu-id="7529d-137">Be careful tooguard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="7529d-138">Essere tooreplace che gli elementi hello  **&lt;angolari&gt;**  con hello correggere le informazioni.</span><span class="sxs-lookup"><span data-stu-id="7529d-138">Be sure tooreplace hello items in **&lt;angle brackets&gt;** with hello correct information.</span></span>  <span data-ttu-id="7529d-139">Per `<redirect URI>`, utilizzare il reindirizzamento di hello URI immesso al momento della registrazione di un'applicazione hello in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="7529d-139">For `<redirect URI>`, use hello redirect URI you entered when you registered hello application in Azure AD.</span></span>
4. <span data-ttu-id="7529d-140">L'applicazione console Node.js verrà tootake alcuni parametri della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="7529d-140">Our Node.js console application is going tootake some command-line parameters.</span></span>  <span data-ttu-id="7529d-141">Verificare che venga passato almeno un parametro.</span><span class="sxs-lookup"><span data-stu-id="7529d-141">Let's validate that at least one parameter was passed.</span></span>
   
   ```javascript
   //Collect command-line parameters
   var parms = process.argv.slice(2);
   
   //Do we have parameters?
   if(parms == null || parms.length == 0)
   {
       console.log("Not enough parameters!");
       console.log("Valid commands are list, delete, create, and purge.");
       process.exit(1);
   }
   ```
5. <span data-ttu-id="7529d-142">Siamo arrivati toohello parte principale di questo programma, in cui si crei rami funzioni tooother in base alle quali i parametri passati.</span><span class="sxs-lookup"><span data-stu-id="7529d-142">That brings us toohello main part of our program, where we branch off tooother functions based on what parameters were passed.</span></span>
   
    ```javascript
    switch(parms[0].toLowerCase())
    {
        case "list":
            cdnList();
            break;
   
        case "create":
            cdnCreate();
            break;
   
        case "delete":
            cdnDelete();
            break;
   
        case "purge":
            cdnPurge();
            break;
   
        default:
            console.log("Valid commands are list, delete, create, and purge.");
            process.exit(1);
    }
    ```
6. <span data-ttu-id="7529d-143">In diverse posizioni in questo programma, è necessario toomake certi del numero corretto di parametri hello sono stato passato e Visualizza alcuni argomenti della Guida se queste non sembrano corrette.</span><span class="sxs-lookup"><span data-stu-id="7529d-143">At several places in our program, we'll need toomake sure hello right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="7529d-144">È possibile creare funzioni toodo che.</span><span class="sxs-lookup"><span data-stu-id="7529d-144">Let's create functions toodo that.</span></span>
   
   ```javascript
   function requireParms(parmCount) {
       if(parms.length < parmCount) {
           usageHelp(parms[0].toLowerCase());
           process.exit(1);
       }
   }
   
   function usageHelp(cmd) {
       console.log("Usage for " + cmd + ":");
       switch(cmd)
       {
           case "list":
               console.log("list profiles");
               console.log("list endpoints <profile name>");
               break;
   
           case "create":
               console.log("create profile <profile name>");
               console.log("create endpoint <profile name> <endpoint name> <origin hostname>");
               break;
   
           case "delete":
               console.log("delete profile <profile name>");
               console.log("delete endpoint <profile name> <endpoint name>");
               break;
   
           case "purge":
               console.log("purge <profile name> <endpoint name> <path>");
               break;
   
           default:
               console.log("Invalid command.");
       }
   }
   ```
7. <span data-ttu-id="7529d-145">Infine, le funzioni hello che verrà usato nel client di gestione della rete CDN hello sono asincrone, pertanto è necessario un metodo toocall quando completati.</span><span class="sxs-lookup"><span data-stu-id="7529d-145">Finally, hello functions we'll be using on hello CDN management client are asynchronous, so they need a method toocall back when they're done.</span></span>  <span data-ttu-id="7529d-146">Verifichiamo che è possibile visualizzare l'output di hello di client di gestione della rete CDN hello (se presente) e uscire dal programma di hello normalmente.</span><span class="sxs-lookup"><span data-stu-id="7529d-146">Let's make one that can display hello output from hello CDN management client (if any) and exit hello program gracefully.</span></span>
   
    ```javascript
    function callback(err, result, request, response) {
        if (err) {
            console.log(err);
            process.exit(1);
        } else {
            console.log((result == null) ? "Done!" : result);
            process.exit(0);
        }
    }
    ```

<span data-ttu-id="7529d-147">Struttura di base hello di questo programma è stato scritto, è necessario creare funzioni hello chiamate in base ai nostri parametri.</span><span class="sxs-lookup"><span data-stu-id="7529d-147">Now that hello basic structure of our program is written, we should create hello functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="7529d-148">Elencare i profili e gli endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="7529d-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="7529d-149">Iniziamo con toolist codice i profili e gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="7529d-149">Let's start with code toolist our existing profiles and endpoints.</span></span>  <span data-ttu-id="7529d-150">I commenti di codice forniscono la sintassi di hello previsto in modo da sapere dove ogni parametro memorizzate.</span><span class="sxs-lookup"><span data-stu-id="7529d-150">My code comments provide hello expected syntax so we know where each parameter goes.</span></span>

```javascript
// list profiles
// list endpoints <profile name>
function cdnList(){
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profiles":
            console.log("Listing profiles...");
            cdnClient.profiles.listByResourceGroup(resourceGroupName, callback);
            break;

        case "endpoints":
            requireParms(3);
            console.log("Listing endpoints...");
            cdnClient.endpoints.listByProfile(parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="7529d-151">Creare profili ed endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="7529d-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="7529d-152">Successivamente, si scriverà gli endpoint e i profili di toocreate funzioni hello.</span><span class="sxs-lookup"><span data-stu-id="7529d-152">Next, we'll write hello functions toocreate profiles and endpoints.</span></span>

```javascript
function cdnCreate() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        case "profile":
            cdnCreateProfile();
            break;

        case "endpoint":
            cdnCreateEndpoint();
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}

// create profile <profile name>
function cdnCreateProfile() {
    requireParms(3);
    console.log("Creating profile...");
    var standardCreateParameters = {
        location: resourceLocation,
        sku: {
            name: 'Standard_Verizon'
        }
    };

    cdnClient.profiles.create(parms[2], standardCreateParameters, resourceGroupName, callback);
}

// create endpoint <profile name> <endpoint name> <origin hostname>        
function cdnCreateEndpoint() {
    requireParms(5);
    console.log("Creating endpoint...");
    var endpointProperties = {
        location: resourceLocation,
        origins: [{
            name: parms[4],
            hostName: parms[4]
        }]
    };

    cdnClient.endpoints.create(parms[3], endpointProperties, parms[2], resourceGroupName, callback);
}
```

## <a name="purge-an-endpoint"></a><span data-ttu-id="7529d-153">Ripulire un endpoint</span><span class="sxs-lookup"><span data-stu-id="7529d-153">Purge an endpoint</span></span>
<span data-ttu-id="7529d-154">Supponendo che l'endpoint di hello è stato creato, un'attività comune che si voglia tooperform in questo programma è eliminazione contenuto in questo endpoint.</span><span class="sxs-lookup"><span data-stu-id="7529d-154">Assuming hello endpoint has been created, one common task that we might want tooperform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="7529d-155">Eliminare profili ed endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="7529d-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="7529d-156">ultima funzione Hello che includeremo Elimina profili e gli endpoint.</span><span class="sxs-lookup"><span data-stu-id="7529d-156">hello last function we will include deletes endpoints and profiles.</span></span>

```javascript
function cdnDelete() {
    requireParms(2);
    switch(parms[1].toLowerCase())
    {
        // delete profile <profile name>
        case "profile":
            requireParms(3);
            console.log("Deleting profile...");
            cdnClient.profiles.deleteIfExists(parms[2], resourceGroupName, callback);
            break;

        // delete endpoint <profile name> <endpoint name>
        case "endpoint":
            requireParms(4);
            console.log("Deleting endpoint...");
            cdnClient.endpoints.deleteIfExists(parms[3], parms[2], resourceGroupName, callback);
            break;

        default:
            console.log("Invalid parameter.");
            process.exit(1);
    }
}
```

## <a name="running-hello-program"></a><span data-ttu-id="7529d-157">Programma hello in esecuzione</span><span class="sxs-lookup"><span data-stu-id="7529d-157">Running hello program</span></span>
<span data-ttu-id="7529d-158">È ora possibile eseguire il programma di Node.js tramite il debugger Preferiti o console hello.</span><span class="sxs-lookup"><span data-stu-id="7529d-158">We can now execute our Node.js program using our favorite debugger or at hello console.</span></span>

> [!TIP]
> <span data-ttu-id="7529d-159">Se si utilizza codice di Visual Studio, come il debugger, è necessario tooset backup toopass l'ambiente nei parametri della riga di comando hello.</span><span class="sxs-lookup"><span data-stu-id="7529d-159">If you're using Visual Studio Code as your debugger, you'll need tooset up your environment toopass in hello command-line parameters.</span></span>  <span data-ttu-id="7529d-160">Codice di Visual Studio esegue l'operazione nel hello **lanuch.json** file.</span><span class="sxs-lookup"><span data-stu-id="7529d-160">Visual Studio Code does this in hello **lanuch.json** file.</span></span>  <span data-ttu-id="7529d-161">Cercare una proprietà denominata **args** e aggiungere una matrice di valori di stringa per i parametri, in modo che risulti simile toothis: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="7529d-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar toothis:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="7529d-162">Iniziare a elencare i profili.</span><span class="sxs-lookup"><span data-stu-id="7529d-162">Let's start by listing our profiles.</span></span>

![Elencare i profili](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="7529d-164">Viene restituita una matrice vuota.</span><span class="sxs-lookup"><span data-stu-id="7529d-164">We got back an empty array.</span></span>  <span data-ttu-id="7529d-165">Si tratta di un risultato previsto, dato che non c'è alcun profilo nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="7529d-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="7529d-166">Creare un profilo.</span><span class="sxs-lookup"><span data-stu-id="7529d-166">Let's create a profile now.</span></span>

![Creare il profilo](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="7529d-168">Aggiungere un endpoint.</span><span class="sxs-lookup"><span data-stu-id="7529d-168">Now, let's add an endpoint.</span></span>

![Creare un endpoint](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="7529d-170">Infine, eliminare il profilo.</span><span class="sxs-lookup"><span data-stu-id="7529d-170">Finally, let's delete our profile.</span></span>

![Eliminare il profilo](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="7529d-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7529d-172">Next Steps</span></span>
<span data-ttu-id="7529d-173">il progetto completato hello toosee da questa procedura dettagliata, [scaricare l'esempio hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="7529d-173">toosee hello completed project from this walkthrough, [download hello sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="7529d-174">riferimento hello toosee per hello Azure CDN SDK per Node.js, hello vista [riferimento](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="7529d-174">toosee hello reference for hello Azure CDN SDK for Node.js, view hello [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="7529d-175">documentazione aggiuntiva toofind su hello Azure SDK per Node.js, hello vista [completo riferimento](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="7529d-175">toofind additional documentation on hello Azure SDK for Node.js, view hello [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="7529d-176">Gestire le risorse della rete CDN con [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="7529d-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

