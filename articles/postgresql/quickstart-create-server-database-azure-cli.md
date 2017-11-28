---
title: Creare un Database di Azure per PostgreSQL utilizzando hello CLI di Azure | Documenti Microsoft
description: Rapido avviare Guida toocreate e gestione dei Database di Azure per server PostgreSQL mediante Azure CLI (interfaccia della riga di comando).
services: postgresql
author: sanagama
ms.author: sanagama
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: quickstart
ms.date: 06/13/2017
ms.openlocfilehash: 946aa3cbf5ff9f5ac4e51248412d3da5d718141e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-using-hello-azure-cli"></a><span data-ttu-id="051c3-103">Creare un Database di Azure per PostgreSQL utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="051c3-103">Create an Azure Database for PostgreSQL using hello Azure CLI</span></span>
<span data-ttu-id="051c3-104">Il Database di Azure per PostgreSQL è un servizio gestito che consente di toorun, gestire e scalare database PostgreSQL a disponibilità elevata nel cloud hello.</span><span class="sxs-lookup"><span data-stu-id="051c3-104">Azure Database for PostgreSQL is a managed service that enables you toorun, manage, and scale highly available PostgreSQL databases in hello cloud.</span></span> <span data-ttu-id="051c3-105">Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="051c3-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="051c3-106">Questa Guida introduttiva viene illustrato come toocreate un Azure del Database per server PostgreSQL in un [gruppo di risorse](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) utilizzando hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="051c3-106">This quickstart shows you how toocreate an Azure Database for PostgreSQL server in an [Azure resource group](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview) using hello Azure CLI.</span></span>

<span data-ttu-id="051c3-107">Se non si ha una sottoscrizione di Azure, creare un account [gratuito](https://azure.microsoft.com/free/) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="051c3-107">If you don't have an Azure subscription, create a [free](https://azure.microsoft.com/free/) account before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="051c3-108">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che si esegue hello Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="051c3-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="051c3-109">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="051c3-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="051c3-110">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="051c3-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

<span data-ttu-id="051c3-111">Se si dispone di più sottoscrizioni, scegliere in cui verranno fatturata risorse hello la sottoscrizione appropriata hello.</span><span class="sxs-lookup"><span data-stu-id="051c3-111">If you have multiple subscriptions, choose hello appropriate subscription in which hello resource will be billed.</span></span> <span data-ttu-id="051c3-112">Selezionare un ID di sottoscrizione specifico sotto l'account tramite il comando [az account set](/cli/azure/account#set).</span><span class="sxs-lookup"><span data-stu-id="051c3-112">Select a specific subscription ID under your account using [az account set](/cli/azure/account#set) command.</span></span>
```azurecli-interactive
az account set --subscription 00000000-0000-0000-0000-000000000000
```

## <a name="create-a-resource-group"></a><span data-ttu-id="051c3-113">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="051c3-113">Create a resource group</span></span>

<span data-ttu-id="051c3-114">Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) utilizzando hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="051c3-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="051c3-115">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.</span><span class="sxs-lookup"><span data-stu-id="051c3-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="051c3-116">esempio Hello crea un gruppo di risorse denominato `myresourcegroup` in hello `westus` percorso.</span><span class="sxs-lookup"><span data-stu-id="051c3-116">hello following example creates a resource group named `myresourcegroup` in hello `westus` location.</span></span>
```azurecli-interactive
az group create --name myresourcegroup --location westus
```

## <a name="create-an-azure-database-for-postgresql-server"></a><span data-ttu-id="051c3-117">Creare un database di Azure per il server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="051c3-117">Create an Azure Database for PostgreSQL server</span></span>

<span data-ttu-id="051c3-118">Creare un [Database di Azure per server PostgreSQL](overview.md) utilizzando hello [az postgres server creare](/cli/azure/postgres/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="051c3-118">Create an [Azure Database for PostgreSQL server](overview.md) using hello [az postgres server create](/cli/azure/postgres/server#create) command.</span></span> <span data-ttu-id="051c3-119">Un server contiene un gruppo di database gestiti come gruppo.</span><span class="sxs-lookup"><span data-stu-id="051c3-119">A server contains a group of databases managed as a group.</span></span> 

<span data-ttu-id="051c3-120">esempio Hello crea un server denominato `mypgserver-20170401` nel gruppo di risorse `myresourcegroup` con account di accesso amministratore server `mylogin`.</span><span class="sxs-lookup"><span data-stu-id="051c3-120">hello following example creates a server named `mypgserver-20170401` in your resource group `myresourcegroup` with server admin login `mylogin`.</span></span> <span data-ttu-id="051c3-121">nome Hello di un server esegue il mapping nome tooDNS ed è pertanto necessario toobe globalmente univoco in Azure.</span><span class="sxs-lookup"><span data-stu-id="051c3-121">hello name of a server maps tooDNS name and is thus required toobe globally unique in Azure.</span></span> <span data-ttu-id="051c3-122">Hello Substitute `<server_admin_password>` con il proprio valore.</span><span class="sxs-lookup"><span data-stu-id="051c3-122">Substitute hello `<server_admin_password>` with your own value.</span></span>
```azurecli-interactive
az postgres server create --resource-group myresourcegroup --name mypgserver-20170401  --location westus --admin-user mylogin --admin-password <server_admin_password> --performance-tier Basic --compute-units 50 --version 9.6
```

> [!IMPORTANT]
> <span data-ttu-id="051c3-123">account di accesso amministratore server Hello e una password che è possibile specificare sono necessari toolog toohello server e i relativi database più avanti in questa Guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="051c3-123">hello server admin login and password that you specify here are required toolog in toohello server and its databases later in this quick start.</span></span> <span data-ttu-id="051c3-124">Prendere nota di queste informazioni per usarle in seguito.</span><span class="sxs-lookup"><span data-stu-id="051c3-124">Remember or record this information for later use.</span></span>

<span data-ttu-id="051c3-125">Per impostazione predefinita, il database **postgres** viene creato nel server.</span><span class="sxs-lookup"><span data-stu-id="051c3-125">By default, **postgres** database gets created under your server.</span></span> <span data-ttu-id="051c3-126">Hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database è un database predefinito può essere utilizzata per gli utenti, utilità e applicazioni di terze parti.</span><span class="sxs-lookup"><span data-stu-id="051c3-126">hello [postgres](https://www.postgresql.org/docs/9.6/static/app-initdb.html) database is a default database meant for use by users, utilities, and third-party applications.</span></span> 


## <a name="configure-a-server-level-firewall-rule"></a><span data-ttu-id="051c3-127">Configurare una regola del firewall a livello di server</span><span class="sxs-lookup"><span data-stu-id="051c3-127">Configure a server-level firewall rule</span></span>

<span data-ttu-id="051c3-128">Creare una regola firewall di livello server Azure PostgreSQL con hello [az postgres regola firewall del server-creare](/cli/azure/postgres/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="051c3-128">Create an Azure PostgreSQL server-level firewall rule with hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> <span data-ttu-id="051c3-129">Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) o [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server firewall hello Azure PostgreSQL servizio.</span><span class="sxs-lookup"><span data-stu-id="051c3-129">A server-level firewall rule allows an external application, such as [psql](https://www.postgresql.org/docs/9.2/static/app-psql.html) or [PgAdmin](https://www.pgadmin.org/) tooconnect tooyour server through hello Azure PostgreSQL service firewall.</span></span> 

<span data-ttu-id="051c3-130">È possibile impostare una regola del firewall che copre un intervallo IP toobe tooconnect in grado di dalla rete.</span><span class="sxs-lookup"><span data-stu-id="051c3-130">You can set a firewall rule that covers an IP range toobe able tooconnect from your network.</span></span> <span data-ttu-id="051c3-131">Hello seguente utilizza [az postgres regola firewall del server-creare](/cli/azure/postgres/server/firewall-rule#create) toocreate una regola del firewall `AllowAllIps` intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="051c3-131">hello following example uses [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) toocreate a firewall rule `AllowAllIps` for an IP address range.</span></span> <span data-ttu-id="051c3-132">tooopen tutti gli indirizzi IP, utilizzare 0.0.0.0 come hello avvio indirizzo IP e 255.255.255.255 come hello indirizzo finale.</span><span class="sxs-lookup"><span data-stu-id="051c3-132">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup --server mypgserver-20170401 --name AllowAllIps --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```

> [!NOTE]
> <span data-ttu-id="051c3-133">Il server PostgreSQL Azure comunica sulla porta 5432.</span><span class="sxs-lookup"><span data-stu-id="051c3-133">Azure PostgreSQL server communicates over port 5432.</span></span> <span data-ttu-id="051c3-134">Quando si esegue la connessione da una rete aziendale, il traffico in uscita sulla porta 5432 potrebbe non essere consentito dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="051c3-134">When connecting from within a corporate network, outbound traffic over port 5432 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="051c3-135">È aperto il reparto IT server porte 5432 tooconnect tooyour Database SQL di Azure.</span><span class="sxs-lookup"><span data-stu-id="051c3-135">Have your IT department open port 5432 tooconnect tooyour Azure SQL Database server.</span></span>

## <a name="get-hello-connection-information"></a><span data-ttu-id="051c3-136">Ottenere informazioni sulla connessione hello</span><span class="sxs-lookup"><span data-stu-id="051c3-136">Get hello connection information</span></span>

<span data-ttu-id="051c3-137">tooconnect tooyour server, sono necessarie credenziali di accesso e le informazioni di host tooprovide.</span><span class="sxs-lookup"><span data-stu-id="051c3-137">tooconnect tooyour server, you need tooprovide host information and access credentials.</span></span>
```azurecli-interactive
az postgres server show --resource-group myresourcegroup --name mypgserver-20170401
```

<span data-ttu-id="051c3-138">il risultato di Hello è nel formato JSON.</span><span class="sxs-lookup"><span data-stu-id="051c3-138">hello result is in JSON format.</span></span> <span data-ttu-id="051c3-139">Prendere nota di hello **administratorLogin** e **fullyQualifiedDomainName**.</span><span class="sxs-lookup"><span data-stu-id="051c3-139">Make a note of hello **administratorLogin** and **fullyQualifiedDomainName**.</span></span>
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

## <a name="connect-toopostgresql-database-using-psql"></a><span data-ttu-id="051c3-140">La connessione a database tooPostgreSQL utilizzando psql</span><span class="sxs-lookup"><span data-stu-id="051c3-140">Connect tooPostgreSQL database using psql</span></span>

<span data-ttu-id="051c3-141">Se il computer client abbia PostgreSQL installato, è possibile utilizzare un'istanza locale di [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server.</span><span class="sxs-lookup"><span data-stu-id="051c3-141">If your client computer has PostgreSQL installed, you can use a local instance of [psql](https://www.postgresql.org/docs/9.6/static/app-psql.html) tooconnect tooan Azure PostgreSQL server.</span></span> <span data-ttu-id="051c3-142">Consente di usare ora il server Azure PostgreSQL toohello tooconnect di hello psql utilità della riga di comando.</span><span class="sxs-lookup"><span data-stu-id="051c3-142">Let's now use hello psql command-line utility tooconnect toohello Azure PostgreSQL server.</span></span>

1. <span data-ttu-id="051c3-143">Eseguire hello seguente psql comando tooconnect tooan Database di Azure per server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="051c3-143">Run hello following psql command tooconnect tooan Azure Database for PostgreSQL server</span></span>
```azurecli-interactive
psql --host=<servername> --port=<port> --username=<user@servername> --dbname=<dbname>
```

  <span data-ttu-id="051c3-144">Ad esempio, hello comando seguente si connette a database predefinito toohello chiamato **postgres** sul server PostgreSQL **mypgserver 20170401.postgres.database.azure.com** utilizzando le credenziali di accesso.</span><span class="sxs-lookup"><span data-stu-id="051c3-144">For example, hello following command connects toohello default database called **postgres** on your PostgreSQL server **mypgserver-20170401.postgres.database.azure.com** using access credentials.</span></span> <span data-ttu-id="051c3-145">Immettere hello `<server_admin_password>` scelto quando viene richiesta la password.</span><span class="sxs-lookup"><span data-stu-id="051c3-145">Enter hello `<server_admin_password>` you chose when prompted for password.</span></span>
  
  ```azurecli-interactive
psql --host=mypgserver-20170401.postgres.database.azure.com --port=5432 --username=mylogin@mypgserver-20170401 --dbname=postgres
```

2.  <span data-ttu-id="051c3-146">Dopo avere connesso toohello server, è possibile creare un database vuoto al prompt dei comandi hello.</span><span class="sxs-lookup"><span data-stu-id="051c3-146">Once you are connected toohello server, create a blank database at hello prompt.</span></span>
```sql
CREATE DATABASE mypgsqldb;
```

3.  <span data-ttu-id="051c3-147">Al prompt dei comandi hello, eseguire hello seguente database toohello appena creato di comando tooswitch connessione **mypgsqldb**:</span><span class="sxs-lookup"><span data-stu-id="051c3-147">At hello prompt, execute hello following command tooswitch connection toohello newly created database **mypgsqldb**:</span></span>
```sql
\c mypgsqldb
```

## <a name="connect-toopostgresql-database-using-pgadmin"></a><span data-ttu-id="051c3-148">La connessione a database tooPostgreSQL utilizzando pgAdmin</span><span class="sxs-lookup"><span data-stu-id="051c3-148">Connect tooPostgreSQL database using pgAdmin</span></span>

<span data-ttu-id="051c3-149">tooconnect tooAzure PostgreSQL server utilizzando lo strumento GUI hello _pgAdmin_</span><span class="sxs-lookup"><span data-stu-id="051c3-149">tooconnect tooAzure PostgreSQL server using hello GUI tool _pgAdmin_</span></span>
1.  <span data-ttu-id="051c3-150">Avviare hello _pgAdmin_ applicazione nel computer client.</span><span class="sxs-lookup"><span data-stu-id="051c3-150">Launch hello _pgAdmin_ application on your client computer.</span></span> <span data-ttu-id="051c3-151">È possibile installare _pgAdmin_ da http://www.pgadmin.org/.</span><span class="sxs-lookup"><span data-stu-id="051c3-151">You can install _pgAdmin_ from http://www.pgadmin.org/.</span></span>
2.  <span data-ttu-id="051c3-152">Scegliere **aggiungere nuovi Server** da hello **collegamenti rapidi** menu.</span><span class="sxs-lookup"><span data-stu-id="051c3-152">Choose **Add New Server** from hello **Quick Links** menu.</span></span>
3.  <span data-ttu-id="051c3-153">In hello **Create - Server** la finestra di dialogo **generale** , immettere un nome descrittivo univoco per il server di hello.</span><span class="sxs-lookup"><span data-stu-id="051c3-153">In hello **Create - Server** dialog box **General** tab, enter a unique friendly Name for hello server.</span></span> <span data-ttu-id="051c3-154">Ad esempio, **Azure PostgreSQL Server**.</span><span class="sxs-lookup"><span data-stu-id="051c3-154">Say **Azure PostgreSQL Server**.</span></span>
 <span data-ttu-id="051c3-155">![Strumento pgAdmin - Finestra di creazione del server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span><span class="sxs-lookup"><span data-stu-id="051c3-155">![pgAdmin tool - create - server](./media/quickstart-create-server-database-azure-cli/1-pgadmin-create-server.png)</span></span>
4.  <span data-ttu-id="051c3-156">In hello **Create - Server** nella finestra di dialogo **connessione** scheda:</span><span class="sxs-lookup"><span data-stu-id="051c3-156">In hello **Create - Server** dialog box, **Connection** tab:</span></span>
    - <span data-ttu-id="051c3-157">Immettere il nome di server completo hello (ad esempio, **mypgserver 20170401.postgres.database.azure.com**) in hello **nome Host / indirizzo** casella.</span><span class="sxs-lookup"><span data-stu-id="051c3-157">Enter hello fully qualified server name (for example, **mypgserver-20170401.postgres.database.azure.com**) in hello **Host Name/ Address** box.</span></span> 
    - <span data-ttu-id="051c3-158">Immettere la porta 5432 in hello **porta** casella.</span><span class="sxs-lookup"><span data-stu-id="051c3-158">Enter port 5432 into hello **Port** box.</span></span> 
    - <span data-ttu-id="051c3-159">Immettere hello **accesso di amministratore di Server (user@mypgserver)** ottenuto in precedenza in questa Guida introduttiva e la password immessa al momento della creazione server hello in hello **Username** e **Password** caselle, rispettivamente.</span><span class="sxs-lookup"><span data-stu-id="051c3-159">Enter hello **Server admin login (user@mypgserver)** obtained earlier in this quickstart and password you entered when you created hello server into hello **Username** and **Password** boxes, respectively.</span></span>
    - <span data-ttu-id="051c3-160">Selezionare **SSL Mode** (Modalità SSL) e impostare **Require** (Richiedi).</span><span class="sxs-lookup"><span data-stu-id="051c3-160">Select **SSL Mode** as **Require**.</span></span> <span data-ttu-id="051c3-161">Per impostazione predefinita, tutti i server PostgreSQL Azure vengono creati con l'opzione di applicazione del protocollo SSL attivata.</span><span class="sxs-lookup"><span data-stu-id="051c3-161">By default, all Azure PostgreSQL servers are created with SSL enforcing turned ON.</span></span> <span data-ttu-id="051c3-162">tooturn OFF applica SSL, vedere i dettagli nella [applicazione SSL](./concepts-ssl-connection-security.md).</span><span class="sxs-lookup"><span data-stu-id="051c3-162">tooturn OFF SSL enforcing, see details in [Enforcing SSL](./concepts-ssl-connection-security.md).</span></span>

    ![pgAdmin - Finestra di creazione del server](./media/quickstart-create-server-database-azure-cli/2-pgadmin-create-server.png)
5.  <span data-ttu-id="051c3-164">Fare clic su **Salva**.</span><span class="sxs-lookup"><span data-stu-id="051c3-164">Click **Save**.</span></span>
6.  <span data-ttu-id="051c3-165">Nel riquadro a sinistra del Visualizzatore hello, espandere hello **gruppi di Server**.</span><span class="sxs-lookup"><span data-stu-id="051c3-165">In hello Browser left pane, expand hello **Server Groups**.</span></span> <span data-ttu-id="051c3-166">Scegliere il server **Azure PostgreSQL Server**.</span><span class="sxs-lookup"><span data-stu-id="051c3-166">Choose your server **Azure PostgreSQL Server**.</span></span>
7.  <span data-ttu-id="051c3-167">Scegliere hello **Server** connessi e quindi scegliere **database** sotto di esso.</span><span class="sxs-lookup"><span data-stu-id="051c3-167">Choose hello **Server** you connected to, and then choose **Databases** under it.</span></span> 
8.  <span data-ttu-id="051c3-168">Fare clic su **database** tooCreate un Database.</span><span class="sxs-lookup"><span data-stu-id="051c3-168">Right-click on **Databases** tooCreate a Database.</span></span>
9.  <span data-ttu-id="051c3-169">Scegliere un nome di database **mypgsqldb** proprietario hello per tale account di accesso amministratore server e **mylogin**.</span><span class="sxs-lookup"><span data-stu-id="051c3-169">Choose a database name **mypgsqldb** and hello owner for it as server admin login **mylogin**.</span></span>
10. <span data-ttu-id="051c3-170">Fare clic su **salvare** toocreate un database vuoto.</span><span class="sxs-lookup"><span data-stu-id="051c3-170">Click **Save** toocreate a blank database.</span></span>
11. <span data-ttu-id="051c3-171">In hello **Browser**, espandere hello **server** gruppo.</span><span class="sxs-lookup"><span data-stu-id="051c3-171">In hello **Browser**, expand hello **Servers** group.</span></span> <span data-ttu-id="051c3-172">Espandere il server di hello è stato creato e vedere database hello **mypgsqldb** in essa contenute.</span><span class="sxs-lookup"><span data-stu-id="051c3-172">Expand hello server you created, and see hello database **mypgsqldb** under it.</span></span>
 <span data-ttu-id="051c3-173">![pgAdmin - Finestra di creazione del database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span><span class="sxs-lookup"><span data-stu-id="051c3-173">![pgAdmin - Create - Database](./media/quickstart-create-server-database-azure-cli/3-pgadmin-database.png)</span></span>


## <a name="clean-up-resources"></a><span data-ttu-id="051c3-174">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="051c3-174">Clean up resources</span></span>

<span data-ttu-id="051c3-175">Pulizia di tutte le risorse è stato creato in avvio rapido di hello eliminando hello [gruppo di risorse](../azure-resource-manager/resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="051c3-175">Clean up all resources you created in hello quickstart by deleting hello [Azure resource group](../azure-resource-manager/resource-group-overview.md).</span></span>

> [!TIP]
> <span data-ttu-id="051c3-176">Altre guide di avvio rapido di questa raccolta si basano sulla presente guida di avvio rapido.</span><span class="sxs-lookup"><span data-stu-id="051c3-176">Other quickstarts in this collection build upon this quick start.</span></span> <span data-ttu-id="051c3-177">Se si intende toocontinue toowork con successive Guide rapide, eseguire la pulizia hello le risorse create in questa Guida rapida.</span><span class="sxs-lookup"><span data-stu-id="051c3-177">If you plan toocontinue on toowork with subsequent quickstarts, do not clean up hello resources created in this quickstart.</span></span> <span data-ttu-id="051c3-178">Se non si prevede toocontinue, utilizzare hello seguendo i passaggi toodelete tutte le risorse create da questa Guida rapida di hello CLI di Azure.</span><span class="sxs-lookup"><span data-stu-id="051c3-178">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quickstart in hello Azure CLI.</span></span>

```azurecli-interactive
az group delete --name myresourcegroup
```

<span data-ttu-id="051c3-179">Se si sarebbe analogo toodelete hello un nuovo server, è possibile eseguire [dell'eliminazione del server postgres az](/cli/azure/postgres/server#delete) comando.</span><span class="sxs-lookup"><span data-stu-id="051c3-179">If you just would like toodelete hello one newly created server, you can run [az postgres server delete](/cli/azure/postgres/server#delete) command.</span></span>
```azurecli-interactive
az postgres server delete --resource-group myresourcegroup --name mypgserver-20170401
```

## <a name="next-steps"></a><span data-ttu-id="051c3-180">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="051c3-180">Next steps</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="051c3-181">Eseguire la migrazione del database usando le funzionalità di esportazione e importazione</span><span class="sxs-lookup"><span data-stu-id="051c3-181">Migrate your database using Export and Import</span></span>](./howto-migrate-using-export-and-import.md)
