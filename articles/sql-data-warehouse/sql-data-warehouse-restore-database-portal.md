---
title: aaaRestore Azure SQL Data Warehouse (portale di Azure) | Documenti Microsoft
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
ms.openlocfilehash: cb225d2a21b61acab70a51b69c266f8d3ffacc9a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-azure-sql-data-warehouse-portal"></a><span data-ttu-id="ae625-103">Ripristinare Azure SQL Data Warehouse (portale)</span><span class="sxs-lookup"><span data-stu-id="ae625-103">Restore Azure SQL Data Warehouse (portal)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="ae625-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="ae625-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="ae625-105">[Portale][Portal]</span><span class="sxs-lookup"><span data-stu-id="ae625-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="ae625-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="ae625-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="ae625-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="ae625-107">[REST][REST]</span></span>
>
>
<span data-ttu-id="ae625-108">In questo articolo si apprenderà come toorestore Azure SQL Data Warehouse utilizzando hello portale di Azure.</span><span class="sxs-lookup"><span data-stu-id="ae625-108">In this article, you will learn how toorestore Azure SQL Data Warehouse by using hello Azure portal.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ae625-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="ae625-109">Before you begin</span></span>
<span data-ttu-id="ae625-110">**Verificare la capacità in DTU.**</span><span class="sxs-lookup"><span data-stu-id="ae625-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="ae625-111">Ogni istanza di SQL Data Warehouse è ospitata in un server SQL (ad esempio mioserver.database.windows.net), che ha una quota di unità elaborate di dati (DTU) predefinita.</span><span class="sxs-lookup"><span data-stu-id="ae625-111">Each instance of SQL Data Warehouse is hosted by a SQL server (for example, myserver.database.windows.net) which has a default data throughput unit (DTU) quota.</span></span> <span data-ttu-id="ae625-112">Prima di poter ripristinare SQL Data Warehouse, verificare che SQL server disponga di sufficiente rimanente quota DTU per database hello che si esegue il ripristino.</span><span class="sxs-lookup"><span data-stu-id="ae625-112">Before you can restore SQL Data Warehouse, verify that your SQL server has enough remaining DTU quota for hello database that you're restoring.</span></span> <span data-ttu-id="ae625-113">toolearn quota DTU toocalculate o toorequest più Dtu, vedere [richiedere una modifica della quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="ae625-113">toolearn how toocalculate DTU quota or toorequest more DTUs, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="ae625-114">Ripristinare un database attivo o sospeso</span><span class="sxs-lookup"><span data-stu-id="ae625-114">Restore an active or paused database</span></span>
<span data-ttu-id="ae625-115">toorestore un database:</span><span class="sxs-lookup"><span data-stu-id="ae625-115">toorestore a database:</span></span>

1. <span data-ttu-id="ae625-116">Accedi toohello [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="ae625-116">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="ae625-117">Nel riquadro sinistro hello selezionare **Sfoglia**, quindi selezionare **istanze di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ae625-117">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selezionare Esplora > SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="ae625-119">Trovare il server e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="ae625-119">Find your server, and then select it.</span></span>

    ![Selezionare il server](./media/sql-data-warehouse-restore-database-portal/01-select-server.png)
4. <span data-ttu-id="ae625-121">Trovare l'istanza di hello di SQL Data Warehouse che si desidera toorestore da e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="ae625-121">Find hello instance of SQL Data Warehouse that you want toorestore from, and then select it.</span></span>

    ![Selezionare l'istanza hello toorestore SQL Data Warehouse](./media/sql-data-warehouse-restore-database-portal/01-select-active-dw.png)
5. <span data-ttu-id="ae625-123">Nella parte superiore di hello del Pannello di hello del Data Warehouse, selezionare **ripristinare**.</span><span class="sxs-lookup"><span data-stu-id="ae625-123">At hello top of hello Data Warehouse blade, select **Restore**.</span></span>

    ![Selezionare Ripristina](./media/sql-data-warehouse-restore-database-portal/01-select-restore-from-active.png)
6. <span data-ttu-id="ae625-125">Specificare un nuovo **nome database**.</span><span class="sxs-lookup"><span data-stu-id="ae625-125">Specify a new **Database name**.</span></span>
7. <span data-ttu-id="ae625-126">Versione più recente hello seleziona **punto di ripristino**.</span><span class="sxs-lookup"><span data-stu-id="ae625-126">Select hello latest **Restore point**.</span></span>

   <span data-ttu-id="ae625-127">Assicurarsi di scegliere il punto di ripristino più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="ae625-127">Make sure you choose hello latest restore point.</span></span> <span data-ttu-id="ae625-128">Poiché i punti di ripristino sono visibili in Coordinated Universal Time (UTC), opzione predefinita hello potrebbe non essere il punto di ripristino più recente di hello.</span><span class="sxs-lookup"><span data-stu-id="ae625-128">Because restore points are shown in Coordinated Universal Time (UTC), hello default option might not be hello latest restore point.</span></span>

      ![Selezionare un punto di ripristino](./media/sql-data-warehouse-restore-database-portal/01-restore-blade-from-active.png)
8. <span data-ttu-id="ae625-130">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae625-130">Select **OK**.</span></span>
9. <span data-ttu-id="ae625-131">processo di ripristino del database Hello verrà avviata ed è possibile utilizzare **notifiche** processo hello toomonitor.</span><span class="sxs-lookup"><span data-stu-id="ae625-131">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="ae625-132">Al termine di ripristino di hello, è possibile configurare il database ripristinato seguendo [configura il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="ae625-132">After hello restore has finished, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="restore-a-deleted-database"></a><span data-ttu-id="ae625-133">Ripristino di un database eliminato</span><span class="sxs-lookup"><span data-stu-id="ae625-133">Restore a deleted database</span></span>
<span data-ttu-id="ae625-134">un database eliminato toorestore:</span><span class="sxs-lookup"><span data-stu-id="ae625-134">toorestore a deleted database:</span></span>

1. <span data-ttu-id="ae625-135">Accedi toohello [portale di Azure][Azure portal].</span><span class="sxs-lookup"><span data-stu-id="ae625-135">Sign in toohello [Azure portal][Azure portal].</span></span>
2. <span data-ttu-id="ae625-136">Nel riquadro sinistro hello selezionare **Sfoglia**, quindi selezionare **istanze di SQL Server**.</span><span class="sxs-lookup"><span data-stu-id="ae625-136">In hello left pane, select **Browse**, and then select **SQL servers**.</span></span>

    ![Selezionare Esplora > SQL Server](./media/sql-data-warehouse-restore-database-portal/01-browse-for-sql-server.png)
3. <span data-ttu-id="ae625-138">Trovare il server e selezionarlo.</span><span class="sxs-lookup"><span data-stu-id="ae625-138">Find your server, and then select it.</span></span>

    ![Selezionare il server](./media/sql-data-warehouse-restore-database-portal/02-select-server.png)
4. <span data-ttu-id="ae625-140">Scorrere verso il basso toohello **operazioni** sezione nel pannello del server.</span><span class="sxs-lookup"><span data-stu-id="ae625-140">Scroll down toohello **Operations** section on your server's blade.</span></span>
5. <span data-ttu-id="ae625-141">Seleziona hello **database eliminati** riquadro.</span><span class="sxs-lookup"><span data-stu-id="ae625-141">Select hello **Deleted databases** tile.</span></span>

    ![Selezionare hello eliminati database riquadro](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dws.png)
6. <span data-ttu-id="ae625-143">Selezionare il database di hello eliminato che si desidera toorestore.</span><span class="sxs-lookup"><span data-stu-id="ae625-143">Select hello deleted database that you want toorestore.</span></span>

    ![Selezionare un database toorestore](./media/sql-data-warehouse-restore-database-portal/02-select-deleted-dw.png)
7. <span data-ttu-id="ae625-145">Specificare un nuovo **nome database**.</span><span class="sxs-lookup"><span data-stu-id="ae625-145">Specify a new **Database name**.</span></span>

    ![Aggiungere un nome per il database hello](./media/sql-data-warehouse-restore-database-portal/02-restore-blade-from-deleted.png)
8. <span data-ttu-id="ae625-147">Selezionare **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae625-147">Select **OK**.</span></span>
9. <span data-ttu-id="ae625-148">processo di ripristino del database Hello verrà avviata ed è possibile utilizzare **notifiche** processo hello toomonitor.</span><span class="sxs-lookup"><span data-stu-id="ae625-148">hello database restore process will begin, and you can use **NOTIFICATIONS** toomonitor hello process.</span></span>

> [!NOTE]
> <span data-ttu-id="ae625-149">vedere il database al termine, il ripristino di hello tooconfigure [configura il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="ae625-149">tooconfigure your database after hello restore has finished, see [Configure your database after recovery][Configure your database after recovery].</span></span>
>
>

## <a name="next-steps"></a><span data-ttu-id="ae625-150">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="ae625-150">Next steps</span></span>
<span data-ttu-id="ae625-151">toolearn sulle funzionalità di continuità aziendale hello delle edizioni di Database SQL di Azure, leggere hello [Panoramica di continuità aziendale di Database SQL di Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="ae625-151">toolearn about hello business continuity features of Azure SQL Database editions, read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

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
