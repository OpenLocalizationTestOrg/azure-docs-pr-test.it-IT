---
title: aaaDesign di Azure prima di Database per database MySQL - CLI di Azure | Documenti Microsoft
description: In questa esercitazione viene illustrato come toocreate e gestire Database di Azure per il server MySQL e di database mediante Azure CLI 2.0 dalla riga di comando hello.
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.custom: mvc
ms.openlocfilehash: 6339913c2af58e0e4c4eabb69097a5c9c245781c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="design-your-first-azure-database-for-mysql-database"></a><span data-ttu-id="60fa3-103">Progettare il primo database di Azure per il database MySQL</span><span class="sxs-lookup"><span data-stu-id="60fa3-103">Design your first Azure Database for MySQL database</span></span>

<span data-ttu-id="60fa3-104">Il Database di Azure per MySQL è un servizio di database relazionale in hello Microsoft cloud basato sul motore di database MySQL Community Edition.</span><span class="sxs-lookup"><span data-stu-id="60fa3-104">Azure Database for MySQL is a relational database service in hello Microsoft cloud based on MySQL Community Edition database engine.</span></span> <span data-ttu-id="60fa3-105">In questa esercitazione, si utilizza Azure CLI (interfaccia della riga di comando) e toolearn altre utilità come a:</span><span class="sxs-lookup"><span data-stu-id="60fa3-105">In this tutorial, you use Azure CLI (command-line interface) and other utilities toolearn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="60fa3-106">Creare un database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="60fa3-106">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="60fa3-107">Configurare firewall hello del server</span><span class="sxs-lookup"><span data-stu-id="60fa3-107">Configure hello server firewall</span></span>
> * <span data-ttu-id="60fa3-108">Utilizzare [strumento da riga di comando mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate un database</span><span class="sxs-lookup"><span data-stu-id="60fa3-108">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="60fa3-109">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="60fa3-109">Load sample data</span></span>
> * <span data-ttu-id="60fa3-110">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="60fa3-110">Query data</span></span>
> * <span data-ttu-id="60fa3-111">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="60fa3-111">Update data</span></span>
> * <span data-ttu-id="60fa3-112">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="60fa3-112">Restore data</span></span>

<span data-ttu-id="60fa3-113">È possibile utilizzare hello Azure Cloud Shell nel browser hello o [installare Azure CLI 2.0]( /cli/azure/install-azure-cli) su blocchi di codice hello toorun propri computer in questa esercitazione.</span><span class="sxs-lookup"><span data-stu-id="60fa3-113">You may use hello Azure Cloud Shell in hello browser, or [Install Azure CLI 2.0]( /cli/azure/install-azure-cli) on your own computer toorun hello code blocks in this tutorial.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="60fa3-114">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="60fa3-114">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="60fa3-115">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="60fa3-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="60fa3-116">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="60fa3-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="60fa3-117">Se si dispone di più sottoscrizioni, scegliere la sottoscrizione appropriata di hello in cui esistano risorse hello o viene fatturata per.</span><span class="sxs-lookup"><span data-stu-id="60fa3-117">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource exists or is billed for.</span></span> <span data-ttu-id="60fa3-118">Selezionare un ID di sottoscrizione specifico sotto l'account tramite il comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="60fa3-118">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="60fa3-119">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="60fa3-119">Create a resource group</span></span>
<span data-ttu-id="60fa3-120">Creare un [gruppo di risorse di Azure](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) con il comando [az group create](https://docs.microsoft.com/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="60fa3-120">Create an [Azure resource group](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview) with [az group create](https://docs.microsoft.com/cli/azure/group#create) command.</span></span> <span data-ttu-id="60fa3-121">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.</span><span class="sxs-lookup"><span data-stu-id="60fa3-121">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span>

<span data-ttu-id="60fa3-122">esempio Hello crea un gruppo di risorse denominato `mycliresource` in hello `westus` percorso.</span><span class="sxs-lookup"><span data-stu-id="60fa3-122">hello following example creates a resource group named `mycliresource` in hello `westus` location.</span></span>

```azurecli-interactive
az group create --name mycliresource --location westus
```

## <a name="create-an-azure-database-for-mysql-server"></a><span data-ttu-id="60fa3-123">Creare un database di Azure per il server MySQL</span><span class="sxs-lookup"><span data-stu-id="60fa3-123">Create an Azure Database for MySQL server</span></span>
<span data-ttu-id="60fa3-124">Creare un Database di Azure per comando di creazione di server MySQL hello az mysql server.</span><span class="sxs-lookup"><span data-stu-id="60fa3-124">Create an Azure Database for MySQL server with hello az mysql server create command.</span></span> <span data-ttu-id="60fa3-125">Un server può gestire più database.</span><span class="sxs-lookup"><span data-stu-id="60fa3-125">A server can manage multiple databases.</span></span> <span data-ttu-id="60fa3-126">In genere, viene usato un database separato per ogni progetto o per ogni utente.</span><span class="sxs-lookup"><span data-stu-id="60fa3-126">Typically, a separate database is used for each project or for each user.</span></span>

<span data-ttu-id="60fa3-127">esempio Hello crea un Database di Azure per il server MySQL situato in `westus` nel gruppo di risorse hello `mycliresource` con nome `mycliserver`.</span><span class="sxs-lookup"><span data-stu-id="60fa3-127">hello following example creates an Azure Database for MySQL server located in `westus` in hello resource group `mycliresource` with name `mycliserver`.</span></span> <span data-ttu-id="60fa3-128">Hello server dispone di un accesso di amministratore in denominato `myadmin` e la password `Password01!`.</span><span class="sxs-lookup"><span data-stu-id="60fa3-128">hello server has an administrator log in named `myadmin` and password `Password01!`.</span></span> <span data-ttu-id="60fa3-129">Hello server viene creato con **base** livello di prestazioni e **50** unità condivisa tra tutti i database hello server hello di calcolo.</span><span class="sxs-lookup"><span data-stu-id="60fa3-129">hello server is created with **Basic** performance tier and **50** compute units shared between all hello databases in hello server.</span></span> <span data-ttu-id="60fa3-130">È possibile applicare la scalabilità di calcolo e archiviazione verso l'alto o verso il basso a seconda delle esigenze dell'applicazione hello.</span><span class="sxs-lookup"><span data-stu-id="60fa3-130">You can scale compute and storage up or down depending on hello application needs.</span></span>

```azurecli-interactive
az mysql server create --resource-group mycliresource --name mycliserver
--location westus --user myadmin --password Password01!
--performance-tier Basic --compute-units 50
```

## <a name="configure-firewall-rule"></a><span data-ttu-id="60fa3-131">Configurare una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="60fa3-131">Configure firewall rule</span></span>
<span data-ttu-id="60fa3-132">Creare un Database di Azure per regola del firewall di livello di server MySQL con hello az mysql regola firewall del server-creare un comando.</span><span class="sxs-lookup"><span data-stu-id="60fa3-132">Create an Azure Database for MySQL server-level firewall rule with hello az mysql server firewall-rule create command.</span></span> <span data-ttu-id="60fa3-133">Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio **mysql** strumento da riga di comando o un server di tooyour tooconnect MySQL Workbench tramite firewall del servizio Azure MySQL hello.</span><span class="sxs-lookup"><span data-stu-id="60fa3-133">A server-level firewall rule allows an external application, such as **mysql** command-line tool or MySQL Workbench tooconnect tooyour server through hello Azure MySQL service firewall.</span></span> 

<span data-ttu-id="60fa3-134">Hello esempio seguente viene creata una regola del firewall per un intervallo di indirizzi predefiniti.</span><span class="sxs-lookup"><span data-stu-id="60fa3-134">hello following example creates a firewall rule for a predefined address range.</span></span> <span data-ttu-id="60fa3-135">In questo esempio viene hello intera possibili intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="60fa3-135">This example shows hello entire possible range of IP addresses.</span></span>

```azurecli-interactive
az mysql server firewall-rule create --resource-group mycliresource --server mycliserver --name AllowYourIP --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

## <a name="get-hello-connection-information"></a><span data-ttu-id="60fa3-136">Ottenere informazioni sulla connessione hello</span><span class="sxs-lookup"><span data-stu-id="60fa3-136">Get hello connection information</span></span>

<span data-ttu-id="60fa3-137">tooconnect tooyour server, sono necessarie credenziali di accesso e le informazioni di host tooprovide.</span><span class="sxs-lookup"><span data-stu-id="60fa3-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az mysql server show --resource-group mycliresource --name mycliserver
```

<span data-ttu-id="60fa3-138">il risultato di Hello è nel formato JSON.</span><span class="sxs-lookup"><span data-stu-id="60fa3-138">hello result is in JSON format.</span></span> <span data-ttu-id="60fa3-139">Prendere nota di hello **fullyQualifiedDomainName** e **administratorLogin**.</span><span class="sxs-lookup"><span data-stu-id="60fa3-139">Make a note of hello **fullyQualifiedDomainName** and **administratorLogin**.</span></span>
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

## <a name="connect-toohello-server-using-mysql"></a><span data-ttu-id="60fa3-140">Connessione server toohello con mysql</span><span class="sxs-lookup"><span data-stu-id="60fa3-140">Connect toohello server using mysql</span></span>
<span data-ttu-id="60fa3-141">Utilizzare [strumento da riga di comando mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish tooyour una connessione Database di Azure per il server MySQL.</span><span class="sxs-lookup"><span data-stu-id="60fa3-141">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) tooestablish a connection tooyour Azure Database for MySQL server.</span></span> <span data-ttu-id="60fa3-142">In questo esempio, il comando hello è:</span><span class="sxs-lookup"><span data-stu-id="60fa3-142">In this example, hello command is:</span></span>
```cmd
mysql -h mycliserver.database.windows.net -u myadmin@mycliserver -p
```

## <a name="create-a-blank-database"></a><span data-ttu-id="60fa3-143">Creazione di un database vuoto</span><span class="sxs-lookup"><span data-stu-id="60fa3-143">Create a blank database</span></span>
<span data-ttu-id="60fa3-144">Dopo aver connesso toohello server, creare un database vuoto.</span><span class="sxs-lookup"><span data-stu-id="60fa3-144">Once you’re connected toohello server, create a blank database.</span></span>
```sql
mysql> CREATE DATABASE mysampledb;
```

<span data-ttu-id="60fa3-145">Al prompt dei comandi hello, eseguire hello seguenti database di comando tooswitch hello connessione toothis appena creato:</span><span class="sxs-lookup"><span data-stu-id="60fa3-145">At hello prompt, run hello following command tooswitch hello connection toothis newly created database:</span></span>
```sql
mysql> USE mysampledb;
```

## <a name="create-tables-in-hello-database"></a><span data-ttu-id="60fa3-146">Creare tabelle nel database di hello</span><span class="sxs-lookup"><span data-stu-id="60fa3-146">Create tables in hello database</span></span>
<span data-ttu-id="60fa3-147">Ora che è stato appreso come tooconnect toohello Database di Azure per il database MySQL, possiamo andare come toocomplete alcune attività di base.</span><span class="sxs-lookup"><span data-stu-id="60fa3-147">Now that you know how tooconnect toohello Azure Database for MySQL database, we can go over how toocomplete some basic tasks.</span></span>

<span data-ttu-id="60fa3-148">In primo luogo, è possibile creare una tabella e caricarla con alcuni dati.</span><span class="sxs-lookup"><span data-stu-id="60fa3-148">First, we can create a table and load it with some data.</span></span> <span data-ttu-id="60fa3-149">Creare una tabella che contenga le informazioni riguardanti l'inventario.</span><span class="sxs-lookup"><span data-stu-id="60fa3-149">Let's create a table that stores inventory information.</span></span>
```sql
CREATE TABLE inventory (
    id serial PRIMARY KEY, 
    name VARCHAR(50), 
    quantity INTEGER
);
```

## <a name="load-data-into-hello-tables"></a><span data-ttu-id="60fa3-150">Caricamento dei dati nelle tabelle di hello</span><span class="sxs-lookup"><span data-stu-id="60fa3-150">Load data into hello tables</span></span>
<span data-ttu-id="60fa3-151">Ora che abbiamo una tabella, possiamo inserire alcuni dati al suo interno.</span><span class="sxs-lookup"><span data-stu-id="60fa3-151">Now that we have a table, we can insert some data into it.</span></span> <span data-ttu-id="60fa3-152">Nella finestra del prompt dei comandi aperta hello eseguire hello seguente query tooinsert alcune righe di dati.</span><span class="sxs-lookup"><span data-stu-id="60fa3-152">At hello open command prompt window, run hello following query tooinsert some rows of data.</span></span>
```sql
INSERT INTO inventory (id, name, quantity) VALUES (1, 'banana', 150); 
INSERT INTO inventory (id, name, quantity) VALUES (2, 'orange', 154);
```

<span data-ttu-id="60fa3-153">Ora si dispone di due righe di dati di esempio nella tabella hello creato in precedenza.</span><span class="sxs-lookup"><span data-stu-id="60fa3-153">Now you have two rows of sample data into hello table you created earlier.</span></span>

## <a name="query-and-update-hello-data-in-hello-tables"></a><span data-ttu-id="60fa3-154">Eseguire una query e aggiornare i dati nelle tabelle di hello hello</span><span class="sxs-lookup"><span data-stu-id="60fa3-154">Query and update hello data in hello tables</span></span>
<span data-ttu-id="60fa3-155">Eseguire le seguenti query tooretrieve informazioni dalla tabella di database hello hello.</span><span class="sxs-lookup"><span data-stu-id="60fa3-155">Execute hello following query tooretrieve information from hello database table.</span></span>
```sql
SELECT * FROM inventory;
```

<span data-ttu-id="60fa3-156">È inoltre possibile aggiornare i dati di hello nelle tabelle di hello.</span><span class="sxs-lookup"><span data-stu-id="60fa3-156">You can also update hello data in hello tables.</span></span>
```sql
UPDATE inventory SET quantity = 200 WHERE name = 'banana';
```

<span data-ttu-id="60fa3-157">la riga Hello Ottiene aggiornata di conseguenza quando si recuperano dati.</span><span class="sxs-lookup"><span data-stu-id="60fa3-157">hello row gets updated accordingly when you retrieve data.</span></span>
```sql
SELECT * FROM inventory;
```

## <a name="restore-a-database-tooa-previous-point-in-time"></a><span data-ttu-id="60fa3-158">Ripristinare un punto precedente tooa di database nel tempo</span><span class="sxs-lookup"><span data-stu-id="60fa3-158">Restore a database tooa previous point in time</span></span>
<span data-ttu-id="60fa3-159">Si supponga di aver eliminato accidentalmente questa tabella.</span><span class="sxs-lookup"><span data-stu-id="60fa3-159">Imagine you have accidentally deleted this table.</span></span> <span data-ttu-id="60fa3-160">Si tratta di un elemento che non è facile da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="60fa3-160">This is something you cannot easily recover from.</span></span> <span data-ttu-id="60fa3-161">Il Database di Azure per MySQL consente toogo tooany indietro punto nel tempo di hello ultimo backup too35 giorni e questo punto nel tempo tooa nuovo server di ripristino.</span><span class="sxs-lookup"><span data-stu-id="60fa3-161">Azure Database for MySQL allows you toogo back tooany point in time in hello last up too35 days and restore this point in time tooa new server.</span></span> <span data-ttu-id="60fa3-162">È possibile utilizzare questo nuovo toorecover server i dati eliminati.</span><span class="sxs-lookup"><span data-stu-id="60fa3-162">You can use this new server toorecover your deleted data.</span></span> <span data-ttu-id="60fa3-163">Hello seguente punto di ripristino hello campione server tooa passaggi prima tabella hello è stato aggiunto.</span><span class="sxs-lookup"><span data-stu-id="60fa3-163">hello following steps restore hello sample server tooa point before hello table was added.</span></span>

<span data-ttu-id="60fa3-164">Per hello ripristino è necessario hello le seguenti informazioni:</span><span class="sxs-lookup"><span data-stu-id="60fa3-164">For hello Restore you need hello following information:</span></span>

- <span data-ttu-id="60fa3-165">Punto di ripristino: selezionare un punto nel tempo che si verifica prima che il server di hello è stato modificato.</span><span class="sxs-lookup"><span data-stu-id="60fa3-165">Restore point: Select a point-in-time that occurs before hello server was changed.</span></span> <span data-ttu-id="60fa3-166">Deve essere maggiore o uguale valore backup meno recenti del database di origine toohello.</span><span class="sxs-lookup"><span data-stu-id="60fa3-166">Must be greater than or equal toohello source database's Oldest backup value.</span></span>
- <span data-ttu-id="60fa3-167">Server di destinazione: fornire un nuovo nome del server desiderato toorestore per</span><span class="sxs-lookup"><span data-stu-id="60fa3-167">Target server: Provide a new server name you want toorestore to</span></span>
- <span data-ttu-id="60fa3-168">Server di origine: specificare il nome di hello hello del server di si desidera toorestore da</span><span class="sxs-lookup"><span data-stu-id="60fa3-168">Source server: Provide hello name of hello server you want toorestore from</span></span>
- <span data-ttu-id="60fa3-169">Percorso: Non è possibile selezionare l'area di hello, per impostazione predefinita è uguale al server di origine hello</span><span class="sxs-lookup"><span data-stu-id="60fa3-169">Location: You cannot select hello region, by default it is same as hello source server</span></span>

```azurecli-interactive
az mysql server restore --resource-group mycliresource --name mycliserver-restored --restore-point-in-time "2017-05-4 03:10" --source-server-name mycliserver
```

<span data-ttu-id="60fa3-170">server hello toorestore e [tooa momento di ripristinare](./howto-restore-server-portal.md) prima tabella hello è stata eliminata.</span><span class="sxs-lookup"><span data-stu-id="60fa3-170">toorestore hello server and [restore tooa point-in-time](./howto-restore-server-portal.md) before hello table was deleted.</span></span> <span data-ttu-id="60fa3-171">Ripristino di un punto diverso di server tooa nel tempo crea un duplicato nuovo server come server originale hello come hello punto nel tempo specificato, purché tale valore entro il periodo di memorizzazione hello per le [livello di servizio](./concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="60fa3-171">Restoring a server tooa different point in time creates a duplicate new server as hello original server as of hello point in time you specify, provided that it is within hello retention period for your [service tier](./concepts-service-tiers.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="60fa3-172">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="60fa3-172">Next Steps</span></span>
<span data-ttu-id="60fa3-173">Questa esercitazione illustra come:</span><span class="sxs-lookup"><span data-stu-id="60fa3-173">In this tutorial you learned to:</span></span>
> [!div class="checklist"]
> * <span data-ttu-id="60fa3-174">Creare un database di Azure per MySQL</span><span class="sxs-lookup"><span data-stu-id="60fa3-174">Create an Azure Database for MySQL</span></span>
> * <span data-ttu-id="60fa3-175">Configurare firewall hello del server</span><span class="sxs-lookup"><span data-stu-id="60fa3-175">Configure hello server firewall</span></span>
> * <span data-ttu-id="60fa3-176">Utilizzare [strumento da riga di comando mysql](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate un database</span><span class="sxs-lookup"><span data-stu-id="60fa3-176">Use [mysql command line tool](https://dev.mysql.com/doc/refman/5.6/en/mysql.html) toocreate a database</span></span>
> * <span data-ttu-id="60fa3-177">Caricare dati di esempio</span><span class="sxs-lookup"><span data-stu-id="60fa3-177">Load sample data</span></span>
> * <span data-ttu-id="60fa3-178">Eseguire query sui dati</span><span class="sxs-lookup"><span data-stu-id="60fa3-178">Query data</span></span>
> * <span data-ttu-id="60fa3-179">Aggiornare i dati</span><span class="sxs-lookup"><span data-stu-id="60fa3-179">Update data</span></span>
> * <span data-ttu-id="60fa3-180">Ripristinare i dati</span><span class="sxs-lookup"><span data-stu-id="60fa3-180">Restore data</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="60fa3-181">Database di Azure per MySQL - Esempi di interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="60fa3-181">Azure Database for MySQL - Azure CLI samples</span></span>](./sample-scripts-azure-cli.md)
