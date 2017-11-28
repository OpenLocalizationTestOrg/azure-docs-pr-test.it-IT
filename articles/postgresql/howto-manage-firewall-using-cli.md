---
title: aaaCreate e gestire i Database di Azure per le regole firewall PostgreSQL mediante Azure CLI | Documenti Microsoft
description: Questo articolo viene descritto come toocreate e gestire i Database di Azure per le regole firewall PostgreSQL tramite riga di comando CLI di Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 06e34c9e3996c2ec3df63191d794bc34d0ca0cf2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-postgresql-firewall-rules-using-azure-cli"></a><span data-ttu-id="0e65d-103">Creare e gestire regole del firewall di Database di Azure per PostgreSQL tramite l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="0e65d-103">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="0e65d-104">Le regole del firewall a livello di server abilitare amministratori toomanage accesso tooan Database di Azure per PostgreSQL Server da un indirizzo IP specifico o l'intervallo di indirizzi IP.</span><span class="sxs-lookup"><span data-stu-id="0e65d-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for PostgreSQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="0e65d-105">Usare i comandi CLI di Azure pratici, è possibile creare, aggiornare, eliminare, elencare e Mostra toomanage regole firewall del server.</span><span class="sxs-lookup"><span data-stu-id="0e65d-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="0e65d-106">Per una panoramica dei firewall di Database di Azure per PostgreSQL, vedere [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md) (Regole del firewall di Database di Azure per il server PostgreSQL)</span><span class="sxs-lookup"><span data-stu-id="0e65d-106">For an overview of Azure Database for PostgreSQL firewalls, see [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0e65d-107">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="0e65d-107">Prerequisites</span></span>
<span data-ttu-id="0e65d-108">toostep tramite questa procedura-tooguide, è necessario:</span><span class="sxs-lookup"><span data-stu-id="0e65d-108">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="0e65d-109">Un [server e un database di Database di Azure per PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="0e65d-109">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="0e65d-110">Installare [CLI di Azure 2.0](/cli/azure/install-azure-cli) riga di comando utilità oppure utilizzare hello Azure Cloud Shell nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="0e65d-110">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-firewall-rules-for-azure-database-for-postgresql"></a><span data-ttu-id="0e65d-111">Configurare le regole del firewall di Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="0e65d-111">Configure firewall rules for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="0e65d-112">Hello [az postgres regola firewall del server-](/cli/azure/postgres/server/firewall-rule) comandi sono utilizzati tooconfigure regole del firewall.</span><span class="sxs-lookup"><span data-stu-id="0e65d-112">hello [az postgres server firewall-rule](/cli/azure/postgres/server/firewall-rule) commands are used tooconfigure firewall rules.</span></span>

## <a name="list-firewall-rules"></a><span data-ttu-id="0e65d-113">Elencare le regole del firewall</span><span class="sxs-lookup"><span data-stu-id="0e65d-113">List firewall rules</span></span> 
<span data-ttu-id="0e65d-114">toolist hello esistente, le regole firewall del server nel server di hello, eseguire hello [elenco regola firewall di az postgres server](/cli/azure/postgres/server/firewall-rule#list) comando.</span><span class="sxs-lookup"><span data-stu-id="0e65d-114">toolist hello existing server firewall rules on hello server, run hello [az postgres server firewall-rule list](/cli/azure/postgres/server/firewall-rule#list) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="0e65d-115">output di Hello Elenca le regole di hello, se presente, per impostazione predefinita in JSON di formato.</span><span class="sxs-lookup"><span data-stu-id="0e65d-115">hello output lists hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="0e65d-116">È possibile utilizzare l'opzione hello `--output table` per un formato più leggibile di tabella come output di hello.</span><span class="sxs-lookup"><span data-stu-id="0e65d-116">You may use hello switch `--output table` for a more readable table format as hello output.</span></span>
```azurecli-interactive
az postgres server firewall-rule list --resource-group myresourcegroup --server mypgserver-20170401 --output table
```
## <a name="create-firewall-rule"></a><span data-ttu-id="0e65d-117">Creare la regola del firewall</span><span class="sxs-lookup"><span data-stu-id="0e65d-117">Create firewall rule</span></span>
<span data-ttu-id="0e65d-118">una nuova regola firewall nel server di hello, eseguire hello toocreate [az postgres regola firewall del server-creare](/cli/azure/postgres/server/firewall-rule#create) comando.</span><span class="sxs-lookup"><span data-stu-id="0e65d-118">toocreate a new firewall rule on hello server, run hello [az postgres server firewall-rule create](/cli/azure/postgres/server/firewall-rule#create) command.</span></span> 

<span data-ttu-id="0e65d-119">In questo esempio consente un intervallo di tutti i server di hello tooaccess di indirizzi IP **mypgserver 20170401.postgres.database.azure.com**</span><span class="sxs-lookup"><span data-stu-id="0e65d-119">This example allows a range of all IP addresses tooaccess hello server **mypgserver-20170401.postgres.database.azure.com**</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
```
<span data-ttu-id="0e65d-120">tooallow un tooaccess di indirizzo IP specifico, fornire hello stesso indirizzo come hello IP iniziale e IP finale, come nel seguente esempio.</span><span class="sxs-lookup"><span data-stu-id="0e65d-120">tooallow a singular IP address tooaccess, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az postgres server firewall-rule create --resource-group myresourcegroup  
--server mypgserver-20170401 --name "AllowSingleIpAddress" --start-ip-address 13.83.152.1 --end-ip-address 13.83.152.1
```
<span data-ttu-id="0e65d-121">Al completamento dell'operazione, l'output del comando hello Elenca i dettagli di hello hello regola del firewall creata per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0e65d-121">Upon success, hello command output lists hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="0e65d-122">Se si verifica un errore, hello output invece showserror testo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="0e65d-122">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="update-firewall-rule"></a><span data-ttu-id="0e65d-123">Aggiornare la regola del firewall</span><span class="sxs-lookup"><span data-stu-id="0e65d-123">Update firewall rule</span></span> 
<span data-ttu-id="0e65d-124">Aggiornare una regola firewall esistente sul server hello utilizzando [aggiornamento regola firewall del server az postgres](/cli/azure/postgres/server/firewall-rule#update) comando.</span><span class="sxs-lookup"><span data-stu-id="0e65d-124">Update an existing firewall rule on hello server using [az postgres server firewall-rule update](/cli/azure/postgres/server/firewall-rule#update) command.</span></span> <span data-ttu-id="0e65d-125">Specificare il nome di hello della regola firewall esistente hello come input e hello inizio IP e fine IP attributi tooupdate.</span><span class="sxs-lookup"><span data-stu-id="0e65d-125">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az postgres server firewall-rule update --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.255
```
<span data-ttu-id="0e65d-126">Al completamento dell'operazione, l'output del comando hello Elenca i dettagli di hello hello regola del firewall che sono state aggiornate, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0e65d-126">Upon success, hello command output lists hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="0e65d-127">Se si verifica un errore, hello output invece showserror testo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="0e65d-127">If there is a failure, hello output showserror message text instead.</span></span>
> [!NOTE]
> <span data-ttu-id="0e65d-128">Se non esiste una regola del firewall hello, viene creato dal comando di aggiornamento hello.</span><span class="sxs-lookup"><span data-stu-id="0e65d-128">If hello firewall rule does not exist, it gets created by hello update command.</span></span>

## <a name="show-firewall-rule-details"></a><span data-ttu-id="0e65d-129">Visualizzare i dettagli di una regola del firewall</span><span class="sxs-lookup"><span data-stu-id="0e65d-129">Show firewall rule details</span></span>
<span data-ttu-id="0e65d-130">È inoltre possibile visualizzare firewall esistente hello dettagli regola per un server eseguendo [Mostra regola firewall di az postgres server](/cli/azure/postgres/server/firewall-rule#show) comando.</span><span class="sxs-lookup"><span data-stu-id="0e65d-130">You can also show hello existing firewall rule details for a server by running [az postgres server firewall-rule show](/cli/azure/postgres/server/firewall-rule#show) command.</span></span>
```azurecli-interactive
az postgres server firewall-rule show --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="0e65d-131">Al completamento dell'operazione, l'output del comando hello Elenca i dettagli di hello hello regola del firewall che è stato specificato, per impostazione predefinita in formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0e65d-131">Upon success, hello command output lists hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="0e65d-132">Se si verifica un errore, hello output invece showserror testo del messaggio.</span><span class="sxs-lookup"><span data-stu-id="0e65d-132">If there is a failure, hello output showserror message text instead.</span></span>

## <a name="delete-firewall-rule"></a><span data-ttu-id="0e65d-133">Eliminare la regola del firewall</span><span class="sxs-lookup"><span data-stu-id="0e65d-133">Delete firewall rule</span></span>
<span data-ttu-id="0e65d-134">accesso toorevoke per un intervallo IP dal server di hello, eliminare una regola firewall esistente eseguendo hello [az postgres regola firewall del server-eliminare](/cli/azure/postgres/server/firewall-rule#delete) comando.</span><span class="sxs-lookup"><span data-stu-id="0e65d-134">toorevoke access for an IP range from hello server, delete an existing firewall rule by executing hello [az postgres server firewall-rule delete](/cli/azure/postgres/server/firewall-rule#delete) command.</span></span> <span data-ttu-id="0e65d-135">Specificare il nome di hello della regola firewall esistente hello.</span><span class="sxs-lookup"><span data-stu-id="0e65d-135">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az postgres server firewall-rule delete --resource-group myresourcegroup --server mypgserver-20170401 --name "AllowIpRange"
```
<span data-ttu-id="0e65d-136">Al completamento dell'operazione non verrà visualizzato alcun output.</span><span class="sxs-lookup"><span data-stu-id="0e65d-136">Upon success, there is no output.</span></span> <span data-ttu-id="0e65d-137">In caso di errore, viene restituito testo del messaggio hello.</span><span class="sxs-lookup"><span data-stu-id="0e65d-137">Upon failure, hello error message text is returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0e65d-138">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0e65d-138">Next steps</span></span>
- <span data-ttu-id="0e65d-139">Analogamente, è possibile utilizzare un web browser troppo[creare e gestire i Database di Azure per le regole firewall PostgreSQL utilizzando hello portale di Azure](howto-manage-firewall-using-portal.md)</span><span class="sxs-lookup"><span data-stu-id="0e65d-139">Similarly, you can use a web browser too[Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal](howto-manage-firewall-using-portal.md)</span></span>
- <span data-ttu-id="0e65d-140">Altre informazioni sulle [regole del firewall di Database di Azure per il server PostgreSQL](concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="0e65d-140">Understand more about [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md)</span></span>
- <span data-ttu-id="0e65d-141">Per informazioni sulla connessione tooan Database di Azure per server PostgreSQL, vedere [raccolte di connessioni per il Database di Azure per PostgreSQL](concepts-connection-libraries.md)</span><span class="sxs-lookup"><span data-stu-id="0e65d-141">For help in connecting tooan Azure Database for PostgreSQL server, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md)</span></span>
