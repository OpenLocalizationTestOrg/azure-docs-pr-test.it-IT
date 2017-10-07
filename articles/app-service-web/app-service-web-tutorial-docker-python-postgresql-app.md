---
title: aaaBuild un'app web di Python di Docker e PostgreSQL in Azure | Documenti Microsoft
description: Informazioni su come un'app di Docker Python tooget Usa Azure, con connessione tooa PostgreSQL del database.
services: app-service\web
documentationcenter: python
author: berndverst
manager: erikre
editor: 
ms.assetid: 2bada123-ef18-44e5-be71-e16323b20466
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: python
ms.topic: tutorial
ms.date: 05/03/2017
ms.author: beverst
ms.custom: mvc
ms.openlocfilehash: e594ef9ec8c04ef2bf725e5f998691f3fb8cf815
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a>Compilare un'app Web Python Docker e PostgreSQL in Azure

Le app Web di Azure offrono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione. Questa esercitazione viene illustrato come una base di Docker Python toocreate web app in Azure. Verrà effettuata una connessione a questo database PostgreSQL tooa di app. Al termine, si avrà un'applicazione Python Flask in esecuzione in un contenitore Docker nelle [app Web del servizio app di Azure](app-service-web-overview.md).

![App Docker Python Flask nel Servizio app di Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

È possibile eseguire operazioni di hello seguenti su macOS. Le istruzioni di Linux e Windows sono uguali hello nella maggior parte dei casi, ma le differenze di hello non sono descritti in questa esercitazione.
 
## <a name="prerequisites"></a>Prerequisiti

toocomplete questa esercitazione:

1. [Installare Git](https://git-scm.com/)
1. [Installare Python](https://www.python.org/downloads/)
1. [Installare ed eseguire PostgreSQL](https://www.postgresql.org/download/)
1. [Installare Docker Community Edition](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva. Eseguire `az --version` versione hello toofind. Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="test-local-postgresql-installation-and-create-a-database"></a>Testare l'installazione di PostgreSQL locale e creare un database

Aprire una finestra terminale hello ed eseguire `psql postgres` tooconnect tooyour locale PostgreSQL server.

```bash
psql postgres
```

Se la connessione ha esito positivo, il database PostgreSQL è in esecuzione. In caso contrario, assicurarsi che sia stato avviato il database PostgresQL locale seguendo i passaggi di hello in [Scarica - PostgreSQL Core distribuzione](https://www.postgresql.org/download/).

Creare un database denominato *eventregistration* e configurare un utente di database separato denominato *manager* con password *supersecretpass*.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
Tipo *\q* client di tooexit hello PostgreSQL. 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a>Creare l'applicazione locale Python Flask

In questo passaggio, impostare il progetto di Python pallone locale hello.

### <a name="clone-hello-sample-application"></a>Applicazione di esempio hello clonare

Finestra terminal aprire hello e `CD` tooa directory di lavoro.  

Seguente hello esecuzione comandi tooclone hello esempio repository e passare toohello *0,1 initialapp* versione.

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

Questo repository di esempio contiene un'applicazione [Flask](http://flask.pocoo.org/). 

### <a name="run-hello-application"></a>Eseguire un'applicazione hello

> [!NOTE] 
> In un passaggio successivo è semplificare questo processo generando un toouse contenitore Docker con il database di produzione hello.

Installare i pacchetti hello necessarie e avviare un'applicazione hello.

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Quando l'applicazione hello è stato caricato completamente, viene visualizzato un codice simile toohello seguente messaggio:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Passare toohttp://127.0.0.1:5000 in un browser. Fare clic su **Registra!** e creare un utente test.

![Applicazione Python Flask in esecuzione in locale](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

applicazione di esempio pallone Hello archivia i dati utente nel database di hello. Se hanno esito positivo alla registrazione di un utente, l'app sta scrivendo database PostgreSQL locale di dati toohello.

server di pallone toostop hello in qualsiasi momento, premere Ctrl + C in hello terminal. 

## <a name="create-a-production-postgresql-database"></a>Creare un database di produzione PostgreSQL

In questo passaggio si crea un database PostgreSQL in Azure. Quando l'applicazione viene distribuita tooAzure, userà questo database cloud.

### <a name="log-in-tooazure"></a>Accedi tooAzure

Si sta risorse hello di corso toouse hello Azure CLI 2.0 toocreate necessari toohost applicazione Python in Azure App Service.  Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni. 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a>Creare un gruppo di risorse

Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) con hello [gruppo az creare](/cli/azure/group#create). 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

Hello esempio seguente viene creato un gruppo di risorse nell'area Stati Uniti occidentali hello:

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

Hello utilizzare [az appservice elenco posizioni](/cli/azure/appservice#list-locations) posizioni disponibili toolist di comando CLI di Azure.

### <a name="create-an-azure-database-for-postgresql-server"></a>Creare un database di Azure per il server PostgreSQL

Creare un server PostgreSQL con hello [az postgres server creare](/cli/azure/documentdb#create) comando.

In hello seguente comando, sostituire con un nome univoco per hello  *\<postgresql_name >* segnaposto e un nome utente per hello  *\<admin_username >* segnaposto . nome del server Hello viene utilizzato come parte dell'endpoint PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), in modo che nome hello deve toobe univoco in tutti i server in Azure. nome utente Hello è per l'account amministratore di database iniziale hello. Si è toopick richiesta una password per questo utente.

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

Quando viene creato hello Azure Database per server PostgreSQL, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

```json
{
  "administratorLogin": "<my_admin_username>",
  "fullyQualifiedDomainName": "<postgresql_name>.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>",
  "location": "westus",
  "name": "<postgresql_name>",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capacity": 100,
    "family": null,
    "name": "PGSQLS3M100",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a>Creare una regola del firewall per hello Azure Database per server PostgreSQL

Eseguire hello seguenti database di toohello access tooallow comando CLI di Azure da tutti gli indirizzi IP.

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

Hello Azure CLI conferma la creazione di regole firewall hello con toohello simili di output esempio seguente:

```json
{
  "endIpAddress": "255.255.255.255",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforPostgreSQL/servers/<postgresql_name>/firewallRules/AllowAllIPs",
  "name": "AllowAllIPs",
  "resourceGroup": "myResourceGroup",
  "startIpAddress": "0.0.0.0",
  "type": "Microsoft.DBforPostgreSQL/servers/firewallRules"
}
```

## <a name="connect-your-python-flask-application-toohello-database"></a>Connettere il database di toohello Python pallone dell'applicazione

In questo passaggio è connettersi il toohello di applicazione di esempio Database Azure pallone Python per PostgreSQL server che è stato creato.

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a>Creare un database vuoto e impostare un nuovo utente dell'applicazione del database

Creare un utente del database con tooa singolo solo database di access. Si utilizzeranno questi tooavoid credenziali consegnare hello applicazione l'accesso completo toohello server.

La connessione a database toohello (richiesta la password di amministratore).

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

Il nome di utente e il database hello hello PostgreSQL CLI.

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

Tipo *\q* client di tooexit hello PostgreSQL.

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a>Testare un'applicazione hello localmente sul database di Azure PostgreSQL hello 

Se si torna indietro ora toohello *app* cartella di hello clonazione il repository di Github, è possibile eseguire un'applicazione hello Python pallone aggiornando le variabili di ambiente database hello.

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Quando l'applicazione hello è stato caricato completamente, viene visualizzato un codice simile toohello seguente messaggio:

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

Passare toohttp://127.0.0.1:5000 in un browser. Fare clic su **Registra!** e creare una registrazione test. Ora si scrive database toohello dati in Azure.

![Applicazione Python Flask in esecuzione in locale](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a>Esecuzione di un'applicazione hello da un contenitore Docker

Immagine del contenitore Docker hello di compilazione.

```bash
cd ..
docker build -t flask-postgresql-sample .
```

Docker consente di visualizzare un messaggio di conferma che il contenitore hello it creato correttamente.

```bash
Successfully built 7548f983a36b
```

Aggiungere database ambiente variabili tooan ambiente variabile file *db.env*. app Hello si connetterà toohello PostgreSQL database di produzione in Azure.

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

Esecuzione dell'applicazione hello all'interno del contenitore Docker hello. Hello comando che segue specifica file variabili di ambiente hello e mappe hello predefinito pallone porta 5000 toolocal port 5000.

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

output di Hello è simile toowhat illustrato in precedenza. Tuttavia, migrazione del database iniziale hello non è più necessario toobe eseguita e pertanto viene ignorata.

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

database di Hello contiene già registrazione hello creato in precedenza.

![Applicazione Python Flask basata sul contenitore Docker in esecuzione in locale](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a>Caricamento del Registro di sistema di hello Docker contenitore tooa contenitore

In questo passaggio è caricare del Registro di sistema di hello Docker contenitore tooa contenitore. Verrà usato il registro contenitori di Azure. È possibile tuttavia usare anche altri registri comuni, ad esempio l'hub Docker.

### <a name="create-an-azure-container-registry"></a>Creare un Registro contenitori di Azure

Nel seguente comando toocreate del Registro di sistema un contenitore hello sostituire  *\<registry_name >* con un nome di contenitore di Azure univoco del Registro di sistema di propria scelta.

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

Output
```json
{
  "adminUserEnabled": false,
  "creationDate": "2017-05-04T08:50:55.635688+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/<registry_name>",
  "location": "westus",
  "loginServer": "<registry_name>.azurecr.io",
  "name": "<registry_name>",
  "provisioningState": "Succeeded",
  "sku": {
    "name": "Basic",
    "tier": "Basic"
  },
  "storageAccount": {
    "name": "<registry_name>01234"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a>Recuperare le credenziali del Registro di sistema di hello per push e pull immagini Docker

le credenziali del Registro di sistema tooshow, abilitare prima la modalità di amministrazione.

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

Vengono visualizzate due password. Prendere nota del nome utente hello e una password prima di hello.

```json
{
  "passwords": [
    {
      "name": "password",
      "value": "<registry_password>"
    },
    {
      "name": "password2",
      "value": "<registry_password2>"
    }
  ],
  "username": "<registry_name>"
}
```

### <a name="upload-your-docker-container-tooazure-container-registry"></a>Caricare il tooAzure contenitore Docker contenitore del Registro di sistema

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a>Distribuire hello Docker Python pallone applicazione tooAzure

In questo passaggio, si distribuisce il tooAzure legata applicazione Python pallone nella basate sul contenitore Docker servizio App.

### <a name="create-an-app-service-plan"></a>Creare un piano di servizio app

Creare un piano di servizio App con hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando. 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

esempio Hello crea un piano di servizio App basata su Linux denominato *myAppServicePlan* hello S1 tariffario utilizzando:

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

Quando viene creato il piano di servizio App hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:

```json 
{
  "adminSiteName": null,
  "appServicePlanName": "myAppServicePlan",
  "geoRegion": "West US",
  "hostingEnvironmentProfile": null,
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Web/serverfarms/myAppServicePlan", 
  "kind": "linux",
  "location": "West US",
  "maximumNumberOfWorkers": 10,
  "name": "myAppServicePlan",
  "numberOfSites": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": true,
  "resourceGroup": "myResourceGroup",
  "sku": {
    "capabilities": null,
    "capacity": 1,
    "family": "S",
    "locations": null,
    "name": "S1",
    "size": "S1",
    "skuCapacity": null,
    "tier": "Standard"
  },
  "status": "Ready",
  "subscription": "00000000-0000-0000-0000-000000000000",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null
}
``` 

### <a name="create-a-web-app"></a>Creare un'app Web

Creare un'app web in hello *myAppServicePlan* il piano di servizio App con hello [az webapp creare](/cli/azure/webapp#create) comando. 

Consente di app web Hello è un tipo di hosting spazio toodeploy il codice e fornisce un URL per l'utente tooview hello applicazione distribuita. Utilizzare toocreate hello web app. 

In hello seguente comando, sostituire hello  *\<nome_app >* segnaposto con un nome univoco dell'app. Questo nome fa parte dell'URL di hello predefinito per l'app web hello, in modo nome hello deve toobe univoco tra tutte le App in Azure App Service. 

```azurecli
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

### <a name="configure-hello-database-environment-variables"></a>Configurare le variabili di ambiente database hello

In precedenza nell'esercitazione hello è definito database PostgreSQL di ambiente variabili tooconnect tooyour.

Nel servizio App, impostare le variabili di ambiente come _impostazioni app_ utilizzando hello [az webapp configurazione appsettings set](/cli/azure/webapp/config#set) comando. 

Hello esempio seguente specifica i dettagli della connessione database hello come impostazioni dell'app. Utilizza inoltre hello *porta* variabile toomap PORT 5000 dal traffico contenitore Docker tooreceive HTTP sulla porta 80.

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a>Configurare la distribuzione del contenitore Docker 

AppService può automaticamente di scaricare ed eseguire un contenitore Docker.

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

Quando si aggiorna contenitore Docker hello o modificare le impostazioni di hello, riavviare l'applicazione hello. Il riavvio garantisce che tutte le impostazioni vengono applicate e contenitore più recente di hello viene effettuato il pull dal Registro di sistema hello.

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a>Sfoglia toohello Azure web app 

Esplorare app web toohello distribuito tramite il browser. 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> app web Hello accetta più tooload poiché hello contenitore dispone di toobe scaricato e avviato dopo la modifica di configurazione del contenitore hello.

Viene visualizzato agli utenti guest registrato in precedenza che sono stati salvati i database di produzione di Azure toohello nel passaggio precedente hello.

![Applicazione Python Flask basata sul contenitore Docker in esecuzione in locale](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

**Congratulazioni.** L'app Python Flask basata sul contenitore Docker è in esecuzione nel Servizio app di Azure.

## <a name="update-data-model-and-redeploy"></a>Aggiornare il modello di dati e ridistribuire

In questo passaggio si aggiunge il numero di hello di registrazione eventi di partecipanti tooeach aggiornando hello Guest modello.

Estrarre hello *0,2 migrazione* versione con hello git comando seguente:

```bash
git checkout tags/0.2-migration
```

Questa versione è già eseguite hello tooviews le modifiche necessarie, controller e modello. Include anche una migrazione del database generata tramite *alembic* (`flask db migrate`). È possibile visualizzare tutte le modifiche apportate tramite hello git comando seguente:

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a>Testare le modifiche in locale

Eseguire hello seguenti comandi tootest le modifiche localmente dal server di pallone hello in esecuzione.

Mac/Linux:
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

Passare toohttp://127.0.0.1:5000 le modifiche di hello tooview browser. Creare una registrazione test.

![Applicazione Python Flask basata sul contenitore Docker in esecuzione in locale](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a>Pubblicare le modifiche tooAzure

Creare una nuova immagine di docker hello, spingerla del Registro di sistema di toohello contenitore e riavviare l'applicazione hello.

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

Passare tooyour Azure web app e provare nuovamente la nuova funzionalità hello. Creare un'altra registrazione dell'evento.

```bash 
http://<app_name>.azurewebsites.net 
```

![App Docker Python Flask nel Servizio app di Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a>Gestire l'app Web di Azure

Passare toohello [portale di Azure](https://portal.azure.com) toosee hello web app è stato creato.

Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.

![Spostamento del portale tooAzure web app](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

Per impostazione predefinita, il portale di hello Mostra dell'app web **Panoramica** pagina. che offre una visualizzazione dello stato dell'app. In questa pagina è anche possibile eseguire attività di gestione di base come esplorare, arrestare, avviare, riavviare ed eliminare. schede di Hello sul lato sinistro di hello della pagina hello mostrano è possibile aprire le pagine di configurazione diverso hello.

![Pagina del servizio app nel portale di Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a>Passaggi successivi

Spostare toolearn esercitazione successiva toohello come toomap un DNS personalizzato denominati tooyour web app.

> [!div class="nextstepaction"] 
> [Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web](app-service-web-tutorial-custom-domain.md)
