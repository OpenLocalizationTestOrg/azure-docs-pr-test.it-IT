---
title: parametri del servizio hello aaaConfigure nel Database di Azure per PostgreSQL | Documenti Microsoft
description: In questo articolo viene descritto come parametri del servizio hello tooconfigure nel Database di Azure per l'utilizzo di PostgreSQL hello della riga di comando CLI di Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 84a11de24ba87fc0eb6744aaa4b53f65a183903d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="customize-server-configuration-parameters-using-azure-cli"></a><span data-ttu-id="d79b2-103">Personalizzare i parametri di configurazione server usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="d79b2-103">Customize server configuration parameters using Azure CLI</span></span>
<span data-ttu-id="d79b2-104">È possibile elencare, visualizzare e aggiornare i parametri di configurazione per un server di Azure PostgreSQL utilizzando hello interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="d79b2-104">You can list, show and update configuration parameters for an Azure PostgreSQL server using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="d79b2-105">ma solo un subset delle configurazioni del motore viene esposto a livello di server e può essere modificato.</span><span class="sxs-lookup"><span data-stu-id="d79b2-105">However, only a subset of engine configurations are exposed at server-level and can be modified.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="d79b2-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="d79b2-106">Prerequisites</span></span>
<span data-ttu-id="d79b2-107">toostep tramite questa procedura-tooguide, è necessario:</span><span class="sxs-lookup"><span data-stu-id="d79b2-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="d79b2-108">Un server e un database [Creare un database di Azure per PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="d79b2-108">A server and database [Create an Azure Database for PostgreSQL](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="d79b2-109">Installare [CLI di Azure 2.0](/cli/azure/install-azure-cli) riga di comando utilità oppure utilizzare hello Azure Cloud Shell nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="d79b2-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="list-server-configuration-parameters-for-azure-database-for-postgresql-server"></a><span data-ttu-id="d79b2-110">Elencare i parametri di configurazione del server per Database di Azure per il server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="d79b2-110">List server configuration parameters for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="d79b2-111">eseguire tutti i parametri modificabili in un server e i relativi valori, toolist hello [elenco configurazione dei server az postgres](/cli/azure/postgres/server/configuration#list) comando.</span><span class="sxs-lookup"><span data-stu-id="d79b2-111">toolist all modifiable parameters in a server and their values, run hello [az postgres server configuration list](/cli/azure/postgres/server/configuration#list) command.</span></span>

<span data-ttu-id="d79b2-112">È possibile elencare i parametri di configurazione server hello per server hello **mypgserver 20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup**.</span><span class="sxs-lookup"><span data-stu-id="d79b2-112">You can list hello server configuration parameters for hello server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup**.</span></span>
```azurecli-interactive
az postgres server configuration list --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="show-server-configuration-parameter-details"></a><span data-ttu-id="d79b2-113">Visualizzare i dettagli dei parametri di configurazione server</span><span class="sxs-lookup"><span data-stu-id="d79b2-113">Show server configuration parameter details</span></span>
<span data-ttu-id="d79b2-114">Dettagli tooshow su un parametro di configurazione specifico per un server, eseguire hello [la dimostrazione di configurazione del server di az postgres](/cli/azure/postgres/server/configuration#show) comando.</span><span class="sxs-lookup"><span data-stu-id="d79b2-114">tooshow details about a particular configuration parameter for a server, run hello [az postgres server configuration show](/cli/azure/postgres/server/configuration#show)  command.</span></span>

<span data-ttu-id="d79b2-115">In questo esempio mostra i dettagli di hello **log\_min\_messaggi** parametro di configurazione server per server **mypgserver 20170401.postgres.database.azure.com** in gruppo di risorse **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="d79b2-115">This example shows details of hello **log\_min\_messages** server configuration parameter for server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration show --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="modify-server-configuration-parameter-value"></a><span data-ttu-id="d79b2-116">Modificare il valore di un parametro di configurazione server</span><span class="sxs-lookup"><span data-stu-id="d79b2-116">Modify server configuration parameter value</span></span>
<span data-ttu-id="d79b2-117">È inoltre possibile modificare il valore di hello di un determinato parametro di configurazione di server e Aggiorna valore di configurazione per il motore di hello PostgreSQL server sottostante hello.</span><span class="sxs-lookup"><span data-stu-id="d79b2-117">You can also modify hello value of a certain server configuration parameter, and this updates hello underlying configuration value for hello PostgreSQL server engine.</span></span> <span data-ttu-id="d79b2-118">hello utilizzare configurazione di tooupdate hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) comando.</span><span class="sxs-lookup"><span data-stu-id="d79b2-118">tooupdate hello configuration use hello [az postgres server configuration set](/cli/azure/postgres/server/configuration#set) command.</span></span> 

<span data-ttu-id="d79b2-119">hello tooupdate **log\_min\_messaggi** parametro di configurazione del server server **mypgserver 20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup.**</span><span class="sxs-lookup"><span data-stu-id="d79b2-119">tooupdate hello **log\_min\_messages** server configuration parameter of server **mypgserver-20170401.postgres.database.azure.com** under resource group **myresourcegroup.**</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401 --value INFO
```
<span data-ttu-id="d79b2-120">Se si desidera tooreset hello valore di un parametro di configurazione, sufficiente scegliere tooleave out hello facoltativo `--value` parametro e il servizio hello applicherà il valore di predefinito hello.</span><span class="sxs-lookup"><span data-stu-id="d79b2-120">If you want tooreset hello value of a configuration parameter, you simply choose tooleave out hello optional `--value` parameter, and hello service will apply hello default value.</span></span> <span data-ttu-id="d79b2-121">Nell'esempio precedente sarà simile a quanto segue:</span><span class="sxs-lookup"><span data-stu-id="d79b2-121">In above example, it would look like:</span></span>
```azurecli-interactive
az postgres server configuration set --name log_min_messages --resource-group myresourcegroup --server mypgserver-20170401
```
<span data-ttu-id="d79b2-122">Questa operazione reimposta hello **log\_min\_messaggi** configurazione valore predefinito di toohello **avviso**.</span><span class="sxs-lookup"><span data-stu-id="d79b2-122">This will reset hello **log\_min\_messages** configuration toohello default value **WARNING**.</span></span> <span data-ttu-id="d79b2-123">Per altre informazioni sulla configurazione server e sui valori consentiti, vedere la documentazione di PostgreSQL in [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html) (Configurazione server).</span><span class="sxs-lookup"><span data-stu-id="d79b2-123">For further details on server configuration and permissible values, see PostgreSQL documentation on [Server Configuration](https://www.postgresql.org/docs/9.6/static/runtime-config.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d79b2-124">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="d79b2-124">Next steps</span></span>
- <span data-ttu-id="d79b2-125">tooconfigure e accesso ai log di server, vedere [log del Server nel Database di Azure per PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="d79b2-125">tooconfigure and access server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
