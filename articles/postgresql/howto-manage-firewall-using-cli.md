---
title: Creare e gestire regole del firewall di Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure | Microsoft Docs
description: Questo articolo descrive come creare e gestire regole del firewall di Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 6f081416dd7d78f0153b3fda21a340a8c1a70c5f
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="c2c1d-103">Creare e gestire regole del firewall di Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="c2c1d-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="c2c1d-104">Le regole del firewall a livello di server consentono agli amministratori di gestire l'accesso a un'istanza di Database di Azure per il server PostgreSQL da uno specifico indirizzo IP o intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-104">Server-level firewall rules enable administrators to manage access to an Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="c2c1d-105">Usando pratici comandi dell'interfaccia della riga di comando di Azure è possibile creare, aggiornare, eliminare, elencare e visualizzare le regole del firewall per gestire il server.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="c2c1d-106">Per una panoramica dei firewall di Database di Azure per PostgreSQL, vedere [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md) (Regole del firewall di Database di Azure per il server PostgreSQL)</span><span class="sxs-lookup"><span data-stu-id="c2c1d-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2c1d-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="c2c1d-107">Prerequisites</span></span>
<span data-ttu-id="c2c1d-108">Per proseguire con questa guida, si richiedono:</span><span class="sxs-lookup"><span data-stu-id="c2c1d-108">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="c2c1d-109">Un [server e un database di Database di Azure per PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="c2c1d-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="c2c1d-110">Installare l'utilità della riga di comando [Azure CLI 2.0](/cli/azure/install-azure-cli) o usare Azure Cloud Shell nel browser.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="c2c1d-111">Configurare le regole del firewall di Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="c2c1d-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="c2c1d-112">I comandi [az postgres server firewall-rule-](/cli/azure/postgres/server/firewall-rule) vengono usati per configurare le regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-112">The [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used to configure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="c2c1d-113">Elencare le regole del firewall</span><span class="sxs-lookup"><span data-stu-id="c2c1d-113">List firewall rules</span></span> 
<span data-ttu-id="c2c1d-114">Per elencare le regole del firewall del server esistenti sul server, eseguire il comando [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list).</span><span class="sxs-lookup"><span data-stu-id="c2c1d-114">To list the existing server firewall rules on the server, run the [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="c2c1d-115">L'output elenca le eventuali regole presenti, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-115">The output lists the rules if any, by default in JSON format.</span></span> <span data-ttu-id="c2c1d-116">È possibile usare l'opzione `--output table` per ottenere un formato di tabella più leggibile come output.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-116">You may use the switch `--output table` for a more readable table format as the output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="c2c1d-117">Creare la regola del firewall</span><span class="sxs-lookup"><span data-stu-id="c2c1d-117">Create firewall rule</span></span>
<span data-ttu-id="c2c1d-118">Per creare una nuova regola del firewall sul server, eseguire il comando [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create).</span><span class="sxs-lookup"><span data-stu-id="c2c1d-118">To create a new firewall rule on the server, run the [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="c2c1d-119">Questo esempio consente un intervallo di tutti gli indirizzi IP per accedere al server **mypgserver-20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="c2c1d-119">This example allows a range of all IP addresses to access the server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="c2c1d-120">Per consentire l'accesso a un solo indirizzo IP, specificare lo stesso valore come indirizzo IP iniziale e finale, come nell'esempio seguente.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-120">To allow a singular IP address to access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="c2c1d-121">Al termine dell'operazione, l'output del comando elenca i dettagli della regola del firewall creata, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-121">Upon success, the command output lists the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="c2c1d-122">Se si verifica un errore, l'output visualizza invece il testo di un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-122">If there is a failure, the output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="c2c1d-123">Aggiornare la regola del firewall</span><span class="sxs-lookup"><span data-stu-id="c2c1d-123">Update firewall rule</span></span> 
<span data-ttu-id="c2c1d-124">Aggiornare una regola del firewall esistente sul server usando il comando [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update).</span><span class="sxs-lookup"><span data-stu-id="c2c1d-124">Update an existing firewall rule on the server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="c2c1d-125">Specificare il nome della regola del firewall esistente come input e gli attributi dell'indirizzo IP iniziale e finale per l'aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-125">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="c2c1d-126">Al termine dell'operazione, l'output del comando elenca i dettagli della regola del firewall aggiornata, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-126">Upon success, the command output lists the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="c2c1d-127">Se si verifica un errore, l'output visualizza invece il testo di un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-127">If there is a failure, the output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="c2c1d-128">Se la regola del firewall non esiste, viene creata dal comando di aggiornamento.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-128">If the firewall rule does not exist, it gets created by the update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="c2c1d-129">Visualizzare i dettagli di una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="c2c1d-129">Show firewall rule details</span></span>
<span data-ttu-id="c2c1d-130">È inoltre possibile visualizzare i dettagli di una regola del firewall esistente per un server eseguendo il comando [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show).</span><span class="sxs-lookup"><span data-stu-id="c2c1d-130">You can also show the existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="c2c1d-131">Al termine dell'operazione, l'output del comando elenca i dettagli della regola del firewall specificata, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-131">Upon success, the command output lists the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="c2c1d-132">Se si verifica un errore, l'output visualizza invece il testo di un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-132">If there is a failure, the output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="c2c1d-133">Eliminare la regola del firewall</span><span class="sxs-lookup"><span data-stu-id="c2c1d-133">Delete firewall rule</span></span>
<span data-ttu-id="c2c1d-134">Per revocare l'accesso per un intervallo IP dal server, eliminare una regola del firewall esistente eseguendo il comando [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete).</span><span class="sxs-lookup"><span data-stu-id="c2c1d-134">To revoke access for an IP range from the server, delete an existing firewall rule by executing the [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="c2c1d-135">Specificare il nome della regola del firewall esistente.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-135">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="c2c1d-136">Al completamento dell'operazione non verrà visualizzato alcun output.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-136">Upon success, there is no output.</span></span> <span data-ttu-id="c2c1d-137">In caso di errore, viene restituito il testo di un messaggio di errore.</span><span class="sxs-lookup"><span data-stu-id="c2c1d-137">Upon failure, the error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c2c1d-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="c2c1d-138">Next steps</span></span>
- <span data-ttu-id="c2c1d-139">Analogamente, è possibile usare un Web browser per [creare e gestire le regole del firewall di Database di Azure per PostgreSQL usando il portale di Azure](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="c2c1d-139">Similarly, you can use a web browser to [Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="c2c1d-140">Altre informazioni sulle [regole del firewall di Database di Azure per il server PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="c2c1d-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="c2c1d-141">Per informazioni sulla connessione a un'istanza di Database di Azure per il server PostgreSQL, vedere [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md) (Raccolte di connessioni per Database di Azure per PostgreSQL)</span><span class="sxs-lookup"><span data-stu-id="c2c1d-141">For help in connecting to an Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
