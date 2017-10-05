---
title: Progettare il primo Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure | Documentazione Microsoft
description: In questa esercitazione viene illustrato come progettare il primo Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: tutorial
ms.date: 06/13/2017
ms.openlocfilehash: cf536fce8925f9173b541b845af25a8d8c38eabd
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="607ed-103">Progettare il primo Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="607ed-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="607ed-104">In questa esercitazione, si usano l'interfaccia della riga di comando di Azure e altre utilità per informazioni su come:</span><span class="sxs-lookup"><span data-stu-id="607ed-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities to learn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="607ed-105">Creare un database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="607ed-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="607ed-106">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="607ed-106">Configure the server firewall</span></span>
> * <span data-ttu-id="607ed-107">Usare l'utilità [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) per creare un database</span><span class="sxs-lookup"><span data-stu-id="607ed-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="607ed-108">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="607ed-108">Load sample data</span></span>
> * <span data-ttu-id="607ed-109">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="607ed-109">Query data</span></span>
> * <span data-ttu-id="607ed-110">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="607ed-110">Update data</span></span>
> * <span data-ttu-id="607ed-111">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="607ed-111">Restore data</span></span>

<span data-ttu-id="607ed-112">È possibile usare Azure Cloud Shell nel browser o [installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli) nel computer in uso per eseguire i blocchi di codice di questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="607ed-112">You may use the Azure Cloud Shell in the browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer to run the code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="607ed-113">Se si sceglie di installare e usare l'interfaccia della riga di comando in locale, per questo argomento è necessario eseguire la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ed-113">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="607ed-114">Eseguire `az --version` per trovare la versione.</span><span class="sxs-lookup"><span data-stu-id="607ed-114">Run `az --version` to find the version.</span></span> <span data-ttu-id="607ed-115">Se è necessario eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="607ed-115">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="607ed-116">Se si dispone di più sottoscrizioni, scegliere la sottoscrizione appropriata in cui la risorsa esiste o per cui è configurata.</span><span class="sxs-lookup"><span data-stu-id="607ed-116">If you have multiple subscriptions, choose the appropriate subscription in which the resource exists or is billed for.</span></span> <span data-ttu-id="607ed-117">Selezionare un ID di sottoscrizione specifico sotto l'account tramite il comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="607ed-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="607ed-118">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="607ed-118">Create a resource group</span></span>
<span data-ttu-id="607ed-119">Creare un [gruppo di risorse di Azure](../azure-resource-manager/resource-group-overview.md) con il comando [az group create](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="607ed-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using the [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="607ed-120">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.</span><span class="sxs-lookup"><span data-stu-id="607ed-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="607ed-121">Nell'esempio seguente viene creato un gruppo di risorse denominato `myresourcegroup` nella posizione `westus`.</span><span class="sxs-lookup"><span data-stu-id="607ed-121">The following example creates a resource group named `myresourcegroup` in the `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="607ed-122">Creare un database di Azure per il server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="607ed-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="607ed-123">Creare un [database di Azure per il server PostgreSQL](overview.md) tramite il comando [az postgres server create](/cli/azure/postgres/server#create).</span><span class="sxs-lookup"><span data-stu-id="607ed-123">Create an [Azure Database for PostgreSQL server](overview.md) using the [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="607ed-124">Un server contiene un gruppo di database gestiti come gruppo.</span><span class="sxs-lookup"><span data-stu-id="607ed-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="607ed-125">Nell'esempio seguente viene creato un server denominato `mypgserver-20170401` nel gruppo di risorse `myresourcegroup` con account di accesso dell'amministratore del server `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="607ed-125">The following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="607ed-126">Il nome di un server esegue il mapping al nome DNS e pertanto deve essere univoco a livello globale in Azure.</span><span class="sxs-lookup"><span data-stu-id="607ed-126">Name of a server maps to DNS name and is thus required to be globally unique in Azure.</span></span> <span data-ttu-id="607ed-127">Sostituire `<server_admin_password>` con il proprio valore.</span><span class="sxs-lookup"><span data-stu-id="607ed-127">Substitute the `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="607ed-128">L'account di accesso amministratore server e la password qui specificati sono necessari per accedere al server e ai relativi database più avanti in questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="607ed-128">The server admin login and password that you specify here are required to log in to the server and its databases later in this quick start.</span></span> <span data-ttu-id="607ed-129">Prendere nota di queste informazioni per usarle in seguito.</span><span class="sxs-lookup"><span data-stu-id="607ed-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="607ed-130">Per impostazione predefinita, il database **postgres** viene creato al di sotto del server.</span><span class="sxs-lookup"><span data-stu-id="607ed-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="607ed-131">Il database [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) è un database predefinito che può essere usato da utenti, utilità e applicazioni di terze parti.</span><span class="sxs-lookup"><span data-stu-id="607ed-131">The [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="607ed-132">Configurare una regola del firewall a livello di server</span><span class="sxs-lookup"><span data-stu-id="607ed-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="607ed-133">Creare una regola del firewall a livello di server per PostgreSQL Azure tramite il comando [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="607ed-133">Create an Azure PostgreSQL server-level firewall rule with the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="607ed-134">Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) o [PgAdmin](https://www.pgadmin.org/), di connettersi al server tramite il firewall del servizio PostgreSQL Azure.</span><span class="sxs-lookup"><span data-stu-id="607ed-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) to connect to your server through the Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="607ed-135">È possibile impostare una regola del firewall relativa a un intervallo IP per consentire la connessione dalla rete.</span><span class="sxs-lookup"><span data-stu-id="607ed-135">You can set a firewall rule that covers an IP range to be able to connect from your network.</span></span> <span data-ttu-id="607ed-136">L'esempio seguente usa [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) per creare una regola del firewall `AllowAllIps` per un intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="607ed-136">The following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) to create a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="607ed-137">Per aprire tutti gli indirizzi IP, usare 0.0.0.0 come indirizzo IP iniziale e 255.255.255.255 come indirizzo finale.</span><span class="sxs-lookup"><span data-stu-id="607ed-137">To open all IP addresses, use 0.0.0.0 as the starting IP address and 255.255.255.255 as the ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="607ed-138">Il server PostgreSQL Azure comunica sulla porta 5432.</span><span class="sxs-lookup"><span data-stu-id="607ed-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="607ed-139">Quando si esegue la connessione da una rete aziendale, il traffico in uscita sulla porta 5432 potrebbe non essere consentito dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="607ed-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="607ed-140">Richiedere al reparto IT di aprire la porta 5432 per connettersi al server di database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ed-140">Have your IT department open port 5432 to connect to your Azure SQL Database server.</span></span>
>

## <a name="get-the-connection-information"></a><span data-ttu-id="607ed-141">Ottenere le informazioni di connessione</span><span class="sxs-lookup"><span data-stu-id="607ed-141">Get the connection information</span></span>

<span data-ttu-id="607ed-142">Per connettersi al server, è necessario specificare le informazioni sull'host e le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="607ed-142">To connect to your server, you need to provide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="607ed-143">Il risultato è in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="607ed-143">The result is in JSON format.</span></span> <span data-ttu-id="607ed-144">Annotare l'**administratorLogin** e il **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="607ed-144">Make a note of the **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
```json
{
  "administratorLogin": "mylogin",
  "fullyQualifiedDomainName": "mypgserver-20170401.postgres.database.azure.com",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.DBforPostgreSQL/servers/mypgserver-20170401",
  "location": "westus",
  "name": "mypgserver-20170401",
  "resourceGroup": "myresourcegroup",
  "sku": {
    "capacity": 50,
    "family": null,
    "name": "PGSQLS2M50",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": null,
  "storageMb": 51200,
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "9.6"
}
```

## <a name="connect-to-azure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="607ed-145">Connettersi al Database di Azure per il database PostgreSQL tramite psql</span><span class="sxs-lookup"><span data-stu-id="607ed-145">Connect to Azure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="607ed-146">Se nel computer client è installato PostgreSQL, è possibile usare un'istanza locale di [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) o la console Cloud di Azure per connettersi a un server PostgreSQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="607ed-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or the Azure Cloud Console to connect to an Azure PostgreSQL server.</span></span> <span data-ttu-id="607ed-147">Si usi ora l'utilità della riga di comando psql per connettersi al Database di Azure per il server PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="607ed-147">Let's now use the psql command-line utility to connect to the Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="607ed-148">Eseguire il comando psql seguente per connettersi a un database di Azure per il server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="607ed-148">Run the following psql command to connect to an Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="607ed-149">Ad esempio, il comando seguente permette di connettersi al database predefinito chiamato **postgres** nel server PostgreSQL **mypgserver-20170401.postgres.database.azure.com** usando le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="607ed-149">For example, the following command connects to the default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="607ed-150">Immettere il valore di `<server_admin_password>` scelto quando viene chiesta la password.</span><span class="sxs-lookup"><span data-stu-id="607ed-150">Enter the `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="607ed-151">Dopo aver eseguito la connessione al server, creare un database vuoto nel prompt.</span><span class="sxs-lookup"><span data-stu-id="607ed-151">Once you are connected to the server, create a blank database at the prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="607ed-152">Nel prompt, eseguire il comando seguente per cambiare la connessione nel database appena creato **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="607ed-152">At the prompt, execute the following command to switch connection to the newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-the-database"></a><span data-ttu-id="607ed-153">Creare tabelle nel database</span><span class="sxs-lookup"><span data-stu-id="607ed-153">Create tables in the database</span></span>
<span data-ttu-id="607ed-154">Dopo aver appreso come connettersi al Database di Azure per PostgreSQL, si può passare al completamento di alcune attività di base.</span><span class="sxs-lookup"><span data-stu-id="607ed-154">Now that you know how to connect to the Azure Database for PostgreSQL, we can go over how to complete some basic tasks.</span></span>

<span data-ttu-id="607ed-155">In primo luogo, è possibile creare una tabella e caricarla con alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="607ed-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="607ed-156">Creare una tabella che tiene traccia delle informazioni riguardanti l'inventario.</span><span class="sxs-lookup"><span data-stu-id="607ed-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="607ed-157">È possibile visualizzare ora la tabella appena creata nell'elenco di tabelle digitando:</span><span class="sxs-lookup"><span data-stu-id="607ed-157">You can see the newly created table in the list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-the-tables"></a><span data-ttu-id="607ed-158">Caricare i dati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="607ed-158">Load data into the tables</span></span>
<span data-ttu-id="607ed-159">Ora che abbiamo una tabella, possiamo inserire alcuni dati al suo interno.</span><span class="sxs-lookup"><span data-stu-id="607ed-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="607ed-160">Nella finestra del prompt dei comandi aperta, eseguire la query seguente per inserire alcune righe di dati</span><span class="sxs-lookup"><span data-stu-id="607ed-160">At the open command prompt window, run the following query to insert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="607ed-161">A questo punto, sono presenti due righe di dati di esempio nella tabella creata in precedenza.</span><span class="sxs-lookup"><span data-stu-id="607ed-161">You have now two rows of sample data into the table you created earlier.</span></span>

## <a name="query-and-update-the-data-in-the-tables"></a><span data-ttu-id="607ed-162">Eseguire una query e aggiornare i dati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="607ed-162">Query and update the data in the tables</span></span>
<span data-ttu-id="607ed-163">Eseguire la query seguente per recuperare informazioni dalla tabella del database.</span><span class="sxs-lookup"><span data-stu-id="607ed-163">Execute the following query to retrieve information from the database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="607ed-164">Si possono anche aggiornare i dati nelle tabelle</span><span class="sxs-lookup"><span data-stu-id="607ed-164">You can also update the data in the tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="607ed-165">La riga viene aggiornata di conseguenza quando si recuperano dati.</span><span class="sxs-lookup"><span data-stu-id="607ed-165">The row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-to-a-previous-point-in-time"></a><span data-ttu-id="607ed-166">Ripristinare un database a un momento precedente</span><span class="sxs-lookup"><span data-stu-id="607ed-166">Restore a database to a previous point in time</span></span>
<span data-ttu-id="607ed-167">Si supponga di aver eliminato accidentalmente una tabella.</span><span class="sxs-lookup"><span data-stu-id="607ed-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="607ed-168">Si tratta di un elemento che non è facile da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="607ed-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="607ed-169">Il Database di Azure per PostgreSQL consente di tornare in qualsiasi punto nel tempo (negli ultimi 7 giorni (Basic) e 35 giorni (Standard)) e ripristinare questo punto nel tempo in un nuovo server.</span><span class="sxs-lookup"><span data-stu-id="607ed-169">Azure Database for PostgreSQL allows you to go back to any point-in-time (in the last up to 7 days (Basic) and 35 days (Standard)) and restore this point-in-time to a new server.</span></span> <span data-ttu-id="607ed-170">È possibile usare questo nuovo server per ripristinare i dati eliminati.</span><span class="sxs-lookup"><span data-stu-id="607ed-170">You can use this new server to recover your deleted data.</span></span> <span data-ttu-id="607ed-171">La procedura seguente consente di ripristinare il server di esempio in un punto precedente all'aggiunta della tabella.</span><span class="sxs-lookup"><span data-stu-id="607ed-171">The following steps restore the sample server to a point before the table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="607ed-172">Il comando `az postgres server restore` richiede i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="607ed-172">The `az postgres server restore` command needs the following parameters:</span></span>
| <span data-ttu-id="607ed-173">Impostazione</span><span class="sxs-lookup"><span data-stu-id="607ed-173">Setting</span></span> | <span data-ttu-id="607ed-174">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="607ed-174">Suggested value</span></span> | <span data-ttu-id="607ed-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="607ed-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="607ed-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="607ed-176">--resource-group</span></span> |  <span data-ttu-id="607ed-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="607ed-177">myResourceGroup</span></span> |  <span data-ttu-id="607ed-178">Il gruppo di risorse in cui si trova il server di origine.</span><span class="sxs-lookup"><span data-stu-id="607ed-178">The resource group in which the source server exists.</span></span>  |
| <span data-ttu-id="607ed-179">--name</span><span class="sxs-lookup"><span data-stu-id="607ed-179">--name</span></span> | <span data-ttu-id="607ed-180">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="607ed-180">mypgserver-restored</span></span> | <span data-ttu-id="607ed-181">Il nome del nuovo server creato con il comando di ripristino.</span><span class="sxs-lookup"><span data-stu-id="607ed-181">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="607ed-182">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="607ed-182">restore-point-in-time</span></span> | <span data-ttu-id="607ed-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="607ed-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="607ed-184">Selezionare un punto di ripristino temporizzato.</span><span class="sxs-lookup"><span data-stu-id="607ed-184">Select a point-in-time to restore to.</span></span> <span data-ttu-id="607ed-185">La data e l'ora devono trovarsi all'interno del periodo di memorizzazione dei backup del server di origine.</span><span class="sxs-lookup"><span data-stu-id="607ed-185">This date and time must be within the source server's backup retention period.</span></span> <span data-ttu-id="607ed-186">Usare il formato ISO8601 per la data e l'ora.</span><span class="sxs-lookup"><span data-stu-id="607ed-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="607ed-187">È possibile usare il fuso orario locale, ad esempio `2017-04-13T05:59:00-08:00`, o il formato UTC Zulu `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="607ed-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="607ed-188">--source-server</span><span class="sxs-lookup"><span data-stu-id="607ed-188">--source-server</span></span> | <span data-ttu-id="607ed-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="607ed-189">mypgserver-20170401</span></span> | <span data-ttu-id="607ed-190">Il nome o l'ID del server di origine da cui eseguire il ripristino.</span><span class="sxs-lookup"><span data-stu-id="607ed-190">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="607ed-191">Il ripristino temporizzato di un server crea un nuovo server, ovvero una copia del server originale nel momento specificato.</span><span class="sxs-lookup"><span data-stu-id="607ed-191">Restoring a server to a point-in-time creates a new server, copying as the original server as of the point in time you specify.</span></span> <span data-ttu-id="607ed-192">I valori relativi al percorso e al piano tariffario del server ripristinato sono gli stessi del server di origine.</span><span class="sxs-lookup"><span data-stu-id="607ed-192">The location and pricing tier values for the restored server are the same as the source server.</span></span>

<span data-ttu-id="607ed-193">Il comando è sincrono e il risultato verrà restituito dopo il ripristino del server.</span><span class="sxs-lookup"><span data-stu-id="607ed-193">The command is synchronous, and will return after the server is restored.</span></span> <span data-ttu-id="607ed-194">Una volta terminato il ripristino, individuare il nuovo server creato.</span><span class="sxs-lookup"><span data-stu-id="607ed-194">Once the restore finishes, locate the new server that was created.</span></span> <span data-ttu-id="607ed-195">Verificare che i dati siano stati ripristinati come previsto.</span><span class="sxs-lookup"><span data-stu-id="607ed-195">Verify the data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="607ed-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="607ed-196">Next steps</span></span>
<span data-ttu-id="607ed-197">In questa esercitazione è stato illustrato come usare l'interfaccia della riga di comando di Azure e altre utilità per:</span><span class="sxs-lookup"><span data-stu-id="607ed-197">In this tutorial, you learned how to use Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="607ed-198">Creare un database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="607ed-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="607ed-199">Configurare il firewall del server</span><span class="sxs-lookup"><span data-stu-id="607ed-199">Configure the server firewall</span></span>
> * <span data-ttu-id="607ed-200">Usare l'utilità [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) per creare un database</span><span class="sxs-lookup"><span data-stu-id="607ed-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility to create a database</span></span>
> * <span data-ttu-id="607ed-201">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="607ed-201">Load sample data</span></span>
> * <span data-ttu-id="607ed-202">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="607ed-202">Query data</span></span>
> * <span data-ttu-id="607ed-203">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="607ed-203">Update data</span></span>
> * <span data-ttu-id="607ed-204">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="607ed-204">Restore data</span></span>

<span data-ttu-id="607ed-205">Successivamente, per informazioni su come usare il portale di Azure per eseguire attività simili, esaminare questa esercitazione: [Progettare il primo Database di Azure per PostgreSQL tramite il portale di Azure](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="607ed-205">Next, learn how to use the Azure portal to do similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using the Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
