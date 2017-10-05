---
title: Progettare il primo Database di Azure per il database MySQL - Interfaccia della riga di comando di Azure | Documentazione Microsoft
description: In questa esercitazione viene illustrato come creare e gestire il database di Azure per il server e il database MySQL tramite l'interfaccia della riga di comando di Azure 2.0 dalla riga di comando.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 590cba6cb58d0c0eaedb9f122ac048c33988004d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="87775-103">Progettare il primo database di Azure per il database MySQL</span><span class="sxs-lookup"><span data-stu-id="87775-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="87775-104">Il database di Azure per MySQL è un servizio di database relazionale in Microsoft Cloud basato sul motore di database MySQL Community Edition.</span><span class="sxs-lookup"><span data-stu-id="87775-104">Azure Database for MySQL is a relational database service in the Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="87775-105">In questa esercitazione, si usano l'interfaccia della riga di comando di Azure e altre utilità per informazioni su come:</span><span class="sxs-lookup"><span data-stu-id="87775-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="87775-106">Creare un database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="87775-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="87775-107">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="87775-107">Configure the server firewall</span></span>
> * <span data-ttu-id="87775-108">Usare lo [strumento della riga di comando mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) per creare un database</span><span class="sxs-lookup"><span data-stu-id="87775-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="87775-109">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="87775-109">Load sample data</span></span>
> * <span data-ttu-id="87775-110">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="87775-110">Query data</span></span>
> * <span data-ttu-id="87775-111">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="87775-111">Update data</span></span>
> * <span data-ttu-id="87775-112">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="87775-112">Restore data</span></span>

<span data-ttu-id="87775-113">È possibile usare Azure Cloud Shell nel browser o [installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli) nel computer in uso per eseguire i blocchi di codice di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="87775-113">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="87775-114">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="87775-114">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="87775-115">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="87775-115">Run `az --version` to find the version.</span></span> <span data-ttu-id="87775-116">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="87775-116">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="87775-117">Se si dispone di più sottoscrizioni, scegliere la sottoscrizione appropriata in cui la risorsa esiste o per cui è configurata.</span><span class="sxs-lookup"><span data-stu-id="87775-117">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="87775-118">Selezionare un ID di sottoscrizione specifico sotto l'account tramite il comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="87775-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="87775-119">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="87775-119">Create a resource group</span></span>
<span data-ttu-id="87775-120">Creare un [gruppo di risorse di Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) con il comando [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="87775-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="87775-121">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.</span><span class="sxs-lookup"><span data-stu-id="87775-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="87775-122">Nell'esempio seguente viene creato un gruppo di risorse denominato `mycliresource` nella posizione `westus`.</span><span class="sxs-lookup"><span data-stu-id="87775-122">The following example creates a resource group named `mycliresource` in the `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="87775-123">Creare un database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="87775-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="87775-124">Creare un database di Azure per il server MySQL con il comando mysql server create.</span><span class="sxs-lookup"><span data-stu-id="87775-124">Create an Azure Database for MySQL server with the az mysql server create command.</span></span> <span data-ttu-id="87775-125">Un server può gestire più database.</span><span class="sxs-lookup"><span data-stu-id="87775-125">A server can manage multiple databases.</span></span> <span data-ttu-id="87775-126">In genere, viene usato un database separato per ogni progetto o per ogni utente.</span><span class="sxs-lookup"><span data-stu-id="87775-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="87775-127">L'esempio seguente crea un database di Azure per il server MySQL disponibile in `westus` nel gruppo di risorse `mycliresource` con nome `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="87775-127">The following example creates an Azure Database for MySQL server located in `westus` in the resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="87775-128">Il server ha un account di accesso amministratore chiamato `myadmin` e la password `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="87775-128">The server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="87775-129">Il server viene creato con livello di prestazioni **Basic** e **50** unità di calcolo condivise tra tutti i database nel server.</span><span class="sxs-lookup"><span data-stu-id="87775-129">The server is created with **Basic** performance tier and **50** compute units shared between all the databases in the server.</span></span> <span data-ttu-id="87775-130">È possibile aumentare o ridurre le capacità di calcolo e archiviazione a seconda delle esigenze dell'applicazione.</span><span class="sxs-lookup"><span data-stu-id="87775-130">You can scale compute and storage up or down depending on the application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="87775-131">Configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="87775-131">Configure firewall rule</span></span>
<span data-ttu-id="87775-132">Creare una regola del firewall a livello di server del Database SQL di Azure con il comando az mysql server firewall-rule create.</span><span class="sxs-lookup"><span data-stu-id="87775-132">Create an Azure Database for MySQL server-level firewall rule with the az mysql server firewall-rule create command.</span></span> <span data-ttu-id="87775-133">Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio lo strumento della riga di comando **mysql** o MySQL Workbench, di connettersi al server tramite il firewall del servizio MySQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="87775-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench to connect to your server through the Azure MySQL service firewall.</span></span> 

<span data-ttu-id="87775-134">Nell'esempio seguente viene creata una regola del firewall per un intervallo di indirizzi predefinito.</span><span class="sxs-lookup"><span data-stu-id="87775-134">The following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="87775-135">In questo esempio viene illustrato l'intero intervallo possibile di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="87775-135">This example shows the entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-the-connection-information"></a><span data-ttu-id="87775-136">Ottenere le informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="87775-136">Get the connection information</span></span>

<span data-ttu-id="87775-137">Per connettersi al server, è necessario specificare le informazioni sull'host e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="87775-137">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="87775-138">Il risultato è in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="87775-138">The result is in JSON format.</span></span> <span data-ttu-id="87775-139">Annotare il **fullyQualifiedDomainName** e l'**administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="87775-139">Make a note of the **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
```json
{
  "administratorLogin": "myadmin",
  "administratorLoginPassword": null,
  "fullyQualifiedDomainName": "mycliserver.database.windows.net",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/mycliresource/providers/Microsoft.DBforMySQL/servers/mycliserver",
  "location": "westus",
  "name": "mycliserver",
  "resourceGroup": "mycliresource",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "MYSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "storageMb": 2048,
  "tags": null,
  "type": "Microsoft.DBforMySQL/servers",
  "userVisibleState": "Ready",
  "version": null
}
```

## <a name="connect-to-the-server-using-mysql"></a><span data-ttu-id="87775-140">Connettersi al server usando mysql</span><span class="sxs-lookup"><span data-stu-id="87775-140">Connect to the server using mysql</span></span>
<span data-ttu-id="87775-141">Usare lo [strumento della riga di comando mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) per stabilire una connessione al Database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="87775-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to establish a connection to your Azure Database for MySQL server.</span></span> <span data-ttu-id="87775-142">In questo esempio, il comando è:</span><span class="sxs-lookup"><span data-stu-id="87775-142">In this example, the command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="87775-143">Creazione di un database vuoto</span><span class="sxs-lookup"><span data-stu-id="87775-143">Create a blank database</span></span>
<span data-ttu-id="87775-144">Una volta connessi al server, creare un database vuoto.</span><span class="sxs-lookup"><span data-stu-id="87775-144">Once you’re connected to the server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="87775-145">Nel prompt, eseguire il comando seguente per cambiare la connessione nel database appena creato:</span><span class="sxs-lookup"><span data-stu-id="87775-145">At the prompt, run the following command to switch the connection to this newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="87775-146">Creare tabelle nel database</span><span class="sxs-lookup"><span data-stu-id="87775-146">Create tables in the database</span></span>
<span data-ttu-id="87775-147">Dopo aver appreso come connettersi al database di Azure per il database MySQL, si può passare al completamento di alcune attività di base.</span><span class="sxs-lookup"><span data-stu-id="87775-147">Now that you know how to connect to the Azure Database for MySQL database, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="87775-148">In primo luogo, è possibile creare una tabella e caricarla con alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="87775-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="87775-149">Creare una tabella che contenga le informazioni riguardanti l'inventario.</span><span class="sxs-lookup"><span data-stu-id="87775-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="87775-150">Caricare i dati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="87775-150">Load data into the tables</span></span>
<span data-ttu-id="87775-151">Ora che abbiamo una tabella, possiamo inserire alcuni dati al suo interno.</span><span class="sxs-lookup"><span data-stu-id="87775-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="87775-152">Nella finestra del prompt dei comandi aperta, eseguire la query seguente per inserire alcune righe di dati.</span><span class="sxs-lookup"><span data-stu-id="87775-152">At the open command prompt window, run the following query to insert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="87775-153">A questo punto, ci sono due righe di dati di esempio nella tabella creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="87775-153">Now you have two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="87775-154">Eseguire una query e aggiornare i dati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="87775-154">Query and update the data in the tables</span></span>
<span data-ttu-id="87775-155">Eseguire la query seguente per recuperare informazioni dalla tabella del database.</span><span class="sxs-lookup"><span data-stu-id="87775-155">Execute the following query to retrieve information from the database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="87775-156">Si possono anche aggiornare query e aggiornare i dati nelle tabelle.</span><span class="sxs-lookup"><span data-stu-id="87775-156">You can also update the data in the tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="87775-157">La riga viene aggiornata di conseguenza quando si recuperano dati.</span><span class="sxs-lookup"><span data-stu-id="87775-157">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="87775-158">Ripristinare un database a un momento precedente</span><span class="sxs-lookup"><span data-stu-id="87775-158">Restore a database to a previous point in time</span></span>
<span data-ttu-id="87775-159">Si supponga di aver eliminato accidentalmente questa tabella.</span><span class="sxs-lookup"><span data-stu-id="87775-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="87775-160">Si tratta di un elemento che non è facile da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="87775-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="87775-161">Il database di Azure per MySQL consente di tornare in qualsiasi punto degli ultimi 35 giorni e di ripristinare questo punto nel tempo in un nuovo server.</span><span class="sxs-lookup"><span data-stu-id="87775-161">Azure Database for MySQL allows you to go back to any point in time in the last up to 35 days and restore this point in time to a new server.</span></span> <span data-ttu-id="87775-162">È possibile usare questo nuovo server per ripristinare i dati eliminati.</span><span class="sxs-lookup"><span data-stu-id="87775-162">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="87775-163">La procedura seguente consente di ripristinare il server di esempio in un punto precedente all'aggiunta della tabella.</span><span class="sxs-lookup"><span data-stu-id="87775-163">The following steps restore the sample server to a point before the table was added.</span></span>

<span data-ttu-id="87775-164">Per il ripristino sono necessarie le informazioni seguenti:</span><span class="sxs-lookup"><span data-stu-id="87775-164">For the Restore you need the following information:</span></span>

- <span data-ttu-id="87775-165">Punto di ripristino: selezionare un punto nel tempo precedente alla modifica del server.</span><span class="sxs-lookup"><span data-stu-id="87775-165">Restore point: Select a point-in-time that occurs before the server was changed.</span></span> <span data-ttu-id="87775-166">Il punto deve essere maggiore o equivalente al valore del backup meno recente del database di origine.</span><span class="sxs-lookup"><span data-stu-id="87775-166">Must be greater than or equal to the source database's Oldest backup value.</span></span>
- <span data-ttu-id="87775-167">Server di destinazione: fornire un nuovo nome del server che si desidera ripristinare.</span><span class="sxs-lookup"><span data-stu-id="87775-167">Target server: Provide a new server name you want to restore to</span></span>
- <span data-ttu-id="87775-168">Server di origine: fornire il nome del server che si desidera ripristinare</span><span class="sxs-lookup"><span data-stu-id="87775-168">Source server: Provide the name of the server you want to restore from</span></span>
- <span data-ttu-id="87775-169">Posizione: non è possibile selezionare l'area, per impostazione predefinita è la stessa del server di origine</span><span class="sxs-lookup"><span data-stu-id="87775-169">Location: You cannot select the region, by default it is same as the source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="87775-170">Per ripristinare il server e [ ripristinare in un punto nel tempo ](./howto-restore-server-portal.md) precedente all'eliminazione delle tabelle.</span><span class="sxs-lookup"><span data-stu-id="87775-170">To restore the server and [restore to a point-in-time](./howto-restore-server-portal.md) before the table was deleted.</span></span> <span data-ttu-id="87775-171">Il ripristino di un server in un altro punto nel tempo crea un duplicato del nuovo server come il server originale nel punto nel tempo specificato, purché sia entro il periodo di conservazione per il [livello di servizio](./concepts-service-tiers.md) applicato.</span><span class="sxs-lookup"><span data-stu-id="87775-171">Restoring a server to a different point in time creates a duplicate new server as the original server as of the point in time you specify, provided that it is within the retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="87775-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="87775-172">Next Steps</span></span>
<span data-ttu-id="87775-173">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="87775-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="87775-174">Creare un database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="87775-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="87775-175">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="87775-175">Configure the server firewall</span></span>
> * <span data-ttu-id="87775-176">Usare lo [strumento della riga di comando mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) per creare un database</span><span class="sxs-lookup"><span data-stu-id="87775-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) to create a database</span></span>
> * <span data-ttu-id="87775-177">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="87775-177">Load sample data</span></span>
> * <span data-ttu-id="87775-178">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="87775-178">Query data</span></span>
> * <span data-ttu-id="87775-179">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="87775-179">Update data</span></span>
> * <span data-ttu-id="87775-180">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="87775-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="87775-181">Database di Azure per MySQL - Esempi di interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="87775-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
