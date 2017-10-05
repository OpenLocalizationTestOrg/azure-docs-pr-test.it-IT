---
title: Configurare i parametri del servizio in Database di Azure per PostgreSQL | Microsoft Docs
description: Questo articolo descrive come configurare i parametri del servizio in Database di Azure per PostgreSQL usando l'interfaccia della riga di comando di Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: c8a3b5a0225c2cede180d8d57681f2e1a6c6cc3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="7eb76-103">Personalizzare i parametri di configurazione server usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="7eb76-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="7eb76-104">È possibile elencare, visualizzare e aggiornare i parametri di configurazione per un server PostgreSQL di Azure usando l'interfaccia della riga di comando di Azure,</span><span class="sxs-lookup"><span data-stu-id="7eb76-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using the Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="7eb76-105">ma solo un subset delle configurazioni del motore viene esposto a livello di server e può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="7eb76-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="7eb76-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="7eb76-106">Prerequisites</span></span>
<span data-ttu-id="7eb76-107">Per proseguire con questa guida, si richiedono:</span><span class="sxs-lookup"><span data-stu-id="7eb76-107">To step through this how-to guide, you need:</span></span>
- <span data-ttu-id="7eb76-108">Un server e un database [Creare un database di Azure per PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="7eb76-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="7eb76-109">Installare l'utilità della riga di comando dell'[interfaccia della riga di comando di Azure 2.0](/cli/azure/install-azure-cli) o usare Azure Cloud Shell nel browser.</span><span class="sxs-lookup"><span data-stu-id="7eb76-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use the Azure Cloud Shell in the browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="7eb76-110">Elencare i parametri di configurazione del server per Database di Azure per il server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="7eb76-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="7eb76-111">Per elencare tutti i parametri modificabili in un server e i relativi valori, eseguire il comando [az postgres server configuration list](/cli/azure/postgres/server/configuration#list).</span><span class="sxs-lookup"><span data-stu-id="7eb76-111">To list all modifiable parameters in a server and their values, run the [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="7eb76-112">È possibile elencare i parametri di configurazione del server per il server **mypgserver-20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="7eb76-112">You can list the server configuration parameters for the server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="7eb76-113">Visualizzare i dettagli dei parametri di configurazione server</span><span class="sxs-lookup"><span data-stu-id="7eb76-113">Show server configuration parameter details</span></span>
<span data-ttu-id="7eb76-114">Per visualizzare i dettagli di un determinato parametro di configurazione per un server, eseguire il comando [az postgres server configuration show](/cli/azure/postgres/server/configuration#show).</span><span class="sxs-lookup"><span data-stu-id="7eb76-114">To show details about a particular configuration parameter for a server, run the [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="7eb76-115">Questo esempio mostra i dettagli del parametro di configurazione del server **log\_min\_messages** per il server **mypgserver-20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="7eb76-115">This example shows details of the **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="7eb76-116">Modificare il valore di un parametro di configurazione server</span><span class="sxs-lookup"><span data-stu-id="7eb76-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="7eb76-117">È anche possibile modificare il valore di un determinato parametro di configurazione del server e in questo modo viene aggiornato il valore di configurazione sottostante del motore del server PostgreSQL.</span><span class="sxs-lookup"><span data-stu-id="7eb76-117">You can also modify the value of a certain server configuration parameter, and this updates the underlying configuration value for the PostgreSQL server engine.</span></span> <span data-ttu-id="7eb76-118">Per aggiornare la configurazione, usare il comando [az postgres server configuration set](/cli/azure/postgres/server/configuration#set).</span><span class="sxs-lookup"><span data-stu-id="7eb76-118">To update the configuration use the [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="7eb76-119">Per aggiornare il parametro di configurazione del server **log\_min\_messages** per il server **mypgserver-20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup**:</span><span class="sxs-lookup"><span data-stu-id="7eb76-119">To update the **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="7eb76-120">Per reimpostare il valore di un parametro di configurazione, è sufficiente non inserire il parametro facoltativo `--value`. In questo caso, il servizio applicherà il valore predefinito.</span><span class="sxs-lookup"><span data-stu-id="7eb76-120">If you want to reset the value of a configuration parameter, you simply choose to leave out the optional `--value` parameter, and the service will apply the default value.</span></span> <span data-ttu-id="7eb76-121">Nell'esempio precedente sarà simile a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="7eb76-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="7eb76-122">In questo modo il parametro di configurazione **log\_min\_messages** viene reimpostato sul valore predefinito **WARNING**.</span><span class="sxs-lookup"><span data-stu-id="7eb76-122">This will reset the **log\_min\_messages** configuration to the default value **WARNING**.</span></span> <span data-ttu-id="7eb76-123">Per altre informazioni sulla configurazione server e sui valori consentiti, vedere la documentazione di PostgreSQL in [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html) (Configurazione server).</span><span class="sxs-lookup"><span data-stu-id="7eb76-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7eb76-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="7eb76-124">Next steps</span></span>
- <span data-ttu-id="7eb76-125">Per configurare e accedere ai log del server, vedere [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md) (Log del server in Database di Azure per PostgreSQL)</span><span class="sxs-lookup"><span data-stu-id="7eb76-125">To configure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
