---
title: Introduzione ad Azure CDN SDK per Node.js | Documentazione Microsoft
description: Informazioni su come scrivere applicazioni Node.js per la gestione della rete CDN di Azure.
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
ms.openlocfilehash: 46ae8cd9775432d126cbde856c1fb06ea319297e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-cdn-development"></a><span data-ttu-id="d779f-103">Introduzione allo sviluppo della rete CDN di Azure</span><span class="sxs-lookup"><span data-stu-id="d779f-103">Get started with Azure CDN development</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="d779f-104">Node.JS</span><span class="sxs-lookup"><span data-stu-id="d779f-104">Node.js</span></span>](cdn-app-dev-node.md)
> * [<span data-ttu-id="d779f-105">.NET</span><span class="sxs-lookup"><span data-stu-id="d779f-105">.NET</span></span>](cdn-app-dev-net.md)
> 
> 

<span data-ttu-id="d779f-106">È possibile usare [Azure CDN SDK per Node.js](https://www.npmjs.com/package/azure-arm-cdn) per automatizzare la creazione e la gestione dei profili e degli endpoint di rete CDN.</span><span class="sxs-lookup"><span data-stu-id="d779f-106">You can use the [Azure CDN SDK for Node.js](https://www.npmjs.com/package/azure-arm-cdn) to automate creation and management of CDN profiles and endpoints.</span></span>  <span data-ttu-id="d779f-107">Questa esercitazione illustra nel dettaglio la creazione di una semplice applicazione console Node.js che dimostra varie operazioni tra quelle disponibili.</span><span class="sxs-lookup"><span data-stu-id="d779f-107">This tutorial walks through the creation of a simple Node.js console application that demonstrates several of the available operations.</span></span>  <span data-ttu-id="d779f-108">Lo scopo di questa esercitazione non è fornire una descrizione dettagliata di tutti gli aspetti di Azure CDN SDK per Node.js.</span><span class="sxs-lookup"><span data-stu-id="d779f-108">This tutorial is not intended to describe all aspects of the Azure CDN SDK for Node.js in detail.</span></span>

<span data-ttu-id="d779f-109">Per completare questa esercitazione, è necessario che [Node.js](http://www.nodejs.org) **4.x.x** o versione successiva sia già installato e configurato.</span><span class="sxs-lookup"><span data-stu-id="d779f-109">To complete this tutorial, you should already have [Node.js](http://www.nodejs.org) **4.x.x** or higher installed and configured.</span></span>  <span data-ttu-id="d779f-110">Per creare l'applicazione Node.js è possibile usare qualsiasi editor di testo.</span><span class="sxs-lookup"><span data-stu-id="d779f-110">You can use any text editor you want to create your Node.js application.</span></span>  <span data-ttu-id="d779f-111">Per scrivere questa esercitazione è stato usato [Visual Studio Code](https://code.visualstudio.com).</span><span class="sxs-lookup"><span data-stu-id="d779f-111">To write this tutorial, I used [Visual Studio Code](https://code.visualstudio.com).</span></span>  

> [!TIP]
> <span data-ttu-id="d779f-112">Il [progetto completato di questa esercitazione](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) è disponibile per il download in MSDN.</span><span class="sxs-lookup"><span data-stu-id="d779f-112">The [completed project from this tutorial](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) is available for download on MSDN.</span></span>
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a><span data-ttu-id="d779f-113">Creare il progetto e aggiungere le dipendenze NPM</span><span class="sxs-lookup"><span data-stu-id="d779f-113">Create your project and add NPM dependencies</span></span>
<span data-ttu-id="d779f-114">Ora che abbiamo creato un gruppo di risorse per i profili di rete CDN e assegnato all'applicazione Azure AD l'autorizzazione per gestire i profili e gli endpoint della rete CDN all'interno del gruppo, è possibile iniziare a creare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d779f-114">Now that we've created a resource group for our CDN profiles and given our Azure AD application permission to manage CDN profiles and endpoints within that group, we can start creating our application.</span></span>

<span data-ttu-id="d779f-115">Creare una cartella in cui archiviare l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="d779f-115">Create a folder to store your application.</span></span>  <span data-ttu-id="d779f-116">Da una console con gli strumenti Node.js nel percorso corrente, posizionarsi sulla nuova cartella e inizializzare il progetto eseguendo:</span><span class="sxs-lookup"><span data-stu-id="d779f-116">From a console with the Node.js tools in your current path, set your current location to this new folder and initialize your project by executing:</span></span>

    npm init

<span data-ttu-id="d779f-117">Verrà quindi visualizzata una serie di domande per inizializzare il progetto.</span><span class="sxs-lookup"><span data-stu-id="d779f-117">You will then be presented a series of questions to initialize your project.</span></span>  <span data-ttu-id="d779f-118">Come **punto di ingresso**questa esercitazione usa *app.js*.</span><span class="sxs-lookup"><span data-stu-id="d779f-118">For **entry point**, this tutorial uses *app.js*.</span></span>  <span data-ttu-id="d779f-119">È possibile visualizzare le altre scelte nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="d779f-119">You can see my other choices in the following example.</span></span>

![Output NPM iniziale](./media/cdn-app-dev-node/cdn-npm-init.png)

<span data-ttu-id="d779f-121">A questo punto il progetto viene inizializzato con un file *packages.json* .</span><span class="sxs-lookup"><span data-stu-id="d779f-121">Our project is now initialized with a *packages.json* file.</span></span>  <span data-ttu-id="d779f-122">Il progetto userà alcune librerie di Azure contenute in pacchetti NPM.</span><span class="sxs-lookup"><span data-stu-id="d779f-122">Our project is going to use some Azure libraries contained in NPM packages.</span></span>  <span data-ttu-id="d779f-123">Verranno usati il runtime del client di Azure per Node.js (ms-rest-azure) e la libreria client della rete CDN di Azure per Node.js (azure-arm-cd).</span><span class="sxs-lookup"><span data-stu-id="d779f-123">We'll use the Azure Client Runtime for Node.js (ms-rest-azure) and the Azure CDN Client Library for Node.js (azure-arm-cd).</span></span>  <span data-ttu-id="d779f-124">Aggiungere tali elementi al progetto come dipendenze.</span><span class="sxs-lookup"><span data-stu-id="d779f-124">Let's add those to the project as dependencies.</span></span>

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

<span data-ttu-id="d779f-125">Al termine dell'installazione dei pacchetti, il file *package.json* dovrebbe avere un aspetto simile a questo esempio, anche se i numeri di versione possono variare:</span><span class="sxs-lookup"><span data-stu-id="d779f-125">After the packages are done installing, the *package.json* file should look similar to this example (version numbers may differ):</span></span>

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

<span data-ttu-id="d779f-126">Infine, usare l'editor di testo per creare un file di testo vuoto e salvarlo nella radice della cartella di progetto denominandolo *app.js*.</span><span class="sxs-lookup"><span data-stu-id="d779f-126">Finally, using your text editor, create a blank text file and save it in the root of our project folder as *app.js*.</span></span>  <span data-ttu-id="d779f-127">Ora è possibile iniziare a scrivere codice.</span><span class="sxs-lookup"><span data-stu-id="d779f-127">We're now ready to begin writing code.</span></span>

## <a name="requires-constants-authentication-and-structure"></a><span data-ttu-id="d779f-128">Istruzioni require, costanti, autenticazione e struttura</span><span class="sxs-lookup"><span data-stu-id="d779f-128">Requires, constants, authentication, and structure</span></span>
<span data-ttu-id="d779f-129">Aprire *app.js* nell'editor e scrivere la struttura di base del programma.</span><span class="sxs-lookup"><span data-stu-id="d779f-129">With *app.js* open in our editor, let's get the basic structure of our program written.</span></span>

1. <span data-ttu-id="d779f-130">Aggiungere le istruzioni "require" per i pacchetti NPM all'inizio inserendo il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="d779f-130">Add the "requires" for our NPM packages at the top with the following:</span></span>
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. <span data-ttu-id="d779f-131">È necessario definire alcune costanti che i metodi useranno.</span><span class="sxs-lookup"><span data-stu-id="d779f-131">We need to define some constants our methods will use.</span></span>  <span data-ttu-id="d779f-132">Aggiungere il codice seguente.</span><span class="sxs-lookup"><span data-stu-id="d779f-132">Add the following.</span></span>  <span data-ttu-id="d779f-133">Sostituire i segnaposto, incluse le **&lt;parentesi acute&gt;**, con i valori necessari.</span><span class="sxs-lookup"><span data-stu-id="d779f-133">Be sure to replace the placeholders, including the **&lt;angle brackets&gt;**, with your own values as needed.</span></span>
   
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
3. <span data-ttu-id="d779f-134">Successivamente, verrà creata un'istanza del client di gestione della rete CDN a cui verranno assegnate le credenziali.</span><span class="sxs-lookup"><span data-stu-id="d779f-134">Next, we'll instantiate the CDN management client and give it our credentials.</span></span>
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="d779f-135">Se si usa l'autenticazione del singolo utente, queste due righe di codice avranno un aspetto leggermente diverso.</span><span class="sxs-lookup"><span data-stu-id="d779f-135">If you are using individual user authentication, these two lines will look slightly different.</span></span>
   
   > [!IMPORTANT]
   > <span data-ttu-id="d779f-136">Usare questo esempio di codice solo se si sceglie l'autenticazione interattiva del singolo utente anziché un'entità servizio.</span><span class="sxs-lookup"><span data-stu-id="d779f-136">Only use this code sample if you are choosing to have individual user authentication instead of a service principal.</span></span>  <span data-ttu-id="d779f-137">Custodire attentamente le credenziali utente individuali e tenerle segrete.</span><span class="sxs-lookup"><span data-stu-id="d779f-137">Be careful to guard your individual user credentials and keep them secret.</span></span>
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    <span data-ttu-id="d779f-138">Sostituire le voci tra **&lt;parentesi acute&gt;** con le informazioni corrette.</span><span class="sxs-lookup"><span data-stu-id="d779f-138">Be sure to replace the items in **&lt;angle brackets&gt;** with the correct information.</span></span>  <span data-ttu-id="d779f-139">Sostituire `<redirect URI>`con l'URI di reindirizzamento immesso al momento della registrazione dell'applicazione in Azure AD.</span><span class="sxs-lookup"><span data-stu-id="d779f-139">For `<redirect URI>`, use the redirect URI you entered when you registered the application in Azure AD.</span></span>
4. <span data-ttu-id="d779f-140">L'applicazione console Node.js necessita di alcuni parametri della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="d779f-140">Our Node.js console application is going to take some command-line parameters.</span></span>  <span data-ttu-id="d779f-141">Verificare che venga passato almeno un parametro.</span><span class="sxs-lookup"><span data-stu-id="d779f-141">Let's validate that at least one parameter was passed.</span></span>
   
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
5. <span data-ttu-id="d779f-142">Nella parte principale del programma si passa poi ad altre funzioni, in base ai parametri che sono stati passati.</span><span class="sxs-lookup"><span data-stu-id="d779f-142">That brings us to the main part of our program, where we branch off to other functions based on what parameters were passed.</span></span>
   
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
6. <span data-ttu-id="d779f-143">In diversi punti del programma sarà necessario assicurarsi che venga passato il numero appropriato di parametri e visualizzare gli argomenti della Guida in caso di inesattezze.</span><span class="sxs-lookup"><span data-stu-id="d779f-143">At several places in our program, we'll need to make sure the right number of parameters were passed in and display some help if they don't look correct.</span></span>  <span data-ttu-id="d779f-144">Creare le funzioni necessarie a tale scopo.</span><span class="sxs-lookup"><span data-stu-id="d779f-144">Let's create functions to do that.</span></span>
   
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
7. <span data-ttu-id="d779f-145">Le funzioni da usare nel client di gestione della rete CDN sono asincrone. È quindi necessario un metodo di richiamata dopo l'esecuzione delle funzioni.</span><span class="sxs-lookup"><span data-stu-id="d779f-145">Finally, the functions we'll be using on the CDN management client are asynchronous, so they need a method to call back when they're done.</span></span>  <span data-ttu-id="d779f-146">Creare un metodo che possa visualizzare l'output del client di gestione dell'eventuale rete CDN e uscire dal programma normalmente.</span><span class="sxs-lookup"><span data-stu-id="d779f-146">Let's make one that can display the output from the CDN management client (if any) and exit the program gracefully.</span></span>
   
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

<span data-ttu-id="d779f-147">Ora che la struttura di base del programma è stata scritta, è necessario creare le funzioni che vengono chiamate in base ai parametri.</span><span class="sxs-lookup"><span data-stu-id="d779f-147">Now that the basic structure of our program is written, we should create the functions called based on our parameters.</span></span>

## <a name="list-cdn-profiles-and-endpoints"></a><span data-ttu-id="d779f-148">Elencare i profili e gli endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="d779f-148">List CDN profiles and endpoints</span></span>
<span data-ttu-id="d779f-149">Scrivere il codice necessario per elencare i profili e gli endpoint esistenti.</span><span class="sxs-lookup"><span data-stu-id="d779f-149">Let's start with code to list our existing profiles and endpoints.</span></span>  <span data-ttu-id="d779f-150">I commenti al codice forniscono la sintassi prevista che permette di determinare la posizione dei parametri.</span><span class="sxs-lookup"><span data-stu-id="d779f-150">My code comments provide the expected syntax so we know where each parameter goes.</span></span>

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

## <a name="create-cdn-profiles-and-endpoints"></a><span data-ttu-id="d779f-151">Creare profili ed endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="d779f-151">Create CDN profiles and endpoints</span></span>
<span data-ttu-id="d779f-152">Scrivere le funzioni per la creazione dei profili e degli endpoint.</span><span class="sxs-lookup"><span data-stu-id="d779f-152">Next, we'll write the functions to create profiles and endpoints.</span></span>

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

## <a name="purge-an-endpoint"></a><span data-ttu-id="d779f-153">Ripulire un endpoint</span><span class="sxs-lookup"><span data-stu-id="d779f-153">Purge an endpoint</span></span>
<span data-ttu-id="d779f-154">Supponendo che l'endpoint sia stato creato, è consigliabile eseguire nel programma un'attività comune di eliminazione del contenuto dell'endpoint.</span><span class="sxs-lookup"><span data-stu-id="d779f-154">Assuming the endpoint has been created, one common task that we might want to perform in our program is purging content in our endpoint.</span></span>

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a><span data-ttu-id="d779f-155">Eliminare profili ed endpoint della rete CDN</span><span class="sxs-lookup"><span data-stu-id="d779f-155">Delete CDN profiles and endpoints</span></span>
<span data-ttu-id="d779f-156">L'ultima funzione da includere elimina gli endpoint e i profili.</span><span class="sxs-lookup"><span data-stu-id="d779f-156">The last function we will include deletes endpoints and profiles.</span></span>

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

## <a name="running-the-program"></a><span data-ttu-id="d779f-157">Esecuzione del programma</span><span class="sxs-lookup"><span data-stu-id="d779f-157">Running the program</span></span>
<span data-ttu-id="d779f-158">Ora è possibile eseguire il programma Node.js con un debugger a scelta o alla console.</span><span class="sxs-lookup"><span data-stu-id="d779f-158">We can now execute our Node.js program using our favorite debugger or at the console.</span></span>

> [!TIP]
> <span data-ttu-id="d779f-159">Se si usa Visual Studio Code come debugger, è necessario configurare l'ambiente per passare i parametri della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="d779f-159">If you're using Visual Studio Code as your debugger, you'll need to set up your environment to pass in the command-line parameters.</span></span>  <span data-ttu-id="d779f-160">Visual Studio Code esegue questa operazione nel file **launch.json** .</span><span class="sxs-lookup"><span data-stu-id="d779f-160">Visual Studio Code does this in the **lanuch.json** file.</span></span>  <span data-ttu-id="d779f-161">Cercare una proprietà denominata **args** e aggiungere una matrice di valori stringa per i parametri, in modo che abbia un aspetto analogo al seguente: `"args": ["list", "profiles"]`.</span><span class="sxs-lookup"><span data-stu-id="d779f-161">Look for a property named **args** and add an array of string values for your parameters, so that it looks similar to this:  `"args": ["list", "profiles"]`.</span></span>
> 
> 

<span data-ttu-id="d779f-162">Iniziare a elencare i profili.</span><span class="sxs-lookup"><span data-stu-id="d779f-162">Let's start by listing our profiles.</span></span>

![Elencare i profili](./media/cdn-app-dev-node/cdn-list-profiles.png)

<span data-ttu-id="d779f-164">Viene restituita una matrice vuota.</span><span class="sxs-lookup"><span data-stu-id="d779f-164">We got back an empty array.</span></span>  <span data-ttu-id="d779f-165">Si tratta di un risultato previsto, dato che non c'è alcun profilo nel gruppo di risorse.</span><span class="sxs-lookup"><span data-stu-id="d779f-165">Since we don't have any profiles in our resource group, that's expected.</span></span>  <span data-ttu-id="d779f-166">Creare un profilo.</span><span class="sxs-lookup"><span data-stu-id="d779f-166">Let's create a profile now.</span></span>

![Creare il profilo](./media/cdn-app-dev-node/cdn-create-profile.png)

<span data-ttu-id="d779f-168">Aggiungere un endpoint.</span><span class="sxs-lookup"><span data-stu-id="d779f-168">Now, let's add an endpoint.</span></span>

![Creare un endpoint](./media/cdn-app-dev-node/cdn-create-endpoint.png)

<span data-ttu-id="d779f-170">Infine, eliminare il profilo.</span><span class="sxs-lookup"><span data-stu-id="d779f-170">Finally, let's delete our profile.</span></span>

![Eliminare il profilo](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a><span data-ttu-id="d779f-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d779f-172">Next Steps</span></span>
<span data-ttu-id="d779f-173">Per vedere il progetto completato di questa procedura dettagliata, [scaricare l'esempio](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span><span class="sxs-lookup"><span data-stu-id="d779f-173">To see the completed project from this walkthrough, [download the sample](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).</span></span>

<span data-ttu-id="d779f-174">Per informazioni su Azure CDN SDK per Node.js, vedere il [riferimento](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span><span class="sxs-lookup"><span data-stu-id="d779f-174">To see the reference for the Azure CDN SDK for Node.js, view the [reference](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).</span></span>

<span data-ttu-id="d779f-175">Per altra documentazione su Azure SDK per Node.js, vedere il [riferimento completo](http://azure.github.io/azure-sdk-for-node/).</span><span class="sxs-lookup"><span data-stu-id="d779f-175">To find additional documentation on the Azure SDK for Node.js, view the [full reference](http://azure.github.io/azure-sdk-for-node/).</span></span>

<span data-ttu-id="d779f-176">Gestire le risorse della rete CDN con [PowerShell](cdn-manage-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="d779f-176">Manage your CDN resources with [PowerShell](cdn-manage-powershell.md).</span></span>

