---
title: aaaBuild un'app web PHP e MySQL in Azure | Documenti Microsoft
description: Informazioni su come tooget un'applicazione PHP Usa Azure, con connessione tooa MySQL di database in Azure.
services: app-service\web
documentationcenter: nodejs
author: cephalin
manager: erikre
editor: 
ms.assetid: 14feb4f3-5095-496e-9a40-690e1414bd73
ms.service: app-service-web
ms.workload: web
ms.tgt_pltfrm: na
ms.devlang: nodejs
ms.topic: tutorial
ms.date: 07/21/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 3c050b30e2e2c80d011bed989cd5f8cecac35d15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="b806e-103">Creare un'app Web PHP e MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="b806e-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="b806e-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="b806e-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="b806e-105">Questa esercitazione viene illustrato come toocreate PHP web app in Azure e connetterla tooa di database MySQL.</span><span class="sxs-lookup"><span data-stu-id="b806e-105">This tutorial shows how toocreate a PHP web app in Azure and connect it tooa MySQL database.</span></span> <span data-ttu-id="b806e-106">Al termine, sarà disponibile un'app [Laravel](https://laravel.com/) in esecuzione nelle app Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="b806e-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![App PHP in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="b806e-108">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="b806e-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b806e-109">Creare un database MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="b806e-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="b806e-110">Connettersi a un tooMySQL app PHP</span><span class="sxs-lookup"><span data-stu-id="b806e-110">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="b806e-111">Distribuire hello app tooAzure</span><span class="sxs-lookup"><span data-stu-id="b806e-111">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="b806e-112">Modello di dati hello e ridistribuire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="b806e-112">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="b806e-113">Eseguire lo streaming dei log di diagnostica in Azure</span><span class="sxs-lookup"><span data-stu-id="b806e-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="b806e-114">Gestire app hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b806e-114">Manage hello app in hello Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b806e-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="b806e-115">Prerequisites</span></span>

<span data-ttu-id="b806e-116">toocomplete questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="b806e-116">toocomplete this tutorial:</span></span>

* [<span data-ttu-id="b806e-117">Installare Git</span><span class="sxs-lookup"><span data-stu-id="b806e-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="b806e-118">Installare PHP 5.6.4 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="b806e-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="b806e-119">Installare Composer</span><span class="sxs-lookup"><span data-stu-id="b806e-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="b806e-120">Abilitare hello seguenti estensioni di PHP esigenze Laravel: OpenSSL, PDO MySQL, Mbstring, Tokenizer, XML</span><span class="sxs-lookup"><span data-stu-id="b806e-120">Enable hello following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="b806e-121">Installare e avviare MySQL</span><span class="sxs-lookup"><span data-stu-id="b806e-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="b806e-122">Preparare MySQL in locale</span><span class="sxs-lookup"><span data-stu-id="b806e-122">Prepare local MySQL</span></span>

<span data-ttu-id="b806e-123">In questo passaggio, si crea un database nel server locale di MySQL da usare in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b806e-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-toolocal-mysql-server"></a><span data-ttu-id="b806e-124">Connettere toolocal MySQL server</span><span class="sxs-lookup"><span data-stu-id="b806e-124">Connect toolocal MySQL server</span></span>

<span data-ttu-id="b806e-125">In una finestra terminale, connettersi tooyour locale MySQL server.</span><span class="sxs-lookup"><span data-stu-id="b806e-125">In a terminal window, connect tooyour local MySQL server.</span></span> <span data-ttu-id="b806e-126">In questa esercitazione, è possibile utilizzare questa finestra terminale di toorun tutti i comandi di hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-126">You can use this terminal window toorun all hello commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="b806e-127">Se viene chiesto di immettere una password, immettere la password di hello per hello `root` account.</span><span class="sxs-lookup"><span data-stu-id="b806e-127">If you're prompted for a password, enter hello password for hello `root` account.</span></span> <span data-ttu-id="b806e-128">Se non si ricorda la password dell'account radice, vedere [MySQL: modalità tooReset hello Password Root](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="b806e-128">If you don't remember your root account password, see [MySQL: How tooReset hello Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="b806e-129">Se il comando viene eseguito correttamente, il server MySQL è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="b806e-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="b806e-130">In caso contrario, assicurarsi che il server MySQL locale viene eseguito da hello seguente [passaggi successivi all'installazione di MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="b806e-130">If not, make sure that your local MySQL server is started by following hello [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="b806e-131">Creare un database in locale</span><span class="sxs-lookup"><span data-stu-id="b806e-131">Create a database locally</span></span>

<span data-ttu-id="b806e-132">In hello `mysql` richiedono, creare un database.</span><span class="sxs-lookup"><span data-stu-id="b806e-132">At hello `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="b806e-133">Chiudere la connessione al server digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="b806e-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="b806e-134">Creare un'app PHP in locale</span><span class="sxs-lookup"><span data-stu-id="b806e-134">Create a PHP app locally</span></span>
<span data-ttu-id="b806e-135">In questo passaggio si ottiene un'applicazione di esempio Laravel, se ne configurare la connessione al database e la si esegue in locale.</span><span class="sxs-lookup"><span data-stu-id="b806e-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-hello-sample"></a><span data-ttu-id="b806e-136">Esempio hello clone</span><span class="sxs-lookup"><span data-stu-id="b806e-136">Clone hello sample</span></span>

<span data-ttu-id="b806e-137">Nella finestra terminal hello `cd` tooa directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="b806e-137">In hello terminal window, `cd` tooa working directory.</span></span>

<span data-ttu-id="b806e-138">Eseguire hello seguenti repository di esempio di comando tooclone hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-138">Run hello following command tooclone hello sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="b806e-139">`cd`directory clonato tooyour.</span><span class="sxs-lookup"><span data-stu-id="b806e-139">`cd` tooyour cloned directory.</span></span>
<span data-ttu-id="b806e-140">Installare i pacchetti hello necessario.</span><span class="sxs-lookup"><span data-stu-id="b806e-140">Install hello required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="b806e-141">Configurare la connessione di MySQL</span><span class="sxs-lookup"><span data-stu-id="b806e-141">Configure MySQL connection</span></span>

<span data-ttu-id="b806e-142">Nella radice del repository hello, creare un file denominato *.env*.</span><span class="sxs-lookup"><span data-stu-id="b806e-142">In hello repository root, create a file named *.env*.</span></span> <span data-ttu-id="b806e-143">Hello copia seguenti variabili in hello *.env* file.</span><span class="sxs-lookup"><span data-stu-id="b806e-143">Copy hello following variables into hello *.env* file.</span></span> <span data-ttu-id="b806e-144">Sostituire hello  _&lt;root_password >_ segnaposto con la password dell'utente di hello MySQL radice.</span><span class="sxs-lookup"><span data-stu-id="b806e-144">Replace hello _&lt;root_password>_ placeholder with hello MySQL root user's password.</span></span>

```
APP_ENV=local
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_DATABASE=sampledb
DB_USERNAME=root
DB_PASSWORD=<root_password>
```

<span data-ttu-id="b806e-145">Per informazioni sulle modalità di utilizzo hello Laravel _.env_ file, vedere [la configurazione dell'ambiente Laravel](https://laravel.com/docs/5.4/configuration#environment-configuration).</span><span class="sxs-lookup"><span data-stu-id="b806e-145">For information on how Laravel uses hello _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-hello-sample-locally"></a><span data-ttu-id="b806e-146">Eseguire in locale: esempio hello</span><span class="sxs-lookup"><span data-stu-id="b806e-146">Run hello sample locally</span></span>

<span data-ttu-id="b806e-147">Eseguire [migrazioni database Laravel](https://laravel.com/docs/5.4/migrations) toocreate hello tabelle hello esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b806e-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) toocreate hello tables hello application needs.</span></span> <span data-ttu-id="b806e-148">le tabelle vengono create nelle migrazioni hello, cercare in hello toosee _database/migrazioni_ directory nel repository Git hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-148">toosee which tables are created in hello migrations, look in hello _database/migrations_ directory in hello Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="b806e-149">Generare una nuova chiave per l'applicazione Laravel.</span><span class="sxs-lookup"><span data-stu-id="b806e-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="b806e-150">Eseguire un'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-150">Run hello application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="b806e-151">Passare troppo`http://localhost:8000` in un browser.</span><span class="sxs-lookup"><span data-stu-id="b806e-151">Navigate too`http://localhost:8000` in a browser.</span></span> <span data-ttu-id="b806e-152">Nella pagina di hello, aggiungere alcune attività.</span><span class="sxs-lookup"><span data-stu-id="b806e-152">Add a few tasks in hello page.</span></span>

![PHP si connette correttamente tooMySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="b806e-154">Digitare toostop PHP, `Ctrl + C` in hello terminal.</span><span class="sxs-lookup"><span data-stu-id="b806e-154">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="b806e-155">Creare MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="b806e-155">Create MySQL in Azure</span></span>

<span data-ttu-id="b806e-156">In questo passaggio viene creato un database MySQL nel [database di Azure per MySQL (anteprima)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="b806e-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="b806e-157">In un secondo momento, configurare il database toothis tooconnect di hello PHP dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b806e-157">Later, you configure hello PHP application tooconnect toothis database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="b806e-158">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="b806e-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="b806e-159">Creare un server MySQL</span><span class="sxs-lookup"><span data-stu-id="b806e-159">Create a MySQL server</span></span>

<span data-ttu-id="b806e-160">Creare un server nel Database di Azure per MySQL (anteprima) con hello [creare server mysql az](/cli/azure/mysql/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b806e-160">Create a server in Azure Database for MySQL (Preview) with hello [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="b806e-161">In hello seguente comando, sostituire il nome del server MySQL in cui si vedere hello  _&lt;mysql_server_name >_ segnaposto (i caratteri validi sono `a-z`, `0-9`, e `-`).</span><span class="sxs-lookup"><span data-stu-id="b806e-161">In hello following command, substitute your MySQL server name where you see hello _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="b806e-162">Questo nome fa parte del nome host del server MySQL hello (`<mysql_server_name>.database.windows.net`), è necessario toobe univoco globale.</span><span class="sxs-lookup"><span data-stu-id="b806e-162">This name is part of hello MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs toobe globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="b806e-163">Creazione di server MySQL hello, hello CLI di Azure Mostra toohello di informazioni simili esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="b806e-163">When hello MySQL server is created, hello Azure CLI shows information similar toohello following example:</span></span>

```json
{
  "administratorLogin": "adminuser",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "<mysql_server_name>.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.DBforMySQL/servers/<mysql_server_name>",
  "location": "northeurope",
  "name": "<mysql_server_name>",
  "resourceGroup": "myResourceGroup",
  ...
}
```

### <a name="configure-server-firewall"></a><span data-ttu-id="b806e-164">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="b806e-164">Configure server firewall</span></span>

<span data-ttu-id="b806e-165">Creare una regola del firewall per il client di MySQL server tooallow connessioni tramite hello [az mysql regola firewall del server-creare](/cli/azure/mysql/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="b806e-165">Create a firewall rule for your MySQL server tooallow client connections by using hello [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="b806e-166">Il Database di Azure per MySQL (anteprima) non attualmente limita servizi tooAzure solo le connessioni.</span><span class="sxs-lookup"><span data-stu-id="b806e-166">Azure Database for MySQL (Preview) doesn't currently limit connections only tooAzure services.</span></span> <span data-ttu-id="b806e-167">Come vengono assegnati dinamicamente agli indirizzi IP in Azure, è preferibile tooenable tutti gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="b806e-167">As IP addresses in Azure are dynamically assigned, it is better tooenable all IP addresses.</span></span> <span data-ttu-id="b806e-168">servizio Hello è in anteprima.</span><span class="sxs-lookup"><span data-stu-id="b806e-168">hello service is in preview.</span></span> <span data-ttu-id="b806e-169">Verranno resi disponibili metodi migliori per la protezione del database.</span><span class="sxs-lookup"><span data-stu-id="b806e-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-tooproduction-mysql-server-locally"></a><span data-ttu-id="b806e-170">Connettersi tooproduction MySQL server in locale</span><span class="sxs-lookup"><span data-stu-id="b806e-170">Connect tooproduction MySQL server locally</span></span>

<span data-ttu-id="b806e-171">Nella finestra terminal hello connettersi toohello MySQL server in Azure.</span><span class="sxs-lookup"><span data-stu-id="b806e-171">In hello terminal window, connect toohello MySQL server in Azure.</span></span> <span data-ttu-id="b806e-172">Utilizzare il valore di hello specificato in precedenza per  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="b806e-172">Use hello value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="b806e-173">Quando viene richiesto di immettere una password, utilizzare _tr0ngPa $$ w0rd!_, specificato al momento della creazione del database hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created hello database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="b806e-174">Creare un database di produzione</span><span class="sxs-lookup"><span data-stu-id="b806e-174">Create a production database</span></span>

<span data-ttu-id="b806e-175">In hello `mysql` richiedono, creare un database.</span><span class="sxs-lookup"><span data-stu-id="b806e-175">At hello `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="b806e-176">Creare un utente con autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="b806e-176">Create a user with permissions</span></span>

<span data-ttu-id="b806e-177">Creare un utente di database denominato _phpappuser_ e assegnare tutti i privilegi in hello `sampledb` database.</span><span class="sxs-lookup"><span data-stu-id="b806e-177">Create a database user called _phpappuser_ and give it all privileges in hello `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* too'phpappuser';
```

<span data-ttu-id="b806e-178">Chiudere una connessione al server hello digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="b806e-178">Exit hello server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-tooazure-mysql"></a><span data-ttu-id="b806e-179">Connettere l'app tooAzure MySQL</span><span class="sxs-lookup"><span data-stu-id="b806e-179">Connect app tooAzure MySQL</span></span>

<span data-ttu-id="b806e-180">In questo passaggio è connettersi hello PHP toohello MySQL database dell'applicazione creato nel Database di Azure per MySQL (anteprima).</span><span class="sxs-lookup"><span data-stu-id="b806e-180">In this step, you connect hello PHP application toohello MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-hello-database-connection"></a><span data-ttu-id="b806e-181">Configurare una connessione al database hello</span><span class="sxs-lookup"><span data-stu-id="b806e-181">Configure hello database connection</span></span>

<span data-ttu-id="b806e-182">Nella radice del repository hello, creare un _. env.production_ file e copia hello seguenti variabili al suo interno.</span><span class="sxs-lookup"><span data-stu-id="b806e-182">In hello repository root, create an _.env.production_ file and copy hello following variables into it.</span></span> <span data-ttu-id="b806e-183">Sostituire il segnaposto hello  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="b806e-183">Replace hello placeholder _&lt;mysql_server_name>_.</span></span>

```
APP_ENV=production
APP_DEBUG=true
APP_KEY=SomeRandomString

DB_CONNECTION=mysql
DB_HOST=<mysql_server_name>.database.windows.net
DB_DATABASE=sampledb
DB_USERNAME=phpappuser@<mysql_server_name>
DB_PASSWORD=MySQLAzure2017
MYSQL_SSL=true
```

<span data-ttu-id="b806e-184">Salvare le modifiche di hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-184">Save hello changes.</span></span>

> [!TIP]
> <span data-ttu-id="b806e-185">le informazioni di connessione MySQL, questo file sono già esclusa dal repository Git hello toosecure (vedere _con estensione gitignore_ nella radice del repository hello).</span><span class="sxs-lookup"><span data-stu-id="b806e-185">toosecure your MySQL connection information, this file is already excluded from hello Git repository (See _.gitignore_ in hello repository root).</span></span> <span data-ttu-id="b806e-186">Successivamente, viene illustrato come variabili di ambiente tooconfigure nel servizio App tooconnect tooyour database nel Database di Azure per MySQL (anteprima).</span><span class="sxs-lookup"><span data-stu-id="b806e-186">Later, you learn how tooconfigure environment variables in App Service tooconnect tooyour database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="b806e-187">Con le variabili di ambiente, non devi hello *.env* file nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="b806e-187">With environment variables, you don't need hello *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="b806e-188">Configurare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="b806e-188">Configure SSL certificate</span></span>

<span data-ttu-id="b806e-189">Per impostazione predefinita, Database di Azure per MySQL impone le connessioni SSL dai client.</span><span class="sxs-lookup"><span data-stu-id="b806e-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="b806e-190">database di MySQL tooconnect tooyour in Azure, è necessario utilizzare un _PEM_ certificato SSL.</span><span class="sxs-lookup"><span data-stu-id="b806e-190">tooconnect tooyour MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="b806e-191">Aprire _config/database.php_ e aggiungere hello _sslmode_ e _opzioni_ parametri troppo`connections.mysql`, come illustrato nel seguente codice hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-191">Open _config/database.php_ and add hello _sslmode_ and _options_ parameters too`connections.mysql`, as shown in hello following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="b806e-192">toolearn come toogenerate questo _certificate.pem_, vedere [connettività configurare SSL in toosecurely l'applicazione connessione tooAzure Database MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="b806e-192">toolearn how toogenerate this _certificate.pem_, see [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="b806e-193">percorso Hello _/ssl/certificate.pem_ punta esistente tooan _certificate.pem_ file nel repository Git hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-193">hello path _/ssl/certificate.pem_ points tooan existing _certificate.pem_ file in hello Git repository.</span></span> <span data-ttu-id="b806e-194">Il file è già incluso per ragioni di praticità in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="b806e-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="b806e-195">È consigliabile non eseguire il commit dei certificati _.pem_ nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="b806e-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-hello-application-locally"></a><span data-ttu-id="b806e-196">Testare l'applicazione hello in locale</span><span class="sxs-lookup"><span data-stu-id="b806e-196">Test hello application locally</span></span>

<span data-ttu-id="b806e-197">Eseguire migrazioni database Laravel con _. env.production_ come hello ambiente file toocreate hello tabelle del database MySQL nel Database di Azure per MySQL (anteprima).</span><span class="sxs-lookup"><span data-stu-id="b806e-197">Run Laravel database migrations with _.env.production_ as hello environment file toocreate hello tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="b806e-198">Tenere presente che _. env.production_ dispone di database di MySQL tooyour informazioni connessione hello in Azure.</span><span class="sxs-lookup"><span data-stu-id="b806e-198">Remember that _.env.production_ has hello connection information tooyour MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="b806e-199">_.env.production_ non dispone ancora di una chiave applicazione valida.</span><span class="sxs-lookup"><span data-stu-id="b806e-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="b806e-200">Generarne uno nuovo per tale in hello terminal.</span><span class="sxs-lookup"><span data-stu-id="b806e-200">Generate a new one for it in hello terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="b806e-201">Eseguire l'applicazione di esempio hello con _. env.production_ come file di ambiente hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-201">Run hello sample application with _.env.production_ as hello environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="b806e-202">Passare troppo`http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="b806e-202">Navigate too`http://localhost:8000`.</span></span> <span data-ttu-id="b806e-203">Se la pagina hello viene caricata senza errori, hello applicazione PHP connessione toohello database MySQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="b806e-203">If hello page loads without errors, hello PHP application is connecting toohello MySQL database in Azure.</span></span>

<span data-ttu-id="b806e-204">Nella pagina di hello, aggiungere alcune attività.</span><span class="sxs-lookup"><span data-stu-id="b806e-204">Add a few tasks in hello page.</span></span>

![PHP si connette correttamente tooAzure Database MySQL (anteprima)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="b806e-206">Digitare toostop PHP, `Ctrl + C` in hello terminal.</span><span class="sxs-lookup"><span data-stu-id="b806e-206">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="b806e-207">Eseguire il commit delle modifiche</span><span class="sxs-lookup"><span data-stu-id="b806e-207">Commit your changes</span></span>

<span data-ttu-id="b806e-208">Eseguire hello toocommit comandi Git dopo le modifiche:</span><span class="sxs-lookup"><span data-stu-id="b806e-208">Run hello following Git commands toocommit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="b806e-209">L'app è pronta toobe distribuito.</span><span class="sxs-lookup"><span data-stu-id="b806e-209">Your app is ready toobe deployed.</span></span>

## <a name="deploy-tooazure"></a><span data-ttu-id="b806e-210">Distribuire tooAzure</span><span class="sxs-lookup"><span data-stu-id="b806e-210">Deploy tooAzure</span></span>

<span data-ttu-id="b806e-211">In questo passaggio, si distribuisce hello connesso MySQL PHP applicazione tooAzure servizio App.</span><span class="sxs-lookup"><span data-stu-id="b806e-211">In this step, you deploy hello MySQL-connected PHP application tooAzure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="b806e-212">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="b806e-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="b806e-213">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="b806e-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-hello-php-version"></a><span data-ttu-id="b806e-214">Imposta la versione di hello PHP</span><span class="sxs-lookup"><span data-stu-id="b806e-214">Set hello PHP version</span></span>

<span data-ttu-id="b806e-215">Versione PHP hello set che hello applicazione richiede mediante hello [az webapp config set](/cli/azure/webapp/config#set) comando.</span><span class="sxs-lookup"><span data-stu-id="b806e-215">Set hello PHP version that hello application requires by using hello [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="b806e-216">Hello il comando seguente imposta too_7.0_ versione di hello PHP.</span><span class="sxs-lookup"><span data-stu-id="b806e-216">hello following command sets hello PHP version too_7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="b806e-217">Configurare le impostazioni del database</span><span class="sxs-lookup"><span data-stu-id="b806e-217">Configure database settings</span></span>

<span data-ttu-id="b806e-218">Come evidenziato in precedenza, è possibile connettere il database di MySQL Azure tooyour utilizzando variabili di ambiente nel servizio App.</span><span class="sxs-lookup"><span data-stu-id="b806e-218">As pointed out previously, you can connect tooyour Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="b806e-219">Nel servizio App, impostare le variabili di ambiente come _impostazioni app_ utilizzando hello [az webapp configurazione appsettings set](/cli/azure/webapp/config/appsettings#set) comando.</span><span class="sxs-lookup"><span data-stu-id="b806e-219">In App Service, you set environment variables as _app settings_ by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="b806e-220">il comando seguente Hello Configura impostazioni app hello `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, e `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="b806e-220">hello following command configures hello app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="b806e-221">Sostituire i segnaposto hello  _&lt;appname >_ e  _&lt;mysql_server_name >_.</span><span class="sxs-lookup"><span data-stu-id="b806e-221">Replace hello placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="b806e-222">È possibile utilizzare hello PHP [getenv](http://www.php.net/manual/function.getenv.php) tooaccess metodo hello impostazioni.</span><span class="sxs-lookup"><span data-stu-id="b806e-222">You can use hello PHP [getenv](http://www.php.net/manual/function.getenv.php) method tooaccess hello settings.</span></span> <span data-ttu-id="b806e-223">Hello Laravel codice utilizza un [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper su hello PHP `getenv`.</span><span class="sxs-lookup"><span data-stu-id="b806e-223">hello Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over hello PHP `getenv`.</span></span> <span data-ttu-id="b806e-224">Ad esempio, hello MySQL configurazione _config/database.php_ simile hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="b806e-224">For example, hello MySQL configuration in _config/database.php_ looks like hello following code:</span></span>

```php
'mysql' => [
    'driver'    => 'mysql',
    'host'      => env('DB_HOST', 'localhost'),
    'database'  => env('DB_DATABASE', 'forge'),
    'username'  => env('DB_USERNAME', 'forge'),
    'password'  => env('DB_PASSWORD', ''),
    ...
],
```

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="b806e-225">Configurare le variabili di ambiente di Laravel</span><span class="sxs-lookup"><span data-stu-id="b806e-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="b806e-226">Laravel richiede una chiave di applicazione nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="b806e-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="b806e-227">È possibile configurarla con le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="b806e-227">You can configure it with app settings.</span></span>

<span data-ttu-id="b806e-228">Utilizzare `php artisan` toogenerate una nuova chiave dell'applicazione senza salvarla too_.env_.</span><span class="sxs-lookup"><span data-stu-id="b806e-228">Use `php artisan` toogenerate a new application key without saving it too_.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="b806e-229">Impostare chiave applicazione hello hello servizio App di app web utilizzando hello [az webapp configurazione appsettings set](/cli/azure/webapp/config/appsettings#set) comando.</span><span class="sxs-lookup"><span data-stu-id="b806e-229">Set hello application key in hello App Service web app by using hello [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="b806e-230">Sostituire i segnaposto hello  _&lt;appname >_ e  _&lt;outputofphpartisankey: generare >_.</span><span class="sxs-lookup"><span data-stu-id="b806e-230">Replace hello placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="b806e-231">`APP_DEBUG="true"`indica Laravel tooreturn informazioni di debug quando hello distribuito l'app web rileva errori.</span><span class="sxs-lookup"><span data-stu-id="b806e-231">`APP_DEBUG="true"` tells Laravel tooreturn debugging information when hello deployed web app encounters errors.</span></span> <span data-ttu-id="b806e-232">Quando si esegue un'applicazione di produzione, impostarlo troppo`false`, che è più sicuro.</span><span class="sxs-lookup"><span data-stu-id="b806e-232">When running a production application, set it too`false`, which is more secure.</span></span>

### <a name="set-hello-virtual-application-path"></a><span data-ttu-id="b806e-233">Percorso dell'applicazione virtuale hello insieme</span><span class="sxs-lookup"><span data-stu-id="b806e-233">Set hello virtual application path</span></span>

<span data-ttu-id="b806e-234">Impostare il percorso virtuale applicazione hello per l'app web hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-234">Set hello virtual application path for hello web app.</span></span> <span data-ttu-id="b806e-235">Questo passaggio è obbligatorio perché hello [ciclo di vita dell'applicazione Laravel](https://laravel.com/docs/5.4/lifecycle) inizia in hello _pubblica_ directory anziché directory radice dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-235">This step is required because hello [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in hello _public_ directory instead of hello application's root directory.</span></span> <span data-ttu-id="b806e-236">Altri framework PHP il cui ciclo di vita Avvia nella directory radice hello può funzionare senza la configurazione manuale del percorso virtuale applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-236">Other PHP frameworks whose lifecycle start in hello root directory can work without manual configuration of hello virtual application path.</span></span>

<span data-ttu-id="b806e-237">Percorso dell'applicazione virtuale hello insieme utilizzando hello [aggiornamento risorse az](/cli/azure/resource#update) comando.</span><span class="sxs-lookup"><span data-stu-id="b806e-237">Set hello virtual application path by using hello [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="b806e-238">Sostituire hello  _&lt;appname >_ segnaposto.</span><span class="sxs-lookup"><span data-stu-id="b806e-238">Replace hello _&lt;appname>_ placeholder.</span></span>

```azurecli-interactive
az resource update \
    --name web \
    --resource-group myResourceGroup \
    --namespace Microsoft.Web \
    --resource-type config \
    --parent sites/<app_name> \
    --set properties.virtualApplications[0].physicalPath="site\wwwroot\public" \
    --api-version 2015-06-01
```

<span data-ttu-id="b806e-239">Per impostazione predefinita, Azure App Service punti percorso dell'applicazione virtuale radice hello (_/_) toohello directory radice di hello distribuiti i file dell'applicazione (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="b806e-239">By default, Azure App Service points hello root virtual application path (_/_) toohello root directory of hello deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="b806e-240">Configurare un utente della distribuzione</span><span class="sxs-lookup"><span data-stu-id="b806e-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="b806e-241">Configurare la distribuzione con l'istanza Git locale</span><span class="sxs-lookup"><span data-stu-id="b806e-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-tooazure-from-git"></a><span data-ttu-id="b806e-242">Eseguire il push tooAzure da Git</span><span class="sxs-lookup"><span data-stu-id="b806e-242">Push tooAzure from Git</span></span>

<span data-ttu-id="b806e-243">Aggiungere un repository Git locale tooyour remoto di Azure.</span><span class="sxs-lookup"><span data-stu-id="b806e-243">Add an Azure remote tooyour local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="b806e-244">Effettuare il push dell'applicazione PHP di hello Azure toodeploy remoto toohello.</span><span class="sxs-lookup"><span data-stu-id="b806e-244">Push toohello Azure remote toodeploy hello PHP application.</span></span> <span data-ttu-id="b806e-245">Viene chiesto di immettere la password di hello fornito in precedenza come parte della creazione di hello dell'utente di distribuzione hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-245">You are prompted for hello password you supplied earlier as part of hello creation of hello deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="b806e-246">Durante la distribuzione, Servizio app di Azure comunica lo stato con Git.</span><span class="sxs-lookup"><span data-stu-id="b806e-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up too8 threads.
Compressing objects: 100% (3/3), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 2), reused 0 (delta 0)
remote: Updating branch 'master'.
remote: Updating submodules.
remote: Preparing deployment for commit id 'a5e076db9c'.
remote: Running custom deployment command...
remote: Running deployment command...
...
< Output has been truncated for readability >
```

> [!NOTE]
> <span data-ttu-id="b806e-247">È possibile notare che il processo di distribuzione hello installa [Composer](https://getcomposer.org/) pacchetti alla fine di hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-247">You may notice that hello deployment process installs [Composer](https://getcomposer.org/) packages at hello end.</span></span> <span data-ttu-id="b806e-248">Servizio App non esegue tali automazioni durante la distribuzione predefinita, pertanto questo repository di esempio ha tre ulteriori file nella relativa tooenable directory radice:</span><span class="sxs-lookup"><span data-stu-id="b806e-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory tooenable it:</span></span>
>
> - <span data-ttu-id="b806e-249">`.deployment`-Questo file indica al servizio App toorun `bash deploy.sh` come script di distribuzione personalizzata hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-249">`.deployment` - This file tells App Service toorun `bash deploy.sh` as hello custom deployment script.</span></span>
> - <span data-ttu-id="b806e-250">`deploy.sh`-hello script di distribuzione personalizzati.</span><span class="sxs-lookup"><span data-stu-id="b806e-250">`deploy.sh` - hello custom deployment script.</span></span> <span data-ttu-id="b806e-251">Se si esamina il file hello, si noterà che l'esecuzione `php composer.phar install` dopo `npm install`.</span><span class="sxs-lookup"><span data-stu-id="b806e-251">If you review hello file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="b806e-252">`composer.phar`-gestione di pacchetti hello Composer.</span><span class="sxs-lookup"><span data-stu-id="b806e-252">`composer.phar` - hello Composer package manager.</span></span>
>
> <span data-ttu-id="b806e-253">È possibile utilizzare questo approccio tooadd qualsiasi tooApp di distribuzione basati su Git tooyour di passaggio del servizio.</span><span class="sxs-lookup"><span data-stu-id="b806e-253">You can use this approach tooadd any step tooyour Git-based deployment tooApp Service.</span></span> <span data-ttu-id="b806e-254">Per altre informazioni, vedere [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script) (Script di distribuzione personalizzata).</span><span class="sxs-lookup"><span data-stu-id="b806e-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-toohello-azure-web-app"></a><span data-ttu-id="b806e-255">Sfoglia toohello Azure web app</span><span class="sxs-lookup"><span data-stu-id="b806e-255">Browse toohello Azure web app</span></span>

<span data-ttu-id="b806e-256">Sfoglia troppo`http://<app_name>.azurewebsites.net` e aggiungere alcune attività toohello elenco.</span><span class="sxs-lookup"><span data-stu-id="b806e-256">Browse too`http://<app_name>.azurewebsites.net` and add a few tasks toohello list.</span></span>

![App PHP in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="b806e-258">L'app PHP basata su dati è in esecuzione nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="b806e-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="b806e-259">Aggiornare il modello in locale e rieseguire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="b806e-259">Update model locally and redeploy</span></span>

<span data-ttu-id="b806e-260">In questo passaggio, si apportata toohello una semplice modifica `task` modello di dati e hello webapp e quindi pubblicare tooAzure aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-260">In this step, you make a simple change toohello `task` data model and hello webapp, and then publish hello update tooAzure.</span></span>

<span data-ttu-id="b806e-261">Scenario di attività hello, modificare un'applicazione hello in modo che è possibile contrassegnare un'attività come completata.</span><span class="sxs-lookup"><span data-stu-id="b806e-261">For hello tasks scenario, you modify hello application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="b806e-262">Aggiungere una colonna</span><span class="sxs-lookup"><span data-stu-id="b806e-262">Add a column</span></span>

<span data-ttu-id="b806e-263">In hello terminal, passare toohello radice del repository Git hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-263">In hello terminal, navigate toohello root of hello Git repository.</span></span>

<span data-ttu-id="b806e-264">Generare una nuova migrazione di database per hello `tasks` tabella:</span><span class="sxs-lookup"><span data-stu-id="b806e-264">Generate a new database migration for hello `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="b806e-265">Questo comando Mostra hello nome del file di migrazione hello che viene generato.</span><span class="sxs-lookup"><span data-stu-id="b806e-265">This command shows you hello name of hello migration file that's generated.</span></span> <span data-ttu-id="b806e-266">Trovare il file in _database/migrations_ e aprirlo.</span><span class="sxs-lookup"><span data-stu-id="b806e-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="b806e-267">Sostituire hello `up` metodo con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="b806e-267">Replace hello `up` method with hello following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="b806e-268">Hello precedente consente di aggiungere una colonna booleana hello `tasks` tabella denominata `complete`.</span><span class="sxs-lookup"><span data-stu-id="b806e-268">hello preceding code adds a boolean column in hello `tasks` table called `complete`.</span></span>

<span data-ttu-id="b806e-269">Sostituire hello `down` metodo con hello seguente codice per l'azione di rollback hello:</span><span class="sxs-lookup"><span data-stu-id="b806e-269">Replace hello `down` method with hello following code for hello rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="b806e-270">In hello terminal, eseguire le modifiche hello Laravel del database le migrazioni toomake nel database locale hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-270">In hello terminal, run Laravel database migrations toomake hello change in hello local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="b806e-271">In base a hello [convenzione di denominazione Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), modello hello `Task` (vedere _app/Task.php_) viene eseguito il mapping toohello `tasks` tabella per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="b806e-271">Based on hello [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), hello model `Task` (see _app/Task.php_) maps toohello `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="b806e-272">Aggiornare la logica dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="b806e-272">Update application logic</span></span>

<span data-ttu-id="b806e-273">Aprire hello *routes/web.php* file.</span><span class="sxs-lookup"><span data-stu-id="b806e-273">Open hello *routes/web.php* file.</span></span> <span data-ttu-id="b806e-274">un'applicazione Hello definisce le route e qui la logica di business.</span><span class="sxs-lookup"><span data-stu-id="b806e-274">hello application defines its routes and business logic here.</span></span>

<span data-ttu-id="b806e-275">Alla fine di hello del file hello, aggiungere una route con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="b806e-275">At hello end of hello file, add a route with hello following code:</span></span>

```php
/**
 * Toggle Task completeness
 */
Route::post('/task/{id}', function ($id) {
    error_log('INFO: post /task/'.$id);
    $task = Task::findOrFail($id);

    $task->complete = !$task->complete;
    $task->save();

    return redirect('/');
});
```

<span data-ttu-id="b806e-276">Hello codice precedente crea un modello di dati semplice aggiornamento toohello attivando e disattivando il valore di hello di `complete`.</span><span class="sxs-lookup"><span data-stu-id="b806e-276">hello preceding code makes a simple update toohello data model by toggling hello value of `complete`.</span></span>

### <a name="update-hello-view"></a><span data-ttu-id="b806e-277">Aggiornare la vista hello</span><span class="sxs-lookup"><span data-stu-id="b806e-277">Update hello view</span></span>

<span data-ttu-id="b806e-278">Aprire hello *resources/views/tasks.blade.php* file.</span><span class="sxs-lookup"><span data-stu-id="b806e-278">Open hello *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="b806e-279">Trovare hello `<tr>` tag di apertura e sostituirlo con:</span><span class="sxs-lookup"><span data-stu-id="b806e-279">Find hello `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="b806e-280">Hello precedente codice colore riga hello di modifiche a seconda se l'attività hello è stata completata.</span><span class="sxs-lookup"><span data-stu-id="b806e-280">hello preceding code changes hello row color depending on whether hello task is complete.</span></span>

<span data-ttu-id="b806e-281">Nella riga successiva hello, è necessario hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="b806e-281">In hello next line, you have hello following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="b806e-282">Sostituire l'intera riga hello con hello seguente codice:</span><span class="sxs-lookup"><span data-stu-id="b806e-282">Replace hello entire line with hello following code:</span></span>

```html
<td>
    <form action="{{ url('task/'.$task->id) }}" method="POST">
        {{ csrf_field() }}

        <button type="submit" class="btn btn-xs">
            <i class="fa {{$task->complete ? 'fa-check-square-o' : 'fa-square-o'}}"></i>
        </button>
        {{ $task->name }}
    </form>
</td>
```

<span data-ttu-id="b806e-283">Hello codice precedente aggiunge pulsante submit hello che fa riferimento a route hello è definito in precedenza.</span><span class="sxs-lookup"><span data-stu-id="b806e-283">hello preceding code adds hello submit button that references hello route that you defined earlier.</span></span>

### <a name="test-hello-changes-locally"></a><span data-ttu-id="b806e-284">Testare le modifiche di hello in locale</span><span class="sxs-lookup"><span data-stu-id="b806e-284">Test hello changes locally</span></span>

<span data-ttu-id="b806e-285">Dalla directory radice di hello del repository Git hello, eseguire il server di sviluppo hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-285">From hello root directory of hello Git repository, run hello development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="b806e-286">hello toosee modifica dello stato delle attività, passare troppo`http://localhost:8000` e hello selezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="b806e-286">toosee hello task status change, navigate too`http://localhost:8000` and select hello checkbox.</span></span>

![Casella di controllo aggiunte tootask](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="b806e-288">Digitare toostop PHP, `Ctrl + C` in hello terminal.</span><span class="sxs-lookup"><span data-stu-id="b806e-288">toostop PHP, type `Ctrl + C` in hello terminal.</span></span>

### <a name="publish-changes-tooazure"></a><span data-ttu-id="b806e-289">Pubblicare le modifiche tooAzure</span><span class="sxs-lookup"><span data-stu-id="b806e-289">Publish changes tooAzure</span></span>

<span data-ttu-id="b806e-290">In hello terminal, eseguire le migrazioni database Laravel con hello produzione connessione stringa toomake hello modifica hello il database di Azure.</span><span class="sxs-lookup"><span data-stu-id="b806e-290">In hello terminal, run Laravel database migrations with hello production connection string toomake hello change in hello Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="b806e-291">Eseguire il commit di tutte le modifiche di hello in Git e quindi push tooAzure modifiche di codice hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-291">Commit all hello changes in Git, and then push hello code changes tooAzure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="b806e-292">Una volta hello `git push` è completo, passare toohello Azure web app e prova hello nuove funzionalità.</span><span class="sxs-lookup"><span data-stu-id="b806e-292">Once hello `git push` is complete, navigate toohello Azure web app and test hello new functionality.</span></span>

![Le modifiche apportate al modello e il database pubblicato tooAzure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="b806e-294">Se si aggiungono tutte le attività, vengono mantenuti nel database di hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-294">If you added any tasks, they are retained in hello database.</span></span> <span data-ttu-id="b806e-295">Schema di data toohello aggiornamenti intatti i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="b806e-295">Updates toohello data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="b806e-296">Eseguire lo streaming dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="b806e-296">Stream diagnostic logs</span></span>

<span data-ttu-id="b806e-297">Mentre è in esecuzione in Azure App Service hello applicazione PHP, è possibile ottenere hello console registri reindirizzato tooyour terminal.</span><span class="sxs-lookup"><span data-stu-id="b806e-297">While hello PHP application runs in Azure App Service, you can get hello console logs piped tooyour terminal.</span></span> <span data-ttu-id="b806e-298">In questo modo, è possibile ottenere hello stessi messaggi di diagnostica toohelp si esegue il debug di errori dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="b806e-298">That way, you can get hello same diagnostic messages toohelp you debug application errors.</span></span>

<span data-ttu-id="b806e-299">log toostart streaming, usare hello [della parte finale del log di az webapp](/cli/azure/webapp/log#tail) comando.</span><span class="sxs-lookup"><span data-stu-id="b806e-299">toostart log streaming, use hello [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="b806e-300">Una volta avviato il flusso di log, aggiornare l'app web di Azure hello in hello browser tooget traffico web.</span><span class="sxs-lookup"><span data-stu-id="b806e-300">Once log streaming has started, refresh hello Azure web app in hello browser tooget some web traffic.</span></span> <span data-ttu-id="b806e-301">È ora possibile visualizzare terminal toohello inoltrato tramite pipe i registri di console.</span><span class="sxs-lookup"><span data-stu-id="b806e-301">You can now see console logs piped toohello terminal.</span></span> <span data-ttu-id="b806e-302">Se i log di console non sono immediatamente visibili, controllare nuovamente dopo 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="b806e-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="b806e-303">log toostop streaming in qualsiasi momento, tipo `Ctrl` + `C`.</span><span class="sxs-lookup"><span data-stu-id="b806e-303">toostop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="b806e-304">Un'applicazione PHP può utilizzare standard di hello [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span><span class="sxs-lookup"><span data-stu-id="b806e-304">A PHP application can use hello standard [error_log()](http://php.net/manual/function.error-log.php) toooutput toohello console.</span></span> <span data-ttu-id="b806e-305">applicazione di esempio Hello viene utilizzato questo approccio in _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="b806e-305">hello sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="b806e-306">Come un framework web [Laravel Usa Monolog](https://laravel.com/docs/5.4/errors) come provider di log hello.</span><span class="sxs-lookup"><span data-stu-id="b806e-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as hello logging provider.</span></span> <span data-ttu-id="b806e-307">toosee come tooget Monolog toooutput messaggi toohello console, vedere [PHP: modalità toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span><span class="sxs-lookup"><span data-stu-id="b806e-307">toosee how tooget Monolog toooutput messages toohello console, see [PHP: How toouse monolog toolog tooconsole (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-hello-azure-web-app"></a><span data-ttu-id="b806e-308">Gestire app web di Azure hello</span><span class="sxs-lookup"><span data-stu-id="b806e-308">Manage hello Azure web app</span></span>

<span data-ttu-id="b806e-309">Passare toohello [portale di Azure](https://portal.azure.com) toomanage hello web app è stato creato.</span><span class="sxs-lookup"><span data-stu-id="b806e-309">Go toohello [Azure portal](https://portal.azure.com) toomanage hello web app you created.</span></span>

<span data-ttu-id="b806e-310">Scegliere dal menu a sinistra hello **servizi App**, quindi fare clic su nome hello dell'app web di Azure.</span><span class="sxs-lookup"><span data-stu-id="b806e-310">From hello left menu, click **App Services**, and then click hello name of your Azure web app.</span></span>

![Spostamento del portale tooAzure web app](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="b806e-312">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="b806e-312">You see your web app's Overview page.</span></span> <span data-ttu-id="b806e-313">Nella pagina è possibile eseguire attività di gestione di base come l'arresto, l'avvio, il riavvio e l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="b806e-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="b806e-314">menu a sinistra di Hello fornisce le pagine di configurazione app.</span><span class="sxs-lookup"><span data-stu-id="b806e-314">hello left menu provides pages for configuring your app.</span></span>

![Pagina del servizio app nel portale di Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="b806e-316">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="b806e-316">Next steps</span></span>

<span data-ttu-id="b806e-317">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="b806e-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="b806e-318">Creare un database MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="b806e-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="b806e-319">Connettersi a un tooMySQL app PHP</span><span class="sxs-lookup"><span data-stu-id="b806e-319">Connect a PHP app tooMySQL</span></span>
> * <span data-ttu-id="b806e-320">Distribuire hello app tooAzure</span><span class="sxs-lookup"><span data-stu-id="b806e-320">Deploy hello app tooAzure</span></span>
> * <span data-ttu-id="b806e-321">Modello di dati hello e ridistribuire l'applicazione hello</span><span class="sxs-lookup"><span data-stu-id="b806e-321">Update hello data model and redeploy hello app</span></span>
> * <span data-ttu-id="b806e-322">Eseguire lo streaming dei log di diagnostica in Azure</span><span class="sxs-lookup"><span data-stu-id="b806e-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="b806e-323">Gestire app hello in hello portale di Azure</span><span class="sxs-lookup"><span data-stu-id="b806e-323">Manage hello app in hello Azure portal</span></span>

<span data-ttu-id="b806e-324">Spostare toolearn esercitazione successiva toohello come toomap un DNS personalizzato denominati tooa web app.</span><span class="sxs-lookup"><span data-stu-id="b806e-324">Advance toohello next tutorial toolearn how toomap a custom DNS name tooa web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b806e-325">Eseguire il mapping di un esistente personalizzato DNS nome tooAzure App Web</span><span class="sxs-lookup"><span data-stu-id="b806e-325">Map an existing custom DNS name tooAzure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
