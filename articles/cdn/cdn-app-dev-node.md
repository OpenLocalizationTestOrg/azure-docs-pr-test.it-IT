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
# <a name="get-started-with-azure-cdn-development"></a>Introduzione allo sviluppo della rete CDN di Azure
> [!div class="op_single_selector"]
> * [Node.JS](cdn-app-dev-node.md)
> * [.NET](cdn-app-dev-net.md)
> 
> 

È possibile utilizzare hello [SDK della rete CDN di Azure per Node.js](https://www.npmjs.com/package/azure-arm-cdn) tooautomate creazione e la gestione dei profili di rete CDN e gli endpoint.  In questa esercitazione vengono illustrati la creazione di hello di una semplice applicazione console Node.js che vengono illustrate diverse operazioni disponibili hello.  In questa esercitazione è non è adatto toodescribe tutti gli aspetti di hello rete CDN di Azure SDK per Node.js in dettaglio.

toocomplete questa esercitazione, dovrebbe già disporre [Node.js](http://www.nodejs.org) **4.x.x** o versione successiva installato e configurato.  È possibile utilizzare qualsiasi editor di testo cui toocreate l'applicazione di Node.js.  toowrite questa esercitazione, utilizzato [codice di Visual Studio](https://code.visualstudio.com).  

> [!TIP]
> Hello [progetto completato questa esercitazione](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74) è disponibile per il download su MSDN.
> 
> 

[!INCLUDE [cdn-app-dev-prep](../../includes/cdn-app-dev-prep.md)]

## <a name="create-your-project-and-add-npm-dependencies"></a>Creare il progetto e aggiungere le dipendenze NPM
Ora che è stato creato un gruppo di risorse per i profili di rete CDN e specificati i profili di rete CDN di Azure AD applicazione autorizzazione toomanage e gli endpoint all'interno del gruppo, è possibile iniziare a creare l'applicazione.

Creare una cartella toostore l'applicazione.  Da una console con gli strumenti di Node.js hello nel percorso corrente, impostare la nuova cartella di percorso toothis corrente e inizializzare il progetto tramite l'esecuzione:

    npm init

Sarà quindi visualizzata una serie di domande tooinitialize il progetto.  Come **punto di ingresso**questa esercitazione usa *app.js*.  È possibile visualizzare le altre scelte in hello di esempio seguente.

![Output NPM iniziale](./media/cdn-app-dev-node/cdn-npm-init.png)

A questo punto il progetto viene inizializzato con un file *packages.json* .  Il progetto verrà toouse alcune librerie di Azure contenuti nei pacchetti NPM.  Utilizzeremo hello Runtime Client di Azure per Node.js (ms-rest azure) e hello libreria Client della rete CDN di Azure per Node.js (azure-arm cd).  Aggiungere tali progetti toohello come dipendenze.

    npm install --save ms-rest-azure
    npm install --save azure-arm-cdn

Dopo aver hello pacchetti vengono eseguiti l'installazione, hello *package. JSON* file dovrebbe essere simile toothis esempio (i numeri di versione potrebbero):

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

Infine, tramite l'editor di testo, creare un file di testo vuoto e salvarlo nella radice hello la cartella di progetto come *app.js*.  Si è ora pronto toobegin la scrittura di codice.

## <a name="requires-constants-authentication-and-structure"></a>Istruzioni require, costanti, autenticazione e struttura
Con *app.js* aprire l'editor, possiamo procedere alla struttura di base di questo programma scritto hello.

1. Aggiungere hello "richiede" per i pacchetti NPM nella parte superiore di hello con seguenti hello:
   
    ``` javascript
    var msRestAzure = require('ms-rest-azure');
    var cdnManagementClient = require('azure-arm-cdn');
    ```
2. È necessario toodefine alcune costanti che utilizzeranno i metodi.  Aggiungere il seguente hello.  Essere tooreplace che segnaposto hello, tra cui hello  **&lt;angolari&gt;**, con valori personalizzati in base alle esigenze.
   
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
3. Viene successivamente, creare un'istanza client di gestione della rete CDN hello e assegnarle il tipo di credenziali.
   
    ``` javascript
    var credentials = new msRestAzure.ApplicationTokenCredentials(clientId, tenantId, clientSecret);
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Se si usa l'autenticazione del singolo utente, queste due righe di codice avranno un aspetto leggermente diverso.
   
   > [!IMPORTANT]
   > Usare questo esempio di codice solo se si sceglie l'autenticazione utente toohave anziché un'entità servizio.  Essere tooguard attenzione le credenziali utente e le mantiene segreta.
   > 
   > 
   
    ``` javascript
    var credentials = new msRestAzure.UserTokenCredentials(clientId, 
        tenantId, '<username>', '<password>', '<redirect URI>');
    var cdnClient = new cdnManagementClient(credentials, subscriptionId);
    ```
   
    Essere tooreplace che gli elementi hello  **&lt;angolari&gt;**  con hello correggere le informazioni.  Per `<redirect URI>`, utilizzare il reindirizzamento di hello URI immesso al momento della registrazione di un'applicazione hello in Azure AD.
4. L'applicazione console Node.js verrà tootake alcuni parametri della riga di comando.  Verificare che venga passato almeno un parametro.
   
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
5. Siamo arrivati toohello parte principale di questo programma, in cui si crei rami funzioni tooother in base alle quali i parametri passati.
   
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
6. In diverse posizioni in questo programma, è necessario toomake certi del numero corretto di parametri hello sono stato passato e Visualizza alcuni argomenti della Guida se queste non sembrano corrette.  È possibile creare funzioni toodo che.
   
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
7. Infine, le funzioni hello che verrà usato nel client di gestione della rete CDN hello sono asincrone, pertanto è necessario un metodo toocall quando completati.  Verifichiamo che è possibile visualizzare l'output di hello di client di gestione della rete CDN hello (se presente) e uscire dal programma di hello normalmente.
   
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

Struttura di base hello di questo programma è stato scritto, è necessario creare funzioni hello chiamate in base ai nostri parametri.

## <a name="list-cdn-profiles-and-endpoints"></a>Elencare i profili e gli endpoint della rete CDN
Iniziamo con toolist codice i profili e gli endpoint.  I commenti di codice forniscono la sintassi di hello previsto in modo da sapere dove ogni parametro memorizzate.

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

## <a name="create-cdn-profiles-and-endpoints"></a>Creare profili ed endpoint della rete CDN
Successivamente, si scriverà gli endpoint e i profili di toocreate funzioni hello.

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

## <a name="purge-an-endpoint"></a>Ripulire un endpoint
Supponendo che l'endpoint di hello è stato creato, un'attività comune che si voglia tooperform in questo programma è eliminazione contenuto in questo endpoint.

```javascript
// purge <profile name> <endpoint name> <path>
function cdnPurge() {
    requireParms(4);
    console.log("Purging endpoint...");
    var purgeContentPaths = [ parms[3] ];
    cdnClient.endpoints.purgeContent(parms[2], parms[1], resourceGroupName, purgeContentPaths, callback);
}
```

## <a name="delete-cdn-profiles-and-endpoints"></a>Eliminare profili ed endpoint della rete CDN
ultima funzione Hello che includeremo Elimina profili e gli endpoint.

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

## <a name="running-hello-program"></a>Programma hello in esecuzione
È ora possibile eseguire il programma di Node.js tramite il debugger Preferiti o console hello.

> [!TIP]
> Se si utilizza codice di Visual Studio, come il debugger, è necessario tooset backup toopass l'ambiente nei parametri della riga di comando hello.  Codice di Visual Studio esegue l'operazione nel hello **lanuch.json** file.  Cercare una proprietà denominata **args** e aggiungere una matrice di valori di stringa per i parametri, in modo che risulti simile toothis: `"args": ["list", "profiles"]`.
> 
> 

Iniziare a elencare i profili.

![Elencare i profili](./media/cdn-app-dev-node/cdn-list-profiles.png)

Viene restituita una matrice vuota.  Si tratta di un risultato previsto, dato che non c'è alcun profilo nel gruppo di risorse.  Creare un profilo.

![Creare il profilo](./media/cdn-app-dev-node/cdn-create-profile.png)

Aggiungere un endpoint.

![Creare un endpoint](./media/cdn-app-dev-node/cdn-create-endpoint.png)

Infine, eliminare il profilo.

![Eliminare il profilo](./media/cdn-app-dev-node/cdn-delete-profile.png)

## <a name="next-steps"></a>Passaggi successivi
il progetto completato hello toosee da questa procedura dettagliata, [scaricare l'esempio hello](https://code.msdn.microsoft.com/Azure-CDN-SDK-for-Nodejs-c712bc74).

riferimento hello toosee per hello Azure CDN SDK per Node.js, hello vista [riferimento](http://azure.github.io/azure-sdk-for-node/azure-arm-cdn/latest/).

documentazione aggiuntiva toofind su hello Azure SDK per Node.js, hello vista [completo riferimento](http://azure.github.io/azure-sdk-for-node/).

Gestire le risorse della rete CDN con [PowerShell](cdn-manage-powershell.md).

