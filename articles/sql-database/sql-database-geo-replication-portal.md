---
title: 'Portale di Azure: replica geografica di database SQL | Microsoft Docs'
description: Configurare la replica geografica per il Database SQL di Azure nel portale di Azure di hello e avviare il failover
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
ms.openlocfilehash: 09cbbdb040f36c42593e3be87ce6db2238f36656
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-active-geo-replication-for-azure-sql-database-in-hello-azure-portal-and-initiate-failover"></a><span data-ttu-id="2174f-103">Configurare la replica geografica attiva per il Database SQL di Azure in hello portale di Azure e avviare il failover</span><span class="sxs-lookup"><span data-stu-id="2174f-103">Configure active geo-replication for Azure SQL Database in hello Azure portal and initiate failover</span></span>

<span data-ttu-id="2174f-104">In questo articolo illustra come tooconfigure replica geografica attiva per il Database SQL in hello [portale di Azure](http://portal.azure.com) e tooinitiate failover.</span><span class="sxs-lookup"><span data-stu-id="2174f-104">This article shows you how tooconfigure active geo-replication for SQL Database in hello [Azure portal](http://portal.azure.com) and tooinitiate failover.</span></span>

<span data-ttu-id="2174f-105">failover tooinitiate con hello portale di Azure, vedere [avviare un failover pianificato o per Database SQL di Azure con il portale di Azure hello](sql-database-geo-replication-portal.md).</span><span class="sxs-lookup"><span data-stu-id="2174f-105">tooinitiate failover with hello Azure portal, see [Initiate a planned or unplanned failover for Azure SQL Database with hello Azure portal](sql-database-geo-replication-portal.md).</span></span>

<span data-ttu-id="2174f-106">tooconfigure replica geografica attiva utilizzando hello portale di Azure, è necessario hello seguenti risorse:</span><span class="sxs-lookup"><span data-stu-id="2174f-106">tooconfigure active geo-replication by using hello Azure portal, you need hello following resource:</span></span>

* <span data-ttu-id="2174f-107">Un database SQL di Azure: database primario di hello che si desidera area geografica di tooreplicate tooa diversa.</span><span class="sxs-lookup"><span data-stu-id="2174f-107">An Azure SQL database: hello primary database that you want tooreplicate tooa different geographical region.</span></span>

> [!Note]
<span data-ttu-id="2174f-108">Replica geografica attiva deve essere compreso tra i database di hello stessa sottoscrizione.</span><span class="sxs-lookup"><span data-stu-id="2174f-108">Active geo-replication must be between databases in hello same subscription.</span></span>

## <a name="add-a-secondary-database"></a><span data-ttu-id="2174f-109">Aggiungere un database secondario</span><span class="sxs-lookup"><span data-stu-id="2174f-109">Add a secondary database</span></span>
<span data-ttu-id="2174f-110">Hello seguente procedura consente di creare un nuovo database secondario in una relazione di replica geografica.</span><span class="sxs-lookup"><span data-stu-id="2174f-110">hello following steps create a new secondary database in a geo-replication partnership.</span></span>  

<span data-ttu-id="2174f-111">tooadd un database secondario, è necessario essere proprietario della sottoscrizione hello o comproprietario.</span><span class="sxs-lookup"><span data-stu-id="2174f-111">tooadd a secondary database, you must be hello subscription owner or co-owner.</span></span>

<span data-ttu-id="2174f-112">database secondario Hello è hello stesso nome come database primario hello e ha, per impostazione predefinita, hello stesso livello di servizio.</span><span class="sxs-lookup"><span data-stu-id="2174f-112">hello secondary database has hello same name as hello primary database and has, by default, hello same service level.</span></span> <span data-ttu-id="2174f-113">database secondario Hello può essere un singolo database o un database in un pool elastico.</span><span class="sxs-lookup"><span data-stu-id="2174f-113">hello secondary database can be a single database or a database in an elastic pool.</span></span> <span data-ttu-id="2174f-114">Per altre informazioni, vedere [Livelli di servizio](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="2174f-114">For more information, see [Service tiers](sql-database-service-tiers.md).</span></span>
<span data-ttu-id="2174f-115">Dopo aver creato e sottoposto a seeding hello secondario, dati iniziano la replica dal database secondario nuovo toohello hello database primario.</span><span class="sxs-lookup"><span data-stu-id="2174f-115">After hello secondary is created and seeded, data begins replicating from hello primary database toohello new secondary database.</span></span>

> [!NOTE]
> <span data-ttu-id="2174f-116">Se esiste un database partner hello (ad esempio, in seguito a terminare una relazione di replica geografica precedente) comando hello ha esito negativo.</span><span class="sxs-lookup"><span data-stu-id="2174f-116">If hello partner database already exists (for example, as a result of terminating a previous geo-replication relationship) hello command fails.</span></span>
> 

1. <span data-ttu-id="2174f-117">In hello [portale di Azure](http://portal.azure.com), esplorare database toohello che si desidera tooset per la replica geografica.</span><span class="sxs-lookup"><span data-stu-id="2174f-117">In hello [Azure portal](http://portal.azure.com), browse toohello database that you want tooset up for geo-replication.</span></span>
2. <span data-ttu-id="2174f-118">Nella pagina di database SQL di hello, selezionare **-replica geografica**e quindi selezionare i database secondari di hello area toocreate hello.</span><span class="sxs-lookup"><span data-stu-id="2174f-118">On hello SQL database page, select **geo-replication**, and then select hello region toocreate hello secondary database.</span></span> <span data-ttu-id="2174f-119">È possibile selezionare qualsiasi area diversa area hello che ospita il database primario hello, ma è consigliabile hello [area abbinata](../best-practices-availability-paired-regions.md).</span><span class="sxs-lookup"><span data-stu-id="2174f-119">You can select any region other than hello region hosting hello primary database, but we recommend hello [paired region](../best-practices-availability-paired-regions.md).</span></span>
   
    ![Configurare la replica geografica](./media/sql-database-geo-replication-portal/configure-geo-replication.png)
3. <span data-ttu-id="2174f-121">Selezionare o configurare server hello e il piano tariffario per il database secondario hello.</span><span class="sxs-lookup"><span data-stu-id="2174f-121">Select or configure hello server and pricing tier for hello secondary database.</span></span>
   
    ![Configurare il database secondario](./media/sql-database-geo-replication-portal/create-secondary.png)
4. <span data-ttu-id="2174f-123">Facoltativamente, è possibile aggiungere un pool elastico tooan di database secondario.</span><span class="sxs-lookup"><span data-stu-id="2174f-123">Optionally, you can add a secondary database tooan elastic pool.</span></span> <span data-ttu-id="2174f-124">database secondario di hello toocreate in un pool, fare clic su **pool elastico** e selezionare un pool nel server di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="2174f-124">toocreate hello secondary database in a pool, click **elastic pool** and select a pool on hello target server.</span></span> <span data-ttu-id="2174f-125">Un pool deve esistere nel server di destinazione hello.</span><span class="sxs-lookup"><span data-stu-id="2174f-125">A pool must already exist on hello target server.</span></span> <span data-ttu-id="2174f-126">Questo flusso di lavoro non crea un pool.</span><span class="sxs-lookup"><span data-stu-id="2174f-126">This workflow does not create a pool.</span></span>
5. <span data-ttu-id="2174f-127">Fare clic su **crea** hello tooadd secondario.</span><span class="sxs-lookup"><span data-stu-id="2174f-127">Click **Create** tooadd hello secondary.</span></span>
6. <span data-ttu-id="2174f-128">creazione del database secondario Hello e inizia il processo di seeding hello.</span><span class="sxs-lookup"><span data-stu-id="2174f-128">hello secondary database is created and hello seeding process begins.</span></span>
   
    ![Configurare il database secondario](./media/sql-database-geo-replication-portal/seeding0.png)
7. <span data-ttu-id="2174f-130">Una volta completato il processo di seeding hello, database secondario hello consente di visualizzare il relativo stato.</span><span class="sxs-lookup"><span data-stu-id="2174f-130">When hello seeding process is complete, hello secondary database displays its status.</span></span>
   
    ![Seeding completo](./media/sql-database-geo-replication-portal/seeding-complete.png)

## <a name="initiate-a-failover"></a><span data-ttu-id="2174f-132">Avviare un failover</span><span class="sxs-lookup"><span data-stu-id="2174f-132">Initiate a failover</span></span>

<span data-ttu-id="2174f-133">database secondario Hello può essere disattivati toobecome hello primario.</span><span class="sxs-lookup"><span data-stu-id="2174f-133">hello secondary database can be switched toobecome hello primary.</span></span>  

1. <span data-ttu-id="2174f-134">In hello [portale di Azure](http://portal.azure.com), Sfoglia toohello database primario in una relazione di replica geografica hello.</span><span class="sxs-lookup"><span data-stu-id="2174f-134">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="2174f-135">Nel Pannello di Database SQL di hello, selezionare **tutte le impostazioni** > **-replica geografica**.</span><span class="sxs-lookup"><span data-stu-id="2174f-135">On hello SQL Database blade, select **All settings** > **geo-replication**.</span></span>
3. <span data-ttu-id="2174f-136">In hello **secondari** elenco, il database di hello selezionare da toobecome hello nuovo database primario e fare clic su **Failover**.</span><span class="sxs-lookup"><span data-stu-id="2174f-136">In hello **SECONDARIES** list, select hello database you want toobecome hello new primary and click **Failover**.</span></span>
   
    ![Failover](./media/sql-database-geo-replication-failover-portal/secondaries.png)
4. <span data-ttu-id="2174f-138">Fare clic su **Sì** toobegin hello failover.</span><span class="sxs-lookup"><span data-stu-id="2174f-138">Click **Yes** toobegin hello failover.</span></span>

<span data-ttu-id="2174f-139">comando Hello passa immediatamente database secondario hello in ruolo primario hello.</span><span class="sxs-lookup"><span data-stu-id="2174f-139">hello command immediately switches hello secondary database into hello primary role.</span></span> 

<span data-ttu-id="2174f-140">È un breve periodo durante il quale entrambi i database non sono disponibili (in ordine di hello di 0 secondi too25) durante il cambio di ruolo hello.</span><span class="sxs-lookup"><span data-stu-id="2174f-140">There is a short period during which both databases are unavailable (on hello order of 0 too25 seconds) while hello roles are switched.</span></span> <span data-ttu-id="2174f-141">Se il database primario hello dispone di più database secondari, il comando hello automaticamente la riconfigurazione hello altri database secondari tooconnect toohello nuovo database primario.</span><span class="sxs-lookup"><span data-stu-id="2174f-141">If hello primary database has multiple secondary databases, hello command automatically reconfigures hello other secondaries tooconnect toohello new primary.</span></span> <span data-ttu-id="2174f-142">intera operazione Hello richiederà meno di un minuto toocomplete in circostanze normali.</span><span class="sxs-lookup"><span data-stu-id="2174f-142">hello entire operation should take less than a minute toocomplete under normal circumstances.</span></span> 

> [!NOTE]
> <span data-ttu-id="2174f-143">Questo comando è progettato per il ripristino rapido dei database hello in caso di interruzione.</span><span class="sxs-lookup"><span data-stu-id="2174f-143">This command is designed for quick recovery of hello database in case of an outage.</span></span> <span data-ttu-id="2174f-144">e attiva il failover senza sincronizzazione dei dati (failover forzato).</span><span class="sxs-lookup"><span data-stu-id="2174f-144">It triggers failover without data synchronization (forced failover).</span></span>  <span data-ttu-id="2174f-145">Se il commit delle transazioni quando il comando hello viene eseguito una perdita di dati può verificarsi hello primario è online.</span><span class="sxs-lookup"><span data-stu-id="2174f-145">If hello primary is online and committing transactions when hello command is issued some data loss may occur.</span></span> 
> 
> 

## <a name="remove-secondary-database"></a><span data-ttu-id="2174f-146">Rimuovere un database secondario</span><span class="sxs-lookup"><span data-stu-id="2174f-146">Remove secondary database</span></span>
<span data-ttu-id="2174f-147">Questa operazione termina in modo permanente i database secondari di hello replica toohello e modifiche hello ruolo di database di lettura / scrittura hello tooa secondaria regolare.</span><span class="sxs-lookup"><span data-stu-id="2174f-147">This operation permanently terminates hello replication toohello secondary database, and changes hello role of hello secondary tooa regular read-write database.</span></span> <span data-ttu-id="2174f-148">Se il database secondario di hello connettività toohello viene interrotto, il comando di hello ha esito positivo ma hello fa secondari non diventano lettura / scrittura fino a dopo il ripristino della connettività.</span><span class="sxs-lookup"><span data-stu-id="2174f-148">If hello connectivity toohello secondary database is broken, hello command succeeds but hello secondary does not become read-write until after connectivity is restored.</span></span>  

1. <span data-ttu-id="2174f-149">In hello [portale di Azure](http://portal.azure.com), Sfoglia toohello database primario in una relazione di replica geografica hello.</span><span class="sxs-lookup"><span data-stu-id="2174f-149">In hello [Azure portal](http://portal.azure.com), browse toohello primary database in hello geo-replication partnership.</span></span>
2. <span data-ttu-id="2174f-150">Nella pagina di database SQL di hello, selezionare **-replica geografica**.</span><span class="sxs-lookup"><span data-stu-id="2174f-150">On hello SQL database page, select **geo-replication**.</span></span>
3. <span data-ttu-id="2174f-151">In hello **secondari** elenco, database selezionare hello da tooremove dalla relazione di replica geografica hello.</span><span class="sxs-lookup"><span data-stu-id="2174f-151">In hello **SECONDARIES** list, select hello database you want tooremove from hello geo-replication partnership.</span></span>
4. <span data-ttu-id="2174f-152">Fare clic su **Arresta replica**.</span><span class="sxs-lookup"><span data-stu-id="2174f-152">Click **Stop Replication**.</span></span>
   
    ![Rimuovere un database secondario](./media/sql-database-geo-replication-portal/remove-secondary.png)
5. <span data-ttu-id="2174f-154">Verrà visualizzata una finestra di conferma.</span><span class="sxs-lookup"><span data-stu-id="2174f-154">A confirmation window opens.</span></span> <span data-ttu-id="2174f-155">Fare clic su **Sì** database hello tooremove dalla relazione di replica geografica hello.</span><span class="sxs-lookup"><span data-stu-id="2174f-155">Click **Yes** tooremove hello database from hello geo-replication partnership.</span></span> <span data-ttu-id="2174f-156">(Impostato il database di lettura / scrittura tooa non fa parte del processo di replica).</span><span class="sxs-lookup"><span data-stu-id="2174f-156">(Set it tooa read-write database not part of any replication.)</span></span>

## <a name="next-steps"></a><span data-ttu-id="2174f-157">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="2174f-157">Next steps</span></span>
* <span data-ttu-id="2174f-158">toolearn più sulla replica geografica attiva, vedere [replica geografica attiva](sql-database-geo-replication-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2174f-158">toolearn more about active geo-replication, see [active geo-replication](sql-database-geo-replication-overview.md).</span></span>
* <span data-ttu-id="2174f-159">Per la panoramica e gli scenari della continuità aziendale, vedere [Continuità aziendale del database SQL di Azure](sql-database-business-continuity.md).</span><span class="sxs-lookup"><span data-stu-id="2174f-159">For a business continuity overview and scenarios, see [Business continuity overview](sql-database-business-continuity.md).</span></span>

