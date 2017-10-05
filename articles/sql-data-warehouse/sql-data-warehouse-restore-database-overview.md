---
title: Ripristinare un'istanza di Azure Data Warehouse - Ridondanza geografica e locale | Documentazione Microsoft
description: Panoramica delle opzioni di ripristino del database per ripristinare un database in Azure SQL Data Warehouse.
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
ms.openlocfilehash: ea42b7135d0695b66d569095e70bb3d9f8b9594b
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: it-IT
ms.lasthandoff: 08/03/2017
---
# <a name="sql-data-warehouse-restore"></a><span data-ttu-id="baeb7-103">Ripristino di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="baeb7-103">SQL Data Warehouse restore</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="baeb7-104">[Panoramica][Overview]</span><span class="sxs-lookup"><span data-stu-id="baeb7-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="baeb7-105">[Portale][Portal]</span><span class="sxs-lookup"><span data-stu-id="baeb7-105">[Portal][Portal]</span></span>
> * <span data-ttu-id="baeb7-106">[PowerShell][PowerShell]</span><span class="sxs-lookup"><span data-stu-id="baeb7-106">[PowerShell][PowerShell]</span></span>
> * <span data-ttu-id="baeb7-107">[REST][REST]</span><span class="sxs-lookup"><span data-stu-id="baeb7-107">[REST][REST]</span></span>
> 
> 

<span data-ttu-id="baeb7-108">SQL Data Warehouse offre ripristini locali e geografici come parte delle sue funzionalità di ripristino di emergenza del data warehouse.</span><span class="sxs-lookup"><span data-stu-id="baeb7-108">SQL Data Warehouse offers both local and geographical restores as part of its data warehouse disaster recovery capabilities.</span></span> <span data-ttu-id="baeb7-109">È possibile i backup del dati warehouse per ripristinare il data warehouse a un punto di ripristino nell'area primaria o usare i backup con ridondanza geografica per ripristinarlo a un'area geografica diversa.</span><span class="sxs-lookup"><span data-stu-id="baeb7-109">Use data warehouse backups to restore your data warehouse to a restore point in the primary region, or use geo-redundant backups to restore to a different geographical region.</span></span> <span data-ttu-id="baeb7-110">Questo articolo illustra le specifiche del ripristino di un data warehouse.</span><span class="sxs-lookup"><span data-stu-id="baeb7-110">This article explains the specifics of restoring a data warehouse.</span></span>

## <a name="what-is-a-data-warehouse-restore"></a><span data-ttu-id="baeb7-111">Cos'è un ripristino del data warehouse?</span><span class="sxs-lookup"><span data-stu-id="baeb7-111">What is a data warehouse restore?</span></span>
<span data-ttu-id="baeb7-112">Un ripristino del data warehouse consiste in un nuovo data warehouse creato da un backup di un data warehouse esistente o eliminato.</span><span class="sxs-lookup"><span data-stu-id="baeb7-112">A data warehouse restore is a new data warehouse that is created from a backup of an existing or deleted data warehouse.</span></span> <span data-ttu-id="baeb7-113">Il data warehouse ripristinato ricrea il data warehouse di backup in un momento specifico.</span><span class="sxs-lookup"><span data-stu-id="baeb7-113">The restored data warehouse re-creates the backed-up data warehouse at a specific time.</span></span> <span data-ttu-id="baeb7-114">Poiché SQL Data Warehouse è un sistema distribuito, il ripristino del data warehouse viene creato da molti file di backup archiviati nei blob di Azure.</span><span class="sxs-lookup"><span data-stu-id="baeb7-114">Since SQL Data Warehouse is a distributed system, a data warehouse restore is created from many backup files that are stored in Azure blobs.</span></span> 

<span data-ttu-id="baeb7-115">Il ripristino del database è un elemento essenziale di qualsiasi strategia di continuità aziendale e di ripristino di emergenza perché ricrea i dati dopo un caso di danneggiamento o eliminazione accidentale.</span><span class="sxs-lookup"><span data-stu-id="baeb7-115">Database restore is an essential part of any business continuity and disaster recovery strategy because it re-creates your data after accidental corruption or deletion.</span></span>

<span data-ttu-id="baeb7-116">Per altre informazioni, vedere:</span><span class="sxs-lookup"><span data-stu-id="baeb7-116">For more information, see:</span></span>

* [<span data-ttu-id="baeb7-117">Backup di SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="baeb7-117">SQL Data Warehouse backups</span></span>](sql-data-warehouse-backups.md)
* [<span data-ttu-id="baeb7-118">Panoramica sulla continuità aziendale</span><span class="sxs-lookup"><span data-stu-id="baeb7-118">Business continuity overview</span></span>](../sql-database/sql-database-business-continuity.md)

## <a name="data-warehouse-restore-points"></a><span data-ttu-id="baeb7-119">Punti di ripristino del data warehouse</span><span class="sxs-lookup"><span data-stu-id="baeb7-119">Data warehouse restore points</span></span>
<span data-ttu-id="baeb7-120">Come vantaggio dell'uso di Archiviazione Premium di Azure, SQL Data Warehouse usa gli snapshot dei BLOB di Archiviazione di Azure per eseguire il backup del data warehouse primario.</span><span class="sxs-lookup"><span data-stu-id="baeb7-120">As a benefit of using Azure Premium Storage, SQL Data Warehouse uses Azure Storage Blob snapshots to backup the primary data warehouse.</span></span> <span data-ttu-id="baeb7-121">Ogni snapshot ha un punto di ripristino che rappresenta l'ora di inizio dello snapshot.</span><span class="sxs-lookup"><span data-stu-id="baeb7-121">Each snapshot has a restore point that represents the time the snapshot started.</span></span> <span data-ttu-id="baeb7-122">Per ripristinare un data warehouse, scegliere un punto di ripristino ed eseguire un comando di ripristino.</span><span class="sxs-lookup"><span data-stu-id="baeb7-122">To restore a data warehouse, you choose a restore point and issue a restore command.</span></span>  

<span data-ttu-id="baeb7-123">SQL Data Warehouse ripristina sempre il backup in un nuovo data warehouse.</span><span class="sxs-lookup"><span data-stu-id="baeb7-123">SQL Data Warehouse always restores the backup to a new data warehouse.</span></span> <span data-ttu-id="baeb7-124">È possibile mantenere il data warehouse ripristinato e quello corrente, oppure eliminare uno di questi.</span><span class="sxs-lookup"><span data-stu-id="baeb7-124">You can either keep the restored data warehouse and the current one, or delete one of them.</span></span> <span data-ttu-id="baeb7-125">Se si desidera sostituire il data warehouse corrente con il data warehouse ripristinato, è possibile rinominarlo.</span><span class="sxs-lookup"><span data-stu-id="baeb7-125">If you want to replace the current data warehouse with the restored data warehouse, you can rename it.</span></span>

<span data-ttu-id="baeb7-126">Se è necessario ripristinare un data warehouse eliminate o messo in pausa, è possibile [creare un ticket di supporto](sql-data-warehouse-get-started-create-support-ticket.md).</span><span class="sxs-lookup"><span data-stu-id="baeb7-126">If you need to restore a deleted or paused data warehouse, you can [create a support ticket](sql-data-warehouse-get-started-create-support-ticket.md).</span></span> 

<!-- 
### Can I restore a deleted data warehouse?

Yes, you can restore the last available restore point.

Yes, for the next seven calendar days. When you delete a data warehouse, SQL Data Warehouse actually keeps the data warehouse and its snapshots for seven days just in case you need the data. After seven days, you won't be able to restore to any of the restore points. -->

## <a name="geo-redundant-restore"></a><span data-ttu-id="baeb7-127">Ripristino con ridondanza geografica</span><span class="sxs-lookup"><span data-stu-id="baeb7-127">Geo-redundant restore</span></span>
<span data-ttu-id="baeb7-128">È possibile ripristinare il data warehouse in qualsiasi area che supporta Azure SQL Data Warehouse con il livello di prestazioni scelto.</span><span class="sxs-lookup"><span data-stu-id="baeb7-128">You can restore your data warehouse to any region supporting Azure SQL Data Warehouse at your chosen performance level.</span></span> <span data-ttu-id="baeb7-129">Si noti che le capacità DWU 9000 e 18000 non sono supportate in tutte le aree durante l'anteprima.</span><span class="sxs-lookup"><span data-stu-id="baeb7-129">Please note that 9000 and 18000 DWU are not supported in all regions during the preview.</span></span>

> [!NOTE]
> <span data-ttu-id="baeb7-130">Per eseguire un ripristino con ridondanza geografica, è necessario non avere rifiutato esplicitamente questa funzionalità.</span><span class="sxs-lookup"><span data-stu-id="baeb7-130">To perform a geo-redundant restore you must not have opted out of this feature.</span></span>
> 
> 

## <a name="restore-timeline"></a><span data-ttu-id="baeb7-131">Sequenza temporale del ripristino</span><span class="sxs-lookup"><span data-stu-id="baeb7-131">Restore timeline</span></span>
<span data-ttu-id="baeb7-132">È possibile ripristinare un database a qualsiasi punto di ripristino disponibile degli ultimi sette giorni.</span><span class="sxs-lookup"><span data-stu-id="baeb7-132">You can restore a database to any available restore point within the last seven days.</span></span> <span data-ttu-id="baeb7-133">Gli snapshot vengono eseguiti ogni quattro-otto ore e sono disponibili per sette giorni.</span><span class="sxs-lookup"><span data-stu-id="baeb7-133">Snapshots start every four to eight hours and are available for seven days.</span></span> <span data-ttu-id="baeb7-134">Quando uno snapshot supera i sette giorni di vita, scade e il relativo punto di ripristino non è più disponibile.</span><span class="sxs-lookup"><span data-stu-id="baeb7-134">When a snapshot is older than seven days, it expires and its restore point is no longer available.</span></span>

## <a name="restore-costs"></a><span data-ttu-id="baeb7-135">Costi di ripristino</span><span class="sxs-lookup"><span data-stu-id="baeb7-135">Restore costs</span></span>
<span data-ttu-id="baeb7-136">Il costo di archiviazione per il data warehouse ripristinato viene fatturato alla tariffa di archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="baeb7-136">The storage charge for the restored data warehouse is billed at the Azure Premium Storage rate.</span></span> 

<span data-ttu-id="baeb7-137">Se si mette in pausa un data warehouse ripristinato, l'archiviazione viene fatturata alla tariffa di archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="baeb7-137">If you pause a restored data warehouse, you are charged for storage at the Azure Premium Storage rate.</span></span> <span data-ttu-id="baeb7-138">Il vantaggio con la messa in pausa è che le risorse di elaborazione DWU non vengono fatturate.</span><span class="sxs-lookup"><span data-stu-id="baeb7-138">The advantage of pausing is you are not charged for the DWU computing resources.</span></span>

<span data-ttu-id="baeb7-139">Per altre informazioni sui prezzi di SQL Data Warehouse, vedere [Prezzi di SQL Data Warehouse](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span><span class="sxs-lookup"><span data-stu-id="baeb7-139">For more information about SQL Data Warehouse pricing, see [SQL Data Warehouse Pricing](https://azure.microsoft.com/pricing/details/sql-data-warehouse/).</span></span>

## <a name="uses-for-restore"></a><span data-ttu-id="baeb7-140">Usi della funzionalità di ripristino</span><span class="sxs-lookup"><span data-stu-id="baeb7-140">Uses for restore</span></span>
<span data-ttu-id="baeb7-141">L'uso primario per il ripristino del data warehouse consiste nel recuperare i dati dopo averli perduti o danneggiati accidentalmente.</span><span class="sxs-lookup"><span data-stu-id="baeb7-141">The primary use for data warehouse restore is to recover data after accidental data loss or corruption.</span></span>

<span data-ttu-id="baeb7-142">Inoltre, è possibile usare la funzionalità di ripristino del data warehouse per conservare una copia di backup per più di sette giorni.</span><span class="sxs-lookup"><span data-stu-id="baeb7-142">You can also use data warehouse restore to retain a backup for longer than seven days.</span></span> <span data-ttu-id="baeb7-143">Dopo aver ripristinato la copia di backup, il data warehouse diventa disponibile online e può essere messo in pausa per un periodo imprecisato al fine di risparmiare sui costi.</span><span class="sxs-lookup"><span data-stu-id="baeb7-143">Once the backup is restored, you have the data warehouse online and can pause it indefinitely to save compute costs.</span></span> <span data-ttu-id="baeb7-144">Il database messo in pausa comporta costi di archiviazione alla frequenza dell'archiviazione Premium di Azure.</span><span class="sxs-lookup"><span data-stu-id="baeb7-144">The paused database incurs storage charges at the Azure Premium Storage rate.</span></span> 

## <a name="related-topics"></a><span data-ttu-id="baeb7-145">Argomenti correlati</span><span class="sxs-lookup"><span data-stu-id="baeb7-145">Related topics</span></span>
### <a name="scenarios"></a><span data-ttu-id="baeb7-146">Scenari</span><span class="sxs-lookup"><span data-stu-id="baeb7-146">Scenarios</span></span>
* <span data-ttu-id="baeb7-147">Per una panoramica sulla continuità aziendale, vedere [Panoramica sulla continuità aziendale](../sql-database/sql-database-business-continuity.md)</span><span class="sxs-lookup"><span data-stu-id="baeb7-147">For a business continuity overview, see [Business continuity overview](../sql-database/sql-database-business-continuity.md)</span></span>

<!-- ### Tasks -->

<span data-ttu-id="baeb7-148">Per eseguire il ripristino di un data warehouse, eseguire il ripristino con:</span><span class="sxs-lookup"><span data-stu-id="baeb7-148">To perform a data warehouse restore, restore using:</span></span>

* <span data-ttu-id="baeb7-149">Portale di Azure (vedere [Ripristinare un data warehouse con il portale di Azure](sql-data-warehouse-restore-database-portal.md))</span><span class="sxs-lookup"><span data-stu-id="baeb7-149">Azure portal, see [Restore a data warehouse using the Azure portal](sql-data-warehouse-restore-database-portal.md)</span></span>
* <span data-ttu-id="baeb7-150">Cmdlet di PowerShell )vedere [Ripristinare un data warehouse con i cmdlet di PowerShell](sql-data-warehouse-restore-database-powershell.md))</span><span class="sxs-lookup"><span data-stu-id="baeb7-150">PowerShell cmdlets, see [Restore a data warehouse using PowerShell cmdlets](sql-data-warehouse-restore-database-powershell.md)</span></span>
* <span data-ttu-id="baeb7-151">API REST (vedere [Ripristinare un data warehouse con le API REST](sql-data-warehouse-restore-database-rest-api.md))</span><span class="sxs-lookup"><span data-stu-id="baeb7-151">REST APIs, see [Restore a data warehouse using the REST APIs](sql-data-warehouse-restore-database-rest-api.md)</span></span>

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
