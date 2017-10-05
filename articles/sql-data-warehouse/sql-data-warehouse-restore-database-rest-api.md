---
title: Ripristinare un'istanza di Azure SQL Data Warehouse (API REST) | Microsoft Docs
description: "Attività dell'API REST per il ripristino di un'istanza di Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: fca922c6-b675-49c7-907e-5dcf26d451dd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: 8656607611e7518e42b51b91774f55abec15c228
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 07/11/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="fa685-103">Ripristinare un'istanza di Azure SQL Data Warehouse (API REST)</span><span class="sxs-lookup"><span data-stu-id="fa685-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="fa685-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="fa685-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="fa685-105">[Portale][Portal]</span><span class="sxs-lookup"><span data-stu-id="fa685-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="fa685-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="fa685-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="fa685-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="fa685-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="fa685-108">Questo articolo illustra come ripristinare un'istanza di Azure SQL Data Warehouse usando l'API REST.</span><span class="sxs-lookup"><span data-stu-id="fa685-108">In this article you will learn how to restore an Azure SQL Data Warehouse using the REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fa685-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="fa685-109">Before you begin</span></span>
<span data-ttu-id="fa685-110">**Verificare la capacità in DTU.**</span><span class="sxs-lookup"><span data-stu-id="fa685-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="fa685-111">Ogni SQL Data Warehouse è ospitato in un server SQL (ad esempio mioserver.database.windows.net), che ha una quota DTU predefinita.</span><span class="sxs-lookup"><span data-stu-id="fa685-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="fa685-112">Per poter ripristinare un SQL Data Warehouse, verificare che la quota DTU rimanente nell'istanza del server SQL sia sufficiente per il database da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="fa685-112">Before you can restore a SQL Data Warehouse, verify that the your SQL server has enough remaining DTU quota for the database being restored.</span></span> <span data-ttu-id="fa685-113">Per informazioni su come calcolare la DTU necessaria o per richiedere altre DTU, vedere come [richiedere una modifica della quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="fa685-113">To learn how to calculate DTU needed or to request more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="fa685-114">Ripristinare un database attivo o sospeso</span><span class="sxs-lookup"><span data-stu-id="fa685-114">Restore an active or paused database</span></span>
<span data-ttu-id="fa685-115">Per ripristinare un database:</span><span class="sxs-lookup"><span data-stu-id="fa685-115">To restore a database:</span></span>

1. <span data-ttu-id="fa685-116">Ottenere l'elenco dei punti di ripristino del database utilizzando l'operazione Get Database Restore Points.</span><span class="sxs-lookup"><span data-stu-id="fa685-116">Get the list of database restore points using the Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="fa685-117">Iniziare il ripristino usando l'operazione [Create database restore request][Create database restore request].</span><span class="sxs-lookup"><span data-stu-id="fa685-117">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="fa685-118">Monitorare lo stato del ripristino tramite l'operazione [Database Operation Status][Database operation status].</span><span class="sxs-lookup"><span data-stu-id="fa685-118">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="fa685-119">Al termine del ripristino sarà possibile configurare il database ripristinato seguendo le istruzioni disponibili in [Configurare il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="fa685-119">After the restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="fa685-120">Ripristino di un database eliminato</span><span class="sxs-lookup"><span data-stu-id="fa685-120">Restore a deleted database</span></span>
<span data-ttu-id="fa685-121">Per ripristinare un database eliminato:</span><span class="sxs-lookup"><span data-stu-id="fa685-121">To restore a deleted database:</span></span>

1. <span data-ttu-id="fa685-122">Elencare tutti i database eliminati ripristinabili tramite l'operazione [List Restorable Dropped Databases][List restorable dropped databases].</span><span class="sxs-lookup"><span data-stu-id="fa685-122">List all of your restorable deleted databases by using the [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="fa685-123">Ottenere i dettagli del database eliminato da ripristinare tramite l'operazione [Get Restorable Dropped Database][Get restorable dropped database].</span><span class="sxs-lookup"><span data-stu-id="fa685-123">Get the details for the deleted database you want to restore by using the [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="fa685-124">Iniziare il ripristino usando l'operazione [Create database restore request][Create database restore request].</span><span class="sxs-lookup"><span data-stu-id="fa685-124">Begin your restore by using the [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="fa685-125">Monitorare lo stato del ripristino tramite l'operazione [Database Operation Status][Database operation status].</span><span class="sxs-lookup"><span data-stu-id="fa685-125">Track the status of your restore by using the [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="fa685-126">Per configurare il database al termine del ripristino, vedere [Configurare il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="fa685-126">To configure your database after the restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="fa685-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="fa685-127">Next steps</span></span>
<span data-ttu-id="fa685-128">Per altre informazioni sulle funzionalità di continuità aziendale delle edizioni del database SQL di Azure, vedere [Panoramica sulla continuità aziendale del database SQL di Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="fa685-128">To learn about the business continuity features of Azure SQL Database editions, please read the [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How to install and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->
[Create database restore request]: https://msdn.microsoft.com/library/azure/dn509571.aspx
[Database operation status]: https://msdn.microsoft.com/library/azure/dn720371.aspx
[Get restorable dropped database]: https://msdn.microsoft.com/library/azure/dn509574.aspx
[List restorable dropped databases]: https://msdn.microsoft.com/library/azure/dn509562.aspx
[Restore-AzureRmSqlDatabase]: https://msdn.microsoft.com/library/mt693390.aspx

<!--Other Web references-->
[Azure Portal]: https://portal.azure.com/
[Microsoft Web Platform Installer]: https://aka.ms/webpi-azps
