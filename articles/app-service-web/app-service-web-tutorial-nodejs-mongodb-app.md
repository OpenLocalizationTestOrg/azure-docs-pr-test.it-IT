---
title: aaaBuild un'app web Node. js e MongoDB in Azure | Documenti Microsoft
description: Informazioni su come tooget un'app Node.js Usa Azure, con connessione tooa Cosmos DB database con una stringa di connessione di MongoDB.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 0b4d7d0e-e984-49a1-a57a-3c0caa955f0e
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 05/04/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 532251c51ed6f8513e6e366393e889b67a85e5b9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-nodejs-and-mongodb-web-app-in-azure"></a>Creare un'app Web Node.js e MongoDB in Azure

Le app Web di Azure offrono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione. Questa esercitazione viene illustrato come un Node.js toocreate web app in Azure e connetterla database MongoDB tooa. Al termine, si avrà un'applicazione MEAN (MongoDB, Express, AngularJS e Node.js) in esecuzione nel [servizio app di Azure](app-service-web-overview.md). Per semplicità, l'applicazione di esempio hello utilizza hello [framework web MEAN.js](http://meanjs.org/).

![App MEAN.js in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Contenuto dell'esercitazione:

> [!div class="checklist"]
> * Creare un database MongoDB in Azure
> * Connettersi a un tooMongoDB app Node.js
> * Distribuire hello app tooAzure
> * Modello di dati hello e ridistribuire l'applicazione hello
> * Eseguire lo streaming dei log di diagnostica in Azure
> * Gestire app hello in hello portale di Azure

## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

1. [Installare Git](https://git-scm.com/)
1. [Installare Node.js e NPM](https://nodejs.org/)
1. [Installare Gulp.js](http://gulpjs.com/), richiesto da [MEAN.js](http://meanjs.org/docs/0.5.x/#getting-started)
1. [Installare ed eseguire MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-mongodb"></a>Testare il MongoDB locale

Finestra terminal aprire hello e `cd` toohello `bin` directory di installazione di MongoDB. In questa esercitazione, è possibile utilizzare questa finestra terminale di toorun tutti i comandi di hello.

Eseguire `mongo` nell'istanza hello tooconnect terminal tooyour locale MongoDB server.

```bash
mongo
```

Se la connessione ha esito positivo significa che il database MongoDB è già in esecuzione. In caso contrario, assicurarsi che sia stato avviato il database MongoDB locale seguendo i passaggi di hello in [installare MongoDB Community Edition](https://docs.mongodb.com/manual/administration/install-community/). Spesso, MongoDB è installato, ma è comunque necessario toostart eseguendo `mongod`. 

Al termine di test del database MongoDB, digitare `Ctrl+C` in hello terminal. 

## <a name="create-local-nodejs-app"></a>Creare l'app Node.js locale

In questo passaggio, impostare il progetto Node.js locale di hello.

### <a name="clone-hello-sample-application"></a>Applicazione di esempio hello clonare

Nella finestra terminal hello `cd` tooa directory di lavoro.  

Eseguire hello seguenti repository di esempio di comando tooclone hello. 

```bash
git clone https://github.com/Azure-Samples/meanjs.git
```

Il repository di esempio contiene una copia di hello [MEAN.js repository](https://github.com/meanjs/mean). È toorun modificate nel servizio App (per ulteriori informazioni, vedere repository MEAN.js hello [file README](https://github.com/Azure-Samples/meanjs/blob/master/README.md)).

### <a name="run-hello-application"></a>Eseguire un'applicazione hello

Eseguire hello i pacchetti hello necessario tooinstall i comandi seguenti e avviare un'applicazione hello.

```bash
cd meanjs
npm install
npm start
```

Quando l'applicazione hello è stato caricato completamente, viene visualizzato un codice simile toohello seguente messaggio:

```
--
MEAN.JS - Development Environment

Environment:     development
Server:          http://0.0.0.0:3000
Database:        mongodb://localhost/mean-dev
App version:     0.5.0
MEAN.JS version: 0.5.0
--
```

Passare toohttp://localhost:3000 in un browser. Fare clic su **iscrizione** in hello menu superiore e creare un utente test. 

applicazione di esempio MEAN.js Hello archivia i dati utente nel database di hello. Se hanno esito positivo alla creazione di un utente ed eseguire l'accesso, l'app sta scrivendo database MongoDB locale di dati toohello.

![MEAN.js si connette correttamente tooMongoDB](./media/app-service-web-tutorial-nodejs-mongodb-app/mongodb-connect-success.png)

Selezionare **amministrazione > Gestisci articoli** tooadd alcuni articoli.

toostop Node.js in qualsiasi momento, premere `Ctrl+C` in hello terminal. 

## <a name="create-production-mongodb"></a>Creare MongoDB di produzione

In questo passaggio si crea un database MongoDB in Azure. Quando l'applicazione viene distribuita tooAzure, Usa questo database cloud.

Per MongoDB, questa esercitazione usa [Azure Cosmos DB](/azure/documentdb/). COSMOS DB supporta le connessioni client MongoDB.

### <a name="log-in-tooazure"></a>Accedi tooAzure

Si userà hello Azure CLI 2.0 toocreate hello risorse necessarie toohost l'app in Azure. Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.

```azurecli-interactive
az login
```   

### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un gruppo di risorse con hello [gruppo az creare](/cli/azure/group#create) comando.

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Hello seguente viene creato un gruppo di risorse nell'area Europa occidentale hello.

```azurecli-interactive
az group create --name myResourceGroup --location "West Europe"
```

Hello utilizzare [az appservice elenco posizioni](/cli/azure/appservice#list-locations) posizioni disponibili toolist di comando CLI di Azure. 

### <a name="create-a-cosmos-db-account"></a>Creare un account Cosmos DB

Creare un account DB Cosmos con hello [cosmosdb az creare](/cli/azure/cosmosdb#create) comando.

In hello seguente comando, sostituire un nome univoco di DB Cosmos per hello  *\<cosmosdb_name >* segnaposto. Questo nome viene utilizzato come parte di hello dell'endpoint Cosmos DB hello `https://<cosmosdb_name>.documents.azure.com/`, in modo che nome hello deve toobe univoco in tutti gli account DB Cosmos in Azure. nome Hello deve contenere solo lettere minuscole, numeri e caratteri di trattino (-) hello e deve essere compresa tra 3 e 50 caratteri.

```azurecli-interactive
az cosmosdb create \
    --name <cosmosdb_name> \
    --resource-group myResourceGroup \
    --kind MongoDB
```

Hello *-MongoDB kind* parametro consente le connessioni client di MongoDB.

Quando viene creato l'account Cosmos DB hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

```json
{
  "consistencyPolicy":
  {
    "defaultConsistencyLevel": "Session",
    "maxIntervalInSeconds": 5,
    "maxStalenessPrefix": 100
  },
  "databaseAccountOfferType": "Standard",
  "documentEndpoint": "https://<cosmosdb_name>.documents.azure.com:443/",
  "failoverPolicies": 
  ...
  < Output truncated for readability >
}
```

## <a name="connect-app-tooproduction-mongodb"></a>Connettere l'app tooproduction MongoDB

In questo passaggio è connettersi MEAN.js esempio database dell'applicazione toohello Cosmos DB che appena creato, utilizzando una stringa di connessione di MongoDB. 

### <a name="retrieve-hello-database-key"></a>Recuperare una chiave del database hello

tooconnect toohello DB Cosmos database, è necessario chiave hello del database. Hello utilizzare [az cosmosdb elenco chiavi](/cli/azure/cosmosdb#list-keys) chiave primaria di comando tooretrieve hello.

```azurecli-interactive
az cosmosdb list-keys --name <cosmosdb_name> --resource-group myResourceGroup
```

Hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

```json
{
  "primaryMasterKey": "RS4CmUwzGRASJPMoc0kiEvdnKmxyRILC9BWisAYh3Hq4zBYKr0XQiSE4pqx3UchBeO4QRCzUt1i7w0rOkitoJw==",
  "primaryReadonlyMasterKey": "HvitsjIYz8TwRmIuPEUAALRwqgKOzJUjW22wPL2U8zoMVhGvregBkBk9LdMTxqBgDETSq7obbwZtdeFY7hElTg==",
  "secondaryMasterKey": "Lu9aeZTiXU4PjuuyGBbvS1N9IRG3oegIrIh95U6VOstf9bJiiIpw3IfwSUgQWSEYM3VeEyrhHJ4rn3Ci0vuFqA==",
  "secondaryReadonlyMasterKey": "LpsCicpVZqHRy7qbMgrzbRKjbYCwCKPQRl0QpgReAOxMcggTvxJFA94fTi0oQ7xtxpftTJcXkjTirQ0pT7QFrQ=="
}
```

Copiare il valore di hello di `primaryMasterKey`. È necessario queste informazioni nel passaggio successivo hello.

<a name="devconfig"></a>
### <a name="configure-hello-connection-string-in-your-nodejs-application"></a>Configurare la stringa di connessione hello nell'applicazione Node.js

Nell'archivio MEAN.js aprire _config/env/production.js_.

In hello `db` oggetto, aggiornare il valore di hello di `uri`:

* Sostituire hello due  *\<cosmosdb_name >* segnaposto con il nome del database DB Cosmos.
* Sostituire hello  *\<primary_master_key >* segnaposto con chiave hello copiato nel passaggio precedente hello.

Hello codice seguente viene illustrato hello `db` oggetto:

```javascript
db: {
  uri: 'mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false',
  ...
},
```

Hello `ssl=true` opzione è necessaria perché [DB Cosmos richiede SSL](../cosmos-db/connect-mongodb-account.md#connection-string-requirements). 

Salvare le modifiche.

### <a name="test-hello-application-in-production-mode"></a>Testare l'applicazione hello in modalità di produzione 

Eseguire i seguenti script toominify e bundle di comando per l'ambiente di produzione hello hello. Questo processo genera file hello necessari dall'ambiente di produzione hello.

```bash
gulp prod
```

Esecuzione hello seguente stringa di comando toouse hello connessione configurata in _config/env/production.js_.

```bash
NODE_ENV=production node server.js
```

`NODE_ENV=production`Imposta variabile di ambiente hello indicante toorun Node.js in ambiente di produzione hello.  `node server.js`Avvia hello server Node.js con `server.js` nella radice del repository. Questo è il modo in cui l'applicazione Node.js viene caricata in Azure. 

Quando viene caricata l'applicazione hello, controllare toomake assicurarsi che sia in esecuzione nell'ambiente di produzione hello:

```
--
MEAN.JS

Environment:     production
Server:          http://0.0.0.0:8443
Database:        mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true&sslverifycertificate=false
App version:     0.5.0
MEAN.JS version: 0.5.0
```

Passare toohttp://localhost:8443 in un browser. Fare clic su **iscrizione** in hello menu superiore e creare un utente test. Se si crea un utente ha esito positivo e l'accesso, l'app sta scrivendo database DB Cosmos toohello di dati in Azure. 

In hello terminal, arrestare Node.js digitando `Ctrl+C`. 

## <a name="deploy-app-tooazure"></a>Distribuire app tooAzure

In questo passaggio, si distribuisce il tooAzure applicazione connessa MongoDB Node.js servizio App.

### <a name="create-an-app-service-plan"></a>Creare un piano di servizio app

Creare un piano di servizio App con hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

esempio Hello crea un piano di servizio App denominato _myAppServicePlan_ utilizzando hello **libero** tariffario:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku FREE
```

Quando viene creato il piano di servizio App hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

```json 
{ 
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "North Europe",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "app",
  "location": "North Europe",
  "maximumNumberOfWorkers": 1,
  "name": "myAppServicePlan",
  ...
  < Output has been truncated for readability >
} 
```

### <a name="create-a-web-app"></a>Creare un'app Web

Creare un'app web in hello `myAppServicePlan` il piano di servizio App con hello [az webapp creare](/cli/azure/webapp#create) comando. 

Consente di app web Hello è un tipo di hosting spazio toodeploy il codice e fornisce un URL per l'utente tooview hello applicazione distribuita. Utilizzare toocreate hello web app. 

In hello seguente comando, sostituire hello  *\<nome_app >* segnaposto con un nome univoco dell'app. Questo nome viene utilizzato come parte di hello dell'URL predefinito hello per app web hello Nome hello deve toobe univoco tra tutte le App in Azure App Service. 

```azurecli-interactive
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

Quando hello web app è stata creata, hello Azure CLI indica toohello di informazioni simili esempio seguente: 

```json 
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "cloningInfo": null,
  "containerSize": 0,
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "<app_name>.azurewebsites.net",
  "enabled": true,
  ...
  < Output has been truncated for readability >
}
```

### <a name="configure-an-environment-variable"></a>Configurare una variabile di ambiente

Nelle sezioni precedenti di hello dell'esercitazione, è hardcoded hello stringa di connessione database in _config/env/production.js_. In conformità a livello di protezione ottimale, si desidera tookeep dati sensibili fuori il repository Git. Per l'app in esecuzione in Azure, si userà invece una variabile di ambiente.

Nel servizio App, impostare le variabili di ambiente come _impostazioni app_ utilizzando hello [az webapp configurazione appsettings aggiornare](/cli/azure/webapp/config/appsettings#update) comando. 

Hello seguente esempio mostra come configurare un `MONGODB_URI` impostazione dell'app nell'app web di Azure. Sostituire hello  *\<nome_app >*,  *\<cosmosdb_name >*, e  *\<primary_master_key >* segnaposto.

```azurecli-interactive
az webapp config appsettings update \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings MONGODB_URI="mongodb://<cosmosdb_name>:<primary_master_key>@<cosmosdb_name>.documents.azure.com:10250/mean?ssl=true"
```

Nel codice Node.js si accede all'impostazione dell'app con `process.env.MONGODB_URI`, esattamente come si accede a una variabile di ambiente qualsiasi. 

A questo punto, è possibile annullare too_config/env/production.js_ le modifiche con hello comando seguente:

```bash
git checkout -- .
```

Aprire di nuovo _config/env/production.js_. App MEAN.js predefinito hello è già configurato toouse hello `MONGODB_URI` variabile di ambiente che è stato creato.

```javascript
db: {
  uri: ... || process.env.MONGODB_URI || ...,
  ...
},
```

### <a name="configure-local-git-deployment"></a>Configurare la distribuzione con l'istanza Git locale 

Hello utilizzare [az webapp distribuzione utente set](/cli/azure/webapp/deployment/user#set) comando toocreate le credenziali per la distribuzione.

È possibile distribuire l'applicazione tooAzure servizio App, in vari modi, tra cui FTP, Git locale, GitHub, Visual Studio Team Services e BitBucket. Per FTP e Git locale, è necessario toohave un utente di distribuzione è configurata su hello server tooauthenticate la distribuzione. L'utente di distribuzione è a livello di account ed è diverso dall'account della sottoscrizione di Azure. È necessario solo tooconfigure questo utente di distribuzione una volta.

In hello seguente comando, sostituire  *\<nome utente >* e  *\<password >* con un nuovo nome utente e una password. nome utente Hello deve essere univoco. Hello password deve essere composta da almeno otto caratteri, con due simboli di hello seguenti tre elementi: lettere, numeri e simboli. Se viene visualizzato un ` 'Conflict'. Details: 409` errore, nome utente hello di modifica. Se viene visualizzato un errore ` 'Bad Request'. Details: 400`, usare una password più complessa.

```azurecli-interactive
az appservice web deployment user set --user-name <username> --password <password>
```

Nome del record hello utente e password da utilizzare nei passaggi successivi quando si distribuisce l'applicazione hello.

Hello utilizzare [az webapp distribuzione origine configurazione-locale-git](/cli/azure/webapp/deployment/source#config-local-git) comando tooconfigure locale Git accesso toohello app web di Azure. 

```azurecli-interactive
az webapp deployment source config-local-git --name <app_name> --resource-group myResourceGroup
```

Quando l'utente di distribuzione hello è configurato, hello CLI di Azure Mostra hello URL di distribuzione per l'app web di Azure in hello seguente formato:

```bash 
https://<username>@<app_name>.scm.azurewebsites.net:443/<app_name>.git 
``` 

Copiare hello output da terminal hello, perché verrà usato nel passaggio successivo hello. 

### <a name="push-tooazure-from-git"></a>Eseguire il push tooAzure da Git

Aggiungere un repository Git locale tooyour remoto di Azure. 

```bash
git remote add azure <paste_copied_url_here> 
```

Push toohello Azure toodeploy remoto dell'applicazione di Node.js. Verrà richiesto di password hello fornito in precedenza come parte della creazione di hello dell'utente di distribuzione hello. 

```bash
git push azure master
```

Durante la distribuzione, Servizio app di Azure comunica lo stato con Git.

```bash
Counting objects: 5, done.
Delta compression using up too4 threads.
Compressing objects: 100% (5/5), done.
Writing objects: 100% (5/5), 489 bytes | 0 bytes/s, done.
Total 5 (delta 3), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id '6c7c716eee'.
remote: Running custom deployment command...
remote: Running deployment command...
remote: Handling node.js deployment.
.
.
.
remote: Deployment successful.
toohttps://<app_name>.scm.azurewebsites.net/<app_name>.git
 * [new branch]      master -> master
``` 

È possibile notare che viene eseguito il processo di distribuzione hello [Gulp](http://gulpjs.com/) dopo `npm install`. Servizio App Gulp o Grunt attività non viene eseguito durante la distribuzione, pertanto questo repository di esempio ha due altri file nel relativo tooenable directory radice: 

- _.Deployment_ -toorun di servizio App di questo file indica `bash deploy.sh` come script di distribuzione personalizzata hello.
- _Deploy.sh_ -hello script di distribuzione personalizzati. Se si esamina il file hello, si noterà che l'esecuzione `gulp prod` dopo `npm install` e `bower install`. 

È possibile utilizzare questo approccio tooadd qualsiasi tooyour passaggio distribuzione basati su Git. Se si riavvia l'app Web di Azure in qualsiasi momento, il servizio app non esegue di nuovo queste attività di automazione.

### <a name="browse-toohello-azure-web-app"></a>Sfoglia toohello Azure web app 

Esplorare app web toohello distribuito tramite il browser. 

```bash 
http://<app_name>.azurewebsites.net 
``` 

Fare clic su **iscrizione** in hello menu superiore e creare un utente fittizio. 

Se hanno esito positivo e l'applicazione hello accede automaticamente database MongoDB (DB Cosmos) di connettività toohello toohello creazione utente, quindi l'app MEAN.js in Azure. 

![App MEAN.js in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/meanjs-in-azure.png)

Selezionare **amministrazione > Gestisci articoli** tooadd alcuni articoli. 

**Congratulazioni.** L'app Node.js basata su dati è in esecuzione nel Servizio app di Azure.

## <a name="update-data-model-and-redeploy"></a>Aggiornare il modello di dati e ridistribuire

In questo passaggio si modifica hello `article` modello di dati e pubblicare il tooAzure di modifica.

### <a name="update-hello-data-model"></a>Aggiornare il modello di dati hello

Aprire _modules/articles/server/models/article.server.model.js_.

In `ArticleSchema` aggiungere un tipo `String` denominato `comment`. Al termine, il codice dello schema dovrebbe avere un aspetto simile al seguente:

```javascript
var ArticleSchema = new Schema({
  ...,
  user: {
    type: Schema.ObjectId,
    ref: 'User'
  },
  comment: {
    type: String,
    default: '',
    trim: true
  }
});
```

### <a name="update-hello-articles-code"></a>Aggiornare il codice di articoli hello

Aggiornare il resto di hello del `articles` codice toouse `comment`.

Esistono cinque file, è necessario toomodify: controller server hello e visualizzazioni client hello quattro. 

Aprire _modules/articles/server/controllers/articles.server.controller.js_.

In hello `update` , aggiungere un'assegnazione di `article.comment`. Hello codice seguente viene illustrato hello completato `update` funzione:

```javascript
exports.update = function (req, res) {
  var article = req.article;

  article.title = req.body.title;
  article.content = req.body.content;
  article.comment = req.body.comment;

  ...
};
```

Aprire _modules/articles/client/views/view-article.client.view.html_.

Sopra la chiusura di hello `</section>` tag, aggiungere hello seguente riga toodisplay `comment` insieme resto hello di dati dell'articolo hello:

```HTML
<p class="lead" ng-bind="vm.article.comment"></p>
```

Aprire _modules/articles/client/views/list-articles.client.view.html_.

Sopra la chiusura di hello `</a>` tag, aggiungere hello seguente riga toodisplay `comment` insieme resto hello di dati dell'articolo hello:

```HTML
<p class="list-group-item-text" ng-bind="article.comment"></p>
```

Aprire _modules/articles/client/views/admin/list-articles.client.view.html_.

Inside hello `<div class="list-group">` elemento e sopra la chiusura di hello `</a>` tag, aggiungere hello seguente riga toodisplay `comment` insieme resto hello di dati dell'articolo hello:

```HTML
<p class="list-group-item-text" data-ng-bind="article.comment"></p>
```

Aprire _modules/articles/client/views/admin/form-article.client.view.html_.

Trovare hello `<div class="form-group">` elemento che contiene il pulsante di invio hello, che ha un aspetto simile:

```HTML
<div class="form-group">
  <button type="submit" class="btn btn-default">{{vm.article._id ? 'Update' : 'Create'}}</button>
</div>
```

Appena sopra il tag, aggiungere un altro `<div class="form-group">` elemento che consente agli utenti di modificare hello `comment` campo. Il nuovo elemento dovrebbe avere un aspetto simile al seguente:

```HTML
<div class="form-group">
  <label class="control-label" for="comment">Comment</label>
  <textarea name="comment" data-ng-model="vm.article.comment" id="comment" class="form-control" cols="30" rows="10" placeholder="Comment"></textarea>
</div>
```

### <a name="test-your-changes-locally"></a>Testare le modifiche in locale

Salvare tutte le modifiche.

Testare di nuovo le modifiche in modalità di produzione.

```bash
gulp prod
NODE_ENV=production node server.js
```

> [!NOTE]
> Tenere presente che il _config/env/production.js_ è stato ripristinato e hello `MONGODB_URI` variabile di ambiente viene impostata solo nell'app web di Azure e non nel computer locale. Se si esamina il file di configurazione di hello, si trova tale hello configurazione production per impostazione predefinita toouse un database locale di MongoDB. Ciò garantisce che non si modifichino i dati di produzione quando si testano modifiche al codice in locale.

Passare troppo`http://localhost:8443` in un browser e assicurarsi di avere effettuato.

Selezionare **amministrazione > Gestisci articoli**, quindi aggiungere un articolo selezionando hello  **+**  pulsante.

Hello vedere nuova `Comment` textbox ora.

![Commento aggiunto campo tooArticles](./media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field.png)

In hello terminal, arrestare Node.js digitando `Ctrl+C`. 

### <a name="publish-changes-tooazure"></a>Pubblicare le modifiche tooAzure

Eseguire il commit delle modifiche in Git, quindi eseguire il push tooAzure modifiche di codice hello.

```bash
git commit -am "added article comment"
git push azure master
```

Una volta hello `git push` è completata, passare tooyour Azure web app e provare la nuova funzionalità di hello.

![Le modifiche apportate al modello e il database pubblicato tooAzure](media/app-service-web-tutorial-nodejs-mongodb-app/added-comment-field-published.png)

Eventuali articoli aggiunti in precedenza sono ancora visibili. I dati esistenti in Cosmos DB non vengono persi. Inoltre, lo schema di dati toohello gli aggiornamenti e lascia intatti i dati esistenti.

## <a name="stream-diagnostic-logs"></a>Eseguire lo streaming dei log di diagnostica 

Durante l'esecuzione dell'applicazione di Node.js in Azure App Service, è possibile ottenere hello console registri reindirizzato tooyour terminal. In questo modo, è possibile ottenere hello stessi messaggi di diagnostica toohelp si esegue il debug di errori dell'applicazione.

log toostart streaming, usare hello [della parte finale del log di az webapp](/cli/azure/webapp/log#tail) comando.

```azurecli-interactive
az webapp log tail --name <app_name> --resource-group myResourceGroup
``` 

Una volta avviato il flusso di log, aggiornare l'app web di Azure in hello browser tooget traffico web. È ora possibile visualizzare i registri di console reindirizzato tooyour terminal.

Arrestare il flusso dei log in qualsiasi momento digitando `Ctrl+C`. 

## <a name="manage-your-azure-web-app"></a>Gestire l'app Web di Azure

Passare toohello [portale di Azure](https://portal.azure.com) toosee hello web app è stato creato.

Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.

![Spostamento del portale tooAzure web app](./media/app-service-web-tutorial-nodejs-mongodb-app/access-portal.png)

Per impostazione predefinita, il portale di hello Mostra dell'app web **Panoramica** pagina. che offre una visualizzazione dello stato dell'app. In questa pagina è anche possibile eseguire attività di gestione di base come esplorare, arrestare, avviare, riavviare ed eliminare. schede di Hello sul lato sinistro di hello della pagina hello mostrano è possibile aprire le pagine di configurazione diverso hello.

![Pagina del servizio app nel portale di Azure](./media/app-service-web-tutorial-nodejs-mongodb-app/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>
## <a name="next-steps"></a>Passaggi successivi

Contenuto dell'esercitazione:

> [!div class="checklist"]
> * Creare un database MongoDB in Azure
> * Connettersi a un tooMongoDB app Node.js
> * Distribuire hello app tooAzure
> * Modello di dati hello e ridistribuire l'applicazione hello
> * Registri di flusso di Azure tooyour terminal
> * Gestire app hello in hello portale di Azure

Spostare toolearn esercitazione successiva toohello come toomap un DNS personalizzato denominati tooyour web app.

> [!div class="nextstepaction"] 
> [Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web](app-service-web-tutorial-custom-domain.md)
