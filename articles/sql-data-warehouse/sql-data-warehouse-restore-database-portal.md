---
title: Ripristinare Azure SQL Data Warehouse (portale di Azure) | Documentazione Microsoft
description: "Attività del portale di Azure per il ripristino di Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: barbkess
editor: 
ms.assetid: b0aef539-7657-4b0e-9899-74098f5c21bc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 09/21/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: f6bc8671410dc7015a8d2a4bea1ba11f9ae526c3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="3adf7-103">Ripristinare Azure SQL Data Warehouse (portale)</span><span class="sxs-lookup"><span data-stu-id="3adf7-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="3adf7-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="3adf7-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="3adf7-105">[Portale][Portal]</span><span class="sxs-lookup"><span data-stu-id="3adf7-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="3adf7-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="3adf7-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="3adf7-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="3adf7-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="3adf7-108">Questo articolo illustra come ripristinare Azure SQL Data Warehouse usando il portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="3adf7-108">In this article, you will learn how to restore Azure SQL Data Warehouse by using the Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="3adf7-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="3adf7-109">Before you begin</span></span>
<span data-ttu-id="3adf7-110">**Verificare la capacità in DTU.**</span><span class="sxs-lookup"><span data-stu-id="3adf7-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="3adf7-111">Ogni istanza di SQL Data Warehouse è ospitata in un server SQL (ad esempio mioserver.database.windows.net), che ha una quota di unità elaborate di dati (DTU) predefinita.</span><span class="sxs-lookup"><span data-stu-id="3adf7-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="3adf7-112">Per poter ripristinare SQL Data Warehouse, verificare che la quota DTU rimanente nel server SQL sia sufficiente per il database da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="3adf7-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for the database that you're restoring.</span></span> <span data-ttu-id="3adf7-113">Per informazioni su come calcolare la quota DTU o per richiedere altre DTU, vedere [Richiedere una modifica della quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="3adf7-113">To learn how to calculate DTU quota or to request more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="3adf7-114">Ripristinare un database attivo o sospeso</span><span class="sxs-lookup"><span data-stu-id="3adf7-114">Restore an active or paused database</span></span>
<span data-ttu-id="3adf7-115">Per ripristinare un database:</span><span class="sxs-lookup"><span data-stu-id="3adf7-115">To restore a database:</span></span>

1. <span data-ttu-id="3adf7-116">Accedere al [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="3adf7-116">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="3adf7-117">Nel riquadro sinistro fare clic su **Esplora** e quindi su **Server SQL**.</span><span class="sxs-lookup"><span data-stu-id="3adf7-117">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selezionare Esplora > SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="3adf7-119">Trovare il server e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="3adf7-119">Find your server, and then select it.</span></span>

    ![Selezionare il server](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="3adf7-121">Trovare l'istanza di SQL Data Warehouse da ripristinare e selezionarla.</span><span class="sxs-lookup"><span data-stu-id="3adf7-121">Find the instance of SQL Data Warehouse that you want to restore from, and then select it.</span></span>

    ![Selezionare l'istanza di SQL Data Warehouse da ripristinare](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="3adf7-123">Nella parte superiore del pannello del data warehouse selezionare **Ripristina**.</span><span class="sxs-lookup"><span data-stu-id="3adf7-123">At the top of the Data Warehouse blade, select **Restore**.</span></span>

    ![Selezionare Ripristina](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="3adf7-125">Specificare un nuovo **nome database**.</span><span class="sxs-lookup"><span data-stu-id="3adf7-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="3adf7-126">Selezionare il **punto di ripristino** più recente.</span><span class="sxs-lookup"><span data-stu-id="3adf7-126">Select the latest **Restore point**.</span></span>

   <span data-ttu-id="3adf7-127">Assicurarsi di selezionare il punto di ripristino più recente.</span><span class="sxs-lookup"><span data-stu-id="3adf7-127">Make sure you choose the latest restore point.</span></span> <span data-ttu-id="3adf7-128">Poiché i punti di ripristino vengono visualizzati in formato UTC (Coordinated Universal Time), l'opzione predefinita potrebbe non corrispondere al punto di ripristino più recente.</span><span class="sxs-lookup"><span data-stu-id="3adf7-128">Because restore points are shown in Coordinated Universal Time (UTC), the default option might not be the latest restore point.</span></span>

      ![Selezionare un punto di ripristino](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="3adf7-130">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="3adf7-130">Select **OK**.</span></span>
9. <span data-ttu-id="3adf7-131">Viene avviato il processo di ripristino del database che sarà possibile monitorare usando le **NOTIFICHE**.</span><span class="sxs-lookup"><span data-stu-id="3adf7-131">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="3adf7-132">Al termine del ripristino sarà possibile configurare il database ripristinato seguendo le istruzioni disponibili in [Configurare il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="3adf7-132">After the restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="3adf7-133">Ripristino di un database eliminato</span><span class="sxs-lookup"><span data-stu-id="3adf7-133">Restore a deleted database</span></span>
<span data-ttu-id="3adf7-134">Per ripristinare un database eliminato:</span><span class="sxs-lookup"><span data-stu-id="3adf7-134">To restore a deleted database:</span></span>

1. <span data-ttu-id="3adf7-135">Accedere al [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="3adf7-135">Sign in to the [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="3adf7-136">Nel riquadro sinistro fare clic su **Esplora** e quindi su **Server SQL**.</span><span class="sxs-lookup"><span data-stu-id="3adf7-136">In the left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selezionare Esplora > SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="3adf7-138">Trovare il server e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="3adf7-138">Find your server, and then select it.</span></span>

    ![Selezionare il server](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="3adf7-140">Scorrere fino alla sezione **Operazioni** nel pannello del server.</span><span class="sxs-lookup"><span data-stu-id="3adf7-140">Scroll down to the **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="3adf7-141">Selezionare il riquadro **Database eliminati**.</span><span class="sxs-lookup"><span data-stu-id="3adf7-141">Select the **Deleted databases** tile.</span></span>

    ![Selezionare il riquadro Database eliminati](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="3adf7-143">Selezionare il database eliminato che si vuole ripristinare.</span><span class="sxs-lookup"><span data-stu-id="3adf7-143">Select the deleted database that you want to restore.</span></span>

    ![Selezionare un database da ripristinare](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="3adf7-145">Specificare un nuovo **nome database**.</span><span class="sxs-lookup"><span data-stu-id="3adf7-145">Specify a new **Database name**.</span></span>

    ![Aggiungere un nome per il database](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="3adf7-147">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="3adf7-147">Select **OK**.</span></span>
9. <span data-ttu-id="3adf7-148">Viene avviato il processo di ripristino del database che sarà possibile monitorare usando le **NOTIFICHE**.</span><span class="sxs-lookup"><span data-stu-id="3adf7-148">The database restore process will begin, and you can use **NOTIFICATIONS** to monitor the process.</span></span>

> [!NOTE]
> <span data-ttu-id="3adf7-149">Per configurare il database al termine del ripristino, vedere [Configurare il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="3adf7-149">To configure your database after the restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="3adf7-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="3adf7-150">Next steps</span></span>
<span data-ttu-id="3adf7-151">Per altre informazioni sulle funzionalità di continuità aziendale delle edizioni del database SQL di Azure, vedere [Panoramica sulla continuità aziendale del database SQL][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="3adf7-151">To learn about the business continuity features of Azure SQL Database editions, read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change

<!--MSDN references-->

<!--Blog references-->

<!--Other Web references-->
[Azure portal]: https://portal.azure.com/
