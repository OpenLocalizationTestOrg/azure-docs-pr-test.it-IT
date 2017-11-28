---
title: Come eseguire il backup e ripristinare un server nel Database di Azure per PostgreSQL | Microsoft Docs
description: Informazioni su come eseguire il backup e il ripristino di un server nel database di Azure per PostgreSQL usando l'interfaccia della riga di comando di Azure.
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 871887e67d686a965a0648d2c6f0c72b3008db05
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-back-up-and-restore-a-server-in-azure-database-for-postgresql-by-using-the-azure-cli"></a><span data-ttu-id="f5af2-103">Come eseguire il backup e il ripristino di un server nel database di Azure per PostgreSQL usando l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f5af2-103">How to back up and restore a server in Azure Database for PostgreSQL by using the Azure CLI</span></span>

<span data-ttu-id="f5af2-104">Usare il database di Azure per PostgreSQL per ripristinare il database di un server a una data precedente che va dai 7 ai 35 giorni.</span><span class="sxs-lookup"><span data-stu-id="f5af2-104">Use Azure Database for PostgreSQL to restore a server database to an earlier date that spans from 7 to 35 days.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f5af2-105">Prerequisiti</span><span class="sxs-lookup"><span data-stu-id="f5af2-105">Prerequisites</span></span>
<span data-ttu-id="f5af2-106">Per completare questa guida, è necessario:</span><span class="sxs-lookup"><span data-stu-id="f5af2-106">To complete this how-to guide, you need:</span></span>
- <span data-ttu-id="f5af2-107">Un [server e un database di Database di Azure per PostgreSQL](quickstart-create-server-database-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="f5af2-107">An [Azure Database for PostgreSQL server and database](quickstart-create-server-database-azure-cli.md)</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../includes/cloud-shell-try-it.md)]

 

> [!IMPORTANT]
> <span data-ttu-id="f5af2-108">Se si installa e si usa l'interfaccia della riga di comando in locale, per questa guida è necessario usare la versione 2.0 o successiva dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5af2-108">If you install and use the Azure CLI locally, this how-to guide requires that you use Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="f5af2-109">Per verificare la versione, al prompt dei comandi dell'interfaccia della riga di comando di Azure immettere `az --version`.</span><span class="sxs-lookup"><span data-stu-id="f5af2-109">To confirm the version, at the Azure CLI command prompt, enter `az --version`.</span></span> <span data-ttu-id="f5af2-110">Per eseguire l'installazione o l'aggiornamento, vedere [Installare l'interfaccia della riga di comando di Azure 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="f5af2-110">To install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span>

## <a name="back-up-happens-automatically"></a><span data-ttu-id="f5af2-111">Il backup viene eseguito automaticamente</span><span class="sxs-lookup"><span data-stu-id="f5af2-111">Back up happens automatically</span></span>
<span data-ttu-id="f5af2-112">Quando si usa Database di Azure per PostgreSQL, il servizio di database esegue automaticamente il backup del servizio ogni 5 minuti.</span><span class="sxs-lookup"><span data-stu-id="f5af2-112">When you use Azure Database for PostgreSQL, the database service automatically makes a backup of the service every 5 minutes.</span></span> 

<span data-ttu-id="f5af2-113">Per il livello di base, il servizio di backup è disponibile per 7 giorni.</span><span class="sxs-lookup"><span data-stu-id="f5af2-113">For Basic Tier, the backups are available for 7 days.</span></span> <span data-ttu-id="f5af2-114">Per il livello standard, il servizio di backup è disponibile per 35 giorni.</span><span class="sxs-lookup"><span data-stu-id="f5af2-114">For Standard Tier, the backups are available for 35 days.</span></span> <span data-ttu-id="f5af2-115">Per altre informazioni, vedere [Piano tariffario di Database di Azure per PostgreSQL](concepts-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="f5af2-115">For more information, see [Azure Database for PostgreSQL pricing tiers](concepts-service-tiers.md).</span></span>

<span data-ttu-id="f5af2-116">Con questa funzionalità di backup automatico è possibile ripristinare il server e i suoi database a una data precedente o a un precedente punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="f5af2-116">With this automatic backup feature, you can restore the server and its databases to an earlier date, or point in time.</span></span>

## <a name="restore-a-database-to-a-previous-point-in-time-by-using-the-azure-cli"></a><span data-ttu-id="f5af2-117">Ripristinare un database a un momento precedente con l'interfaccia della riga di comando di Azure</span><span class="sxs-lookup"><span data-stu-id="f5af2-117">Restore a database to a previous point in time by using the Azure CLI</span></span>
<span data-ttu-id="f5af2-118">Usare Database di Azure per PostgreSQL per ripristinare il server a un momento precedente.</span><span class="sxs-lookup"><span data-stu-id="f5af2-118">Use Azure Database for PostgreSQL to restore the server to a previous point in time.</span></span> <span data-ttu-id="f5af2-119">I dati ripristinati vengono copiati in un nuovo server e il server esistente viene lasciato invariato.</span><span class="sxs-lookup"><span data-stu-id="f5af2-119">The restored data is copied to a new server, and the existing server is left as is.</span></span> <span data-ttu-id="f5af2-120">Se, ad esempio, una tabella è stata involontariamente eliminata a mezzogiorno di oggi, è possibile eseguire il ripristino a un qualsiasi momento prima di mezzogiorno.</span><span class="sxs-lookup"><span data-stu-id="f5af2-120">For example, if a table is accidentally dropped at noon today, you can restore to the time just before noon.</span></span> <span data-ttu-id="f5af2-121">È possibile quindi recuperare la tabella e i dati mancanti dalla copia ripristinata del server.</span><span class="sxs-lookup"><span data-stu-id="f5af2-121">Then, you can retrieve the missing table and data from the restored copy of the server.</span></span> 

<span data-ttu-id="f5af2-122">Per ripristinare il server usare il comando [az postgres server restore](/cli/azure/postgres/server#restore) dell'interfaccia della riga di comando di Azure.</span><span class="sxs-lookup"><span data-stu-id="f5af2-122">To restore the server, use the Azure CLI [az postgres server restore](/cli/azure/postgres/server#restore) command.</span></span>

### <a name="run-the-restore-command"></a><span data-ttu-id="f5af2-123">Eseguire il comando di ripristino</span><span class="sxs-lookup"><span data-stu-id="f5af2-123">Run the restore command</span></span>

<span data-ttu-id="f5af2-124">Per ripristinare il server, al prompt dei comandi dell'interfaccia della riga di comando di Azure immettere il comando seguente:</span><span class="sxs-lookup"><span data-stu-id="f5af2-124">To restore the server, at the Azure CLI command prompt, enter the following command:</span></span>

```azurecli-interactive
az postgres server restore --resource-group myResourceGroup --name mypgserver-restored --restore-point-in-time 2017-04-13T13:59:00Z --source-server mypgserver-20170401
```

<span data-ttu-id="f5af2-125">Il comando `az postgres server restore` richiede i parametri seguenti:</span><span class="sxs-lookup"><span data-stu-id="f5af2-125">The `az postgres server restore` command requires the following parameters:</span></span>
| <span data-ttu-id="f5af2-126">Impostazione</span><span class="sxs-lookup"><span data-stu-id="f5af2-126">Setting</span></span> | <span data-ttu-id="f5af2-127">Valore consigliato</span><span class="sxs-lookup"><span data-stu-id="f5af2-127">Suggested value</span></span> | <span data-ttu-id="f5af2-128">Descrizione</span><span class="sxs-lookup"><span data-stu-id="f5af2-128">Description</span></span>  |
| --- | --- | --- |
| <span data-ttu-id="f5af2-129">resource-group</span><span class="sxs-lookup"><span data-stu-id="f5af2-129">resource-group</span></span> |  <span data-ttu-id="f5af2-130">myResourceGroup</span><span class="sxs-lookup"><span data-stu-id="f5af2-130">myResourceGroup</span></span> |  <span data-ttu-id="f5af2-131">Il gruppo di risorse in cui si trova il server di origine.</span><span class="sxs-lookup"><span data-stu-id="f5af2-131">The resource group where the source server exists.</span></span>  |
| <span data-ttu-id="f5af2-132">name</span><span class="sxs-lookup"><span data-stu-id="f5af2-132">name</span></span> | <span data-ttu-id="f5af2-133">mypgserver-restored</span><span class="sxs-lookup"><span data-stu-id="f5af2-133">mypgserver-restored</span></span> | <span data-ttu-id="f5af2-134">Il nome del nuovo server creato con il comando di ripristino.</span><span class="sxs-lookup"><span data-stu-id="f5af2-134">The name of the new server that is created by the restore command.</span></span> |
| <span data-ttu-id="f5af2-135">restore-point-in-time</span><span class="sxs-lookup"><span data-stu-id="f5af2-135">restore-point-in-time</span></span> | <span data-ttu-id="f5af2-136">2017-04-13T13:59:00Z</span><span class="sxs-lookup"><span data-stu-id="f5af2-136">2017-04-13T13:59:00Z</span></span> | <span data-ttu-id="f5af2-137">Selezionare un punto nel tempo per il ripristino.</span><span class="sxs-lookup"><span data-stu-id="f5af2-137">Select a point in time to restore to.</span></span> <span data-ttu-id="f5af2-138">La data e l'ora devono trovarsi all'interno del periodo di memorizzazione dei backup del server di origine.</span><span class="sxs-lookup"><span data-stu-id="f5af2-138">This date and time must be within the source server's back up retention period.</span></span> <span data-ttu-id="f5af2-139">Usare il formato ISO8601 per la data e l'ora.</span><span class="sxs-lookup"><span data-stu-id="f5af2-139">Use the ISO8601 date and time format.</span></span> <span data-ttu-id="f5af2-140">È possibile usare il proprio fuso orario locale, ad esempio `2017-04-13T05:59:00-08:00`.</span><span class="sxs-lookup"><span data-stu-id="f5af2-140">For example, you can use your own local time zone, such as `2017-04-13T05:59:00-08:00`.</span></span> <span data-ttu-id="f5af2-141">È anche possibile usare il formato UTC Zulu, ad esempio `2017-04-13T13:59:00Z`.</span><span class="sxs-lookup"><span data-stu-id="f5af2-141">You can also use the UTC Zulu format, for example, `2017-04-13T13:59:00Z`.</span></span> |
| <span data-ttu-id="f5af2-142">source-server</span><span class="sxs-lookup"><span data-stu-id="f5af2-142">source-server</span></span> | <span data-ttu-id="f5af2-143">mypgserver-20170401</span><span class="sxs-lookup"><span data-stu-id="f5af2-143">mypgserver-20170401</span></span> | <span data-ttu-id="f5af2-144">Il nome o l'ID del server di origine da cui eseguire il ripristino.</span><span class="sxs-lookup"><span data-stu-id="f5af2-144">The name or ID of the source server to restore from.</span></span> |

<span data-ttu-id="f5af2-145">Quando si ripristina un server a un punto precedente nel tempo, viene creato un nuovo server.</span><span class="sxs-lookup"><span data-stu-id="f5af2-145">When you restore a server to an earlier point in time, a new server is created.</span></span> <span data-ttu-id="f5af2-146">Il server originale e i database dal punto nel punto specificato vengono copiati nel nuovo server.</span><span class="sxs-lookup"><span data-stu-id="f5af2-146">The original server and its databases from the specified point in time are copied to the new server.</span></span>

<span data-ttu-id="f5af2-147">I valori relativi al percorso e al piano tariffario per il server ripristinato sono gli stessi del server di origine.</span><span class="sxs-lookup"><span data-stu-id="f5af2-147">The location and pricing tier values for the restored server remain the same as the original server.</span></span> 

<span data-ttu-id="f5af2-148">Il comando `az postgres server restore` è sincrono.</span><span class="sxs-lookup"><span data-stu-id="f5af2-148">The `az postgres server restore` command is synchronous.</span></span> <span data-ttu-id="f5af2-149">Dopo il ripristino, il server può essere usato di nuovo per ripetere il processo per un altro punto nel tempo.</span><span class="sxs-lookup"><span data-stu-id="f5af2-149">After the server is restored, you can use it again to repeat the process for a different point in time.</span></span> 

<span data-ttu-id="f5af2-150">Al termine del ripristino, individuare il nuovo server creato per verificare che il ripristino dei dati sia avvenuto come previsto.</span><span class="sxs-lookup"><span data-stu-id="f5af2-150">After the restore process finishes, locate the new server and verify that the data is restored as expected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f5af2-151">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="f5af2-151">Next steps</span></span>
[<span data-ttu-id="f5af2-152">Raccolte connessioni per il Database di Azure per PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f5af2-152">Connection libraries for Azure Database for PostgreSQL</span></span>](concepts-connection-libraries.md)
