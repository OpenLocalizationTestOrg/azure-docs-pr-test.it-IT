---
title: aaaConfigure accesso server nei registri e PostgreSQL mediante Azure CLI | Documenti Microsoft
description: In questo articolo viene descritto come tooconfigure e accesso hello i log del server nel Database di Azure per PostgreSQL tramite riga di comando CLI di Azure.
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 924d4e7634cc48405bcb0f813cf61d8b72ad8aa0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-and-access-server-logs-using-azure-cli"></a><span data-ttu-id="89a47-103">Configurare e accedere ai log del server usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="89a47-103">Configure and access server logs using Azure CLI</span></span>
<span data-ttu-id="89a47-104">È possibile scaricare i log degli errori server PostgreSQL hello utilizzando hello interfaccia della riga di comando (CLI di Azure).</span><span class="sxs-lookup"><span data-stu-id="89a47-104">You can download hello PostgreSQL server error logs using hello Command Line Interface (Azure CLI).</span></span> <span data-ttu-id="89a47-105">Tuttavia, i registri tootransaction di accesso non è supportata.</span><span class="sxs-lookup"><span data-stu-id="89a47-105">However, access tootransaction logs is not supported.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="89a47-106">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="89a47-106">Prerequisites</span></span>
<span data-ttu-id="89a47-107">toostep tramite questa procedura-tooguide, è necessario:</span><span class="sxs-lookup"><span data-stu-id="89a47-107">toostep through this how-tooguide, you need:</span></span>
- <span data-ttu-id="89a47-108">[Database di Azure per il server PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="89a47-108">An [Azure Database for PostgreSQL server](quickstart-create-server-database-azure-cli.md)</span></span>
- <span data-ttu-id="89a47-109">Installare [CLI di Azure 2.0](/cli/azure/install-azure-cli) della riga di comando utilità oppure utilizzare hello Azure Cloud Shell nel browser hello.</span><span class="sxs-lookup"><span data-stu-id="89a47-109">Install [Azure CLI 2.0](/cli/azure/install-azure-cli) command-line utility or use hello Azure Cloud Shell in hello browser.</span></span>

## <a name="configure-logging-for-azure-database-for-postgresql"></a><span data-ttu-id="89a47-110">Configurare la registrazione per Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="89a47-110">Configure logging for Azure Database for PostgreSQL</span></span>
<span data-ttu-id="89a47-111">È possibile configurare i log di query di hello server tooaccess e i log degli errori.</span><span class="sxs-lookup"><span data-stu-id="89a47-111">You can configure hello server tooaccess query logs and error logs.</span></span> <span data-ttu-id="89a47-112">I log degli errori possono contenere informazioni su checkpoint, connessioni e vuoto automatico.</span><span class="sxs-lookup"><span data-stu-id="89a47-112">Error logs can contain auto-vacuum, connection, and checkpoints information.</span></span>
1. <span data-ttu-id="89a47-113">Abilitare la registrazione</span><span class="sxs-lookup"><span data-stu-id="89a47-113">Turn on logging</span></span>
2. <span data-ttu-id="89a47-114">Registro aggiornamento\_istruzione e log\_min\_durata\_registrazione delle query tooenable istruzione</span><span class="sxs-lookup"><span data-stu-id="89a47-114">Update log\_statement and log\_min\_duration\_statement tooenable query logging</span></span>
3. <span data-ttu-id="89a47-115">Abilitare il periodo di conservazione</span><span class="sxs-lookup"><span data-stu-id="89a47-115">Update retention period</span></span>

<span data-ttu-id="89a47-116">Per altre informazioni, vedere [Personalizzazione dei parametri di configurazione](howto-configure-server-parameters-using-cli.md).</span><span class="sxs-lookup"><span data-stu-id="89a47-116">For more information, see [customizing server configuration parameters](howto-configure-server-parameters-using-cli.md).</span></span>

## <a name="list-logs-for-azure-database-for-postgresql-server"></a><span data-ttu-id="89a47-117">Elencare i log per il database di Azure per il server PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="89a47-117">List logs for Azure Database for PostgreSQL server</span></span>
<span data-ttu-id="89a47-118">file di log disponibili toolist hello del server, eseguire hello [elenco di registri server az postgres](/cli/azure/postgres/server-logs#list) comando.</span><span class="sxs-lookup"><span data-stu-id="89a47-118">toolist hello available log files for your server, run hello [az postgres server-logs list](/cli/azure/postgres/server-logs#list) command.</span></span>

<span data-ttu-id="89a47-119">È possibile elencare i file di log hello per server **mypgserver 20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup**e indirizzarlo testo tooa file denominato **log\_file\_txt.**</span><span class="sxs-lookup"><span data-stu-id="89a47-119">You can list hello log files for server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup**, and direct it tooa text file called **log\_files\_list.txt.**</span></span>
```azurecli-interactive
az postgres server-logs list --resource-group myresourcegroup --server mypgserver-20170401 > log_files_list.txt
```
## <a name="download-logs-locally-from-hello-server"></a><span data-ttu-id="89a47-120">Scaricare i log in locale dal server hello</span><span class="sxs-lookup"><span data-stu-id="89a47-120">Download logs locally from hello server</span></span>
<span data-ttu-id="89a47-121">Hello [az postgres server-log scaricare](/cli/azure/postgres/server-logs#download) comando consente toodownload singoli file di log per il server.</span><span class="sxs-lookup"><span data-stu-id="89a47-121">hello [az postgres server-logs download](/cli/azure/postgres/server-logs#download) command allows you toodownload individual log files for your server.</span></span> 

<span data-ttu-id="89a47-122">In questo esempio hello di download di file di log specifici per il server di hello **mypgserver 20170401.postgres.database.azure.com** nel gruppo di risorse **myresourcegroup** tooyour di ambiente locale.</span><span class="sxs-lookup"><span data-stu-id="89a47-122">This example downloads hello specific log file for hello server **mypgserver-20170401.postgres.database.azure.com** under Resource Group **myresourcegroup** tooyour local environment.</span></span>
```azurecli-interactive
az postgres server-logs download --name 20170414-mypgserver-20170401-postgresql.log --resource-group myresourcegroup --server mypgserver-20170401
```
## <a name="next-steps"></a><span data-ttu-id="89a47-123">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="89a47-123">Next steps</span></span>
- <span data-ttu-id="89a47-124">toolearn più sui log del server, vedere [log del Server nel Database di Azure per PostgreSQL](concepts-server-logs.md)</span><span class="sxs-lookup"><span data-stu-id="89a47-124">toolearn more about server logs, see [Server Logs in Azure Database for PostgreSQL](concepts-server-logs.md)</span></span>
- <span data-ttu-id="89a47-125">Per altre informazioni sui parametri del server, vedere [Personalizzare i parametri di configurazione server usando l'interfaccia della riga di comando di Azure](howto-configure-server-parameters-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="89a47-125">For more information on server parameters, see [Customize server configuration parameters using Azure CLI](howto-configure-server-parameters-using-cli.md)</span></span>
