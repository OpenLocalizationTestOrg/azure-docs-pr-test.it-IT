---
title: Come tooback di backup e ripristino di un server di Database di Azure per PostgreSQL | Documenti Microsoft
description: Informazioni su come tooback backup e ripristino da un server di Database di Azure per PostgreSQL utilizzando hello CLI di Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 0b9ed25e3e3a88dd5c7ffe2ae7c27f8eef9be710
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooback-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-hello-azure-cli"></a><span data-ttu-id="5ff2a-103">Come tooback backup e ripristino da un server di Database di Azure per PostgreSQL utilizzando hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="5ff2a-103">How tooback up and restore a server in Azure Database for PostgreSQL by using hello Azure CLI</span></span>

<span data-ttu-id="5ff2a-104">Utilizzare il Database di Azure per PostgreSQL toorestore un tooan di database del server Data precedente che si estende da 7 giorni too35.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-104">Use Azure Database for PostgreSQL toorestore a server database tooan earlier date that spans from 7 too35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5ff2a-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="5ff2a-105">Prerequisites</span></span>
<span data-ttu-id="5ff2a-106">toocomplete questo come-tooguide, è necessario:</span><span class="sxs-lookup"><span data-stu-id="5ff2a-106">toocomplete this how-tooguide, you need:</span></span>
- <span data-ttu-id="5ff2a-107">Un [server e un database di Database di Azure per PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="5ff2a-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="5ff2a-108">Se si installa e utilizza hello CLI di Azure localmente, questa procedura-tooguide richiede l'utilizzo di Azure CLI versione 2.0 o versione successiva.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-108">If you install and use hello Azure CLI locally, this how-tooguide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5ff2a-109">versione di hello tooconfirm, al prompt dei comandi di hello CLI di Azure, immettere `az --version`.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-109">tooconfirm hello version, at hello Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="5ff2a-110">tooinstall o l'aggiornamento, vedere [installare Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="5ff2a-110">tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="5ff2a-111">Il backup viene eseguito automaticamente</span><span class="sxs-lookup"><span data-stu-id="5ff2a-111">Back up happens automatically</span></span>
<span data-ttu-id="5ff2a-112">Quando si utilizza il Database di Azure per PostgreSQL, servizio database hello esegue automaticamente il backup del servizio di hello ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-112">When you use Azure Database for PostgreSQL, hello database service automatically makes a backup of hello service every 5 minutes.</span></span> 

<span data-ttu-id="5ff2a-113">Per il livello di base, sono disponibili backup hello per 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-113">For Basic Tier, hello backups are available for 7 days.</span></span> <span data-ttu-id="5ff2a-114">Per il livello Standard, i backup hello sono disponibili per 35 giorni.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-114">For Standard Tier, hello backups are available for 35 days.</span></span> <span data-ttu-id="5ff2a-115">Per altre informazioni, vedere [Piano tariffario di Database di Azure per PostgreSQL](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="5ff2a-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="5ff2a-116">Con questa funzionalità di backup automatico, è possibile ripristinare il server di hello e tooan il database Data precedente o punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-116">With this automatic backup feature, you can restore hello server and its databases tooan earlier date, or point in time.</span></span>

## <a name="restore-a-database-tooa-previous-point-in-time-by-using-hello-azure-cli"></a><span data-ttu-id="5ff2a-117">Ripristinare un punto precedente tooa di database nel tempo tramite hello CLI di Azure</span><span class="sxs-lookup"><span data-stu-id="5ff2a-117">Restore a database tooa previous point in time by using hello Azure CLI</span></span>
<span data-ttu-id="5ff2a-118">Utilizzare il Database di Azure per PostgreSQL toorestore hello server tooa precedente punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-118">Use Azure Database for PostgreSQL toorestore hello server tooa previous point in time.</span></span> <span data-ttu-id="5ff2a-119">i dati ripristinato Hello sono copiato tooa nuovo server e server esistente hello viene lasciato invariato.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-119">hello restored data is copied tooa new server, and hello existing server is left as is.</span></span> <span data-ttu-id="5ff2a-120">Se, ad esempio, una tabella viene accidentalmente eliminata a mezzogiorno oggi, è possibile ripristinare toohello tempo prima di mezzogiorno.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-120">For example, if a table is accidentally dropped at noon today, you can restore toohello time just before noon.</span></span> <span data-ttu-id="5ff2a-121">Quindi, è possibile recuperare hello mancante nella tabella e i dati dalla copia ripristinata hello del server di hello.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-121">Then, you can retrieve hello missing table and data from hello restored copy of hello server.</span></span> 

<span data-ttu-id="5ff2a-122">server hello toorestore, utilizzare hello Azure CLI [ripristino del server postgres az](/cli/azure/postgres/server#restore) comando.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-122">toorestore hello server, use hello Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-hello-restore-command"></a><span data-ttu-id="5ff2a-123">Eseguire il comando di ripristino hello</span><span class="sxs-lookup"><span data-stu-id="5ff2a-123">Run hello restore command</span></span>

<span data-ttu-id="5ff2a-124">server hello toorestore, al prompt dei comandi di hello CLI di Azure, immettere hello comando seguente:</span><span class="sxs-lookup"><span data-stu-id="5ff2a-124">toorestore hello server, at hello Azure CLI command prompt, enter hello following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="5ff2a-125">Hello `az postgres server restore` comando richiede hello seguenti parametri:</span><span class="sxs-lookup"><span data-stu-id="5ff2a-125">hello `az postgres server restore` command requires hello following parameters:</span></span>
| <span data-ttu-id="5ff2a-126">Impostazione</span><span class="sxs-lookup"><span data-stu-id="5ff2a-126">Setting</span></span> | <span data-ttu-id="5ff2a-127">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="5ff2a-127">Suggested value</span></span> | <span data-ttu-id="5ff2a-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="5ff2a-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="5ff2a-129">resource-group</span><span class="sxs-lookup"><span data-stu-id="5ff2a-129">resource-group</span></span> |  <span data-ttu-id="5ff2a-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5ff2a-130">myResourceGroup</span></span> |  <span data-ttu-id="5ff2a-131">Il gruppo di risorse in cui è presente il server di origine hello.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-131">The resource group where hello source server exists.</span></span>  |
| <span data-ttu-id="5ff2a-132">name</span><span class="sxs-lookup"><span data-stu-id="5ff2a-132">name</span></span> | <span data-ttu-id="5ff2a-133">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="5ff2a-133">mypgserver-restored</span></span> | <span data-ttu-id="5ff2a-134">nome di Hello del server di nuovo hello viene creato dal comando di ripristino hello.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-134">hello name of hello new server that is created by hello restore command.</span></span> |
| <span data-ttu-id="5ff2a-135">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="5ff2a-135">restore-point-in-time</span></span> | <span data-ttu-id="5ff2a-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="5ff2a-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="5ff2a-137">Selezionare un punto nel tempo toorestore per.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-137">Select a point in time toorestore to.</span></span> <span data-ttu-id="5ff2a-138">Questa data e ora deve essere compresa hello del server di origine eseguire il backup periodo di memorizzazione.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-138">This date and time must be within hello source server's back up retention period.</span></span> <span data-ttu-id="5ff2a-139">Utilizzare il formato di data e ora hello ISO8601.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-139">Use hello ISO8601 date and time format.</span></span> <span data-ttu-id="5ff2a-140">È possibile usare il proprio fuso orario locale, ad esempio `2017-04-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="5ff2a-141">È inoltre possibile utilizzare hello UTC Zulu formato, ad esempio, `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-141">You can also use hello UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="5ff2a-142">source-server</span><span class="sxs-lookup"><span data-stu-id="5ff2a-142">source-server</span></span> | <span data-ttu-id="5ff2a-143">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="5ff2a-143">mypgserver-20170401</span></span> | <span data-ttu-id="5ff2a-144">Hello nome o ID di hello origine server toorestore da.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-144">hello name or ID of hello source server toorestore from.</span></span> |

<span data-ttu-id="5ff2a-145">Quando si ripristina un server tooan punto nel tempo precedente, viene creato un nuovo server.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-145">When you restore a server tooan earlier point in time, a new server is created.</span></span> <span data-ttu-id="5ff2a-146">server originale Hello e i relativi database da hello specificato punto nel tempo vengono copiati toohello nuovo server.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-146">hello original server and its databases from hello specified point in time are copied toohello new server.</span></span>

<span data-ttu-id="5ff2a-147">valori di livello di posizione e prezzi Hello per server hello ripristinato rimangono hello stesso come server originale hello.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-147">hello location and pricing tier values for hello restored server remain hello same as hello original server.</span></span> 

<span data-ttu-id="5ff2a-148">Hello `az postgres server restore` comando è sincrono.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-148">hello `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="5ff2a-149">Dopo il ripristino del server hello, è possibile utilizzare il nuovo toorepeat hello processo per un altro punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-149">After hello server is restored, you can use it again toorepeat hello process for a different point in time.</span></span> 

<span data-ttu-id="5ff2a-150">Dopo hello ripristino configurazione di processo è completato, individuare il nuovo server di hello e verificare che i dati hello vengano ripristinati come previsto.</span><span class="sxs-lookup"><span data-stu-id="5ff2a-150">After hello restore process finishes, locate hello new server and verify that hello data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5ff2a-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="5ff2a-151">Next steps</span></span>
[<span data-ttu-id="5ff2a-152">Raccolte connessioni per il Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="5ff2a-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
