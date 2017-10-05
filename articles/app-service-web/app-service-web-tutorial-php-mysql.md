---
title: Creare un'app Web PHP e MySQL in Azure | Microsoft Docs
description: "Informazioni su come ottenere un'app PHP che è possibile usare in Azure con connessione a un database MySQL in Azure."
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
ms.openlocfilehash: 6e8d8962180f7534b0b9074f03ecc8ea431ae1a4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="build-a-php-and-mysql-web-app-in-azure"></a><span data-ttu-id="94f6a-103">Creare un'app Web PHP e MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-103">Build a PHP and MySQL web app in Azure</span></span>

<span data-ttu-id="94f6a-104">Le [app Web di Azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) forniscono un servizio di hosting Web ad alta scalabilità e con funzioni di auto-correzione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-104">[Azure Web Apps](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) provides a highly scalable, self-patching web hosting service.</span></span> <span data-ttu-id="94f6a-105">Questa esercitazione illustra come creare un'app Web PHP in Azure e connetterla a un database MySQL.</span><span class="sxs-lookup"><span data-stu-id="94f6a-105">This tutorial shows how to create a PHP web app in Azure and connect it to a MySQL database.</span></span> <span data-ttu-id="94f6a-106">Al termine, sarà disponibile un'app [Laravel](https://laravel.com/) in esecuzione nelle app Web del servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="94f6a-106">When you're finished, you'll have a [Laravel](https://laravel.com/) app running on Azure App Service Web Apps.</span></span>

![App PHP in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="94f6a-108">In questa esercitazione si apprenderà come:</span><span class="sxs-lookup"><span data-stu-id="94f6a-108">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94f6a-109">Creare un database MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-109">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="94f6a-110">Connettere un'app PHP a MySQL</span><span class="sxs-lookup"><span data-stu-id="94f6a-110">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="94f6a-111">Distribuire l'app in Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-111">Deploy the app to Azure</span></span>
> * <span data-ttu-id="94f6a-112">Aggiornare il modello di dati e ridistribuire l'app</span><span class="sxs-lookup"><span data-stu-id="94f6a-112">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="94f6a-113">Eseguire lo streaming dei log di diagnostica in Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-113">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="94f6a-114">Gestire l'app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-114">Manage the app in the Azure portal</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94f6a-115">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="94f6a-115">Prerequisites</span></span>

<span data-ttu-id="94f6a-116">Per completare questa esercitazione:</span><span class="sxs-lookup"><span data-stu-id="94f6a-116">To complete this tutorial:</span></span>

* [<span data-ttu-id="94f6a-117">Installare Git</span><span class="sxs-lookup"><span data-stu-id="94f6a-117">Install Git</span></span>](https://git-scm.com/)
* [<span data-ttu-id="94f6a-118">Installare PHP 5.6.4 o versione successiva</span><span class="sxs-lookup"><span data-stu-id="94f6a-118">Install PHP 5.6.4 or above</span></span>](http://php.net/downloads.php)
* [<span data-ttu-id="94f6a-119">Installare Composer</span><span class="sxs-lookup"><span data-stu-id="94f6a-119">Install Composer</span></span>](https://getcomposer.org/doc/00-intro.md)
* <span data-ttu-id="94f6a-120">Abilitare le estensioni PHP seguenti necessarie per Laravel: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span><span class="sxs-lookup"><span data-stu-id="94f6a-120">Enable the following PHP extensions Laravel needs: OpenSSL, PDO-MySQL, Mbstring, Tokenizer, XML</span></span>
* [<span data-ttu-id="94f6a-121">Installare e avviare MySQL</span><span class="sxs-lookup"><span data-stu-id="94f6a-121">Install and start MySQL</span></span>](https://dev.mysql.com/doc/refman/5.7/en/installing.html) 

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="prepare-local-mysql"></a><span data-ttu-id="94f6a-122">Preparare MySQL in locale</span><span class="sxs-lookup"><span data-stu-id="94f6a-122">Prepare local MySQL</span></span>

<span data-ttu-id="94f6a-123">In questo passaggio, si crea un database nel server locale di MySQL da usare in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-123">In this step, you create a database in your local MySQL server for your use in this tutorial.</span></span>

### <a name="connect-to-local-mysql-server"></a><span data-ttu-id="94f6a-124">Connettersi al server MySQL locale</span><span class="sxs-lookup"><span data-stu-id="94f6a-124">Connect to local MySQL server</span></span>

<span data-ttu-id="94f6a-125">In una finestra terminale connettersi al server MySQL locale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-125">In a terminal window, connect to your local MySQL server.</span></span> <span data-ttu-id="94f6a-126">È possibile usare questa finestra del terminale per eseguire tutti i comandi presenti in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-126">You can use this terminal window to run all the commands in this tutorial.</span></span>

```bash
mysql -u root -p
```

<span data-ttu-id="94f6a-127">Se viene richiesto di immettere una password, immettere la password per l'account `root`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-127">If you're prompted for a password, enter the password for the `root` account.</span></span> <span data-ttu-id="94f6a-128">Se non si ricorda la password dell'account radice, vedere [MySQL: procedura per reimpostare la password radice](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span><span class="sxs-lookup"><span data-stu-id="94f6a-128">If you don't remember your root account password, see [MySQL: How to Reset the Root Password](https://dev.mysql.com/doc/refman/5.7/en/resetting-permissions.html).</span></span>

<span data-ttu-id="94f6a-129">Se il comando viene eseguito correttamente, il server MySQL è in esecuzione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-129">If your command runs successfully, then your MySQL server is running.</span></span> <span data-ttu-id="94f6a-130">In caso contrario, assicurarsi che il server MySQL locale sia stato avviato seguendo la [procedura successiva all'installazione di MySQL](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span><span class="sxs-lookup"><span data-stu-id="94f6a-130">If not, make sure that your local MySQL server is started by following the [MySQL post-installation steps](https://dev.mysql.com/doc/refman/5.7/en/postinstallation.html).</span></span>

### <a name="create-a-database-locally"></a><span data-ttu-id="94f6a-131">Creare un database in locale</span><span class="sxs-lookup"><span data-stu-id="94f6a-131">Create a database locally</span></span>

<span data-ttu-id="94f6a-132">Al prompt `mysql` creare un database.</span><span class="sxs-lookup"><span data-stu-id="94f6a-132">At the `mysql` prompt, create a database.</span></span>

```sql 
CREATE DATABASE sampledb;
```

<span data-ttu-id="94f6a-133">Chiudere la connessione al server digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-133">Exit your server connection by typing `quit`.</span></span>

```sql
quit
```

<a name="step2"></a>

## <a name="create-a-php-app-locally"></a><span data-ttu-id="94f6a-134">Creare un'app PHP in locale</span><span class="sxs-lookup"><span data-stu-id="94f6a-134">Create a PHP app locally</span></span>
<span data-ttu-id="94f6a-135">In questo passaggio si ottiene un'applicazione di esempio Laravel, se ne configurare la connessione al database e la si esegue in locale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-135">In this step, you get a Laravel sample application, configure its database connection, and run it locally.</span></span> 

### <a name="clone-the-sample"></a><span data-ttu-id="94f6a-136">Clonare l'esempio</span><span class="sxs-lookup"><span data-stu-id="94f6a-136">Clone the sample</span></span>

<span data-ttu-id="94f6a-137">Nella finestra del terminale usare il comando `cd` per passare a una directory di lavoro.</span><span class="sxs-lookup"><span data-stu-id="94f6a-137">In the terminal window, `cd` to a working directory.</span></span>

<span data-ttu-id="94f6a-138">Eseguire il comando seguente per clonare l'archivio di esempio.</span><span class="sxs-lookup"><span data-stu-id="94f6a-138">Run the following command to clone the sample repository.</span></span>

```bash
git clone https://github.com/Azure-Samples/laravel-tasks
```

<span data-ttu-id="94f6a-139">Eseguire `cd` nella directory clonata.</span><span class="sxs-lookup"><span data-stu-id="94f6a-139">`cd` to your cloned directory.</span></span>
<span data-ttu-id="94f6a-140">Installare i pacchetti necessari.</span><span class="sxs-lookup"><span data-stu-id="94f6a-140">Install the required packages.</span></span>

```bash
cd laravel-tasks
composer install
```

### <a name="configure-mysql-connection"></a><span data-ttu-id="94f6a-141">Configurare la connessione di MySQL</span><span class="sxs-lookup"><span data-stu-id="94f6a-141">Configure MySQL connection</span></span>

<span data-ttu-id="94f6a-142">Nella radice del repository creare un file denominato *.env*.</span><span class="sxs-lookup"><span data-stu-id="94f6a-142">In the repository root, create a file named *.env*.</span></span> <span data-ttu-id="94f6a-143">Copiare le variabili seguenti nel file *.env*.</span><span class="sxs-lookup"><span data-stu-id="94f6a-143">Copy the following variables into the *.env* file.</span></span> <span data-ttu-id="94f6a-144">Sostituire il segnaposto _&lt;root_password>_ con la password dell'utente ROOT MySQL.</span><span class="sxs-lookup"><span data-stu-id="94f6a-144">Replace the _&lt;root_password>_ placeholder with the MySQL root user's password.</span></span>

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

<span data-ttu-id="94f6a-145">Per informazioni su come viene usato il file _.env_ da Laravel, vedere [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration) (Configurazione dell'ambiente Laravel).</span><span class="sxs-lookup"><span data-stu-id="94f6a-145">For information on how Laravel uses the _.env_ file, see [Laravel Environment Configuration](https://laravel.com/docs/5.4/configuration#environment-configuration).</span></span>

### <a name="run-the-sample-locally"></a><span data-ttu-id="94f6a-146">Eseguire l'esempio in locale</span><span class="sxs-lookup"><span data-stu-id="94f6a-146">Run the sample locally</span></span>

<span data-ttu-id="94f6a-147">Eseguire le [migrazioni del database di Laravel](https://laravel.com/docs/5.4/migrations) per creare le tabelle necessarie all'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-147">Run [Laravel database migrations](https://laravel.com/docs/5.4/migrations) to create the tables the application needs.</span></span> <span data-ttu-id="94f6a-148">Per visualizzare le tabelle create nelle migrazioni, esaminare la directory _database/migrations_ nel repository Git.</span><span class="sxs-lookup"><span data-stu-id="94f6a-148">To see which tables are created in the migrations, look in the _database/migrations_ directory in the Git repository.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="94f6a-149">Generare una nuova chiave per l'applicazione Laravel.</span><span class="sxs-lookup"><span data-stu-id="94f6a-149">Generate a new Laravel application key.</span></span>

```bash
php artisan key:generate
```

<span data-ttu-id="94f6a-150">Eseguire l'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-150">Run the application.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="94f6a-151">Andare a `http://localhost:8000` in un browser.</span><span class="sxs-lookup"><span data-stu-id="94f6a-151">Navigate to `http://localhost:8000` in a browser.</span></span> <span data-ttu-id="94f6a-152">Nella pagina aggiungere alcune attività.</span><span class="sxs-lookup"><span data-stu-id="94f6a-152">Add a few tasks in the page.</span></span>

![PHP si connette correttamente a MySQL](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="94f6a-154">Per arrestare PHP, digitare `Ctrl + C` nel terminale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-154">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

## <a name="create-mysql-in-azure"></a><span data-ttu-id="94f6a-155">Creare MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-155">Create MySQL in Azure</span></span>

<span data-ttu-id="94f6a-156">In questo passaggio viene creato un database MySQL nel [database di Azure per MySQL (anteprima)](/azure/mysql).</span><span class="sxs-lookup"><span data-stu-id="94f6a-156">In this step, you create a MySQL database in [Azure Database for MySQL (Preview)](/azure/mysql).</span></span> <span data-ttu-id="94f6a-157">Successivamente viene configurata l'applicazione PHP per la connessione al database.</span><span class="sxs-lookup"><span data-stu-id="94f6a-157">Later, you configure the PHP application to connect to this database.</span></span>

### <a name="create-a-resource-group"></a><span data-ttu-id="94f6a-158">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="94f6a-158">Create a resource group</span></span>

[!INCLUDE [Create resource group](../../includes/app-service-web-create-resource-group-no-h.md)] 

### <a name="create-a-mysql-server"></a><span data-ttu-id="94f6a-159">Creare un server MySQL</span><span class="sxs-lookup"><span data-stu-id="94f6a-159">Create a MySQL server</span></span>

<span data-ttu-id="94f6a-160">Creare un server nel database di Azure per MySQL (anteprima) con il comando [az mysql server create](/cli/azure/mysql/server#create).</span><span class="sxs-lookup"><span data-stu-id="94f6a-160">Create a server in Azure Database for MySQL (Preview) with the [az mysql server create](/cli/azure/mysql/server#create) command.</span></span>

<span data-ttu-id="94f6a-161">Nel comando seguente sostituire il segnaposto _&lt;mysql_server_name>_ con il nome del server MySQL (i caratteri validi sono `a-z`, `0-9` e `-`).</span><span class="sxs-lookup"><span data-stu-id="94f6a-161">In the following command, substitute your MySQL server name where you see the _&lt;mysql_server_name>_ placeholder (valid characters are `a-z`, `0-9`, and `-`).</span></span> <span data-ttu-id="94f6a-162">Poiché questo nome fa parte del nome host del server MySQL (`<mysql_server_name>.database.windows.net`) è necessario che sia univoco a livello globale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-162">This name is part of the MySQL server's hostname  (`<mysql_server_name>.database.windows.net`), it needs to be globally unique.</span></span>

```azurecli-interactive
az mysql server create \
    --name <mysql_server_name> \
    --resource-group myResourceGroup \
    --location "North Europe" \
    --admin-user adminuser \
    --admin-password MySQLAzure2017
```

<span data-ttu-id="94f6a-163">Al termine della creazione del server MySQL, l'interfaccia della riga di comando di Azure mostra informazioni simili all'esempio seguente:</span><span class="sxs-lookup"><span data-stu-id="94f6a-163">When the MySQL server is created, the Azure CLI shows information similar to the following example:</span></span>

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

### <a name="configure-server-firewall"></a><span data-ttu-id="94f6a-164">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="94f6a-164">Configure server firewall</span></span>

<span data-ttu-id="94f6a-165">Creare una regola del firewall per il server MySQL per consentire le connessioni client tramite il comando [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="94f6a-165">Create a firewall rule for your MySQL server to allow client connections by using the [az mysql server firewall-rule create](/cli/azure/mysql/server/firewall-rule#create) command.</span></span>

```azurecli-interactive
az mysql server firewall-rule create \
    --name allIPs \
    --server <mysql_server_name> \
    --resource-group myResourceGroup \
    --start-ip-address 0.0.0.0 \
    --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="94f6a-166">Database di Azure per MySQL (anteprima) attualmente non limita le connessioni solo ai servizi di Azure.</span><span class="sxs-lookup"><span data-stu-id="94f6a-166">Azure Database for MySQL (Preview) doesn't currently limit connections only to Azure services.</span></span> <span data-ttu-id="94f6a-167">Poiché gli indirizzi IP in Azure sono assegnati dinamicamente, è consigliabile abilitare tutti gli indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="94f6a-167">As IP addresses in Azure are dynamically assigned, it is better to enable all IP addresses.</span></span> <span data-ttu-id="94f6a-168">Il servizio è disponibile in anteprima.</span><span class="sxs-lookup"><span data-stu-id="94f6a-168">The service is in preview.</span></span> <span data-ttu-id="94f6a-169">Verranno resi disponibili metodi migliori per la protezione del database.</span><span class="sxs-lookup"><span data-stu-id="94f6a-169">Better methods for securing your database are planned.</span></span>
>
>

### <a name="connect-to-production-mysql-server-locally"></a><span data-ttu-id="94f6a-170">Connettersi al server MySQL di produzione in locale</span><span class="sxs-lookup"><span data-stu-id="94f6a-170">Connect to production MySQL server locally</span></span>

<span data-ttu-id="94f6a-171">Nella finestra terminale connettersi al server MySQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="94f6a-171">In the terminal window, connect to the MySQL server in Azure.</span></span> <span data-ttu-id="94f6a-172">Usare il valore specificato in precedenza per _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="94f6a-172">Use the value you specified previously for _&lt;mysql_server_name>_.</span></span>

```bash
mysql -u adminuser@<mysql_server_name> -h <mysql_server_name>.database.windows.net -P 3306 -p
```

<span data-ttu-id="94f6a-173">Quando viene richiesto di immettere una password, usare _$tr0ngPa$w0rd!_, la password specificata al momento della creazione del database.</span><span class="sxs-lookup"><span data-stu-id="94f6a-173">When prompted for a password, use _$tr0ngPa$w0rd!_, which you specified when you created the database.</span></span>

### <a name="create-a-production-database"></a><span data-ttu-id="94f6a-174">Creare un database di produzione</span><span class="sxs-lookup"><span data-stu-id="94f6a-174">Create a production database</span></span>

<span data-ttu-id="94f6a-175">Al prompt `mysql` creare un database.</span><span class="sxs-lookup"><span data-stu-id="94f6a-175">At the `mysql` prompt, create a database.</span></span>

```sql
CREATE DATABASE sampledb;
```

### <a name="create-a-user-with-permissions"></a><span data-ttu-id="94f6a-176">Creare un utente con autorizzazioni</span><span class="sxs-lookup"><span data-stu-id="94f6a-176">Create a user with permissions</span></span>

<span data-ttu-id="94f6a-177">Creare un utente di database denominato _phpappuser_ e assegnare all'utente tutti i privilegi per il database `sampledb`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-177">Create a database user called _phpappuser_ and give it all privileges in the `sampledb` database.</span></span>

```sql
CREATE USER 'phpappuser' IDENTIFIED BY 'MySQLAzure2017'; 
GRANT ALL PRIVILEGES ON sampledb.* TO 'phpappuser';
```

<span data-ttu-id="94f6a-178">Chiudere la connessione al server digitando `quit`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-178">Exit the server connection by typing `quit`.</span></span>

```sql
quit
```

## <a name="connect-app-to-azure-mysql"></a><span data-ttu-id="94f6a-179">Connettere l'app a MySQL di Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-179">Connect app to Azure MySQL</span></span>

<span data-ttu-id="94f6a-180">In questo passaggio l'applicazione PHP viene connessa al database MySQL creato in Database di Azure per MySQL (anteprima).</span><span class="sxs-lookup"><span data-stu-id="94f6a-180">In this step, you connect the PHP application to the MySQL database you created in Azure Database for MySQL (Preview).</span></span>

<a name="devconfig"></a>

### <a name="configure-the-database-connection"></a><span data-ttu-id="94f6a-181">Configurare la connessione al database</span><span class="sxs-lookup"><span data-stu-id="94f6a-181">Configure the database connection</span></span>

<span data-ttu-id="94f6a-182">Nella radice del repository creare un file _.env.production_ e copiare le variabili seguenti nel file.</span><span class="sxs-lookup"><span data-stu-id="94f6a-182">In the repository root, create an _.env.production_ file and copy the following variables into it.</span></span> <span data-ttu-id="94f6a-183">Sostituire il segnaposto _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="94f6a-183">Replace the placeholder _&lt;mysql_server_name>_.</span></span>

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

<span data-ttu-id="94f6a-184">Salvare le modifiche.</span><span class="sxs-lookup"><span data-stu-id="94f6a-184">Save the changes.</span></span>

> [!TIP]
> <span data-ttu-id="94f6a-185">Per proteggere le informazioni di connessione MySQL, il file è già escluso dal repository Git (vedere _.gitignore_ nella radice del repository).</span><span class="sxs-lookup"><span data-stu-id="94f6a-185">To secure your MySQL connection information, this file is already excluded from the Git repository (See _.gitignore_ in the repository root).</span></span> <span data-ttu-id="94f6a-186">Successivamente verrà illustrato come configurare le variabili di ambiente nel servizio app per connettere il database in Database di Azure per MySQL (anteprima).</span><span class="sxs-lookup"><span data-stu-id="94f6a-186">Later, you learn how to configure environment variables in App Service to connect to your database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="94f6a-187">Con le variabili di ambiente non è necessario il file *.env* nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="94f6a-187">With environment variables, you don't need the *.env* file in App Service.</span></span>
>

### <a name="configure-ssl-certificate"></a><span data-ttu-id="94f6a-188">Configurare il certificato SSL</span><span class="sxs-lookup"><span data-stu-id="94f6a-188">Configure SSL certificate</span></span>

<span data-ttu-id="94f6a-189">Per impostazione predefinita, Database di Azure per MySQL impone le connessioni SSL dai client.</span><span class="sxs-lookup"><span data-stu-id="94f6a-189">By default, Azure Database for MySQL enforces SSL connections from clients.</span></span> <span data-ttu-id="94f6a-190">Per connettersi al database MySQL in Azure è necessario usare un certificato SSL _.pem_.</span><span class="sxs-lookup"><span data-stu-id="94f6a-190">To connect to your MySQL database in Azure, you must use a _.pem_ SSL certificate.</span></span>

<span data-ttu-id="94f6a-191">Aprire _config/database.php_ e aggiungere i parametri _sslmode_ e _options_ a `connections.mysql`, come illustrato nel codice seguente.</span><span class="sxs-lookup"><span data-stu-id="94f6a-191">Open _config/database.php_ and add the _sslmode_ and _options_ parameters to `connections.mysql`, as shown in the following code.</span></span>

```php
'mysql' => [
    ...
    'sslmode' => env('DB_SSLMODE', 'prefer'),
    'options' => (env('MYSQL_SSL')) ? [
        PDO::MYSQL_ATTR_SSL_KEY    => '/ssl/certificate.pem', 
    ] : []
],
```

<span data-ttu-id="94f6a-192">Per informazioni su come generare il file _certificate.pem_, vedere [Configurare la connettività SSL nell'applicazione per la connessione sicura a Database di Azure per MySQL](../mysql/howto-configure-ssl.md).</span><span class="sxs-lookup"><span data-stu-id="94f6a-192">To learn how to generate this _certificate.pem_, see [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](../mysql/howto-configure-ssl.md).</span></span>

> [!TIP]
> <span data-ttu-id="94f6a-193">Il percorso _/ssl/certificate.pem_ punta a un file _certificate.pem_ esistente nel repository Git.</span><span class="sxs-lookup"><span data-stu-id="94f6a-193">The path _/ssl/certificate.pem_ points to an existing _certificate.pem_ file in the Git repository.</span></span> <span data-ttu-id="94f6a-194">Il file è già incluso per ragioni di praticità in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-194">This file is provided for convenience in this tutorial.</span></span> <span data-ttu-id="94f6a-195">È consigliabile non eseguire il commit dei certificati _.pem_ nel controllo del codice sorgente.</span><span class="sxs-lookup"><span data-stu-id="94f6a-195">For best practice, you should not commit your _.pem_ certificates into source control.</span></span> 
>

### <a name="test-the-application-locally"></a><span data-ttu-id="94f6a-196">Testare l'applicazione in locale</span><span class="sxs-lookup"><span data-stu-id="94f6a-196">Test the application locally</span></span>

<span data-ttu-id="94f6a-197">Eseguire le migrazioni del database di Laravel con _.env.production_ come file dell'ambiente per creare le tabelle nel proprio database MySQL nel database di Azure per MySQL (anteprima).</span><span class="sxs-lookup"><span data-stu-id="94f6a-197">Run Laravel database migrations with _.env.production_ as the environment file to create the tables in your MySQL database in Azure Database for MySQL (Preview).</span></span> <span data-ttu-id="94f6a-198">Tenere presente che _. env.production_ include le informazioni di connessione al database MySQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="94f6a-198">Remember that _.env.production_ has the connection information to your MySQL database in Azure.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="94f6a-199">_.env.production_ non dispone ancora di una chiave applicazione valida.</span><span class="sxs-lookup"><span data-stu-id="94f6a-199">_.env.production_ doesn't have a valid application key yet.</span></span> <span data-ttu-id="94f6a-200">Generarne una nuova nel terminale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-200">Generate a new one for it in the terminal.</span></span>

```bash
php artisan key:generate --env=production --force
```

<span data-ttu-id="94f6a-201">Eseguire l'applicazione di esempio con _.env.production_ come file dell'ambiente.</span><span class="sxs-lookup"><span data-stu-id="94f6a-201">Run the sample application with _.env.production_ as the environment file.</span></span>

```bash
php artisan serve --env=production
```

<span data-ttu-id="94f6a-202">Accedere a `http://localhost:8000`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-202">Navigate to `http://localhost:8000`.</span></span> <span data-ttu-id="94f6a-203">Se la pagina viene caricata senza errori, l'applicazione PHP si connette al database MySQL in Azure.</span><span class="sxs-lookup"><span data-stu-id="94f6a-203">If the page loads without errors, the PHP application is connecting to the MySQL database in Azure.</span></span>

<span data-ttu-id="94f6a-204">Nella pagina aggiungere alcune attività.</span><span class="sxs-lookup"><span data-stu-id="94f6a-204">Add a few tasks in the page.</span></span>

![PHP si connette correttamente al database di Azure per MySQL (anteprima)](./media/app-service-web-tutorial-php-mysql/mysql-connect-success.png)

<span data-ttu-id="94f6a-206">Per arrestare PHP, digitare `Ctrl + C` nel terminale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-206">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="commit-your-changes"></a><span data-ttu-id="94f6a-207">Eseguire il commit delle modifiche</span><span class="sxs-lookup"><span data-stu-id="94f6a-207">Commit your changes</span></span>

<span data-ttu-id="94f6a-208">Eseguire i comandi Git seguenti per eseguire il commit delle modifiche:</span><span class="sxs-lookup"><span data-stu-id="94f6a-208">Run the following Git commands to commit your changes:</span></span>

```bash
git add .
git commit -m "database.php updates"
```

<span data-ttu-id="94f6a-209">L'app è pronta per la distribuzione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-209">Your app is ready to be deployed.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="94f6a-210">Distribuzione in Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-210">Deploy to Azure</span></span>

<span data-ttu-id="94f6a-211">In questo passaggio viene distribuita l'applicazione PHP connessa a MySQL nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="94f6a-211">In this step, you deploy the MySQL-connected PHP application to Azure App Service.</span></span>

### <a name="create-an-app-service-plan"></a><span data-ttu-id="94f6a-212">Creare un piano di servizio app</span><span class="sxs-lookup"><span data-stu-id="94f6a-212">Create an App Service plan</span></span>

[!INCLUDE [Create app service plan no h](../../includes/app-service-web-create-app-service-plan-no-h.md)]

### <a name="create-a-web-app"></a><span data-ttu-id="94f6a-213">Creare un'app Web</span><span class="sxs-lookup"><span data-stu-id="94f6a-213">Create a web app</span></span>

[!INCLUDE [Create web app no h](../../includes/app-service-web-create-web-app-no-h.md)]

### <a name="set-the-php-version"></a><span data-ttu-id="94f6a-214">Impostare la versione di PHP</span><span class="sxs-lookup"><span data-stu-id="94f6a-214">Set the PHP version</span></span>

<span data-ttu-id="94f6a-215">Impostare la versione PHP necessaria all'applicazione usando il comando [az webapp config set](/cli/azure/webapp/config#set).</span><span class="sxs-lookup"><span data-stu-id="94f6a-215">Set the PHP version that the application requires by using the [az webapp config set](/cli/azure/webapp/config#set) command.</span></span>

<span data-ttu-id="94f6a-216">Il comando seguente imposta la versione PHP su _7.0_.</span><span class="sxs-lookup"><span data-stu-id="94f6a-216">The following command sets the PHP version to _7.0_.</span></span>

```azurecli-interactive
az webapp config set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --php-version 7.0
```

### <a name="configure-database-settings"></a><span data-ttu-id="94f6a-217">Configurare le impostazioni del database</span><span class="sxs-lookup"><span data-stu-id="94f6a-217">Configure database settings</span></span>

<span data-ttu-id="94f6a-218">Come evidenziato in precedenza, è possibile connettersi al database MySQL di Azure mediante le variabili di ambiente nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="94f6a-218">As pointed out previously, you can connect to your Azure MySQL database using environment variables in App Service.</span></span>

<span data-ttu-id="94f6a-219">Nel servizio app le variabili di ambiente vengono impostate come _impostazioni dell'app_ usando il comando [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="94f6a-219">In App Service, you set environment variables as _app settings_ by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span>

<span data-ttu-id="94f6a-220">Il comando seguente configura le impostazioni dell'app `DB_HOST`, `DB_DATABASE`, `DB_USERNAME` e `DB_PASSWORD`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-220">The following command configures the app settings `DB_HOST`, `DB_DATABASE`, `DB_USERNAME`, and `DB_PASSWORD`.</span></span> <span data-ttu-id="94f6a-221">Sostituire i segnaposto _&lt;appname>_ e _&lt;mysql_server_name>_.</span><span class="sxs-lookup"><span data-stu-id="94f6a-221">Replace the placeholders _&lt;appname>_ and _&lt;mysql_server_name>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings DB_HOST="<mysql_server_name>.database.windows.net" DB_DATABASE="sampledb" DB_USERNAME="phpappuser@<mysql_server_name>" DB_PASSWORD="MySQLAzure2017" MYSQL_SSL="true"
```

<span data-ttu-id="94f6a-222">È possibile usare il metodo [getenv](http://www.php.net/manual/function.getenv.php) di PHP per accedere alle impostazioni.</span><span class="sxs-lookup"><span data-stu-id="94f6a-222">You can use the PHP [getenv](http://www.php.net/manual/function.getenv.php) method to access the settings.</span></span> <span data-ttu-id="94f6a-223">Il codice Laravel usa un wrapper [env](https://laravel.com/docs/5.4/helpers#method-env) su `getenv` di PHP.</span><span class="sxs-lookup"><span data-stu-id="94f6a-223">the Laravel code uses an [env](https://laravel.com/docs/5.4/helpers#method-env) wrapper over the PHP `getenv`.</span></span> <span data-ttu-id="94f6a-224">Ad esempio, la configurazione di MySQL in _config/database.php_ è simile al codice seguente:</span><span class="sxs-lookup"><span data-stu-id="94f6a-224">For example, the MySQL configuration in _config/database.php_ looks like the following code:</span></span>

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

### <a name="configure-laravel-environment-variables"></a><span data-ttu-id="94f6a-225">Configurare le variabili di ambiente di Laravel</span><span class="sxs-lookup"><span data-stu-id="94f6a-225">Configure Laravel environment variables</span></span>

<span data-ttu-id="94f6a-226">Laravel richiede una chiave di applicazione nel servizio app.</span><span class="sxs-lookup"><span data-stu-id="94f6a-226">Laravel needs an application key in App Service.</span></span> <span data-ttu-id="94f6a-227">È possibile configurarla con le impostazioni dell'app.</span><span class="sxs-lookup"><span data-stu-id="94f6a-227">You can configure it with app settings.</span></span>

<span data-ttu-id="94f6a-228">Usare `php artisan` per generare una nuova chiave applicazione senza salvarla in _.env_.</span><span class="sxs-lookup"><span data-stu-id="94f6a-228">Use `php artisan` to generate a new application key without saving it to _.env_.</span></span>

```bash
php artisan key:generate --show
```

<span data-ttu-id="94f6a-229">Impostare la chiave dell'applicazione nell'app Web del servizio app usando il comando [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set).</span><span class="sxs-lookup"><span data-stu-id="94f6a-229">Set the application key in the App Service web app by using the [az webapp config appsettings set](/cli/azure/webapp/config/appsettings#set) command.</span></span> <span data-ttu-id="94f6a-230">Sostituire i segnaposto _&lt;appname>_ e _&lt;outputofphpartisankey:generate>_.</span><span class="sxs-lookup"><span data-stu-id="94f6a-230">Replace the placeholders _&lt;appname>_ and _&lt;outputofphpartisankey:generate>_.</span></span>

```azurecli-interactive
az webapp config appsettings set \
    --name <app_name> \
    --resource-group myResourceGroup \
    --settings APP_KEY="<output_of_php_artisan_key:generate>" APP_DEBUG="true"
```

<span data-ttu-id="94f6a-231">`APP_DEBUG="true"` indica a Laravel di restituire le informazioni di debug quando l'app Web distribuita rileva errori.</span><span class="sxs-lookup"><span data-stu-id="94f6a-231">`APP_DEBUG="true"` tells Laravel to return debugging information when the deployed web app encounters errors.</span></span> <span data-ttu-id="94f6a-232">Quando si esegue un'applicazione di produzione, è consigliabile impostarla su `false`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-232">When running a production application, set it to `false`, which is more secure.</span></span>

### <a name="set-the-virtual-application-path"></a><span data-ttu-id="94f6a-233">Impostare il percorso virtuale dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="94f6a-233">Set the virtual application path</span></span>

<span data-ttu-id="94f6a-234">Impostare il percorso virtuale dell'applicazione per l'app Web.</span><span class="sxs-lookup"><span data-stu-id="94f6a-234">Set the virtual application path for the web app.</span></span> <span data-ttu-id="94f6a-235">Questo passaggio è necessario perché il [ciclo di vita dell'applicazione Laravel](https://laravel.com/docs/5.4/lifecycle) ha inizio nella directory _public_ anziché nella directory radice dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-235">This step is required because the [Laravel application lifecycle](https://laravel.com/docs/5.4/lifecycle) begins in the _public_ directory instead of the application's root directory.</span></span> <span data-ttu-id="94f6a-236">Gli altri framework PHP il cui ciclo di vita si avvia nella directory radice funzionano anche senza la configurazione manuale del percorso dell'applicazione virtuale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-236">Other PHP frameworks whose lifecycle start in the root directory can work without manual configuration of the virtual application path.</span></span>

<span data-ttu-id="94f6a-237">Impostare il percorso virtuale dell'applicazione usando il comando [az resource update](/cli/azure/resource#update).</span><span class="sxs-lookup"><span data-stu-id="94f6a-237">Set the virtual application path by using the [az resource update](/cli/azure/resource#update) command.</span></span> <span data-ttu-id="94f6a-238">Sostituire il segnaposto _&lt;appname>_ .</span><span class="sxs-lookup"><span data-stu-id="94f6a-238">Replace the _&lt;appname>_ placeholder.</span></span>

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

<span data-ttu-id="94f6a-239">Per impostazione predefinita, il servizio app di Azure fa in modo che il percorso virtuale dell'applicazione radice (_/_) punti alla directory radice dei file dell'applicazione distribuiti (_sites\wwwroot_).</span><span class="sxs-lookup"><span data-stu-id="94f6a-239">By default, Azure App Service points the root virtual application path (_/_) to the root directory of the deployed application files (_sites\wwwroot_).</span></span>

### <a name="configure-a-deployment-user"></a><span data-ttu-id="94f6a-240">Configurare un utente della distribuzione</span><span class="sxs-lookup"><span data-stu-id="94f6a-240">Configure a deployment user</span></span>

[!INCLUDE [Configure deployment user](../../includes/configure-deployment-user-no-h.md)]

### <a name="configure-local-git-deployment"></a><span data-ttu-id="94f6a-241">Configurare la distribuzione con l'istanza Git locale</span><span class="sxs-lookup"><span data-stu-id="94f6a-241">Configure local Git deployment</span></span>

[!INCLUDE [Configure local git](../../includes/app-service-web-configure-local-git-no-h.md)]

### <a name="push-to-azure-from-git"></a><span data-ttu-id="94f6a-242">Effettuare il push in Azure da Git</span><span class="sxs-lookup"><span data-stu-id="94f6a-242">Push to Azure from Git</span></span>

<span data-ttu-id="94f6a-243">Aggiungere un'istanza remota di Azure al repository Git locale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-243">Add an Azure remote to your local Git repository.</span></span>

```bash
git remote add azure <paste_copied_url_here>
```

<span data-ttu-id="94f6a-244">Effettuare il push a un'istanza remota di Azure per distribuire l'applicazione PHP.</span><span class="sxs-lookup"><span data-stu-id="94f6a-244">Push to the Azure remote to deploy the PHP application.</span></span> <span data-ttu-id="94f6a-245">Verrà richiesta la password specificata in precedenza durante la creazione dell'utente di distribuzione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-245">You are prompted for the password you supplied earlier as part of the creation of the deployment user.</span></span>

```bash
git push azure master
```

<span data-ttu-id="94f6a-246">Durante la distribuzione, Servizio app di Azure comunica lo stato con Git.</span><span class="sxs-lookup"><span data-stu-id="94f6a-246">During deployment, Azure App Service communicates its progress with Git.</span></span>

```bash
Counting objects: 3, done.
Delta compression using up to 8 threads.
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
> <span data-ttu-id="94f6a-247">Si può notare che, alla fine, il processo di distribuzione installa i pacchetti [Composer](https://getcomposer.org/).</span><span class="sxs-lookup"><span data-stu-id="94f6a-247">You may notice that the deployment process installs [Composer](https://getcomposer.org/) packages at the end.</span></span> <span data-ttu-id="94f6a-248">Il servizio app non esegue tali automazioni durante la distribuzione predefinita, pertanto questo repository di esempio include tre file aggiuntivi nella directory radice per abilitarlo:</span><span class="sxs-lookup"><span data-stu-id="94f6a-248">App Service does not run these automations during default deployment, so this sample repository has three additional files in its root directory to enable it:</span></span>
>
> - <span data-ttu-id="94f6a-249">`.deployment` - Questo file indica al servizio app di eseguire `bash deploy.sh` come script di distribuzione personalizzato.</span><span class="sxs-lookup"><span data-stu-id="94f6a-249">`.deployment` - This file tells App Service to run `bash deploy.sh` as the custom deployment script.</span></span>
> - <span data-ttu-id="94f6a-250">`deploy.sh` - Script di distribuzione personalizzato.</span><span class="sxs-lookup"><span data-stu-id="94f6a-250">`deploy.sh` - The custom deployment script.</span></span> <span data-ttu-id="94f6a-251">Se si esamina il file, si noterà che esegue `php composer.phar install` dopo `npm install`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-251">If you review the file, you will see that it runs `php composer.phar install` after `npm install`.</span></span>
> - <span data-ttu-id="94f6a-252">`composer.phar` - Gestione pacchetti Composer.</span><span class="sxs-lookup"><span data-stu-id="94f6a-252">`composer.phar` - The Composer package manager.</span></span>
>
> <span data-ttu-id="94f6a-253">È possibile usare questo approccio per aggiungere uno o più passaggi alla distribuzione basata su Git al servizio app.</span><span class="sxs-lookup"><span data-stu-id="94f6a-253">You can use this approach to add any step to your Git-based deployment to App Service.</span></span> <span data-ttu-id="94f6a-254">Per altre informazioni, vedere [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script) (Script di distribuzione personalizzata).</span><span class="sxs-lookup"><span data-stu-id="94f6a-254">For more information, see [Custom Deployment Script](https://github.com/projectkudu/kudu/wiki/Custom-Deployment-Script).</span></span>
>

### <a name="browse-to-the-azure-web-app"></a><span data-ttu-id="94f6a-255">Passare all'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-255">Browse to the Azure web app</span></span>

<span data-ttu-id="94f6a-256">Passare a `http://<app_name>.azurewebsites.net` e aggiungere alcune attività all'elenco.</span><span class="sxs-lookup"><span data-stu-id="94f6a-256">Browse to `http://<app_name>.azurewebsites.net` and add a few tasks to the list.</span></span>

![App PHP in esecuzione nel Servizio app di Azure](./media/app-service-web-tutorial-php-mysql/php-mysql-in-azure.png)

<span data-ttu-id="94f6a-258">L'app PHP basata su dati è in esecuzione nel servizio app di Azure.</span><span class="sxs-lookup"><span data-stu-id="94f6a-258">Congratulations, you're running a data-driven PHP app in Azure App Service.</span></span>

## <a name="update-model-locally-and-redeploy"></a><span data-ttu-id="94f6a-259">Aggiornare il modello in locale e rieseguire la distribuzione</span><span class="sxs-lookup"><span data-stu-id="94f6a-259">Update model locally and redeploy</span></span>

<span data-ttu-id="94f6a-260">In questo passaggio viene apportata una modifica semplice al modello di dati `task` e all'app Web e quindi viene pubblicato l'aggiornamento in Azure.</span><span class="sxs-lookup"><span data-stu-id="94f6a-260">In this step, you make a simple change to the `task` data model and the webapp, and then publish the update to Azure.</span></span>

<span data-ttu-id="94f6a-261">Per lo scenario delle attività, l'applicazione viene modificata per poter contrassegnare un'attività come completata.</span><span class="sxs-lookup"><span data-stu-id="94f6a-261">For the tasks scenario, you modify the application so that you can mark a task as complete.</span></span>

### <a name="add-a-column"></a><span data-ttu-id="94f6a-262">Aggiungere una colonna</span><span class="sxs-lookup"><span data-stu-id="94f6a-262">Add a column</span></span>

<span data-ttu-id="94f6a-263">Nel terminale passare alla radice del repository Git.</span><span class="sxs-lookup"><span data-stu-id="94f6a-263">In the terminal, navigate to the root of the Git repository.</span></span>

<span data-ttu-id="94f6a-264">Generare una nuova migrazione di database per la tabella `tasks`:</span><span class="sxs-lookup"><span data-stu-id="94f6a-264">Generate a new database migration for the `tasks` table:</span></span>

```bash
php artisan make:migration add_complete_column --table=tasks
```

<span data-ttu-id="94f6a-265">Questo comando mostra il nome del file di migrazione che viene generato.</span><span class="sxs-lookup"><span data-stu-id="94f6a-265">This command shows you the name of the migration file that's generated.</span></span> <span data-ttu-id="94f6a-266">Trovare il file in _database/migrations_ e aprirlo.</span><span class="sxs-lookup"><span data-stu-id="94f6a-266">Find this file in _database/migrations_ and open it.</span></span>

<span data-ttu-id="94f6a-267">Sostituire il metodo `up` con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="94f6a-267">Replace the `up` method with the following code:</span></span>

```php
public function up()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->boolean('complete')->default(False);
    });
}
```

<span data-ttu-id="94f6a-268">Il codice precedente aggiunge una colonna booleana nella tabella `tasks` denominata `complete`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-268">The preceding code adds a boolean column in the `tasks` table called `complete`.</span></span>

<span data-ttu-id="94f6a-269">Sostituire il metodo `down` con il codice seguente per l'azione di ripristino dello stato precedente:</span><span class="sxs-lookup"><span data-stu-id="94f6a-269">Replace the `down` method with the following code for the rollback action:</span></span>

```php
public function down()
{
    Schema::table('tasks', function (Blueprint $table) {
        $table->dropColumn('complete');
    });
}
```

<span data-ttu-id="94f6a-270">Nel terminale eseguire le migrazioni del database Laravel per apportare la modifica nel database locale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-270">In the terminal, run Laravel database migrations to make the change in the local database.</span></span>

```bash
php artisan migrate
```

<span data-ttu-id="94f6a-271">In base alla [convenzione di denominazione Laravel](https://laravel.com/docs/5.4/eloquent#defining-models), il modello `Task` (vedere _app/Task.php_) esegue il mapping alla tabella `tasks` per impostazione predefinita.</span><span class="sxs-lookup"><span data-stu-id="94f6a-271">Based on the [Laravel naming convention](https://laravel.com/docs/5.4/eloquent#defining-models), the model `Task` (see _app/Task.php_) maps to the `tasks` table by default.</span></span>

### <a name="update-application-logic"></a><span data-ttu-id="94f6a-272">Aggiornare la logica dell'applicazione</span><span class="sxs-lookup"><span data-stu-id="94f6a-272">Update application logic</span></span>

<span data-ttu-id="94f6a-273">Aprire il file *routes/web.php*.</span><span class="sxs-lookup"><span data-stu-id="94f6a-273">Open the *routes/web.php* file.</span></span> <span data-ttu-id="94f6a-274">L'applicazione definisce qui le route e la logica di business.</span><span class="sxs-lookup"><span data-stu-id="94f6a-274">The application defines its routes and business logic here.</span></span>

<span data-ttu-id="94f6a-275">Alla fine del file aggiungere una route con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="94f6a-275">At the end of the file, add a route with the following code:</span></span>

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

<span data-ttu-id="94f6a-276">Il codice precedente esegue un semplice aggiornamento del modello di dati tramite l'attivazione e la disattivazione del valore di `complete`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-276">The preceding code makes a simple update to the data model by toggling the value of `complete`.</span></span>

### <a name="update-the-view"></a><span data-ttu-id="94f6a-277">Aggiornare la visualizzazione</span><span class="sxs-lookup"><span data-stu-id="94f6a-277">Update the view</span></span>

<span data-ttu-id="94f6a-278">Aprire il file *resources/views/tasks.blade.php*.</span><span class="sxs-lookup"><span data-stu-id="94f6a-278">Open the *resources/views/tasks.blade.php* file.</span></span> <span data-ttu-id="94f6a-279">Trovare il tag di apertura `<tr>` e sostituirlo con:</span><span class="sxs-lookup"><span data-stu-id="94f6a-279">Find the `<tr>` opening tag and replace it with:</span></span>

```html
<tr class="{{ $task->complete ? 'success' : 'active' }}" >
```

<span data-ttu-id="94f6a-280">Il codice precedente modifica il colore di riga in base al completamento dell'attività.</span><span class="sxs-lookup"><span data-stu-id="94f6a-280">The preceding code changes the row color depending on whether the task is complete.</span></span>

<span data-ttu-id="94f6a-281">Nella riga successiva il codice è quello riportato di seguito:</span><span class="sxs-lookup"><span data-stu-id="94f6a-281">In the next line, you have the following code:</span></span>

```html
<td class="table-text"><div>{{ $task->name }}</div></td>
```

<span data-ttu-id="94f6a-282">Sostituire l'intera riga con il codice seguente:</span><span class="sxs-lookup"><span data-stu-id="94f6a-282">Replace the entire line with the following code:</span></span>

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

<span data-ttu-id="94f6a-283">Il codice precedente aggiunge il pulsante di invio che fa riferimento alla route definita in precedenza.</span><span class="sxs-lookup"><span data-stu-id="94f6a-283">The preceding code adds the submit button that references the route that you defined earlier.</span></span>

### <a name="test-the-changes-locally"></a><span data-ttu-id="94f6a-284">Testare le modifiche in locale</span><span class="sxs-lookup"><span data-stu-id="94f6a-284">Test the changes locally</span></span>

<span data-ttu-id="94f6a-285">Dalla directory radice del repository Git eseguire il server di sviluppo.</span><span class="sxs-lookup"><span data-stu-id="94f6a-285">From the root directory of the Git repository, run the development server.</span></span>

```bash
php artisan serve
```

<span data-ttu-id="94f6a-286">Per visualizzare la modifica dello stato dell'attività, passare a `http://localhost:8000` e selezionare la casella di controllo.</span><span class="sxs-lookup"><span data-stu-id="94f6a-286">To see the task status change, navigate to `http://localhost:8000` and select the checkbox.</span></span>

![Casella di controllo aggiuntiva all'attività](./media/app-service-web-tutorial-php-mysql/complete-checkbox.png)

<span data-ttu-id="94f6a-288">Per arrestare PHP, digitare `Ctrl + C` nel terminale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-288">To stop PHP, type `Ctrl + C` in the terminal.</span></span>

### <a name="publish-changes-to-azure"></a><span data-ttu-id="94f6a-289">Pubblicare le modifiche in Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-289">Publish changes to Azure</span></span>

<span data-ttu-id="94f6a-290">Nel terminale eseguire le migrazioni del database Laravel con la stringa di connessione di produzione per apportare la modifica nel database di Azure.</span><span class="sxs-lookup"><span data-stu-id="94f6a-290">In the terminal, run Laravel database migrations with the production connection string to make the change in the Azure database.</span></span>

```bash
php artisan migrate --env=production --force
```

<span data-ttu-id="94f6a-291">Eseguire il commit di tutte le modifiche in Git e quindi effettuare il push delle modifiche al codice in Azure.</span><span class="sxs-lookup"><span data-stu-id="94f6a-291">Commit all the changes in Git, and then push the code changes to Azure.</span></span>

```bash
git add .
git commit -m "added complete checkbox"
git push azure master
```

<span data-ttu-id="94f6a-292">Dopo aver completato `git push`, passare all'app Web di Azure e testare la nuova funzionalità.</span><span class="sxs-lookup"><span data-stu-id="94f6a-292">Once the `git push` is complete, navigate to the Azure web app and test the new functionality.</span></span>

![Modifiche al modello e al database pubblicate in Azure](media/app-service-web-tutorial-php-mysql/complete-checkbox-published.png)

<span data-ttu-id="94f6a-294">Le attività aggiunte vengono mantenute nel database.</span><span class="sxs-lookup"><span data-stu-id="94f6a-294">If you added any tasks, they are retained in the database.</span></span> <span data-ttu-id="94f6a-295">Gli aggiornamenti allo schema di dati non modificano i dati esistenti.</span><span class="sxs-lookup"><span data-stu-id="94f6a-295">Updates to the data schema leave existing data intact.</span></span>

## <a name="stream-diagnostic-logs"></a><span data-ttu-id="94f6a-296">Eseguire lo streaming dei log di diagnostica</span><span class="sxs-lookup"><span data-stu-id="94f6a-296">Stream diagnostic logs</span></span>

<span data-ttu-id="94f6a-297">Mentre l'applicazione PHP è in esecuzione nel servizio app di Azure, è possibile fare in modo che i log di console siano inviati tramite pipe al terminale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-297">While the PHP application runs in Azure App Service, you can get the console logs piped to your terminal.</span></span> <span data-ttu-id="94f6a-298">Ciò consente di ottenere gli stessi messaggi di diagnostica per il debug degli errori dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-298">That way, you can get the same diagnostic messages to help you debug application errors.</span></span>

<span data-ttu-id="94f6a-299">Per avviare lo streaming dei log, usare il comando [az webapp log tail](/cli/azure/webapp/log#tail).</span><span class="sxs-lookup"><span data-stu-id="94f6a-299">To start log streaming, use the [az webapp log tail](/cli/azure/webapp/log#tail) command.</span></span>

```azurecli-interactive
az webapp log tail \
    --name <app_name> \
    --resource-group myResourceGroup
```

<span data-ttu-id="94f6a-300">Dopo avere avviato lo streaming dei log, aggiornare l'app Web di Azure nel browser per ricevere traffico Web.</span><span class="sxs-lookup"><span data-stu-id="94f6a-300">Once log streaming has started, refresh the Azure web app in the browser to get some web traffic.</span></span> <span data-ttu-id="94f6a-301">I log di console vengono inviati tramite pipe al terminale.</span><span class="sxs-lookup"><span data-stu-id="94f6a-301">You can now see console logs piped to the terminal.</span></span> <span data-ttu-id="94f6a-302">Se i log di console non sono immediatamente visibili, controllare nuovamente dopo 30 secondi.</span><span class="sxs-lookup"><span data-stu-id="94f6a-302">If you don't see console logs immediately, check again in 30 seconds.</span></span>

<span data-ttu-id="94f6a-303">Per interrompere lo streaming dei log in qualsiasi momento, digitare `Ctrl`+`C`.</span><span class="sxs-lookup"><span data-stu-id="94f6a-303">To stop log streaming at anytime, type `Ctrl`+`C`.</span></span>

> [!TIP]
> <span data-ttu-id="94f6a-304">Un'applicazione PHP può usare lo standard [error_log()](http://php.net/manual/function.error-log.php) da inviare alla console.</span><span class="sxs-lookup"><span data-stu-id="94f6a-304">A PHP application can use the standard [error_log()](http://php.net/manual/function.error-log.php) to output to the console.</span></span> <span data-ttu-id="94f6a-305">L'applicazione di esempio usa questo approccio in _app/Http/routes.php_.</span><span class="sxs-lookup"><span data-stu-id="94f6a-305">The sample application uses this approach in _app/Http/routes.php_.</span></span>
>
> <span data-ttu-id="94f6a-306">Come framework Web, [Laravel usa Monolog](https://laravel.com/docs/5.4/errors) come provider di registrazione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-306">As a web framework, [Laravel uses Monolog](https://laravel.com/docs/5.4/errors) as the logging provider.</span></span> <span data-ttu-id="94f6a-307">Per informazioni su come fare in modo che Monolog invii messaggi alla console, vedere [PHP: How to use monolog to log to console (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out) (PHP: procedura per usare Monolog per registrarsi alla console (php://out)).</span><span class="sxs-lookup"><span data-stu-id="94f6a-307">To see how to get Monolog to output messages to the console, see [PHP: How to use monolog to log to console (php://out)](http://stackoverflow.com/questions/25787258/php-how-to-use-monolog-to-log-to-console-php-out).</span></span>
>
>

## <a name="manage-the-azure-web-app"></a><span data-ttu-id="94f6a-308">Gestire l'app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-308">Manage the Azure web app</span></span>

<span data-ttu-id="94f6a-309">Accedere al [portale di Azure](https://portal.azure.com) per gestire l'app Web creata.</span><span class="sxs-lookup"><span data-stu-id="94f6a-309">Go to the [Azure portal](https://portal.azure.com) to manage the web app you created.</span></span>

<span data-ttu-id="94f6a-310">Nel menu a sinistra fare clic su **Servizi app** e quindi sul nome dell'app Web di Azure.</span><span class="sxs-lookup"><span data-stu-id="94f6a-310">From the left menu, click **App Services**, and then click the name of your Azure web app.</span></span>

![Passare all'app Web di Azure nel portale](./media/app-service-web-tutorial-php-mysql/access-portal.png)

<span data-ttu-id="94f6a-312">Verrà visualizzata la pagina di panoramica dell'app Web.</span><span class="sxs-lookup"><span data-stu-id="94f6a-312">You see your web app's Overview page.</span></span> <span data-ttu-id="94f6a-313">Nella pagina è possibile eseguire attività di gestione di base come l'arresto, l'avvio, il riavvio e l'eliminazione.</span><span class="sxs-lookup"><span data-stu-id="94f6a-313">Here, you can perform basic management tasks like  stop, start, restart, browse, and delete.</span></span>

<span data-ttu-id="94f6a-314">Il menu a sinistra consente di visualizzare le pagine di configurazione dell'app.</span><span class="sxs-lookup"><span data-stu-id="94f6a-314">The left menu provides pages for configuring your app.</span></span>

![Pagina del servizio app nel portale di Azure](./media/app-service-web-tutorial-php-mysql/web-app-blade.png)

[!INCLUDE [cli-samples-clean-up](../../includes/cli-samples-clean-up.md)]

<a name="next"></a>

## <a name="next-steps"></a><span data-ttu-id="94f6a-316">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="94f6a-316">Next steps</span></span>

<span data-ttu-id="94f6a-317">In questa esercitazione si è appreso come:</span><span class="sxs-lookup"><span data-stu-id="94f6a-317">In this tutorial, you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="94f6a-318">Creare un database MySQL in Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-318">Create a MySQL database in Azure</span></span>
> * <span data-ttu-id="94f6a-319">Connettere un'app PHP a MySQL</span><span class="sxs-lookup"><span data-stu-id="94f6a-319">Connect a PHP app to MySQL</span></span>
> * <span data-ttu-id="94f6a-320">Distribuire l'app in Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-320">Deploy the app to Azure</span></span>
> * <span data-ttu-id="94f6a-321">Aggiornare il modello di dati e ridistribuire l'app</span><span class="sxs-lookup"><span data-stu-id="94f6a-321">Update the data model and redeploy the app</span></span>
> * <span data-ttu-id="94f6a-322">Eseguire lo streaming dei log di diagnostica in Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-322">Stream diagnostic logs from Azure</span></span>
> * <span data-ttu-id="94f6a-323">Gestire l'app nel portale di Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-323">Manage the app in the Azure portal</span></span>

<span data-ttu-id="94f6a-324">Passare all'esercitazione successiva per apprendere come eseguire il mapping di un nome DNS personalizzato a un'app Web.</span><span class="sxs-lookup"><span data-stu-id="94f6a-324">Advance to the next tutorial to learn how to map a custom DNS name to a web app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="94f6a-325">Eseguire il mapping di un nome DNS personalizzato esistente ad app Web di Azure</span><span class="sxs-lookup"><span data-stu-id="94f6a-325">Map an existing custom DNS name to Azure Web Apps</span></span>](app-service-web-tutorial-custom-domain.md)
