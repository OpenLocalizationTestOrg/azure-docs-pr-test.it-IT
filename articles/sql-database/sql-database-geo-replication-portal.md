---
title: 'Portale di Azure: replica geografica di database SQL | Microsoft Docs'
description: Configurare la replica geografica per il database SQL di Azure nel portale di Azure e avviare il failover
services: sql-database
documentationcenter: 
author: CarlRabeler
manager: jhubbard
editor: 
ms.assetid: d0b29822-714f-4633-a5ab-fb1a09d43ced
ms.service: sql-database
ms.custom: business continuity
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 03/06/2016
ms.author: carlrab
ms.openlocfilehash: db90fad2fe397f0c8466db6bdc1bd8c8d1cf8f15
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-the-azure-portal-and-initiate-failover"></a><span data-ttu-id="93790-103">Configurare la replica geografica attiva per il database SQL di Azure nel portale di Azure e avviare il failover</span><span class="sxs-lookup"><span data-stu-id="93790-103">Configure active geo-replication for Azure SQL Database in the Azure portal and initiate failover</span></span>

<span data-ttu-id="93790-104">Questo articolo illustra come configurare la replica geografica attiva per il database SQL nel [portale di Azure](http://portal.azure.com) e avviare il failover.</span><span class="sxs-lookup"><span data-stu-id="93790-104">This article shows you how to configure active geo-replication for SQL Database in the [Azure portal](http://portal.azure.com) and to initiate failover.</span></span>

<span data-ttu-id="93790-105">Per avviare un failover con il portale di Azure, vedere [Avviare un failover pianificato o non pianificato per il database SQL di Azure con il portale di Azure](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="93790-105">To initiate failover with the Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with the Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="93790-106">Per configurare la replica geografica attiva tramite il portale di Azure, è necessaria la risorsa seguente:</span><span class="sxs-lookup"><span data-stu-id="93790-106">To configure active geo-replication by using the Azure portal, you need the following resource:</span></span>

* <span data-ttu-id="93790-107">Un database SQL di Azure logico: il database primario che si vuole replicare in una area geografica diversa.</span><span class="sxs-lookup"><span data-stu-id="93790-107">An Azure SQL database: The primary database that you want to replicate to a different geographical region.</span></span>

> [!Note]
<span data-ttu-id="93790-108">La replica geografica attiva deve essere avvenire tra database della stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="93790-108">Active geo-replication must be between databases in the same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="93790-109">Aggiungere un database secondario</span><span class="sxs-lookup"><span data-stu-id="93790-109">Add a secondary database</span></span>
<span data-ttu-id="93790-110">La procedura seguente crea un nuovo database secondario in una relazione di replica geografica.</span><span class="sxs-lookup"><span data-stu-id="93790-110">The following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="93790-111">Per aggiungere un database secondario, è necessario essere il proprietario o un comproprietario della sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="93790-111">To add a secondary database, you must be the subscription owner or co-owner.</span></span>

<span data-ttu-id="93790-112">Il database secondario ha lo stesso nome del database primario e ha, per impostazione predefinita, lo stesso livello di servizio.</span><span class="sxs-lookup"><span data-stu-id="93790-112">The secondary database has the same name as the primary database and has, by default, the same service level.</span></span> <span data-ttu-id="93790-113">Il database secondario può essere un database singolo o un database in un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="93790-113">The secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="93790-114">Per altre informazioni, vedere [Livelli di servizio](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="93790-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="93790-115">Dopo aver creato ed eseguito il seeding del database secondario, inizia la replica dei dati dal database primario al nuovo database secondario.</span><span class="sxs-lookup"><span data-stu-id="93790-115">After the secondary is created and seeded, data begins replicating from the primary database to the new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="93790-116">Se il database partner esiste già, ad esempio come risultato della terminazione di una precedente relazione di replica geografica, il comando non riesce.</span><span class="sxs-lookup"><span data-stu-id="93790-116">If the partner database already exists (for example, as a result of terminating a previous geo-replication relationship) the command fails.</span></span>
> 

1. <span data-ttu-id="93790-117">Nel [portale di Azure](http://portal.azure.com) passare al database per cui si vuole installare la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="93790-117">In the [Azure portal](http://portal.azure.com), browse to the database that you want to set up for geo-replication.</span></span>
2. <span data-ttu-id="93790-118">Nella pagina del database SQL selezionare **Replica geografica** e quindi selezionare l'area per creare il database secondario.</span><span class="sxs-lookup"><span data-stu-id="93790-118">On the SQL database page, select **geo-replication**, and then select the region to create the secondary database.</span></span> <span data-ttu-id="93790-119">Sebbene sia possibile selezionare qualsiasi area diversa dall'area che ospita il database primario, si consiglia di scegliere l'[area abbinata](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="93790-119">You can select any region other than the region hosting the primary database, but we recommend the [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Configurare la replica geografica](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="93790-121">Selezionare o configurare il server e il piano tariffario per il database secondario.</span><span class="sxs-lookup"><span data-stu-id="93790-121">Select or configure the server and pricing tier for the secondary database.</span></span>
   
    ![Configurare il database secondario](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="93790-123">Facoltativamente, è possibile aggiungere un database secondario a un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="93790-123">Optionally, you can add a secondary database to an elastic pool.</span></span> <span data-ttu-id="93790-124">Per creare il database secondario in un pool, fare clic su **Pool elastico** e selezionare un pool sul server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="93790-124">To create the secondary database in a pool, click **elastic pool** and select a pool on the target server.</span></span> <span data-ttu-id="93790-125">Un pool deve esistere già nel server di destinazione.</span><span class="sxs-lookup"><span data-stu-id="93790-125">A pool must already exist on the target server.</span></span> <span data-ttu-id="93790-126">Questo flusso di lavoro non crea un pool.</span><span class="sxs-lookup"><span data-stu-id="93790-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="93790-127">Fare clic su **Crea** per aggiungere il database secondario.</span><span class="sxs-lookup"><span data-stu-id="93790-127">Click **Create** to add the secondary.</span></span>
6. <span data-ttu-id="93790-128">Il database secondario viene creato e viene avviato il processo di seeding.</span><span class="sxs-lookup"><span data-stu-id="93790-128">The secondary database is created and the seeding process begins.</span></span>
   
    ![Configurare il database secondario](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="93790-130">Una volta completato il processo di seeding il database secondario visualizza il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="93790-130">When the seeding process is complete, the secondary database displays its status.</span></span>
   
    ![Seeding completo](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="93790-132">Avviare un failover</span><span class="sxs-lookup"><span data-stu-id="93790-132">Initiate a failover</span></span>

<span data-ttu-id="93790-133">Il database secondario può diventare il database primario.</span><span class="sxs-lookup"><span data-stu-id="93790-133">The secondary database can be switched to become the primary.</span></span>  

1. <span data-ttu-id="93790-134">Nel [portale di Azure](http://portal.azure.com) passare al database primario nella relazione di replica geografica.</span><span class="sxs-lookup"><span data-stu-id="93790-134">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="93790-135">Nel pannello del database SQL selezionare **Tutte le impostazioni** > **Replica geografica**.</span><span class="sxs-lookup"><span data-stu-id="93790-135">On the SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="93790-136">Nell'elenco **SECONDARI** selezionare il database che si vuole usare come nuovo database primario e fare clic su **Failover**.</span><span class="sxs-lookup"><span data-stu-id="93790-136">In the **SECONDARIES** list, select the database you want to become the new primary and click **Failover**.</span></span>
   
    ![Failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="93790-138">Fare clic su **Sì** per avviare il failover.</span><span class="sxs-lookup"><span data-stu-id="93790-138">Click **Yes** to begin the failover.</span></span>

<span data-ttu-id="93790-139">Il comando passa immediatamente il database secondario al ruolo di database primario.</span><span class="sxs-lookup"><span data-stu-id="93790-139">The command immediately switches the secondary database into the primary role.</span></span> 

<span data-ttu-id="93790-140">Per un breve periodo, da 0 a 25 secondi, entrambi i database non sono disponibili mentre vengono scambiati i ruoli.</span><span class="sxs-lookup"><span data-stu-id="93790-140">There is a short period during which both databases are unavailable (on the order of 0 to 25 seconds) while the roles are switched.</span></span> <span data-ttu-id="93790-141">Se il database primario ha più database secondari, il comando riconfigura automaticamente gli altri database secondari per la connessione al nuovo database primario.</span><span class="sxs-lookup"><span data-stu-id="93790-141">If the primary database has multiple secondary databases, the command automatically reconfigures the other secondaries to connect to the new primary.</span></span> <span data-ttu-id="93790-142">Il completamento dell'intera operazione dovrebbe richiedere meno di un minuto in circostanze normali.</span><span class="sxs-lookup"><span data-stu-id="93790-142">The entire operation should take less than a minute to complete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="93790-143">Questo comando è progettato per il ripristino rapido del database in caso di interruzione del servizio</span><span class="sxs-lookup"><span data-stu-id="93790-143">This command is designed for quick recovery of the database in case of an outage.</span></span> <span data-ttu-id="93790-144">e attiva il failover senza sincronizzazione dei dati (failover forzato).</span><span class="sxs-lookup"><span data-stu-id="93790-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="93790-145">Se il database primario è online sta eseguendo il commit di transazioni al momento dell'esecuzione del comando, può verificarsi la perdita di dati.</span><span class="sxs-lookup"><span data-stu-id="93790-145">If the primary is online and committing transactions when the command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="93790-146">Rimuovere un database secondario</span><span class="sxs-lookup"><span data-stu-id="93790-146">Remove secondary database</span></span>
<span data-ttu-id="93790-147">Questa operazione interrompe in modo permanente la replica al database secondario e modifica il ruolo del database secondario in un database di lettura/scrittura normale.</span><span class="sxs-lookup"><span data-stu-id="93790-147">This operation permanently terminates the replication to the secondary database, and changes the role of the secondary to a regular read-write database.</span></span> <span data-ttu-id="93790-148">Se la connettività al database secondario viene interrotta il comando ha esito positivo ma il database secondario non diventa un database di lettura-scrittura fino a quando la connettività non verrà ripristinata.</span><span class="sxs-lookup"><span data-stu-id="93790-148">If the connectivity to the secondary database is broken, the command succeeds but the secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="93790-149">Nel [portale di Azure](http://portal.azure.com) passare al database primario nella relazione di replica geografica.</span><span class="sxs-lookup"><span data-stu-id="93790-149">In the [Azure portal](http://portal.azure.com), browse to the primary database in the geo-replication partnership.</span></span>
2. <span data-ttu-id="93790-150">Nella pagina del database SQL selezionare **Replica geografica**.</span><span class="sxs-lookup"><span data-stu-id="93790-150">On the SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="93790-151">Nell'elenco **SECONDARI** passare al database da rimuovere dalla relazione di replica geografica.</span><span class="sxs-lookup"><span data-stu-id="93790-151">In the **SECONDARIES** list, select the database you want to remove from the geo-replication partnership.</span></span>
4. <span data-ttu-id="93790-152">Fare clic su **Arresta replica**.</span><span class="sxs-lookup"><span data-stu-id="93790-152">Click **Stop Replication**.</span></span>
   
    ![Rimuovere un database secondario](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="93790-154">Verrà visualizzata una finestra di conferma.</span><span class="sxs-lookup"><span data-stu-id="93790-154">A confirmation window opens.</span></span> <span data-ttu-id="93790-155">Fare clic su **Sì** per rimuovere il database dalla relazione di replica geografica.</span><span class="sxs-lookup"><span data-stu-id="93790-155">Click **Yes** to remove the database from the geo-replication partnership.</span></span> <span data-ttu-id="93790-156">Impostarla su un database di lettura/scrittura che non fa parte del processo di replica.</span><span class="sxs-lookup"><span data-stu-id="93790-156">(Set it to a read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="93790-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="93790-157">Next steps</span></span>
* <span data-ttu-id="93790-158">Per altre informazioni sulla replica geografica attiva, vedere [Replica geografica attiva](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93790-158">To learn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="93790-159">Per la panoramica e gli scenari della continuità aziendale, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="93790-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

