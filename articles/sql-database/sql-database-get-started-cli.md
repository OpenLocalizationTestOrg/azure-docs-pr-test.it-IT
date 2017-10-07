---
title: 'Interfaccia della riga di comando di Azure: creare un database SQL | Microsoft Docs'
description: Informazioni su come toocreate un server logico di Database SQL regola del firewall a livello di server e database che utilizzano hello CLI di Azure.
keywords: esercitazione sul database sql, creare un database sql
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,DBs & servers
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: azurecli
ms.topic: hero-article
ms.date: 04/17/2017
ms.author: carlrab
ms.openlocfilehash: 9b1ffb17eabeb70a000ff0c997128832b07aa4fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-single-azure-sql-database-using-hello-azure-cli"></a><span data-ttu-id="5efe6-104">Creare un singolo database di SQL Azure mediante Azure CLI hello</span><span class="sxs-lookup"><span data-stu-id="5efe6-104">Create a single Azure SQL database using hello Azure CLI</span></span>

<span data-ttu-id="5efe6-105">Hello CLI di Azure viene utilizzato toocreate e gestire le risorse di Azure dalla riga di comando hello o negli script.</span><span class="sxs-lookup"><span data-stu-id="5efe6-105">hello Azure CLI is used toocreate and manage Azure resources from hello command line or in scripts.</span></span> <span data-ttu-id="5efe6-106">Questa Guida dettagli hello Azure CLI toodeploy utilizzando un database SQL di Azure in un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) in un [server logico di Database SQL di Azure](sql-database-features.md).</span><span class="sxs-lookup"><span data-stu-id="5efe6-106">This guide details using hello Azure CLI toodeploy an Azure SQL database in an [Azure resource group](../azure-resource-manager/resource-group-overview.md) in an [Azure SQL Database logical server](sql-database-features.md).</span></span>

<span data-ttu-id="5efe6-107">Se non si ha una sottoscrizione di Azure, creare un [account gratuito](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) prima di iniziare.</span><span class="sxs-lookup"><span data-stu-id="5efe6-107">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5efe6-108">Se si sceglie tooinstall e utilizza hello CLI in locale, in questo argomento è necessario che sia in esecuzione hello Azure CLI versione 2.0.4 o versioni successive.</span><span class="sxs-lookup"><span data-stu-id="5efe6-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="5efe6-109">Eseguire `az --version` versione hello toofind.</span><span class="sxs-lookup"><span data-stu-id="5efe6-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="5efe6-110">Se è necessario tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5efe6-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="define-variables"></a><span data-ttu-id="5efe6-111">Definire le variabili</span><span class="sxs-lookup"><span data-stu-id="5efe6-111">Define variables</span></span>

<span data-ttu-id="5efe6-112">Definire le variabili da usare negli script hello in questa Guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="5efe6-112">Define variables for use in hello scripts in this quick start.</span></span>

```azurecli-interactive
# hello data center and resource name for your resources
export resourcegroupname = myResourceGroup
export location = westeurope
# hello logical server name: Use a random value or replace with your own value (do not capitalize)
export servername = server-$RANDOM
# Set an admin login and password for your database
export adminlogin = ServerAdmin
export password = ChangeYourAdminPassword1
# hello ip address range that you want tooallow tooaccess your DB
export startip = "0.0.0.0"
export endip = "0.0.0.0"
# hello database name
export databasename = mySampleDatabase
```

## <a name="create-a-resource-group"></a><span data-ttu-id="5efe6-113">Creare un gruppo di risorse</span><span class="sxs-lookup"><span data-stu-id="5efe6-113">Create a resource group</span></span>

<span data-ttu-id="5efe6-114">Creare un [gruppo di risorse](../azure-resource-manager/resource-group-overview.md) utilizzando hello [gruppo az creare](/cli/azure/group#create) comando.</span><span class="sxs-lookup"><span data-stu-id="5efe6-114">Create an [Azure resource group](../azure-resource-manager/resource-group-overview.md) using hello [az group create](/cli/azure/group#create) command.</span></span> <span data-ttu-id="5efe6-115">Un gruppo di risorse è un contenitore logico in cui le risorse di Azure vengono distribuite e gestite come gruppo.</span><span class="sxs-lookup"><span data-stu-id="5efe6-115">A resource group is a logical container into which Azure resources are deployed and managed as a group.</span></span> <span data-ttu-id="5efe6-116">esempio Hello crea un gruppo di risorse denominato `myResourceGroup` in hello `westeurope` percorso.</span><span class="sxs-lookup"><span data-stu-id="5efe6-116">hello following example creates a resource group named `myResourceGroup` in hello `westeurope` location.</span></span>

```azurecli-interactive
az group create --name $resourcegroupname --location $location
```
## <a name="create-a-logical-server"></a><span data-ttu-id="5efe6-117">Creare un server logico</span><span class="sxs-lookup"><span data-stu-id="5efe6-117">Create a logical server</span></span>

<span data-ttu-id="5efe6-118">Creare un [server logico di Database SQL di Azure](sql-database-features.md) utilizzando hello [az sql server creare](/cli/azure/sql/server#create) comando.</span><span class="sxs-lookup"><span data-stu-id="5efe6-118">Create an [Azure SQL Database logical server](sql-database-features.md) using hello [az sql server create](/cli/azure/sql/server#create) command.</span></span> <span data-ttu-id="5efe6-119">Un server logico contiene un gruppo di database gestiti come gruppo.</span><span class="sxs-lookup"><span data-stu-id="5efe6-119">A logical server contains a group of databases managed as a group.</span></span> <span data-ttu-id="5efe6-120">Hello seguente viene creato un server denominato in modo casuale nel gruppo di risorse con un account di accesso amministratore denominato `ServerAdmin` e la password `ChangeYourAdminPassword1`.</span><span class="sxs-lookup"><span data-stu-id="5efe6-120">hello following example creates a randomly named server in your resource group with an admin login named `ServerAdmin` and a password of `ChangeYourAdminPassword1`.</span></span> <span data-ttu-id="5efe6-121">Sostituire questi valori predefiniti con quelli desiderati.</span><span class="sxs-lookup"><span data-stu-id="5efe6-121">Replace these pre-defined values as desired.</span></span>

```azurecli-interactive
az sql server create --name $servername --resource-group $resourcegroupname --location $location \
    --admin-user $adminlogin --admin-password $password
```

## <a name="configure-a-server-firewall-rule"></a><span data-ttu-id="5efe6-122">Configurare una regola del firewall del server</span><span class="sxs-lookup"><span data-stu-id="5efe6-122">Configure a server firewall rule</span></span>

<span data-ttu-id="5efe6-123">Creare un [regola del firewall a livello di server Database SQL di Azure](sql-database-firewall-configure.md) utilizzando hello [firewall del server sql az creare](/cli/azure/sql/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="5efe6-123">Create an [Azure SQL Database server-level firewall rule](sql-database-firewall-configure.md) using hello [az sql server firewall create](/cli/azure/sql/server/firewall-rule#create) command.</span></span> <span data-ttu-id="5efe6-124">Una regola del firewall a livello di server consente a un'applicazione esterna, ad esempio SQL Server Management Studio o hello SQLCMD utility tooconnect tooa database SQL tramite firewall del servizio Database SQL hello.</span><span class="sxs-lookup"><span data-stu-id="5efe6-124">A server-level firewall rule allows an external application, such as SQL Server Management Studio or hello SQLCMD utility tooconnect tooa SQL database through hello SQL Database service firewall.</span></span> <span data-ttu-id="5efe6-125">Nell'esempio seguente di hello, firewall hello è aperta solo per le altre risorse di Azure.</span><span class="sxs-lookup"><span data-stu-id="5efe6-125">In hello following example, hello firewall is only opened for other Azure resources.</span></span> <span data-ttu-id="5efe6-126">connettività esterna tooenable, modifica hello tooan appropriato indirizzo per l'ambiente.</span><span class="sxs-lookup"><span data-stu-id="5efe6-126">tooenable external connectivity, change hello IP address tooan appropriate address for your environment.</span></span> <span data-ttu-id="5efe6-127">tooopen tutti gli indirizzi IP, utilizzare 0.0.0.0 come hello avvio indirizzo IP e 255.255.255.255 come hello indirizzo finale.</span><span class="sxs-lookup"><span data-stu-id="5efe6-127">tooopen all IP addresses, use 0.0.0.0 as hello starting IP address and 255.255.255.255 as hello ending address.</span></span>  

```azurecli-interactive
az sql server firewall-rule create --resource-group $resourcegroupname --server $servername \
    -n AllowYourIp --start-ip-address $startip --end-ip-address $endip
```

> [!NOTE]
> <span data-ttu-id="5efe6-128">Il database SQL comunica attraverso la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="5efe6-128">SQL Database communicates over port 1433.</span></span> <span data-ttu-id="5efe6-129">Se si sta tentando di tooconnect da una rete aziendale, può non essere consentito il traffico in uscita sulla porta 1433 dal firewall della rete.</span><span class="sxs-lookup"><span data-stu-id="5efe6-129">If you are trying tooconnect from within a corporate network, outbound traffic over port 1433 may not be allowed by your network's firewall.</span></span> <span data-ttu-id="5efe6-130">In questo caso, non sarà server di Database SQL di Azure in grado di tooconnect tooyour, a meno che il reparto IT consente di aprire la porta 1433.</span><span class="sxs-lookup"><span data-stu-id="5efe6-130">If so, you will not be able tooconnect tooyour Azure SQL Database server unless your IT department opens port 1433.</span></span>
>

## <a name="create-a-database-in-hello-server-with-sample-data"></a><span data-ttu-id="5efe6-131">Creare un database in server hello con dati di esempio</span><span class="sxs-lookup"><span data-stu-id="5efe6-131">Create a database in hello server with sample data</span></span>

<span data-ttu-id="5efe6-132">Creare un database con un [livello di prestazioni S0](sql-database-service-tiers.md) nel server di hello tramite hello [creare database di sql server az](/cli/azure/sql/db#create) comando.</span><span class="sxs-lookup"><span data-stu-id="5efe6-132">Create a database with an [S0 performance level](sql-database-service-tiers.md) in hello server using hello [az sql db create](/cli/azure/sql/db#create) command.</span></span> <span data-ttu-id="5efe6-133">esempio Hello crea un database denominato `mySampleDatabase` e carica i dati di esempio AdventureWorksLT di hello in questo database.</span><span class="sxs-lookup"><span data-stu-id="5efe6-133">hello following example creates a database called `mySampleDatabase` and loads hello AdventureWorksLT sample data into this database.</span></span> <span data-ttu-id="5efe6-134">Sostituire questi predefiniti i valori in base alle esigenze (altre guide introduttive in questa compilazione insieme ai valori hello in questa Guida introduttiva).</span><span class="sxs-lookup"><span data-stu-id="5efe6-134">Replace these predefined values as desired (other quick starts in this collection build upon hello values in this quick start).</span></span>

```azurecli-interactive
az sql db create --resource-group $resourcegroupname --server $servername \
    --name $databasename --sample-name AdventureWorksLT --service-objective S0
```

## <a name="clean-up-resources"></a><span data-ttu-id="5efe6-135">Pulire le risorse</span><span class="sxs-lookup"><span data-stu-id="5efe6-135">Clean up resources</span></span>

<span data-ttu-id="5efe6-136">Altre guide introduttive di questa raccolta si basano sui valori di questa guida introduttiva.</span><span class="sxs-lookup"><span data-stu-id="5efe6-136">Other quick starts in this collection build upon this quick start.</span></span> 

> [!TIP]
> <span data-ttu-id="5efe6-137">Se si intende toocontinue toowork con avvio rapido successive, non pulire le risorse di hello create in questa Guida introduttiva avviato.</span><span class="sxs-lookup"><span data-stu-id="5efe6-137">If you plan toocontinue on toowork with subsequent quick starts, do not clean up hello resources created in this quick start.</span></span> <span data-ttu-id="5efe6-138">Se non si prevede toocontinue, utilizzare hello seguendo i passaggi toodelete tutte le risorse create da questa Guida introduttiva in hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="5efe6-138">If you do not plan toocontinue, use hello following steps toodelete all resources created by this quick start in hello Azure portal.</span></span>
>

```azurecli-interactive
az group delete --name $resourcegroupname
```

## <a name="next-steps"></a><span data-ttu-id="5efe6-139">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5efe6-139">Next steps</span></span>

<span data-ttu-id="5efe6-140">Dopo aver creato un database, è possibile connettersi ed eseguire query usando gli strumenti preferiti.</span><span class="sxs-lookup"><span data-stu-id="5efe6-140">Now that you have a database, you can connect and query using your favorite tools.</span></span> <span data-ttu-id="5efe6-141">Per altre informazioni, scegliere uno strumento di seguito:</span><span class="sxs-lookup"><span data-stu-id="5efe6-141">Learn more by choosing your tool below:</span></span>

- [<span data-ttu-id="5efe6-142">SQL Server Management Studio</span><span class="sxs-lookup"><span data-stu-id="5efe6-142">SQL Server Management Studio</span></span>](sql-database-connect-query-ssms.md)
- [<span data-ttu-id="5efe6-143">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="5efe6-143">Visual Studio Code</span></span>](sql-database-connect-query-vscode.md)
- [<span data-ttu-id="5efe6-144">.NET</span><span class="sxs-lookup"><span data-stu-id="5efe6-144">.NET</span></span>](sql-database-connect-query-dotnet.md)
- [<span data-ttu-id="5efe6-145">PHP</span><span class="sxs-lookup"><span data-stu-id="5efe6-145">PHP</span></span>](sql-database-connect-query-php.md)
- [<span data-ttu-id="5efe6-146">Node.JS</span><span class="sxs-lookup"><span data-stu-id="5efe6-146">Node.js</span></span>](sql-database-connect-query-nodejs.md)
- [<span data-ttu-id="5efe6-147">Java</span><span class="sxs-lookup"><span data-stu-id="5efe6-147">Java</span></span>](sql-database-connect-query-java.md)
- [<span data-ttu-id="5efe6-148">Python</span><span class="sxs-lookup"><span data-stu-id="5efe6-148">Python</span></span>](sql-database-connect-query-python.md)
- [<span data-ttu-id="5efe6-149">Ruby</span><span class="sxs-lookup"><span data-stu-id="5efe6-149">Ruby</span></span>](sql-database-connect-query-ruby.md)

