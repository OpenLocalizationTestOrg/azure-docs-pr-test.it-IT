---
title: Progettare il primo Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure | Documentazione Microsoft
description: In questa esercitazione viene illustrato come tooDesign di Azure prima di Database per PostgreSQL utilizzando CLI di Azure.
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
ms.openlocfilehash: 7914925c090e0b6f3e7c8a999eedb0b2baf83d7d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-postgresql-using-azure-cli"></a><span data-ttu-id="6ce5c-103">Progettare il primo Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="6ce5c-103">Design your first Azure Database for PostgreSQL using Azure CLI</span></span> 
<span data-ttu-id="6ce5c-104">In questa esercitazione, si utilizza Azure CLI (interfaccia della riga di comando) e toolearn altre utilità come a:</span><span class="sxs-lookup"><span data-stu-id="6ce5c-104">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="6ce5c-105">Creare un database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6ce5c-105">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="6ce5c-106">Configurare firewall hello del server</span><span class="sxs-lookup"><span data-stu-id="6ce5c-106">Configure hello server firewall</span></span>
> * <span data-ttu-id="6ce5c-107">Utilizzare [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilità un database</span><span class="sxs-lookup"><span data-stu-id="6ce5c-107">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="6ce5c-108">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="6ce5c-108">Load sample data</span></span>
> * <span data-ttu-id="6ce5c-109">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="6ce5c-109">Query data</span></span>
> * <span data-ttu-id="6ce5c-110">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="6ce5c-110">Update data</span></span>
> * <span data-ttu-id="6ce5c-111">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="6ce5c-111">Restore data</span></span>

<span data-ttu-id="6ce5c-112">È possibile utilizzare hello Azure Cloud Shell nel browser hello o [installare Azure CLI 2.0]( /cli/azure/install-azure-cli) su blocchi di codice hello toorun propri computer in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-112">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6ce5c-113">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-113">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6ce5c-114">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-114">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="6ce5c-115">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="6ce5c-115">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="6ce5c-116">Se si dispone di più sottoscrizioni, scegliere la sottoscrizione appropriata di hello in cui esistano risorse hello o viene fatturata per.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-116">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="6ce5c-117">Selezionare un ID di sottoscrizione specifico sotto l'account tramite il comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="6ce5c-117">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="6ce5c-118">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="6ce5c-118">Create a resource group</span></span>
<span data-ttu-id="6ce5c-119">Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) utilizzando hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-119">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="6ce5c-120">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-120">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="6ce5c-121">esempio Hello crea un gruppo di risorse denominato `myresourcegroup` in hello `westus` percorso.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-121">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="6ce5c-122">Creare un database di Azure per il server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6ce5c-122">Create an Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="6ce5c-123">Creare un [Database di Azure per server PostgreSQL](overview.md) utilizzando hello [az postgres server creare](/cli/azure/postgres/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-123">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="6ce5c-124">Un server contiene un gruppo di database gestiti come gruppo.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-124">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="6ce5c-125">esempio Hello crea un server denominato `mypgserver-20170401` nel gruppo di risorse `myresourcegroup` con account di accesso amministratore server `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-125">hello following example creates a server called `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="6ce5c-126">Nome di un server esegue il mapping nome tooDNS ed è pertanto necessario toobe globalmente univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-126">Name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="6ce5c-127">Hello Substitute `<server_admin_password>` con il proprio valore.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-127">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401 --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="6ce5c-128">account di accesso amministratore server Hello e una password che è possibile specificare sono necessari toolog toohello server e i relativi database più avanti in questa Guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-128">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="6ce5c-129">Prendere nota di queste informazioni per usarle in seguito.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-129">Remember or record this information for later use.</span></span>

<span data-ttu-id="6ce5c-130">Per impostazione predefinita, il database **postgres** viene creato nel server.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-130">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="6ce5c-131">Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database è un database predefinito può essere utilizzata per gli utenti, utilità e applicazioni di terze parti.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-131">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="6ce5c-132">Configurare una regola del firewall a livello di server</span><span class="sxs-lookup"><span data-stu-id="6ce5c-132">Configure a server-level firewall rule</span></span>

<span data-ttu-id="6ce5c-133">Creare una regola firewall di livello server Azure PostgreSQL con hello [az postgres regola firewall del server-creare](/cli/azure/postgres/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-133">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="6ce5c-134">Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) o [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server firewall hello Azure PostgreSQL servizio.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-134">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="6ce5c-135">È possibile impostare una regola del firewall che copre un intervallo IP toobe tooconnect in grado di dalla rete.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-135">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="6ce5c-136">Hello seguente utilizza [az postgres regola firewall del server-creare](/cli/azure/postgres/server/firewall-rule#create) toocreate una regola del firewall `AllowAllIps` intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-136">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="6ce5c-137">tooopen tutti gli indirizzi IP, utilizzare 0.0.0.0 come hello avvio indirizzo IP e 255.255.255.255 come hello indirizzo finale.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-137">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="6ce5c-138">Il server PostgreSQL Azure comunica sulla porta 5432.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-138">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="6ce5c-139">Quando si esegue la connessione da una rete aziendale, il traffico in uscita sulla porta 5432 potrebbe non essere consentito dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-139">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="6ce5c-140">È aperto il reparto IT server porte 5432 tooconnect tooyour Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-140">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>
>

## <a name="get-hello-connection-information"></a><span data-ttu-id="6ce5c-141">Ottenere informazioni sulla connessione hello</span><span class="sxs-lookup"><span data-stu-id="6ce5c-141">Get hello connection information</span></span>

<span data-ttu-id="6ce5c-142">tooconnect tooyour server, sono necessarie credenziali di accesso e le informazioni di host tooprovide.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-142">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="6ce5c-143">il risultato di Hello è nel formato JSON.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-143">hello result is in JSON format.</span></span> <span data-ttu-id="6ce5c-144">Prendere nota di hello **administratorLogin** e **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-144">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-tooazure-database-for-postgresql-database-using-psql"></a><span data-ttu-id="6ce5c-145">Connettersi tooAzure Database per database PostgreSQL utilizzando psql</span><span class="sxs-lookup"><span data-stu-id="6ce5c-145">Connect tooAzure Database for PostgreSQL database using psql</span></span>
<span data-ttu-id="6ce5c-146">Se il computer client abbia PostgreSQL installato, è possibile utilizzare un'istanza locale di [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), o hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-146">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html), or hello Azure Cloud Console tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="6ce5c-147">Verrà ora utilizzare hello psql utilità della riga di comando tooconnect toohello Azure Database PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-147">Let's now use hello psql command-line utility tooconnect toohello Azure Database for PostgreSQL server.</span></span>

1. <span data-ttu-id="6ce5c-148">Eseguire hello seguente psql comando tooconnect tooan Database di Azure per server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6ce5c-148">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="6ce5c-149">Ad esempio, hello comando seguente si connette a database predefinito toohello chiamato **postgres** sul server PostgreSQL **mypgserver 20170401.postgres.database.azure.com** utilizzando le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-149">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="6ce5c-150">Immettere hello `<server_admin_password>` scelto quando viene richiesta la password.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-150">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 ---dbname=postgres
```

2.  <span data-ttu-id="6ce5c-151">Dopo avere connesso toohello server, è possibile creare un database vuoto al prompt dei comandi hello.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-151">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="6ce5c-152">Al prompt dei comandi hello, eseguire hello seguente database toohello appena creato di comando tooswitch connessione **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="6ce5c-152">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="6ce5c-153">Creare tabelle nel database di hello</span><span class="sxs-lookup"><span data-stu-id="6ce5c-153">Create tables in hello database</span></span>
<span data-ttu-id="6ce5c-154">Ora che è stato appreso come tooconnect toohello Database di Azure per PostgreSQL, possiamo andare come toocomplete alcune attività di base.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-154">Now that you know how tooconnect toohello Azure Database for PostgreSQL, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="6ce5c-155">In primo luogo, è possibile creare una tabella e caricarla con alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-155">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="6ce5c-156">Creare una tabella che tiene traccia delle informazioni riguardanti l'inventario.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-156">Let's create a table that tracks inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

<span data-ttu-id="6ce5c-157">È possibile visualizzare hello creata tabella nell'elenco delle tabelle di hello ora digitando:</span><span class="sxs-lookup"><span data-stu-id="6ce5c-157">You can see hello newly created table in hello list of tables now by typing:</span></span>
```sql
\dt
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="6ce5c-158">Caricamento dei dati nelle tabelle di hello</span><span class="sxs-lookup"><span data-stu-id="6ce5c-158">Load data into hello tables</span></span>
<span data-ttu-id="6ce5c-159">Ora che abbiamo una tabella, possiamo inserire alcuni dati al suo interno.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-159">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="6ce5c-160">Nella finestra del prompt dei comandi aperta hello eseguire hello seguente query tooinsert alcune righe di dati</span><span class="sxs-lookup"><span data-stu-id="6ce5c-160">At hello open command prompt window, run hello following query tooinsert some rows of data</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="6ce5c-161">È ora due righe di dati di esempio nella tabella hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-161">You have now two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="6ce5c-162">Eseguire una query e aggiornare i dati nelle tabelle di hello hello</span><span class="sxs-lookup"><span data-stu-id="6ce5c-162">Query and update hello data in hello tables</span></span>
<span data-ttu-id="6ce5c-163">Eseguire le seguenti query tooretrieve informazioni dalla tabella di database hello hello.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-163">Execute hello following query tooretrieve information from hello database table.</span></span> 
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="6ce5c-164">È inoltre possibile aggiornare i dati di hello nelle tabelle di hello</span><span class="sxs-lookup"><span data-stu-id="6ce5c-164">You can also update hello data in hello tables</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="6ce5c-165">la riga Hello Ottiene aggiornata di conseguenza quando si recuperano dati.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-165">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="6ce5c-166">Ripristinare un punto precedente tooa di database nel tempo</span><span class="sxs-lookup"><span data-stu-id="6ce5c-166">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="6ce5c-167">Si supponga di aver eliminato accidentalmente una tabella.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-167">Imagine you have accidentally deleted a table.</span></span> <span data-ttu-id="6ce5c-168">Si tratta di un elemento che non è facile da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-168">This is something you cannot easily recover from.</span></span> <span data-ttu-id="6ce5c-169">Il Database di Azure per PostgreSQL consente toogo tooany indietro punto nel tempo (in hello ultimo backup too7 giorni (Basic) e 35 giorni (Standard)) e il ripristino di questo nuovo server tooa punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-169">Azure Database for PostgreSQL allows you toogo back tooany point-in-time (in hello last up too7 days (Basic) and 35 days (Standard)) and restore this point-in-time tooa new server.</span></span> <span data-ttu-id="6ce5c-170">È possibile utilizzare questo nuovo toorecover server i dati eliminati.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-170">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="6ce5c-171">Hello seguente punto di ripristino hello campione server tooa passaggi prima tabella hello è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-171">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="6ce5c-172">Hello `az postgres server restore` comando deve hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="6ce5c-172">hello `az postgres server restore` command needs hello following parameters:</span></span>
| <span data-ttu-id="6ce5c-173">Impostazione</span><span class="sxs-lookup"><span data-stu-id="6ce5c-173">Setting</span></span> | <span data-ttu-id="6ce5c-174">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="6ce5c-174">Suggested value</span></span> | <span data-ttu-id="6ce5c-175">Descrizione</span><span class="sxs-lookup"><span data-stu-id="6ce5c-175">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="6ce5c-176">--resource-group</span><span class="sxs-lookup"><span data-stu-id="6ce5c-176">--resource-group</span></span> |  <span data-ttu-id="6ce5c-177">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6ce5c-177">myResourceGroup</span></span> |  <span data-ttu-id="6ce5c-178">Il gruppo di risorse in cui hello server di origine esiste.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-178">The resource group in which hello source server exists.</span></span>  |
| <span data-ttu-id="6ce5c-179">--name</span><span class="sxs-lookup"><span data-stu-id="6ce5c-179">--name</span></span> | <span data-ttu-id="6ce5c-180">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="6ce5c-180">mypgserver-restored</span></span> | <span data-ttu-id="6ce5c-181">nome di Hello del server di nuovo hello viene creato dal comando di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-181">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="6ce5c-182">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="6ce5c-182">restore-point-in-time</span></span> | <span data-ttu-id="6ce5c-183">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="6ce5c-183">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="6ce5c-184">Selezionare un toorestore punto nel tempo per.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-184">Select a point-in-time toorestore to.</span></span> <span data-ttu-id="6ce5c-185">Questa data e ora deve essere entro il periodo di conservazione dei backup del server di origine hello.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-185">This date and time must be within hello source server's backup retention period.</span></span> <span data-ttu-id="6ce5c-186">Usare il formato ISO8601 per la data e l'ora.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-186">Use ISO8601 date and time format.</span></span> <span data-ttu-id="6ce5c-187">È possibile usare il fuso orario locale, ad esempio `2017-04-13T05:59:00-08:00`, o il formato UTC Zulu `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-187">For example, you may use your own local timezone, such as `2017-04-13T05:59:00-08:00`, or use UTC Zulu format `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="6ce5c-188">--source-server</span><span class="sxs-lookup"><span data-stu-id="6ce5c-188">--source-server</span></span> | <span data-ttu-id="6ce5c-189">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="6ce5c-189">mypgserver-20170401</span></span> | <span data-ttu-id="6ce5c-190">Hello nome o ID di hello origine server toorestore da.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-190">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="6ce5c-191">Ripristino di un server tooa punto nel tempo, viene creato un nuovo server, la copia come server originale di hello a partire da hello punto nel tempo specificato.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-191">Restoring a server tooa point-in-time creates a new server, copying as hello original server as of hello point in time you specify.</span></span> <span data-ttu-id="6ce5c-192">percorso Hello e prezzi indicati i livelli per server hello ripristinato sono hello stesso come server di origine hello.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-192">hello location and pricing tier values for hello restored server are hello same as hello source server.</span></span>

<span data-ttu-id="6ce5c-193">comando Hello è sincrono e verrà restituito dopo il ripristino del server di hello.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-193">hello command is synchronous, and will return after hello server is restored.</span></span> <span data-ttu-id="6ce5c-194">Al termine del ripristino di hello, individuare hello nuovo server in cui è stato creato.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-194">Once hello restore finishes, locate hello new server that was created.</span></span> <span data-ttu-id="6ce5c-195">Verificare hello ripristino dei dati nel modo previsto.</span><span class="sxs-lookup"><span data-stu-id="6ce5c-195">Verify hello data was restored as expected.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6ce5c-196">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6ce5c-196">Next steps</span></span>
<span data-ttu-id="6ce5c-197">In questa esercitazione, si è appreso toouse CLI di Azure (interfaccia della riga di comando) e di altre utilità per:</span><span class="sxs-lookup"><span data-stu-id="6ce5c-197">In this tutorial, you learned how toouse Azure CLI (command-line interface) and other utilities to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="6ce5c-198">Creare un database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6ce5c-198">Create an Azure Database for PostgreSQL</span></span>
> * <span data-ttu-id="6ce5c-199">Configurare firewall hello del server</span><span class="sxs-lookup"><span data-stu-id="6ce5c-199">Configure hello server firewall</span></span>
> * <span data-ttu-id="6ce5c-200">Utilizzare [ **psql** ](https://www.postgresql.org/docs/9.6/static/app-psql.html) toocreate utilità un database</span><span class="sxs-lookup"><span data-stu-id="6ce5c-200">Use [**psql**](https://www.postgresql.org/docs/9.6/static/app-psql.html) utility toocreate a database</span></span>
> * <span data-ttu-id="6ce5c-201">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="6ce5c-201">Load sample data</span></span>
> * <span data-ttu-id="6ce5c-202">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="6ce5c-202">Query data</span></span>
> * <span data-ttu-id="6ce5c-203">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="6ce5c-203">Update data</span></span>
> * <span data-ttu-id="6ce5c-204">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="6ce5c-204">Restore data</span></span>

<span data-ttu-id="6ce5c-205">Successivamente, informazioni su come toouse hello attività simili toodo portale Azure, rivedere l'esercitazione: [di progettazione di un Database di Azure per PostgreSQL utilizzando hello portale di Azure](tutorial-design-database-using-azure-portal.md)</span><span class="sxs-lookup"><span data-stu-id="6ce5c-205">Next, learn how toouse hello Azure portal toodo similar tasks, review this tutorial: [Design your first Azure Database for PostgreSQL using hello Azure portal](tutorial-design-database-using-azure-portal.md)</span></span>
