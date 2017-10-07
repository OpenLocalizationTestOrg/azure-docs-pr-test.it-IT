---
title: aaaRestore un Azure SQL Data Warehouse (API REST) | Documenti Microsoft
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
ms.openlocfilehash: cf6678d71aafff71b1ea715f447e41e25f20d1b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="restore-an-azure-sql-data-warehouse-rest-api"></a><span data-ttu-id="0665d-103">Ripristinare un'istanza di Azure SQL Data Warehouse (API REST)</span><span class="sxs-lookup"><span data-stu-id="0665d-103">Restore an Azure SQL Data Warehouse (REST API)</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="0665d-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="0665d-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="0665d-105">[Portale][Portal]</span><span class="sxs-lookup"><span data-stu-id="0665d-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="0665d-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="0665d-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="0665d-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="0665d-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="0665d-108">In questo articolo si apprenderà come toorestore un Azure SQL Data Warehouse utilizzando hello API REST.</span><span class="sxs-lookup"><span data-stu-id="0665d-108">In this article you will learn how toorestore an Azure SQL Data Warehouse using hello REST API.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0665d-109">Prima di iniziare</span><span class="sxs-lookup"><span data-stu-id="0665d-109">Before you begin</span></span>
<span data-ttu-id="0665d-110">**Verificare la capacità in DTU.**</span><span class="sxs-lookup"><span data-stu-id="0665d-110">**Verify your DTU capacity.**</span></span> <span data-ttu-id="0665d-111">Ogni SQL Data Warehouse è ospitato in un server SQL (ad esempio mioserver.database.windows.net), che ha una quota DTU predefinita.</span><span class="sxs-lookup"><span data-stu-id="0665d-111">Each SQL Data Warehouse is hosted by a SQL server (e.g. myserver.database.windows.net) which has a default DTU quota.</span></span>  <span data-ttu-id="0665d-112">Prima di poter ripristinare un SQL Data Warehouse, verificare che hello che di SQL server è sufficientemente rimanente quota DTU per database hello da ripristinare.</span><span class="sxs-lookup"><span data-stu-id="0665d-112">Before you can restore a SQL Data Warehouse, verify that hello your SQL server has enough remaining DTU quota for hello database being restored.</span></span> <span data-ttu-id="0665d-113">toolearn come toocalculate DTU necessarie o toorequest più DTU, vedere [richiedere una modifica della quota DTU][Request a DTU quota change].</span><span class="sxs-lookup"><span data-stu-id="0665d-113">toolearn how toocalculate DTU needed or toorequest more DTU, see [Request a DTU quota change][Request a DTU quota change].</span></span>

## <a name="restore-an-active-or-paused-database"></a><span data-ttu-id="0665d-114">Ripristinare un database attivo o sospeso</span><span class="sxs-lookup"><span data-stu-id="0665d-114">Restore an active or paused database</span></span>
<span data-ttu-id="0665d-115">toorestore un database:</span><span class="sxs-lookup"><span data-stu-id="0665d-115">toorestore a database:</span></span>

1. <span data-ttu-id="0665d-116">Ottenere l'elenco di hello dei punti di ripristino di database tramite l'operazione Get punti di ripristino di Database hello.</span><span class="sxs-lookup"><span data-stu-id="0665d-116">Get hello list of database restore points using hello Get Database Restore Points operation.</span></span>
2. <span data-ttu-id="0665d-117">Iniziare il ripristino utilizzando hello [richiesta di ripristino di database crea] [ Create database restore request] operazione.</span><span class="sxs-lookup"><span data-stu-id="0665d-117">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
3. <span data-ttu-id="0665d-118">Tenere traccia dello stato di hello del ripristino utilizzando hello [dello stato dell'operazione di Database] [ Database operation status] operazione.</span><span class="sxs-lookup"><span data-stu-id="0665d-118">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="0665d-119">Al termine del ripristino di hello, è possibile configurare il database ripristinato seguendo [configura il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="0665d-119">After hello restore has completed, you can configure your recovered database by following [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="restore-a-deleted-database"></a><span data-ttu-id="0665d-120">Ripristino di un database eliminato</span><span class="sxs-lookup"><span data-stu-id="0665d-120">Restore a deleted database</span></span>
<span data-ttu-id="0665d-121">un database eliminato toorestore:</span><span class="sxs-lookup"><span data-stu-id="0665d-121">toorestore a deleted database:</span></span>

1. <span data-ttu-id="0665d-122">Elencare tutti i database eliminati ripristinabili utilizzando hello [elenco ripristinabile eliminati database] [ List restorable dropped databases] operazione.</span><span class="sxs-lookup"><span data-stu-id="0665d-122">List all of your restorable deleted databases by using hello [List restorable dropped databases][List restorable dropped databases] operation.</span></span>
2. <span data-ttu-id="0665d-123">Ottenere i dettagli di hello per database hello eliminato da toorestore utilizzando hello [Get restorable eliminati database] [ Get restorable dropped database] operazione.</span><span class="sxs-lookup"><span data-stu-id="0665d-123">Get hello details for hello deleted database you want toorestore by using hello [Get restorable dropped database][Get restorable dropped database] operation.</span></span>
3. <span data-ttu-id="0665d-124">Iniziare il ripristino utilizzando hello [richiesta di ripristino di database crea] [ Create database restore request] operazione.</span><span class="sxs-lookup"><span data-stu-id="0665d-124">Begin your restore by using hello [Create database restore request][Create database restore request] operation.</span></span>
4. <span data-ttu-id="0665d-125">Tenere traccia dello stato di hello del ripristino utilizzando hello [dello stato dell'operazione di Database] [ Database operation status] operazione.</span><span class="sxs-lookup"><span data-stu-id="0665d-125">Track hello status of your restore by using hello [Database operation status][Database operation status] operation.</span></span>

> [!NOTE]
> <span data-ttu-id="0665d-126">vedere il database al termine del ripristino di hello, tooconfigure [configura il database dopo il ripristino][Configure your database after recovery].</span><span class="sxs-lookup"><span data-stu-id="0665d-126">tooconfigure your database after hello restore has completed, see [Configure your database after recovery][Configure your database after recovery].</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="0665d-127">Passaggi successivi</span><span class="sxs-lookup"><span data-stu-id="0665d-127">Next steps</span></span>
<span data-ttu-id="0665d-128">toolearn sulle funzionalità di continuità aziendale hello delle edizioni di Database SQL di Azure, leggere hello [Panoramica di continuità aziendale di Database SQL di Azure][Azure SQL Database business continuity overview].</span><span class="sxs-lookup"><span data-stu-id="0665d-128">toolearn about hello business continuity features of Azure SQL Database editions, please read hello [Azure SQL Database business continuity overview][Azure SQL Database business continuity overview].</span></span>

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Request a DTU quota change]: ./sql-data-warehouse-get-started-create-support-ticket.md#request-quota-change
[Configure your database after recovery]: ../sql-database/sql-database-disaster-recovery.md#configure-your-database-after-recovery
[How tooinstall and configure Azure PowerShell]: /powershell/azureps-cmdlets-docs
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
