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
# <a name="build-a-docker-python-and-postgresql-web-app-in-azure"></a><span data-ttu-id="c4714-103">Compilare un'app Web Python Docker e PostgreSQL in Azure</span><span class="sxs-lookup"><span data-stu-id="c4714-103">Build a Docker Python and PostgreSQL web app in Azure</span></span>

<span data-ttu-id="c4714-104">Le app Web di Azure offrono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="c4714-104">Azure Web Apps provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="c4714-105">Questa esercitazione viene illustrato come una base di Docker Python toocreate web app in Azure.</span><span class="sxs-lookup"><span data-stu-id="c4714-105">This tutorial shows how toocreate a basic Docker Python web app in Azure.</span></span> <span data-ttu-id="c4714-106">Verrà effettuata una connessione a questo database PostgreSQL tooa di app.</span><span class="sxs-lookup"><span data-stu-id="c4714-106">You'll connect this app tooa PostgreSQL database.</span></span> <span data-ttu-id="c4714-107">Al termine, si avrà un'applicazione Python Flask in esecuzione in un contenitore Docker nelle [app Web del servizio app di Azure](app-service-web-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c4714-107">When you're done, you'll have a Python Flask application running within a Docker container on [Azure App Service Web Apps](app-service-web-overview.md).</span></span>

![App Docker Python Flask nel Servizio app di Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

<span data-ttu-id="c4714-109">È possibile eseguire operazioni di hello seguenti su macOS.</span><span class="sxs-lookup"><span data-stu-id="c4714-109">You can follow hello steps below on macOS.</span></span> <span data-ttu-id="c4714-110">Le istruzioni di Linux e Windows sono uguali hello nella maggior parte dei casi, ma le differenze di hello non sono descritti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="c4714-110">Linux and Windows instructions are hello same in most cases, but hello differences are not detailed in this tutorial.</span></span>
 
## <a name="prerequisites"></a><span data-ttu-id="c4714-111">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c4714-111">Prerequisites</span></span>

<span data-ttu-id="c4714-112">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="c4714-112">toocomplete this tutorial:</span></span>

1. [<span data-ttu-id="c4714-113">Installare Git</span><span class="sxs-lookup"><span data-stu-id="c4714-113">Install Git</span></span>](https://git-scm.com/)
1. [<span data-ttu-id="c4714-114">Installare Python</span><span class="sxs-lookup"><span data-stu-id="c4714-114">Install Python</span></span>](https://www.python.org/downloads/)
1. [<span data-ttu-id="c4714-115">Installare ed eseguire PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="c4714-115">Install and run PostgreSQL</span></span>](https://www.postgresql.org/download/)
1. [<span data-ttu-id="c4714-116">Installare Docker Community Edition</span><span class="sxs-lookup"><span data-stu-id="c4714-116">Install Docker Community Edition</span></span>](https://www.docker.com/community-edition)

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="c4714-117">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="c4714-117">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="c4714-118">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="c4714-118">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="c4714-119">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="c4714-119">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="test-local-postgresql-installation-and-create-a-database"></a><span data-ttu-id="c4714-120">Testare l'installazione di PostgreSQL locale e creare un database</span><span class="sxs-lookup"><span data-stu-id="c4714-120">Test local PostgreSQL installation and create a database</span></span>

<span data-ttu-id="c4714-121">Aprire una finestra terminale hello ed eseguire `psql postgres` tooconnect tooyour locale PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="c4714-121">Open hello terminal window and run `psql postgres` tooconnect tooyour local PostgreSQL server.</span></span>

```bash
psql postgres
```

<span data-ttu-id="c4714-122">Se la connessione ha esito positivo, il database PostgreSQL è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c4714-122">If your connection is successful, your PostgreSQL database is running.</span></span> <span data-ttu-id="c4714-123">In caso contrario, assicurarsi che sia stato avviato il database PostgresQL locale seguendo i passaggi di hello in [Scarica - PostgreSQL Core distribuzione](https://www.postgresql.org/download/).</span><span class="sxs-lookup"><span data-stu-id="c4714-123">If not, make sure that your local PostgresQL database is started by following hello steps at [Downloads - PostgreSQL Core Distribution](https://www.postgresql.org/download/).</span></span>

<span data-ttu-id="c4714-124">Creare un database denominato *eventregistration* e configurare un utente di database separato denominato *manager* con password *supersecretpass*.</span><span class="sxs-lookup"><span data-stu-id="c4714-124">Create a database called *eventregistration* and set up a separate database user named *manager* with password *supersecretpass*.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```
<span data-ttu-id="c4714-125">Tipo *\q* client di tooexit hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4714-125">Type *\q* tooexit hello PostgreSQL client.</span></span> 

<a name="step2"></a>

## <a name="create-local-python-flask-application"></a><span data-ttu-id="c4714-126">Creare l'applicazione locale Python Flask</span><span class="sxs-lookup"><span data-stu-id="c4714-126">Create local Python Flask application</span></span>

<span data-ttu-id="c4714-127">In questo passaggio, impostare il progetto di Python pallone locale hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-127">In this step, you set up hello local Python Flask project.</span></span>

### <a name="clone-hello-sample-application"></a><span data-ttu-id="c4714-128">Applicazione di esempio hello clonare</span><span class="sxs-lookup"><span data-stu-id="c4714-128">Clone hello sample application</span></span>

<span data-ttu-id="c4714-129">Finestra terminal aprire hello e `CD` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="c4714-129">Open hello terminal window, and `CD` tooa working directory.</span></span>  

<span data-ttu-id="c4714-130">Seguente hello esecuzione comandi tooclone hello esempio repository e passare toohello *0,1 initialapp* versione.</span><span class="sxs-lookup"><span data-stu-id="c4714-130">Run hello following commands tooclone hello sample repository and go toohello *0.1-initialapp* release.</span></span>

```bash
git clone https://github.com/Azure-Samples/docker-flask-postgres.git
cd docker-flask-postgres
git checkout tags/0.1-initialapp
```

<span data-ttu-id="c4714-131">Questo repository di esempio contiene un'applicazione [Flask](http://flask.pocoo.org/).</span><span class="sxs-lookup"><span data-stu-id="c4714-131">This sample repository contains a [Flask](http://flask.pocoo.org/) application.</span></span> 

### <a name="run-hello-application"></a><span data-ttu-id="c4714-132">Eseguire un'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="c4714-132">Run hello application</span></span>

> [!NOTE] 
> <span data-ttu-id="c4714-133">In un passaggio successivo è semplificare questo processo generando un toouse contenitore Docker con il database di produzione hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-133">In a later step you simplify this process by building a Docker container toouse with hello production database.</span></span>

<span data-ttu-id="c4714-134">Installare i pacchetti hello necessarie e avviare un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-134">Install hello required packages and start hello application.</span></span>

```bash
pip install virtualenv
virtualenv venv
source venv/bin/activate
pip install -r requirements.txt
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="c4714-135">Quando l'applicazione hello è stato caricato completamente, viene visualizzato un codice simile toohello seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="c4714-135">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="c4714-136">Passare toohttp://127.0.0.1:5000 in un browser.</span><span class="sxs-lookup"><span data-stu-id="c4714-136">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="c4714-137">Fare clic su **Registra!**</span><span class="sxs-lookup"><span data-stu-id="c4714-137">Click **Register!**</span></span> <span data-ttu-id="c4714-138">e creare un utente test.</span><span class="sxs-lookup"><span data-stu-id="c4714-138">and create a test user.</span></span>

![Applicazione Python Flask in esecuzione in locale](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

<span data-ttu-id="c4714-140">applicazione di esempio pallone Hello archivia i dati utente nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-140">hello Flask sample application stores user data in hello database.</span></span> <span data-ttu-id="c4714-141">Se hanno esito positivo alla registrazione di un utente, l'app sta scrivendo database PostgreSQL locale di dati toohello.</span><span class="sxs-lookup"><span data-stu-id="c4714-141">If you are successful at registering a user, your app is writing data toohello local PostgreSQL database.</span></span>

<span data-ttu-id="c4714-142">server di pallone toostop hello in qualsiasi momento, premere Ctrl + C in hello terminal.</span><span class="sxs-lookup"><span data-stu-id="c4714-142">toostop hello Flask server at anytime, type Ctrl+C in hello terminal.</span></span> 

## <a name="create-a-production-postgresql-database"></a><span data-ttu-id="c4714-143">Creare un database di produzione PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="c4714-143">Create a production PostgreSQL database</span></span>

<span data-ttu-id="c4714-144">In questo passaggio si crea un database PostgreSQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="c4714-144">In this step, you create a PostgreSQL database in Azure.</span></span> <span data-ttu-id="c4714-145">Quando l'applicazione viene distribuita tooAzure, userà questo database cloud.</span><span class="sxs-lookup"><span data-stu-id="c4714-145">When your app is deployed tooAzure, it will use this cloud database.</span></span>

### <a name="log-in-tooazure"></a><span data-ttu-id="c4714-146">Accedi tooAzure</span><span class="sxs-lookup"><span data-stu-id="c4714-146">Log in tooAzure</span></span>

<span data-ttu-id="c4714-147">Si sta risorse hello di corso toouse hello Azure CLI 2.0 toocreate necessari toohost applicazione Python in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c4714-147">You are now going toouse hello Azure CLI 2.0 toocreate hello resources needed toohost your Python application in Azure App Service.</span></span>  <span data-ttu-id="c4714-148">Accedere alla sottoscrizione di Azure con hello tooyour [accesso az](/cli/azure/#login) comando e seguire hello le direzioni.</span><span class="sxs-lookup"><span data-stu-id="c4714-148">Log in tooyour Azure subscription with hello [az login](/cli/azure/#login) command and follow hello on-screen directions.</span></span> 

```azurecli
az login 
``` 
   
### <a name="create-a-resource-group"></a><span data-ttu-id="c4714-149">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="c4714-149">Create a resource group</span></span>

<span data-ttu-id="c4714-150">Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) con hello [gruppo az creare](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="c4714-150">Create a [resource group](../azure-resource-manager/resource-group-overview.md) with hello [az group create](/cli/azure/group#create).</span></span> 

[!INCLUDE [Resource group intro](../../includes/resource-group.md)]

<span data-ttu-id="c4714-151">Hello esempio seguente viene creato un gruppo di risorse nell'area Stati Uniti occidentali hello:</span><span class="sxs-lookup"><span data-stu-id="c4714-151">hello following example creates a resource group in hello West US region:</span></span>

```azurecli-interactive
az group create --name myResourceGroup --location "West US"
```

<span data-ttu-id="c4714-152">Hello utilizzare [az appservice elenco posizioni](/cli/azure/appservice#list-locations) posizioni disponibili toolist di comando CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4714-152">Use hello [az appservice list-locations](/cli/azure/appservice#list-locations) Azure CLI command toolist available locations.</span></span>

### <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="c4714-153">Creare un database di Azure per il server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="c4714-153">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="c4714-154">Creare un server PostgreSQL con hello [az postgres server creare](/cli/azure/documentdb#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c4714-154">Create a PostgreSQL server with hello [az postgres server create](/cli/azure/documentdb#create) command.</span></span>

<span data-ttu-id="c4714-155">In hello seguente comando, sostituire con un nome univoco per hello  *\<postgresql_name >* segnaposto e un nome utente per hello  *\<admin_username >* segnaposto .</span><span class="sxs-lookup"><span data-stu-id="c4714-155">In hello following command, substitute a unique server name for hello *\<postgresql_name>* placeholder and a user name for hello *\<admin_username>* placeholder.</span></span> <span data-ttu-id="c4714-156">nome del server Hello viene utilizzato come parte dell'endpoint PostgreSQL (`https://<postgresql_name>.postgres.database.azure.com`), in modo che nome hello deve toobe univoco in tutti i server in Azure.</span><span class="sxs-lookup"><span data-stu-id="c4714-156">hello server name is used as part of your PostgreSQL endpoint (`https://<postgresql_name>.postgres.database.azure.com`), so hello name needs toobe unique across all servers in Azure.</span></span> <span data-ttu-id="c4714-157">nome utente Hello è per l'account amministratore di database iniziale hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-157">hello user name is for hello initial database admin user account.</span></span> <span data-ttu-id="c4714-158">Si è toopick richiesta una password per questo utente.</span><span class="sxs-lookup"><span data-stu-id="c4714-158">You are prompted toopick a password for this user.</span></span>

```azurecli-interactive
az postgres server create --resource-group myResourceGroup --name <postgresql_name> --admin-user <admin_username>
```

<span data-ttu-id="c4714-159">Quando viene creato hello Azure Database per server PostgreSQL, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c4714-159">When hello Azure Database for PostgreSQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-firewall-rule-for-hello-azure-database-for-postgresql-server"></a><span data-ttu-id="c4714-160">Creare una regola del firewall per hello Azure Database per server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="c4714-160">Create a firewall rule for hello Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="c4714-161">Eseguire hello seguenti database di toohello access tooallow comando CLI di Azure da tutti gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="c4714-161">Run hello following Azure CLI command tooallow access toohello database from all IP addresses.</span></span>

```azurecli-interactive
az postgres server firewall-rule create --resource-group myResourceGroup --server-name <postgresql_name> --start-ip-address=0.0.0.0 --end-ip-address=255.255.255.255 --name AllowAllIPs
```

<span data-ttu-id="c4714-162">Hello Azure CLI conferma la creazione di regole firewall hello con toohello simili di output esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c4714-162">hello Azure CLI confirms hello firewall rule creation with output similar toohello following example:</span></span>

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

## <a name="connect-your-python-flask-application-toohello-database"></a><span data-ttu-id="c4714-163">Connettere il database di toohello Python pallone dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="c4714-163">Connect your Python Flask application toohello database</span></span>

<span data-ttu-id="c4714-164">In questo passaggio è connettersi il toohello di applicazione di esempio Database Azure pallone Python per PostgreSQL server che è stato creato.</span><span class="sxs-lookup"><span data-stu-id="c4714-164">In this step, you connect your Python Flask sample application toohello Azure Database for PostgreSQL server you created.</span></span>

### <a name="create-an-empty-database-and-set-up-a-new-database-application-user"></a><span data-ttu-id="c4714-165">Creare un database vuoto e impostare un nuovo utente dell'applicazione del database</span><span class="sxs-lookup"><span data-stu-id="c4714-165">Create an empty database and set up a new database application user</span></span>

<span data-ttu-id="c4714-166">Creare un utente del database con tooa singolo solo database di access.</span><span class="sxs-lookup"><span data-stu-id="c4714-166">Create a database user with access tooa single database only.</span></span> <span data-ttu-id="c4714-167">Si utilizzeranno questi tooavoid credenziali consegnare hello applicazione l'accesso completo toohello server.</span><span class="sxs-lookup"><span data-stu-id="c4714-167">You'll use these credentials tooavoid giving hello application full access toohello server.</span></span>

<span data-ttu-id="c4714-168">La connessione a database toohello (richiesta la password di amministratore).</span><span class="sxs-lookup"><span data-stu-id="c4714-168">Connect toohello database (you're prompted for your admin password).</span></span>

```bash
psql -h <postgresql_name>.postgres.database.azure.com -U <my_admin_username>@<postgresql_name> postgres
```

<span data-ttu-id="c4714-169">Il nome di utente e il database hello hello PostgreSQL CLI.</span><span class="sxs-lookup"><span data-stu-id="c4714-169">Create hello database and user from hello PostgreSQL CLI.</span></span>

```bash
CREATE DATABASE eventregistration;
CREATE USER manager WITH PASSWORD 'supersecretpass';
GRANT ALL PRIVILEGES ON DATABASE eventregistration toomanager;
```

<span data-ttu-id="c4714-170">Tipo *\q* client di tooexit hello PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="c4714-170">Type *\q* tooexit hello PostgreSQL client.</span></span>

### <a name="test-hello-application-locally-against-hello-azure-postgresql-database"></a><span data-ttu-id="c4714-171">Testare un'applicazione hello localmente sul database di Azure PostgreSQL hello</span><span class="sxs-lookup"><span data-stu-id="c4714-171">Test hello application locally against hello Azure PostgreSQL database</span></span> 

<span data-ttu-id="c4714-172">Se si torna indietro ora toohello *app* cartella di hello clonazione il repository di Github, è possibile eseguire un'applicazione hello Python pallone aggiornando le variabili di ambiente database hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-172">Going back now toohello *app* folder of hello cloned Github repository, you can run hello Python Flask application by updating hello database environment variables.</span></span>

```bash
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="c4714-173">Quando l'applicazione hello è stato caricato completamente, viene visualizzato un codice simile toohello seguente messaggio:</span><span class="sxs-lookup"><span data-stu-id="c4714-173">When hello app is fully loaded, you see something similar toohello following message:</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
INFO  [alembic.runtime.migration] Running upgrade  -> 791cd7d80402, empty message
 * Serving Flask app "app"
 * Running on http://127.0.0.1:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="c4714-174">Passare toohttp://127.0.0.1:5000 in un browser.</span><span class="sxs-lookup"><span data-stu-id="c4714-174">Navigate toohttp://127.0.0.1:5000 in a browser.</span></span> <span data-ttu-id="c4714-175">Fare clic su **Registra!**</span><span class="sxs-lookup"><span data-stu-id="c4714-175">Click **Register!**</span></span> <span data-ttu-id="c4714-176">e creare una registrazione test.</span><span class="sxs-lookup"><span data-stu-id="c4714-176">and create a test registration.</span></span> <span data-ttu-id="c4714-177">Ora si scrive database toohello dati in Azure.</span><span class="sxs-lookup"><span data-stu-id="c4714-177">You are now writing data toohello database in Azure.</span></span>

![Applicazione Python Flask in esecuzione in locale](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app.png)

### <a name="running-hello-application-from-a-docker-container"></a><span data-ttu-id="c4714-179">Esecuzione di un'applicazione hello da un contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="c4714-179">Running hello application from a Docker Container</span></span>

<span data-ttu-id="c4714-180">Immagine del contenitore Docker hello di compilazione.</span><span class="sxs-lookup"><span data-stu-id="c4714-180">Build hello Docker container image.</span></span>

```bash
cd ..
docker build -t flask-postgresql-sample .
```

<span data-ttu-id="c4714-181">Docker consente di visualizzare un messaggio di conferma che il contenitore hello it creato correttamente.</span><span class="sxs-lookup"><span data-stu-id="c4714-181">Docker displays a confirmation that it successfully created hello container.</span></span>

```bash
Successfully built 7548f983a36b
```

<span data-ttu-id="c4714-182">Aggiungere database ambiente variabili tooan ambiente variabile file *db.env*.</span><span class="sxs-lookup"><span data-stu-id="c4714-182">Add database environment variables tooan environment variable file *db.env*.</span></span> <span data-ttu-id="c4714-183">app Hello si connetterà toohello PostgreSQL database di produzione in Azure.</span><span class="sxs-lookup"><span data-stu-id="c4714-183">hello app will connect toohello PostgreSQL production database in Azure.</span></span>

```text
DBHOST="<postgresql_name>.postgres.database.azure.com"
DBUSER="manager@<postgresql_name>"
DBNAME="eventregistration"
DBPASS="supersecretpass"
```

<span data-ttu-id="c4714-184">Esecuzione dell'applicazione hello all'interno del contenitore Docker hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-184">Run hello app from within hello Docker container.</span></span> <span data-ttu-id="c4714-185">Hello comando che segue specifica file variabili di ambiente hello e mappe hello predefinito pallone porta 5000 toolocal port 5000.</span><span class="sxs-lookup"><span data-stu-id="c4714-185">hello following command specifies hello environment variable file and maps hello default Flask port 5000 toolocal port 5000.</span></span>

```bash
docker run -it --env-file db.env -p 5000:5000 flask-postgresql-sample
```

<span data-ttu-id="c4714-186">output di Hello è simile toowhat illustrato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c4714-186">hello output is similar toowhat you saw earlier.</span></span> <span data-ttu-id="c4714-187">Tuttavia, migrazione del database iniziale hello non è più necessario toobe eseguita e pertanto viene ignorata.</span><span class="sxs-lookup"><span data-stu-id="c4714-187">However, hello initial database migration no longer needs toobe performed and therefore is skipped.</span></span>

```bash
INFO  [alembic.runtime.migration] Context impl PostgresqlImpl.
INFO  [alembic.runtime.migration] Will assume transactional DDL.
 * Serving Flask app "app"
 * Running on http://0.0.0.0:5000/ (Press CTRL+C tooquit)
```

<span data-ttu-id="c4714-188">database di Hello contiene già registrazione hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="c4714-188">hello database already contains hello registration you created previously.</span></span>

![Applicazione Python Flask basata sul contenitore Docker in esecuzione in locale](./media/app-service-web-tutorial-docker-python-postgresql-app/local-docker.png)

## <a name="upload-hello-docker-container-tooa-container-registry"></a><span data-ttu-id="c4714-190">Caricamento del Registro di sistema di hello Docker contenitore tooa contenitore</span><span class="sxs-lookup"><span data-stu-id="c4714-190">Upload hello Docker container tooa container registry</span></span>

<span data-ttu-id="c4714-191">In questo passaggio è caricare del Registro di sistema di hello Docker contenitore tooa contenitore.</span><span class="sxs-lookup"><span data-stu-id="c4714-191">In this step, you upload hello Docker container tooa container registry.</span></span> <span data-ttu-id="c4714-192">Verrà usato il registro contenitori di Azure. È possibile tuttavia usare anche altri registri comuni, ad esempio l'hub Docker.</span><span class="sxs-lookup"><span data-stu-id="c4714-192">You'll use Azure Container Registry, but you could also use other popular ones such as Docker Hub.</span></span>

### <a name="create-an-azure-container-registry"></a><span data-ttu-id="c4714-193">Creare un Registro contenitori di Azure</span><span class="sxs-lookup"><span data-stu-id="c4714-193">Create an Azure Container Registry</span></span>

<span data-ttu-id="c4714-194">Nel seguente comando toocreate del Registro di sistema un contenitore hello sostituire  *\<registry_name >* con un nome di contenitore di Azure univoco del Registro di sistema di propria scelta.</span><span class="sxs-lookup"><span data-stu-id="c4714-194">In hello following command toocreate a container registry replace *\<registry_name>* with a unique Azure container registry name of your choice.</span></span>

```azurecli-interactive
az acr create --name <registry_name> --resource-group myResourceGroup --location "West US" --sku Basic
```

<span data-ttu-id="c4714-195">Output</span><span class="sxs-lookup"><span data-stu-id="c4714-195">Output</span></span>
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

### <a name="retrieve-hello-registry-credentials-for-pushing-and-pulling-docker-images"></a><span data-ttu-id="c4714-196">Recuperare le credenziali del Registro di sistema di hello per push e pull immagini Docker</span><span class="sxs-lookup"><span data-stu-id="c4714-196">Retrieve hello registry credentials for pushing and pulling Docker images</span></span>

<span data-ttu-id="c4714-197">le credenziali del Registro di sistema tooshow, abilitare prima la modalità di amministrazione.</span><span class="sxs-lookup"><span data-stu-id="c4714-197">tooshow registry credentials, enable admin mode first.</span></span>

```azurecli-interactive
az acr update --name <registry_name> --admin-enabled true
az acr credential show -n <registry_name>
```

<span data-ttu-id="c4714-198">Vengono visualizzate due password.</span><span class="sxs-lookup"><span data-stu-id="c4714-198">You see two passwords.</span></span> <span data-ttu-id="c4714-199">Prendere nota del nome utente hello e una password prima di hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-199">Make note of hello user name and hello first password.</span></span>

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

### <a name="upload-your-docker-container-tooazure-container-registry"></a><span data-ttu-id="c4714-200">Caricare il tooAzure contenitore Docker contenitore del Registro di sistema</span><span class="sxs-lookup"><span data-stu-id="c4714-200">Upload your Docker container tooAzure Container Registry</span></span>

```bash
docker login <registry_name>.azurecr.io -u <registry_name> -p "<registry_password>"
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
```

## <a name="deploy-hello-docker-python-flask-application-tooazure"></a><span data-ttu-id="c4714-201">Distribuire hello Docker Python pallone applicazione tooAzure</span><span class="sxs-lookup"><span data-stu-id="c4714-201">Deploy hello Docker Python Flask application tooAzure</span></span>

<span data-ttu-id="c4714-202">In questo passaggio, si distribuisce il tooAzure legata applicazione Python pallone nella basate sul contenitore Docker servizio App.</span><span class="sxs-lookup"><span data-stu-id="c4714-202">In this step, you deploy your Docker container-based Python Flask application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="c4714-203">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="c4714-203">Create an App Service plan</span></span>

<span data-ttu-id="c4714-204">Creare un piano di servizio App con hello [crea piano di servizio App az](/cli/azure/appservice/plan#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c4714-204">Create an App Service plan with hello [az appservice plan create](/cli/azure/appservice/plan#create) command.</span></span> 

[!INCLUDE [app-service-plan](../../includes/app-service-plan.md)]

<span data-ttu-id="c4714-205">esempio Hello crea un piano di servizio App basata su Linux denominato *myAppServicePlan* hello S1 tariffario utilizzando:</span><span class="sxs-lookup"><span data-stu-id="c4714-205">hello following example creates a Linux-based App Service plan named *myAppServicePlan* using hello S1 pricing tier:</span></span>

```azurecli-interactive
az appservice plan create --name myAppServicePlan --resource-group myResourceGroup --sku S1 --is-linux
```

<span data-ttu-id="c4714-206">Quando viene creato il piano di servizio App hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c4714-206">When hello App Service plan is created, hello Azure CLI shows information similar toohello following example:</span></span>

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

### <a name="create-a-web-app"></a><span data-ttu-id="c4714-207">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="c4714-207">Create a web app</span></span>

<span data-ttu-id="c4714-208">Creare un'app web in hello *myAppServicePlan* il piano di servizio App con hello [az webapp creare](/cli/azure/webapp#create) comando.</span><span class="sxs-lookup"><span data-stu-id="c4714-208">Create a web app in hello *myAppServicePlan* App Service plan with hello [az webapp create](/cli/azure/webapp#create) command.</span></span> 

<span data-ttu-id="c4714-209">Consente di app web Hello è un tipo di hosting spazio toodeploy il codice e fornisce un URL per l'utente tooview hello applicazione distribuita.</span><span class="sxs-lookup"><span data-stu-id="c4714-209">hello web app gives you a hosting space toodeploy your code and provides a URL for you tooview hello deployed application.</span></span> <span data-ttu-id="c4714-210">Utilizzare toocreate hello web app.</span><span class="sxs-lookup"><span data-stu-id="c4714-210">Use  toocreate hello web app.</span></span> 

<span data-ttu-id="c4714-211">In hello seguente comando, sostituire hello  *\<nome_app >* segnaposto con un nome univoco dell'app.</span><span class="sxs-lookup"><span data-stu-id="c4714-211">In hello following command, replace hello *\<app_name>* placeholder with a unique app name.</span></span> <span data-ttu-id="c4714-212">Questo nome fa parte dell'URL di hello predefinito per l'app web hello, in modo nome hello deve toobe univoco tra tutte le App in Azure App Service.</span><span class="sxs-lookup"><span data-stu-id="c4714-212">This name is part of hello default URL for hello web app, so hello name needs toobe unique across all apps in Azure App Service.</span></span> 

```azurecli
az webapp create --name <app_name> --resource-group myResourceGroup --plan myAppServicePlan
```

<span data-ttu-id="c4714-213">Quando hello web app è stata creata, hello Azure CLI indica toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="c4714-213">When hello web app has been created, hello Azure CLI shows information similar toohello following example:</span></span> 

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

### <a name="configure-hello-database-environment-variables"></a><span data-ttu-id="c4714-214">Configurare le variabili di ambiente database hello</span><span class="sxs-lookup"><span data-stu-id="c4714-214">Configure hello database environment variables</span></span>

<span data-ttu-id="c4714-215">In precedenza nell'esercitazione hello è definito database PostgreSQL di ambiente variabili tooconnect tooyour.</span><span class="sxs-lookup"><span data-stu-id="c4714-215">Earlier in hello tutorial, you defined environment variables tooconnect tooyour PostgreSQL database.</span></span>

<span data-ttu-id="c4714-216">Nel servizio App, impostare le variabili di ambiente come _impostazioni app_ utilizzando hello [az webapp configurazione appsettings set](/cli/azure/webapp/config#set) comando.</span><span class="sxs-lookup"><span data-stu-id="c4714-216">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config#set) command.</span></span> 

<span data-ttu-id="c4714-217">Hello esempio seguente specifica i dettagli della connessione database hello come impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="c4714-217">hello following example specifies hello database connection details as app settings.</span></span> <span data-ttu-id="c4714-218">Utilizza inoltre hello *porta* variabile toomap PORT 5000 dal traffico contenitore Docker tooreceive HTTP sulla porta 80.</span><span class="sxs-lookup"><span data-stu-id="c4714-218">It also uses hello *PORT* variable toomap PORT 5000 from your Docker Container tooreceive HTTP traffic on PORT 80.</span></span>

```azurecli-interactive
az webapp config appsettings set --name <app_name> --resource-group myResourceGroup --settings DBHOST="<postgresql_name>.postgres.database.azure.com" DBUSER="manager@<postgresql_name>" DBPASS="supersecretpass" DBNAME="eventregistration" PORT=5000
```

### <a name="configure-docker-container-deployment"></a><span data-ttu-id="c4714-219">Configurare la distribuzione del contenitore Docker</span><span class="sxs-lookup"><span data-stu-id="c4714-219">Configure Docker container deployment</span></span> 

<span data-ttu-id="c4714-220">AppService può automaticamente di scaricare ed eseguire un contenitore Docker.</span><span class="sxs-lookup"><span data-stu-id="c4714-220">AppService can automatically download and run a Docker container.</span></span>

```azurecli
az webapp config container set --resource-group myResourceGroup --name <app_name> --docker-registry-server-user "<registry_name>" --docker-registry-server-password "<registry_password>" --docker-custom-image-name "<registry_name>.azurecr.io/flask-postgresql-sample" --docker-registry-server-url "https://<registry_name>.azurecr.io"
```

<span data-ttu-id="c4714-221">Quando si aggiorna contenitore Docker hello o modificare le impostazioni di hello, riavviare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-221">Whenever you update hello Docker container or change hello settings, restart hello app.</span></span> <span data-ttu-id="c4714-222">Il riavvio garantisce che tutte le impostazioni vengono applicate e contenitore più recente di hello viene effettuato il pull dal Registro di sistema hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-222">Restarting ensures that all settings are applied and hello latest container is pulled from hello registry.</span></span>

```azurecli-interactive
az webapp restart --resource-group myResourceGroup --name <app_name>
```

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="c4714-223">Sfoglia toohello Azure web app</span><span class="sxs-lookup"><span data-stu-id="c4714-223">Browse toohello Azure web app</span></span> 

<span data-ttu-id="c4714-224">Esplorare app web toohello distribuito tramite il browser.</span><span class="sxs-lookup"><span data-stu-id="c4714-224">Browse toohello deployed web app using your web browser.</span></span> 

```bash 
http://<app_name>.azurewebsites.net 
```
> [!NOTE]
> <span data-ttu-id="c4714-225">app web Hello accetta più tooload poiché hello contenitore dispone di toobe scaricato e avviato dopo la modifica di configurazione del contenitore hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-225">hello web app takes longer tooload because hello container has toobe downloaded and started after hello container configuration is changed.</span></span>

<span data-ttu-id="c4714-226">Viene visualizzato agli utenti guest registrato in precedenza che sono stati salvati i database di produzione di Azure toohello nel passaggio precedente hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-226">You see previously registered guests that were saved toohello Azure production database in hello previous step.</span></span>

![Applicazione Python Flask basata sul contenitore Docker in esecuzione in locale](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-app-deployed.png)

<span data-ttu-id="c4714-228">**Congratulazioni.**</span><span class="sxs-lookup"><span data-stu-id="c4714-228">**Congratulations!**</span></span> <span data-ttu-id="c4714-229">L'app Python Flask basata sul contenitore Docker è in esecuzione nel Servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4714-229">You're running a Docker container-based Python Flask app in Azure App Service.</span></span>

## <a name="update-data-model-and-redeploy"></a><span data-ttu-id="c4714-230">Aggiornare il modello di dati e ridistribuire</span><span class="sxs-lookup"><span data-stu-id="c4714-230">Update data model and redeploy</span></span>

<span data-ttu-id="c4714-231">In questo passaggio si aggiunge il numero di hello di registrazione eventi di partecipanti tooeach aggiornando hello Guest modello.</span><span class="sxs-lookup"><span data-stu-id="c4714-231">In this step, you add hello number of attendees tooeach event registration by updating hello Guest model.</span></span>

<span data-ttu-id="c4714-232">Estrarre hello *0,2 migrazione* versione con hello git comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c4714-232">Check out hello *0.2-migration* release with hello following git command:</span></span>

```bash
git checkout tags/0.2-migration
```

<span data-ttu-id="c4714-233">Questa versione è già eseguite hello tooviews le modifiche necessarie, controller e modello.</span><span class="sxs-lookup"><span data-stu-id="c4714-233">This release already made hello necessary changes tooviews, controllers, and model.</span></span> <span data-ttu-id="c4714-234">Include anche una migrazione del database generata tramite *alembic* (`flask db migrate`).</span><span class="sxs-lookup"><span data-stu-id="c4714-234">It also includes a database migration generated via *alembic* (`flask db migrate`).</span></span> <span data-ttu-id="c4714-235">È possibile visualizzare tutte le modifiche apportate tramite hello git comando seguente:</span><span class="sxs-lookup"><span data-stu-id="c4714-235">You can see all changes made via hello following git command:</span></span>

```bash
git diff 0.1-initialapp 0.2-migration
```

### <a name="test-your-changes-locally"></a><span data-ttu-id="c4714-236">Testare le modifiche in locale</span><span class="sxs-lookup"><span data-stu-id="c4714-236">Test your changes locally</span></span>

<span data-ttu-id="c4714-237">Eseguire hello seguenti comandi tootest le modifiche localmente dal server di pallone hello in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="c4714-237">Run hello following commands tootest your changes locally by running hello flask server.</span></span>

<span data-ttu-id="c4714-238">Mac/Linux:</span><span class="sxs-lookup"><span data-stu-id="c4714-238">Mac / Linux:</span></span>
```bash
source venv/bin/activate
cd app
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask db upgrade
FLASK_APP=app.py DBHOST="localhost" DBUSER="manager" DBNAME="eventregistration" DBPASS="supersecretpass" flask run
```

<span data-ttu-id="c4714-239">Passare toohttp://127.0.0.1:5000 le modifiche di hello tooview browser.</span><span class="sxs-lookup"><span data-stu-id="c4714-239">Navigate toohttp://127.0.0.1:5000 in your browser tooview hello changes.</span></span> <span data-ttu-id="c4714-240">Creare una registrazione test.</span><span class="sxs-lookup"><span data-stu-id="c4714-240">Create a test registration.</span></span>

![Applicazione Python Flask basata sul contenitore Docker in esecuzione in locale](./media/app-service-web-tutorial-docker-python-postgresql-app/local-app-v2.png)

### <a name="publish-changes-tooazure"></a><span data-ttu-id="c4714-242">Pubblicare le modifiche tooAzure</span><span class="sxs-lookup"><span data-stu-id="c4714-242">Publish changes tooAzure</span></span>

<span data-ttu-id="c4714-243">Creare una nuova immagine di docker hello, spingerla del Registro di sistema di toohello contenitore e riavviare l'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-243">Build hello new docker image, push it toohello container registry, and restart hello app.</span></span>

```bash
docker build -t flask-postgresql-sample .
docker tag flask-postgresql-sample <registry_name>.azurecr.io/flask-postgresql-sample
docker push <registry_name>.azurecr.io/flask-postgresql-sample
az appservice web restart --resource-group myResourceGroup --name <app_name>
```

<span data-ttu-id="c4714-244">Passare tooyour Azure web app e provare nuovamente la nuova funzionalità hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-244">Navigate tooyour Azure web app and try out hello new functionality again.</span></span> <span data-ttu-id="c4714-245">Creare un'altra registrazione dell'evento.</span><span class="sxs-lookup"><span data-stu-id="c4714-245">Create another event registration.</span></span>

```bash 
http://<app_name>.azurewebsites.net 
```

![App Docker Python Flask nel Servizio app di Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/docker-flask-in-azure.png)

## <a name="manage-your-azure-web-app"></a><span data-ttu-id="c4714-247">Gestire l'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="c4714-247">Manage your Azure web app</span></span>

<span data-ttu-id="c4714-248">Passare toohello [portale di Azure](https://portal.azure.com) toosee hello web app è stato creato.</span><span class="sxs-lookup"><span data-stu-id="c4714-248">Go toohello [Azure portal](https://portal.azure.com) toosee hello web app you created.</span></span>

<span data-ttu-id="c4714-249">Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="c4714-249">From hello left menu, click **App Services**, then click hello name of your Azure web app.</span></span>

![Spostamento del portale tooAzure web app](./media/app-service-web-tutorial-docker-python-postgresql-app/app-resource.png)

<span data-ttu-id="c4714-251">Per impostazione predefinita, il portale di hello Mostra dell'app web **Panoramica** pagina.</span><span class="sxs-lookup"><span data-stu-id="c4714-251">By default, hello portal shows your web app's **Overview** page.</span></span> <span data-ttu-id="c4714-252">che offre una visualizzazione dello stato dell'app.</span><span class="sxs-lookup"><span data-stu-id="c4714-252">This page gives you a view of how your app is doing.</span></span> <span data-ttu-id="c4714-253">In questa pagina è anche possibile eseguire attività di gestione di base come esplorare, arrestare, avviare, riavviare ed eliminare.</span><span class="sxs-lookup"><span data-stu-id="c4714-253">Here, you can also perform basic management tasks like browse, stop, start, restart, and delete.</span></span> <span data-ttu-id="c4714-254">schede di Hello sul lato sinistro di hello della pagina hello mostrano è possibile aprire le pagine di configurazione diverso hello.</span><span class="sxs-lookup"><span data-stu-id="c4714-254">hello tabs on hello left side of hello page show hello different configuration pages you can open.</span></span>

![Pagina del servizio app nel portale di Azure](./media/app-service-web-tutorial-docker-python-postgresql-app/app-mgmt.png)

## <a name="next-steps"></a><span data-ttu-id="c4714-256">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c4714-256">Next steps</span></span>

<span data-ttu-id="c4714-257">Spostare toolearn esercitazione successiva toohello come toomap un DNS personalizzato denominati tooyour web app.</span><span class="sxs-lookup"><span data-stu-id="c4714-257">Advance toohello next tutorial toolearn how toomap a custom DNS name tooyour web app.</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="c4714-258">Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web</span><span class="sxs-lookup"><span data-stu-id="c4714-258">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
