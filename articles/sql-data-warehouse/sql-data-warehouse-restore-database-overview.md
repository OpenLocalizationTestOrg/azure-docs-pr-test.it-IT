---
title: aaaRestore un Azure data warehouse - locale e con ridondanza geografica | Documenti Microsoft
description: Panoramica delle opzioni di ripristino di database di hello per il ripristino di un database in Azure SQL Data Warehouse.
services: sql-data-warehouse
documentationcenter: NA
author: Lakshmi1812
manager: jhubbard
editor: 
ms.assetid: 3e01c65c-6708-4fd7-82f5-4e1b5f61d304
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: backup-restore
ms.date: 10/31/2016
ms.author: lakshmir;barbkess
ms.openlocfilehash: a96b898372b29d420e1416ca93a172ff8af47fc7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 10/06/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="e344f-103">Ripristino di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e344f-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="e344f-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="e344f-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="e344f-105">[Portale][Portal]</span><span class="sxs-lookup"><span data-stu-id="e344f-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="e344f-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="e344f-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="e344f-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="e344f-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="e344f-108">SQL Data Warehouse offre ripristini locali e geografici come parte delle sue funzionalità di ripristino di emergenza del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="e344f-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="e344f-109">Utilizzare dati warehouse backup toorestore il ripristino di data warehouse tooa punto nell'area primaria hello oppure utilizzare l'area geografica diversa tooa backup con ridondanza geografica toorestore.</span><span class="sxs-lookup"><span data-stu-id="e344f-109">Use data warehouse backups toorestore your data warehouse tooa restore point in hello primary region, or use geo-redundant backups toorestore tooa different geographical region.</span></span> <span data-ttu-id="e344f-110">Questo articolo illustra le specifiche di hello del ripristino di un data warehouse.</span><span class="sxs-lookup"><span data-stu-id="e344f-110">This article explains hello specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="e344f-111">Cos'è un ripristino del data warehouse?</span><span class="sxs-lookup"><span data-stu-id="e344f-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="e344f-112">Un ripristino del data warehouse consiste in un nuovo data warehouse creato da un backup di un data warehouse esistente o eliminato.</span><span class="sxs-lookup"><span data-stu-id="e344f-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="e344f-113">warehouse di dati ripristinati Hello ricrea warehouse dati di backup hello in un momento specifico.</span><span class="sxs-lookup"><span data-stu-id="e344f-113">hello restored data warehouse re-creates hello backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="e344f-114">Poiché SQL Data Warehouse è un sistema distribuito, il ripristino del data warehouse viene creato da molti file di backup archiviati nei blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="e344f-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="e344f-115">Il ripristino del database è un elemento essenziale di qualsiasi strategia di continuità aziendale e di ripristino di emergenza perché ricrea i dati dopo un caso di danneggiamento o eliminazione accidentale.</span><span class="sxs-lookup"><span data-stu-id="e344f-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="e344f-116">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="e344f-116">For more information, see:</span></span>

* [<span data-ttu-id="e344f-117">Backup di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="e344f-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="e344f-118">Panoramica sulla continuità aziendale</span><span class="sxs-lookup"><span data-stu-id="e344f-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="e344f-119">Punti di ripristino del data warehouse</span><span class="sxs-lookup"><span data-stu-id="e344f-119">Data warehouse restore points</span></span>
<span data-ttu-id="e344f-120">Il vantaggio dell'utilizzo di archiviazione Premium di Azure SQL Data Warehouse utilizza il Blob di archiviazione di Azure degli snapshot toobackup hello primario del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="e344f-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots toobackup hello primary data warehouse.</span></span> <span data-ttu-id="e344f-121">Ogni snapshot è un punto di ripristino che rappresenta il tempo di hello snapshot hello avviato.</span><span class="sxs-lookup"><span data-stu-id="e344f-121">Each snapshot has a restore point that represents hello time hello snapshot started.</span></span> <span data-ttu-id="e344f-122">toorestore un data warehouse, scegliere un punto di ripristino e inviare un comando di ripristino.</span><span class="sxs-lookup"><span data-stu-id="e344f-122">toorestore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="e344f-123">SQL Data Warehouse viene sempre ripristinato hello tooa backup nuovo data warehouse.</span><span class="sxs-lookup"><span data-stu-id="e344f-123">SQL Data Warehouse always restores hello backup tooa new data warehouse.</span></span> <span data-ttu-id="e344f-124">È possibile mantenere hello ripristinato del data warehouse e hello corrente o eliminare uno di essi.</span><span class="sxs-lookup"><span data-stu-id="e344f-124">You can either keep hello restored data warehouse and hello current one, or delete one of them.</span></span> <span data-ttu-id="e344f-125">Se si desidera tooreplace hello corrente del data warehouse con hello ripristino del data warehouse, è possibile rinominarlo.</span><span class="sxs-lookup"><span data-stu-id="e344f-125">If you want tooreplace hello current data warehouse with hello restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="e344f-126">Se è necessario toorestore eliminate o in pausa data warehouse, è possibile [creare un ticket di supporto](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="e344f-126">If you need toorestore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore hello last available restore point.

Yes, for hello next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps hello data warehouse and its snapshots for seven days just in case you need hello data. After seven days, you won't be able toorestore tooany of hello restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="e344f-127">Ripristino con ridondanza geografica</span><span class="sxs-lookup"><span data-stu-id="e344f-127">Geo-redundant restore</span></span>
<span data-ttu-id="e344f-128">È possibile ripristinare l'area tooany warehouse di dati che supporta Azure SQL Data Warehouse con il livello di prestazioni scelto.</span><span class="sxs-lookup"><span data-stu-id="e344f-128">You can restore your data warehouse tooany region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="e344f-129">Si noti che DWU 9000 e 18000 non sono supportate in tutte le aree durante l'anteprima di hello.</span><span class="sxs-lookup"><span data-stu-id="e344f-129">Please note that 9000 and 18000 DWU are not supported in all regions during hello preview.</span></span>

> [!NOTE]
> <span data-ttu-id="e344f-130">ripristino di un con ridondanza geografica tooperform che è necessario non stata esplicitamente questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="e344f-130">tooperform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="e344f-131">Sequenza temporale del ripristino</span><span class="sxs-lookup"><span data-stu-id="e344f-131">Restore timeline</span></span>
<span data-ttu-id="e344f-132">È possibile ripristinare un punto di ripristino disponibile tooany di database all'interno di hello negli ultimi sette giorni.</span><span class="sxs-lookup"><span data-stu-id="e344f-132">You can restore a database tooany available restore point within hello last seven days.</span></span> <span data-ttu-id="e344f-133">Gli snapshot avviare ogni quattro ore tooeight e sono disponibili sette giorni.</span><span class="sxs-lookup"><span data-stu-id="e344f-133">Snapshots start every four tooeight hours and are available for seven days.</span></span> <span data-ttu-id="e344f-134">Quando uno snapshot supera i sette giorni di vita, scade e il relativo punto di ripristino non è più disponibile.</span><span class="sxs-lookup"><span data-stu-id="e344f-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="e344f-135">Costi di ripristino</span><span class="sxs-lookup"><span data-stu-id="e344f-135">Restore costs</span></span>
<span data-ttu-id="e344f-136">costi di archiviazione Hello per hello ripristinato data warehouse viene fatturato alla tariffa di archiviazione di Azure Premium hello.</span><span class="sxs-lookup"><span data-stu-id="e344f-136">hello storage charge for hello restored data warehouse is billed at hello Azure Premium Storage rate.</span></span> 

<span data-ttu-id="e344f-137">Se si sospende un ripristinato data warehouse, viene addebitata per l'archiviazione con frequenza di archiviazione di Azure Premium hello.</span><span class="sxs-lookup"><span data-stu-id="e344f-137">If you pause a restored data warehouse, you are charged for storage at hello Azure Premium Storage rate.</span></span> <span data-ttu-id="e344f-138">Il vantaggio di Hello della sospensione è che non vengono addebitate le risorse di elaborazione DWU hello.</span><span class="sxs-lookup"><span data-stu-id="e344f-138">hello advantage of pausing is you are not charged for hello DWU computing resources.</span></span>

<span data-ttu-id="e344f-139">Per altre informazioni sui prezzi di SQL Data Warehouse, vedere [Prezzi di SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="e344f-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="e344f-140">Usi della funzionalità di ripristino</span><span class="sxs-lookup"><span data-stu-id="e344f-140">Uses for restore</span></span>
<span data-ttu-id="e344f-141">uso principale Hello ripristino dei dati del warehouse è toorecover dati dopo la perdita di dati accidentali.</span><span class="sxs-lookup"><span data-stu-id="e344f-141">hello primary use for data warehouse restore is toorecover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="e344f-142">Inoltre, è possibile utilizzare dati warehouse ripristino tooretain una copia di backup per più di sette giorni.</span><span class="sxs-lookup"><span data-stu-id="e344f-142">You can also use data warehouse restore tooretain a backup for longer than seven days.</span></span> <span data-ttu-id="e344f-143">Una volta ripristinato il backup di hello, in base a cui si dispone di data warehouse di hello online e possibile sospenderla indefinitamente toosave calcolo dei costi.</span><span class="sxs-lookup"><span data-stu-id="e344f-143">Once hello backup is restored, you have hello data warehouse online and can pause it indefinitely toosave compute costs.</span></span> <span data-ttu-id="e344f-144">database sospeso Hello comporta costi di archiviazione con frequenza di archiviazione di Azure Premium hello.</span><span class="sxs-lookup"><span data-stu-id="e344f-144">hello paused database incurs storage charges at hello Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="e344f-145">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="e344f-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="e344f-146">Scenari</span><span class="sxs-lookup"><span data-stu-id="e344f-146">Scenarios</span></span>
* <span data-ttu-id="e344f-147">Per una panoramica sulla continuità aziendale, vedere [Panoramica sulla continuità aziendale](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="e344f-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="e344f-148">tooperform un data warehouse di ripristino, eseguire il ripristino utilizzando:</span><span class="sxs-lookup"><span data-stu-id="e344f-148">tooperform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="e344f-149">Azure portale, vedere [ripristino configurazione di un data warehouse utilizzando hello portale di Azure](sql-data-warehouse-restore-database-portal.md)</span><span class="sxs-lookup"><span data-stu-id="e344f-149">Azure portal, see [Restore a data warehouse using hello Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="e344f-150">Cmdlet di PowerShell )vedere [Ripristinare un data warehouse con i cmdlet di PowerShell](sql-data-warehouse-restore-database-powershell.md))</span><span class="sxs-lookup"><span data-stu-id="e344f-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="e344f-151">API REST, vedere [ripristino configurazione di un data warehouse utilizzando le API REST hello](sql-data-warehouse-restore-database-rest-api.md)</span><span class="sxs-lookup"><span data-stu-id="e344f-151">REST APIs, see [Restore a data warehouse using hello REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

<!-- ### Tutorials -->

<!--Image references-->

<!--Article references-->
[Azure SQL Database business continuity overview]: ../sql-database/sql-database-business-continuity.md
[Overview]: ./sql-data-warehouse-restore-database-overview.md
[Portal]: ./sql-data-warehouse-restore-database-portal.md
[PowerShell]: ./sql-data-warehouse-restore-database-powershell.md
[REST]: ./sql-data-warehouse-restore-database-rest-api.md

<!--MSDN references-->


<!--Other Web references-->
