---
title: Configurare e accedere ai log del server per PostgreSQL usando l'interfaccia della riga di comando di Azure | Microsoft Docs
description: Questo articolo descrive come configurare e accedere ai log del server in Database di Azure per PostgreSQL usando l'interfaccia della riga di comando di Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 26f8e12c493904f722cad5191ee053feff20f7fc
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="6279f-103">Configurare e accedere ai log del server usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="6279f-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="6279f-104">È possibile scaricare i log degli errori del server PostgreSQL usando l'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="6279f-104">You can download the PostgreSQL server error logs using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="6279f-105">Tuttavia, l'accesso ai log delle transazioni non è supportato.</span><span class="sxs-lookup"><span data-stu-id="6279f-105">However, access to transaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="6279f-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="6279f-106">Prerequisites</span></span>
<span data-ttu-id="6279f-107">Per proseguire con questa guida, si richiedono:</span><span class="sxs-lookup"><span data-stu-id="6279f-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="6279f-108">[Database di Azure per il server PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="6279f-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="6279f-109">Installare l'utilità della riga di comando dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-azure-cli) o usare Azure Cloud Shell nel browser.</span><span class="sxs-lookup"><span data-stu-id="6279f-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="6279f-110">Configurare la registrazione per Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6279f-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="6279f-111">È possibile configurare il server per l'accesso ai log di query e ai log degli errori.</span><span class="sxs-lookup"><span data-stu-id="6279f-111">You can configure the server to access query logs and error logs.</span></span> <span data-ttu-id="6279f-112">I log degli errori possono contenere informazioni su checkpoint, connessioni e vuoto automatico.</span><span class="sxs-lookup"><span data-stu-id="6279f-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="6279f-113">Abilitare la registrazione</span><span class="sxs-lookup"><span data-stu-id="6279f-113">Turn on logging</span></span>
2. <span data-ttu-id="6279f-114">Abilitare log\_statement e log\_min\_duration\_statement per abilitare la registrazione delle query</span><span class="sxs-lookup"><span data-stu-id="6279f-114">Update log\_statement and log\_min\_duration\_statement to enable query logging</span></span>
3. <span data-ttu-id="6279f-115">Abilitare il periodo di conservazione</span><span class="sxs-lookup"><span data-stu-id="6279f-115">Update retention period</span></span>

<span data-ttu-id="6279f-116">Per altre informazioni, vedere [Personalizzazione dei parametri di configurazione](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="6279f-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="6279f-117">Elencare i log per il database di Azure per il server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="6279f-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="6279f-118">Per elencare i file di log disponibili per il server, eseguire il comando [az postgres server-logs list](/cli/azure/postgres/server-logs#list).</span><span class="sxs-lookup"><span data-stu-id="6279f-118">To list the available log files for your server, run the [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="6279f-119">È possibile elencare i file di log per il server **mypgserver-20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup** e indirizzarlo a un file di testo denominato **log\_files\_list.txt.**</span><span class="sxs-lookup"><span data-stu-id="6279f-119">You can list the log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it to a text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-the-server"></a><span data-ttu-id="6279f-120">Scaricare i log dal server in locale</span><span class="sxs-lookup"><span data-stu-id="6279f-120">Download logs locally from the server</span></span>
<span data-ttu-id="6279f-121">Il comando [az postgres server-logs download](/cli/azure/postgres/server-logs#download) consente di scaricare i singoli file di log per il server.</span><span class="sxs-lookup"><span data-stu-id="6279f-121">The [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you to download individual log files for your server.</span></span> 

<span data-ttu-id="6279f-122">Questo esempio scarica il file di log specifico per il server **mypgserver-20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup** nell'ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="6279f-122">This example downloads the specific log file for the server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** to your local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="6279f-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="6279f-123">Next steps</span></span>
- <span data-ttu-id="6279f-124">Per altre informazioni sui log del server, vedere [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md) (Log del server in Database di Azure per PostgreSQL)</span><span class="sxs-lookup"><span data-stu-id="6279f-124">To learn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="6279f-125">Per altre informazioni sui parametri del server, vedere [Personalizzare i parametri di configurazione server usando l'interfaccia della riga di comando di Azure](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="6279f-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
